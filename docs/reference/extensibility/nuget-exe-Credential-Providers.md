---
title: NuGet. exe kimlik bilgileri sağlayıcıları
description: NuGet. exe kimlik bilgileri sağlayıcıları bir akışa kimlik doğrular ve belirli kuralları izleyen komut satırı yürütülebilir dosyaları olarak uygulanır.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230791"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>NuGet. exe kimlik bilgisi sağlayıcılarıyla akışların kimliğini doğrulama

Sürüm `3.3` `nuget.exe` belirli kimlik bilgileri sağlayıcıları için destek eklenmiştir. Sonrasında, tüm komut satırı senaryolarında (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) çalışan [kimlik bilgileri sağlayıcıları için](NuGet-Cross-Platform-Authentication-Plugin.md) sürüm `4.8` desteği eklenmiştir.

`nuget.exe` yönelik tüm kimlik doğrulama yaklaşımları hakkında daha fazla bilgi için bkz. [kimliği doğrulanmış akışlardan paketleri](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) kullanma

## <a name="nugetexe-credential-provider-discovery"></a>NuGet. exe kimlik bilgisi sağlayıcısı bulma

NuGet. exe kimlik bilgileri sağlayıcıları 3 şekilde kullanılabilir:

- **Küresel**: bir kimlik bilgisi sağlayıcısını geçerli kullanıcının profilinde çalıştırılan tüm `nuget.exe` örnekleri için kullanılabilir hale getirmek için, `%LocalAppData%\NuGet\CredentialProviders`ekleyin. `CredentialProviders` klasörünü oluşturmanız gerekebilir. Kimlik bilgileri sağlayıcıları `CredentialProviders` klasörünün köküne veya bir alt klasöre yüklenebilir. Bir kimlik bilgisi sağlayıcısında birden çok dosya/derleme varsa, sağlayıcıları düzenli tutmak için alt klasörleri kullanabilirsiniz.

- **Bir ortam değişkeninden**: kimlik bilgileri sağlayıcıları her yerde depolanabilir ve `%NUGET_CREDENTIALPROVIDERS_PATH%` ortam değişkeni sağlayıcı konumuna ayarlanarak `nuget.exe` erişilebilir hale getirilebilir. Birden çok konumunuz varsa, bu değişken noktalı virgülle ayrılmış bir liste (örneğin, `path1;path2`) olabilir.

- **NuGet. exe ' nin yanı sıra**, NuGet. exe kimlik bilgileri sağlayıcıları `nuget.exe`ile aynı klasöre yerleştirilebilir.

Kimlik bilgileri sağlayıcıları yüklenirken `nuget.exe`, Yukarıdaki konumları sırasıyla, `credentialprovider*.exe`adlı herhangi bir dosya için arar ve ardından bu dosyaları bulundukları sırada yükler. Aynı klasörde birden çok kimlik bilgisi sağlayıcısı varsa, bunlar alfabetik sırayla yüklenir.

## <a name="creating-a-nugetexe-credential-provider"></a>NuGet. exe kimlik bilgisi sağlayıcısı oluşturma

Kimlik bilgisi sağlayıcısı, girdileri toplayan, uygun kimlik bilgilerini alan ve uygun çıkış durum kodunu ve Standart çıktıyı döndüren form `CredentialProvider*.exe`adlı bir komut satırı çalıştırılabilir dosyadır.

Sağlayıcı aşağıdakileri yapması gerekir:

- Kimlik bilgilerinin alımı başlatmadan önce hedeflenen URI için kimlik bilgileri sağlayıp sağlayamayacağını belirleme. Aksi takdirde, kimlik bilgileri olmadan durum kodu 1 döndürmelidir.
- `Nuget.Config` değiştirmeyin (burada kimlik bilgilerini ayarlama gibi).
- NuGet, eklentiye ara sunucu bilgileri sağlamadığından, HTTP proxy yapılandırmasını kendi kendine işleyin.
- UTF-8 kodlaması kullanarak, stdout için bir JSON yanıt nesnesi (aşağıya bakın) yazarak `nuget.exe` kimlik bilgilerini veya hata ayrıntılarını döndürün.
- İsteğe bağlı olarak stderr 'e ek izleme günlüğü yayın. Ayrıntı düzeyleri "normal" veya "ayrıntılı" olarak, bu tür izlemelerin konsola NuGet tarafından yankılanmış olması nedeniyle, hiçbir gizli dizi hiçbir zaman stderr 'e yazılmamalıdır.
- NuGet 'in gelecekteki sürümleriyle ileri doğru uyumluluk sağlayan beklenmeyen parametreler göz ardı edilmelidir.

### <a name="input-parameters"></a>Giriş parametreleri

| Parametre/anahtar |Açıklama|
|----------------|-----------|
| URI {Value} | Kimlik bilgileri gerektiren paket kaynak URI 'SI.|
| NonInteractive | Varsa, sağlayıcı etkileşimli istemler vermez. |
| Isretry | Varsa, bu girişimin daha önce başarısız olan bir girişimin yeniden denendiğini gösterir. Sağlayıcılar genellikle bu bayrağı, var olan herhangi bir önbelleği atlamalarını ve mümkünse yeni kimlik bilgilerini sormasını sağlamak için kullanır.|
| Ayrıntı ayrıntısı {Value} | Varsa, aşağıdaki değerlerden biri: "normal", "sessiz" veya "ayrıntılı". Değer sağlanmazsa, varsayılan olarak "normal" olur. Sağlayıcılar bunu standart hata akışına yayma için isteğe bağlı günlük kaydı düzeyinin bir göstergesi olarak kullanmalıdır. |

### <a name="exit-codes"></a>Çıkış kodları

| Kod |Sonuç | Açıklama |
|----------------|-----------|-----------|
| 0 | Başarılı | Kimlik bilgileri başarıyla alındı ve STDOUT 'a yazıldı.|
| 1 | ProviderNotApplicable | Geçerli sağlayıcı verilen URI için kimlik bilgileri sağlamıyor.|
| 2 | Hata | Sağlayıcı, belirtilen URI için doğru sağlayıcıdır, ancak kimlik bilgileri sağlayamaz. Bu durumda, NuGet. exe kimlik doğrulamasını yeniden denemez ve başarısız olur. Tipik bir örnek, bir kullanıcı etkileşimli oturum açmayı iptal ettiğinde olur. |

### <a name="standard-output"></a>Standart çıktı

| Özellik |Notlar|
|----------------|-----------|
| Kullanıcı adı | Kimliği doğrulanmış istekler için Kullanıcı adı.|
| Parola | Kimliği doğrulanmış istekler için parola.|
| İleti | Yanıtla ilgili isteğe bağlı ayrıntılar, yalnızca hata durumlarında ek ayrıntıları göstermek için kullanılır. |

Örnek stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Kimlik bilgisi sağlayıcısı sorunlarını giderme

NuGet, özel kimlik bilgisi sağlayıcılarının hatalarını ayıklamak için çok doğrudan destek sağlamaz. [sorun 4598](https://github.com/NuGet/Home/issues/4598) , bu çalışmayı izliyor.

Şunları da yapabilirsiniz:

- Ayrıntılı çıktıyı incelemek için NuGet. exe ' yi `-verbosity` anahtarıyla çalıştırın.
- Uygun yerlere `stdout` hata ayıklama iletileri ekleyin.
- NuGet. exe 3,3 veya üstünü kullandığınızdan emin olun.
- Bu kod parçacığı ile başlangıçta hata ayıklayıcı ekle:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
