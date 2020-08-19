---
title: NuGet CLı Yereller komutu
description: nuget.exe Yereller komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: cdc2b760021ffc4a9e02edacb45beac01cc99bf1
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623064"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="10cd8-103">Yereller komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="10cd8-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="10cd8-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="10cd8-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="10cd8-105">*Http önbelleği*, *genel paketler* klasörü ve temp klasörü gibi yerel NuGet kaynaklarını temizler veya listeler.</span><span class="sxs-lookup"><span data-stu-id="10cd8-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="10cd8-106">`locals`Komut ayrıca bu konumların bir listesini göstermek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="10cd8-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="10cd8-107">Daha fazla bilgi için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="10cd8-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="10cd8-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="10cd8-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="10cd8-109">Burada `<folder>` `all` ,, `http-cache` , `packages-cache` *(3,5 ve öncesi)*, `global-packages` , `temp` *(3.4 +)* ve `plugins-cache` *(4.8 +)*' den biridir.</span><span class="sxs-lookup"><span data-stu-id="10cd8-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="10cd8-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="10cd8-110">Options</span></span>

- **`-Clear`**

  <span data-ttu-id="10cd8-111">Belirtilen klasörü temizler.</span><span class="sxs-lookup"><span data-stu-id="10cd8-111">Clears the specified folder.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="10cd8-112">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="10cd8-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="10cd8-113">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="10cd8-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="10cd8-114">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="10cd8-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="10cd8-115">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="10cd8-115">Displays help information for the command.</span></span>

- **`-List`**

  <span data-ttu-id="10cd8-116">Belirtilen klasörün konumunu veya tüm klasörlerin konumlarını, *Tümü*ile birlikte kullanıldığında listeler.</span><span class="sxs-lookup"><span data-stu-id="10cd8-116">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="10cd8-117">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="10cd8-117">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="10cd8-118">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="10cd8-118">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="10cd8-119">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="10cd8-119">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="10cd8-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="10cd8-120">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="10cd8-121">Daha fazla örnek için bkz. [genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="10cd8-121">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
