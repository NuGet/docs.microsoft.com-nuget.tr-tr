---
title: "NuGet 2.0 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 51c7e94f-0084-4c62-bfba-7dfd81675361
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 2.0 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.0 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41eed1a7c6ad91d63813fb74986aa498765f3dea
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="a84dd-104">NuGet 2.0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="a84dd-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="a84dd-105">[NuGet 1.8 sürüm notları](../release-notes/nuget-1.8.md) | [NuGet 2.1 sürüm notları](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="a84dd-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="a84dd-106">NuGet 2.0 19 Haziran 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="a84dd-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a84dd-107">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="a84dd-107">Known Installation Issue</span></span>
<span data-ttu-id="a84dd-108">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a84dd-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a84dd-109">Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a84dd-110">Bkz: [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) daha fazla bilgi için veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="a84dd-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="a84dd-111">Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="a84dd-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="a84dd-112">Paket geri yükleme izni şimdi etkindir</span><span class="sxs-lookup"><span data-stu-id="a84dd-112">Package restore consent is now active</span></span>

<span data-ttu-id="a84dd-113">Bu konuda açıklandığı gibi [sonrası paket geri yükleme izni üzerinde](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, çevrimiçi ve paketleri indirmek paket geri yüklemesi etkinleştirmek için izin verilmesini şimdi gerektirecektir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="a84dd-114">Paket Yöneticisi yapılandırma iletişim kutusu veya EnableNuGetPackageRestore ortam değişkeni aracılığıyla izin verilen emin olun.</span><span class="sxs-lookup"><span data-stu-id="a84dd-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="a84dd-115">Bir hedef çerçeveyi Grup bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="a84dd-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="a84dd-116">2.0 sürümünden başlayarak, paket bağımlılıkları değişebilir hedef projeyi framework profilini temel alan.</span><span class="sxs-lookup"><span data-stu-id="a84dd-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="a84dd-117">Bu güncelleştirilmiş kullanılarak gerçekleştirilir `.nuspec` şema.</span><span class="sxs-lookup"><span data-stu-id="a84dd-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="a84dd-118">`<dependencies>` Öğesi artık bir dizi içeren `<group>` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="a84dd-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="a84dd-119">Sıfır veya daha fazla içeren her grubu `<dependency>` öğeleri ve bir `targetFramework` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="a84dd-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="a84dd-120">Hedef Framework'ü hedef proje framework profili ile uyumlu ise, bir grup içindeki tüm bağımlılıkları birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="a84dd-121">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a84dd-121">For example:</span></span>

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

<span data-ttu-id="a84dd-122">Bir grup içerebilir Not **sıfır** bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="a84dd-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="a84dd-123">Paket bir projeye Silverlight 3.0 hedefler veya üstünü, ise yukarıdaki örnekte, bağımlılık yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="a84dd-124">Paket, yüklü olan .NET 4.0 hedefleyen projesine veya sonrası ise, iki bağımlılıkları, jQuery ve WebActivator, yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="a84dd-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="a84dd-125">Paketin 2 Bu çerçeveleri ya da diğer framework eski bir sürümü hedefleyen bir projeye yüklüyse, RouteMagic 1.1.0 yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="a84dd-126">Grupları arasında hiçbir devralma yoktur.</span><span class="sxs-lookup"><span data-stu-id="a84dd-126">There is no inheritance between groups.</span></span> <span data-ttu-id="a84dd-127">Bir projenin hedef çerçevesi eşleşirse `targetFramework` öznitelik grubunun, yalnızca o grup dahilindeki bağımlılıklar yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="a84dd-128">Bir paketi Paket bağımlılıklarını iki biçim birini belirtebilirsiniz: düz listesini eski biçimi `<dependency>` öğeleri ya da gruplar.</span><span class="sxs-lookup"><span data-stu-id="a84dd-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="a84dd-129">Varsa `<group>` biçimi kullanıldığında, NuGet 2.0'den önceki sürümleri içine paket yüklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="a84dd-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="a84dd-130">İki biçim karıştırma verilmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a84dd-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="a84dd-131">Örneğin, aşağıdaki kod parçacığında **geçersiz** ve NuGet tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="a84dd-132">İçerik dosyaları ve PowerShell komut dosyaları hedef çerçevesi tarafından gruplandırma</span><span class="sxs-lookup"><span data-stu-id="a84dd-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="a84dd-133">Derleme başvurularını ek olarak, içerik dosyaları ve PowerShell komut dosyalarını da hedef çerçevesi tarafından gruplandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="a84dd-134">Aynı klasör yapısını bulunan `lib` hedef Framework'ü belirtmek için klasör şimdi uygulanabilir aynı şekilde `content` ve `tools` klasörler.</span><span class="sxs-lookup"><span data-stu-id="a84dd-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="a84dd-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a84dd-135">For example:</span></span>

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

<span data-ttu-id="a84dd-136">**Not**: çünkü `init.ps1` çözüm düzeyinde yürütülür ve olduğu her bir proje üzerinde bağlı değil, bunu doğrudan altında yerleştirilmelidir `tools` klasör.</span><span class="sxs-lookup"><span data-stu-id="a84dd-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="a84dd-137">İçinde çerçeveye özel bir klasöre girdiyseniz yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="a84dd-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="a84dd-138">Ayrıca, yeni bir NuGet 2.0 framework klasör olabilir özelliktir *boş*, bu durumda NuGet değil derleme başvurularını ekler, içerik dosyalarını eklemek veya belirli framework sürümü için PowerShell betikleri çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="a84dd-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="a84dd-139">Klasör yukarıdaki örnekte `content\net40` boş.</span><span class="sxs-lookup"><span data-stu-id="a84dd-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="a84dd-140">Gelişmiş sekmesi tamamlama performansı</span><span class="sxs-lookup"><span data-stu-id="a84dd-140">Improved tab completion performance</span></span>
<span data-ttu-id="a84dd-141">NuGet Paket Yöneticisi konsolunda sekme tamamlama özelliği, performansı önemli ölçüde artırmak için güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="a84dd-142">Öneri açılır listesinde görünene kadar SEKME tuşuna basılana zamandan daha az gecikme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a84dd-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a84dd-143">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="a84dd-143">Bug Fixes</span></span>
<span data-ttu-id="a84dd-144">NuGet 2.0 paket geri yükleme izni ve performans ile ilgili bir Vurgu ile birçok hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a84dd-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="a84dd-145">Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="a84dd-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
