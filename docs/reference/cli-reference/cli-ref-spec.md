---
title: NuGet CLı spec komutu
description: nuget.exe spec komutu başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622570"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="08384-103">spec komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="08384-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="08384-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="08384-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="08384-105">`.nuspec`Yeni bir paket için bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="08384-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="08384-106">Aynı klasörde bir proje dosyası ( `.csproj` , `.vbproj` ,) ile çalıştırırsanız `.fsproj` , `spec` simgeleştirilmiş bir `.nuspec` dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="08384-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="08384-107">Daha fazla bilgi için bkz. [paket oluşturma](../../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="08384-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="08384-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="08384-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="08384-109">, `<packageID>` dosyada kaydedilecek isteğe bağlı bir paket tanımlayıcısıdır `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="08384-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="08384-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="08384-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="08384-111">Meta veriler için kullanılacak derlemenin yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="08384-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="08384-112">Var olan tüm `.nuspec` dosyaların üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="08384-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="08384-113">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="08384-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="08384-114">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="08384-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="08384-115">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="08384-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="08384-116">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="08384-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="08384-117">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="08384-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="08384-118">Örnekler</span><span class="sxs-lookup"><span data-stu-id="08384-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
