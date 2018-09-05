---
title: NuGet 2.0 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.0 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547581"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="5a3f6-103">NuGet 2.0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="5a3f6-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="5a3f6-104">[1.8 NuGet sürüm notları](../release-notes/nuget-1.8.md) | [2.1 NuGet sürüm notları](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="5a3f6-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="5a3f6-105">NuGet 2.0 19 Haziran 2012 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="5a3f6-106">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="5a3f6-106">Known Installation Issue</span></span>
<span data-ttu-id="5a3f6-107">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="5a3f6-108">Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="5a3f6-109">Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi edinmek veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="5a3f6-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="5a3f6-110">Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="5a3f6-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="5a3f6-111">Paket geri yükleme onayı artık etkindir</span><span class="sxs-lookup"><span data-stu-id="5a3f6-111">Package restore consent is now active</span></span>

<span data-ttu-id="5a3f6-112">Bu konuda açıklandığı gibi [paket geri yükleme onay sonrası](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, çevrimiçi ve paketleri indirmek paket geri yükleme etkinleştirmek için onay verilmesi artık gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="5a3f6-113">Paket Yöneticisi'ni yapılandırma iletişim kutusu veya EnableNuGetPackageRestore ortam değişkeni aracılığıyla onay sağladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="5a3f6-114">Grup bağımlılıklarını hedef çerçeve tarafından</span><span class="sxs-lookup"><span data-stu-id="5a3f6-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="5a3f6-115">Sürüm 2.0 ile başlayarak, paket bağımlılıkları değişebilir projenin hedef çerçevesi profilini temel alan.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="5a3f6-116">Bu güncelleştirilmiş kullanılarak gerçekleştirilir `.nuspec` şema.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="5a3f6-117">`<dependencies>` Öğesi artık bir dizi içeren `<group>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="5a3f6-118">Sıfır veya daha fazlasını içeren her grubu `<dependency>` öğeleri ve `targetFramework` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="5a3f6-119">Hedef Framework'ü hedef proje framework profili ile uyumlu ise, bir grup içindeki tüm bağımlılıkları birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="5a3f6-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5a3f6-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="5a3f6-121">Bir grup içerebilir Not **sıfır** bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="5a3f6-122">Paket Silverlight 3.0 hedefleyen bir projeye veya üstünü, varsa, yukarıdaki örnekte, bağımlılık yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="5a3f6-123">Paket, .NET 4.0 hedefleyen bir projeye veya üstünü ise, jQuery ve WebActivator, iki bağımlılıklar yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="5a3f6-124">Bu 2 çerçeveleri veya diğer herhangi bir çerçeveyi eski bir sürümünü hedefleyen bir projeye paketini yüklediyseniz, RouteMagic 1.1.0 yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="5a3f6-125">Grupları arasında hiçbir devralma yoktur.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-125">There is no inheritance between groups.</span></span> <span data-ttu-id="5a3f6-126">Bir projenin hedef çatısının eşleşiyorsa `targetFramework` öznitelik grubunun, yalnızca o grup içindeki bağımlılıklar yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="5a3f6-127">Bir paketi Paket bağımlılıklarını iki biçimlerden birini belirtebilirsiniz: düz listesini eski biçimi `<dependency>` öğeleri veya gruplar.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="5a3f6-128">Varsa `<group>` biçimi kullanılır, paket 2.0 sürümünden öncekileri NuGet sürümlerine yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="5a3f6-129">İki biçim karıştırılmasına izin olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="5a3f6-130">Örneğin, aşağıdaki kod parçacığını olduğu **geçersiz** ve NuGet tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="5a3f6-131">İçerik dosyaları ve PowerShell betikleri tarafından hedef Framework'ü gruplandırma</span><span class="sxs-lookup"><span data-stu-id="5a3f6-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="5a3f6-132">Derleme başvuruları ek olarak, içerik dosyaları ve PowerShell betikleri de hedef Framework'ü gruplandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="5a3f6-133">Aynı klasör yapısında bulunan `lib` klasörü hedef Framework'ü belirtmek için artık uygulanabilir aynı şekilde `content` ve `tools` klasörleri.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="5a3f6-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5a3f6-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="5a3f6-135">**Not**: çünkü `init.ps1` çözüm düzeyinde yürütülür ve olduğu bağımlı olmayan her bir proje, bunu doğrudan altında yerleştirilmelidir `tools` klasör.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="5a3f6-136">Çerçeveye özgü bir klasörde yerleştirdiyseniz göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="5a3f6-137">Ayrıca, bir çerçeve klasörü olabilir NuGet 2.0 içinde yeni bir özellik olan *boş*, bu durumda, NuGet değil derleme başvurularını ekler, içerik dosyalarını eklemek veya belirli framework sürümü için PowerShell betikleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="5a3f6-138">Klasör yukarıdaki örnekte `content\net40` boştur.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="5a3f6-139">Geliştirilmiş sekme tamamlama performans</span><span class="sxs-lookup"><span data-stu-id="5a3f6-139">Improved tab completion performance</span></span>
<span data-ttu-id="5a3f6-140">NuGet Paket Yöneticisi konsolu için sekmesinde Tamamlama özelliği, performansı önemli ölçüde artırmak için güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="5a3f6-141">Öneri açılan görünene kadar SEKME tuşuna basıldığında saatten daha az gecikme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5a3f6-142">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="5a3f6-142">Bug Fixes</span></span>
<span data-ttu-id="5a3f6-143">NuGet 2.0 paket geri yükleme onayı ve performans ile ilgili bir Vurgu ile birçok hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5a3f6-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="5a3f6-144">Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5a3f6-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
