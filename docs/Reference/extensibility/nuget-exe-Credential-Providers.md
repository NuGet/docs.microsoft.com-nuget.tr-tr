---
title: "nuget.exe kimlik bilgisi sağlayıcıları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe kimlik bilgisi sağlayıcıları akış ile kimlik doğrulaması ve belirli kurallarına uygun komut satırı yürütülebilir dosyalar uygulanır."
keywords: "nuget.exe kimlik bilgisi sağlayıcıları, kimlik bilgisi sağlayıcısı API, akış ile kimlik doğrulaması, Galerisi ile kimlik doğrulaması"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Akışları nuget.exe kimlik bilgisi sağlayıcıları ile kimlik doğrulaması

*NuGet 3.3 +*

Zaman `nuget.exe` akış ile kimlik doğrulaması için kimlik bilgileri gerekiyor kendileri için aşağıdaki şekilde görünür:

1. NuGet ilk arar kimlik bilgilerini `Nuget.Config` dosyaları.
1. NuGet sonra aşağıda verilen sıralama tabi eklenti kimlik bilgisi sağlayıcıları kullanır. (Ve örnek [Visual Studio Team Services kimlik bilgisi sağlayıcısı](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet sonra kullanıcıdan kimlik bilgilerini komut satırında ister.

Burada açıklanan kimlik bilgisi sağlayıcıları yalnızca iş Not `nuget.exe` 'dotnet geri yükleme' ya da Visual Studio içinde değil. Visual Studio ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe Visual Studio için kimlik bilgisi sağlayıcıları](nuget-credential-providers-for-visual-studio.md)

nuget.exe kimlik bilgisi sağlayıcıları 3 şekillerde kullanılabilir:

- **Genel olarak**: bir kimlik bilgisi sağlayıcısı tüm örnekleri kullanılabilir hale getirmek için `nuget.exe` geçerli kullanıcının profili altında çalıştırmak, ekleyin `%LocalAppData%\NuGet\CredentialProviders`. Oluşturmanız gerekebilir `CredentialProviders` klasör. Kimlik bilgisi sağlayıcıları kökünde yüklenebilir `CredentialProviders` klasörü veya bir alt klasör içinde. Bir kimlik bilgisi sağlayıcısı birden çok dosya derlemeleri varsa, alt klasörler düzenlenmiş sağlayıcıları tutmak için kullanabilirsiniz.

- **Bir ortam değişkeni gelen**: kimlik bilgisi sağlayıcıları herhangi bir yerde depolanabilir ve için erişilebilir hale `nuget.exe` ayarlayarak `%NUGET_CREDENTIALPROVIDERS_PATH%` Sağlayıcısı'nın konumunu ortam değişkenine. Bu değişken noktalı virgülle ayrılmış listesini olabilir (örneğin, `path1;path2`) birden çok konumda varsa.

- **Nuget.exe yanında**: nuget.exe kimlik bilgisi sağlayıcıları, aynı klasörde yerleştirilebilen `nuget.exe`.

Kimlik bilgisi sağlayıcıları yüklenirken `nuget.exe` adlı dosyası için sırasıyla Yukarıdaki konumlarda arar `credentialprovider*.exe`, bulunan sırada bu dosyaları yükler. Birden çok kimlik bilgisi sağlayıcısı aynı klasörde varsa, bunlar alfabetik sırada yüklü.

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe kimlik bilgisi sağlayıcısı oluşturma

Komut satırı yürütülebilir dosyasını bir kimlik bilgisi sağlayıcıdır biçiminde adlı `CredentialProvider*.exe`, girişleri toplar, uygun kimlik bilgilerini alır ve standart çıktı ve uygun çıkış durum kodu döndürür.

Bir sağlayıcı aşağıdakileri yapmanız gerekir:

- Bu kimlik bilgileri hedeflenen URI'sini kimlik bilgisi edinme başlatmadan önce sağlayıp sağlayamayacağını belirler. Yoksa, durum kodu 1 hiçbir kimlik bilgileriyle döndürmelidir.
- Değişiklik `Nuget.Config` (örneğin var. kimlik bilgilerini ayarlama).
- Tanıtıcı HTTP proxy yapılandırması kendi olarak NuGet üzerinde eklentisi için proxy bilgileri sağlamaz.
- Kimlik bilgileri veya hata ayrıntıları için iade `nuget.exe` UTF-8 kodlaması kullanarak stdout, JSON yanıt nesnesi (aşağıya bakın) yazarak.
- İsteğe bağlı olarak ek izleme günlüğü stderr'e yayma. Ayrıntı düzeyleri "normal" veya "ayrıntılı" gibi izlemeleri NuGet tarafından konsola echoed bu yana hiçbir gizli stderr, herhangi bir zamanda yazılması gerekir.
- NuGet gelecekteki sürümleriyle ileriye dönük uyumluluğu sağlama beklenmeyen parametreleri sayılır.

### <a name="input-parameters"></a>Giriş parametreleri

| Parametre/anahtarı |Açıklama|
|----------------|-----------|
| URI {value} | Paket Kaynak URI gerektiren kimlik bilgileri.|
| Etkileşimli olmayan | Varsa, sağlayıcı etkileşimli istemleri kesmez. |
| IsRetry | Varsa, bu deneme daha önce başarısız girişim yinelenmesini olduğunu gösterir. Sağlayıcılar genellikle tüm mevcut önbelleği atlama ve yeni kimlik bilgilerini mümkünse sormasına emin olmak için bu bayrağı kullanın.|
| Ayrıntı {value} | Varsa, aşağıdaki değerlerden birini: "normal", "quiet" veya "ayrıntılı". Herhangi bir değer belirtilirse, "normal" varsayılan olarak ayarlanır. Sağlayıcıları bu isteğe bağlı günlüğe kaydetme düzeyini belirtisi standart hata akışı yaymak üzere kullanmanız gerekir. |

### <a name="exit-codes"></a>Çıkış kodları

| Kod |Sonuç | Açıklama |
|----------------|-----------|-----------|
| 0 | Başarılı | Kimlik bilgileri başarıyla alındı ve stdout yazılır.|
| 1. | ProviderNotApplicable | Geçerli sağlayıcı verili URI için kimlik bilgilerini sağlamaz.|
| 2 | Hata | Sağlayıcı verili URI için doğru sağlayıcısıdır, ancak kimlik bilgileri girilemez. Bu durumda, nuget.exe kimlik doğrulaması yinelemez ve başarısız olur. Etkileşimli oturum açma kullanıcı iptal ettiğinde tipik bir örnektir. |

### <a name="standard-output"></a>Standart çıktı

| Özellik |Notlar|
|----------------|-----------|
| Kullanıcı adı | Kimliği doğrulanmış istekler için kullanıcı adı.|
| Parola | Kimliği doğrulanmış istekler için parola.|
| İleti | İsteğe bağlı ayrıntıları hakkında ek ayrıntılar hatası durumlarda yalnızca göstermek için kullanılan yanıt. |

Örnek stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Bir kimlik bilgisi sağlayıcı sorunlarını giderme

Şu anda, özel kimlik bilgisi sağlayıcıları hata ayıklama için NuGet kadar doğrudan destek sağlamaz; [sorun 4598](https://github.com/NuGet/Home/issues/4598) bu iş izleme.

Şunları da yapabilirsiniz:

- Nuget.exe ile Çalıştır `-verbosity` ayrıntılı çıktı incelemek için anahtar.
- Hata ayıklama iletileri ekleme `stdout` uygun yerlerde.
- 3.3 ya da daha yüksek nuget.exe kullandığınızdan emin olun.
- Bu kod parçacığı ile başlangıçta hata ayıklayıcı Ekle:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Daha fazla yardım için [bir destek isteği bir nuget.org göndermek](https://www.nuget.org/policies/Contact).
