---
title: NuGet CLI Ekle komutu
description: Nuget.exe için başvuru Ekle komutu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817616"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="291eb-103">Ekle komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="291eb-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="291eb-104">**Uygulandığı öğe**: paketini yayımlama &bullet; **desteklenen sürümleri**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="291eb-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="291eb-105">Belirli bir paket (bir klasör veya UNC yolu) HTTP olmayan paket kaynağı klasörler için paket kimliği ve sürüm numarası; burada görüntülerle oluşturulan bir hiyerarşik düzende ekler.</span><span class="sxs-lookup"><span data-stu-id="291eb-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="291eb-106">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="291eb-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="291eb-107">Geri yükleme veya paket kaynağında Güncelleştirme sırasında hiyerarşik düzeni önemli ölçüde daha iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="291eb-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="291eb-108">Paketteki tüm dosyaları hedef paket kaynağına genişletmek için kullanmak `-Expand` geçin.</span><span class="sxs-lookup"><span data-stu-id="291eb-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="291eb-109">Bu genellikle hedef gibi görünen ek alt klasörler sonuçları `tools` ve `lib`.</span><span class="sxs-lookup"><span data-stu-id="291eb-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="291eb-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="291eb-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="291eb-111">Burada `<packagePath>` eklemek için paket için yol adı ve `<sourcePath>` için paket eklenecek klasör tabanlı paket kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="291eb-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="291eb-112">HTTP kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="291eb-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="291eb-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="291eb-113">Options</span></span>

| <span data-ttu-id="291eb-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="291eb-114">Option</span></span> | <span data-ttu-id="291eb-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="291eb-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="291eb-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="291eb-116">ConfigFile</span></span> | <span data-ttu-id="291eb-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="291eb-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="291eb-118">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="291eb-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="291eb-119">Genişletme</span><span class="sxs-lookup"><span data-stu-id="291eb-119">Expand</span></span> | <span data-ttu-id="291eb-120">Tüm dosyalar paket kaynağına pakette ekler.</span><span class="sxs-lookup"><span data-stu-id="291eb-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="291eb-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="291eb-121">ForceEnglishOutput</span></span> | <span data-ttu-id="291eb-122">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="291eb-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="291eb-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="291eb-123">Help</span></span> | <span data-ttu-id="291eb-124">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="291eb-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="291eb-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="291eb-125">NonInteractive</span></span> | <span data-ttu-id="291eb-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="291eb-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="291eb-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="291eb-127">Verbosity</span></span> | <span data-ttu-id="291eb-128">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="291eb-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="291eb-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="291eb-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="291eb-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="291eb-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
