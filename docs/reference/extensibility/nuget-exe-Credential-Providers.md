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
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="d91c2-103">NuGet. exe kimlik bilgisi sağlayıcılarıyla akışların kimliğini doğrulama</span><span class="sxs-lookup"><span data-stu-id="d91c2-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="d91c2-104">Sürüm `3.3` `nuget.exe` belirli kimlik bilgileri sağlayıcıları için destek eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="d91c2-105">Sonrasında, tüm komut satırı senaryolarında (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) çalışan [kimlik bilgileri sağlayıcıları için](NuGet-Cross-Platform-Authentication-Plugin.md) sürüm `4.8` desteği eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="d91c2-106">`nuget.exe` yönelik tüm kimlik doğrulama yaklaşımları hakkında daha fazla bilgi için bkz. [kimliği doğrulanmış akışlardan paketleri](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) kullanma</span><span class="sxs-lookup"><span data-stu-id="d91c2-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="d91c2-107">NuGet. exe kimlik bilgisi sağlayıcısı bulma</span><span class="sxs-lookup"><span data-stu-id="d91c2-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="d91c2-108">NuGet. exe kimlik bilgileri sağlayıcıları 3 şekilde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="d91c2-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="d91c2-109">**Küresel**: bir kimlik bilgisi sağlayıcısını geçerli kullanıcının profilinde çalıştırılan tüm `nuget.exe` örnekleri için kullanılabilir hale getirmek için, `%LocalAppData%\NuGet\CredentialProviders`ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d91c2-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="d91c2-110">`CredentialProviders` klasörünü oluşturmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="d91c2-111">Kimlik bilgileri sağlayıcıları `CredentialProviders` klasörünün köküne veya bir alt klasöre yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="d91c2-112">Bir kimlik bilgisi sağlayıcısında birden çok dosya/derleme varsa, sağlayıcıları düzenli tutmak için alt klasörleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d91c2-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="d91c2-113">**Bir ortam değişkeninden**: kimlik bilgileri sağlayıcıları her yerde depolanabilir ve `%NUGET_CREDENTIALPROVIDERS_PATH%` ortam değişkeni sağlayıcı konumuna ayarlanarak `nuget.exe` erişilebilir hale getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="d91c2-114">Birden çok konumunuz varsa, bu değişken noktalı virgülle ayrılmış bir liste (örneğin, `path1;path2`) olabilir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="d91c2-115">**NuGet. exe ' nin yanı sıra**, NuGet. exe kimlik bilgileri sağlayıcıları `nuget.exe`ile aynı klasöre yerleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="d91c2-116">Kimlik bilgileri sağlayıcıları yüklenirken `nuget.exe`, Yukarıdaki konumları sırasıyla, `credentialprovider*.exe`adlı herhangi bir dosya için arar ve ardından bu dosyaları bulundukları sırada yükler.</span><span class="sxs-lookup"><span data-stu-id="d91c2-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="d91c2-117">Aynı klasörde birden çok kimlik bilgisi sağlayıcısı varsa, bunlar alfabetik sırayla yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="d91c2-118">NuGet. exe kimlik bilgisi sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d91c2-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="d91c2-119">Kimlik bilgisi sağlayıcısı, girdileri toplayan, uygun kimlik bilgilerini alan ve uygun çıkış durum kodunu ve Standart çıktıyı döndüren form `CredentialProvider*.exe`adlı bir komut satırı çalıştırılabilir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="d91c2-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="d91c2-120">Sağlayıcı aşağıdakileri yapması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d91c2-120">A provider must do the following:</span></span>

