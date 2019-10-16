---
title: NuGet platformlar arası eklentiler
description: NuGet. exe, DotNet. exe, MSBuild. exe ve Visual Studio için NuGet platformlar arası eklentileri
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380496"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet platformlar arası eklentiler

NuGet 4.8 + platformlar arası eklentiler için destek eklendi.
Bu, bir işlem kuralları kümesine uyması gereken yeni bir eklenti genişletilebilirlik modeli oluşturarak ile elde edildi.
Eklentiler, NuGet Istemcilerinin ayrı bir işlemde başlatması için kendi içinde bulunan yürütülebilir dosya (.NET Core World ' te çalıştırılabilir).
Bu bir kez doğru yazma, her yerde çalışan eklenti. Bu, tüm NuGet istemci araçlarıyla çalışır.
Eklentiler .NET Framework (NuGet. exe, MSBuild. exe ve Visual Studio) ya da .NET Core (DotNet. exe) olabilir.
NuGet Istemcisi ve eklentisi arasındaki sürümlü bir iletişim protokolü tanımlanmıştır. Başlangıç el sıkışması sırasında, 2 işlem protokol sürümü üzerinde anlaşacak.

Tüm NuGet istemci araçları senaryolarını kapsayacak şekilde, bunlardan biri hem .NET Framework hem de .NET Core eklentisine gerek duyar.
Aşağıda, eklentilerin istemci/çerçeve birleşimleri açıklanmıştır.

| İstemci aracı  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| DotNet. exe | .NET Core |
| NuGet. exe | .NET Framework |
| MSBuild. exe | .NET Framework |
| Mono üzerinde NuGet. exe | .NET Framework |

## <a name="how-does-it-work"></a>Nasıl çalışır?

Üst düzey iş akışı aşağıdaki gibi açıklanabilir:

1. NuGet kullanılabilir eklentileri bulur.
1. Uygun olduğunda NuGet, eklentileri öncelik sırasıyla yineleyebilir ve tek tek başlatır.
1. NuGet, isteğe hizmet veren ilk eklentiyi kullanacaktır.
1. Eklentiler artık gerekli olmadığında kapatılacak.

## <a name="general-plugin-requirements"></a>Genel eklenti gereksinimleri

Geçerli protokol sürümü *2.0.0*.
Bu sürüm altında, gereksinimler aşağıdaki gibidir:

- Windows ve mono üzerinde çalışacak geçerli, güvenilir bir Authenticode imza Derlemeleriyle aynı. Henüz Linux ve Mac üzerinde çalıştırılan derlemeler için özel bir güven gereksinimi yoktur. [İlgili sorun](https://github.com/NuGet/Home/issues/6702)
- NuGet istemci araçlarının geçerli güvenlik bağlamı altında durum bilgisiz başlatma desteği. Örneğin, NuGet istemci araçları daha sonra açıklanan eklenti protokolünün dışında yükseltme veya ek başlatma gerçekleştirmeyecektir.
- Açıkça belirtilmediği takdirde etkileşimli değil.
- Anlaşmalı eklenti Protokolü sürümüne bağlı olarak.
- Makul bir zaman dönemi içindeki tüm isteklere yanıt verir.
- Devam eden tüm işlemler için iptal isteklerini dikkate alarak.

Teknik belirtim aşağıdaki özelliklere göre daha ayrıntılı olarak açıklanmıştır:

- [NuGet paketi Indirme eklentisi](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet çapraz Plat kimlik doğrulama eklentisi](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>İstemci-eklentisi etkileşimi

NuGet istemci araçları ve eklentileri, JSON ile standart akışlar (stdin, stdout, stderr) üzerinden iletişim kurar. Tüm veriler UTF-8 kodlu olmalıdır.
Eklentiler "-Plugin" bağımsız değişkeniyle başlatılır. Bir Kullanıcı bu bağımsız değişken olmadan bir eklenti yürütülebiliri doğrudan başlattığında, eklenti bir protokol el sıkışması için beklemek yerine bilgilendirici bir ileti verebilir.
Protokol el sıkışma zaman aşımı 5 saniyedir. Eklenti, kurulumu olabildiğince kısa bir süre içinde tamamlamalıdır.
NuGet istemci araçları, bir NuGet kaynağı için hizmet dizinini geçirerek bir eklentinin desteklenen işlemlerini sorgular. Bir eklenti desteklenen hizmet türlerinin varlığını denetlemek için hizmet dizinini kullanabilir.

NuGet istemci araçları ve eklentisi arasındaki iletişim çift yönlüdür. Her istekte 5 saniyelik bir zaman aşımı vardır. İşlemlerin daha uzun sürme olması gerekiyorsa, isteğin zaman aşımına uğramasını engellemek için ilgili işlemin bir ilerleme iletisi göndermesi gerekir. 1 dakika sonra bir eklenti boşta kabul edilir ve kapatılır.

## <a name="plugin-installation-and-discovery"></a>Eklenti yükleme ve bulma

Eklentiler, kural tabanlı bir dizin yapısı aracılığıyla keşfedilir.
CI/CD senaryoları ve Power Users, davranışı geçersiz kılmak için ortam değişkenlerini kullanabilir. Ortam değişkenlerini kullanırken yalnızca mutlak yollara izin verilir. @No__t-0 ve `NUGET_NETCORE_PLUGIN_PATHS` ' in yalnızca NuGet araçları 'nın ve sonraki sürümlerin 5.3 + sürümü ile kullanılabildiğini unutmayın.

- `NUGET_NETFX_PLUGIN_PATHS`-.NET Framework tabanlı araç (NuGet. exe/MSBuild. exe/Visual Studio) tarafından kullanılacak eklentileri tanımlar. @No__t-0 ' a kadar önceliklidir. (Yalnızca NuGet sürümü 5.3 +)
- `NUGET_NETCORE_PLUGIN_PATHS`-.NET Core tabanlı araç (DotNet. exe) tarafından kullanılacak eklentileri tanımlar. @No__t-0 ' a kadar önceliklidir. (Yalnızca NuGet sürümü 5.3 +)
- `NUGET_PLUGIN_PATHS`-bu NuGet işlemi için kullanılacak eklentileri tanımlar, öncelik korunur. Bu ortam değişkeni ayarlandıysa, kural tabanlı bulmayı geçersiz kılar. Çerçeveye özgü değişkenlerden biri belirtilmişse yok sayılır.
-  @No__t-0 ' daki NuGet giriş konumu Kullanıcı konumu. Bu konum geçersiz kılınamaz. .NET Core ve .NET Framework eklentileri için farklı bir kök dizin kullanılır.

| Framework | Kök bulma konumu  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Her eklenti kendi klasörüne yüklenmelidir.
Eklenti giriş noktası, yüklü klasörün adı, .NET Core için. dll uzantıları ve .NET Framework için. exe uzantısı olur.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Şu anda eklentilerin yüklenmesi için Kullanıcı hikayesi yok. Gerekli dosyaları önceden belirlenmiş konuma taşımak basittir.

## <a name="supported-operations"></a>Desteklenen işlemler

Yeni eklenti Protokolü altında iki işlem desteklenir.

| İşlem adı | En düşük protokol sürümü | En düşük NuGet istemci sürümü |
| -------------- | ----------------------- | --------------------- |
| Paketi indir | 1.0.0 | 4.3.0 |
| [Kimlik Doğrulaması](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Doğru çalışma zamanı altında eklenti çalıştırma

DotNet. exe senaryolarında NuGet için, eklentiler DotNet. exe ' nin söz konusu çalışma zamanının altında yürütebilmelidir.
Bu, uyumlu bir DotNet. exe/eklenti birleşiminin kullanıldığından emin olmak için eklenti sağlayıcıdır ve tüketicidir.
Örnek olarak, Kullanıcı-konum eklentilerine yönelik olası bir sorun oluşabilir. 2,0 çalışma zamanı altındaki bir DotNet. exe, 2,1 çalışma zamanı için yazılmış bir eklenti kullanmaya çalışır.

## <a name="capabilities-caching"></a>Özellikleri önbelleğe alma

Eklentilerin güvenlik doğrulaması ve örnekleme maliyetlidir. İndirme işlemi kimlik doğrulama işleminden daha sık yapılır, ancak ortalama NuGet kullanıcısının yalnızca bir kimlik doğrulama eklentisine sahip olma olasılığı vardır.
Bu deneyimi geliştirmek için, NuGet verilen istek için işlem taleplerini önbelleğe alacak. Bu önbellek, eklenti anahtarı eklenti yolu olacak şekilde eklenti başına ve bu özellik önbelleğinin süresi 30 gündür. 

Önbellek `%LocalAppData%/NuGet/plugins-cache` ' da bulunur ve `NUGET_PLUGINS_CACHE_PATH` ortam değişkeniyle geçersiz kılınmalıdır. Bu [önbelleği](../../consume-packages/managing-the-global-packages-and-cache-folders.md)temizlemek için, birisi `plugins-cache` seçeneğiyle Yereller komutunu çalıştırabilir.
@No__t-0 Yereller seçeneği artık eklenti önbelleğini de silecek. 

## <a name="protocol-messages-index"></a>Protokol iletileri dizini

Protokol sürümü *1.0.0* iletileri:

1.  Close
    * İstek yönü: NuGet-> eklentisi
    * İstek yük içermez
    * Yanıt beklenmez.  Doğru yanıt, eklenti işleminin hemen çıkmak için gereken bir işlemdir.

2.  Paketteki dosyaları Kopyala
    * İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket KIMLIĞI ve sürümü
        * paket kaynağı depo konumu
        * hedef dizin yolu
        * paketteki hedef dizin yoluna kopyalanacak numaralandırılabilir dosyalar
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olduysa, hedef dizindeki kopyalanmış dosyalar için bir dizi tam yol

3.  Paket dosyasını Kopyala (. nupkg)
    * İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket KIMLIĞI ve sürümü
        * paket kaynağı depo konumu
        * Hedef dosya yolu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu

4.  Kimlik bilgilerini al
    * İstek yönü: eklenti > NuGet
    * Bu istek şunları içerir:
        * paket kaynağı depo konumu
        * geçerli kimlik bilgileri kullanılarak paket kaynak deposundan alınan HTTP durum kodu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * varsa, bir Kullanıcı adı
        * bir parola varsa

5.  Paketteki dosyaları al
    * İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket KIMLIĞI ve sürümü
        * paket kaynağı depo konumu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olursa paketteki dosya yollarının numaralandırılabilir olması

6.  İşlem taleplerini al 
    * İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket kaynağı için hizmet dizini. JSON
        * paket kaynağı depo konumu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olduysa, desteklenen işlem sayısı (ör.: paket indirme).  Bir eklenti paket kaynağını desteklemiyorsa, eklenti boş bir desteklenen işlemler kümesi döndürmelidir.

> [!Note]
> Bu ileti, *2.0.0*sürümünde güncelleştirilmiştir. Bu, geriye dönük uyumluluğu korumak için istemcsahiptir.

7.  Paket karmasını al
    * İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket KIMLIĞI ve sürümü
        * paket kaynağı depo konumu
        * karma algoritması
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olduysa, istenen karma algoritmasını kullanan bir paket dosyası karması

8.  Paket sürümlerini al
    * İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket KIMLIĞI
        * paket kaynağı depo konumu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olduysa paket sürümleri Numaralandırılabilir

9.  Hizmet dizinini al
    * İstek yönü: eklenti > NuGet
    * Bu istek şunları içerir:
        * paket kaynağı depo konumu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olduysa hizmet dizini

10.  Masını
     * İstek yönü: NuGet <-> eklentisi
     * Bu istek şunları içerir:
         * Geçerli eklenti Protokolü sürümü
         * desteklenen en düşük eklenti Protokolü sürümü
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu
         * işlem başarılı olduysa, anlaşmalı protokol sürümü.  Bir hata, eklentinin sonlandırılmasıyla sonuçlanır.

11.  Initialize
     * İstek yönü: NuGet-> eklentisi
     * Bu istek şunları içerir:
         * NuGet istemci aracı sürümü
         * NuGet istemci aracı etkin dili.  Bu, kullanılıyorsa ForceEnglishOutput ayarını dikkate alır.
         * varsayılan protokol varsayılan istek zaman aşımı.
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu.  Bir hata, eklentinin sonlandırılmasıyla sonuçlanır.

12.  Günlük
     * İstek yönü: eklenti > NuGet
     * Bu istek şunları içerir:
         * istek için günlük düzeyi
         * günlüğe kaydedilecek ileti
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu.

13.  NuGet işlemini izle çıkış çıkışı
     * İstek yönü: NuGet-> eklentisi
     * Bu istek şunları içerir:
         * NuGet işlem KIMLIĞI
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu.

14.  Önceden getirme paketi
     * İstek yönü: NuGet-> eklentisi
     * Bu istek şunları içerir:
         * paket KIMLIĞI ve sürümü
         * paket kaynağı depo konumu
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu

15.  Kimlik bilgilerini ayarla
     * İstek yönü: NuGet-> eklentisi
     * Bu istek şunları içerir:
         * paket kaynağı depo konumu
         * kullanılabiliyorsa, bilinen son paket kaynağı Kullanıcı adı
         * kullanılabiliyorsa, bilinen son paket kaynak parolası
         * kullanılabiliyorsa, bilinen son Proxy Kullanıcı adı
         * kullanılabiliyorsa, bilinen son proxy parolası
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu

16.  Günlük düzeyini ayarla
     * İstek yönü: NuGet-> eklentisi
     * Bu istek şunları içerir:
         * Varsayılan günlük düzeyi
     * Bir yanıt şunu içerir:
         * işlemin sonucunu gösteren bir yanıt kodu

Protokol sürümü *2.0.0* iletileri

17. Işlem taleplerini al

* İstek yönü: NuGet-> eklentisi
    * Bu istek şunları içerir:
        * paket kaynağı için hizmet dizini. JSON
        * paket kaynağı depo konumu
    * Bir yanıt şunu içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * işlem başarılı olduysa, desteklenen işlem sayısı.  Bir eklenti paket kaynağını desteklemiyorsa, eklenti boş bir desteklenen işlemler kümesi döndürmelidir.

    Hizmet dizini ve paket kaynağı null ise, eklenti kimlik doğrulamasıyla yanıt verebilir.

18. Kimlik doğrulama kimlik bilgilerini al

* İstek yönü: NuGet-> eklentisi
* Bu istek şunları içerir:
    * Kullanılmamışsa
    * ısretry
    * Etkileşimsiz
    * CanShowDialog
* Bir yanıt şunu içerir
    * Kullanıcı adı
    * istemcisiyle yönetilen bir cihaz için)
    * İleti
    * Kimlik doğrulama türleri listesi
    * MessageResponseCode
