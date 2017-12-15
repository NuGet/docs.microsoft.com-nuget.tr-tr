---
title: NuGet CLI Ekle komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4f68a016-ad4e-41fc-b869-88910fc5121e
description: "Nuget.exe için başvuru Ekle komutu"
keywords: "nuget başvuru eklemek için paket komut ekleme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bf9a6e51dfbf1716ba40273487b76ae04c18e948
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="76126-104">Ekle komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="76126-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="76126-105">**Uygulandığı öğe**: paketini yayımlama &bullet; **desteklenen sürümleri**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="76126-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="76126-106">Belirli bir paket (bir klasör veya UNC yolu) HTTP olmayan paket kaynağı klasörler için paket kimliği ve sürüm numarası; burada görüntülerle oluşturulan bir hiyerarşik düzende ekler.</span><span class="sxs-lookup"><span data-stu-id="76126-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="76126-107">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76126-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="76126-108">Geri yükleme veya paket kaynağında Güncelleştirme sırasında hiyerarşik düzeni önemli ölçüde daha iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="76126-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="76126-109">Paketteki tüm dosyaları hedef paket kaynağına genişletmek için kullanmak `-Expand` geçin.</span><span class="sxs-lookup"><span data-stu-id="76126-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="76126-110">Bu genellikle hedef gibi görünen ek alt klasörler sonuçları `tools` ve `lib`.</span><span class="sxs-lookup"><span data-stu-id="76126-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="76126-111">Kullanım</span><span class="sxs-lookup"><span data-stu-id="76126-111">Usage</span></span>

```
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="76126-112">Burada `<packagePath>` eklemek için paket için yol adı ve `<sourcePath>` için paket eklenecek klasör tabanlı paket kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="76126-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="76126-113">HTTP kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="76126-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="76126-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="76126-114">Options</span></span>

| <span data-ttu-id="76126-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="76126-115">Option</span></span> | <span data-ttu-id="76126-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="76126-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76126-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="76126-117">ConfigFile</span></span> | <span data-ttu-id="76126-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="76126-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="76126-119">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="76126-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="76126-120">Genişletme</span><span class="sxs-lookup"><span data-stu-id="76126-120">Expand</span></span> | <span data-ttu-id="76126-121">Tüm dosyalar paket kaynağına pakette ekler.</span><span class="sxs-lookup"><span data-stu-id="76126-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="76126-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="76126-122">ForceEnglishOutput</span></span> | <span data-ttu-id="76126-123">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="76126-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="76126-124">Yardım</span><span class="sxs-lookup"><span data-stu-id="76126-124">Help</span></span> | <span data-ttu-id="76126-125">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="76126-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="76126-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="76126-126">NonInteractive</span></span> | <span data-ttu-id="76126-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="76126-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="76126-128">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="76126-128">Verbosity</span></span> | <span data-ttu-id="76126-129">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="76126-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="76126-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="76126-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="76126-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="76126-131">Examples</span></span>

```
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