- <span data-ttu-id="d91c2-121">Kimlik bilgilerinin alımı başlatmadan önce hedeflenen URI için kimlik bilgileri sağlayıp sağlayamayacağını belirleme.</span><span class="sxs-lookup"><span data-stu-id="d91c2-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="d91c2-122">Aksi takdirde, kimlik bilgileri olmadan durum kodu 1 döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="d91c2-123">`Nuget.Config` değiştirmeyin (burada kimlik bilgilerini ayarlama gibi).</span><span class="sxs-lookup"><span data-stu-id="d91c2-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="d91c2-124">NuGet, eklentiye ara sunucu bilgileri sağlamadığından, HTTP proxy yapılandırmasını kendi kendine işleyin.</span><span class="sxs-lookup"><span data-stu-id="d91c2-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="d91c2-125">UTF-8 kodlaması kullanarak, stdout için bir JSON yanıt nesnesi (aşağıya bakın) yazarak `nuget.exe` kimlik bilgilerini veya hata ayrıntılarını döndürün.</span><span class="sxs-lookup"><span data-stu-id="d91c2-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="d91c2-126">İsteğe bağlı olarak stderr 'e ek izleme günlüğü yayın.</span><span class="sxs-lookup"><span data-stu-id="d91c2-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="d91c2-127">Ayrıntı düzeyleri "normal" veya "ayrıntılı" olarak, bu tür izlemelerin konsola NuGet tarafından yankılanmış olması nedeniyle, hiçbir gizli dizi hiçbir zaman stderr 'e yazılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d91c2-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="d91c2-128">NuGet 'in gelecekteki sürümleriyle ileri doğru uyumluluk sağlayan beklenmeyen parametreler göz ardı edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="d91c2-129">Giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="d91c2-129">Input parameters</span></span>

| <span data-ttu-id="d91c2-130">Parametre/anahtar</span><span class="sxs-lookup"><span data-stu-id="d91c2-130">Parameter/Switch</span></span> |<span data-ttu-id="d91c2-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d91c2-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="d91c2-132">URI {Value}</span><span class="sxs-lookup"><span data-stu-id="d91c2-132">Uri {value}</span></span> | <span data-ttu-id="d91c2-133">Kimlik bilgileri gerektiren paket kaynak URI 'SI.</span><span class="sxs-lookup"><span data-stu-id="d91c2-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="d91c2-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d91c2-134">NonInteractive</span></span> | <span data-ttu-id="d91c2-135">Varsa, sağlayıcı etkileşimli istemler vermez.</span><span class="sxs-lookup"><span data-stu-id="d91c2-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="d91c2-136">Isretry</span><span class="sxs-lookup"><span data-stu-id="d91c2-136">IsRetry</span></span> | <span data-ttu-id="d91c2-137">Varsa, bu girişimin daha önce başarısız olan bir girişimin yeniden denendiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d91c2-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="d91c2-138">Sağlayıcılar genellikle bu bayrağı, var olan herhangi bir önbelleği atlamalarını ve mümkünse yeni kimlik bilgilerini sormasını sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d91c2-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="d91c2-139">Ayrıntı ayrıntısı {Value}</span><span class="sxs-lookup"><span data-stu-id="d91c2-139">Verbosity {value}</span></span> | <span data-ttu-id="d91c2-140">Varsa, aşağıdaki değerlerden biri: "normal", "sessiz" veya "ayrıntılı".</span><span class="sxs-lookup"><span data-stu-id="d91c2-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="d91c2-141">Değer sağlanmazsa, varsayılan olarak "normal" olur.</span><span class="sxs-lookup"><span data-stu-id="d91c2-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="d91c2-142">Sağlayıcılar bunu standart hata akışına yayma için isteğe bağlı günlük kaydı düzeyinin bir göstergesi olarak kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d91c2-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="d91c2-143">Çıkış kodları</span><span class="sxs-lookup"><span data-stu-id="d91c2-143">Exit codes</span></span>

