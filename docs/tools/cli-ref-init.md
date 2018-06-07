---
title: NuGet CLI init komutu
description: Nuget.exe init komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4fda33aabd51fbbf0e5559baaa42af065366ba4
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817824"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="234c2-103">Init komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="234c2-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="234c2-104">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="234c2-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="234c2-105">Tüm paketler için açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre düz bir klasörden kopyalar [Ekle komutu](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="234c2-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="234c2-106">Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paketinizdeki komutu.</span><span class="sxs-lookup"><span data-stu-id="234c2-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="234c2-107">İle `add`, hedef bir yerel klasör veya bir UNC yolu; olmalıdır HTTP paket depoları nuget.org veya özel sunucuları gibi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="234c2-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="234c2-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="234c2-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="234c2-109">Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname paketleri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="234c2-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="234c2-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="234c2-110">Options</span></span>

| <span data-ttu-id="234c2-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="234c2-111">Option</span></span> | <span data-ttu-id="234c2-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="234c2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="234c2-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="234c2-113">ConfigFile</span></span> | <span data-ttu-id="234c2-114">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="234c2-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="234c2-115">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="234c2-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="234c2-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="234c2-116">ForceEnglishOutput</span></span> | <span data-ttu-id="234c2-117">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="234c2-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="234c2-118">Genişletme</span><span class="sxs-lookup"><span data-stu-id="234c2-118">Expand</span></span> | <span data-ttu-id="234c2-119">Paket kaynağı eklenen her paketindeki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu.</span><span class="sxs-lookup"><span data-stu-id="234c2-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="234c2-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="234c2-120">Help</span></span> | <span data-ttu-id="234c2-121">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="234c2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="234c2-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="234c2-122">NonInteractive</span></span> | <span data-ttu-id="234c2-123">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="234c2-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="234c2-124">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="234c2-124">Verbosity</span></span> | <span data-ttu-id="234c2-125">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="234c2-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="234c2-126">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="234c2-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="234c2-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="234c2-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
