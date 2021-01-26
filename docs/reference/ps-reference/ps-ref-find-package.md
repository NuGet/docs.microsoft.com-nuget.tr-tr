---
title: NuGet Find-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Find-Package PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777512"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="eea6c-103">Find-Package (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="eea6c-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="eea6c-104">*Sürüm 3.0 +; Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Find-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="eea6c-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="eea6c-105">Belirtilen KIMLIĞE veya anahtar sözcüklere sahip uzak paket kümesini paket kaynağından alır.</span><span class="sxs-lookup"><span data-stu-id="eea6c-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="eea6c-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="eea6c-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="eea6c-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eea6c-107">Parameters</span></span>

| <span data-ttu-id="eea6c-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="eea6c-108">Parameter</span></span> | <span data-ttu-id="eea6c-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eea6c-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eea6c-110">Kimlik &lt; anahtar sözcükleri&gt;</span><span class="sxs-lookup"><span data-stu-id="eea6c-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="eea6c-111">Istenir Paket kaynağı aranırken kullanılacak anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="eea6c-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="eea6c-112">Yalnızca paket KIMLIĞI anahtar sözcüklerle eşleşen paketleri döndürmek için-ExactMatch kullanın.</span><span class="sxs-lookup"><span data-stu-id="eea6c-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="eea6c-113">Hiçbir anahtar sözcük verilmezse, `Find-Package` indirmelere göre ilk 20 paketin bir listesini ya da önce tarafından belirtilen sayıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="eea6c-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="eea6c-114">Kimliğin isteğe bağlı olduğunu ve bir op olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eea6c-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="eea6c-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="eea6c-115">Source</span></span> | <span data-ttu-id="eea6c-116">Aranacak paket kaynağının URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="eea6c-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="eea6c-117">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="eea6c-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="eea6c-118">Atlanırsa, `Find-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="eea6c-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="eea6c-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="eea6c-119">AllVersions</span></span> | <span data-ttu-id="eea6c-120">Her bir paketin yalnızca en son sürümü yerine tüm kullanılabilir sürümlerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eea6c-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="eea6c-121">Birinci</span><span class="sxs-lookup"><span data-stu-id="eea6c-121">First</span></span> | <span data-ttu-id="eea6c-122">Listenin başından döndürülecek paket sayısı; Varsayılan değer 20 ' dir.</span><span class="sxs-lookup"><span data-stu-id="eea6c-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="eea6c-123">Atla</span><span class="sxs-lookup"><span data-stu-id="eea6c-123">Skip</span></span> | <span data-ttu-id="eea6c-124">&lt;Görüntülenmiş listedeki ilk int &gt; paketleri atlar.</span><span class="sxs-lookup"><span data-stu-id="eea6c-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="eea6c-125">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="eea6c-125">IncludePrerelease</span></span> | <span data-ttu-id="eea6c-126">Sonuçlarda yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="eea6c-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="eea6c-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="eea6c-127">ExactMatch</span></span> | <span data-ttu-id="eea6c-128">&lt;Anahtar sözcükleri, &gt; büyük/küçük harfe duyarlı BIR paket kimliği olarak kullanmak için belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eea6c-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="eea6c-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="eea6c-129">StartWith</span></span> | <span data-ttu-id="eea6c-130">Paket KIMLIĞI anahtar sözcüklerle başlayan paketleri döndürür &lt; &gt; .</span><span class="sxs-lookup"><span data-stu-id="eea6c-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="eea6c-131">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="eea6c-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="eea6c-132">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="eea6c-132">Common Parameters</span></span>

<span data-ttu-id="eea6c-133">`Find-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="eea6c-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="eea6c-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="eea6c-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```