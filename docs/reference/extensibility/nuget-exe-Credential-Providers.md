---
title: nuget.exe kimlik bilgileri sağlayıcıları
description: nuget.exe kimlik bilgileri sağlayıcıları bir akışa göre kimlik doğrulaması yapabilir ve belirli kuralları izleyen komut satırı yürütülebilir dosyaları olarak uygulanır.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238120"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>nuget.exe kimlik bilgileri sağlayıcılarıyla akışların kimliğini doğrulama

`3.3` `nuget.exe` Belirli kimlik bilgileri sağlayıcıları için sürüm desteği eklenmiştir. Sonrasında, `4.8` tüm komut satırı senaryolarında (,,) çalışan [kimlik bilgileri sağlayıcıları için sürüm desteği](NuGet-Cross-Platform-Authentication-Plugin.md) ' nde `nuget.exe` `dotnet.exe` `msbuild.exe` eklenmiştir.

Tüm kimlik doğrulama yaklaşımları hakkında daha fazla bilgi için bkz. [kimliği doğrulanmış akışlardan paketleri](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) kullanma `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe kimlik bilgisi sağlayıcısı bulma

nuget.exe kimlik bilgileri sağlayıcıları 3 şekilde kullanılabilir:

- **Küresel** : bir kimlik bilgisi sağlayıcısını geçerli kullanıcının profilinde çalıştırılacak tüm örnekleri için kullanılabilir hale getirmek için `nuget.exe` , ' ye ekleyin `%LocalAppData%\NuGet\CredentialProviders` . Klasörünü oluşturmanız gerekebilir `CredentialProviders` . Kimlik bilgisi sağlayıcıları `CredentialProviders`  klasörün köküne veya bir alt klasöre yüklenebilir. Bir kimlik bilgisi sağlayıcısında birden çok dosya/derleme varsa, sağlayıcıları düzenli tutmak için alt klasörleri kullanabilirsiniz.

- **Bir ortam değişkeninden** : kimlik bilgileri sağlayıcıları `nuget.exe` , `%NUGET_CREDENTIALPROVIDERS_PATH%` ortam değişkeni sağlayıcı konumuna ayarlanarak her yerde depolanabilir ve erişilebilir hale getirilebilir. Bu değişken, birden fazla konumunuz varsa, noktalı virgülle ayrılmış bir liste olabilir (örneğin, `path1;path2` ).

- **nuget.exe** : nuget.exe kimlik bilgileri sağlayıcıları ile aynı klasöre yerleştirilebilir `nuget.exe` .

Kimlik bilgileri sağlayıcıları yüklenirken, `nuget.exe` Yukarıdaki konumları sırasıyla, adlı herhangi bir dosya için arar `credentialprovider*.exe` ve ardından bu dosyaları bulundukları sırada yükler. Aynı klasörde birden çok kimlik bilgisi sağlayıcısı varsa, bunlar alfabetik sırayla yüklenir.

## <a name="creating-a-nugetexe-credential-provider"></a>nuget.exe kimlik bilgisi sağlayıcısı oluşturma

Kimlik bilgisi sağlayıcısı, formda adlı, `CredentialProvider*.exe` girdileri toplayan, uygun şekilde kimlik bilgilerini alan ve uygun çıkış durum kodunu ve Standart çıktıyı döndüren bir komut satırı çalıştırılabilir dosyadır.

Sağlayıcı aşağıdakileri yapması gerekir:

- Kimlik bilgilerinin alımı başlatmadan önce hedeflenen URI için kimlik bilgileri sağlayıp sağlayamayacağını belirleme. Aksi takdirde, kimlik bilgileri olmadan durum kodu 1 döndürmelidir.
- Değiştirme `Nuget.Config` (kimlik bilgilerini orada ayarlama gibi).
- NuGet, eklentiye ara sunucu bilgileri sağlamadığından, HTTP proxy yapılandırmasını kendi kendine işleyin.
- `nuget.exe`UTF-8 kodlaması kullanarak, stdout için BIR JSON yanıt nesnesi (aşağıya bakın) yazarak kimlik bilgilerini veya hata ayrıntılarını geri döndürün.
- İsteğe bağlı olarak stderr 'e ek izleme günlüğü yayın. Ayrıntı düzeyleri "normal" veya "ayrıntılı" olarak, bu tür izlemelerin konsola NuGet tarafından yankılanmış olması nedeniyle, hiçbir gizli dizi hiçbir zaman stderr 'e yazılmamalıdır.
- NuGet 'in gelecekteki sürümleriyle ileri doğru uyumluluk sağlayan beklenmeyen parametreler göz ardı edilmelidir.

### <a name="input-parameters"></a>Giriş parametreleri

| Parametre/anahtar |Açıklama|
|----------------|-----------|
| URI {Value} | Kimlik bilgileri gerektiren paket kaynak URI 'SI.|
| Etkileşimsiz | Varsa, sağlayıcı etkileşimli istemler vermez. |
| Isretry | Varsa, bu girişimin daha önce başarısız olan bir girişimin yeniden denendiğini gösterir. Sağlayıcılar genellikle bu bayrağı, var olan herhangi bir önbelleği atlamalarını ve mümkünse yeni kimlik bilgilerini sormasını sağlamak için kullanır.|
| Ayrıntı ayrıntısı {Value} | Varsa, aşağıdaki değerlerden biri: "normal", "sessiz" veya "ayrıntılı". Değer sağlanmazsa, varsayılan olarak "normal" olur. Sağlayıcılar bunu standart hata akışına yayma için isteğe bağlı günlük kaydı düzeyinin bir göstergesi olarak kullanmalıdır. |

### <a name="exit-codes"></a>Çıkış kodları

| Kod |Sonuç | Açıklama |
|----------------|-----------|-----------|
| 0 | Başarılı | Kimlik bilgileri başarıyla alındı ve STDOUT 'a yazıldı.|
| 1 | ProviderNotApplicable | Geçerli sağlayıcı verilen URI için kimlik bilgileri sağlamıyor.|
| 2 | Hata | Sağlayıcı, belirtilen URI için doğru sağlayıcıdır, ancak kimlik bilgileri sağlayamaz. Bu durumda nuget.exe kimlik doğrulaması yeniden denenmez ve başarısız olur. Tipik bir örnek, bir kullanıcı etkileşimli oturum açmayı iptal ettiğinde olur. |

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

- `-verbosity`Ayrıntılı çıktıyı incelemek için nuget.exe anahtarla çalıştırın.
- Uygun yerlere hata ayıklama iletileri ekleyin `stdout` .
- nuget.exe 3,3 veya üstünü kullandığınızdan emin olun.
- Bu kod parçacığı ile başlangıçta hata ayıklayıcı ekle:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
