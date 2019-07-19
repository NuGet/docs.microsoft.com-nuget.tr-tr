---
title: NuGet CLı spec komutu
description: NuGet. exe spec komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328275"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="e9dd7-103">spec komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="e9dd7-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="e9dd7-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="e9dd7-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="e9dd7-105">Yeni bir `.nuspec` paket için bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="e9dd7-106">Aynı klasörde bir proje dosyası (`.csproj`, `.vbproj`, `.fsproj`) ile çalıştırırsanız, `spec` simgeleştirilmiş `.nuspec` bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="e9dd7-107">Daha fazla bilgi için bkz. [paket oluşturma](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e9dd7-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="e9dd7-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="e9dd7-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="e9dd7-109">`<packageID>` , `.nuspec` dosyada kaydedilecek isteğe bağlı bir paket tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="e9dd7-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="e9dd7-110">Options</span></span>

| <span data-ttu-id="e9dd7-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="e9dd7-111">Option</span></span> | <span data-ttu-id="e9dd7-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e9dd7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e9dd7-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="e9dd7-113">AssemblyPath</span></span> | <span data-ttu-id="e9dd7-114">Meta veriler için kullanılacak derlemenin yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="e9dd7-115">Zorla</span><span class="sxs-lookup"><span data-stu-id="e9dd7-115">Force</span></span> | <span data-ttu-id="e9dd7-116">Var olan `.nuspec` tüm dosyaların üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="e9dd7-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e9dd7-117">ForceEnglishOutput</span></span> | <span data-ttu-id="e9dd7-118">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e9dd7-119">Help</span><span class="sxs-lookup"><span data-stu-id="e9dd7-119">Help</span></span> | <span data-ttu-id="e9dd7-120">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="e9dd7-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="e9dd7-121">NonInteractive</span></span> | <span data-ttu-id="e9dd7-122">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e9dd7-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="e9dd7-123">Verbosity</span></span> | <span data-ttu-id="e9dd7-124">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="e9dd7-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="e9dd7-125">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e9dd7-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="e9dd7-126">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e9dd7-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
