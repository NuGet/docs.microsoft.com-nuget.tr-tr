---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975852"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="8d80e-101">NuGet 5.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="8d80e-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="8d80e-102">NuGet dağıtım araçları:</span><span class="sxs-lookup"><span data-stu-id="8d80e-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="8d80e-103">NuGet sürüm</span><span class="sxs-lookup"><span data-stu-id="8d80e-103">NuGet version</span></span> | <span data-ttu-id="8d80e-104">Visual Studio sürümü içinde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="8d80e-104">Available in Visual Studio version</span></span>| <span data-ttu-id="8d80e-105">.NET SDK'sı sürümünü kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="8d80e-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="8d80e-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="8d80e-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="8d80e-107">Visual Studio 2019 16.1 sürümü</span><span class="sxs-lookup"><span data-stu-id="8d80e-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="8d80e-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="8d80e-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="8d80e-109"><sup>1</sup>.NET Core iş yüküyle Visual Studio 2019 ile yüklü</span><span class="sxs-lookup"><span data-stu-id="8d80e-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="8d80e-110"><sup>2</sup>.NET Core iş yüküyle Visual Studio 2019 ile isteğe bağlı bir yükleme olarak kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="8d80e-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="8d80e-111">Özet: 5.1 yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="8d80e-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="8d80e-112">Daha iyi iş akışlarıyla tümleştirme CI/CD - izin vermek için zaten bir paket anında iletme atlayın için destek [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="8d80e-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="8d80e-113">Visual Studio artık uygun bir bağlantı sağlar paketin nuget.org galeri sayfası - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="8d80e-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="8d80e-114">Yeni .NET Core 3.0 varlıklarını gibi destekleyen [Targeting Pack](https://github.com/dotnet/cli/issues/10006) ve [çalışma zamanı paketleri](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="8d80e-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="8d80e-115">NuGet paketi ve geri yükleme desteği ve çalışma zamanı paket başvuruları - etkinleştirmek FrameworkReferences için destek [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="8d80e-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="8d80e-116">Destek "yalnızca indirin" PackageDownload - paket senaryosuyla [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="8d80e-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="8d80e-117">Exlcude çalışma zamanı ve arama sonuçları & geri yükleme paketlerinden hedefleyen grafiğini kullanarak PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="8d80e-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8d80e-118">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="8d80e-118">Issues fixed in this release</span></span>

<span data-ttu-id="8d80e-119">**Hataları**</span><span class="sxs-lookup"><span data-stu-id="8d80e-119">**Bugs**</span></span>

* <span data-ttu-id="8d80e-120">Eklentiler: özel durum ayrıntıları kayıp eklentisi oluşturma sırasında - [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="8d80e-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="8d80e-121">Alt sınır kaynaklardan biri mevcutsa PackageReference aralığı özel alt sınırı ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="8d80e-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="8d80e-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="8d80e-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="8d80e-123">IsPackableFalseError iletisi - geliştirmek [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="8d80e-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="8d80e-124">Paketler kilidi dosyası - proje graf değiştiğinde yeniden oluşturma kilit - [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="8d80e-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="8d80e-125">Proje sistemi hatası: Nuget paketlerini otomatik alma kaldırıldı - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="8d80e-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="8d80e-126">FrameworkReference döndürmek için bir hedef ekleyin CollectPackageDownloads ve CollectPackageReferences - benzer [#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="8d80e-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="8d80e-127">HTTP önbellek:  Tutulan bir biçimde - RepositoryResources kaynak önbelleğe alınmamış [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="8d80e-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="8d80e-128">Günlüğe kaydetme: özel durum çağrı yığınını ayrıntılı ayrıntı ile - bildirilmez [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="8d80e-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="8d80e-129">Tüm NuGet belgeleri - HTTPS kullanacak şekilde URL'leri değiştirmeyi [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="8d80e-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="8d80e-130">Uyarı iletisi NU3024 - geliştirmek [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="8d80e-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="8d80e-131">ne zaman güncelleştirilmiyor kilit dosyası kaldırıldı - packagereference [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="8d80e-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="8d80e-132">Hata örneği işleme nuspec - licenseurl ve lisans öğesindeki doğrularken geliştirmek [#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="8d80e-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="8d80e-133">PM UI - sağ tıklayın sekmesini üstbilgi ve sonuçları hata - tıklatarak "dosya konumunu Aç" [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="8d80e-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="8d80e-134">Eklentiler: oturum eklentisi işlem çıktığında - [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="8d80e-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="8d80e-135">Eklentiler: yüksek çakışma oranı günlük datetime değerleri - [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="8d80e-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="8d80e-136">Manifest.ReadFrom başarısız LicenseExpression ile-herhangi bir nuspec üzerinde [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="8d80e-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="8d80e-137">RestoreLockedMode: Bir projeye özel AssemblyName ile-ProjectReference başvurduğunda beklenmeyen NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="8d80e-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="8d80e-138">Bir özel durumla - eklentisi başlatma başarısız olduğunda daha iyi hata iletisi [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="8d80e-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="8d80e-139">NoOp geri yükleme yaparken önlemek \*. obj dizinindeki - dgspec.json yazma [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="8d80e-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="8d80e-140">GeneratePathProperty büyük/küçük harf uyuşmazlığı - özelliği oluşturmak için true başarısız = [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="8d80e-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="8d80e-141">Ayarları: VS - paket kaynağı yolu geçersiz karakter çökebilir [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="8d80e-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="8d80e-142">Kilit dosya silinirse, geri yükleme - NoOp üzerinde kilit dosyası oluşturmaz [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="8d80e-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="8d80e-143">Lisans URL'si ve lisans nedenleri okuma hatası - meta verilerle [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="8d80e-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="8d80e-144">İşlenmeyen özel durumları V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="8d80e-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="8d80e-145">nuget.exe - geçersiz bağımsız değişkenler için çıkış kodu sıfır döndürür [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="8d80e-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="8d80e-146">Hata ve uyarı docs imzalama ilgili senaryoları - yansıtacak şekilde güncelleştirmek [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="8d80e-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="8d80e-147">Varlıklar dosya taşıma projeleri daha bir kolayca - etkinleştirmek için göreli yolların kullanmalıdır [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="8d80e-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="8d80e-148">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="8d80e-148">**DCRs**</span></span>

* <span data-ttu-id="8d80e-149">Eklentiler: Tanılama günlüğüne kaydetme - etkinleştirme [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="8d80e-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="8d80e-150">NetStandard 2.1 - yapma Tizen 6 eşlemesine [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="8d80e-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="8d80e-151">**[Bu sürümde - 5.1 RTM düzeltilen tüm sorunlara listesi](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="8d80e-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
