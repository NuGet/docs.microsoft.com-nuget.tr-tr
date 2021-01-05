---
title: NuGet 5,1 RTM sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,1 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699859"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="3fc4d-103">NuGet 5,1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="3fc4d-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="3fc4d-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="3fc4d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3fc4d-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="3fc4d-105">NuGet version</span></span> | <span data-ttu-id="3fc4d-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="3fc4d-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3fc4d-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="3fc4d-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3fc4d-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="3fc4d-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3fc4d-109">Visual Studio 2019 sürüm 16,1</span><span class="sxs-lookup"><span data-stu-id="3fc4d-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3fc4d-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="3fc4d-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="3fc4d-111"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="3fc4d-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="3fc4d-112"><sup>2</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile isteğe bağlı bir install olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="3fc4d-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="3fc4d-113">Özet: 5,1 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="3fc4d-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="3fc4d-114">CI/CD iş akışlarıyla daha iyi tümleştirme sağlamak için zaten mevcutsa bir paket gönderimi atlama desteği- [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="3fc4d-115">Visual Studio artık paketin nuget.org Galeri sayfasına uygun bir bağlantı sağlamaktadır [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="3fc4d-116">[Hedefleme paketleri](https://github.com/dotnet/cli/issues/10006) ve [çalışma zamanı paketleri](https://github.com/dotnet/cli/issues/10007) gibi yeni .NET Core 3,0 varlıkları için destek</span><span class="sxs-lookup"><span data-stu-id="3fc4d-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="3fc4d-117">Hedef ve çalışma zamanı paket başvurularını etkinleştirmek üzere FrameworkReferences için NuGet paketi ve geri yükleme desteği- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="3fc4d-118">PackageDownload- [#7339](https://github.com/NuGet/Home/issues/7339) ile "yalnızca indir" paket senaryosunu destekleme</span><span class="sxs-lookup"><span data-stu-id="3fc4d-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="3fc4d-119">Çalışma zamanı ve hedefleme paketlerini, PackageType- [#7337](https://github.com/NuGet/Home/issues/7337) kullanarak & geri yükleme graflarından çıkar</span><span class="sxs-lookup"><span data-stu-id="3fc4d-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3fc4d-120">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3fc4d-120">Issues fixed in this release</span></span>

<span data-ttu-id="3fc4d-121">**Hata**</span><span class="sxs-lookup"><span data-stu-id="3fc4d-121">**Bugs**</span></span>

* <span data-ttu-id="3fc4d-122">Eklentiler: eklenti oluşturma sırasında özel durum ayrıntıları kayboldu- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="3fc4d-123">, Kaynaklardan birinde alt sınır varsa, özel alt sınırı olan PackageReference aralığı çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="3fc4d-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="3fc4d-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="3fc4d-125">Ispackabsolalseerror iletisini geliştirme- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="3fc4d-126">Paketler kilit dosyası-proje grafiği değiştiğinde kilit dosyasını yeniden oluştur- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="3fc4d-127">ProjectSystem hatası: NuGet paketleri otomatik olarak kaldırılıyor- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="3fc4d-128">CollectPackageDownloads ve Collectpackagerefersin- [#8005](https://github.com/NuGet/Home/issues/8005) benzer bir frameworkreference döndürmek için bir hedef ekleyin</span><span class="sxs-lookup"><span data-stu-id="3fc4d-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="3fc4d-129">HTTP önbelleği: Depokaynak kaynağı, sürümlü bir şekilde önbelleğe alınmaz- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="3fc4d-130">Günlüğe kaydetme: özel durum callyığınları ayrıntılı ayrıntı düzeyi ile bildirilmedi [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="3fc4d-131">Tüm NuGet belgeleri URL 'Lerini HTTPS- [#7950](https://github.com/NuGet/Home/issues/7950) kullanacak şekilde değiştir</span><span class="sxs-lookup"><span data-stu-id="3fc4d-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="3fc4d-132">NU3024 uyarı iletisini geliştirme- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="3fc4d-133">packagereference kaldırıldığında kilit dosyası güncelleştirilmiyor- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="3fc4d-134">Nuspec- [#7915](https://github.com/NuGet/Home/issues/7915) içinde licenseurl ve lisans öğesi doğrulanırken hata durum işlemeyi geliştir</span><span class="sxs-lookup"><span data-stu-id="3fc4d-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="3fc4d-135">PM Kullanıcı arabirimi-sekme başlığına sağ tıklayıp "dosya konumunu aç" seçeneğine tıkladığınızda hata [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="3fc4d-136">Eklentiler: eklenti işlemi çıktığında günlüğe kaydet- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="3fc4d-137">Eklentiler: günlük tarih değerlerini günlüğe kaydetme sırasında yüksek çakışma oranı- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="3fc4d-138">LicenseExpression- [#7894](https://github.com/NuGet/Home/issues/7894) ile herhangi bir nuspec üzerinde manifest. ReadFrom başarısız</span><span class="sxs-lookup"><span data-stu-id="3fc4d-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="3fc4d-139">RestoreLockedMode: ProjectReference özel AssemblyName içeren bir projeye başvurduğunda, beklenmeyen NU1004- [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="3fc4d-140">Eklenti başlatması bir özel durumla başarısız olduğunda daha iyi hata iletisi [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="3fc4d-141">Bir NoOp geri yükleme işlemi yaparken, obj dizininde yazma sırasında \* .dgspec.jsönleyin- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="3fc4d-142">GeneratePathProperty = true, büyük/küçük harf uyuşmazlığı üzerinde özellik üretemiyor- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="3fc4d-143">Ayarlar: paket kaynak yolunda geçersiz karakter kilitlenebilir VS- [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="3fc4d-144">Kilit dosyası silinirse, geri yükleme işlemi NoOp 'de kilit dosyası oluşturmaz [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="3fc4d-145">Lisans URL 'SI ve lisans, meta verilerle okuma hatasına neden olur- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="3fc4d-146">V2FeedParser- [#7523](https://github.com/NuGet/Home/issues/7523) işlenmemiş özel durumlar</span><span class="sxs-lookup"><span data-stu-id="3fc4d-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="3fc4d-147">nuget.exe geçersiz bağımsız değişkenler için sıfır çıkış kodu döndürüyor- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="3fc4d-148">İmzalama ilgili senaryolarını yansıtmak için hataları ve uyarı belgelerini güncelleştirin- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="3fc4d-149">Varlıklar dosyası, projeleri taşımayı daha kolay bir şekilde etkinleştirmek için göreli yollar kullanmalıdır [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="3fc4d-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="3fc4d-150">**DCRs**</span></span>

* <span data-ttu-id="3fc4d-151">Eklentiler: Tanılama günlüğünü etkinleştirme- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="3fc4d-152">Tizen 6 eşlemesini NetStandard 2,1 ile yapın [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="3fc4d-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="3fc4d-153">**[Bu yayında düzeltilen tüm sorunların listesi-5,1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="3fc4d-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
