---
title: NuGet.Config dosyasındaki başvurusu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet.Config dosya başvurusu yapılandırma, bindingRedirects, packageRestore, çözüm ve packageSource bölümler dahil olmak üzere.
keywords: NuGet.Config dosyasındaki, NuGet yapılandırma başvurusu, NuGet yapılandırma seçenekleri
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="bf710-104">NuGet.Config başvurusu</span><span class="sxs-lookup"><span data-stu-id="bf710-104">NuGet.Config reference</span></span>

<span data-ttu-id="bf710-105">NuGet davranışı farklı ayarları tarafından denetlenir `NuGet.Config` dosyaları açıklandığı gibi [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="bf710-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="bf710-106">`NuGet.Config` bir üst düzey içeren bir XML dosyası `<configuration>` düğümü, bu konuda açıklanan bölümünün öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="bf710-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="bf710-107">Her bölüm sıfır veya daha fazla içerir `<add>` öğeleriyle `key` ve `value` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="bf710-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="bf710-108">Bkz: [örnekler yapılandırma dosyası](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="bf710-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="bf710-109">Ayar adları büyük küçük harf duyarsız ve değerleri kullanabilir [ortam değişkenleri](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="bf710-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="bf710-110">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="bf710-110">In this topic:</span></span>

- [<span data-ttu-id="bf710-111">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-111">config section</span></span>](#config-section)
- [<span data-ttu-id="bf710-112">bindingRedirects bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="bf710-113">packageRestore section</span><span class="sxs-lookup"><span data-stu-id="bf710-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="bf710-114">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="bf710-115">[Paket kaynak bölümler](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="bf710-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="bf710-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="bf710-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="bf710-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="bf710-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="bf710-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="bf710-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="bf710-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="bf710-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="bf710-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="bf710-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="bf710-121">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bf710-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="bf710-122">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="bf710-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="bf710-123">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-123">config section</span></span>

<span data-ttu-id="bf710-124">Kullanılarak ayarlanabilir çeşitli yapılandırma ayarlarını içeren [ `nuget config` komutu](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="bf710-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="bf710-125">`dependencyVersion` ve `repositoryPath` kullanarak projeleri için geçerli `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="bf710-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="bf710-126">`globalPackagesFolder` PackageReference biçimini kullanarak projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bf710-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="bf710-127">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-127">Key</span></span> | <span data-ttu-id="bf710-128">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-129">dependencyVersion (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="bf710-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="bf710-130">Varsayılan `DependencyVersion` paketi yükle, geri yükleme ve güncelleştirme için değer olduğunda `-DependencyVersion` anahtar doğrudan belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="bf710-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="bf710-131">Bu değer ayrıca NuGet Paket Yöneticisi kullanıcı Arabirimi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf710-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="bf710-132">Değerler `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="bf710-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="bf710-133">globalPackagesFolder (PackageReference yalnızca kullanarak projeleri)</span><span class="sxs-lookup"><span data-stu-id="bf710-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="bf710-134">Varsayılan Genel paketler klasörü konumu.</span><span class="sxs-lookup"><span data-stu-id="bf710-134">The location of the default global packages folder.</span></span> <span data-ttu-id="bf710-135">Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="bf710-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="bf710-136">Göreli bir yol projeye özgü içinde kullanılabilir `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bf710-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="bf710-137">Bu ayar önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="bf710-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="bf710-138">repositoryPath (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="bf710-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="bf710-139">NuGet paketleri yerine varsayılan yükleme konumu `$(Solutiondir)/packages` klasörü.</span><span class="sxs-lookup"><span data-stu-id="bf710-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="bf710-140">Göreli bir yol projeye özgü içinde kullanılabilir `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bf710-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="bf710-141">Bu ayar önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="bf710-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="bf710-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="bf710-142">defaultPushSource</span></span> | <span data-ttu-id="bf710-143">URL veya bir işlem için başka bir paket kaynaklarını bulunursa, varsayılan olarak kullanılması gereken paket kaynağının yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bf710-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="bf710-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="bf710-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="bf710-145">Proxy ayarlarını; paket kaynaklarına bağlanırken kullanmak için `http_proxy` biçiminde olmalıdır `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="bf710-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="bf710-146">Parolaları şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="bf710-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="bf710-147">İçin `no_proxy`, değer atlama proxy sunucusu etki alanları virgülle ayrılmış bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bf710-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="bf710-148">Alternatif olarak, bu değerleri http_proxy ve no_proxy ortam değişkenleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf710-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="bf710-149">Daha fazla bilgi için bkz: [NuGet proxy ayarlarını](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="bf710-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="bf710-150">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="bf710-151">bindingRedirects bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-151">bindingRedirects section</span></span>

<span data-ttu-id="bf710-152">Bir paketi yüklendiğinde NuGet otomatik bağlama yeniden yönlendirmeleri yapar olup olmadığını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bf710-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="bf710-153">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-153">Key</span></span> | <span data-ttu-id="bf710-154">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-155">Atla</span><span class="sxs-lookup"><span data-stu-id="bf710-155">skip</span></span> | <span data-ttu-id="bf710-156">Otomatik bağlama yeniden yönlendirmeleri Atla görüntülenmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="bf710-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="bf710-157">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="bf710-157">The default is false.</span></span> |

<span data-ttu-id="bf710-158">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="bf710-159">packageRestore bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-159">packageRestore section</span></span>

<span data-ttu-id="bf710-160">Denetimleri paket geri yüklemesi sırasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bf710-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="bf710-161">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-161">Key</span></span> | <span data-ttu-id="bf710-162">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-163">Etkin</span><span class="sxs-lookup"><span data-stu-id="bf710-163">enabled</span></span> | <span data-ttu-id="bf710-164">NuGet otomatik geri yükleme gerçekleştirmek olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="bf710-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="bf710-165">Ayrıca ayarlayabilirsiniz `EnableNuGetPackageRestore` ortam değişkeni değerini `True` yapılandırma dosyasında bu anahtarı ayarı yerine.</span><span class="sxs-lookup"><span data-stu-id="bf710-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="bf710-166">otomatik</span><span class="sxs-lookup"><span data-stu-id="bf710-166">automatic</span></span> | <span data-ttu-id="bf710-167">NuGet bir yapı sırasında eksik paketleri denetleyip denetlemeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="bf710-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="bf710-168">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="bf710-169">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="bf710-169">solution section</span></span>

<span data-ttu-id="bf710-170">Denetimleri olup olmadığını `packages` klasörü, çözümün kaynak denetiminde yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="bf710-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="bf710-171">Bu bölüm yalnızca çalışır `Nuget.Config` bir çözüm klasördeki dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bf710-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="bf710-172">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-172">Key</span></span> | <span data-ttu-id="bf710-173">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="bf710-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="bf710-175">Kaynak denetimi ile çalışırken, paketler klasörü yoksay tutulmayacağını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="bf710-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="bf710-176">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="bf710-176">The default value is false.</span></span> |

<span data-ttu-id="bf710-177">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="bf710-178">Paket kaynak bölümleri</span><span class="sxs-lookup"><span data-stu-id="bf710-178">Package source sections</span></span>

<span data-ttu-id="bf710-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, Ve `disabledPackageSources` birlikte yükleme, geri yükleme ve güncelleştirme işlemi sırasında NuGet paketi depoları ile nasıl çalıştığını yapılandırmak için tüm iş.</span><span class="sxs-lookup"><span data-stu-id="bf710-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="bf710-180">[ `nuget sources` Komutu](../tools/cli-ref-sources.md) genellikle dışında bu ayarları yönetmek için kullanılan `apikeys` hangi kullanılarak yönetilir [ `nuget setapikey` komutu](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="bf710-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="bf710-181">Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="bf710-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="bf710-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="bf710-182">packageSources</span></span>

<span data-ttu-id="bf710-183">Tüm bilinen paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="bf710-183">Lists all known package sources.</span></span> <span data-ttu-id="bf710-184">Geri yükleme işlemleri sırasında ve PackageReference biçimini kullanarak herhangi bir projeyle sırası göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="bf710-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="bf710-185">NuGet kaynakları sırasını yükleme için uyar ve güncelleştirme işlemleri kullanarak projeleri ile `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="bf710-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="bf710-186">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-186">Key</span></span> | <span data-ttu-id="bf710-187">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-188">Paket kaynağı atamak (ad)</span><span class="sxs-lookup"><span data-stu-id="bf710-188">(name to assign to the package source)</span></span> | <span data-ttu-id="bf710-189">Yolu veya paket kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="bf710-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="bf710-190">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="bf710-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="bf710-191">packageSourceCredentials</span></span>

<span data-ttu-id="bf710-192">Kullanıcı adları ve parolalar genellikle ile belirtilen kaynakları için depolar `-username` ve `-password` ile geçer `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="bf710-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="bf710-193">Parolalar, varsayılan olarak şifrelenir, sürece `-storepasswordincleartext` seçeneği de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf710-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="bf710-194">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-194">Key</span></span> | <span data-ttu-id="bf710-195">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-196">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="bf710-196">username</span></span> | <span data-ttu-id="bf710-197">Düz metin kaynak için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="bf710-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="bf710-198">Parola</span><span class="sxs-lookup"><span data-stu-id="bf710-198">password</span></span> | <span data-ttu-id="bf710-199">Kaynağı şifrelenmiş parolası.</span><span class="sxs-lookup"><span data-stu-id="bf710-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="bf710-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="bf710-200">cleartextpassword</span></span> | <span data-ttu-id="bf710-201">Kaynak şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="bf710-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="bf710-202">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bf710-202">**Example:**</span></span>

<span data-ttu-id="bf710-203">Yapılandırma dosyasındaki `<packageSourceCredentials>` öğesi her bir geçerli kaynak adı için alt düğümleri içerir (adında boşluk ile değiştirilir `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="bf710-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="bf710-204">Diğer bir deyişle, "Contoso" ve "Test kaynağı" adlı kaynakları için yapılandırma dosyası aşağıdaki şifrelenmiş parolalar kullanırken içerir:</span><span class="sxs-lookup"><span data-stu-id="bf710-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="bf710-205">Şifrelenmemiş parolalar kullanırken:</span><span class="sxs-lookup"><span data-stu-id="bf710-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="bf710-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="bf710-206">apikeys</span></span>

<span data-ttu-id="bf710-207">Depolar kümesiyle olarak API anahtar kimlik doğrulaması kullanan kaynakları tuşları [ `nuget setapikey` komutu](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="bf710-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="bf710-208">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-208">Key</span></span> | <span data-ttu-id="bf710-209">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-210">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="bf710-210">(source URL)</span></span> | <span data-ttu-id="bf710-211">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="bf710-211">The encrypted API key.</span></span> |

<span data-ttu-id="bf710-212">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="bf710-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="bf710-213">disabledPackageSources</span></span>

<span data-ttu-id="bf710-214">Şu anda devre dışı bırakılmış kaynakları tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="bf710-214">Identified currently disabled sources.</span></span> <span data-ttu-id="bf710-215">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="bf710-215">May be empty.</span></span>

| <span data-ttu-id="bf710-216">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-216">Key</span></span> | <span data-ttu-id="bf710-217">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-218">(kaynak adı)</span><span class="sxs-lookup"><span data-stu-id="bf710-218">(name of source)</span></span> | <span data-ttu-id="bf710-219">Kaynak devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="bf710-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="bf710-220">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bf710-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="bf710-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="bf710-221">activePackageSource</span></span>

<span data-ttu-id="bf710-222">*(yalnızca 2.x; içinde kullanım dışı 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="bf710-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="bf710-223">Şu anda etkin kaynağını tanımlayan veya toplama tüm kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="bf710-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="bf710-224">Anahtar</span><span class="sxs-lookup"><span data-stu-id="bf710-224">Key</span></span> | <span data-ttu-id="bf710-225">Değer</span><span class="sxs-lookup"><span data-stu-id="bf710-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bf710-226">(kaynak adı) veya `All`</span><span class="sxs-lookup"><span data-stu-id="bf710-226">(name of source) or `All`</span></span> | <span data-ttu-id="bf710-227">Anahtar bir kaynak adı ise, kaynak yolu veya URL'si değerdir.</span><span class="sxs-lookup"><span data-stu-id="bf710-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="bf710-228">Varsa `All`, değer olmalıdır `(Aggregate source)` Aksi durumda devre dışı tüm paket kaynaklarını birleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="bf710-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="bf710-229">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="bf710-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="bf710-230">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bf710-230">Using environment variables</span></span>

<span data-ttu-id="bf710-231">Ortam değişkenleri kullanabilirsiniz `NuGet.Config` değerleri (ayarları uygulamak için NuGet 3.4 +) çalışma süresi.</span><span class="sxs-lookup"><span data-stu-id="bf710-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="bf710-232">Örneğin, varsa `HOME` Windows ortam değişkeni ayarlanır `c:\users\username`, ardından değeri `%HOME%\NuGetRepository` dosya yapılandırmada çözümler `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="bf710-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="bf710-233">Benzer şekilde, varsa `HOME` Mac/Linux'ta kümesine `/home/myStuff`, ardından `$HOME/NuGetRepository` dosya yapılandırmada çözümler `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="bf710-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="bf710-234">Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından hazır değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="bf710-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="bf710-235">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="bf710-235">Example config file</span></span>

<span data-ttu-id="bf710-236">Aşağıda `NuGet.Config` çeşitli ayarlar gösterilmektedir dosyası:</span><span class="sxs-lookup"><span data-stu-id="bf710-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
