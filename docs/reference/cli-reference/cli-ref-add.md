---
title: NuGet CLı Add komutu
description: nuget.exe Add komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622908"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="6360a-103">Add komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="6360a-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="6360a-104">**Uygulama hedefi**: paket yayımlaması &bullet; **Desteklenen sürümler**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="6360a-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="6360a-105">, Paket KIMLIĞI ve sürüm numarası için klasörler içinde oluşturulan, bir hiyerarşik düzende, belirtilen bir paketi HTTP olmayan bir kaynak (klasör veya UNC yolu) öğesine ekler.</span><span class="sxs-lookup"><span data-stu-id="6360a-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="6360a-106">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6360a-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="6360a-107">Paket kaynağına göre geri yükleme veya güncelleştirme yaparken hiyerarşik düzen önemli ölçüde daha iyi performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="6360a-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="6360a-108">Paketteki tüm dosyaları hedef paket kaynağına genişletmek için `-Expand` anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="6360a-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="6360a-109">Bu genellikle, ve gibi, hedefte görüntülenen ek alt klasörlere neden olur `tools` `lib` .</span><span class="sxs-lookup"><span data-stu-id="6360a-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="6360a-110">Kullanım</span><span class="sxs-lookup"><span data-stu-id="6360a-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="6360a-111">, `<packagePath>` eklenecek paketin yol adı, ve `<sourcePath>` paketin ekleneceği klasör tabanlı paket kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6360a-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="6360a-112">HTTP kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="6360a-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="6360a-113">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="6360a-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6360a-114">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="6360a-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6360a-115">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6360a-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="6360a-116">Paketteki tüm dosyaları paket kaynağına ekler.</span><span class="sxs-lookup"><span data-stu-id="6360a-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6360a-117">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="6360a-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="6360a-118">nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="6360a-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6360a-119">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6360a-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6360a-120">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="6360a-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="6360a-121">Nupkg 'nin ekleneceği bir klasör veya UNC paylaşma olan paket kaynağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6360a-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="6360a-122">Http kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="6360a-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6360a-123">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6360a-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="6360a-124">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6360a-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6360a-125">Örnekler</span><span class="sxs-lookup"><span data-stu-id="6360a-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
