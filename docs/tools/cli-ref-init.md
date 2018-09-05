---
title: NuGet CLI init komutunu
description: Nuget.exe init komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551416"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="7b7c5-103">init komutunu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7b7c5-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="7b7c5-104">**İçin geçerlidir:** paket oluşturma &bullet; **desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7b7c5-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7b7c5-105">Tüm paketler için açıklandığı gibi bir hiyerarşik yerleşim kullanarak bir hedef klasöre kopyalama yapan düz bir klasörden [Ekle komutu](cli-ref-add.md).</span><span class="sxs-lookup"><span data-stu-id="7b7c5-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="7b7c5-106">Diğer bir deyişle, kullanarak `init` kullanmakla eşdeğerdir `add` klasöründeki her paket komutu.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="7b7c5-107">Olduğu gibi `add`, hedef, yerel bir klasöre ya da bir UNC yolu; olmalıdır. Nuget.org veya özel sunucuları gibi HTTP paketinin depoları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="7b7c5-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7b7c5-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="7b7c5-109">Burada `<source>` paketleri içeren klasör ve `<destination>` yerel klasör veya UNC pathname paketler kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="7b7c5-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="7b7c5-110">Options</span></span>

| <span data-ttu-id="7b7c5-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="7b7c5-111">Option</span></span> | <span data-ttu-id="7b7c5-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7b7c5-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b7c5-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7b7c5-113">ConfigFile</span></span> | <span data-ttu-id="7b7c5-114">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7b7c5-115">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7b7c5-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7b7c5-116">ForceEnglishOutput</span></span> | <span data-ttu-id="7b7c5-117">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7b7c5-118">Genişletin</span><span class="sxs-lookup"><span data-stu-id="7b7c5-118">Expand</span></span> | <span data-ttu-id="7b7c5-119">Paket kaynağı için eklenen her paketteki tüm dosyaları ekler; aynı `-Expand` ile `add` komutu.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="7b7c5-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="7b7c5-120">Help</span></span> | <span data-ttu-id="7b7c5-121">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="7b7c5-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7b7c5-122">NonInteractive</span></span> | <span data-ttu-id="7b7c5-123">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7b7c5-124">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="7b7c5-124">Verbosity</span></span> | <span data-ttu-id="7b7c5-125">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="7b7c5-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7b7c5-126">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7b7c5-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7b7c5-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7b7c5-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