| <span data-ttu-id="d91c2-144">Kod</span><span class="sxs-lookup"><span data-stu-id="d91c2-144">Code</span></span> |<span data-ttu-id="d91c2-145">Sonuç</span><span class="sxs-lookup"><span data-stu-id="d91c2-145">Result</span></span> | <span data-ttu-id="d91c2-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d91c2-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="d91c2-147">0</span><span class="sxs-lookup"><span data-stu-id="d91c2-147">0</span></span> | <span data-ttu-id="d91c2-148">Başarılı</span><span class="sxs-lookup"><span data-stu-id="d91c2-148">Success</span></span> | <span data-ttu-id="d91c2-149">Kimlik bilgileri başarıyla alındı ve STDOUT 'a yazıldı.</span><span class="sxs-lookup"><span data-stu-id="d91c2-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="d91c2-150">1</span><span class="sxs-lookup"><span data-stu-id="d91c2-150">1</span></span> | <span data-ttu-id="d91c2-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="d91c2-151">ProviderNotApplicable</span></span> | <span data-ttu-id="d91c2-152">Geçerli sağlayıcı verilen URI için kimlik bilgileri sağlamıyor.</span><span class="sxs-lookup"><span data-stu-id="d91c2-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="d91c2-153">2</span><span class="sxs-lookup"><span data-stu-id="d91c2-153">2</span></span> | <span data-ttu-id="d91c2-154">Hata</span><span class="sxs-lookup"><span data-stu-id="d91c2-154">Failure</span></span> | <span data-ttu-id="d91c2-155">Sağlayıcı, belirtilen URI için doğru sağlayıcıdır, ancak kimlik bilgileri sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="d91c2-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="d91c2-156">Bu durumda, NuGet. exe kimlik doğrulamasını yeniden denemez ve başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d91c2-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="d91c2-157">Tipik bir örnek, bir kullanıcı etkileşimli oturum açmayı iptal ettiğinde olur.</span><span class="sxs-lookup"><span data-stu-id="d91c2-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="d91c2-158">Standart çıktı</span><span class="sxs-lookup"><span data-stu-id="d91c2-158">Standard output</span></span>

| <span data-ttu-id="d91c2-159">Özellik</span><span class="sxs-lookup"><span data-stu-id="d91c2-159">Property</span></span> |<span data-ttu-id="d91c2-160">Notlar</span><span class="sxs-lookup"><span data-stu-id="d91c2-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="d91c2-161">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d91c2-161">Username</span></span> | <span data-ttu-id="d91c2-162">Kimliği doğrulanmış istekler için Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="d91c2-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="d91c2-163">Parola</span><span class="sxs-lookup"><span data-stu-id="d91c2-163">Password</span></span> | <span data-ttu-id="d91c2-164">Kimliği doğrulanmış istekler için parola.</span><span class="sxs-lookup"><span data-stu-id="d91c2-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="d91c2-165">İleti</span><span class="sxs-lookup"><span data-stu-id="d91c2-165">Message</span></span> | <span data-ttu-id="d91c2-166">Yanıtla ilgili isteğe bağlı ayrıntılar, yalnızca hata durumlarında ek ayrıntıları göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d91c2-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="d91c2-167">Örnek stdout:</span><span class="sxs-lookup"><span data-stu-id="d91c2-167">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="d91c2-168">Kimlik bilgisi sağlayıcısı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="d91c2-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="d91c2-169">NuGet, özel kimlik bilgisi sağlayıcılarının hatalarını ayıklamak için çok doğrudan destek sağlamaz. [sorun 4598](https://github.com/NuGet/Home/issues/4598) , bu çalışmayı izliyor.</span><span class="sxs-lookup"><span data-stu-id="d91c2-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="d91c2-170">Şunları da yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d91c2-170">You can also do the following:</span></span>

- <span data-ttu-id="d91c2-171">Ayrıntılı çıktıyı incelemek için NuGet. exe ' yi `-verbosity` anahtarıyla çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d91c2-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="d91c2-172">Uygun yerlere `stdout` hata ayıklama iletileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d91c2-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="d91c2-173">NuGet. exe 3,3 veya üstünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d91c2-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="d91c2-174">Bu kod parçacığı ile başlangıçta hata ayıklayıcı ekle:</span><span class="sxs-lookup"><span data-stu-id="d91c2-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
