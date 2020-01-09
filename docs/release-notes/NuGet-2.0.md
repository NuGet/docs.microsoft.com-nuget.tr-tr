---
title: NuGet 2,0 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,0 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383073"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="ecec5-103">NuGet 2,0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ecec5-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="ecec5-104">[Nuget 1,8 sürüm notları](../release-notes/nuget-1.8.md) | [NuGet 2,1 sürüm notları](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="ecec5-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="ecec5-105">NuGet 2,0, 19 Haziran 2012 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ecec5-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="ecec5-106">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="ecec5-106">Known Installation Issue</span></span>
<span data-ttu-id="ecec5-107">VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecec5-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="ecec5-108">Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ecec5-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="ecec5-109">Daha fazla bilgi için bkz. <https://support.microsoft.com/kb/2581019> veya [doğrudan vs düzeltmesine git](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="ecec5-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="ecec5-110">Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="ecec5-111">Paket geri yükleme onayı artık etkin</span><span class="sxs-lookup"><span data-stu-id="ecec5-111">Package restore consent is now active</span></span>

<span data-ttu-id="ecec5-112">[Paket geri yükleme onayı](http://blog.nuget.org/20120518/package-restore-and-consent.html)' nda bu gönderi bölümünde açıklandığı gibi, NuGet 2,0 artık paket geri yükleme 'nin çevrimiçi hale geçmesine ve paketleri indirmesine olanak tanımak için izin verilmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="ecec5-113">Lütfen Paket Yöneticisi yapılandırma iletişim kutusu veya Enablenugetpackageresant ortam değişkeni aracılığıyla izin sağladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ecec5-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="ecec5-114">Hedef çerçevelere göre bağımlılıkları Gruplandır</span><span class="sxs-lookup"><span data-stu-id="ecec5-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="ecec5-115">Sürüm 2,0 ' den başlayarak, paket bağımlılıkları hedef projenin çerçeve profiline göre farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="ecec5-116">Bu, güncelleştirilmiş bir `.nuspec` şeması kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="ecec5-117">`<dependencies>` öğesi artık, bir dizi `<group>` öğesi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="ecec5-118">Her grup sıfır veya daha fazla `<dependency>` öğesi ve bir `targetFramework` özniteliği içerir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="ecec5-119">Hedef çerçeve hedef proje çerçevesi profiliyle uyumluysa, bir grup içindeki tüm bağımlılıklar birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="ecec5-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ecec5-120">For example:</span></span>

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

<span data-ttu-id="ecec5-121">Bir grubun **sıfır** bağımlılıklar içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecec5-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="ecec5-122">Yukarıdaki örnekte, paket Silverlight 3,0 veya sonraki bir sürümü hedefleyen bir projeye yüklenirse, hiçbir bağımlılık yüklenmez.</span><span class="sxs-lookup"><span data-stu-id="ecec5-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="ecec5-123">Paket, .NET 4,0 veya sonraki bir sürümü hedefleyen bir projeye yüklendiyse, iki bağımlılık, jQuery ve WebActivator yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="ecec5-124">Paket, bu 2 çerçevenin erken bir sürümünü veya başka bir çerçeveyi hedefleyen bir projeye yüklenirse, bir Kab1.1.0 yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="ecec5-125">Gruplar arasında devralma yoktur.</span><span class="sxs-lookup"><span data-stu-id="ecec5-125">There is no inheritance between groups.</span></span> <span data-ttu-id="ecec5-126">Projenin hedef çerçevesi bir grubun `targetFramework` özniteliğiyle eşleşiyorsa, yalnızca o gruptaki bağımlılıklar yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="ecec5-127">Bir paket iki biçimden birinde paket bağımlılıklarını belirtebilir: `<dependency>` öğelerinin veya grupların düz listesinin eski biçimi.</span><span class="sxs-lookup"><span data-stu-id="ecec5-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="ecec5-128">`<group>` biçimi kullanılırsa, paket 2,0 öncesi NuGet sürümüne yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="ecec5-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="ecec5-129">İki biçimin karıştırılmasına izin verilmeyeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecec5-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="ecec5-130">Örneğin, aşağıdaki kod parçacığı **geçersiz** olur ve NuGet tarafından reddedilir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="ecec5-131">Hedef çerçeveye göre içerik dosyalarını ve PowerShell betiklerini gruplandırma</span><span class="sxs-lookup"><span data-stu-id="ecec5-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="ecec5-132">Derleme başvurularına ek olarak, içerik dosyaları ve PowerShell betikleri hedef çerçeveye göre de gruplandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="ecec5-133">Hedef Framework belirtmek için `lib` klasöründe bulunan aynı klasör yapısı artık `content` ve `tools` klasörlerine aynı şekilde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="ecec5-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ecec5-134">For example:</span></span>

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

<span data-ttu-id="ecec5-135">**Not**: `init.ps1` çözüm düzeyinde yürütüldüğü ve tek bir projeye bağımlı olmadığından, doğrudan `tools` klasörünün altına yerleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="ecec5-136">Çerçeveye özgü bir klasör içine yerleştirilirse, yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="ecec5-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="ecec5-137">Ayrıca, NuGet 2,0 ' deki yeni bir özellik çerçeve klasörünün *boş*olması, bu durumda NuGet derleme başvuruları eklememe, içerik dosyaları eklemesi veya belirli Framework sürümü için PowerShell betikleri çalıştırmayacak.</span><span class="sxs-lookup"><span data-stu-id="ecec5-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="ecec5-138">Yukarıdaki örnekte, `content\net40` klasör boştur.</span><span class="sxs-lookup"><span data-stu-id="ecec5-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="ecec5-139">Gelişmiş sekme tamamlama performansı</span><span class="sxs-lookup"><span data-stu-id="ecec5-139">Improved tab completion performance</span></span>
<span data-ttu-id="ecec5-140">NuGet Paket Yöneticisi konsolundaki sekme tamamlama özelliği performansı önemli ölçüde artırmak için güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="ecec5-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="ecec5-141">Öneri açılan menüsü görünene kadar SEKME tuşuna basıldığında, bu süreden çok daha az gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="ecec5-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ecec5-142">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="ecec5-142">Bug Fixes</span></span>
<span data-ttu-id="ecec5-143">NuGet 2,0, paket geri yükleme onayı ve performansı üzerine bir vurgu içeren çok sayıda hata düzeltmesi içerir.</span><span class="sxs-lookup"><span data-stu-id="ecec5-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="ecec5-144">NuGet 2,0 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="ecec5-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
