---
title: NuGet CLI Ekle komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe için başvuru Ekle komutu"
keywords: "nuget başvuru eklemek için paket komut ekleme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70c86f8d240bd308224f6b7887b630cc1e953bf8
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="9269d-104">Ekle komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9269d-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="9269d-105">**Uygulandığı öğe**: paketini yayımlama &bullet; **desteklenen sürümleri**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="9269d-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="9269d-106">Belirli bir paket (bir klasör veya UNC yolu) HTTP olmayan paket kaynağı klasörler için paket kimliği ve sürüm numarası; burada görüntülerle oluşturulan bir hiyerarşik düzende ekler.</span><span class="sxs-lookup"><span data-stu-id="9269d-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="9269d-107">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9269d-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="9269d-108">Geri yükleme veya paket kaynağında Güncelleştirme sırasında hiyerarşik düzeni önemli ölçüde daha iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="9269d-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="9269d-109">Paketteki tüm dosyaları hedef paket kaynağına genişletmek için kullanmak `-Expand` geçin.</span><span class="sxs-lookup"><span data-stu-id="9269d-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="9269d-110">Bu genellikle hedef gibi görünen ek alt klasörler sonuçları `tools` ve `lib`.</span><span class="sxs-lookup"><span data-stu-id="9269d-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="9269d-111">Kullanım</span><span class="sxs-lookup"><span data-stu-id="9269d-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="9269d-112">Burada `<packagePath>` eklemek için paket için yol adı ve `<sourcePath>` için paket eklenecek klasör tabanlı paket kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9269d-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="9269d-113">HTTP kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9269d-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="9269d-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="9269d-114">Options</span></span>

| <span data-ttu-id="9269d-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="9269d-115">Option</span></span> | <span data-ttu-id="9269d-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9269d-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9269d-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9269d-117">ConfigFile</span></span> | <span data-ttu-id="9269d-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="9269d-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9269d-119">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9269d-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="9269d-120">Genişletme</span><span class="sxs-lookup"><span data-stu-id="9269d-120">Expand</span></span> | <span data-ttu-id="9269d-121">Tüm dosyalar paket kaynağına pakette ekler.</span><span class="sxs-lookup"><span data-stu-id="9269d-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="9269d-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9269d-122">ForceEnglishOutput</span></span> | <span data-ttu-id="9269d-123">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="9269d-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9269d-124">Yardım</span><span class="sxs-lookup"><span data-stu-id="9269d-124">Help</span></span> | <span data-ttu-id="9269d-125">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9269d-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="9269d-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="9269d-126">NonInteractive</span></span> | <span data-ttu-id="9269d-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="9269d-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9269d-128">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="9269d-128">Verbosity</span></span> | <span data-ttu-id="9269d-129">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="9269d-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9269d-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9269d-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9269d-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9269d-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
