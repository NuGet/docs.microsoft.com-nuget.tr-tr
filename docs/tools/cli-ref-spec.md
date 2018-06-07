---
title: NuGet CLI belirtim komutu
description: Nuget.exe belirtim komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817092"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="4b54e-103">belirtim komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4b54e-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="4b54e-104">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="4b54e-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4b54e-105">Oluşturan bir `.nuspec` dosyası yeni bir paket için.</span><span class="sxs-lookup"><span data-stu-id="4b54e-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="4b54e-106">Proje dosyası ile aynı klasörde çalıştırırsanız (`.csproj`, `.vbproj`, `.fsproj`), `spec` bir parçalanmış oluşturur `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="4b54e-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="4b54e-107">Ek bilgi için bkz: [paket oluşturma](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4b54e-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="4b54e-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="4b54e-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="4b54e-109">Burada `<packageID>` kaydetmek için bir isteğe bağlı paket tanımlayıcısı `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="4b54e-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="4b54e-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="4b54e-110">Options</span></span>

| <span data-ttu-id="4b54e-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="4b54e-111">Option</span></span> | <span data-ttu-id="4b54e-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4b54e-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b54e-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="4b54e-113">AssemblyPath</span></span> | <span data-ttu-id="4b54e-114">Meta veriler için kullanmak için derleme yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="4b54e-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="4b54e-115">Zorla</span><span class="sxs-lookup"><span data-stu-id="4b54e-115">Force</span></span> | <span data-ttu-id="4b54e-116">Var olan üzerine yazar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="4b54e-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="4b54e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="4b54e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="4b54e-118">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="4b54e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="4b54e-119">Yardım</span><span class="sxs-lookup"><span data-stu-id="4b54e-119">Help</span></span> | <span data-ttu-id="4b54e-120">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4b54e-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="4b54e-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4b54e-121">NonInteractive</span></span> | <span data-ttu-id="4b54e-122">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="4b54e-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="4b54e-123">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="4b54e-123">Verbosity</span></span> | <span data-ttu-id="4b54e-124">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="4b54e-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="4b54e-125">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="4b54e-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4b54e-126">Örnekler</span><span class="sxs-lookup"><span data-stu-id="4b54e-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
