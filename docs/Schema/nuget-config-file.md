---
title: "NuGet.Config dosyasındaki başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet.Config dosya başvurusu yapılandırma, bindingRedirects, packageRestore, çözüm ve packageSource bölümler dahil olmak üzere."
keywords: "NuGet.Config dosyasındaki, NuGet yapılandırma başvurusu, NuGet yapılandırma seçenekleri"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9a183b67ae18f4fa5c042f1806f8abcc9b799b77
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="1d2a0-104">NuGet.Config başvurusu</span><span class="sxs-lookup"><span data-stu-id="1d2a0-104">NuGet.Config reference</span></span>

<span data-ttu-id="1d2a0-105">NuGet davranışı farklı ayarları tarafından denetlenir `NuGet.Config` dosyaları açıklandığı gibi [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="1d2a0-106">`NuGet.Config`bir üst düzey içeren bir XML dosyası `<configuration>` düğümü, bu konuda açıklanan bölümünün öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="1d2a0-107">Her bölüm sıfır veya daha fazla içerir `<add>` öğeleriyle `key` ve `value` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="1d2a0-108">Bkz: [örnekler yapılandırma dosyası](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="1d2a0-109">Ayar adları büyük küçük harf duyarsız ve değerleri kullanabilir [ortam değişkenleri](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="1d2a0-110">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-110">In this topic:</span></span>

- [<span data-ttu-id="1d2a0-111">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-111">config section</span></span>](#config-section)
- [<span data-ttu-id="1d2a0-112">bindingRedirects bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="1d2a0-113">packageRestore section</span><span class="sxs-lookup"><span data-stu-id="1d2a0-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="1d2a0-114">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="1d2a0-115">[Paket kaynak bölümler](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="1d2a0-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="1d2a0-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="1d2a0-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="1d2a0-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="1d2a0-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="1d2a0-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="1d2a0-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="1d2a0-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="1d2a0-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="1d2a0-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="1d2a0-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="1d2a0-121">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1d2a0-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="1d2a0-122">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="1d2a0-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="1d2a0-123">yapılandırma bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-123">config section</span></span>

<span data-ttu-id="1d2a0-124">Kullanılarak ayarlanabilir çeşitli yapılandırma ayarlarını içeren [ `nuget config` komutu](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="1d2a0-125">Not: `dependencyVersion` ve `repositoryPath` kullanarak projeleri için geçerli `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="1d2a0-126">`globalPackagesFolder`PackageReference biçimini kullanarak projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="1d2a0-127">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-127">Key</span></span> | <span data-ttu-id="1d2a0-128">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-129">dependencyVersion (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="1d2a0-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="1d2a0-130">Varsayılan `DependencyVersion` paketi yükle, geri yükleme ve güncelleştirme için değer olduğunda `-DependencyVersion` anahtar doğrudan belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="1d2a0-131">Bu değer ayrıca NuGet Paket Yöneticisi kullanıcı Arabirimi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="1d2a0-132">Değerler `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="1d2a0-133">globalPackagesFolder (kullanmıyorsa projeleri `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="1d2a0-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="1d2a0-134">Varsayılan Genel paketler klasörü konumu.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-134">The location of the default global packages folder.</span></span> <span data-ttu-id="1d2a0-135">Varsayılan değer `%USERPROFILE%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="1d2a0-136">Göreli bir yol projeye özgü içinde kullanılabilir `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="1d2a0-137">repositoryPath (`packages.config` yalnızca)</span><span class="sxs-lookup"><span data-stu-id="1d2a0-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="1d2a0-138">NuGet paketleri yerine varsayılan yükleme konumu `$(Solutiondir)/packages` klasörü.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="1d2a0-139">Göreli bir yol projeye özgü içinde kullanılabilir `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="1d2a0-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="1d2a0-140">defaultPushSource</span></span> | <span data-ttu-id="1d2a0-141">URL veya bir işlem için başka bir paket kaynaklarını bulunursa, varsayılan olarak kullanılması gereken paket kaynağının yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="1d2a0-142">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="1d2a0-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="1d2a0-143">Proxy ayarlarını; paket kaynaklarına bağlanırken kullanmak için `http_proxy` biçiminde olmalıdır `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="1d2a0-144">Parolaları şifrelenir ve el ile eklenemez.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="1d2a0-145">İçin `no_proxy`, değer atlama proxy sunucusu etki alanları virgülle ayrılmış bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="1d2a0-146">Alternatif olarak, bu değerleri http_proxy ve no_proxy ortam değişkenleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="1d2a0-147">Daha fazla bilgi için bkz: [NuGet proxy ayarlarını](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="1d2a0-148">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="1d2a0-149">bindingRedirects bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-149">bindingRedirects section</span></span>

<span data-ttu-id="1d2a0-150">Bir paketi yüklendiğinde NuGet otomatik bağlama yeniden yönlendirmeleri yapar olup olmadığını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="1d2a0-151">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-151">Key</span></span> | <span data-ttu-id="1d2a0-152">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-153">Atla</span><span class="sxs-lookup"><span data-stu-id="1d2a0-153">skip</span></span> | <span data-ttu-id="1d2a0-154">Otomatik bağlama yeniden yönlendirmeleri Atla görüntülenmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="1d2a0-155">Varsayılan olarak yanlıştır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-155">The default is false.</span></span> |

<span data-ttu-id="1d2a0-156">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="1d2a0-157">packageRestore bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-157">packageRestore section</span></span>

<span data-ttu-id="1d2a0-158">*2.7 + göz ardı*</span><span class="sxs-lookup"><span data-stu-id="1d2a0-158">*Ignored in 2.7+*</span></span>

<span data-ttu-id="1d2a0-159">Denetimleri paket geri yüklemesi sırasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="1d2a0-160">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-160">Key</span></span> | <span data-ttu-id="1d2a0-161">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-162">Etkin</span><span class="sxs-lookup"><span data-stu-id="1d2a0-162">enabled</span></span> | <span data-ttu-id="1d2a0-163">NuGet otomatik geri yükleme gerçekleştirmek olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="1d2a0-164">Ayrıca ayarlayabilirsiniz `EnableNuGetPackageRestore` ortam değişkeni değerini `True` yapılandırma dosyasında bu anahtarı ayarı yerine.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="1d2a0-165">otomatik</span><span class="sxs-lookup"><span data-stu-id="1d2a0-165">automatic</span></span> | <span data-ttu-id="1d2a0-166">NuGet bir yapı sırasında eksik paketleri denetleyip denetlemeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="1d2a0-167">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="1d2a0-168">Çözüm bölümü</span><span class="sxs-lookup"><span data-stu-id="1d2a0-168">solution section</span></span>

<span data-ttu-id="1d2a0-169">Denetimleri olup olmadığını `packages` klasörü, çözümün kaynak denetiminde yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="1d2a0-170">Bu bölüm yalnızca çalışır `Nuget.Config` bir çözüm klasördeki dosyaları.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-170">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="1d2a0-171">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-171">Key</span></span> | <span data-ttu-id="1d2a0-172">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="1d2a0-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="1d2a0-174">Kaynak denetimi ile çalışırken, paketler klasörü yoksay tutulmayacağını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="1d2a0-175">Varsayılan değer false'tur.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-175">The default value is false.</span></span> |

<span data-ttu-id="1d2a0-176">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="1d2a0-177">Paket kaynak bölümleri</span><span class="sxs-lookup"><span data-stu-id="1d2a0-177">Package source sections</span></span>

<span data-ttu-id="1d2a0-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, Ve `disabledPackageSources` birlikte yükleme, geri yükleme ve güncelleştirme işlemi sırasında NuGet paketi depoları ile nasıl çalıştığını yapılandırmak için tüm iş.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="1d2a0-179">[ `nuget sources` Komutu](../tools/cli-ref-sources.md) genellikle dışında bu ayarları yönetmek için kullanılan `apikeys` hangi kullanılarak yönetilir [ `nuget setapikey` komutu](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="1d2a0-180">Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="1d2a0-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="1d2a0-181">packageSources</span></span>

<span data-ttu-id="1d2a0-182">Tüm bilinen paket kaynaklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-182">Lists all known package sources.</span></span>

| <span data-ttu-id="1d2a0-183">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-183">Key</span></span> | <span data-ttu-id="1d2a0-184">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-184">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-185">Paket kaynağı atamak (ad)</span><span class="sxs-lookup"><span data-stu-id="1d2a0-185">(name to assign to the package source)</span></span> | <span data-ttu-id="1d2a0-186">Yolu veya paket kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-186">The path or URL of the package source.</span></span> |

<span data-ttu-id="1d2a0-187">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-187">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="1d2a0-188">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="1d2a0-188">packageSourceCredentials</span></span>

<span data-ttu-id="1d2a0-189">Kullanıcı adları ve parolalar genellikle ile belirtilen kaynakları için depolar `-username` ve `-password` ile geçer `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-189">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="1d2a0-190">Parolalar, varsayılan olarak şifrelenir, sürece `-storepasswordincleartext` seçeneği de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-190">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="1d2a0-191">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-191">Key</span></span> | <span data-ttu-id="1d2a0-192">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-192">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-193">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="1d2a0-193">username</span></span> | <span data-ttu-id="1d2a0-194">Düz metin kaynak için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-194">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="1d2a0-195">Parola</span><span class="sxs-lookup"><span data-stu-id="1d2a0-195">password</span></span> | <span data-ttu-id="1d2a0-196">Kaynağı şifrelenmiş parolası.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-196">The encrypted password for the source.</span></span> |
| <span data-ttu-id="1d2a0-197">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="1d2a0-197">cleartextpassword</span></span> | <span data-ttu-id="1d2a0-198">Kaynak şifrelenmemiş parola.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-198">The unencrypted password for the source.</span></span> |

<span data-ttu-id="1d2a0-199">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1d2a0-199">**Example:**</span></span>

<span data-ttu-id="1d2a0-200">Yapılandırma dosyasındaki `<packageSourceCredentials>` öğesi her bir geçerli kaynak adı için alt düğümleri içerir (adında boşluk ile değiştirilir `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-200">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="1d2a0-201">Diğer bir deyişle, "Contoso" ve "Test kaynağı" adlı kaynakları için yapılandırma dosyası aşağıdaki şifrelenmiş parolalar kullanırken içerir:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-201">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="1d2a0-202">Şifrelenmemiş parolalar kullanırken:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-202">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="1d2a0-203">apikeys</span><span class="sxs-lookup"><span data-stu-id="1d2a0-203">apikeys</span></span>

<span data-ttu-id="1d2a0-204">Depolar kümesiyle olarak API anahtar kimlik doğrulaması kullanan kaynakları tuşları [ `nuget setapikey` komutu](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="1d2a0-204">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="1d2a0-205">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-205">Key</span></span> | <span data-ttu-id="1d2a0-206">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-206">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-207">(kaynak URL)</span><span class="sxs-lookup"><span data-stu-id="1d2a0-207">(source URL)</span></span> | <span data-ttu-id="1d2a0-208">Şifrelenmiş API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-208">The encrypted API key.</span></span> |

<span data-ttu-id="1d2a0-209">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-209">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="1d2a0-210">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="1d2a0-210">disabledPackageSources</span></span>

<span data-ttu-id="1d2a0-211">Şu anda devre dışı bırakılmış kaynakları tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-211">Identified currently disabled sources.</span></span> <span data-ttu-id="1d2a0-212">Boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-212">May be empty.</span></span>

| <span data-ttu-id="1d2a0-213">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-213">Key</span></span> | <span data-ttu-id="1d2a0-214">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-214">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-215">(kaynak adı)</span><span class="sxs-lookup"><span data-stu-id="1d2a0-215">(name of source)</span></span> | <span data-ttu-id="1d2a0-216">Kaynak devre dışı olup olmadığını gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-216">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="1d2a0-217">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="1d2a0-217">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="1d2a0-218">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="1d2a0-218">activePackageSource</span></span>

<span data-ttu-id="1d2a0-219">*(yalnızca 2.x; içinde kullanım dışı 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="1d2a0-219">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="1d2a0-220">Şu anda etkin kaynağını tanımlayan veya toplama tüm kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-220">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="1d2a0-221">Anahtar</span><span class="sxs-lookup"><span data-stu-id="1d2a0-221">Key</span></span> | <span data-ttu-id="1d2a0-222">Değer</span><span class="sxs-lookup"><span data-stu-id="1d2a0-222">Value</span></span> |
| --- | --- |
| <span data-ttu-id="1d2a0-223">(kaynak adı) veya`All`</span><span class="sxs-lookup"><span data-stu-id="1d2a0-223">(name of source) or `All`</span></span> | <span data-ttu-id="1d2a0-224">Anahtar bir kaynak adı ise, kaynak yolu veya URL'si değerdir.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-224">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="1d2a0-225">Varsa `All`, değer olmalıdır `(Aggregate source)` Aksi durumda devre dışı tüm paket kaynaklarını birleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-225">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="1d2a0-226">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-226">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="1d2a0-227">Ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1d2a0-227">Using environment variables</span></span>

<span data-ttu-id="1d2a0-228">Ortam değişkenleri kullanabilirsiniz `NuGet.Config` değerleri (ayarları uygulamak için NuGet 3.4 +) çalışma süresi.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-228">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="1d2a0-229">Örneğin, varsa `HOME` Windows ortam değişkeni ayarlanır `c:\users\username`, ardından değeri `%HOME%\NuGetRepository` dosya yapılandırmada çözümler `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-229">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="1d2a0-230">Benzer şekilde, varsa `HOME` Mac/Linux'ta kümesine `/home/myStuff`, ardından `$HOME/NuGetRepository` dosya yapılandırmada çözümler `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-230">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="1d2a0-231">Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından hazır değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="1d2a0-231">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="1d2a0-232">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="1d2a0-232">Example config file</span></span>

<span data-ttu-id="1d2a0-233">Aşağıda `NuGet.Config` çeşitli ayarlar gösterilmektedir dosyası:</span><span class="sxs-lookup"><span data-stu-id="1d2a0-233">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
