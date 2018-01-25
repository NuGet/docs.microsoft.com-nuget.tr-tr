---
title: NuGet paketleri ve kaynak denetimi | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Sürüm denetimi ve kaynak denetim sistemleri içindeki NuGet paketleri kabul etme ve git ve TFVC'yi paketlerle atlayın durumları."
keywords: "Depoları NuGet kaynak denetimi, NuGet sürüm denetimi, NuGet ve git, NuGet ve TFS, NuGet ve TFVC'yi, atlama paketleri, kaynak denetimi depoları, sürüm denetimi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 274492f2b1d05c781dadaab70cdc7d281549d002
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="25ef3-104">Kaynak Denetim sistemleri NuGet paketlerini atlama</span><span class="sxs-lookup"><span data-stu-id="25ef3-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="25ef3-105">Geliştiriciler genellikle kendi kaynak denetimi depoları NuGet paketleri atlayın ve bunun yerine Bel [paket geri yükleme](../consume-packages/package-restore.md) bir yapı önce bir proje bağımlılıklarınızı yeniden yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="25ef3-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](../consume-packages/package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="25ef3-106">Paket geri yükleme bağlı nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="25ef3-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="25ef3-107">Git gibi dağıtılmış sürüm denetim sistemleri her sürüm deposu içinde her dosyanın tam kopyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="25ef3-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="25ef3-108">Sık sık güncelleştirilen ikili dosyaları için önemli oluşan şişirmeyi sağlama ve depoyu kopyalayın süresini düşey çizgi ise uzar.</span><span class="sxs-lookup"><span data-stu-id="25ef3-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="25ef3-109">Paketleri depoya eklendiğinde, geliştiricilerin, doğrudan paket içeriğini başvuru paketler sabit kodlanmış yol adları projesinde açabilir NuGet aracılığıyla yerine disk eklemek zararlardan önerilir.</span><span class="sxs-lookup"><span data-stu-id="25ef3-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="25ef3-110">Paket klasörleri hala kullanımda silmeyin emin olmak gereksinim duyduğunuz çözümünüzün herhangi kullanılmayan paket klasörlerinin temiz zor olur.</span><span class="sxs-lookup"><span data-stu-id="25ef3-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="25ef3-111">Paketleri kaldırarak sahipliği temiz sınırlarının kodunuzu, bağlı diğer paketleri arasındaki korur.</span><span class="sxs-lookup"><span data-stu-id="25ef3-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="25ef3-112">Birçok NuGet paketleri kendi kaynak denetimi depoları zaten saklanır.</span><span class="sxs-lookup"><span data-stu-id="25ef3-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="25ef3-113">Paket geri yüklemesi varsayılan davranışı NuGet ile el ile bazı iş paketleri atlamak gerekli olsa da&mdash;öğesine, `packages` projenizdeki klasöre&mdash;kaynak denetiminden aşağıdaki bölümlerde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="25ef3-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in the following sections.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="25ef3-114">Git paketlerle atlama</span><span class="sxs-lookup"><span data-stu-id="25ef3-114">Omitting packages with Git</span></span>

<span data-ttu-id="25ef3-115">Kullanım [.gitignore dosyası](https://git-scm.com/docs/gitignore) eklenmesini önlemek için `packages` kaynak denetimi klasöründe.</span><span class="sxs-lookup"><span data-stu-id="25ef3-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to avoid including the `packages` folder in source control.</span></span> <span data-ttu-id="25ef3-116">Başvuru için bkz: [örnek `.gitignore` Visual Studio projeleri için](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="25ef3-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="25ef3-117">Önemli kısımlarını `.gitignore` dosyası:</span><span class="sxs-lookup"><span data-stu-id="25ef3-117">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="25ef3-118">Team Foundation sürüm denetimi paketlerle atlama</span><span class="sxs-lookup"><span data-stu-id="25ef3-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="25ef3-119">Bu yönergeleri mümkünse *önce* projenizi kaynak denetimine ekleme.</span><span class="sxs-lookup"><span data-stu-id="25ef3-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="25ef3-120">Aksi takdirde, el ile silmeniz `packages` klasöründen depo ve devam etmeden önce bu değişikliği denetleyin.</span><span class="sxs-lookup"><span data-stu-id="25ef3-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="25ef3-121">Seçili dosyaları için TFVC'yi kaynak denetimi tümleştirmesi devre dışı bırakmak için:</span><span class="sxs-lookup"><span data-stu-id="25ef3-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="25ef3-122">Adlı bir klasör oluşturun `.nuget` çözüm klasördeki (burada `.sln` dosyası).</span><span class="sxs-lookup"><span data-stu-id="25ef3-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="25ef3-123">İpucu: Kullanın adı, Windows bu klasörü Windows Gezgini'nde oluşturmak için `.nuget.` *ile* sondaki noktayı.</span><span class="sxs-lookup"><span data-stu-id="25ef3-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="25ef3-124">Bu klasörde adlı bir dosya oluşturun `NuGet.Config` ve düzenlemek için açın.</span><span class="sxs-lookup"><span data-stu-id="25ef3-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="25ef3-125">Minimum olarak aşağıdaki metni ekleyin nerede [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) ayarı bildirir her şeyi atlamak için Visual Studio `packages` klasörü:</span><span class="sxs-lookup"><span data-stu-id="25ef3-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="25ef3-126">TFS 2010 veya önceki bir sürümünü kullanıyorsanız, gizlemek `packages` çalışma eşlemelerinizin klasöründe.</span><span class="sxs-lookup"><span data-stu-id="25ef3-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="25ef3-127">TFS 2012 veya sonraki sürümünü veya Visual Studio Team Services ile oluşturma bir `.tfignore` dosya açıklandığı gibi [AddFiles sunucuya](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span><span class="sxs-lookup"><span data-stu-id="25ef3-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="25ef3-128">Bu dosyada yapılan değişiklikler açıkça yoksaymak için aşağıdaki içerik `\packages` depo düzeyi ve diğer birkaç Ara dosyaları klasörü.</span><span class="sxs-lookup"><span data-stu-id="25ef3-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="25ef3-129">(Dosya adını kullanarak Windows Gezgini'nde oluşturabileceğiniz bir `.tfignore.` sondaki noktayı, ancak ile devre dışı bırakmak için "Bilinen dosya uzantılarını gizle" ilk seçenek.):</span><span class="sxs-lookup"><span data-stu-id="25ef3-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="25ef3-130">Ekleme `NuGet.Config` ve `.tfignore` kaynak denetimi ve yaptığınız değişiklikleri denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="25ef3-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
