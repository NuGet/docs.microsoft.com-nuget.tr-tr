---
title: NuGet 3,0 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,0 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776569"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="8a81c-103">NuGet 3,0 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="8a81c-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="8a81c-104">[NuGet 3,0 beta sürüm notları](../release-notes/nuget-3.0-beta.md)  |  [NuGet 3,0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="8a81c-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="8a81c-105">NuGet 3,0 RC, Visual Studio 2015 RC sürümü ile 29 Nisan 2015 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8a81c-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="8a81c-106">Bu sürümde, yeni çerçeveleri desteklemeye yönelik bazı önemli hata düzeltmeleri, performans geliştirmeleri ve güncelleştirmeler bulunur.</span><span class="sxs-lookup"><span data-stu-id="8a81c-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="8a81c-107">Yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8a81c-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="8a81c-108">Performansa devam eden odak</span><span class="sxs-lookup"><span data-stu-id="8a81c-108">Continued Focus on Performance</span></span>

<span data-ttu-id="8a81c-109">NuGet sorgularının kararlılığı ve performansı, odaklandığımız bir sıcak konu olarak devam eder.</span><span class="sxs-lookup"><span data-stu-id="8a81c-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="8a81c-110">Bu sürümle birlikte, NuGet Kullanıcı arabiriminde ve Web sitesinde çok hızlı arama işlemlerini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a81c-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="8a81c-111">Hizmeti ve hizmeti nasıl kullanacağınızı, bu işlemleri ayarlamaya devam edebilmemiz için izliyoruz.</span><span class="sxs-lookup"><span data-stu-id="8a81c-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="8a81c-112">Çözümlenen önemli sorunlar</span><span class="sxs-lookup"><span data-stu-id="8a81c-112">Significant Issues Resolved</span></span>

<span data-ttu-id="8a81c-113">NuGet istemcilerinin kararlı olması için, bu yayının bir parçası olarak birçok sorunu çöztik.</span><span class="sxs-lookup"><span data-stu-id="8a81c-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="8a81c-114">Aşağıda, çözümlenmiş bazı önemli sorunların kısa bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8a81c-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="8a81c-115">ASP.NET 5 için K çerçevesinin yeniden adlandırılması kapsamında, çerçeve takma adları DNX ve dnxcore [bağlantısını](https://github.com/NuGet/Home/issues/215) işleyecek şekilde güncelleştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="8a81c-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="8a81c-116">Visual Studio UI [bağlantısı](https://github.com/NuGet/Home/issues/232) 'ndaki bağlantılardan yardım belgeleri eklendi</span><span class="sxs-lookup"><span data-stu-id="8a81c-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="8a81c-117">`.nuspec`Virgülle ayrılmış çerçeve başvuruları [bağlantısı](https://github.com/NuGet/Home/issues/276) ile içinde karmaşık başvuruların daha iyi işlenmesi</span><span class="sxs-lookup"><span data-stu-id="8a81c-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="8a81c-118">Japonca kültürler için sabit destek [bağlantısı](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="8a81c-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="8a81c-119">ASP.NET 5 projelerinin Yeni v3 uç noktaları [bağlantısı](https://github.com/NuGet/Home/issues/219) kullanmasına izin vermek için istemci güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="8a81c-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="8a81c-120">Kaynak denetimi [bağlantısı](https://github.com/NuGet/Home/issues/56) ile paket klasörünü daha iyi işleyecek şekilde güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="8a81c-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="8a81c-121">Uydu paketleri için sabit destek [bağlantısı](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="8a81c-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="8a81c-122">Çerçeveye özgü içerik dosyaları [bağlantısı](https://github.com/NuGet/Home/issues/18) için düzeltilen destek</span><span class="sxs-lookup"><span data-stu-id="8a81c-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="8a81c-123">GitHub varlık fazla mesafe</span><span class="sxs-lookup"><span data-stu-id="8a81c-123">GitHub presence overhaul</span></span>

<span data-ttu-id="8a81c-124">[GitHub 'da kaynak kodu depolarımızda](http://github.com/nuget/home)bazı değişiklikler yaptık.</span><span class="sxs-lookup"><span data-stu-id="8a81c-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="8a81c-125">NuGet Visual Studio istemcisiyle ilgili herhangi bir sorununuz varsa, PowerShell komutları veya komut satırı yürütülebilir dosyası varsa, bu sorunları günlüğe kaydedebilir ve [GitHub giriş deposu sorunları listenizde](http://github.com/nuget/home/issues)ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a81c-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="8a81c-126">[GitHub NuGetGallery deponuzdaki](http://github.com/nuget/NuGetGallery/issues)galerinin sorunlarını izliyoruz.</span><span class="sxs-lookup"><span data-stu-id="8a81c-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="8a81c-127">Ayarlanmış durumda kal</span><span class="sxs-lookup"><span data-stu-id="8a81c-127">Stay Tuned</span></span>

<span data-ttu-id="8a81c-128">NuGet 3,0 için daha fazla ilerleme ve duyuru için lütfen [blogumuza](http://blog.nuget.org) göz önünde bulundurun!</span><span class="sxs-lookup"><span data-stu-id="8a81c-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>