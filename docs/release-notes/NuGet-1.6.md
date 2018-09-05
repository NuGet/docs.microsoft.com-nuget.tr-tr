---
title: NuGet 1.6 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.6 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549018"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="51dbc-103">NuGet 1.6 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="51dbc-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="51dbc-104">[1.5 NuGet sürüm notları](../release-notes/nuget-1.5.md) | [1.7 NuGet sürüm notları](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="51dbc-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="51dbc-105">NuGet 1.6 13 Aralık 2011'de yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="51dbc-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="51dbc-106">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="51dbc-106">Known Installation Issue</span></span>
<span data-ttu-id="51dbc-107">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51dbc-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="51dbc-108">Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="51dbc-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="51dbc-109">Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="51dbc-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="51dbc-110">Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="51dbc-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="51dbc-111">Özellikler</span><span class="sxs-lookup"><span data-stu-id="51dbc-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="51dbc-112">Semantic Versioning ve yayın öncesi paketleri için destek</span><span class="sxs-lookup"><span data-stu-id="51dbc-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="51dbc-113">NuGet 1.6 Semantic Versioning (SemVer) için destek sunuyor.</span><span class="sxs-lookup"><span data-stu-id="51dbc-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="51dbc-114">SemVer kullanma hakkında ayrıntılı bilgi için okuma [sürüm belgeleri](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="51dbc-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="51dbc-115">NuGet paketleri (paket geri yükleme) denetlemeden kullanma</span><span class="sxs-lookup"><span data-stu-id="51dbc-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="51dbc-116">NuGet 1.6 artık hangi NuGet paketleri kaynak denetimine eklenmez ancak bunun yerine derleme zamanında eksikse geri yüklenir iş akışı için birinci sınıf desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="51dbc-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="51dbc-117">Daha fazla bilgi edinmek için [NuGet paketleri kaynak denetimine yürüten olmadan kullanarak](../consume-packages/packages-and-source-control.md) konu.</span><span class="sxs-lookup"><span data-stu-id="51dbc-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="51dbc-118">NuGet paketlerini yükleme öğesi şablonları</span><span class="sxs-lookup"><span data-stu-id="51dbc-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="51dbc-119">Önceden yüklenmiş NuGet paketini Visual Studio Proje şablonları desteklemek için iş oluşturma, NuGet 1.6 ayrıca Visual Studio öğe şablonları için destek ekler.</span><span class="sxs-lookup"><span data-stu-id="51dbc-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="51dbc-120">Öğe şablonları şablonda çağrıldığında, yüklü olan NuGet paketlerini ilişkili.</span><span class="sxs-lookup"><span data-stu-id="51dbc-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="51dbc-121">NuGet paketlerini yüklemek için bir proje/öğe şablon değiştirme hakkında daha fazla ayrıntı için okuma [Visual Studio şablonları paketlerinde](../visual-studio-extensibility/visual-studio-templates.md) konu.</span><span class="sxs-lookup"><span data-stu-id="51dbc-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="51dbc-122">Paket kaynaklarını devre dışı bırakma desteği</span><span class="sxs-lookup"><span data-stu-id="51dbc-122">Support for disabling package sources</span></span>
<span data-ttu-id="51dbc-123">Birden çok paket kaynaklarını yapılandırıldığında, NuGet paketleri için her biri bir paketi ve bağımlılıkları yükleme sırasında bakar.</span><span class="sxs-lookup"><span data-stu-id="51dbc-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="51dbc-124">Herhangi bir nedenle NuGet ciddi bir şekilde yavaş aşağı doğru için kapalı bir paket kaynağı.</span><span class="sxs-lookup"><span data-stu-id="51dbc-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="51dbc-125">NuGet 1.6 önce paket kaynağı kaldırabilirsiniz, ancak ayrıntıları eklemek istediğiniz zaman geri anımsamak zorunda sonra.</span><span class="sxs-lookup"><span data-stu-id="51dbc-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="51dbc-126">NuGet 1.6 devre dışı bırakır, ancak geçici olarak saklamak için bir paket kaynağı işaretini verir.</span><span class="sxs-lookup"><span data-stu-id="51dbc-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Bir paketi devre dışı bırakma](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="51dbc-128">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="51dbc-128">Bug Fixes</span></span>
<span data-ttu-id="51dbc-129">NuGet 1.6 106 toplam iş öğeleri sabit vardı.</span><span class="sxs-lookup"><span data-stu-id="51dbc-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="51dbc-130">Bu 95 hataları olarak sınıflandırılan ve 10 bu özellikleri silindi.</span><span class="sxs-lookup"><span data-stu-id="51dbc-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="51dbc-131">Tam bir listesi için iş öğeleri NuGet 1.6 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="51dbc-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
