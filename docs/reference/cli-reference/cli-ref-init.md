---
title: NuGet CLı init komutu
description: nuget.exe Init komutu başvurusu
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f37572624cea744ce60a9a2e58ad3cbe2696cb9e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780075"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="7034f-103">init komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="7034f-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="7034f-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="7034f-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="7034f-105">Bir düz klasörden tüm paketleri, [Add komutunda](cli-ref-add.md)açıklandığı gibi hiyerarşik bir düzen kullanarak bir hedef klasöre kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7034f-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="7034f-106">Diğer bir deyişle, bu, `init` `add` klasöründeki her pakette komutunu kullanmakla eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="7034f-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="7034f-107">İle olduğu gibi `add` , hedef yerel bir klasör ya da bır UNC yolu olmalıdır; Nuget.org veya özel sunucular gibi HTTP paket depoları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="7034f-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="7034f-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7034f-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="7034f-109">, `<source>` paketleri içeren klasördür ve `<destination>` paketlerin kopyalandığı yerel klasör veya UNC yol adı olur.</span><span class="sxs-lookup"><span data-stu-id="7034f-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="7034f-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="7034f-110">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="7034f-111">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="7034f-111">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7034f-112">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7034f-112">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="7034f-113">Paket kaynağına eklenen her pakette bulunan tüm dosyaları ekler; komutuyla aynı `-Expand` `add` .</span><span class="sxs-lookup"><span data-stu-id="7034f-113">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="7034f-114">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="7034f-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="7034f-115">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7034f-115">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="7034f-116">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="7034f-116">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="7034f-117">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="7034f-117">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="7034f-118">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7034f-118">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7034f-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7034f-119">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
