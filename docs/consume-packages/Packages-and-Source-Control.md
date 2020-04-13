---
title: NuGet Paketleri ve Kaynak Kontrolü
description: Sürüm kontrol ve kaynak kontrol sistemleri içinde NuGet paketlerinin nasıl tedavi edilecek ve git ve TFVC ile paketleri nasıl atlatırsınız hakkında dikkat edilmesi gerekenler.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019987"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="affc1-103">Kaynak kontrol sistemlerinde NuGet paketlerini atlayarak</span><span class="sxs-lookup"><span data-stu-id="affc1-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="affc1-104">Geliştiriciler genellikle NuGet paketlerini kaynak denetim depolarından atlar ve bunun yerine bir projenin bağımlılıklarını oluşturmadan önce yeniden yüklemek için [paket geri yüklemesine](package-restore.md) güvenirler.</span><span class="sxs-lookup"><span data-stu-id="affc1-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="affc1-105">Paket geri yüklemeye güvenmenedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="affc1-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="affc1-106">Git gibi dağıtılmış sürüm kontrol sistemleri, depodaki her dosyanın her sürümünün tam kopyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="affc1-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="affc1-107">Sık sık güncelleştirilen ikili dosyalar önemli şişkinliğe yol açar ve depoyu klonlamak için gereken süreyi uzatır.</span><span class="sxs-lookup"><span data-stu-id="affc1-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="affc1-108">Paketler depoya dahil edildiğinde, geliştiriciler projede sabit kodlanmış yol adlarına yol açabilecek NuGet aracılığıyla paketlere başvurmak yerine doğrudan diskteki paket içeriğine referans eklemekle yükümlüdürler.</span><span class="sxs-lookup"><span data-stu-id="affc1-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="affc1-109">Hala kullanılmakta olan paket klasörlerini silmediğinizden emin olmanız gerektiğinden, çözümünüzü kullanılmayan paket klasörlerinden temizlemek zorlaşır.</span><span class="sxs-lookup"><span data-stu-id="affc1-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="affc1-110">Paketleri atlayarak, kodunuz la bağlı olduğunuz diğer paketler arasındaki sahiplik sınırlarını korursunuz.</span><span class="sxs-lookup"><span data-stu-id="affc1-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="affc1-111">Birçok NuGet paketi zaten kendi kaynak denetim depolarında muhafaza edilir.</span><span class="sxs-lookup"><span data-stu-id="affc1-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="affc1-112">Paket geri yükleme NuGet ile varsayılan davranış olmasına rağmen, bu&mdash;makalede `packages` açıklandığı gibi,&mdash;yani, kaynak denetiminden projenizdeki klasörü atlamak için bazı el ile çalışma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="affc1-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="affc1-113">Git ile paketleri atlayarak</span><span class="sxs-lookup"><span data-stu-id="affc1-113">Omitting packages with Git</span></span>

<span data-ttu-id="affc1-114">NuGet paketlerini (`.nupkg`) klasörü ve `packages` `project.assets.json`diğer şeylerin yanı sıra yoksaymak için [.gitignore dosyasını](https://git-scm.com/docs/gitignore) kullanın.</span><span class="sxs-lookup"><span data-stu-id="affc1-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="affc1-115">Referans için Visual [ `.gitignore` Studio projeleri için örneğe](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)bakın:</span><span class="sxs-lookup"><span data-stu-id="affc1-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="affc1-116">Dosyanın `.gitignore` önemli bölümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="affc1-116">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="affc1-117">Team Foundation Sürüm Kontrolü ile paketleri atlayarak</span><span class="sxs-lookup"><span data-stu-id="affc1-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="affc1-118">Projenizi kaynak denetimine eklemeden *önce* mümkünse bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="affc1-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="affc1-119">Aksi takdirde, klasörü `packages` deponuzdan el ile silin ve devam etmeden önce bu değişikliği iade edin.</span><span class="sxs-lookup"><span data-stu-id="affc1-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="affc1-120">Seçili dosyalar için Kaynak Denetimi tümleştirmesini TFVC ile devre dışı kalmak için:</span><span class="sxs-lookup"><span data-stu-id="affc1-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="affc1-121">Çözüm klasörünüzde (dosyanın `.nuget` `.sln` olduğu yerde) adlandırılan bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="affc1-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="affc1-122">İpucu: Windows'da, Windows Gezgini'nde bu `.nuget.` klasörü oluşturmak için, sondaki *noktaile* adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="affc1-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="affc1-123">Bu klasörde, adlı `NuGet.Config` bir dosya oluşturun ve düzenleme için açın.</span><span class="sxs-lookup"><span data-stu-id="affc1-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="affc1-124">Devre [dışı kalanSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ayarı Visual Studio'ya `packages` klasördeki her şeyi atlamasını söylediği aşağıdaki metni minimum olarak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="affc1-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="affc1-125">TFS 2010 veya daha erken kullanıyorsanız, çalışma alanı eşlemelerinizde klasörü `packages` göşeyin.</span><span class="sxs-lookup"><span data-stu-id="affc1-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="affc1-126">TFS 2012 veya sonraki veya Visual Studio Team `.tfignore` Services [ile, Sunucuya Dosya Ekle'de](/vsts/tfvc/add-files-server?view=vsts#tfignore)açıklandığı gibi bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="affc1-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="affc1-127">Bu dosyada, depo düzeyinde `\packages` klasörde yapılan değişiklikleri ve birkaç diğer ara dosyaları açıkça yok saymak için aşağıdaki içeriği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="affc1-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="affc1-128">(Dosyayı Windows Gezgini'nde a `.tfignore.` adını kullanarak oluşturabilirsiniz, ancak önce "Bilinen dosya uzantılarını gizle" seçeneğini devre dışı bırakabilirsiniz.):</span><span class="sxs-lookup"><span data-stu-id="affc1-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="affc1-129">Kaynak `NuGet.Config` `.tfignore` denetimi ne ekler ve değişikliklere iade edin.</span><span class="sxs-lookup"><span data-stu-id="affc1-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
