---
title: nuget.config dosyası başvurusu
description: NuGet.Config dosyası başvurusu yapılandırma, SecurityPermission packageRestore, çözüm ve packageSource bölümler dahil olmak üzere.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 504a48224051265164f9ab183e63fa5e7f5867e6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546921"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="e3b4b-103">nuget.config başvurusu</span><span class="sxs-lookup"><span data-stu-id="e3b4b-103">nuget.config reference</span></span>

<span data-ttu-id="e3b4b-104">NuGet davranışını farklı ayarları tarafından denetlenir `NuGet.Config` dosyaları açıklandığı [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="e3b4b-105">`nuget.config` bir üst düzey içeren bir XML dosyası `<configuration>` düğümü, ardından bu konuda açıklanan bölüm öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="e3b4b-106">Her bölüm, sıfır veya daha fazla içerir `<add>` öğelerle `key` ve `value` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-106">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="e3b4b-107">Bkz: [örnek yapılandırma dosyası](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="e3b4b-108">Ayar adları büyük/küçük harfe ve değerlerini kullanabilirsiniz [ortam değişkenlerini](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="e3b4b-109">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-109">In this topic:</span></span>

- [<span data-ttu-id="e3b4b-110">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-110">config section</span></span>](#config-section)
- [<span data-ttu-id="e3b4b-111">SecurityPermission bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="e3b4b-112">packageRestore bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="e3b4b-113">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="e3b4b-114">[Paket kaynak bölümler](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="e3b4b-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="e3b4b-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="e3b4b-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="e3b4b-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="e3b4b-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="e3b4b-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="e3b4b-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="e3b4b-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="e3b4b-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="e3b4b-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="e3b4b-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="e3b4b-120">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="e3b4b-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="e3b4b-121">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="e3b4b-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="e3b4b-122">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-122">config section</span></span>

<span data-ttu-id="e3b4b-123">Kullanarak ayarlayabileceğiniz çeşitli yapılandırma ayarlarını içeren [ `nuget config` komut](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="e3b4b-124">`dependencyVersion` ve `repositoryPath` kullanarak projeleri için geçerli `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-124">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="e3b4b-125">`globalPackagesFolder` PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-125">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="e3b4b-126">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-126">Key</span></span> | <span data-ttu-id="e3b4b-127">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-128">dependencyVersion (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="e3b4b-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="e3b4b-129">Varsayılan `DependencyVersion` değeri paket yükleme, geri yükleme ve güncelleştirme, zaman `-DependencyVersion` anahtar doğrudan belirtiliyor.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="e3b4b-130">Bu değer ayrıca NuGet Paket Yöneticisi kullanıcı Arabirimi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="e3b4b-131">Değerler `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="e3b4b-132">globalPackagesFolder (PackageReference yalnızca kullanarak projeleri)</span><span class="sxs-lookup"><span data-stu-id="e3b4b-132">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="e3b4b-133">Varsayılan Genel paketleri klasörün konumu.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-133">The location of the default global packages folder.</span></span> <span data-ttu-id="e3b4b-134">Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-134">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="e3b4b-135">Göreli bir yol projeye özgü kullanılabilir `nuget.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-135">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="e3b4b-136">Bu ayarı önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-136">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="e3b4b-137">repositoryPath (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="e3b4b-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="e3b4b-138">NuGet paketleri yerine varsayılan yükleme konumu `$(Solutiondir)/packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="e3b4b-139">Göreli bir yol projeye özgü kullanılabilir `nuget.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-139">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="e3b4b-140">Bu ayarı önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-140">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="e3b4b-141">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="e3b4b-141">defaultPushSource</span></span> | <span data-ttu-id="e3b4b-142">URL veya yol için bir işlem başka bir paket kaynaklarını bulunmazsa, varsayılan olarak kullanılması gereken paket kaynağının tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-142">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="e3b4b-143">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="e3b4b-143">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="e3b4b-144">Paket kaynaklarını bağlanırken kullanması için proxy ayarlarını; `http_proxy` biçiminde olması gerektiğini `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-144">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="e3b4b-145">Parolaları şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-145">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="e3b4b-146">İçin `no_proxy`, değeri etki alanlarının virgülle ayrılmış listesi olduğu proxy sunucusunu atla.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-146">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="e3b4b-147">Alternatif olarak, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-147">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="e3b4b-148">Ek ayrıntılar için bkz. [NuGet proxy ayarlarını](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-148">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="e3b4b-149">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-149">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="e3b4b-150">SecurityPermission bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-150">bindingRedirects section</span></span>

<span data-ttu-id="e3b4b-151">Bir paketi yüklendiğinde NuGet otomatik bağlama yeniden yönlendirmeleri yapar paylaşamayacağını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-151">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="e3b4b-152">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-152">Key</span></span> | <span data-ttu-id="e3b4b-153">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-153">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-154">Atla</span><span class="sxs-lookup"><span data-stu-id="e3b4b-154">skip</span></span> | <span data-ttu-id="e3b4b-155">Otomatik bağlama yeniden yönlendirmeleri atlanmayacağını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-155">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="e3b4b-156">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-156">The default is false.</span></span> |

<span data-ttu-id="e3b4b-157">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-157">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="e3b4b-158">packageRestore bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-158">packageRestore section</span></span>

<span data-ttu-id="e3b4b-159">Denetimleri paket geri yükleme sırasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="e3b4b-160">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-160">Key</span></span> | <span data-ttu-id="e3b4b-161">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-162">Etkin</span><span class="sxs-lookup"><span data-stu-id="e3b4b-162">enabled</span></span> | <span data-ttu-id="e3b4b-163">NuGet otomatik geri yükleme gerçekleştirme olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="e3b4b-164">Ayrıca `EnableNuGetPackageRestore` ortam değişkeni değerinin `True` yerine bu anahtarı yapılandırma dosyasında ayarı.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="e3b4b-165">otomatik</span><span class="sxs-lookup"><span data-stu-id="e3b4b-165">automatic</span></span> | <span data-ttu-id="e3b4b-166">NuGet eksik paketleri için bir yapı sırasında denetleyin olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="e3b4b-167">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="e3b4b-168">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="e3b4b-168">solution section</span></span>

<span data-ttu-id="e3b4b-169">Denetimleri olmadığını `packages` bir çözüm klasörü kaynak denetimine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="e3b4b-170">Bu bölüm yalnızca çalışır `nuget.config` çözüm klasöründe bulunan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-170">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="e3b4b-171">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-171">Key</span></span> | <span data-ttu-id="e3b4b-172">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="e3b4b-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="e3b4b-174">Kaynak denetimi ile çalışırken packages klasörünü yoksay verilip verilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="e3b4b-175">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-175">The default value is false.</span></span> |

<span data-ttu-id="e3b4b-176">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="e3b4b-177">Paket kaynak bölümler</span><span class="sxs-lookup"><span data-stu-id="e3b4b-177">Package source sections</span></span>

<span data-ttu-id="e3b4b-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, Ve `disabledPackageSources` birlikte yükleme, geri yükleme ve güncelleştirme işlemleri sırasında NuGet paketi depoları ile nasıl çalıştığını yapılandırmak için tüm işler.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="e3b4b-179">[ `nuget sources` Komut](../tools/cli-ref-sources.md) dışında bu ayarları yönetmek için genel olarak kullanılan `apikeys` hangi kullanılarak yönetilir [ `nuget setapikey` komut](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="e3b4b-180">Nuget.org kaynak URL'si Not `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="e3b4b-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="e3b4b-181">packageSources</span></span>

<span data-ttu-id="e3b4b-182">Tüm bilinen paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-182">Lists all known package sources.</span></span> <span data-ttu-id="e3b4b-183">Geri yükleme işlemleri sırasında ve herhangi bir projeyi PackageReference biçimi kullanarak ile sırası göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="e3b4b-184">NuGet kaynakları sırasını yükleme için uyar ve güncelleştirme işlemleri kullanarak projeleriyle `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="e3b4b-185">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-185">Key</span></span> | <span data-ttu-id="e3b4b-186">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-187">(adı paket kaynağına atamak için)</span><span class="sxs-lookup"><span data-stu-id="e3b4b-187">(name to assign to the package source)</span></span> | <span data-ttu-id="e3b4b-188">Yol veya paket kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="e3b4b-189">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="e3b4b-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="e3b4b-190">packageSourceCredentials</span></span>

<span data-ttu-id="e3b4b-191">Kullanıcı adları ve parolalar kaynakları, genellikle ile belirtilen için depolar `-username` ve `-password` ile geçer `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="e3b4b-192">Parolaları sürece varsayılan olarak şifrelenmiş `-storepasswordincleartext` seçeneği de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="e3b4b-193">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-193">Key</span></span> | <span data-ttu-id="e3b4b-194">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-195">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="e3b4b-195">username</span></span> | <span data-ttu-id="e3b4b-196">Kaynak düz metin biçiminde kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="e3b4b-197">Parola</span><span class="sxs-lookup"><span data-stu-id="e3b4b-197">password</span></span> | <span data-ttu-id="e3b4b-198">Kaynağı için şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="e3b4b-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="e3b4b-199">cleartextpassword</span></span> | <span data-ttu-id="e3b4b-200">Kaynağı için şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="e3b4b-201">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="e3b4b-201">**Example:**</span></span>

<span data-ttu-id="e3b4b-202">Yapılandırma dosyasında `<packageSourceCredentials>` öğeyi içeren her bir geçerli kaynak adı için alt düğümleri (adında boşluklar ile değiştirilir `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="e3b4b-203">Diğer bir deyişle, "Contoso" ve "Test kaynağı" olarak adlandırılan kaynaklar için yapılandırma dosyasına aşağıdaki şifrelenmiş parolalar kullanırken içerir:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="e3b4b-204">Şifrelenmemiş parolaları kullanırken:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="e3b4b-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="e3b4b-205">apikeys</span></span>

<span data-ttu-id="e3b4b-206">Depolar ile belirlenen API anahtar kimlik doğrulaması kullanan kaynakları için anahtarları [ `nuget setapikey` komut](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="e3b4b-207">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-207">Key</span></span> | <span data-ttu-id="e3b4b-208">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-209">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="e3b4b-209">(source URL)</span></span> | <span data-ttu-id="e3b4b-210">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-210">The encrypted API key.</span></span> |

<span data-ttu-id="e3b4b-211">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="e3b4b-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="e3b4b-212">disabledPackageSources</span></span>

<span data-ttu-id="e3b4b-213">Şu anda devre dışı bırakılmış kaynakları belirledik.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-213">Identified currently disabled sources.</span></span> <span data-ttu-id="e3b4b-214">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-214">May be empty.</span></span>

| <span data-ttu-id="e3b4b-215">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-215">Key</span></span> | <span data-ttu-id="e3b4b-216">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-217">(kaynak adı)</span><span class="sxs-lookup"><span data-stu-id="e3b4b-217">(name of source)</span></span> | <span data-ttu-id="e3b4b-218">Kaynak etkinleştirilip etkinleştirilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="e3b4b-219">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="e3b4b-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="e3b4b-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="e3b4b-220">activePackageSource</span></span>

<span data-ttu-id="e3b4b-221">*(yalnızca 2.x; 3.x+ içinde kullanım dışı)*</span><span class="sxs-lookup"><span data-stu-id="e3b4b-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="e3b4b-222">Etkin kaynak tanımlayan veya toplama tüm kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="e3b4b-223">Anahtar</span><span class="sxs-lookup"><span data-stu-id="e3b4b-223">Key</span></span> | <span data-ttu-id="e3b4b-224">Değer</span><span class="sxs-lookup"><span data-stu-id="e3b4b-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="e3b4b-225">(kaynak adı) veya `All`</span><span class="sxs-lookup"><span data-stu-id="e3b4b-225">(name of source) or `All`</span></span> | <span data-ttu-id="e3b4b-226">Anahtarı bir kaynak adı ise kaynak yolu veya URL değerdir.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="e3b4b-227">Varsa `All`, değeri `(Aggregate source)` Aksi durumda devre dışı paket kaynaklarının tümüne birleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="e3b4b-228">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="e3b4b-229">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="e3b4b-229">Using environment variables</span></span>

<span data-ttu-id="e3b4b-230">Ortam değişkenleri kullanabilirsiniz `nuget.config` çalışma zamanında değerleri (ayarları uygulamak için NuGet 3.4 +).</span><span class="sxs-lookup"><span data-stu-id="e3b4b-230">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="e3b4b-231">Örneğin, varsa `HOME` Windows ortam değişkeni ayarlandığında `c:\users\username`, ardından değerini `%HOME%\NuGetRepository` dosya yapılandırmada çözümler `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="e3b4b-232">Benzer şekilde, varsa `HOME` Mac/Linux üzerinde ayarlanır `/home/myStuff`, ardından `%HOME%/NuGetRepository` dosya yapılandırmada çözümler `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="e3b4b-233">Bir ortam değişkeni bulunamadı, NuGet yapılandırma dosyasından değişmez değer kullanır.</span><span class="sxs-lookup"><span data-stu-id="e3b4b-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="e3b4b-234">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="e3b4b-234">Example config file</span></span>

<span data-ttu-id="e3b4b-235">Aşağıda bir örnek verilmiştir `nuget.config` ayar gösterilmektedir dosyanın:</span><span class="sxs-lookup"><span data-stu-id="e3b4b-235">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
</configuration>
```
