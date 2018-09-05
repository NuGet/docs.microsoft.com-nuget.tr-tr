---
title: nuget.exe kimlik bilgileri sağlayıcıları
description: nuget.exe kimlik bilgileri sağlayıcıları bir akış ile kimlik doğrulaması ve belirli kurallarına uygun komut satırı yürütülebilir dosyaları uygulanır.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550195"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe kimlik bilgileri sağlayıcıları ile kimlik doğrulama akışları

*NuGet 3.3 +*

Zaman `nuget.exe` akış ile kimlik doğrulaması için kimlik bilgileri gerekiyor kendileri için şu şekilde görünür:

1. NuGet kimlik bilgileri için önce arar `Nuget.Config` dosyaları.
1. NuGet, daha sonra aşağıda verilen sıralama tabi eklenti kimlik bilgisi sağlayıcıları kullanır. (Ve örnek [Visual Studio Team Services kimlik bilgisi sağlayıcısı](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet daha sonra kullanıcıdan komut satırında kimlik bilgilerini ister.

Burada açıklanan kimlik bilgisi sağlayıcıları yalnızca iş Not `nuget.exe` 'dotnet restore' veya Visual Studio içinde değil. Visual Studio ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe Visual Studio için kimlik bilgileri sağlayıcısı](nuget-credential-providers-for-visual-studio.md)

nuget.exe kimlik bilgileri sağlayıcıları 3 şekilde kullanılabilir:

- **Genel olarak**: kimlik bilgisi Sağlayıcı'nın tüm örnekleri kullanılabilir hale getirmek için `nuget.exe` ekleyin, geçerli kullanıcının profilini altında çalıştırma `%LocalAppData%\NuGet\CredentialProviders`. Oluşturmanız gerekebilir `CredentialProviders` klasör. Kimlik bilgisi sağlayıcıları kökünde yüklenebilir `CredentialProviders` klasörü veya bir alt klasör içinde. Bir kimlik bilgisi sağlayıcısı, birden çok dosya derlemeleri varsa, sağlayıcıları düzenli tutmak için alt klasörleri'ni kullanabilirsiniz.

- **Bir ortam değişkeninden**: kimlik bilgisi sağlayıcıları herhangi bir yerde depolanabilir ve için erişilebilir hale `nuget.exe` ayarlayarak `%NUGET_CREDENTIALPROVIDERS_PATH%` ortam değişkeni sağlayıcı konumu. Bu değişken bir noktalı virgülle ayrılmış liste olabilir (örneğin, `path1;path2`) birden çok konumda varsa.

- **Nuget.exe yanı sıra**: nuget.exe kimlik bilgileri sağlayıcısı, aynı klasörde yerleştirilebileceğini `nuget.exe`.

Kimlik bilgisi sağlayıcıları yüklenirken `nuget.exe` adlı herhangi bir dosya için sırayla yukarıdaki konumları arar `credentialprovider*.exe`, daha sonra bu dosyaları bulundukları sıraya yükler. Birden çok kimlik bilgisi sağlayıcı aynı klasörde varsa, alfabetik olarak yüklendi.

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe kimlik bilgileri sağlayıcısı oluşturma

Komut satırı yürütülebilir dosyasını bir kimlik bilgisi sağlayıcıdır biçiminde adlandırılmış `CredentialProvider*.exe`, girişleri toplar, uygun kimlik bilgilerini alır ve ardından standart çıktı ve uygun çıkış durum kodu döndürür.

Bir sağlayıcı aşağıdakileri yapmalısınız:

- Bu kimlik bilgileri hedeflenen URI için kimlik bilgilerini almayı başlatmadan önce sağlayıp sağlayamayacağını belirleyin. Aksi durumda, durum kodu 1 ile kimlik bilgileri döndürmesi gerekir.
- Değişiklik `Nuget.Config` (örneğin, burada kimlik bilgilerini ayarlama).
- Tanıtıcı HTTP proxy yapılandırması kendi olarak NuGet üzerindeki eklentisi için proxy bilgileri sağlamaz.
- Kimlik bilgileri veya hata ayrıntılarını dönüş `nuget.exe` Stdout'a UTF-8 kodlaması kullanarak bir JSON yanıtı nesnesi (aşağıya bakın) yazarak.
- İsteğe bağlı olarak ek izleme günlüğü stderr'e gösterin. Ayrıntı düzeylerinde "normal" veya "ayrıntılı", bu tür izleme tarafından NuGet konsola okunmaz olduğundan gizli dizi stderr için hiç olmadığı kadar yazılması gerekir.
- NuGet gelecekteki sürümleriyle ileriye dönük uyumluluk sağlama beklenmeyen parametre yoksayılacak.

### <a name="input-parameters"></a>Giriş parametreleri

| Parametre/anahtarı |Açıklama|
|----------------|-----------|
| URI {value} | Paket Kaynak URI gerektiren kimlik bilgileri.|
| NonInteractive | Varsa, sağlayıcı etkileşimli istemleri kesmez. |
| isRetry | Varsa, bu deneme daha önce başarısız bir girişimden yinelenmesini olduğunu gösterir. Sağlayıcıları, genellikle tüm mevcut önbelleğini atla ve mümkünse yeni kimlik bilgilerinizi ister emin olmak için bu bayrağı kullanın.|
| {Value} ayrıntı düzeyi | Varsa, aşağıdaki değerlerden biri: "normal", "quiet" veya "ayrıntılı". Hiçbir değer sağlanmazsa, "normal" varsayılan olarak. Sağlayıcıları bu için standart hata akışı yaymak için bir isteğe bağlı günlüğe kaydetme düzeyini göstergesi olarak kullanmalısınız. |

### <a name="exit-codes"></a>Çıkış kodları

| Kod |Sonuç | Açıklama |
|----------------|-----------|-----------|
| 0 | Başarılı | Kimlik bilgileri başarıyla alındı ve stdout için yazılmıştır.|
| 1. | ProviderNotApplicable | Geçerli sağlayıcı verilen URI için kimlik bilgileri sağlamaz.|
| 2 | hata | Sağlayıcı, verilen URI için doğru sağlayıcısıdır, ancak kimlik bilgileri girilemez. Bu durumda, nuget.exe kimlik doğrulaması yeniden denensin değil ve başarısız olur. Bir kullanıcı bir etkileşimli oturum açma işlemi iptal ettiğinde tipik bir örnektir. |

### <a name="standard-output"></a>Standart çıktı

| Özellik |Notlar|
|----------------|-----------|
| Kullanıcı adı | Kimliği doğrulanmış istekler için kullanıcı adı.|
| Parola | Kimliği doğrulanmış istekler için parola.|
| İleti | Yalnızca hata durumlarda ek ayrıntıları göstermek için kullanılan yanıt hakkında isteğe bağlı ayrıntılar. |

Stdout. örnek:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Bir kimlik bilgisi sağlayıcı sorunlarını giderme

Şu anda, özel kimlik bilgileri sağlayıcısı hata ayıklama için NuGet kadar doğrudan destek sağlamaz; [sorun 4598](https://github.com/NuGet/Home/issues/4598) bu iş izleme.

Şunları da yapabilirsiniz:

- Nuget.exe ile çalıştırma `-verbosity` ayrıntılı çıkış incelemek için anahtar.
- Hata ayıklama ileti için ekleme `stdout` uygun yerlerde.
- Nuget.exe 3.3 ya da daha yüksek kullandığınızdan emin olun.
- Başlangıçta bu kod parçacığı ile hata ayıklayıcının:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Daha fazla yardım için [bir destek isteği bir nuget.org](https://www.nuget.org/policies/Contact).
