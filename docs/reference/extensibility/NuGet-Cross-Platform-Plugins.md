---
title: NuGet çapraz platform eklentileri
description: NuGet.exe, dotnet.exe, msbuild.exe ve Visual Studio için NuGet çapraz platform eklentileri
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794206"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet çapraz platform eklentileri

Nuget'te 4.8 + çapraz platform eklentileri için destek eklendi.
Bu ile katı bir işlemin kuralları kümesi için uygun olan yeni bir eklenti genişletilebilirlik modeli, oluşturarak elde.
NuGet istemcileri ayrı bir işlemde başlatma bağımsız yürütülebilir (runnables) .NET Core dünyanın artırmasını.
Doğru yazma eklentisi her yerde çalıştırın bir kez budur. NuGet istemci araçları ile çalışır.
Eklentileri, .NET Framework'ün (NuGet.exe, MSBuild.exe ve Visual Studio) ya da .NET Core (dotnet.exe) olabilir.
NuGet istemci ile eklenti arasındaki tutulan iletişim protokolü tanımlanır. Başlangıç anlaşması sırasında Protokolü sürüm 2 işlemleri anlaşır.

Tüm NuGet istemci araçları senaryolarınızı kapsaması için bir .NET Framework hem de .NET Core eklentisi gerekir.
Aşağıdaki eklenti istemci/framework birleşimlerini açıklar.

| İstemci aracı  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| DotNet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe Mono üzerinde | .NET Framework |

## <a name="how-does-it-work"></a>Nasıl çalışır

Üst düzey iş akışı şu şekilde açıklanabilir:

1. NuGet, kullanılabilir eklentiler bulur.
1. Uygun olduğunda NuGet öncelik sırasına ve başlar birer birer eklentileri üzerinden yineleme yapma.
1. NuGet, istek servis edebilirsiniz ilk eklenti kullanır.
1. Artık gerekli olmadığında eklentileri kapatılır.

## <a name="general-plugin-requirements"></a>Genel eklentisi gereksinimleri

Geçerli protokol sürümü *2.0.0*.
Bu sürümü'nün altında gereksinimleri aşağıdaki gibidir:

