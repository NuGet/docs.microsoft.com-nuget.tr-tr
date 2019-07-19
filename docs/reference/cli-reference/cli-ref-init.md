---
title: NuGet CLı init komutu
description: NuGet. exe init komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328338"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="17ee2-103">init komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="17ee2-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="17ee2-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="17ee2-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="17ee2-105">Bir düz klasörden tüm paketleri, [Add komutunda](cli-ref-add.md)açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre kopyalar.</span><span class="sxs-lookup"><span data-stu-id="17ee2-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="17ee2-106">Diğer bir deyişle, `init` bu, klasöründeki her pakette `add` komutunu kullanmakla eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="17ee2-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="17ee2-107">İle `add`olduğu gibi, hedef yerel bir klasör ya da bir UNC yolu olmalıdır; Nuget.org veya özel sunucular gibi HTTP paket depoları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="17ee2-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="17ee2-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="17ee2-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="17ee2-109">, paketleri içeren klasördür ve `<destination>` paketlerin kopyalandığı yerel klasör veya UNC yol adı olur. `<source>`</span><span class="sxs-lookup"><span data-stu-id="17ee2-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="17ee2-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="17ee2-110">Options</span></span>

| <span data-ttu-id="17ee2-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="17ee2-111">Option</span></span> | <span data-ttu-id="17ee2-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="17ee2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17ee2-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="17ee2-113">ConfigFile</span></span> | <span data-ttu-id="17ee2-114">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="17ee2-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="17ee2-115">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="17ee2-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="17ee2-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="17ee2-116">ForceEnglishOutput</span></span> | <span data-ttu-id="17ee2-117">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="17ee2-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="17ee2-118">Expand</span><span class="sxs-lookup"><span data-stu-id="17ee2-118">Expand</span></span> | <span data-ttu-id="17ee2-119">Paket kaynağına eklenen her pakette bulunan tüm dosyaları ekler; `-Expand` komutuyla aynı`add` .</span><span class="sxs-lookup"><span data-stu-id="17ee2-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="17ee2-120">Help</span><span class="sxs-lookup"><span data-stu-id="17ee2-120">Help</span></span> | <span data-ttu-id="17ee2-121">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="17ee2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="17ee2-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="17ee2-122">NonInteractive</span></span> | <span data-ttu-id="17ee2-123">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="17ee2-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="17ee2-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="17ee2-124">Verbosity</span></span> | <span data-ttu-id="17ee2-125">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="17ee2-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="17ee2-126">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="17ee2-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="17ee2-127">Örnekler</span><span class="sxs-lookup"><span data-stu-id="17ee2-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
