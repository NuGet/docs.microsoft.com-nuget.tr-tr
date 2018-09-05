---
title: NuGet Register-TabExpansion PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu kayıt TabExpansion PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546611"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="a470b-103">Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="a470b-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a470b-104">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="a470b-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a470b-105">Belirtilen komut parametreleri için bir sekme genişletmeyi sekmesini komutu girerken kullanıldığında, söz konusu parametresi için kullanılabilir seçenekler olarak genişletilmiş değerlerin göründüğü şekilde kaydeder.</span><span class="sxs-lookup"><span data-stu-id="a470b-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="a470b-106">Komut için önceki tüm genişletmeleri üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="a470b-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="a470b-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a470b-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a470b-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="a470b-108">Parameters</span></span>

| <span data-ttu-id="a470b-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="a470b-109">Parameter</span></span> | <span data-ttu-id="a470b-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a470b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a470b-111">Ad</span><span class="sxs-lookup"><span data-stu-id="a470b-111">Name</span></span> | <span data-ttu-id="a470b-112">(Gerekli) Hangi genişletmeleri kaydetmek komutu.</span><span class="sxs-lookup"><span data-stu-id="a470b-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="a470b-113">-Name anahtarın kendisinde, isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a470b-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="a470b-114">Tanım</span><span class="sxs-lookup"><span data-stu-id="a470b-114">Definition</span></span> | <span data-ttu-id="a470b-115">(Gerekli) Bağımsız değişken söz diziminde açıklayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` burada `<parameter>` değiştirmek için parametre ve her adıdır `<value>` belirli bir genişletme sağlar.</span><span class="sxs-lookup"><span data-stu-id="a470b-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="a470b-116">Tek ve çift tırnak işaretleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a470b-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="a470b-117">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="a470b-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a470b-118">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="a470b-118">Common Parameters</span></span>

<span data-ttu-id="a470b-119">`Register-TabExpansion` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="a470b-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a470b-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a470b-120">Examples</span></span>

<span data-ttu-id="a470b-121">Üç projeleri adları EventManager ve yardımcı programları SpecialParser içeren bir çözümü göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="a470b-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="a470b-122">Geliştirici sık kullandığı `Update-Package` ile bu projelerin her biri farklı zamanlarda komutu.</span><span class="sxs-lookup"><span data-stu-id="a470b-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="a470b-123">Kendisi kullanışlı bulur `Update-Package` komut sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` her zaman bir proje adı yazabileceğiniz geliştirmiyor bu yüzden bağımsız değişken.</span><span class="sxs-lookup"><span data-stu-id="a470b-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="a470b-124">Aşağıdaki komutu, bu üç proje adları için bir genişletme olarak daha sonra kaydeder `-ProjectName` parametresi:</span><span class="sxs-lookup"><span data-stu-id="a470b-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="a470b-125">Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve Otomatik Tamamlama seçeneği olarak sunulan genişletmeleri bakın:</span><span class="sxs-lookup"><span data-stu-id="a470b-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
