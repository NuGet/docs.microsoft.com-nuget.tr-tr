---
title: NuGet. config dosyası başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, Solution ve packageSource bölümlerini içeren NuGet. config dosyası başvurusu.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230532"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="37e1b-103">NuGet. config başvurusu</span><span class="sxs-lookup"><span data-stu-id="37e1b-103">nuget.config reference</span></span>

<span data-ttu-id="37e1b-104">NuGet davranışı, [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi farklı `NuGet.Config` veya `nuget.config` dosyalardaki ayarlarla denetlenir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="37e1b-105">`nuget.config`, daha sonra bu konuda açıklanan bölüm öğelerini içeren üst düzey bir `<configuration>` düğümü içeren bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="37e1b-106">Her bölüm sıfır veya daha fazla öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-106">Each section contains zero or more items.</span></span> <span data-ttu-id="37e1b-107">[Örnekler yapılandırma dosyasına](#example-config-file)bakın.</span><span class="sxs-lookup"><span data-stu-id="37e1b-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="37e1b-108">Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="37e1b-109">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-109">config section</span></span>

<span data-ttu-id="37e1b-110">[`nuget config` komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="37e1b-111">`dependencyVersion` ve `repositoryPath` yalnızca `packages.config`kullanan projelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="37e1b-112">`globalPackagesFolder` yalnızca PackageReference biçimi kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="37e1b-113">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-113">Key</span></span> | <span data-ttu-id="37e1b-114">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-115">dependencyVersion (yalnızca`packages.config`)</span><span class="sxs-lookup"><span data-stu-id="37e1b-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="37e1b-116">`-DependencyVersion` anahtarı doğrudan belirtilmediğinde paket yükleme, geri yükleme ve güncelleştirme için varsayılan `DependencyVersion` değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="37e1b-117">Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="37e1b-118">Değerler `Lowest`, `HighestPatch`, `HighestMinor``Highest`.</span><span class="sxs-lookup"><span data-stu-id="37e1b-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="37e1b-119">globalPackagesFolder (yalnızca PackageReference kullanan projeler)</span><span class="sxs-lookup"><span data-stu-id="37e1b-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="37e1b-120">Varsayılan genel paketler klasörünün konumu.</span><span class="sxs-lookup"><span data-stu-id="37e1b-120">The location of the default global packages folder.</span></span> <span data-ttu-id="37e1b-121">Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="37e1b-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="37e1b-122">Göreli bir yol, projeye özgü `nuget.config` dosyalarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="37e1b-123">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="37e1b-124">Depoyolu (yalnızca`packages.config`)</span><span class="sxs-lookup"><span data-stu-id="37e1b-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="37e1b-125">Varsayılan `$(Solutiondir)/packages` klasörü yerine NuGet paketlerinin yükleneceği konum.</span><span class="sxs-lookup"><span data-stu-id="37e1b-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="37e1b-126">Göreli bir yol, projeye özgü `nuget.config` dosyalarında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="37e1b-127">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="37e1b-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="37e1b-128">defaultPushSource</span></span> | <span data-ttu-id="37e1b-129">Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="37e1b-130">http_proxy http_proxy. User http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="37e1b-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="37e1b-131">Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` `http://<username>:<password>@<domain>`biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="37e1b-132">Parolalar şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="37e1b-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="37e1b-133">`no_proxy`, değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="37e1b-134">Ayrıca, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e1b-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="37e1b-135">Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="37e1b-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="37e1b-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="37e1b-136">signatureValidationMode</span></span> | <span data-ttu-id="37e1b-137">Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="37e1b-138">Değerler `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="37e1b-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="37e1b-139">
          \`accept\` değerini varsayılan olarak alır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-139">Defaults to `accept`.</span></span>

<span data-ttu-id="37e1b-140">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="37e1b-141">Bindingyönlendirmeler bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-141">bindingRedirects section</span></span>

<span data-ttu-id="37e1b-142">Bir paket yüklendiğinde NuGet 'in otomatik bağlama yeniden yönlendirmelerini yapıp yönlendirmeyeceğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="37e1b-143">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-143">Key</span></span> | <span data-ttu-id="37e1b-144">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-145">Atla</span><span class="sxs-lookup"><span data-stu-id="37e1b-145">skip</span></span> | <span data-ttu-id="37e1b-146">Otomatik bağlama yeniden yönlendirmelerinin atlanıp atlanmayacağını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="37e1b-147">Varsayılan değer false.</span><span class="sxs-lookup"><span data-stu-id="37e1b-147">The default is false.</span></span> |

<span data-ttu-id="37e1b-148">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="37e1b-149">Packageresesme bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-149">packageRestore section</span></span>

<span data-ttu-id="37e1b-150">Derlemeler sırasında paket geri yüklemeyi denetler.</span><span class="sxs-lookup"><span data-stu-id="37e1b-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="37e1b-151">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-151">Key</span></span> | <span data-ttu-id="37e1b-152">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-153">enabled</span><span class="sxs-lookup"><span data-stu-id="37e1b-153">enabled</span></span> | <span data-ttu-id="37e1b-154">NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="37e1b-155">Ayrıca, yapılandırma dosyasında bu anahtarı ayarlamak yerine `EnableNuGetPackageRestore` ortam değişkenini `True` bir değerle ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e1b-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="37e1b-156">otomatik</span><span class="sxs-lookup"><span data-stu-id="37e1b-156">automatic</span></span> | <span data-ttu-id="37e1b-157">Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="37e1b-158">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="37e1b-159">çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-159">solution section</span></span>

<span data-ttu-id="37e1b-160">Bir çözümün `packages` klasörünün kaynak denetimine dahil edilip edilmeyeceğini denetler.</span><span class="sxs-lookup"><span data-stu-id="37e1b-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="37e1b-161">Bu bölüm yalnızca bir çözüm klasöründeki `nuget.config` dosyalarında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="37e1b-162">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-162">Key</span></span> | <span data-ttu-id="37e1b-163">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-164">Disablesourcecontrolintefini</span><span class="sxs-lookup"><span data-stu-id="37e1b-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="37e1b-165">Kaynak denetimiyle çalışırken paketler klasörünün yoksayılıp yoksayılmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="37e1b-166">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="37e1b-166">The default value is false.</span></span> |

<span data-ttu-id="37e1b-167">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="37e1b-168">Paket kaynak bölümleri</span><span class="sxs-lookup"><span data-stu-id="37e1b-168">Package source sections</span></span>

<span data-ttu-id="37e1b-169">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` ve `trustedSigners`, yükleme, geri yükleme ve güncelleştirme işlemleri sırasında NuGet 'in paket depolarıyla nasıl çalıştığını yapılandırmak için birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="37e1b-170">[`nuget sources` komutu](../reference/cli-reference/cli-ref-sources.md) genellikle bu ayarları yönetmek için kullanılır; [`nuget setapikey` komutu](../reference/cli-reference/cli-ref-setapikey.md)kullanılarak yönetilen `apikeys` ve [`nuget trusted-signers` komutu](../reference/cli-reference/cli-ref-trusted-signers.md)kullanılarak yönetilen `trustedSigners`.</span><span class="sxs-lookup"><span data-stu-id="37e1b-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="37e1b-171">Nuget.org için kaynak URL 'sinin `https://api.nuget.org/v3/index.json`olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="37e1b-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="37e1b-172">packagesonak</span><span class="sxs-lookup"><span data-stu-id="37e1b-172">packageSources</span></span>

<span data-ttu-id="37e1b-173">Bilinen tüm paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="37e1b-173">Lists all known package sources.</span></span> <span data-ttu-id="37e1b-174">Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="37e1b-175">NuGet, `packages.config`kullanarak projelerle ilgili Install ve Update işlemlerine yönelik kaynak sırasını uyar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="37e1b-176">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-176">Key</span></span> | <span data-ttu-id="37e1b-177">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-178">(paket kaynağına atanacak ad)</span><span class="sxs-lookup"><span data-stu-id="37e1b-178">(name to assign to the package source)</span></span> | <span data-ttu-id="37e1b-179">Paket kaynağının yolu veya URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="37e1b-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="37e1b-180">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="37e1b-181">Belirli bir düğüm için `<clear />` mevcut olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="37e1b-182">[Ayarların nasıl uygulandığı hakkında daha fazla bilgi edinin](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="37e1b-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="37e1b-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="37e1b-183">packageSourceCredentials</span></span>

<span data-ttu-id="37e1b-184">Genellikle `-username` ve `-password` anahtarlarıyla belirtilen `nuget sources`olan kaynaklar için Kullanıcı adlarını ve parolaları depolar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="37e1b-185">`-storepasswordincleartext` seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="37e1b-186">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-186">Key</span></span> | <span data-ttu-id="37e1b-187">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-188">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="37e1b-188">username</span></span> | <span data-ttu-id="37e1b-189">Kaynağın düz metin olarak Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="37e1b-189">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="37e1b-190">password</span><span class="sxs-lookup"><span data-stu-id="37e1b-190">password</span></span> | <span data-ttu-id="37e1b-191">Kaynak için şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="37e1b-191">The encrypted password for the source.</span></span> |
| <span data-ttu-id="37e1b-192">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="37e1b-192">cleartextpassword</span></span> | <span data-ttu-id="37e1b-193">Kaynak için şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="37e1b-193">The unencrypted password for the source.</span></span> |

<span data-ttu-id="37e1b-194">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="37e1b-194">**Example:**</span></span>

<span data-ttu-id="37e1b-195">Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar `_x0020_`ile değiştirilmiştir).</span><span class="sxs-lookup"><span data-stu-id="37e1b-195">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="37e1b-196">Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="37e1b-196">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="37e1b-197">Şifrelenmemiş parolalar kullanırken:</span><span class="sxs-lookup"><span data-stu-id="37e1b-197">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="37e1b-198">apikeys tuşları</span><span class="sxs-lookup"><span data-stu-id="37e1b-198">apikeys</span></span>

<span data-ttu-id="37e1b-199">API anahtar kimlik doğrulaması kullanan kaynaklar için [`nuget setapikey` komutuyla](../reference/cli-reference/cli-ref-setapikey.md)ayarlanan anahtarları depolar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-199">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="37e1b-200">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-200">Key</span></span> | <span data-ttu-id="37e1b-201">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-201">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-202">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="37e1b-202">(source URL)</span></span> | <span data-ttu-id="37e1b-203">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="37e1b-203">The encrypted API key.</span></span> |

<span data-ttu-id="37e1b-204">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-204">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="37e1b-205">disabledpackagesonak</span><span class="sxs-lookup"><span data-stu-id="37e1b-205">disabledPackageSources</span></span>

<span data-ttu-id="37e1b-206">Şu anda devre dışı olan kaynaklar tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="37e1b-206">Identified currently disabled sources.</span></span> <span data-ttu-id="37e1b-207">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-207">May be empty.</span></span>

| <span data-ttu-id="37e1b-208">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-208">Key</span></span> | <span data-ttu-id="37e1b-209">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-210">(kaynağın adı)</span><span class="sxs-lookup"><span data-stu-id="37e1b-210">(name of source)</span></span> | <span data-ttu-id="37e1b-211">Kaynağın devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-211">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="37e1b-212">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="37e1b-212">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="37e1b-213">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="37e1b-213">activePackageSource</span></span>

<span data-ttu-id="37e1b-214">*(yalnızca 2. x, 3. x + ' de kullanım dışı)*</span><span class="sxs-lookup"><span data-stu-id="37e1b-214">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="37e1b-215">Şu anda etkin olan kaynağı tanımlar veya tüm kaynakların toplamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-215">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="37e1b-216">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-216">Key</span></span> | <span data-ttu-id="37e1b-217">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-218">(kaynağın adı) veya `All`</span><span class="sxs-lookup"><span data-stu-id="37e1b-218">(name of source) or `All`</span></span> | <span data-ttu-id="37e1b-219">Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur.</span><span class="sxs-lookup"><span data-stu-id="37e1b-219">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="37e1b-220">`All`, aksi durumda devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için değer `(Aggregate source)` olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-220">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="37e1b-221">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-221">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="37e1b-222">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-222">trustedSigners section</span></span>

<span data-ttu-id="37e1b-223">Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-223">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="37e1b-224">Kullanıcı `require``signatureValidationMode` ayarladığında bu liste boş olamaz.</span><span class="sxs-lookup"><span data-stu-id="37e1b-224">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="37e1b-225">Bu bölüm [`nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-225">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="37e1b-226">**Şema**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-226">**Schema**:</span></span>

<span data-ttu-id="37e1b-227">Güvenilen bir imzalayan, belirli bir İmzalayanın tanımlayan tüm sertifikaların listelendiği `certificate` öğeleri koleksiyonuna sahiptir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-227">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="37e1b-228">Güvenilen bir imzalayan bir `Author` veya `Repository`olabilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-228">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="37e1b-229">Güvenilen *Depo* Ayrıca, deponun `serviceIndex` (geçerli bir `https` URI olması gerekir) belirtir ve isteğe bağlı olarak, belirli bir depodan daha fazla güvenilir olan bir `owners` noktalı virgülle ayrılmış listesi belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-229">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="37e1b-230">Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları `SHA256`, `SHA384` ve `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="37e1b-230">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="37e1b-231">Bir `certificate` `true` `allowUntrustedRoot` belirtiyorsa, belirtilen sertifikanın, imza doğrulamasının bir parçası olarak sertifika zincirini oluştururken güvenilmeyen bir köke zincirine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-231">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="37e1b-232">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-232">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="37e1b-233">fallbackPackageFolders bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-233">fallbackPackageFolders section</span></span>

<span data-ttu-id="37e1b-234">*(3,5 +)* Paket, geri dönüş klasörlerinde bulunursa hiçbir işin gerçekleştirilmesi gerekmediği için paketleri önceden yüklemeye yönelik bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-234">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="37e1b-235">Geri dönüş paketi klasörleri, genel paket klasörüyle aynı klasöre ve dosya yapısına sahiptir: *. nupkg* var ve tüm dosyalar ayıklandı.</span><span class="sxs-lookup"><span data-stu-id="37e1b-235">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="37e1b-236">Bu yapılandırma için arama mantığı:</span><span class="sxs-lookup"><span data-stu-id="37e1b-236">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="37e1b-237">Paketin/sürümün zaten indirildiğini görmek için genel paket klasörüne bakın.</span><span class="sxs-lookup"><span data-stu-id="37e1b-237">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="37e1b-238">Paket/sürüm eşleşmesi için geri dönüş klasörlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="37e1b-238">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="37e1b-239">Her iki arama başarılı olursa, indirme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="37e1b-239">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="37e1b-240">Bir eşleşme bulunmazsa, NuGet dosya kaynaklarını ve ardından http kaynakları ' nı denetleyip paketleri indirir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-240">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="37e1b-241">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-241">Key</span></span> | <span data-ttu-id="37e1b-242">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-242">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-243">(geri dönüş klasörünün adı)</span><span class="sxs-lookup"><span data-stu-id="37e1b-243">(name of fallback folder)</span></span> | <span data-ttu-id="37e1b-244">Geri dönüş klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="37e1b-244">Path to fallback folder.</span></span> |

<span data-ttu-id="37e1b-245">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-245">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="37e1b-246">packageManagement bölümü</span><span class="sxs-lookup"><span data-stu-id="37e1b-246">packageManagement section</span></span>

<span data-ttu-id="37e1b-247">Varsayılan paket yönetim biçimini Package *. config* ya da packagereference olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="37e1b-247">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="37e1b-248">SDK stilindeki projeler her zaman PackageReference kullanır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-248">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="37e1b-249">Anahtar</span><span class="sxs-lookup"><span data-stu-id="37e1b-249">Key</span></span> | <span data-ttu-id="37e1b-250">Değer</span><span class="sxs-lookup"><span data-stu-id="37e1b-250">Value</span></span> |
| --- | --- |
| <span data-ttu-id="37e1b-251">biçim</span><span class="sxs-lookup"><span data-stu-id="37e1b-251">format</span></span> | <span data-ttu-id="37e1b-252">Varsayılan paket yönetimi biçimini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-252">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="37e1b-253">`1`, format, PackageReference olur.</span><span class="sxs-lookup"><span data-stu-id="37e1b-253">If `1`, format is PackageReference.</span></span> <span data-ttu-id="37e1b-254">`0`, biçim *Packages. config*olur.</span><span class="sxs-lookup"><span data-stu-id="37e1b-254">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="37e1b-255">devre dışı</span><span class="sxs-lookup"><span data-stu-id="37e1b-255">disabled</span></span> | <span data-ttu-id="37e1b-256">İlk paket yüklemesi sırasında varsayılan bir paket biçimi seçme isteminin gösterilip gösterilmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="37e1b-256">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="37e1b-257">`False`, istemi gizler.</span><span class="sxs-lookup"><span data-stu-id="37e1b-257">`False` hides the prompt.</span></span> |

<span data-ttu-id="37e1b-258">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="37e1b-258">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="37e1b-259">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="37e1b-259">Using environment variables</span></span>

<span data-ttu-id="37e1b-260">Çalışma zamanında ayarları uygulamak için, `nuget.config` değerlerinde (NuGet 3.4 +) ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37e1b-260">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="37e1b-261">Örneğin, Windows üzerinde `HOME` ortam değişkeni `c:\users\username`olarak ayarlanırsa, yapılandırma dosyasındaki `%HOME%\NuGetRepository` değeri `c:\users\username\NuGetRepository`olarak çözümlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-261">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="37e1b-262">Windows stili ortam değişkenlerini (başladığı ve bitişi%) kullanmanız gerektiğini unutmayın Mac/Linux üzerinde bile.</span><span class="sxs-lookup"><span data-stu-id="37e1b-262">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="37e1b-263">Yapılandırma dosyasında `$HOME/NuGetRepository` olması çözümlenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-263">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="37e1b-264">Mac/Linux üzerinde `%HOME%\NuGetRepository` değeri `/home/myStuff/NuGetRepository`çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="37e1b-264">On Mac/Linux the value of `%HOME%\NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="37e1b-265">Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="37e1b-265">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="37e1b-266">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="37e1b-266">Example config file</span></span>

<span data-ttu-id="37e1b-267">Aşağıda, isteğe bağlı olanlar dahil olmak üzere bir dizi ayarı gösteren örnek bir `nuget.config` dosyası verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="37e1b-267">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
