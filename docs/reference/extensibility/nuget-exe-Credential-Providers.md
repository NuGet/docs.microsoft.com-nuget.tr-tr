---
title: nuget.exe kimlik bilgisi sağlayıcıları
description: nuget.exe kimlik bilgisi sağlayıcıları akış ile kimlik doğrulaması ve belirli kurallarına uygun komut satırı yürütülebilir dosyalar uygulanır.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 494ea83007895e973585395e0cfe05b7226c4c3e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="1ec84-103">Akışları nuget.exe kimlik bilgisi sağlayıcıları ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1ec84-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="1ec84-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="1ec84-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="1ec84-105">Zaman `nuget.exe` akış ile kimlik doğrulaması için kimlik bilgileri gerekiyor kendileri için aşağıdaki şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="1ec84-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="1ec84-106">NuGet ilk arar kimlik bilgilerini `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="1ec84-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="1ec84-107">NuGet sonra aşağıda verilen sıralama tabi eklenti kimlik bilgisi sağlayıcıları kullanır.</span><span class="sxs-lookup"><span data-stu-id="1ec84-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="1ec84-108">(Ve örnek [Visual Studio Team Services kimlik bilgisi sağlayıcısı](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="1ec84-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="1ec84-109">NuGet sonra kullanıcıdan kimlik bilgilerini komut satırında ister.</span><span class="sxs-lookup"><span data-stu-id="1ec84-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="1ec84-110">Burada açıklanan kimlik bilgisi sağlayıcıları yalnızca iş Not `nuget.exe` 'dotnet geri yükleme' ya da Visual Studio içinde değil.</span><span class="sxs-lookup"><span data-stu-id="1ec84-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="1ec84-111">Visual Studio ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe Visual Studio için kimlik bilgisi sağlayıcıları](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="1ec84-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="1ec84-112">nuget.exe kimlik bilgisi sağlayıcıları 3 şekillerde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="1ec84-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="1ec84-113">**Genel olarak**: bir kimlik bilgisi sağlayıcısı tüm örnekleri kullanılabilir hale getirmek için `nuget.exe` geçerli kullanıcının profili altında çalıştırmak, ekleyin `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="1ec84-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="1ec84-114">Oluşturmanız gerekebilir `CredentialProviders` klasör.</span><span class="sxs-lookup"><span data-stu-id="1ec84-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="1ec84-115">Kimlik bilgisi sağlayıcıları kökünde yüklenebilir `CredentialProviders` klasörü veya bir alt klasör içinde.</span><span class="sxs-lookup"><span data-stu-id="1ec84-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="1ec84-116">Bir kimlik bilgisi sağlayıcısı birden çok dosya derlemeleri varsa, alt klasörler düzenlenmiş sağlayıcıları tutmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ec84-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="1ec84-117">**Bir ortam değişkeni gelen**: kimlik bilgisi sağlayıcıları herhangi bir yerde depolanabilir ve için erişilebilir hale `nuget.exe` ayarlayarak `%NUGET_CREDENTIALPROVIDERS_PATH%` Sağlayıcısı'nın konumunu ortam değişkenine.</span><span class="sxs-lookup"><span data-stu-id="1ec84-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="1ec84-118">Bu değişken noktalı virgülle ayrılmış listesini olabilir (örneğin, `path1;path2`) birden çok konumda varsa.</span><span class="sxs-lookup"><span data-stu-id="1ec84-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="1ec84-119">**Nuget.exe yanında**: nuget.exe kimlik bilgisi sağlayıcıları, aynı klasörde yerleştirilebilen `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="1ec84-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="1ec84-120">Kimlik bilgisi sağlayıcıları yüklenirken `nuget.exe` adlı dosyası için sırasıyla Yukarıdaki konumlarda arar `credentialprovider*.exe`, bulunan sırada bu dosyaları yükler.</span><span class="sxs-lookup"><span data-stu-id="1ec84-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="1ec84-121">Birden çok kimlik bilgisi sağlayıcısı aynı klasörde varsa, bunlar alfabetik sırada yüklü.</span><span class="sxs-lookup"><span data-stu-id="1ec84-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="1ec84-122">Nuget.exe kimlik bilgisi sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ec84-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="1ec84-123">Komut satırı yürütülebilir dosyasını bir kimlik bilgisi sağlayıcıdır biçiminde adlı `CredentialProvider*.exe`, girişleri toplar, uygun kimlik bilgilerini alır ve standart çıktı ve uygun çıkış durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1ec84-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="1ec84-124">Bir sağlayıcı aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ec84-124">A provider must do the following:</span></span>

- <span data-ttu-id="1ec84-125">Bu kimlik bilgileri hedeflenen URI'sini kimlik bilgisi edinme başlatmadan önce sağlayıp sağlayamayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="1ec84-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1ec84-126">Yoksa, durum kodu 1 hiçbir kimlik bilgileriyle döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="1ec84-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="1ec84-127">Değişiklik `Nuget.Config` (örneğin var. kimlik bilgilerini ayarlama).</span><span class="sxs-lookup"><span data-stu-id="1ec84-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="1ec84-128">Tanıtıcı HTTP proxy yapılandırması kendi olarak NuGet üzerinde eklentisi için proxy bilgileri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1ec84-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="1ec84-129">Kimlik bilgileri veya hata ayrıntıları için iade `nuget.exe` UTF-8 kodlaması kullanarak stdout, JSON yanıt nesnesi (aşağıya bakın) yazarak.</span><span class="sxs-lookup"><span data-stu-id="1ec84-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="1ec84-130">İsteğe bağlı olarak ek izleme günlüğü stderr'e yayma.</span><span class="sxs-lookup"><span data-stu-id="1ec84-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="1ec84-131">Ayrıntı düzeyleri "normal" veya "ayrıntılı" gibi izlemeleri NuGet tarafından konsola echoed bu yana hiçbir gizli stderr, herhangi bir zamanda yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ec84-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="1ec84-132">NuGet gelecekteki sürümleriyle ileriye dönük uyumluluğu sağlama beklenmeyen parametreleri sayılır.</span><span class="sxs-lookup"><span data-stu-id="1ec84-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="1ec84-133">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="1ec84-133">Input parameters</span></span>

| <span data-ttu-id="1ec84-134">Parametre/anahtarı</span><span class="sxs-lookup"><span data-stu-id="1ec84-134">Parameter/Switch</span></span> |<span data-ttu-id="1ec84-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ec84-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="1ec84-136">URI {value}</span><span class="sxs-lookup"><span data-stu-id="1ec84-136">Uri {value}</span></span> | <span data-ttu-id="1ec84-137">Paket Kaynak URI gerektiren kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1ec84-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="1ec84-138">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="1ec84-138">NonInteractive</span></span> | <span data-ttu-id="1ec84-139">Varsa, sağlayıcı etkileşimli istemleri kesmez.</span><span class="sxs-lookup"><span data-stu-id="1ec84-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="1ec84-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="1ec84-140">IsRetry</span></span> | <span data-ttu-id="1ec84-141">Varsa, bu deneme daha önce başarısız girişim yinelenmesini olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1ec84-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="1ec84-142">Sağlayıcılar genellikle tüm mevcut önbelleği atlama ve yeni kimlik bilgilerini mümkünse sormasına emin olmak için bu bayrağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ec84-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="1ec84-143">Ayrıntı {value}</span><span class="sxs-lookup"><span data-stu-id="1ec84-143">Verbosity {value}</span></span> | <span data-ttu-id="1ec84-144">Varsa, aşağıdaki değerlerden birini: "normal", "quiet" veya "ayrıntılı".</span><span class="sxs-lookup"><span data-stu-id="1ec84-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="1ec84-145">Herhangi bir değer belirtilirse, "normal" varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1ec84-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="1ec84-146">Sağlayıcıları bu isteğe bağlı günlüğe kaydetme düzeyini belirtisi standart hata akışı yaymak üzere kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ec84-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="1ec84-147">Çıkış kodları</span><span class="sxs-lookup"><span data-stu-id="1ec84-147">Exit codes</span></span>

| <span data-ttu-id="1ec84-148">Kod</span><span class="sxs-lookup"><span data-stu-id="1ec84-148">Code</span></span> |<span data-ttu-id="1ec84-149">Sonuç</span><span class="sxs-lookup"><span data-stu-id="1ec84-149">Result</span></span> | <span data-ttu-id="1ec84-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ec84-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="1ec84-151">0</span><span class="sxs-lookup"><span data-stu-id="1ec84-151">0</span></span> | <span data-ttu-id="1ec84-152">Başarılı</span><span class="sxs-lookup"><span data-stu-id="1ec84-152">Success</span></span> | <span data-ttu-id="1ec84-153">Kimlik bilgileri başarıyla alındı ve stdout yazılır.</span><span class="sxs-lookup"><span data-stu-id="1ec84-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="1ec84-154">1.</span><span class="sxs-lookup"><span data-stu-id="1ec84-154">1</span></span> | <span data-ttu-id="1ec84-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="1ec84-155">ProviderNotApplicable</span></span> | <span data-ttu-id="1ec84-156">Geçerli sağlayıcı verili URI için kimlik bilgilerini sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1ec84-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="1ec84-157">2</span><span class="sxs-lookup"><span data-stu-id="1ec84-157">2</span></span> | <span data-ttu-id="1ec84-158">Hata</span><span class="sxs-lookup"><span data-stu-id="1ec84-158">Failure</span></span> | <span data-ttu-id="1ec84-159">Sağlayıcı verili URI için doğru sağlayıcısıdır, ancak kimlik bilgileri girilemez.</span><span class="sxs-lookup"><span data-stu-id="1ec84-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="1ec84-160">Bu durumda, nuget.exe kimlik doğrulaması yinelemez ve başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1ec84-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="1ec84-161">Etkileşimli oturum açma kullanıcı iptal ettiğinde tipik bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="1ec84-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="1ec84-162">Standart çıktı</span><span class="sxs-lookup"><span data-stu-id="1ec84-162">Standard output</span></span>

| <span data-ttu-id="1ec84-163">Özellik</span><span class="sxs-lookup"><span data-stu-id="1ec84-163">Property</span></span> |<span data-ttu-id="1ec84-164">Notlar</span><span class="sxs-lookup"><span data-stu-id="1ec84-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="1ec84-165">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="1ec84-165">Username</span></span> | <span data-ttu-id="1ec84-166">Kimliği doğrulanmış istekler için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="1ec84-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="1ec84-167">Parola</span><span class="sxs-lookup"><span data-stu-id="1ec84-167">Password</span></span> | <span data-ttu-id="1ec84-168">Kimliği doğrulanmış istekler için parola.</span><span class="sxs-lookup"><span data-stu-id="1ec84-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="1ec84-169">İleti</span><span class="sxs-lookup"><span data-stu-id="1ec84-169">Message</span></span> | <span data-ttu-id="1ec84-170">İsteğe bağlı ayrıntıları hakkında ek ayrıntılar hatası durumlarda yalnızca göstermek için kullanılan yanıt.</span><span class="sxs-lookup"><span data-stu-id="1ec84-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="1ec84-171">Örnek stdout:</span><span class="sxs-lookup"><span data-stu-id="1ec84-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="1ec84-172">Bir kimlik bilgisi sağlayıcı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="1ec84-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="1ec84-173">Şu anda, özel kimlik bilgisi sağlayıcıları hata ayıklama için NuGet kadar doğrudan destek sağlamaz; [sorun 4598](https://github.com/NuGet/Home/issues/4598) bu iş izleme.</span><span class="sxs-lookup"><span data-stu-id="1ec84-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="1ec84-174">Şunları da yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1ec84-174">You can also do the following:</span></span>

- <span data-ttu-id="1ec84-175">Nuget.exe ile Çalıştır `-verbosity` ayrıntılı çıktı incelemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="1ec84-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="1ec84-176">Hata ayıklama iletileri ekleme `stdout` uygun yerlerde.</span><span class="sxs-lookup"><span data-stu-id="1ec84-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="1ec84-177">3.3 ya da daha yüksek nuget.exe kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1ec84-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="1ec84-178">Bu kod parçacığı ile başlangıçta hata ayıklayıcı Ekle:</span><span class="sxs-lookup"><span data-stu-id="1ec84-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="1ec84-179">Daha fazla yardım için [bir destek isteği bir nuget.org göndermek](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="1ec84-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
