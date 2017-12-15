---
title: NuGet CLI init komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Nuget.exe init komut başvurusu"
keywords: "nuget init başvuru, Init komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="2c674-104">Init komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2c674-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="2c674-105">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="2c674-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="2c674-106">Tüm paketler için açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre düz bir klasörden kopyalar [Ekle komutu](#add) üstünde.</span><span class="sxs-lookup"><span data-stu-id="2c674-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="2c674-107">Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paketinizdeki komutu.</span><span class="sxs-lookup"><span data-stu-id="2c674-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="2c674-108">İle `add`, hedef bir yerel klasör veya bir UNC yolu; olmalıdır HTTP paket depoları nuget.org veya özel sunucuları gibi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2c674-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="2c674-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="2c674-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="2c674-110">Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname olduğu paketleri kopyalanacak.</span><span class="sxs-lookup"><span data-stu-id="2c674-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="2c674-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="2c674-111">Options</span></span>

| <span data-ttu-id="2c674-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="2c674-112">Option</span></span> | <span data-ttu-id="2c674-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2c674-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c674-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2c674-114">ConfigFile</span></span> | <span data-ttu-id="2c674-115">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="2c674-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2c674-116">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2c674-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="2c674-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2c674-117">ForceEnglishOutput</span></span> | <span data-ttu-id="2c674-118">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="2c674-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2c674-119">Genişletme</span><span class="sxs-lookup"><span data-stu-id="2c674-119">Expand</span></span> | <span data-ttu-id="2c674-120">Paket kaynağı eklenen her paketindeki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu.</span><span class="sxs-lookup"><span data-stu-id="2c674-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="2c674-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="2c674-121">Help</span></span> | <span data-ttu-id="2c674-122">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2c674-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="2c674-123">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="2c674-123">NonInteractive</span></span> | <span data-ttu-id="2c674-124">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="2c674-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2c674-125">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="2c674-125">Verbosity</span></span> | <span data-ttu-id="2c674-126">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="2c674-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="2c674-127">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2c674-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2c674-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="2c674-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
