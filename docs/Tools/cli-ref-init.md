---
title: NuGet CLI init komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe init komut başvurusu"
keywords: "nuget init başvuru, Init komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="cc6be-104">Init komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cc6be-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="cc6be-105">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="cc6be-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="cc6be-106">Tüm paketler için açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre düz bir klasörden kopyalar [Ekle komutu](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="cc6be-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="cc6be-107">Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paketinizdeki komutu.</span><span class="sxs-lookup"><span data-stu-id="cc6be-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="cc6be-108">İle `add`, hedef bir yerel klasör veya bir UNC yolu; olmalıdır HTTP paket depoları nuget.org veya özel sunucuları gibi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="cc6be-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="cc6be-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cc6be-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="cc6be-110">Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname paketleri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="cc6be-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="cc6be-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="cc6be-111">Options</span></span>

| <span data-ttu-id="cc6be-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="cc6be-112">Option</span></span> | <span data-ttu-id="cc6be-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc6be-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc6be-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cc6be-114">ConfigFile</span></span> | <span data-ttu-id="cc6be-115">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="cc6be-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cc6be-116">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc6be-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="cc6be-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cc6be-117">ForceEnglishOutput</span></span> | <span data-ttu-id="cc6be-118">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="cc6be-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cc6be-119">Genişletme</span><span class="sxs-lookup"><span data-stu-id="cc6be-119">Expand</span></span> | <span data-ttu-id="cc6be-120">Paket kaynağı eklenen her paketindeki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu.</span><span class="sxs-lookup"><span data-stu-id="cc6be-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="cc6be-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="cc6be-121">Help</span></span> | <span data-ttu-id="cc6be-122">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="cc6be-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="cc6be-123">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="cc6be-123">NonInteractive</span></span> | <span data-ttu-id="cc6be-124">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="cc6be-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cc6be-125">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="cc6be-125">Verbosity</span></span> | <span data-ttu-id="cc6be-126">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="cc6be-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cc6be-127">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cc6be-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cc6be-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="cc6be-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
