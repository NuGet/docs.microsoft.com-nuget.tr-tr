---
title: nuget.config dosya başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, çözüm ve packageSource bölümlerini içeren dosya başvurusunu NuGet.Config.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 9b15550d0e6e8aec4d526391d77c654a756f343e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777670"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="5fa1f-103">nuget.config başvurusu</span><span class="sxs-lookup"><span data-stu-id="5fa1f-103">nuget.config reference</span></span>

<span data-ttu-id="5fa1f-104">NuGet davranışı, `NuGet.Config` `nuget.config` [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi farklı veya dosyalardaki ayarlarla denetlenir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="5fa1f-105">`nuget.config``<configuration>`, daha sonra bu konuda açıklanan bölüm öğelerini içeren üst düzey bir düğüm içeren BIR XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="5fa1f-106">Her bölüm sıfır veya daha fazla öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-106">Each section contains zero or more items.</span></span> <span data-ttu-id="5fa1f-107">[Örnekler yapılandırma dosyasına](#example-config-file)bakın.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="5fa1f-108">Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="5fa1f-109">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-109">config section</span></span>

<span data-ttu-id="5fa1f-110">[ `nuget config` Komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="5fa1f-111">`dependencyVersion` ve `repositoryPath` yalnızca kullanan projeler için geçerlidir `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="5fa1f-112">`globalPackagesFolder` yalnızca PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="5fa1f-113">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-113">Key</span></span> | <span data-ttu-id="5fa1f-114">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-115">dependencyVersion ( `packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="5fa1f-116">`DependencyVersion`Anahtar doğrudan belirtilmediğinde, paket yükleme, geri yükleme ve güncelleştirme için varsayılan değer `-DependencyVersion` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="5fa1f-117">Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="5fa1f-118">Değerler,,, `Lowest` `HighestPatch` `HighestMinor` `Highest` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="5fa1f-119">globalPackagesFolder (yalnızca PackageReference kullanan projeler)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="5fa1f-120">Varsayılan genel paketler klasörünün konumu.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-120">The location of the default global packages folder.</span></span> <span data-ttu-id="5fa1f-121">Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5fa1f-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="5fa1f-122">Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="5fa1f-123">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="5fa1f-124">Depoyolu ( `packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="5fa1f-125">Varsayılan klasör yerine NuGet paketlerinin yükleneceği konum `$(Solutiondir)/packages` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="5fa1f-126">Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="5fa1f-127">Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="5fa1f-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="5fa1f-128">defaultPushSource</span></span> | <span data-ttu-id="5fa1f-129">Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="5fa1f-130">http_proxy http_proxy. User http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="5fa1f-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="5fa1f-131">Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` biçiminde olmalıdır `http://<username>:<password>@<domain>` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="5fa1f-132">Parolalar şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="5fa1f-133">İçin `no_proxy` , değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="5fa1f-134">Ayrıca, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="5fa1f-135">Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="5fa1f-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="5fa1f-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="5fa1f-136">signatureValidationMode</span></span> | <span data-ttu-id="5fa1f-137">Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="5fa1f-138">Değerler `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="5fa1f-139">Varsayılan olarak olur `accept` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-139">Defaults to `accept`.</span></span>

<span data-ttu-id="5fa1f-140">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="5fa1f-141">Bindingyönlendirmeler bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-141">bindingRedirects section</span></span>

<span data-ttu-id="5fa1f-142">Bir paket yüklendiğinde NuGet 'in otomatik bağlama yeniden yönlendirmelerini yapıp yönlendirmeyeceğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="5fa1f-143">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-143">Key</span></span> | <span data-ttu-id="5fa1f-144">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-145">Atla</span><span class="sxs-lookup"><span data-stu-id="5fa1f-145">skip</span></span> | <span data-ttu-id="5fa1f-146">Otomatik bağlama yeniden yönlendirmelerinin atlanıp atlanmayacağını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="5fa1f-147">Varsayılan değer false.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-147">The default is false.</span></span> |

<span data-ttu-id="5fa1f-148">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="5fa1f-149">Packageresesme bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-149">packageRestore section</span></span>

<span data-ttu-id="5fa1f-150">Derlemeler sırasında paket geri yüklemeyi denetler.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="5fa1f-151">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-151">Key</span></span> | <span data-ttu-id="5fa1f-152">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-153">enabled</span><span class="sxs-lookup"><span data-stu-id="5fa1f-153">enabled</span></span> | <span data-ttu-id="5fa1f-154">NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="5fa1f-155">Ayrıca, `EnableNuGetPackageRestore` `True` yapılandırma dosyasında bu anahtarı ayarlamak yerine, ortam değişkenini bir değeriyle ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="5fa1f-156">otomatik</span><span class="sxs-lookup"><span data-stu-id="5fa1f-156">automatic</span></span> | <span data-ttu-id="5fa1f-157">Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="5fa1f-158">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="5fa1f-159">çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-159">solution section</span></span>

<span data-ttu-id="5fa1f-160">`packages`Kaynak denetimine bir çözüm klasörünün eklenip eklenmeyeceğini denetler.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="5fa1f-161">Bu bölüm yalnızca `nuget.config` bir çözüm klasöründeki dosyalarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="5fa1f-162">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-162">Key</span></span> | <span data-ttu-id="5fa1f-163">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-164">Disablesourcecontrolintefini</span><span class="sxs-lookup"><span data-stu-id="5fa1f-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="5fa1f-165">Kaynak denetimiyle çalışırken paketler klasörünün yoksayılıp yoksayılmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="5fa1f-166">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-166">The default value is false.</span></span> |

<span data-ttu-id="5fa1f-167">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="5fa1f-168">Paket kaynak bölümleri</span><span class="sxs-lookup"><span data-stu-id="5fa1f-168">Package source sections</span></span>

<span data-ttu-id="5fa1f-169">`packageSources`,, `packageSourceCredentials` , `apikeys` `activePackageSource` `disabledPackageSources` Ve `trustedSigners` tüm çalışmaları birlikte çalışarak, NuGet 'in yükleme, geri yükleme ve güncelleştirme işlemleri sırasında paket depolarıyla nasıl çalıştığını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="5fa1f-170">Komutu [ `nuget sources` genellikle](../reference/cli-reference/cli-ref-sources.md) bu ayarları yönetmek için kullanılır, ancak `apikeys` [ `nuget setapikey` komutu](../reference/cli-reference/cli-ref-setapikey.md)kullanılarak yönetilir ve `trustedSigners` [ `nuget trusted-signers` komutu](../reference/cli-reference/cli-ref-trusted-signers.md)kullanılarak yönetilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="5fa1f-171">Nuget.org için kaynak URL 'sinin olduğunu unutmayın `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="5fa1f-172">packagesonak</span><span class="sxs-lookup"><span data-stu-id="5fa1f-172">packageSources</span></span>

<span data-ttu-id="5fa1f-173">Bilinen tüm paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-173">Lists all known package sources.</span></span> <span data-ttu-id="5fa1f-174">Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="5fa1f-175">NuGet, kullanan projelerle ilgili güncelleştirme ve güncelleştirme işlemlerine yönelik kaynakların sırasını duyar `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="5fa1f-176">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-176">Key</span></span> | <span data-ttu-id="5fa1f-177">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-178">(paket kaynağına atanacak ad)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-178">(name to assign to the package source)</span></span> | <span data-ttu-id="5fa1f-179">Paket kaynağının yolu veya URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="5fa1f-180">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="5fa1f-181">`<clear />`Belirli bir düğüm için olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="5fa1f-182">[Ayarların nasıl uygulandığı hakkında daha fazla bilgi edinin](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="5fa1f-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="5fa1f-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="5fa1f-183">packageSourceCredentials</span></span>

<span data-ttu-id="5fa1f-184">Genellikle ve anahtarlarıyla belirtilen kaynaklar için Kullanıcı adlarını ve parolaları depolar `-username` `-password` `nuget sources` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="5fa1f-185">`-storepasswordincleartext`Seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="5fa1f-186">İsteğe bağlı olarak, anahtarla geçerli kimlik doğrulama türleri de belirtilebilir `-validauthenticationtypes` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="5fa1f-187">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-187">Key</span></span> | <span data-ttu-id="5fa1f-188">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-189">username</span><span class="sxs-lookup"><span data-stu-id="5fa1f-189">username</span></span> | <span data-ttu-id="5fa1f-190">Kaynağın düz metin olarak Kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="5fa1f-191">password</span><span class="sxs-lookup"><span data-stu-id="5fa1f-191">password</span></span> | <span data-ttu-id="5fa1f-192">Kaynak için şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-192">The encrypted password for the source.</span></span> <span data-ttu-id="5fa1f-193">Şifrelenmiş parolalar yalnızca Windows 'da desteklenir ve yalnızca aynı makinede kullanıldığında ve özgün şifrelemeyle aynı kullanıcı aracılığıyla şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="5fa1f-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="5fa1f-194">cleartextpassword</span></span> | <span data-ttu-id="5fa1f-195">Kaynak için şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-195">The unencrypted password for the source.</span></span> <span data-ttu-id="5fa1f-196">Note: ortam değişkenleri, geliştirilmiş güvenlik için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="5fa1f-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-197">validauthenticationtypes</span></span> | <span data-ttu-id="5fa1f-198">Bu kaynak için geçerli kimlik doğrulama türlerinin virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="5fa1f-199">`basic`Sunucu ntlm veya anlaşma duyurur ise ve şirket içi Azure DevOps Server BIR Pat kullanırken, kimlik bilgilerinizin temel mekanizma kullanılarak gönderilmesi gerekiyorsa, bunu olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="5fa1f-200">Diğer geçerli değerler,,, ve içerir, `negotiate` `kerberos` `ntlm` `digest` ancak bu değerlerin yararlı olması çok düşüktür.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="5fa1f-201">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="5fa1f-201">**Example:**</span></span>

<span data-ttu-id="5fa1f-202">Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar ile değiştirilmiştir `_x0020_` ).</span><span class="sxs-lookup"><span data-stu-id="5fa1f-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="5fa1f-203">Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="5fa1f-204">Bir ortam değişkeninde depolanan şifrelenmemiş parolaları kullanırken:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="5fa1f-205">Şifrelenmemiş parolalar kullanırken:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="5fa1f-206">Ayrıca, geçerli kimlik doğrulama yöntemleri sağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="5fa1f-207">apikeys tuşları</span><span class="sxs-lookup"><span data-stu-id="5fa1f-207">apikeys</span></span>

<span data-ttu-id="5fa1f-208">[ `nuget setapikey` Komutuyla](../reference/cli-reference/cli-ref-setapikey.md)ayarlanan API anahtarı kimlik doğrulaması kullanan kaynaklar için anahtarları depolar.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="5fa1f-209">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-209">Key</span></span> | <span data-ttu-id="5fa1f-210">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-211">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-211">(source URL)</span></span> | <span data-ttu-id="5fa1f-212">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-212">The encrypted API key.</span></span> |

<span data-ttu-id="5fa1f-213">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="5fa1f-214">disabledpackagesonak</span><span class="sxs-lookup"><span data-stu-id="5fa1f-214">disabledPackageSources</span></span>

<span data-ttu-id="5fa1f-215">Şu anda devre dışı olan kaynaklar tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-215">Identified currently disabled sources.</span></span> <span data-ttu-id="5fa1f-216">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-216">May be empty.</span></span>

| <span data-ttu-id="5fa1f-217">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-217">Key</span></span> | <span data-ttu-id="5fa1f-218">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-219">(kaynağın adı)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-219">(name of source)</span></span> | <span data-ttu-id="5fa1f-220">Kaynağın devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="5fa1f-221">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="5fa1f-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="5fa1f-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="5fa1f-222">activePackageSource</span></span>

<span data-ttu-id="5fa1f-223">*(yalnızca 2. x, 3. x + ' de kullanım dışı)*</span><span class="sxs-lookup"><span data-stu-id="5fa1f-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="5fa1f-224">Şu anda etkin olan kaynağı tanımlar veya tüm kaynakların toplamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="5fa1f-225">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-225">Key</span></span> | <span data-ttu-id="5fa1f-226">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-227">(kaynağın adı) veya `All`</span><span class="sxs-lookup"><span data-stu-id="5fa1f-227">(name of source) or `All`</span></span> | <span data-ttu-id="5fa1f-228">Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="5fa1f-229">Eğer `All` değeri, `(Aggregate source)` Aksi durumda devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="5fa1f-230">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="5fa1f-231">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-231">trustedSigners section</span></span>

<span data-ttu-id="5fa1f-232">Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="5fa1f-233">Kullanıcı öğesine ayarlandığında bu liste boş olamaz `signatureValidationMode` `require` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="5fa1f-234">Bu bölüm, [ `nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="5fa1f-235">**Şema**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-235">**Schema**:</span></span>

<span data-ttu-id="5fa1f-236">Güvenilen bir imzalayan `certificate` , belirli bir İmzalayanın tanımlayan tüm sertifikaları içeren bir öğe koleksiyonuna sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="5fa1f-237">Güvenilen bir imzalayan ya da olabilir `Author` `Repository` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="5fa1f-238">Güvenilen bir *Depo* Ayrıca `serviceIndex` Depo için (geçerli bir URI olması gerekir `https` ) belirtir ve isteğe bağlı olarak, `owners` belirli bir depodan güvenilir olan daha fazla sayıda kısıtlamak için noktalı virgülle ayrılmış bir liste belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="5fa1f-239">Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları `SHA256` , ve ' dir `SHA384` `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="5fa1f-240">Bir ise `certificate` , `allowUntrustedRoot` `true` imza doğrulamasının parçası olarak sertifika zincirini oluştururken, belirtilen sertifikanın güvenilmeyen bir köke zincirine izin verileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="5fa1f-241">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="5fa1f-242">fallbackPackageFolders bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="5fa1f-243">*(3,5 +)* Paket, geri dönüş klasörlerinde bulunursa hiçbir işin gerçekleştirilmesi gerekmediği için paketleri önceden yüklemeye yönelik bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="5fa1f-244">Geri dönüş paketi klasörleri, genel paket klasörüyle aynı klasöre ve dosya yapısına sahiptir: *. nupkg* var ve tüm dosyalar ayıklandı.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="5fa1f-245">Bu yapılandırma için arama mantığı:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="5fa1f-246">Paketin/sürümün zaten indirildiğini görmek için genel paket klasörüne bakın.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="5fa1f-247">Paket/sürüm eşleşmesi için geri dönüş klasörlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="5fa1f-248">Her iki arama başarılı olursa, indirme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="5fa1f-249">Bir eşleşme bulunmazsa, NuGet dosya kaynaklarını ve ardından http kaynakları ' nı denetleyip paketleri indirir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="5fa1f-250">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-250">Key</span></span> | <span data-ttu-id="5fa1f-251">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-252">(geri dönüş klasörünün adı)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-252">(name of fallback folder)</span></span> | <span data-ttu-id="5fa1f-253">Geri dönüş klasörünün yolu.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-253">Path to fallback folder.</span></span> |

<span data-ttu-id="5fa1f-254">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="5fa1f-255">packageManagement bölümü</span><span class="sxs-lookup"><span data-stu-id="5fa1f-255">packageManagement section</span></span>

<span data-ttu-id="5fa1f-256">Varsayılan paket yönetim biçimini *packages.config* ya da packagereference olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="5fa1f-257">SDK stilindeki projeler her zaman PackageReference kullanır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="5fa1f-258">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5fa1f-258">Key</span></span> | <span data-ttu-id="5fa1f-259">Değer</span><span class="sxs-lookup"><span data-stu-id="5fa1f-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5fa1f-260">biçim</span><span class="sxs-lookup"><span data-stu-id="5fa1f-260">format</span></span> | <span data-ttu-id="5fa1f-261">Varsayılan paket yönetimi biçimini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="5fa1f-262">İse `1` Format, PackageReference olur.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="5fa1f-263">İse `0` , biçim *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="5fa1f-264">devre dışı</span><span class="sxs-lookup"><span data-stu-id="5fa1f-264">disabled</span></span> | <span data-ttu-id="5fa1f-265">İlk paket yüklemesi sırasında varsayılan bir paket biçimi seçme isteminin gösterilip gösterilmeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="5fa1f-266">`False` istemi gizler.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="5fa1f-267">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="5fa1f-268">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="5fa1f-268">Using environment variables</span></span>

<span data-ttu-id="5fa1f-269">`nuget.config`Çalışma zamanında ayarları uygulamak için değerler (NuGet 3.4 +) cinsinden ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="5fa1f-270">Örneğin, `HOME` Windows üzerindeki ortam değişkeni olarak ayarlandıysa `c:\users\username` , `%HOME%\NuGetRepository` yapılandırma dosyasındaki değeri olarak çözümlenir `c:\users\username\NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="5fa1f-271">Windows stili ortam değişkenlerini (başladığı ve bitişi%) kullanmanız gerektiğini unutmayın Mac/Linux üzerinde bile.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="5fa1f-272">`$HOME/NuGetRepository`Yapılandırma dosyasında bulunması çözümlenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="5fa1f-273">Mac/Linux üzerinde değeri `%HOME%/NuGetRepository` olarak çözümlenir `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="5fa1f-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="5fa1f-274">Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="5fa1f-275">Örneğin `%MY_UNDEFINED_VAR%/NuGetRepository` , şu şekilde çözümlenir `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="5fa1f-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="5fa1f-276">Aşağıdaki tabloda, NuGet.Config dosyaları için environnment değişken sözdizimi ve yol ayırıcı desteği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5fa1f-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="5fa1f-277">NuGet.Config ortam değişkeni desteği</span><span class="sxs-lookup"><span data-stu-id="5fa1f-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="5fa1f-278">Syntax</span><span class="sxs-lookup"><span data-stu-id="5fa1f-278">Syntax</span></span> | <span data-ttu-id="5fa1f-279">Dizin ayırıcı</span><span class="sxs-lookup"><span data-stu-id="5fa1f-279">Dir separator</span></span> | <span data-ttu-id="5fa1f-280">Windows nuget.exe</span><span class="sxs-lookup"><span data-stu-id="5fa1f-280">Windows nuget.exe</span></span> | <span data-ttu-id="5fa1f-281">Windows dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="5fa1f-281">Windows dotnet.exe</span></span> | <span data-ttu-id="5fa1f-282">Mac nuget.exe (mono)</span><span class="sxs-lookup"><span data-stu-id="5fa1f-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="5fa1f-283">Mac dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="5fa1f-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="5fa1f-284">Yes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-284">Yes</span></span> | <span data-ttu-id="5fa1f-285">Yes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-285">Yes</span></span> | <span data-ttu-id="5fa1f-286">Yes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-286">Yes</span></span> | <span data-ttu-id="5fa1f-287">Yes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="5fa1f-288">Yes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-288">Yes</span></span> | <span data-ttu-id="5fa1f-289">Yes</span><span class="sxs-lookup"><span data-stu-id="5fa1f-289">Yes</span></span> | <span data-ttu-id="5fa1f-290">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-290">No</span></span> | <span data-ttu-id="5fa1f-291">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="5fa1f-292">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-292">No</span></span> | <span data-ttu-id="5fa1f-293">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-293">No</span></span> | <span data-ttu-id="5fa1f-294">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-294">No</span></span> | <span data-ttu-id="5fa1f-295">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="5fa1f-296">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-296">No</span></span> | <span data-ttu-id="5fa1f-297">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-297">No</span></span> | <span data-ttu-id="5fa1f-298">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-298">No</span></span> | <span data-ttu-id="5fa1f-299">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fa1f-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="5fa1f-300">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="5fa1f-300">Example config file</span></span>

<span data-ttu-id="5fa1f-301">Aşağıda, `nuget.config` isteğe bağlı olanlar dahil olmak üzere bir dizi ayarı gösteren örnek bir dosya verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5fa1f-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
