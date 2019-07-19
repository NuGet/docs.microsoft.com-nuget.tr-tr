---
title: NuGet. config dosyası başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, Solution ve packageSource bölümlerini içeren NuGet. config dosyası başvurusu.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317216"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="0767a-103">NuGet. config başvurusu</span><span class="sxs-lookup"><span data-stu-id="0767a-103">nuget.config reference</span></span>

<span data-ttu-id="0767a-104">NuGet davranışı, [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi `NuGet.Config` farklı dosyalardaki ayarlarla denetlenir.</span><span class="sxs-lookup"><span data-stu-id="0767a-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="0767a-105">`nuget.config`, daha sonra bu konuda açıklanan bölüm öğelerini içeren `<configuration>` üst düzey bir düğüm içeren bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="0767a-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="0767a-106">Her bölüm sıfır veya daha fazla öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="0767a-106">Each section contains zero or more items.</span></span> <span data-ttu-id="0767a-107">[Örnekler yapılandırma dosyasına](#example-config-file)bakın.</span><span class="sxs-lookup"><span data-stu-id="0767a-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="0767a-108">Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="0767a-109">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="0767a-109">In this topic:</span></span>

- [<span data-ttu-id="0767a-110">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-110">config section</span></span>](#config-section)
- [<span data-ttu-id="0767a-111">Bindingyönlendirmeler bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="0767a-112">Packageresesme bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="0767a-113">çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="0767a-114">[Paket kaynağı bölümleri](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="0767a-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="0767a-115">packagesonak</span><span class="sxs-lookup"><span data-stu-id="0767a-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="0767a-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="0767a-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="0767a-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="0767a-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="0767a-118">disabledpackagesonak</span><span class="sxs-lookup"><span data-stu-id="0767a-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="0767a-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="0767a-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="0767a-120">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="0767a-121">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="0767a-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="0767a-122">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="0767a-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="0767a-123">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-123">config section</span></span>

<span data-ttu-id="0767a-124">Komutu kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir. [ `nuget config` ](../reference/cli-reference/cli-ref-config.md)</span><span class="sxs-lookup"><span data-stu-id="0767a-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="0767a-125">`dependencyVersion`ve `repositoryPath` yalnızca kullanan `packages.config`projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0767a-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="0767a-126">`globalPackagesFolder`yalnızca PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0767a-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="0767a-127">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-127">Key</span></span> | <span data-ttu-id="0767a-128">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-129">dependencyversion (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="0767a-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="0767a-130">Anahtar doğrudan `DependencyVersion` belirtilmediğinde, paket yükleme, geri yükleme ve güncelleştirme için varsayılan değer. `-DependencyVersion`</span><span class="sxs-lookup"><span data-stu-id="0767a-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="0767a-131">Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0767a-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="0767a-132">Değerler,,, .`Highest` `Lowest` `HighestPatch` `HighestMinor`</span><span class="sxs-lookup"><span data-stu-id="0767a-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="0767a-133">globalPackagesFolder (yalnızca PackageReference kullanan projeler)</span><span class="sxs-lookup"><span data-stu-id="0767a-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="0767a-134">Varsayılan genel paketler klasörünün konumu.</span><span class="sxs-lookup"><span data-stu-id="0767a-134">The location of the default global packages folder.</span></span> <span data-ttu-id="0767a-135">Varsayılan `%userprofile%\.nuget\packages` değer (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0767a-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="0767a-136">Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="0767a-137">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="0767a-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="0767a-138">depoyolu (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="0767a-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="0767a-139">Varsayılan `$(Solutiondir)/packages` klasör yerine NuGet paketlerinin yükleneceği konum.</span><span class="sxs-lookup"><span data-stu-id="0767a-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="0767a-140">Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="0767a-141">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="0767a-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="0767a-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="0767a-142">defaultPushSource</span></span> | <span data-ttu-id="0767a-143">Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0767a-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="0767a-144">http_proxy http_proxy. User http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="0767a-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="0767a-145">Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` biçiminde`http://<username>:<password>@<domain>`olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0767a-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="0767a-146">Parolalar şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="0767a-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="0767a-147">İçin `no_proxy`, değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir.</span><span class="sxs-lookup"><span data-stu-id="0767a-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="0767a-148">Bu değerler için http_proxy ve no_proxy ortam değişkenlerini alternatif olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0767a-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="0767a-149">Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="0767a-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="0767a-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="0767a-150">signatureValidationMode</span></span> | <span data-ttu-id="0767a-151">Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="0767a-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="0767a-152">`accept`Değerler, .`require`</span><span class="sxs-lookup"><span data-stu-id="0767a-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="0767a-153">Varsayılan olarak `accept`.</span><span class="sxs-lookup"><span data-stu-id="0767a-153">Defaults to `accept`.</span></span>

<span data-ttu-id="0767a-154">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="0767a-155">Bindingyönlendirmeler bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-155">bindingRedirects section</span></span>

<span data-ttu-id="0767a-156">Bir paket yüklendiğinde NuGet 'in otomatik bağlama yeniden yönlendirmelerini yapıp yönlendirmeyeceğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="0767a-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="0767a-157">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-157">Key</span></span> | <span data-ttu-id="0767a-158">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-159">Atla</span><span class="sxs-lookup"><span data-stu-id="0767a-159">skip</span></span> | <span data-ttu-id="0767a-160">Otomatik bağlama yeniden yönlendirmelerinin atlanıp atlanmayacağını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0767a-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="0767a-161">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="0767a-161">The default is false.</span></span> |

<span data-ttu-id="0767a-162">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="0767a-163">Packageresesme bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-163">packageRestore section</span></span>

<span data-ttu-id="0767a-164">Derlemeler sırasında paket geri yüklemeyi denetler.</span><span class="sxs-lookup"><span data-stu-id="0767a-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="0767a-165">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-165">Key</span></span> | <span data-ttu-id="0767a-166">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-167">Etkinletir</span><span class="sxs-lookup"><span data-stu-id="0767a-167">enabled</span></span> | <span data-ttu-id="0767a-168">NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0767a-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="0767a-169">Ayrıca, `EnableNuGetPackageRestore` yapılandırma dosyasında bu anahtarı ayarlamak `True` yerine, ortam değişkenini bir değeriyle ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0767a-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="0767a-170">otomatik</span><span class="sxs-lookup"><span data-stu-id="0767a-170">automatic</span></span> | <span data-ttu-id="0767a-171">Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0767a-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="0767a-172">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="0767a-173">çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-173">solution section</span></span>

<span data-ttu-id="0767a-174">Kaynak denetimine bir `packages` çözüm klasörünün eklenip eklenmeyeceğini denetler.</span><span class="sxs-lookup"><span data-stu-id="0767a-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="0767a-175">Bu bölüm yalnızca `nuget.config` bir çözüm klasöründeki dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="0767a-176">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-176">Key</span></span> | <span data-ttu-id="0767a-177">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-178">Disablesourcecontrolintefini</span><span class="sxs-lookup"><span data-stu-id="0767a-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="0767a-179">Kaynak denetimiyle çalışırken paketler klasörünün yoksayılıp yoksayılmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0767a-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="0767a-180">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="0767a-180">The default value is false.</span></span> |

<span data-ttu-id="0767a-181">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="0767a-182">Paket kaynak bölümleri</span><span class="sxs-lookup"><span data-stu-id="0767a-182">Package source sections</span></span>

<span data-ttu-id="0767a-183">`packageSources` ,`packageSourceCredentials` ,,`trustedSigners`Vetüm çalışmaları birlikte çalışarak, NuGet 'in yükleme, geri yükleme ve güncelleştirme işlemleri sırasında paket depolarıyla nasıl çalıştığını yapılandırır. `disabledPackageSources` `apikeys` `activePackageSource`</span><span class="sxs-lookup"><span data-stu-id="0767a-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="0767a-184">[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)Komutu genellikle Bu`apikeys` ayarları yönetmek için kullanılır, ancak komutu kullanılarak yönetilir ve komutu kullanılarak yönetilir. [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md)</span><span class="sxs-lookup"><span data-stu-id="0767a-184">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="0767a-185">Nuget.org için kaynak URL 'sinin olduğunu `https://api.nuget.org/v3/index.json`unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0767a-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="0767a-186">packagesonak</span><span class="sxs-lookup"><span data-stu-id="0767a-186">packageSources</span></span>

<span data-ttu-id="0767a-187">Bilinen tüm paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="0767a-187">Lists all known package sources.</span></span> <span data-ttu-id="0767a-188">Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="0767a-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="0767a-189">NuGet, kullanan `packages.config`projelerle ilgili güncelleştirme ve güncelleştirme işlemlerine yönelik kaynakların sırasını duyar.</span><span class="sxs-lookup"><span data-stu-id="0767a-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="0767a-190">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-190">Key</span></span> | <span data-ttu-id="0767a-191">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-192">(paket kaynağına atanacak ad)</span><span class="sxs-lookup"><span data-stu-id="0767a-192">(name to assign to the package source)</span></span> | <span data-ttu-id="0767a-193">Paket kaynağının yolu veya URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="0767a-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="0767a-194">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="0767a-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="0767a-195">packageSourceCredentials</span></span>

<span data-ttu-id="0767a-196">Genellikle `-username` ve `-password` anahtarlarıyla belirtilenkaynaklariçinKullanıcıadlarınıveparolalarıdepolar.`nuget sources`</span><span class="sxs-lookup"><span data-stu-id="0767a-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="0767a-197">`-storepasswordincleartext` Seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="0767a-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="0767a-198">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-198">Key</span></span> | <span data-ttu-id="0767a-199">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-200">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="0767a-200">username</span></span> | <span data-ttu-id="0767a-201">Kaynağın düz metin olarak Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="0767a-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="0767a-202">password</span><span class="sxs-lookup"><span data-stu-id="0767a-202">password</span></span> | <span data-ttu-id="0767a-203">Kaynak için şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="0767a-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="0767a-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="0767a-204">cleartextpassword</span></span> | <span data-ttu-id="0767a-205">Kaynak için şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="0767a-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="0767a-206">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="0767a-206">**Example:**</span></span>

<span data-ttu-id="0767a-207">Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar ile `_x0020_`değiştirilmiştir).</span><span class="sxs-lookup"><span data-stu-id="0767a-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="0767a-208">Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="0767a-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="0767a-209">Şifrelenmemiş parolalar kullanırken:</span><span class="sxs-lookup"><span data-stu-id="0767a-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="0767a-210">apikeys tuşları</span><span class="sxs-lookup"><span data-stu-id="0767a-210">apikeys</span></span>

<span data-ttu-id="0767a-211">Komutuyla ayarlanan API anahtarı kimlik doğrulaması kullanan kaynaklar için anahtarları depolar. [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)</span><span class="sxs-lookup"><span data-stu-id="0767a-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="0767a-212">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-212">Key</span></span> | <span data-ttu-id="0767a-213">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-214">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="0767a-214">(source URL)</span></span> | <span data-ttu-id="0767a-215">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="0767a-215">The encrypted API key.</span></span> |

<span data-ttu-id="0767a-216">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="0767a-217">disabledpackagesonak</span><span class="sxs-lookup"><span data-stu-id="0767a-217">disabledPackageSources</span></span>

<span data-ttu-id="0767a-218">Şu anda devre dışı olan kaynaklar tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="0767a-218">Identified currently disabled sources.</span></span> <span data-ttu-id="0767a-219">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-219">May be empty.</span></span>

| <span data-ttu-id="0767a-220">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-220">Key</span></span> | <span data-ttu-id="0767a-221">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-222">(kaynağın adı)</span><span class="sxs-lookup"><span data-stu-id="0767a-222">(name of source)</span></span> | <span data-ttu-id="0767a-223">Kaynağın devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="0767a-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="0767a-224">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="0767a-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="0767a-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="0767a-225">activePackageSource</span></span>

<span data-ttu-id="0767a-226">*(yalnızca 2. x, 3. x + ' de kullanım dışı)*</span><span class="sxs-lookup"><span data-stu-id="0767a-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="0767a-227">Şu anda etkin olan kaynağı tanımlar veya tüm kaynakların toplamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0767a-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="0767a-228">Anahtar</span><span class="sxs-lookup"><span data-stu-id="0767a-228">Key</span></span> | <span data-ttu-id="0767a-229">Değer</span><span class="sxs-lookup"><span data-stu-id="0767a-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0767a-230">(kaynağın adı) veya`All`</span><span class="sxs-lookup"><span data-stu-id="0767a-230">(name of source) or `All`</span></span> | <span data-ttu-id="0767a-231">Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur.</span><span class="sxs-lookup"><span data-stu-id="0767a-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="0767a-232">Eğer `All`değeri, aksi durumda `(Aggregate source)` devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0767a-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="0767a-233">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="0767a-234">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="0767a-234">trustedSigners section</span></span>

<span data-ttu-id="0767a-235">Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar.</span><span class="sxs-lookup"><span data-stu-id="0767a-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="0767a-236">Kullanıcı `signatureValidationMode` öğesine`require`ayarlandığında bu liste boş olamaz.</span><span class="sxs-lookup"><span data-stu-id="0767a-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="0767a-237">Bu bölüm, [ `nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-237">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="0767a-238">**Şema**:</span><span class="sxs-lookup"><span data-stu-id="0767a-238">**Schema**:</span></span>

<span data-ttu-id="0767a-239">Güvenilen bir imzalayan, belirli bir İmzalayanın `certificate` tanımlayan tüm sertifikaları içeren bir öğe koleksiyonuna sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0767a-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="0767a-240">Güvenilen bir imzalayan ya da `Author` `Repository`olabilir.</span><span class="sxs-lookup"><span data-stu-id="0767a-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="0767a-241">Güvenilen bir *Depo* Ayrıca depo `serviceIndex` için (geçerli `https` bir URI olması gerekir) belirtir ve isteğe bağlı olarak, bu belirli `owners` bir istemciden güvenilir bir şekilde kısıtlamak için noktalı virgülle ayrılmış bir liste belirtebilir Depo.</span><span class="sxs-lookup"><span data-stu-id="0767a-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="0767a-242">Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları, `SHA256`ve `SHA384` `SHA512`' dir.</span><span class="sxs-lookup"><span data-stu-id="0767a-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="0767a-243">Bir `certificate` ise, imza `true` doğrulamasının parçası olarak sertifika zincirini oluştururken, belirtilen sertifikanın güvenilmeyen bir köke zincirine izin verileceğini belirtir `allowUntrustedRoot` .</span><span class="sxs-lookup"><span data-stu-id="0767a-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="0767a-244">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="0767a-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="0767a-245">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="0767a-245">Using environment variables</span></span>

<span data-ttu-id="0767a-246">Çalışma zamanında ayarları uygulamak için değerler `nuget.config` (NuGet 3.4 +) cinsinden ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0767a-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="0767a-247">Örneğin, `HOME` Windows üzerindeki ortam değişkeni olarak `c:\users\username`ayarlandıysa `%HOME%\NuGetRepository` , yapılandırma dosyasındaki değeri olarak `c:\users\username\NuGetRepository`çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="0767a-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="0767a-248">Benzer şekilde, Mac/Linux `%HOME%/NuGetRepository` , olarak `/home/myStuff`ayarlanmışsa yapılandırma dosyasında olarak `/home/myStuff/NuGetRepository`çözümlenir. `HOME`</span><span class="sxs-lookup"><span data-stu-id="0767a-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="0767a-249">Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="0767a-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="0767a-250">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="0767a-250">Example config file</span></span>

<span data-ttu-id="0767a-251">Aşağıda, bir dizi `nuget.config` ayarı gösteren örnek bir dosya verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0767a-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
