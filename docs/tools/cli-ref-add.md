---
title: NuGet CLI komut ekleme
description: Nuget.exe için başvuru Ekle komutu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545840"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="dfdad-103">Ekle komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="dfdad-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="dfdad-104">**Uygulandığı**: Paket yayımlama &bullet; **desteklenen sürümler**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="dfdad-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="dfdad-105">Belirtilen paket için paket kimliği ve sürüm numarasını klasörler burada görüntülerle oluşturulur bir hiyerarşik düzende HTTP olmayan paket kaynağını (bir klasör veya UNC yolu) ekler.</span><span class="sxs-lookup"><span data-stu-id="dfdad-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="dfdad-106">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="dfdad-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="dfdad-107">Geri yükleme veya güncelleştirme karşı paket kaynağı, hiyerarşik yerleşim önemli ölçüde daha iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="dfdad-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="dfdad-108">Paketteki tüm dosyaların hedef paket kaynak genişletmek için kullanmak `-Expand` geçin.</span><span class="sxs-lookup"><span data-stu-id="dfdad-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="dfdad-109">Bu genellikle hedef, aşağıdaki gibi görünen ek alt klasörlerinde sonuçları `tools` ve `lib`.</span><span class="sxs-lookup"><span data-stu-id="dfdad-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="dfdad-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="dfdad-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="dfdad-111">Burada `<packagePath>` eklemek için paket için bir yol adı ve `<sourcePath>` , pakete eklenecek klasör tabanlı paket kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="dfdad-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="dfdad-112">HTTP kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="dfdad-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="dfdad-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="dfdad-113">Options</span></span>

| <span data-ttu-id="dfdad-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="dfdad-114">Option</span></span> | <span data-ttu-id="dfdad-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="dfdad-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dfdad-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dfdad-116">ConfigFile</span></span> | <span data-ttu-id="dfdad-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="dfdad-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dfdad-118">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dfdad-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dfdad-119">Genişletin</span><span class="sxs-lookup"><span data-stu-id="dfdad-119">Expand</span></span> | <span data-ttu-id="dfdad-120">Tüm dosyalar paket kaynağına pakette ekler.</span><span class="sxs-lookup"><span data-stu-id="dfdad-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="dfdad-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dfdad-121">ForceEnglishOutput</span></span> | <span data-ttu-id="dfdad-122">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="dfdad-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dfdad-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="dfdad-123">Help</span></span> | <span data-ttu-id="dfdad-124">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dfdad-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="dfdad-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dfdad-125">NonInteractive</span></span> | <span data-ttu-id="dfdad-126">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="dfdad-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dfdad-127">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="dfdad-127">Verbosity</span></span> | <span data-ttu-id="dfdad-128">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="dfdad-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="dfdad-129">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dfdad-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dfdad-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="dfdad-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
