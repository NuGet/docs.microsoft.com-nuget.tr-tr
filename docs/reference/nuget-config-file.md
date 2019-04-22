---
title: nuget.config dosyası başvurusu
description: NuGet.Config dosyası başvurusu yapılandırma, SecurityPermission packageRestore, çözüm ve packageSource bölümler dahil olmak üzere.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911094"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="74c10-103">nuget.config başvurusu</span><span class="sxs-lookup"><span data-stu-id="74c10-103">nuget.config reference</span></span>

<span data-ttu-id="74c10-104">NuGet davranışını farklı ayarları tarafından denetlenir `NuGet.Config` dosyaları açıklandığı [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="74c10-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="74c10-105">`nuget.config` bir üst düzey içeren bir XML dosyası `<configuration>` düğümü, ardından bu konuda açıklanan bölüm öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="74c10-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="74c10-106">Her bölüm, sıfır veya daha fazla öğe içerir.</span><span class="sxs-lookup"><span data-stu-id="74c10-106">Each section contains zero or more items.</span></span> <span data-ttu-id="74c10-107">Bkz: [örnek yapılandırma dosyası](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="74c10-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="74c10-108">Ayar adları büyük/küçük harfe ve değerlerini kullanabilirsiniz [ortam değişkenlerini](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="74c10-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="74c10-109">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="74c10-109">In this topic:</span></span>

- [<span data-ttu-id="74c10-110">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-110">config section</span></span>](#config-section)
- [<span data-ttu-id="74c10-111">SecurityPermission bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="74c10-112">packageRestore bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="74c10-113">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="74c10-114">[Paket kaynak bölümler](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="74c10-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="74c10-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="74c10-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="74c10-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="74c10-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="74c10-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="74c10-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="74c10-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="74c10-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="74c10-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="74c10-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="74c10-120">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="74c10-121">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="74c10-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="74c10-122">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="74c10-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="74c10-123">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-123">config section</span></span>

<span data-ttu-id="74c10-124">Kullanarak ayarlayabileceğiniz çeşitli yapılandırma ayarlarını içeren [ `nuget config` komut](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="74c10-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="74c10-125">`dependencyVersion` ve `repositoryPath` kullanarak projeleri için geçerli `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="74c10-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="74c10-126">`globalPackagesFolder` PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="74c10-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="74c10-127">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-127">Key</span></span> | <span data-ttu-id="74c10-128">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-129">dependencyVersion (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="74c10-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="74c10-130">Varsayılan `DependencyVersion` değeri paket yükleme, geri yükleme ve güncelleştirme, zaman `-DependencyVersion` anahtar doğrudan belirtiliyor.</span><span class="sxs-lookup"><span data-stu-id="74c10-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="74c10-131">Bu değer ayrıca NuGet Paket Yöneticisi kullanıcı Arabirimi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="74c10-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="74c10-132">Değerler `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="74c10-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="74c10-133">globalPackagesFolder (PackageReference yalnızca kullanarak projeleri)</span><span class="sxs-lookup"><span data-stu-id="74c10-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="74c10-134">Varsayılan Genel paketleri klasörün konumu.</span><span class="sxs-lookup"><span data-stu-id="74c10-134">The location of the default global packages folder.</span></span> <span data-ttu-id="74c10-135">Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="74c10-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="74c10-136">Göreli bir yol projeye özgü kullanılabilir `nuget.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="74c10-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="74c10-137">Bu ayarı önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="74c10-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="74c10-138">repositoryPath (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="74c10-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="74c10-139">NuGet paketleri yerine varsayılan yükleme konumu `$(Solutiondir)/packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="74c10-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="74c10-140">Göreli bir yol projeye özgü kullanılabilir `nuget.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="74c10-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="74c10-141">Bu ayarı önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="74c10-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="74c10-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="74c10-142">defaultPushSource</span></span> | <span data-ttu-id="74c10-143">URL veya yol için bir işlem başka bir paket kaynaklarını bulunmazsa, varsayılan olarak kullanılması gereken paket kaynağının tanımlar.</span><span class="sxs-lookup"><span data-stu-id="74c10-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="74c10-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="74c10-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="74c10-145">Paket kaynaklarını bağlanırken kullanması için proxy ayarlarını; `http_proxy` biçiminde olması gerektiğini `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="74c10-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="74c10-146">Parolaları şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="74c10-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="74c10-147">İçin `no_proxy`, değeri etki alanlarının virgülle ayrılmış listesi olduğu proxy sunucusunu atla.</span><span class="sxs-lookup"><span data-stu-id="74c10-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="74c10-148">Alternatif olarak, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74c10-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="74c10-149">Ek ayrıntılar için bkz. [NuGet proxy ayarlarını](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="74c10-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="74c10-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="74c10-150">signatureValidationMode</span></span> | <span data-ttu-id="74c10-151">Paket yüklemesi için paket imzaları doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="74c10-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="74c10-152">Değerler `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="74c10-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="74c10-153">Varsayılan olarak `accept`.</span><span class="sxs-lookup"><span data-stu-id="74c10-153">Defaults to `accept`.</span></span>

<span data-ttu-id="74c10-154">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="74c10-155">SecurityPermission bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-155">bindingRedirects section</span></span>

<span data-ttu-id="74c10-156">Bir paketi yüklendiğinde NuGet otomatik bağlama yeniden yönlendirmeleri yapar paylaşamayacağını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="74c10-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="74c10-157">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-157">Key</span></span> | <span data-ttu-id="74c10-158">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-159">Atla</span><span class="sxs-lookup"><span data-stu-id="74c10-159">skip</span></span> | <span data-ttu-id="74c10-160">Otomatik bağlama yeniden yönlendirmeleri atlanmayacağını belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="74c10-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="74c10-161">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="74c10-161">The default is false.</span></span> |

<span data-ttu-id="74c10-162">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="74c10-163">packageRestore bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-163">packageRestore section</span></span>

<span data-ttu-id="74c10-164">Denetimleri paket geri yükleme sırasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="74c10-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="74c10-165">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-165">Key</span></span> | <span data-ttu-id="74c10-166">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-167">Etkin</span><span class="sxs-lookup"><span data-stu-id="74c10-167">enabled</span></span> | <span data-ttu-id="74c10-168">NuGet otomatik geri yükleme gerçekleştirme olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="74c10-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="74c10-169">Ayrıca `EnableNuGetPackageRestore` ortam değişkeni değerinin `True` yerine bu anahtarı yapılandırma dosyasında ayarı.</span><span class="sxs-lookup"><span data-stu-id="74c10-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="74c10-170">otomatik</span><span class="sxs-lookup"><span data-stu-id="74c10-170">automatic</span></span> | <span data-ttu-id="74c10-171">NuGet eksik paketleri için bir yapı sırasında denetleyin olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="74c10-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="74c10-172">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="74c10-173">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-173">solution section</span></span>

<span data-ttu-id="74c10-174">Denetimleri olmadığını `packages` bir çözüm klasörü kaynak denetimine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="74c10-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="74c10-175">Bu bölüm yalnızca çalışır `nuget.config` çözüm klasöründe bulunan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="74c10-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="74c10-176">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-176">Key</span></span> | <span data-ttu-id="74c10-177">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="74c10-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="74c10-179">Kaynak denetimi ile çalışırken packages klasörünü yoksay verilip verilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="74c10-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="74c10-180">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="74c10-180">The default value is false.</span></span> |

<span data-ttu-id="74c10-181">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="74c10-182">Paket kaynak bölümler</span><span class="sxs-lookup"><span data-stu-id="74c10-182">Package source sections</span></span>

<span data-ttu-id="74c10-183">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` Ve `trustedSigners` birlikte yükleme, geri yükleme ve güncelleştirme işlemleri sırasında NuGet paketi depoları ile nasıl çalıştığını yapılandırmak için tüm işler.</span><span class="sxs-lookup"><span data-stu-id="74c10-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="74c10-184">[ `nuget sources` Komut](../tools/cli-ref-sources.md) dışında bu ayarları yönetmek için genel olarak kullanılan `apikeys` hangi kullanılarak yönetilir [ `nuget setapikey` komut](../tools/cli-ref-setapikey.md), ve `trustedSigners` hangi yönetilir kullanarak [ `nuget trusted-signers` komut](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="74c10-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="74c10-185">Nuget.org kaynak URL'si Not `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="74c10-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="74c10-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="74c10-186">packageSources</span></span>

<span data-ttu-id="74c10-187">Tüm bilinen paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="74c10-187">Lists all known package sources.</span></span> <span data-ttu-id="74c10-188">Geri yükleme işlemleri sırasında ve herhangi bir projeyi PackageReference biçimi kullanarak ile sırası göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="74c10-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="74c10-189">NuGet kaynakları sırasını yükleme için uyar ve güncelleştirme işlemleri kullanarak projeleriyle `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="74c10-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="74c10-190">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-190">Key</span></span> | <span data-ttu-id="74c10-191">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-192">(adı paket kaynağına atamak için)</span><span class="sxs-lookup"><span data-stu-id="74c10-192">(name to assign to the package source)</span></span> | <span data-ttu-id="74c10-193">Yol veya paket kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="74c10-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="74c10-194">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="74c10-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="74c10-195">packageSourceCredentials</span></span>

<span data-ttu-id="74c10-196">Kullanıcı adları ve parolalar kaynakları, genellikle ile belirtilen için depolar `-username` ve `-password` ile geçer `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="74c10-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="74c10-197">Parolaları sürece varsayılan olarak şifrelenmiş `-storepasswordincleartext` seçeneği de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="74c10-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="74c10-198">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-198">Key</span></span> | <span data-ttu-id="74c10-199">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-200">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="74c10-200">username</span></span> | <span data-ttu-id="74c10-201">Kaynak düz metin biçiminde kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="74c10-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="74c10-202">password</span><span class="sxs-lookup"><span data-stu-id="74c10-202">password</span></span> | <span data-ttu-id="74c10-203">Kaynağı için şifrelenmiş parola.</span><span class="sxs-lookup"><span data-stu-id="74c10-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="74c10-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="74c10-204">cleartextpassword</span></span> | <span data-ttu-id="74c10-205">Kaynağı için şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="74c10-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="74c10-206">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="74c10-206">**Example:**</span></span>

<span data-ttu-id="74c10-207">Yapılandırma dosyasında `<packageSourceCredentials>` öğeyi içeren her bir geçerli kaynak adı için alt düğümleri (adında boşluklar ile değiştirilir `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="74c10-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="74c10-208">Diğer bir deyişle, "Contoso" ve "Test kaynağı" olarak adlandırılan kaynaklar için yapılandırma dosyasına aşağıdaki şifrelenmiş parolalar kullanırken içerir:</span><span class="sxs-lookup"><span data-stu-id="74c10-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="74c10-209">Şifrelenmemiş parolaları kullanırken:</span><span class="sxs-lookup"><span data-stu-id="74c10-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="74c10-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="74c10-210">apikeys</span></span>

<span data-ttu-id="74c10-211">Depolar ile belirlenen API anahtar kimlik doğrulaması kullanan kaynakları için anahtarları [ `nuget setapikey` komut](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="74c10-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="74c10-212">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-212">Key</span></span> | <span data-ttu-id="74c10-213">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-214">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="74c10-214">(source URL)</span></span> | <span data-ttu-id="74c10-215">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="74c10-215">The encrypted API key.</span></span> |

<span data-ttu-id="74c10-216">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="74c10-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="74c10-217">disabledPackageSources</span></span>

<span data-ttu-id="74c10-218">Şu anda devre dışı bırakılmış kaynakları belirledik.</span><span class="sxs-lookup"><span data-stu-id="74c10-218">Identified currently disabled sources.</span></span> <span data-ttu-id="74c10-219">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="74c10-219">May be empty.</span></span>

| <span data-ttu-id="74c10-220">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-220">Key</span></span> | <span data-ttu-id="74c10-221">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-222">(kaynak adı)</span><span class="sxs-lookup"><span data-stu-id="74c10-222">(name of source)</span></span> | <span data-ttu-id="74c10-223">Kaynak etkinleştirilip etkinleştirilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="74c10-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="74c10-224">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="74c10-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="74c10-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="74c10-225">activePackageSource</span></span>

<span data-ttu-id="74c10-226">*(yalnızca 2.x; 3.x+ içinde kullanım dışı)*</span><span class="sxs-lookup"><span data-stu-id="74c10-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="74c10-227">Etkin kaynak tanımlayan veya toplama tüm kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="74c10-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="74c10-228">Anahtar</span><span class="sxs-lookup"><span data-stu-id="74c10-228">Key</span></span> | <span data-ttu-id="74c10-229">Değer</span><span class="sxs-lookup"><span data-stu-id="74c10-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="74c10-230">(kaynak adı) veya `All`</span><span class="sxs-lookup"><span data-stu-id="74c10-230">(name of source) or `All`</span></span> | <span data-ttu-id="74c10-231">Anahtarı bir kaynak adı ise kaynak yolu veya URL değerdir.</span><span class="sxs-lookup"><span data-stu-id="74c10-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="74c10-232">Varsa `All`, değeri `(Aggregate source)` Aksi durumda devre dışı paket kaynaklarının tümüne birleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="74c10-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="74c10-233">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="74c10-234">trustedSigners bölümü</span><span class="sxs-lookup"><span data-stu-id="74c10-234">trustedSigners section</span></span>

<span data-ttu-id="74c10-235">Depoları İmzalayanları paketi yüklemek veya geri yükleme sırasında izin vermek için kullanılan güvenilir.</span><span class="sxs-lookup"><span data-stu-id="74c10-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="74c10-236">Kullanıcı ayarlar, bu liste boş olamaz `signatureValidationMode` için `require`.</span><span class="sxs-lookup"><span data-stu-id="74c10-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="74c10-237">Bu bölümde ile güncelleştirilebilir [ `nuget trusted-signers` komut](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="74c10-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="74c10-238">**Şema**:</span><span class="sxs-lookup"><span data-stu-id="74c10-238">**Schema**:</span></span>

<span data-ttu-id="74c10-239">Güvenilen imzalayan koleksiyonu vardır `certificate` verilen imzalayan tanımlayan tüm sertifikaları listeleme öğeleri.</span><span class="sxs-lookup"><span data-stu-id="74c10-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="74c10-240">Güvenilen imzalayan olabilir bir `Author` veya `Repository`.</span><span class="sxs-lookup"><span data-stu-id="74c10-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="74c10-241">Güvenilen bir *depo* ayrıca belirtir `serviceIndex` deponun (sahip geçerli bir `https` URI'si) ve isteğe bağlı olarak noktalı virgülle ayrılmış listesini belirtebilirsiniz `owners` daha güvenilir kim kısıtlamak için Bu özel depodan.</span><span class="sxs-lookup"><span data-stu-id="74c10-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="74c10-242">Sertifika parmak izi için kullanılan desteklenen karma algoritmaları `SHA256`, `SHA384` ve `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="74c10-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="74c10-243">Varsa bir `certificate` belirtir `allowUntrustedRoot` olarak `true` verilen sertifika zinciri güvenilmeyen bir kökü için imza doğrulaması bir parçası olarak sertifika zinciri oluşturulurken izin verilir.</span><span class="sxs-lookup"><span data-stu-id="74c10-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="74c10-244">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="74c10-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="74c10-245">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="74c10-245">Using environment variables</span></span>

<span data-ttu-id="74c10-246">Ortam değişkenleri kullanabilirsiniz `nuget.config` çalışma zamanında değerleri (ayarları uygulamak için NuGet 3.4 +).</span><span class="sxs-lookup"><span data-stu-id="74c10-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="74c10-247">Örneğin, varsa `HOME` Windows ortam değişkeni ayarlandığında `c:\users\username`, ardından değerini `%HOME%\NuGetRepository` dosya yapılandırmada çözümler `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="74c10-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="74c10-248">Benzer şekilde, varsa `HOME` Mac/Linux üzerinde ayarlanır `/home/myStuff`, ardından `%HOME%/NuGetRepository` dosya yapılandırmada çözümler `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="74c10-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="74c10-249">Bir ortam değişkeni bulunamadı, NuGet yapılandırma dosyasından değişmez değer kullanır.</span><span class="sxs-lookup"><span data-stu-id="74c10-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="74c10-250">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="74c10-250">Example config file</span></span>

<span data-ttu-id="74c10-251">Aşağıda bir örnek verilmiştir `nuget.config` ayar gösterilmektedir dosyanın:</span><span class="sxs-lookup"><span data-stu-id="74c10-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
