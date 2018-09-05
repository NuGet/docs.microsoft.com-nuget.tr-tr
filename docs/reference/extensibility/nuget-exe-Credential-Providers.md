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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="ade8e-103">Nuget.exe kimlik bilgileri sağlayıcıları ile kimlik doğrulama akışları</span><span class="sxs-lookup"><span data-stu-id="ade8e-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="ade8e-104">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="ade8e-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="ade8e-105">Zaman `nuget.exe` akış ile kimlik doğrulaması için kimlik bilgileri gerekiyor kendileri için şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="ade8e-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="ade8e-106">NuGet kimlik bilgileri için önce arar `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ade8e-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="ade8e-107">NuGet, daha sonra aşağıda verilen sıralama tabi eklenti kimlik bilgisi sağlayıcıları kullanır.</span><span class="sxs-lookup"><span data-stu-id="ade8e-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="ade8e-108">(Ve örnek [Visual Studio Team Services kimlik bilgisi sağlayıcısı](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="ade8e-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="ade8e-109">NuGet daha sonra kullanıcıdan komut satırında kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="ade8e-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="ade8e-110">Burada açıklanan kimlik bilgisi sağlayıcıları yalnızca iş Not `nuget.exe` 'dotnet restore' veya Visual Studio içinde değil.</span><span class="sxs-lookup"><span data-stu-id="ade8e-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="ade8e-111">Visual Studio ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe Visual Studio için kimlik bilgileri sağlayıcısı](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ade8e-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="ade8e-112">nuget.exe kimlik bilgileri sağlayıcıları 3 şekilde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="ade8e-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="ade8e-113">**Genel olarak**: kimlik bilgisi Sağlayıcı'nın tüm örnekleri kullanılabilir hale getirmek için `nuget.exe` ekleyin, geçerli kullanıcının profilini altında çalıştırma `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="ade8e-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="ade8e-114">Oluşturmanız gerekebilir `CredentialProviders` klasör.</span><span class="sxs-lookup"><span data-stu-id="ade8e-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="ade8e-115">Kimlik bilgisi sağlayıcıları kökünde yüklenebilir `CredentialProviders` klasörü veya bir alt klasör içinde.</span><span class="sxs-lookup"><span data-stu-id="ade8e-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="ade8e-116">Bir kimlik bilgisi sağlayıcısı, birden çok dosya derlemeleri varsa, sağlayıcıları düzenli tutmak için alt klasörleri'ni kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ade8e-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="ade8e-117">**Bir ortam değişkeninden**: kimlik bilgisi sağlayıcıları herhangi bir yerde depolanabilir ve için erişilebilir hale `nuget.exe` ayarlayarak `%NUGET_CREDENTIALPROVIDERS_PATH%` ortam değişkeni sağlayıcı konumu.</span><span class="sxs-lookup"><span data-stu-id="ade8e-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="ade8e-118">Bu değişken bir noktalı virgülle ayrılmış liste olabilir (örneğin, `path1;path2`) birden çok konumda varsa.</span><span class="sxs-lookup"><span data-stu-id="ade8e-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="ade8e-119">**Nuget.exe yanı sıra**: nuget.exe kimlik bilgileri sağlayıcısı, aynı klasörde yerleştirilebileceğini `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ade8e-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="ade8e-120">Kimlik bilgisi sağlayıcıları yüklenirken `nuget.exe` adlı herhangi bir dosya için sırayla yukarıdaki konumları arar `credentialprovider*.exe`, daha sonra bu dosyaları bulundukları sıraya yükler.</span><span class="sxs-lookup"><span data-stu-id="ade8e-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="ade8e-121">Birden çok kimlik bilgisi sağlayıcı aynı klasörde varsa, alfabetik olarak yüklendi.</span><span class="sxs-lookup"><span data-stu-id="ade8e-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="ade8e-122">Nuget.exe kimlik bilgileri sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ade8e-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="ade8e-123">Komut satırı yürütülebilir dosyasını bir kimlik bilgisi sağlayıcıdır biçiminde adlandırılmış `CredentialProvider*.exe`, girişleri toplar, uygun kimlik bilgilerini alır ve ardından standart çıktı ve uygun çıkış durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ade8e-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="ade8e-124">Bir sağlayıcı aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="ade8e-124">A provider must do the following:</span></span>

- <span data-ttu-id="ade8e-125">Bu kimlik bilgileri hedeflenen URI için kimlik bilgilerini almayı başlatmadan önce sağlayıp sağlayamayacağını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="ade8e-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="ade8e-126">Aksi durumda, durum kodu 1 ile kimlik bilgileri döndürmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade8e-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="ade8e-127">Değişiklik `Nuget.Config` (örneğin, burada kimlik bilgilerini ayarlama).</span><span class="sxs-lookup"><span data-stu-id="ade8e-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="ade8e-128">Tanıtıcı HTTP proxy yapılandırması kendi olarak NuGet üzerindeki eklentisi için proxy bilgileri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ade8e-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="ade8e-129">Kimlik bilgileri veya hata ayrıntılarını dönüş `nuget.exe` Stdout'a UTF-8 kodlaması kullanarak bir JSON yanıtı nesnesi (aşağıya bakın) yazarak.</span><span class="sxs-lookup"><span data-stu-id="ade8e-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="ade8e-130">İsteğe bağlı olarak ek izleme günlüğü stderr'e gösterin.</span><span class="sxs-lookup"><span data-stu-id="ade8e-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="ade8e-131">Ayrıntı düzeylerinde "normal" veya "ayrıntılı", bu tür izleme tarafından NuGet konsola okunmaz olduğundan gizli dizi stderr için hiç olmadığı kadar yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ade8e-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="ade8e-132">NuGet gelecekteki sürümleriyle ileriye dönük uyumluluk sağlama beklenmeyen parametre yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="ade8e-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="ade8e-133">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="ade8e-133">Input parameters</span></span>

| <span data-ttu-id="ade8e-134">Parametre/anahtarı</span><span class="sxs-lookup"><span data-stu-id="ade8e-134">Parameter/Switch</span></span> |<span data-ttu-id="ade8e-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ade8e-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="ade8e-136">URI {value}</span><span class="sxs-lookup"><span data-stu-id="ade8e-136">Uri {value}</span></span> | <span data-ttu-id="ade8e-137">Paket Kaynak URI gerektiren kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ade8e-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="ade8e-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ade8e-138">NonInteractive</span></span> | <span data-ttu-id="ade8e-139">Varsa, sağlayıcı etkileşimli istemleri kesmez.</span><span class="sxs-lookup"><span data-stu-id="ade8e-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="ade8e-140">isRetry</span><span class="sxs-lookup"><span data-stu-id="ade8e-140">IsRetry</span></span> | <span data-ttu-id="ade8e-141">Varsa, bu deneme daha önce başarısız bir girişimden yinelenmesini olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ade8e-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="ade8e-142">Sağlayıcıları, genellikle tüm mevcut önbelleğini atla ve mümkünse yeni kimlik bilgilerinizi ister emin olmak için bu bayrağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ade8e-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="ade8e-143">{Value} ayrıntı düzeyi</span><span class="sxs-lookup"><span data-stu-id="ade8e-143">Verbosity {value}</span></span> | <span data-ttu-id="ade8e-144">Varsa, aşağıdaki değerlerden biri: "normal", "quiet" veya "ayrıntılı".</span><span class="sxs-lookup"><span data-stu-id="ade8e-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="ade8e-145">Hiçbir değer sağlanmazsa, "normal" varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="ade8e-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="ade8e-146">Sağlayıcıları bu için standart hata akışı yaymak için bir isteğe bağlı günlüğe kaydetme düzeyini göstergesi olarak kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="ade8e-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="ade8e-147">Çıkış kodları</span><span class="sxs-lookup"><span data-stu-id="ade8e-147">Exit codes</span></span>

| <span data-ttu-id="ade8e-148">Kod</span><span class="sxs-lookup"><span data-stu-id="ade8e-148">Code</span></span> |<span data-ttu-id="ade8e-149">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ade8e-149">Result</span></span> | <span data-ttu-id="ade8e-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ade8e-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="ade8e-151">0</span><span class="sxs-lookup"><span data-stu-id="ade8e-151">0</span></span> | <span data-ttu-id="ade8e-152">Başarılı</span><span class="sxs-lookup"><span data-stu-id="ade8e-152">Success</span></span> | <span data-ttu-id="ade8e-153">Kimlik bilgileri başarıyla alındı ve stdout için yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ade8e-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="ade8e-154">1.</span><span class="sxs-lookup"><span data-stu-id="ade8e-154">1</span></span> | <span data-ttu-id="ade8e-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="ade8e-155">ProviderNotApplicable</span></span> | <span data-ttu-id="ade8e-156">Geçerli sağlayıcı verilen URI için kimlik bilgileri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ade8e-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="ade8e-157">2</span><span class="sxs-lookup"><span data-stu-id="ade8e-157">2</span></span> | <span data-ttu-id="ade8e-158">hata</span><span class="sxs-lookup"><span data-stu-id="ade8e-158">Failure</span></span> | <span data-ttu-id="ade8e-159">Sağlayıcı, verilen URI için doğru sağlayıcısıdır, ancak kimlik bilgileri girilemez.</span><span class="sxs-lookup"><span data-stu-id="ade8e-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="ade8e-160">Bu durumda, nuget.exe kimlik doğrulaması yeniden denensin değil ve başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ade8e-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="ade8e-161">Bir kullanıcı bir etkileşimli oturum açma işlemi iptal ettiğinde tipik bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="ade8e-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="ade8e-162">Standart çıktı</span><span class="sxs-lookup"><span data-stu-id="ade8e-162">Standard output</span></span>

| <span data-ttu-id="ade8e-163">Özellik</span><span class="sxs-lookup"><span data-stu-id="ade8e-163">Property</span></span> |<span data-ttu-id="ade8e-164">Notlar</span><span class="sxs-lookup"><span data-stu-id="ade8e-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="ade8e-165">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ade8e-165">Username</span></span> | <span data-ttu-id="ade8e-166">Kimliği doğrulanmış istekler için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="ade8e-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="ade8e-167">Parola</span><span class="sxs-lookup"><span data-stu-id="ade8e-167">Password</span></span> | <span data-ttu-id="ade8e-168">Kimliği doğrulanmış istekler için parola.</span><span class="sxs-lookup"><span data-stu-id="ade8e-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="ade8e-169">İleti</span><span class="sxs-lookup"><span data-stu-id="ade8e-169">Message</span></span> | <span data-ttu-id="ade8e-170">Yalnızca hata durumlarda ek ayrıntıları göstermek için kullanılan yanıt hakkında isteğe bağlı ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="ade8e-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="ade8e-171">Stdout. örnek:</span><span class="sxs-lookup"><span data-stu-id="ade8e-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="ade8e-172">Bir kimlik bilgisi sağlayıcı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="ade8e-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="ade8e-173">Şu anda, özel kimlik bilgileri sağlayıcısı hata ayıklama için NuGet kadar doğrudan destek sağlamaz; [sorun 4598](https://github.com/NuGet/Home/issues/4598) bu iş izleme.</span><span class="sxs-lookup"><span data-stu-id="ade8e-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="ade8e-174">Şunları da yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ade8e-174">You can also do the following:</span></span>

- <span data-ttu-id="ade8e-175">Nuget.exe ile çalıştırma `-verbosity` ayrıntılı çıkış incelemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="ade8e-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="ade8e-176">Hata ayıklama ileti için ekleme `stdout` uygun yerlerde.</span><span class="sxs-lookup"><span data-stu-id="ade8e-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="ade8e-177">Nuget.exe 3.3 ya da daha yüksek kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ade8e-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="ade8e-178">Başlangıçta bu kod parçacığı ile hata ayıklayıcının:</span><span class="sxs-lookup"><span data-stu-id="ade8e-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="ade8e-179">Daha fazla yardım için [bir destek isteği bir nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="ade8e-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
