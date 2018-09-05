---
title: NuGet paketleri ve kaynak denetimi
description: İçin nasıl işlemesi gerektiğini NuGet paketleri içinde sürüm denetimi ve kaynak denetimi sistemlerini ve git ve TFVC paketlerle atlamak nasıl konuları.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 0338c3445b2a3d8169158171d97d1e874533a80a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551805"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="d750b-103">NuGet paketlerini kaynak denetimi sistemlerini atlama</span><span class="sxs-lookup"><span data-stu-id="d750b-103">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="d750b-104">Geliştiriciler genellikle kendi kaynak denetim depolarından NuGet paketlerini atlayın ve bunun yerine dayanır [geri yükleme paketini](package-restore.md) bir yapıdan önce bir proje bağımlılıklarınızı yeniden yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="d750b-104">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="d750b-105">Paket geri yükleme'yi bağlı olan nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d750b-105">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="d750b-106">Dağıtılmış sürüm denetim sistemleri, Git gibi tam kopyasını havuz içindeki her dosyanın her sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="d750b-106">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="d750b-107">Sık sık güncelleştirilir ikili dosyalar için önemli bir şişmeye neden ve uygulamanın deposunu kopyalamak için geçen süreyi düşey çizgi ise uzar.</span><span class="sxs-lookup"><span data-stu-id="d750b-107">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="d750b-108">Paketleri depoda eklendiğinde, geliştiricilerin doğrudan paket içeriğini, proje adlarında sabit kodlanmış bir yol açabilir ve NuGet aracılığıyla başvuran paketleri yerine disk eklemek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="d750b-108">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="d750b-109">Hala kullanımda paket klasörleri silme emin olmak gerek duyduğunuz tüm kullanılmayan paket klasörlerinin çözümünüzü temizlemek daha zor hale gelir.</span><span class="sxs-lookup"><span data-stu-id="d750b-109">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="d750b-110">Paketleri gt;(yok) sahiplik temiz sınırları kodunuzu, bağlı diğer paketlerden arasındaki korur.</span><span class="sxs-lookup"><span data-stu-id="d750b-110">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="d750b-111">Birçok NuGet paketi zaten kendi kaynak denetimi depoları saklanır.</span><span class="sxs-lookup"><span data-stu-id="d750b-111">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="d750b-112">Paket geri yükleme ile NuGet varsayılan davranışı olsa da, bazı el ile iş paketleri atlamak gerekli olan&mdash;yani `packages` projenizdeki klasöre&mdash;kaynak denetiminden bu makalede açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="d750b-112">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="d750b-113">Git ile paketleri atlama</span><span class="sxs-lookup"><span data-stu-id="d750b-113">Omitting packages with Git</span></span>

<span data-ttu-id="d750b-114">Kullanım [.gitignore dosyası](https://git-scm.com/docs/gitignore) NuGet paketlerini yok saymak için (`.nupkg`) `packages` klasöründe ve `project.assets.json`, başka şeylerin yanında.</span><span class="sxs-lookup"><span data-stu-id="d750b-114">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="d750b-115">Başvuru için bkz: [örnek `.gitignore` Visual Studio projeleri için](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="d750b-115">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="d750b-116">Önemli bölümleri `.gitignore` dosyası:</span><span class="sxs-lookup"><span data-stu-id="d750b-116">The important parts of the `.gitignore` file are:</span></span>

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

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="d750b-117">Team Foundation sürüm denetimi paketlerle atlama</span><span class="sxs-lookup"><span data-stu-id="d750b-117">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="d750b-118">Mümkünse bu yönergeleri izleyin *önce* kaynak denetimine projenize ekleme.</span><span class="sxs-lookup"><span data-stu-id="d750b-118">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="d750b-119">Aksi takdirde, el ile silmeniz `packages` depo ve devam etmeden önce bu değişikliği iade klasöründen.</span><span class="sxs-lookup"><span data-stu-id="d750b-119">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="d750b-120">Seçili dosyaları için TFVC ile kaynak denetimi tümleştirmesi devre dışı bırakmak için:</span><span class="sxs-lookup"><span data-stu-id="d750b-120">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="d750b-121">Adlı bir klasör oluşturun `.nuget` çözüm klasöründe (burada `.sln` dosyasıdır).</span><span class="sxs-lookup"><span data-stu-id="d750b-121">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="d750b-122">İpucu: Windows üzerinde bu klasörü Windows Gezgini'nde oluşturmak için adı kullanın `.nuget.` *ile* nokta karakteri.</span><span class="sxs-lookup"><span data-stu-id="d750b-122">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="d750b-123">Bu klasörde adlı bir dosya oluşturun `NuGet.Config` ve düzenleme için açın.</span><span class="sxs-lookup"><span data-stu-id="d750b-123">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="d750b-124">Minimum olarak aşağıdaki metni ekleyin burada [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ayarı bildirir her şeyi atlamak için Visual Studio `packages` klasörü:</span><span class="sxs-lookup"><span data-stu-id="d750b-124">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="d750b-125">TFS 2010 veya önceki bir sürümü kullanıyorsanız, gizlemek `packages` klasöründe, çalışma alanı eşlemeleri.</span><span class="sxs-lookup"><span data-stu-id="d750b-125">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="d750b-126">TFS 2012 veya sonraki sürümünü veya Visual Studio Team Services ile oluşturma bir `.tfignore` dosya çubuğunda açıklandığı [sunucuya AddFiles](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span><span class="sxs-lookup"><span data-stu-id="d750b-126">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](/vsts/tfvc/add-files-server.md?view=vsts#tfignore).</span></span> <span data-ttu-id="d750b-127">Bu dosyada, açıkça Değişiklikleri yoksaymak için aşağıdaki içeriği içerir `\packages` depo düzey ve diğer birkaç Ara dosyaları klasörü.</span><span class="sxs-lookup"><span data-stu-id="d750b-127">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="d750b-128">(Dosya adını kullanarak Windows Gezgini'nde oluşturabileceğiniz bir `.tfignore.` sondaki noktayı ancak siz ile devre dışı bırakmak için "Bilinen dosya uzantıları gizle" ilk seçenek.):</span><span class="sxs-lookup"><span data-stu-id="d750b-128">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="d750b-129">Ekleme `NuGet.Config` ve `.tfignore` kaynak denetimi ve değişikliklerinizi iade edin.</span><span class="sxs-lookup"><span data-stu-id="d750b-129">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
