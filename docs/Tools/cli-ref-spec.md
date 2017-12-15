---
title: NuGet CLI belirtim komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe belirtim komut başvurusu"
keywords: "nuget belirtim başvurusu, belirtim komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="566c7-104">belirtim komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="566c7-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="566c7-105">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="566c7-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="566c7-106">Oluşturan bir `.nuspec` dosyası yeni bir paket için.</span><span class="sxs-lookup"><span data-stu-id="566c7-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="566c7-107">Proje dosyası ile aynı klasörde çalıştırırsanız (`.csproj`, `.vbproj`, `.fsproj`), `spec` bir parçalanmış oluşturur `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="566c7-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="566c7-108">Ek bilgi için bkz: [paket oluşturma](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="566c7-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="566c7-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="566c7-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="566c7-110">Burada `<packageID>` kaydetmek için bir isteğe bağlı paket tanımlayıcısı `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="566c7-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="566c7-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="566c7-111">Options</span></span>

| <span data-ttu-id="566c7-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="566c7-112">Option</span></span> | <span data-ttu-id="566c7-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="566c7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="566c7-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="566c7-114">AssemblyPath</span></span> | <span data-ttu-id="566c7-115">Meta veriler için kullanmak için derleme yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="566c7-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="566c7-116">Zorla</span><span class="sxs-lookup"><span data-stu-id="566c7-116">Force</span></span> | <span data-ttu-id="566c7-117">Var olan üzerine yazar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="566c7-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="566c7-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="566c7-118">ForceEnglishOutput</span></span> | <span data-ttu-id="566c7-119">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="566c7-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="566c7-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="566c7-120">Help</span></span> | <span data-ttu-id="566c7-121">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="566c7-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="566c7-122">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="566c7-122">NonInteractive</span></span> | <span data-ttu-id="566c7-123">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="566c7-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="566c7-124">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="566c7-124">Verbosity</span></span> | <span data-ttu-id="566c7-125">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="566c7-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="566c7-126">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="566c7-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="566c7-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="566c7-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
