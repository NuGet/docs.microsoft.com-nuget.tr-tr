---
title: Yüklü paketlerin sorunlarını giderme
description: Ayrı paketler için kullanılan paket kaynağını bulma
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387573"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="cc848-103">Yüklü paketlerin sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="cc848-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="cc848-104">Bazen belirli bir paketin hangi kaynağa yüklendiğini doğrulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc848-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="cc848-105">Burada, bazı şekillerde denetim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc848-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="cc848-106">Bazı paket kaynakları, yukarı akış kaynakları olarak bilinen bir kavramı destekler.</span><span class="sxs-lookup"><span data-stu-id="cc848-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="cc848-107">Örneğin, [yukarı akış kaynakları Azure Artifacts](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="cc848-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="cc848-108">NuGet istemcileri bir paketin yukarı akış kaynağından geldiğini bilmez.</span><span class="sxs-lookup"><span data-stu-id="cc848-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="cc848-109">Bu nedenle, paket kaynağının herhangi bir günlüğü, yukarı akış kaynağını değil, yapılandırılmış kaynağı listeler.</span><span class="sxs-lookup"><span data-stu-id="cc848-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="cc848-110">`.nupkg.metadata` Genel paketler klasöründeki dosya</span><span class="sxs-lookup"><span data-stu-id="cc848-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="cc848-111">Bir paket *genel paketler* klasörüne ayıklandığında bir dosya `.nupkg.metadata` yazılır.</span><span class="sxs-lookup"><span data-stu-id="cc848-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="cc848-112">NuGet 5.9.0 'den başlayarak, NuGet paket kaynağını ekler.</span><span class="sxs-lookup"><span data-stu-id="cc848-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="cc848-113">NuGet sürümlerini Visual Studio veya .NET SDK sürümleriyle eşlemek için aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="cc848-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="cc848-114">Örnek:</span><span class="sxs-lookup"><span data-stu-id="cc848-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="cc848-115">*Genel paketler* klasörünüzün, NuGet 5.9.0 içeren araçların daha yeni bir sürümüne yükseltmeden önce ayıklandığı paketler varsa, `.nupkg.metadata` Dosya sürüm 1 olur ve paket kaynağını içermez.</span><span class="sxs-lookup"><span data-stu-id="cc848-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="cc848-116">Tüm paketlerin paket kaynağını içermesini sağlamak için [ *genel paketler* klasörünüzü temizleyebilirsiniz](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .</span><span class="sxs-lookup"><span data-stu-id="cc848-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="cc848-117">NuGet `.nupkg.metadata` dosyayı yalnızca *genel paketler* klasörüne yazar.</span><span class="sxs-lookup"><span data-stu-id="cc848-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="cc848-118">Kullanan projeler bir `packages.config` dosya oluşturmayan çözüm paketleri klasörünü kullanır `.nupkg.metadata` .</span><span class="sxs-lookup"><span data-stu-id="cc848-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="cc848-119">Paket günlük iletisi yüklendi</span><span class="sxs-lookup"><span data-stu-id="cc848-119">Installed package log message</span></span>

<span data-ttu-id="cc848-120">NuGet 5.9.0 'den başlayarak NuGet, geri yükleme iletisindeki paket kaynağını bir paketin yüklendiğini bildiren çıkış olarak verir.</span><span class="sxs-lookup"><span data-stu-id="cc848-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="cc848-121">Örnek:</span><span class="sxs-lookup"><span data-stu-id="cc848-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="cc848-122">Bu ileti, normal/bilgilendirici Ayrıntı ayrıntısı sırasında çıktıdır.</span><span class="sxs-lookup"><span data-stu-id="cc848-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="cc848-123">Visual Studio ve `dotnet` CLI varsayılan olarak en az ayrıntı düzeyi, bu nedenle bu ileti varsayılan olarak görünür olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="cc848-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="cc848-124">`msbuild`Ve `nuget` CLI araçları varsayılan olarak normal ayrıntı düzeyi olarak görünür, bu nedenle bu ileti varsayılan olarak görünür olur.</span><span class="sxs-lookup"><span data-stu-id="cc848-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="cc848-125">HTTP günlüğü iletisi</span><span class="sxs-lookup"><span data-stu-id="cc848-125">HTTP log message</span></span>