- Windows ve Mono üzerinde çalışacak bir geçerli ve güvenilen Authenticode imzası derlemeleri vardır. Linux ve Mac henüz çalışan derlemeler için özel güven gereksinimi yoktur. [İlgili sorun](https://github.com/NuGet/Home/issues/6702)
- NuGet istemci Araçları'nın geçerli güvenlik bağlamı altında durum bilgisi olmayan başlatma destekler. Örneğin, NuGet istemci araçlarını yükseltme veya daha sonra açıklanan eklenti Protokolü dışında ek başlatma gerçekleştirmez.
- Açıkça belirtilmediği sürece olmayan etkileşimli olması.
- Üzerinde anlaşılan eklentisini protokolü sürümüne bağlıdır.
- Tüm istekler için makul bir süre içinde yanıt.
- Tüm devam eden işlemi iptal isteklerini dikkate.

Teknik belirtim aşağıdaki özellikleri daha ayrıntılı açıklanmıştır:

- [NuGet paketini indirme eklentisi](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet kimlik doğrulama eklentisini plat çapraz](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>İstemci - eklentisi etkileşimi

NuGet istemci araçları ve eklentileri ile JSON standart akış (stdin, stdout, stderr) iletişim kurar. Tüm verileri UTF-8 olarak kodlanmış olmalıdır.
Eklenti bağımsız değişkeniyle başlatılır "-eklentisi". Kullanıcı doğrudan bu bağımsız değişken yürütülebilir bir eklenti başlatır durumunda, eklenti için bir protokol anlaşması beklemek yerine bilgilendirici bir ileti verebilirsiniz.
Protokol anlaşması zaman aşımı, 5 saniyedir. Eklenti, mümkün olduğunca bir miktar eksikliği kurulum olarak tamamlanmalıdır.
NuGet istemci araçları NuGet kaynağı için hizmet dizini geçirerek bir eklenti'nın desteklenen işlemler sorgular. Bir eklenti için desteklenen hizmet türlerinin varlığını denetlemek için hizmet dizini kullanabilir.

NuGet istemci araçları ile eklenti arasındaki iletişim çift yönlü ' dir. Her isteğin 5 saniyelik bir zaman aşımı vardır. İşlemleri daha uzun sürer istemiyorsanız ilgili işlem istek zaman aşımına uğramadan engellemek için bir ilerleme iletisi göndermesi gerekir. 1 dakika kaldıktan sonra bir eklenti boşta kabul edilip kapatılır.

## <a name="plugin-installation-and-discovery"></a>Eklenti yükleme ve bulma

Eklentileri tabanlı bir dizin yapısı bulunacaktır.
CI/CD senaryoları ve ileri kullanıcılar bir ortam değişkeni davranışı geçersiz kılmak için kullanabilirsiniz.

- `NUGET_PLUGIN_PATHS` -ayrılmış öncelik o NuGet işlemi için kullanılacak eklentileri tanımlar. Bu ortam değişkenine ayarlanmışsa tabanlı bulma geçersiz kılar.
-  Kullanıcı konumu, NuGet giriş konumda `%UserProfile%/.nuget/plugins`. Bu konum, geçersiz kılınan olamaz. .NET Core ve .NET Framework eklenti için farklı bir kök dizini kullanılacak.

| Framework | Bulma kökü  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Her eklentinin kendi klasöründe yüklü olması gerekir.
Eklentisi giriş noktası adı yüklü klasöründe .dll uzantılar için .NET Core ve .NET Framework için .exe uzantısına sahip olacaktır.

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
> Şu anda hiçbir kullanıcı hikayesi için eklenti yüklemesi. Gerekli dosyaları önceden belirlenmiş konuma hareket ettirmek kadar basittir.

## <a name="supported-operations"></a>Desteklenen işlemler

İki işlem altında yeni eklenti Protokolü desteklenir.

| İşlem adı | En düşük protokol sürümü | En düşük NuGet istemci sürümü |
| -------------- | ----------------------- | --------------------- |
| Paketini indirme | 1.0.0 | 4.3.0 |
| [Kimlik Doğrulaması](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Eklentileri doğru çalışma zamanı altında çalışan

Bu belirli dotnet.exe çalışma zamanı altında yürütebilmek için eklentileri dotnet.exe senaryolarda NuGet için gerekir.
Bu uyumlu dotnet.exe/plugin birlikte kullanılan emin olmak için eklenti sağlayıcısı ve tüketici üzerinde olur.
Olası bir sorun meydana gelebilecek kullanıcı konumu eklenti ile olduğunda, örneğin, 2.0 çalışma zamanı altında bir dotnet.exe 2.1 çalışma zamanı için yazılan bir eklenti kullanmayı dener.

## <a name="capabilities-caching"></a>Önbelleğe alma özellikleri

Güvenlik doğrulaması ve eklentileri örneğinin pahalı. İndirme işlemi, ancak ortalama NuGet kullanıcının yalnızca bir kimlik doğrulama eklentisini olasılığı kimlik doğrulama işlemi, daha sık gerçekleşir.
NuGet deneyimini iyileştirmek üzere belirtilen istek için işlem talepleri önbelleğe alır. Bu önbellek eklentisi eklentisi yolu olan eklentisi anahtarı ile ve bu özellikleri önbellek için sona erme 30 gündür. 

Önbellek bulunan `%LocalAppData%/NuGet/plugins-cache` ve ortam değişkeni ile geçersiz kılınmış `NUGET_PLUGINS_CACHE_PATH`. Bu temizlemek için [önbellek](../../consume-packages/managing-the-global-packages-and-cache-folders.md), bir yerel öğeler çalıştırabilirsiniz komutunu `plugins-cache` seçeneği.
`all` Yereller seçeneği artık da silinir plugins önbellek. 

## <a name="protocol-messages-index"></a>İletişim kuralı iletileri dizini

Protokol sürümü *1.0.0* iletileri:

1.  Close
    * Yön istek: NuGet eklentisi ->
    * İstek yükü yok içerir
    * Yanıt bekleniyor.  Doğru yanıtı hemen çıkılmasına eklentisi için işlemidir.

2.  Paketteki dosyaları Kopyala
    * Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * paket kimliği ve sürüm
        * Paket kaynağı depo konumu
        * Hedef dizin yolu
        * numaralandırılabilir bir hedef dizin yolu kopyalanacak paket dosyaları
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * İşlem başarılı ise hedef dizinde kopyalanan dosyaların tam yollarının bir numaralandırılabilir

3.  Paket dosyası (.nupkg) kopyalayın
    * Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * paket kimliği ve sürüm
        * Paket kaynağı depo konumu
        * Hedef dosya yolu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu

4.  Kimlik bilgilerini alma
    * Yön istek: eklenti NuGet ->
    * İstek içerir:
        * Paket kaynağı depo konumu
        * Geçerli kimlik bilgilerini kullanarak paket kaynak deposundan alınan HTTP durum kodu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * varsa bir kullanıcı adı
        * varsa bir parola

5.  Paketteki dosyaları Al
    * Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * paket kimliği ve sürüm
        * Paket kaynağı depo konumu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * İşlem başarılı olduysa, paketteki dosya yollarının bir numaralandırılabilir

6.  İşlem talebi alır 
    * Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * Paket kaynağı için hizmet index.json
        * Paket kaynağı depo konumu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * numaralandırılabilir, desteklenen işlemler (örn: paket yükleme) işlemi başarılı olursa.  Eklenti, bir eklenti paket kaynağı desteklemiyorsa boş bir desteklenen işlemler kümesi döndürmelidir.

> [!Note]
> Bu ileti sürümünde güncelleştirildi *2.0.0*. Geriye dönük uyumluluğu korumak için istemcide var.

7.  Paket karmasını alır
    * Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * paket kimliği ve sürüm
        * Paket kaynağı depo konumu
        * karma algoritması
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * İşlem başarılı olursa, istenen karma algoritması kullanarak bir paket dosya karması

8.  Paket sürümü alma
    * Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * paket kimliği
        * Paket kaynağı depo konumu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * numaralandırılabilir işlemi başarılı olursa, paket sürümleri

9.  Hizmet dizini alın
    * Yön istek: eklenti NuGet ->
    * İstek içerir:
        * Paket kaynağı depo konumu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * İşlem başarılı ise hizmet dizini

10.  Anlaşması
     * Yön istek: NuGet <> – eklentisi
     * İstek içerir:
         * Geçerli eklentisi protokolü sürümü
         * desteklenen en düşük eklentisi protokol sürümü
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu
         * İşlem başarılı olduysa anlaşılan protokol sürümü.  Bir hata eklenti sonlandırmada neden olur.

11.  başlatma
     * Yön istek: NuGet eklentisi ->
     * İstek içerir:
         * NuGet istemci aracı sürümü
         * NuGet istemci aracı geçerli dili.  Bu dikkate ForceEnglishOutput ayarı kullandıysanız alır.
         * protokol varsayılan yerini varsayılan isteği zaman aşımı.
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu.  Bir hata eklenti sonlandırmada neden olur.

12.  Günlük
     * Yön istek: eklenti NuGet ->
     * İstek içerir:
         * istek için günlük düzeyi
         * günlüğe kaydedilecek iletinin
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu.

13.  İzleyici NuGet işlem çıkışı
     * Yön istek: NuGet eklentisi ->
     * İstek içerir:
         * NuGet işlem kimliği
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu.

14.  Paket Hazırlık
     * Yön istek: NuGet eklentisi ->
     * İstek içerir:
         * paket kimliği ve sürüm
         * Paket kaynağı depo konumu
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu

15.  Kimlik bilgilerini ayarla
     * Yön istek: NuGet eklentisi ->
     * İstek içerir:
         * Paket kaynağı depo konumu
         * Son bilinen paket kaynağı kullanıcı adı, mevcutsa
         * Son bilinen paket kaynağı parolası, mevcutsa
         * Son bilinen proxy kullanıcı adı, mevcutsa
         * Son bilinen bir ara sunucu parolasını, mevcutsa
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu

16.  Günlük düzeyini ayarlama
     * Yön istek: NuGet eklentisi ->
     * İstek içerir:
         * Varsayılan günlük düzeyi
     * Bir yanıt içerir:
         * işlemin sonucunu gösteren bir yanıt kodu

Protokol sürümü *2.0.0* iletileri

17. İşlem talebi alır

* Yön istek: NuGet eklentisi ->
    * İstek içerir:
        * Paket kaynağı için hizmet index.json
        * Paket kaynağı depo konumu
    * Bir yanıt içerir:
        * işlemin sonucunu gösteren bir yanıt kodu
        * bir numaralandırma işlemi başarılı olursa, desteklenen işlemler.  Eklenti, bir eklenti paket kaynağı desteklemiyorsa boş bir desteklenen işlemler kümesi döndürmelidir.

    Hizmet dizini ve paket kaynağı null ise, eklenti ile kimlik doğrulaması yanıt verebilir.

18. Kimlik doğrulama kimlik bilgilerini alma

* Yön istek: NuGet eklentisi ->
* İstek içerir:
    * URI
    * isRetry
    * NonInteractive
    * CanShowDialog
* Bir yanıt içerir
    * Kullanıcı adı
    * Parola
    * İleti
    * Kimlik doğrulama türlerinin listesi
    * MessageResponseCode