---
title: NuGet paketleri ve kaynak denetimi
description: Sürüm denetimi ve kaynak denetim sistemleri içindeki NuGet paketlerinin nasıl değerlendirildiğinin ve git ve TFVC ile paketlerin nasıl devralınmasında dikkat edilecek noktalar.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019987"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="c8ccd-103">Kaynak denetim sistemlerinde NuGet paketlerini atlama</span><span class="sxs-lookup"><span data-stu-id="c8ccd-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="c8ccd-104">Geliştiriciler tipik olarak kaynak denetim depolarından NuGet paketlerini atlayın ve bir projenin bağımlılıklarını yapılandırmadan önce yeniden yüklemek için [paket geri yükleme](package-restore.md) ' ye güvenir.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="c8ccd-105">Paket geri yüklemeye bağlı olma nedenleri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="c8ccd-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="c8ccd-106">Git gibi dağıtılmış sürüm denetim sistemleri, depo içindeki her dosyanın her bir sürümünün tam kopyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="c8ccd-107">Sık güncellenen ikili dosyalar, önemli blobu ve deponun kopyalanması için geçen süreyi uzunlukla düşürür.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="c8ccd-108">Paketler depoya dahil edildiğinde, geliştiriciler,, projedeki sabit kodlanmış yol adlarına yol açabilecek şekilde, NuGet aracılığıyla paketlere başvurmak yerine disk üzerindeki paket içeriklerine doğrudan başvuru eklemeye tabi olur.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="c8ccd-109">Hala kullanımda olan herhangi bir paket klasörünü silmemenizi güvence altına aldığınızdan emin olmak için, kullanılmayan paket klasörlerinin çözümünüzü temizlemek daha zor hale gelir.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="c8ccd-110">Paketleri atlayarak, kodunuzun ve bağlı olduğunuz diğer kişilerin paketleri arasındaki sahipliğinin Temizleme sınırlarını koruursunuz.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="c8ccd-111">Birçok NuGet paketi zaten kendi kaynak denetimi depolarında saklanır.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="c8ccd-112">Paket geri yükleme, NuGet ile varsayılan davranış olsa da, bu makalede açıklandığı gibi&mdash; `packages` , bazı el ile yapılan diğer işler, kaynak denetiminden&mdash;, bu makaledeki paketleri atlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="c8ccd-113">Git ile paketleri atlama</span><span class="sxs-lookup"><span data-stu-id="c8ccd-113">Omitting packages with Git</span></span>

<span data-ttu-id="c8ccd-114">[. Gitignore dosyasını](https://git-scm.com/docs/gitignore) , NuGet paketleri (`.nupkg`) `packages` klasörünü ve `project.assets.json`diğer şeyleri göz ardı etmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="c8ccd-115">Başvuru için bkz. [Visual Studio `.gitignore` projeleri için örnek](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="c8ccd-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="c8ccd-116">`.gitignore` Dosyanın önemli kısımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c8ccd-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="c8ccd-117">Team Foundation Sürüm Denetimi paketlerini atlama</span><span class="sxs-lookup"><span data-stu-id="c8ccd-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="c8ccd-118">Projenizi kaynak denetimine eklemeden *önce* mümkünse bu yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="c8ccd-119">Aksi takdirde, `packages` klasörü deponuzdan el ile silin ve devam etmeden önce bu değişikliği iade edin.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="c8ccd-120">Seçili dosyalar için TFVC ile kaynak denetimi tümleştirmesini devre dışı bırakmak için:</span><span class="sxs-lookup"><span data-stu-id="c8ccd-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="c8ccd-121">Çözüm klasörünüzde ( `.sln` dosyanın `.nuget` olduğu) adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="c8ccd-122">İpucu: Windows 'ta, bu klasörü Windows Gezgini 'nde oluşturmak için, adın `.nuget.` sonundaki noktayla *birlikte* kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="c8ccd-123">Bu klasörde adlı `NuGet.Config` bir dosya oluşturun ve dosyayı düzenlenmek üzere açın.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="c8ccd-124">Aşağıdaki metni minimum olarak ekleyin; burada [disablesourcecontrolinteize](../reference/nuget-config-file.md#solution-section) ayarı Visual Studio 'yu `packages` klasördeki her şeyi atlayacak şekilde bildirir:</span><span class="sxs-lookup"><span data-stu-id="c8ccd-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="c8ccd-125">TFS 2010 veya önceki bir sürümünü kullanıyorsanız, çalışma alanı eşlemelerinizde `packages` klasörü gizlerin.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="c8ccd-126">TFS 2012 veya üzeri sürümlerde veya Visual Studio Team Services ile [sunucuya dosya ekleme](/vsts/tfvc/add-files-server?view=vsts#tfignore)bölümünde `.tfignore` açıklandığı gibi bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [Add Files to the Server](/vsts/tfvc/add-files-server?view=vsts#tfignore).</span></span> <span data-ttu-id="c8ccd-127">Bu dosyada, depo düzeyindeki `\packages` klasöre yapılan değişiklikleri ve diğer birkaç ara dosyayı açıkça yoksaymak için aşağıdaki içeriği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c8ccd-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="c8ccd-128">(Dosya adını `.tfignore.` izleyen noktayla kullanarak Windows Gezgini 'nde oluşturabilirsiniz, ancak önce "bilinen dosya uzantılarını gizle" seçeneğini devre dışı bırakmanız gerekebilir.):</span><span class="sxs-lookup"><span data-stu-id="c8ccd-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

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

1. <span data-ttu-id="c8ccd-129">Kaynak denetimi ekleyin `NuGet.Config` ve değişikliklerinizi iade edin. `.tfignore`</span><span class="sxs-lookup"><span data-stu-id="c8ccd-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
