---
title: NuGet CLı Add komutu
description: NuGet. exe Add komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328362"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="a5c2c-103">Add komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="a5c2c-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="a5c2c-104">**Uygulama hedefi**: paket yayımlaması &bullet; **Desteklenen sürümler**: 3.3+</span><span class="sxs-lookup"><span data-stu-id="a5c2c-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="a5c2c-105">, Paket KIMLIĞI ve sürüm numarası için klasörler içinde oluşturulan, bir hiyerarşik düzende, belirtilen bir paketi HTTP olmayan bir kaynak (klasör veya UNC yolu) öğesine ekler.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="a5c2c-106">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a5c2c-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="a5c2c-107">Paket kaynağına göre geri yükleme veya güncelleştirme yaparken hiyerarşik düzen önemli ölçüde daha iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="a5c2c-108">Paketteki tüm dosyaları hedef paket kaynağına genişletmek için `-Expand` anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="a5c2c-109">Bu genellikle, `tools` ve `lib`gibi, hedefte görüntülenen ek alt klasörlere neden olur.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="a5c2c-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a5c2c-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="a5c2c-111">, eklenecek paketin yol adı, ve `<sourcePath>` paketin ekleneceği klasör tabanlı paket kaynağını belirtir. `<packagePath>`</span><span class="sxs-lookup"><span data-stu-id="a5c2c-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="a5c2c-112">HTTP kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="a5c2c-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="a5c2c-113">Options</span></span>

| <span data-ttu-id="a5c2c-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="a5c2c-114">Option</span></span> | <span data-ttu-id="a5c2c-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a5c2c-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5c2c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a5c2c-116">ConfigFile</span></span> | <span data-ttu-id="a5c2c-117">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a5c2c-118">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a5c2c-119">Expand</span><span class="sxs-lookup"><span data-stu-id="a5c2c-119">Expand</span></span> | <span data-ttu-id="a5c2c-120">Paketteki tüm dosyaları paket kaynağına ekler.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="a5c2c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a5c2c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="a5c2c-122">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a5c2c-123">Help</span><span class="sxs-lookup"><span data-stu-id="a5c2c-123">Help</span></span> | <span data-ttu-id="a5c2c-124">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="a5c2c-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a5c2c-125">NonInteractive</span></span> | <span data-ttu-id="a5c2c-126">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a5c2c-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a5c2c-127">Verbosity</span></span> | <span data-ttu-id="a5c2c-128">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="a5c2c-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a5c2c-129">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a5c2c-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a5c2c-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a5c2c-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