<span data-ttu-id="cc848-126">Bir paket yerel olarak mevcut olmadığında, *genel paketler* klasöründe, bir geri dönüş klasöründe veya yerel bir dosya kaynağında, NUGET bunu http üzerinden yapılandırılmış herhangi bir paket kaynağından indirir.</span><span class="sxs-lookup"><span data-stu-id="cc848-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="cc848-127">HTTP istekleri ve yanıtları normal ayrıntı düzeyinde günlüğe kaydedilir ve paket sürümüne göre yalnızca tek bir istek ve yanıt görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc848-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="cc848-128">Örnek:</span><span class="sxs-lookup"><span data-stu-id="cc848-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="cc848-129">Dosyalar yakın zamanda indirildiyse NuGet 'in *http önbelleğinden* alınmış olabilir</span><span class="sxs-lookup"><span data-stu-id="cc848-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="cc848-130">URL biçimi farklı NuGet HTTP sunucu uygulamaları için farklı olabilir ve NuGet v2 ya da v3 HTTP protokolünü mi uygulamadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cc848-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="cc848-131">`nuget.config`Tanımlanmış birden çok http kaynağı varsa her `index.json` bir paket dosyası için her bir kaynak için birden çok istek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cc848-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="cc848-132">Ancak `nupkg` paketin her sürümü için yalnızca tek bir indirme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cc848-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="cc848-133">Paket imza günlüğü iletisi</span><span class="sxs-lookup"><span data-stu-id="cc848-133">Package signature log message</span></span>

<span data-ttu-id="cc848-134">İndirilen paket imzalanmışsa, NuGet imzayı doğrular ve ayrıntılı ayrıntı olarak şu iletiyi günlüğe kaydeder:</span><span class="sxs-lookup"><span data-stu-id="cc848-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="cc848-135">Bu ileti, paketin bir HTTP paket kaynağından indirilip indirilmediğini veya yerel bir paket kaynağından kopyalanıp kopyalanmadığını rapor eder.</span><span class="sxs-lookup"><span data-stu-id="cc848-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="cc848-136">Paket, *genel paketler* klasöründe veya bir geri dönüş klasöründe zaten kullanılabiliyorsa çıkış olmaz.</span><span class="sxs-lookup"><span data-stu-id="cc848-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="cc848-137">[VERISIGN CA 'nın güveninin kaldırılması](https://github.com/dotnet/announcements/issues/180) nedeniyle belirli platformlarda, belirli bir NuGet ve .NET SDK sürümünde imzalı paket doğrulaması devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="cc848-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="cc848-138">Bu nedenle, `PackageSignatureVerificationLog` geri yükleme çalıştırdığınız platforma ve hangi .NET veya NuGet sürümüne bağlı olarak, aynı paketlerde Günlükler olabilir veya bu Günlükler eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc848-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="cc848-139">NuGet sürüm Haritası</span><span class="sxs-lookup"><span data-stu-id="cc848-139">NuGet Version Map</span></span>

<span data-ttu-id="cc848-140">Aşağıdaki NuGet sürümlerinde, paket kaynağı günlük kaydıyla ilgili önemli değişiklikler vardır:</span><span class="sxs-lookup"><span data-stu-id="cc848-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="cc848-141">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="cc848-141">NuGet Version</span></span>|<span data-ttu-id="cc848-142">Visual Studio sürümü</span><span class="sxs-lookup"><span data-stu-id="cc848-142">Visual Studio Version</span></span>|<span data-ttu-id="cc848-143">.NET SDK sürümü</span><span class="sxs-lookup"><span data-stu-id="cc848-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="cc848-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="cc848-144">NuGet 5.9.0</span></span>|<span data-ttu-id="cc848-145">Visual Studio 2019 16.9.0</span><span class="sxs-lookup"><span data-stu-id="cc848-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="cc848-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="cc848-146">.NET 5 SDK 5.0.200</span></span>|
