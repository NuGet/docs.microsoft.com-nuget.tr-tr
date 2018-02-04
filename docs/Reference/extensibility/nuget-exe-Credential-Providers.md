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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="3c325-104">Akışları nuget.exe kimlik bilgisi sağlayıcıları ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3c325-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="3c325-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="3c325-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="3c325-106">Zaman `nuget.exe` akış ile kimlik doğrulaması için kimlik bilgileri gerekiyor kendileri için aşağıdaki şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="3c325-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="3c325-107">NuGet ilk arar kimlik bilgilerini `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="3c325-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="3c325-108">NuGet sonra aşağıda verilen sıralama tabi eklenti kimlik bilgisi sağlayıcıları kullanır.</span><span class="sxs-lookup"><span data-stu-id="3c325-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="3c325-109">(Ve örnek [Visual Studio Team Services kimlik bilgisi sağlayıcısı](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="3c325-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="3c325-110">NuGet sonra kullanıcıdan kimlik bilgilerini komut satırında ister.</span><span class="sxs-lookup"><span data-stu-id="3c325-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="3c325-111">Burada açıklanan kimlik bilgisi sağlayıcıları yalnızca iş Not `nuget.exe` 'dotnet geri yükleme' ya da Visual Studio içinde değil.</span><span class="sxs-lookup"><span data-stu-id="3c325-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="3c325-112">Visual Studio ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe Visual Studio için kimlik bilgisi sağlayıcıları](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="3c325-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="3c325-113">nuget.exe kimlik bilgisi sağlayıcıları 3 şekillerde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3c325-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="3c325-114">**Genel olarak**: bir kimlik bilgisi sağlayıcısı tüm örnekleri kullanılabilir hale getirmek için `nuget.exe` geçerli kullanıcının profili altında çalıştırmak, ekleyin `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="3c325-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="3c325-115">Oluşturmanız gerekebilir `CredentialProviders` klasör.</span><span class="sxs-lookup"><span data-stu-id="3c325-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="3c325-116">Kimlik bilgisi sağlayıcıları kökünde yüklenebilir `CredentialProviders` klasörü veya bir alt klasör içinde.</span><span class="sxs-lookup"><span data-stu-id="3c325-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="3c325-117">Bir kimlik bilgisi sağlayıcısı birden çok dosya derlemeleri varsa, alt klasörler düzenlenmiş sağlayıcıları tutmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c325-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="3c325-118">**Bir ortam değişkeni gelen**: kimlik bilgisi sağlayıcıları herhangi bir yerde depolanabilir ve için erişilebilir hale `nuget.exe` ayarlayarak `%NUGET_CREDENTIALPROVIDERS_PATH%` Sağlayıcısı'nın konumunu ortam değişkenine.</span><span class="sxs-lookup"><span data-stu-id="3c325-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="3c325-119">Bu değişken noktalı virgülle ayrılmış listesini olabilir (örneğin, `path1;path2`) birden çok konumda varsa.</span><span class="sxs-lookup"><span data-stu-id="3c325-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="3c325-120">**Nuget.exe yanında**: nuget.exe kimlik bilgisi sağlayıcıları, aynı klasörde yerleştirilebilen `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="3c325-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="3c325-121">Kimlik bilgisi sağlayıcıları yüklenirken `nuget.exe` adlı dosyası için sırasıyla Yukarıdaki konumlarda arar `credentialprovider*.exe`, bulunan sırada bu dosyaları yükler.</span><span class="sxs-lookup"><span data-stu-id="3c325-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="3c325-122">Birden çok kimlik bilgisi sağlayıcısı aynı klasörde varsa, bunlar alfabetik sırada yüklü.</span><span class="sxs-lookup"><span data-stu-id="3c325-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="3c325-123">Nuget.exe kimlik bilgisi sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c325-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="3c325-124">Komut satırı yürütülebilir dosyasını bir kimlik bilgisi sağlayıcıdır biçiminde adlı `CredentialProvider*.exe`, girişleri toplar, uygun kimlik bilgilerini alır ve standart çıktı ve uygun çıkış durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3c325-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="3c325-125">Bir sağlayıcı aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3c325-125">A provider must do the following:</span></span>

- <span data-ttu-id="3c325-126">Bu kimlik bilgileri hedeflenen URI'sini kimlik bilgisi edinme başlatmadan önce sağlayıp sağlayamayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="3c325-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="3c325-127">Yoksa, durum kodu 1 hiçbir kimlik bilgileriyle döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="3c325-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="3c325-128">Değişiklik `Nuget.Config` (örneğin var. kimlik bilgilerini ayarlama).</span><span class="sxs-lookup"><span data-stu-id="3c325-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="3c325-129">Tanıtıcı HTTP proxy yapılandırması kendi olarak NuGet üzerinde eklentisi için proxy bilgileri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="3c325-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="3c325-130">Kimlik bilgileri veya hata ayrıntıları için iade `nuget.exe` UTF-8 kodlaması kullanarak stdout, JSON yanıt nesnesi (aşağıya bakın) yazarak.</span><span class="sxs-lookup"><span data-stu-id="3c325-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="3c325-131">İsteğe bağlı olarak ek izleme günlüğü stderr'e yayma.</span><span class="sxs-lookup"><span data-stu-id="3c325-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="3c325-132">Ayrıntı düzeyleri "normal" veya "ayrıntılı" gibi izlemeleri NuGet tarafından konsola echoed bu yana hiçbir gizli stderr, herhangi bir zamanda yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c325-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="3c325-133">NuGet gelecekteki sürümleriyle ileriye dönük uyumluluğu sağlama beklenmeyen parametreleri sayılır.</span><span class="sxs-lookup"><span data-stu-id="3c325-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="3c325-134">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="3c325-134">Input parameters</span></span>

| <span data-ttu-id="3c325-135">Parametre/anahtarı</span><span class="sxs-lookup"><span data-stu-id="3c325-135">Parameter/Switch</span></span> |<span data-ttu-id="3c325-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3c325-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="3c325-137">URI {value}</span><span class="sxs-lookup"><span data-stu-id="3c325-137">Uri {value}</span></span> | <span data-ttu-id="3c325-138">Paket Kaynak URI gerektiren kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3c325-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="3c325-139">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="3c325-139">NonInteractive</span></span> | <span data-ttu-id="3c325-140">Varsa, sağlayıcı etkileşimli istemleri kesmez.</span><span class="sxs-lookup"><span data-stu-id="3c325-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="3c325-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="3c325-141">IsRetry</span></span> | <span data-ttu-id="3c325-142">Varsa, bu deneme daha önce başarısız girişim yinelenmesini olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3c325-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="3c325-143">Sağlayıcılar genellikle tüm mevcut önbelleği atlama ve yeni kimlik bilgilerini mümkünse sormasına emin olmak için bu bayrağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c325-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="3c325-144">Ayrıntı {value}</span><span class="sxs-lookup"><span data-stu-id="3c325-144">Verbosity {value}</span></span> | <span data-ttu-id="3c325-145">Varsa, aşağıdaki değerlerden birini: "normal", "quiet" veya "ayrıntılı".</span><span class="sxs-lookup"><span data-stu-id="3c325-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="3c325-146">Herhangi bir değer belirtilirse, "normal" varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3c325-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="3c325-147">Sağlayıcıları bu isteğe bağlı günlüğe kaydetme düzeyini belirtisi standart hata akışı yaymak üzere kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3c325-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="3c325-148">Çıkış kodları</span><span class="sxs-lookup"><span data-stu-id="3c325-148">Exit codes</span></span>

| <span data-ttu-id="3c325-149">Kod</span><span class="sxs-lookup"><span data-stu-id="3c325-149">Code</span></span> |<span data-ttu-id="3c325-150">Sonuç</span><span class="sxs-lookup"><span data-stu-id="3c325-150">Result</span></span> | <span data-ttu-id="3c325-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3c325-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="3c325-152">0</span><span class="sxs-lookup"><span data-stu-id="3c325-152">0</span></span> | <span data-ttu-id="3c325-153">Başarılı</span><span class="sxs-lookup"><span data-stu-id="3c325-153">Success</span></span> | <span data-ttu-id="3c325-154">Kimlik bilgileri başarıyla alındı ve stdout yazılır.</span><span class="sxs-lookup"><span data-stu-id="3c325-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="3c325-155">1.</span><span class="sxs-lookup"><span data-stu-id="3c325-155">1</span></span> | <span data-ttu-id="3c325-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="3c325-156">ProviderNotApplicable</span></span> | <span data-ttu-id="3c325-157">Geçerli sağlayıcı verili URI için kimlik bilgilerini sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="3c325-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="3c325-158">2</span><span class="sxs-lookup"><span data-stu-id="3c325-158">2</span></span> | <span data-ttu-id="3c325-159">Hata</span><span class="sxs-lookup"><span data-stu-id="3c325-159">Failure</span></span> | <span data-ttu-id="3c325-160">Sağlayıcı verili URI için doğru sağlayıcısıdır, ancak kimlik bilgileri girilemez.</span><span class="sxs-lookup"><span data-stu-id="3c325-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="3c325-161">Bu durumda, nuget.exe kimlik doğrulaması yinelemez ve başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="3c325-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="3c325-162">Etkileşimli oturum açma kullanıcı iptal ettiğinde tipik bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="3c325-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="3c325-163">Standart çıktı</span><span class="sxs-lookup"><span data-stu-id="3c325-163">Standard output</span></span>

| <span data-ttu-id="3c325-164">Özellik</span><span class="sxs-lookup"><span data-stu-id="3c325-164">Property</span></span> |<span data-ttu-id="3c325-165">Notlar</span><span class="sxs-lookup"><span data-stu-id="3c325-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="3c325-166">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3c325-166">Username</span></span> | <span data-ttu-id="3c325-167">Kimliği doğrulanmış istekler için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="3c325-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="3c325-168">Parola</span><span class="sxs-lookup"><span data-stu-id="3c325-168">Password</span></span> | <span data-ttu-id="3c325-169">Kimliği doğrulanmış istekler için parola.</span><span class="sxs-lookup"><span data-stu-id="3c325-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="3c325-170">İleti</span><span class="sxs-lookup"><span data-stu-id="3c325-170">Message</span></span> | <span data-ttu-id="3c325-171">İsteğe bağlı ayrıntıları hakkında ek ayrıntılar hatası durumlarda yalnızca göstermek için kullanılan yanıt.</span><span class="sxs-lookup"><span data-stu-id="3c325-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="3c325-172">Örnek stdout:</span><span class="sxs-lookup"><span data-stu-id="3c325-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="3c325-173">Bir kimlik bilgisi sağlayıcı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="3c325-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="3c325-174">Şu anda, özel kimlik bilgisi sağlayıcıları hata ayıklama için NuGet kadar doğrudan destek sağlamaz; [sorun 4598](https://github.com/NuGet/Home/issues/4598) bu iş izleme.</span><span class="sxs-lookup"><span data-stu-id="3c325-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="3c325-175">Şunları da yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3c325-175">You can also do the following:</span></span>

- <span data-ttu-id="3c325-176">Nuget.exe ile Çalıştır `-verbosity` ayrıntılı çıktı incelemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="3c325-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="3c325-177">Hata ayıklama iletileri ekleme `stdout` uygun yerlerde.</span><span class="sxs-lookup"><span data-stu-id="3c325-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="3c325-178">3.3 ya da daha yüksek nuget.exe kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3c325-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="3c325-179">Bu kod parçacığı ile başlangıçta hata ayıklayıcı Ekle:</span><span class="sxs-lookup"><span data-stu-id="3c325-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="3c325-180">Daha fazla yardım için [bir destek isteği bir nuget.org göndermek](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="3c325-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
