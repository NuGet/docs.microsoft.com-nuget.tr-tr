---
title: Özel NuGet CLI komutu
description: Nuget.exe özel komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794157"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="fe58b-103">özel komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fe58b-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="fe58b-104">**İçin geçerlidir:** paket oluşturma &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="fe58b-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fe58b-105">Oluşturur bir `.nuspec` için yeni bir paket dosyası.</span><span class="sxs-lookup"><span data-stu-id="fe58b-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="fe58b-106">Bir proje dosyası ile aynı klasörde çalıştırırsanız (`.csproj`, `.vbproj`, `.fsproj`), `spec` bir simgeleştirilmiş oluşturur `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="fe58b-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="fe58b-107">Ek bilgi için bkz: [paket oluşturma](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="fe58b-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fe58b-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="fe58b-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="fe58b-109">Burada `<packageID>` kaydetmek için bir isteğe bağlı paket tanımlayıcısı `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="fe58b-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="fe58b-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="fe58b-110">Options</span></span>

| <span data-ttu-id="fe58b-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="fe58b-111">Option</span></span> | <span data-ttu-id="fe58b-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe58b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe58b-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="fe58b-113">AssemblyPath</span></span> | <span data-ttu-id="fe58b-114">Meta verileri için kullanılacak derleme yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="fe58b-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="fe58b-115">Zorla</span><span class="sxs-lookup"><span data-stu-id="fe58b-115">Force</span></span> | <span data-ttu-id="fe58b-116">Var olan tüm üzerine yazar `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="fe58b-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="fe58b-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fe58b-117">ForceEnglishOutput</span></span> | <span data-ttu-id="fe58b-118">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="fe58b-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fe58b-119">Yardım</span><span class="sxs-lookup"><span data-stu-id="fe58b-119">Help</span></span> | <span data-ttu-id="fe58b-120">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fe58b-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="fe58b-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="fe58b-121">NonInteractive</span></span> | <span data-ttu-id="fe58b-122">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="fe58b-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fe58b-123">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="fe58b-123">Verbosity</span></span> | <span data-ttu-id="fe58b-124">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="fe58b-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fe58b-125">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fe58b-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fe58b-126">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fe58b-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
