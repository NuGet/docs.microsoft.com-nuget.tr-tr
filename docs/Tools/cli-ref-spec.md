---
title: NuGet CLI belirtim komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe belirtim komut başvurusu"
keywords: "nuget belirtim başvurusu, belirtim komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="f979e-104">belirtim komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f979e-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="f979e-105">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="f979e-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f979e-106">Oluşturan bir `.nuspec` dosyası yeni bir paket için.</span><span class="sxs-lookup"><span data-stu-id="f979e-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="f979e-107">Proje dosyası ile aynı klasörde çalıştırırsanız (`.csproj`, `.vbproj`, `.fsproj`), `spec` bir parçalanmış oluşturur `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="f979e-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="f979e-108">Ek bilgi için bkz: [paket oluşturma](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="f979e-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f979e-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="f979e-109">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="f979e-110">Burada `<packageID>` kaydetmek için bir isteğe bağlı paket tanımlayıcısı `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="f979e-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="f979e-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="f979e-111">Options</span></span>

| <span data-ttu-id="f979e-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="f979e-112">Option</span></span> | <span data-ttu-id="f979e-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f979e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f979e-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="f979e-114">AssemblyPath</span></span> | <span data-ttu-id="f979e-115">Meta veriler için kullanmak için derleme yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f979e-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="f979e-116">Force</span><span class="sxs-lookup"><span data-stu-id="f979e-116">Force</span></span> | <span data-ttu-id="f979e-117">Var olan üzerine yazar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="f979e-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="f979e-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f979e-118">ForceEnglishOutput</span></span> | <span data-ttu-id="f979e-119">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="f979e-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f979e-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="f979e-120">Help</span></span> | <span data-ttu-id="f979e-121">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f979e-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="f979e-122">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="f979e-122">NonInteractive</span></span> | <span data-ttu-id="f979e-123">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="f979e-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f979e-124">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="f979e-124">Verbosity</span></span> | <span data-ttu-id="f979e-125">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="f979e-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f979e-126">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f979e-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f979e-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f979e-127">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
