---
title: NuGet 1,6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,6 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2878d3809b2be4fb71f4e7b1a1e08e405ead44b9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384143"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="14092-103">NuGet 1,6 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="14092-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="14092-104">[Nuget 1,5 sürüm notları](../release-notes/nuget-1.5.md) | [NuGet 1,7 sürüm notları](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="14092-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="14092-105">NuGet 1,6, 13 Aralık 2011 tarihinde yayınlandı.</span><span class="sxs-lookup"><span data-stu-id="14092-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="14092-106">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="14092-106">Known Installation Issue</span></span>
<span data-ttu-id="14092-107">VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14092-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="14092-108">Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="14092-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="14092-109">Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="14092-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="14092-110">Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="14092-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="14092-111">Özellikler</span><span class="sxs-lookup"><span data-stu-id="14092-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="14092-112">Anlamsal sürüm oluşturma ve ön sürüm paketleri desteği</span><span class="sxs-lookup"><span data-stu-id="14092-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="14092-113">NuGet 1,6 anlam sürümü oluşturma (SemVer) için destek sunar.</span><span class="sxs-lookup"><span data-stu-id="14092-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="14092-114">SemVer 'in nasıl kullanıldığı hakkında daha fazla bilgi için [sürüm oluşturma belgelerini](../create-packages/prerelease-packages.md)okuyun.</span><span class="sxs-lookup"><span data-stu-id="14092-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="14092-115">Paketleri Iade etmeden NuGet kullanma (paket geri yükleme)</span><span class="sxs-lookup"><span data-stu-id="14092-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="14092-116">NuGet 1,6 artık, NuGet paketlerinin kaynak denetimine eklendiği iş akışı için birinci sınıf desteğe sahiptir, bunun yerine derleme zamanında geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="14092-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="14092-117">Daha fazla ayrıntı için, [paketi kaynak denetimine kaydetmeden NuGet kullanma](../consume-packages/packages-and-source-control.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="14092-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="14092-118">NuGet paketlerini yükleyen öğe şablonları</span><span class="sxs-lookup"><span data-stu-id="14092-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="14092-119">Visual Studio proje şablonlarına önceden yüklenmiş NuGet paketini desteklemeye yönelik iş üzerinde oluşturma, NuGet 1,6, Visual Studio öğe şablonları için de destek ekler.</span><span class="sxs-lookup"><span data-stu-id="14092-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="14092-120">Öğe şablonlarında, bir şablon çağrıldığında yüklenen ilişkili NuGet paketleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="14092-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="14092-121">NuGet paketlerini yüklemek için bir proje/öğe şablonunu değiştirme hakkında daha fazla bilgi için, [Visual Studio şablonlarındaki paketler](../visual-studio-extensibility/visual-studio-templates.md) konusunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="14092-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="14092-122">Paket kaynaklarını devre dışı bırakma desteği</span><span class="sxs-lookup"><span data-stu-id="14092-122">Support for disabling package sources</span></span>
<span data-ttu-id="14092-123">Birden çok paket kaynağı yapılandırıldığında, NuGet bir paket yükleme sırasında paketler için her birine bakar.</span><span class="sxs-lookup"><span data-stu-id="14092-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="14092-124">Bir nedenden dolayı çalışan bir paket kaynağı, NuGet 'i ciddi ölçüde yavaşlatabilir.</span><span class="sxs-lookup"><span data-stu-id="14092-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="14092-125">NuGet 1,6 ' den önce, paket kaynağını kaldırabilir, ancak sonra geri eklemek istediğiniz zaman ayrıntılarını hatırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="14092-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="14092-126">NuGet 1,6, bir paket kaynağının devre dışı bırakılacağını kaldırmak, ancak geçici bir çözüm olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="14092-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Bir paketi devre dışı bırakma](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="14092-128">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="14092-128">Bug Fixes</span></span>
<span data-ttu-id="14092-129">NuGet 1,6, Toplam 106 iş öğesine sahipti.</span><span class="sxs-lookup"><span data-stu-id="14092-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="14092-130">Bunlar hata olarak sınıflandırılmıştı ve bu özelliklerin 10 ' dur. 95</span><span class="sxs-lookup"><span data-stu-id="14092-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="14092-131">NuGet 1,6 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="14092-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
