---
title: NuGet. config dosyası başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, Solution ve packageSource bölümlerini içeren NuGet. config dosyası başvurusu.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: a2955617b899bfadab42d1ae98dd20c8fc6ddca9
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020046"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="f5b35-103">NuGet. config başvurusu</span><span class="sxs-lookup"><span data-stu-id="f5b35-103">nuget.config reference</span></span>

<span data-ttu-id="f5b35-104">NuGet davranışı, [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi `NuGet.Config` farklı dosyalardaki ayarlarla denetlenir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="f5b35-105">`nuget.config`, daha sonra bu konuda açıklanan bölüm öğelerini içeren `<configuration>` üst düzey bir düğüm içeren bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="f5b35-106">Her bölüm sıfır veya daha fazla öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-106">Each section contains zero or more items.</span></span> <span data-ttu-id="f5b35-107">[Örnekler yapılandırma dosyasına](#example-config-file)bakın.</span><span class="sxs-lookup"><span data-stu-id="f5b35-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="f5b35-108">Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="f5b35-109">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-109">config section</span></span>

<span data-ttu-id="f5b35-110">Komutu kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir. [ `nuget config` ](../reference/cli-reference/cli-ref-config.md)</span><span class="sxs-lookup"><span data-stu-id="f5b35-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="f5b35-111">`dependencyVersion`ve `repositoryPath` yalnızca kullanan `packages.config`projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="f5b35-112">`globalPackagesFolder`yalnızca PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="f5b35-113">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-113">Key</span></span> | <span data-ttu-id="f5b35-114">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-115">dependencyversion (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="f5b35-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="f5b35-116">Anahtar doğrudan `DependencyVersion` belirtilmediğinde, paket yükleme, geri yükleme ve güncelleştirme için varsayılan değer. `-DependencyVersion`</span><span class="sxs-lookup"><span data-stu-id="f5b35-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="f5b35-117">Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="f5b35-118">Değerler,,, .`Highest` `Lowest` `HighestPatch` `HighestMinor`</span><span class="sxs-lookup"><span data-stu-id="f5b35-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="f5b35-119">globalPackagesFolder (yalnızca PackageReference kullanan projeler)</span><span class="sxs-lookup"><span data-stu-id="f5b35-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="f5b35-120">Varsayılan genel paketler klasörünün konumu.</span><span class="sxs-lookup"><span data-stu-id="f5b35-120">The location of the default global packages folder.</span></span> <span data-ttu-id="f5b35-121">Varsayılan `%userprofile%\.nuget\packages` değer (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="f5b35-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="f5b35-122">Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="f5b35-123">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="f5b35-124">depoyolu (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="f5b35-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="f5b35-125">Varsayılan `$(Solutiondir)/packages` klasör yerine NuGet paketlerinin yükleneceği konum.</span><span class="sxs-lookup"><span data-stu-id="f5b35-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="f5b35-126">Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="f5b35-127">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="f5b35-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="f5b35-128">defaultPushSource</span></span> | <span data-ttu-id="f5b35-129">Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f5b35-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="f5b35-130">http_proxy http_proxy. User http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="f5b35-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="f5b35-131">Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` biçiminde`http://<username>:<password>@<domain>`olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="f5b35-132">Parolalar şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="f5b35-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="f5b35-133">İçin `no_proxy`, değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="f5b35-134">Bu değerler için http_proxy ve no_proxy ortam değişkenlerini alternatif olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5b35-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="f5b35-135">Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="f5b35-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="f5b35-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="f5b35-136">signatureValidationMode</span></span> | <span data-ttu-id="f5b35-137">Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="f5b35-138">`accept`Değerler, .`require`</span><span class="sxs-lookup"><span data-stu-id="f5b35-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="f5b35-139">Varsayılan olarak `accept`.</span><span class="sxs-lookup"><span data-stu-id="f5b35-139">Defaults to `accept`.</span></span>

<span data-ttu-id="f5b35-140">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="f5b35-141">Bindingyönlendirmeler bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-141">bindingRedirects section</span></span>

<span data-ttu-id="f5b35-142">Bir paket yüklendiğinde NuGet 'in otomatik bağlama yeniden yönlendirmelerini yapıp yönlendirmeyeceğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="f5b35-143">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-143">Key</span></span> | <span data-ttu-id="f5b35-144">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-145">Atla</span><span class="sxs-lookup"><span data-stu-id="f5b35-145">skip</span></span> | <span data-ttu-id="f5b35-146">Otomatik bağlama yeniden yönlendirmelerinin atlanıp atlanmayacağını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="f5b35-147">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-147">The default is false.</span></span> |

<span data-ttu-id="f5b35-148">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="f5b35-149">Packageresesme bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-149">packageRestore section</span></span>

<span data-ttu-id="f5b35-150">Derlemeler sırasında paket geri yüklemeyi denetler.</span><span class="sxs-lookup"><span data-stu-id="f5b35-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="f5b35-151">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-151">Key</span></span> | <span data-ttu-id="f5b35-152">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-153">etkinletir</span><span class="sxs-lookup"><span data-stu-id="f5b35-153">enabled</span></span> | <span data-ttu-id="f5b35-154">NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="f5b35-155">Ayrıca, `EnableNuGetPackageRestore` yapılandırma dosyasında bu anahtarı ayarlamak `True` yerine, ortam değişkenini bir değeriyle ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5b35-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="f5b35-156">otomatik</span><span class="sxs-lookup"><span data-stu-id="f5b35-156">automatic</span></span> | <span data-ttu-id="f5b35-157">Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="f5b35-158">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="f5b35-159">çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-159">solution section</span></span>

<span data-ttu-id="f5b35-160">Kaynak denetimine bir `packages` çözüm klasörünün eklenip eklenmeyeceğini denetler.</span><span class="sxs-lookup"><span data-stu-id="f5b35-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="f5b35-161">Bu bölüm yalnızca `nuget.config` bir çözüm klasöründeki dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="f5b35-162">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-162">Key</span></span> | <span data-ttu-id="f5b35-163">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-164">Disablesourcecontrolintefini</span><span class="sxs-lookup"><span data-stu-id="f5b35-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="f5b35-165">Kaynak denetimiyle çalışırken paketler klasörünün yoksayılıp yoksayılmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="f5b35-166">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="f5b35-166">The default value is false.</span></span> |

<span data-ttu-id="f5b35-167">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="f5b35-168">Paket kaynak bölümleri</span><span class="sxs-lookup"><span data-stu-id="f5b35-168">Package source sections</span></span>

<span data-ttu-id="f5b35-169">`packageSources` ,`packageSourceCredentials` ,,`trustedSigners`Vetüm çalışmaları birlikte çalışarak, NuGet 'in yükleme, geri yükleme ve güncelleştirme işlemleri sırasında paket depolarıyla nasıl çalıştığını yapılandırır. `disabledPackageSources` `apikeys` `activePackageSource`</span><span class="sxs-lookup"><span data-stu-id="f5b35-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="f5b35-170">[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)Komutu genellikle Bu`apikeys` ayarları yönetmek için kullanılır, ancak komutu kullanılarak yönetilir ve komutu kullanılarak yönetilir. [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md)</span><span class="sxs-lookup"><span data-stu-id="f5b35-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="f5b35-171">Nuget.org için kaynak URL 'sinin olduğunu `https://api.nuget.org/v3/index.json`unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f5b35-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="f5b35-172">packagesonak</span><span class="sxs-lookup"><span data-stu-id="f5b35-172">packageSources</span></span>

<span data-ttu-id="f5b35-173">Bilinen tüm paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="f5b35-173">Lists all known package sources.</span></span> <span data-ttu-id="f5b35-174">Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="f5b35-175">NuGet, kullanan `packages.config`projelerle ilgili güncelleştirme ve güncelleştirme işlemlerine yönelik kaynakların sırasını duyar.</span><span class="sxs-lookup"><span data-stu-id="f5b35-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="f5b35-176">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-176">Key</span></span> | <span data-ttu-id="f5b35-177">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-178">(paket kaynağına atanacak ad)</span><span class="sxs-lookup"><span data-stu-id="f5b35-178">(name to assign to the package source)</span></span> | <span data-ttu-id="f5b35-179">Paket kaynağının yolu veya URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="f5b35-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="f5b35-180">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="f5b35-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="f5b35-181">packageSourceCredentials</span></span>

<span data-ttu-id="f5b35-182">Genellikle `-username` ve `-password` anahtarlarıyla belirtilenkaynaklariçinKullanıcıadlarınıveparolalarıdepolar.`nuget sources`</span><span class="sxs-lookup"><span data-stu-id="f5b35-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="f5b35-183">`-storepasswordincleartext` Seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="f5b35-184">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-184">Key</span></span> | <span data-ttu-id="f5b35-185">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-186">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="f5b35-186">username</span></span> | <span data-ttu-id="f5b35-187">Kaynağın düz metin olarak Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="f5b35-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="f5b35-188">password</span><span class="sxs-lookup"><span data-stu-id="f5b35-188">password</span></span> | <span data-ttu-id="f5b35-189">Kaynak için şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="f5b35-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="f5b35-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="f5b35-190">cleartextpassword</span></span> | <span data-ttu-id="f5b35-191">Kaynak için şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="f5b35-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="f5b35-192">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f5b35-192">**Example:**</span></span>

<span data-ttu-id="f5b35-193">Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar ile `_x0020_`değiştirilmiştir).</span><span class="sxs-lookup"><span data-stu-id="f5b35-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="f5b35-194">Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="f5b35-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="f5b35-195">Şifrelenmemiş parolalar kullanırken:</span><span class="sxs-lookup"><span data-stu-id="f5b35-195">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="f5b35-196">apikeys tuşları</span><span class="sxs-lookup"><span data-stu-id="f5b35-196">apikeys</span></span>

<span data-ttu-id="f5b35-197">Komutuyla ayarlanan API anahtarı kimlik doğrulaması kullanan kaynaklar için anahtarları depolar. [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)</span><span class="sxs-lookup"><span data-stu-id="f5b35-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="f5b35-198">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-198">Key</span></span> | <span data-ttu-id="f5b35-199">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-200">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="f5b35-200">(source URL)</span></span> | <span data-ttu-id="f5b35-201">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f5b35-201">The encrypted API key.</span></span> |

<span data-ttu-id="f5b35-202">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="f5b35-203">disabledpackagesonak</span><span class="sxs-lookup"><span data-stu-id="f5b35-203">disabledPackageSources</span></span>

<span data-ttu-id="f5b35-204">Şu anda devre dışı olan kaynaklar tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="f5b35-204">Identified currently disabled sources.</span></span> <span data-ttu-id="f5b35-205">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-205">May be empty.</span></span>

| <span data-ttu-id="f5b35-206">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-206">Key</span></span> | <span data-ttu-id="f5b35-207">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-208">(kaynağın adı)</span><span class="sxs-lookup"><span data-stu-id="f5b35-208">(name of source)</span></span> | <span data-ttu-id="f5b35-209">Kaynağın devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="f5b35-210">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f5b35-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="f5b35-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="f5b35-211">activePackageSource</span></span>

<span data-ttu-id="f5b35-212">*(yalnızca 2. x, 3. x + ' de kullanım dışı)*</span><span class="sxs-lookup"><span data-stu-id="f5b35-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="f5b35-213">Şu anda etkin olan kaynağı tanımlar veya tüm kaynakların toplamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="f5b35-214">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-214">Key</span></span> | <span data-ttu-id="f5b35-215">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-216">(kaynağın adı) veya`All`</span><span class="sxs-lookup"><span data-stu-id="f5b35-216">(name of source) or `All`</span></span> | <span data-ttu-id="f5b35-217">Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur.</span><span class="sxs-lookup"><span data-stu-id="f5b35-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="f5b35-218">Eğer `All`değeri, aksi durumda `(Aggregate source)` devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="f5b35-219">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="f5b35-220">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-220">trustedSigners section</span></span>

<span data-ttu-id="f5b35-221">Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar.</span><span class="sxs-lookup"><span data-stu-id="f5b35-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="f5b35-222">Kullanıcı `signatureValidationMode` öğesine`require`ayarlandığında bu liste boş olamaz.</span><span class="sxs-lookup"><span data-stu-id="f5b35-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="f5b35-223">Bu bölüm, [ `nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="f5b35-224">**Şema**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-224">**Schema**:</span></span>

<span data-ttu-id="f5b35-225">Güvenilen bir imzalayan, belirli bir İmzalayanın `certificate` tanımlayan tüm sertifikaları içeren bir öğe koleksiyonuna sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="f5b35-226">Güvenilen bir imzalayan ya da `Author` `Repository`olabilir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="f5b35-227">Güvenilen bir *Depo* Ayrıca depo `serviceIndex` için (geçerli `https` bir URI olması gerekir) belirtir ve isteğe bağlı olarak, bu belirli `owners` bir istemciden güvenilir bir şekilde kısıtlamak için noktalı virgülle ayrılmış bir liste belirtebilir Depo.</span><span class="sxs-lookup"><span data-stu-id="f5b35-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="f5b35-228">Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları, `SHA256`ve `SHA384` `SHA512`' dir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="f5b35-229">Bir `certificate` ise, imza `true` doğrulamasının parçası olarak sertifika zincirini oluştururken, belirtilen sertifikanın güvenilmeyen bir köke zincirine izin verileceğini belirtir `allowUntrustedRoot` .</span><span class="sxs-lookup"><span data-stu-id="f5b35-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="f5b35-230">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-230">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="f5b35-231">fallbackPackageFolders bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="f5b35-232">*(3,5 +)* Paket, geri dönüş klasörlerinde bulunursa hiçbir işin gerçekleştirilmesi gerekmediği için paketleri önceden yüklemeye yönelik bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5b35-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="f5b35-233">Geri dönüş paketi klasörleri, genel paket klasörüyle aynı klasöre ve dosya yapısına sahiptir: *. nupkg* var ve tüm dosyalar ayıklandı.</span><span class="sxs-lookup"><span data-stu-id="f5b35-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="f5b35-234">Bu yapılandırma için arama mantığı:</span><span class="sxs-lookup"><span data-stu-id="f5b35-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="f5b35-235">Paketin/sürümün zaten indirildiğini görmek için genel paket klasörüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f5b35-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="f5b35-236">Paket/sürüm eşleşmesi için geri dönüş klasörlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="f5b35-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="f5b35-237">Her iki arama başarılı olursa, indirme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f5b35-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="f5b35-238">Bir eşleşme bulunmazsa, NuGet dosya kaynaklarını ve ardından http kaynakları ' nı denetleyip paketleri indirir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="f5b35-239">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-239">Key</span></span> | <span data-ttu-id="f5b35-240">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-241">(geri dönüş klasörünün adı)</span><span class="sxs-lookup"><span data-stu-id="f5b35-241">(name of fallback folder)</span></span> | <span data-ttu-id="f5b35-242">Geri dönüş klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="f5b35-242">Path to fallback folder.</span></span> |

<span data-ttu-id="f5b35-243">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="f5b35-244">packageManagement bölümü</span><span class="sxs-lookup"><span data-stu-id="f5b35-244">packageManagement section</span></span>

<span data-ttu-id="f5b35-245">Varsayılan paket yönetim biçimini Package *. config* ya da packagereference olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f5b35-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="f5b35-246">SDK stilindeki projeler her zaman PackageReference kullanır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="f5b35-247">Anahtar</span><span class="sxs-lookup"><span data-stu-id="f5b35-247">Key</span></span> | <span data-ttu-id="f5b35-248">Değer</span><span class="sxs-lookup"><span data-stu-id="f5b35-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f5b35-249">biçim</span><span class="sxs-lookup"><span data-stu-id="f5b35-249">format</span></span> | <span data-ttu-id="f5b35-250">Varsayılan paket yönetimi biçimini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="f5b35-251">İse `1`format, packagereference olur.</span><span class="sxs-lookup"><span data-stu-id="f5b35-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="f5b35-252">İse `0`, biçimi *Packages. config*olur.</span><span class="sxs-lookup"><span data-stu-id="f5b35-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="f5b35-253">devre dışı</span><span class="sxs-lookup"><span data-stu-id="f5b35-253">disabled</span></span> | <span data-ttu-id="f5b35-254">İlk paket yüklemesi sırasında varsayılan bir paket biçimi seçme isteminin gösterilip gösterilmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f5b35-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="f5b35-255">`False`istemi gizler.</span><span class="sxs-lookup"><span data-stu-id="f5b35-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="f5b35-256">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="f5b35-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="f5b35-257">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="f5b35-257">Using environment variables</span></span>

<span data-ttu-id="f5b35-258">Çalışma zamanında ayarları uygulamak için değerler `nuget.config` (NuGet 3.4 +) cinsinden ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5b35-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="f5b35-259">Örneğin, `HOME` Windows üzerindeki ortam değişkeni olarak `c:\users\username`ayarlandıysa `%HOME%\NuGetRepository` , yapılandırma dosyasındaki değeri olarak `c:\users\username\NuGetRepository`çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="f5b35-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="f5b35-260">Benzer şekilde, Mac/Linux `%HOME%/NuGetRepository` , olarak `/home/myStuff`ayarlanmışsa yapılandırma dosyasında olarak `/home/myStuff/NuGetRepository`çözümlenir. `HOME`</span><span class="sxs-lookup"><span data-stu-id="f5b35-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="f5b35-261">Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="f5b35-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="f5b35-262">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="f5b35-262">Example config file</span></span>

<span data-ttu-id="f5b35-263">Aşağıda, bir dizi `nuget.config` ayarı gösteren örnek bir dosya verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f5b35-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
