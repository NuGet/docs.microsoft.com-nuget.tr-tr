---
title: NuGet Register-TabExpansion PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Register-TabExpansion PowerShell komut başvurusu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 02f6d4ecd246b7ce5425cf56ade10789cf03113c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="bccb3-103">Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="bccb3-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bccb3-104">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="bccb3-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="bccb3-105">Sekme komutu girerken kullanıldığında genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekleri görünür olacağı şekilde bir sekme genişlemesi parametreler için belirtilen komut kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bccb3-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="bccb3-106">Komutu için önceki tüm genişletmeleri üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="bccb3-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="bccb3-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="bccb3-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="bccb3-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="bccb3-108">Parameters</span></span>

| <span data-ttu-id="bccb3-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="bccb3-109">Parameter</span></span> | <span data-ttu-id="bccb3-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bccb3-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bccb3-111">Ad</span><span class="sxs-lookup"><span data-stu-id="bccb3-111">Name</span></span> | <span data-ttu-id="bccb3-112">(Gerekli) Hangi genişletmeleri kaydetmek komutu.</span><span class="sxs-lookup"><span data-stu-id="bccb3-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="bccb3-113">-Name anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="bccb3-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="bccb3-114">Tanım</span><span class="sxs-lookup"><span data-stu-id="bccb3-114">Definition</span></span> | <span data-ttu-id="bccb3-115">(Gerekli) Sözdizimi değişkeninde açıklayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` nerede `<parameter>` değiştirmek için parametre ve her adıdır `<value>` belirli bir genişletme sağlar.</span><span class="sxs-lookup"><span data-stu-id="bccb3-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="bccb3-116">Tek ve çift tırnak işaretleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="bccb3-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="bccb3-117">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="bccb3-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bccb3-118">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="bccb3-118">Common Parameters</span></span>

<span data-ttu-id="bccb3-119">`Register-TabExpansion` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bccb3-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bccb3-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bccb3-120">Examples</span></span>

<span data-ttu-id="bccb3-121">Üç projeleri adları EventManager, yardımcı programlar ve SpecialParser içeren bir çözüm göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="bccb3-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="bccb3-122">Geliştirici sık kullandığı `Update-Package` bu projelerin her biri ile farklı zamanlarda komutu.</span><span class="sxs-lookup"><span data-stu-id="bccb3-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="bccb3-123">Kendisi kullanışlı bulur `Update-Package` komutu sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` kendisi her zaman bir proje adı yazın gerekmez şekilde bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="bccb3-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="bccb3-124">Aşağıdaki komutu için bir genişletme bu üç proje adları daha sonra kaydeder `-ProjectName` parametre:</span><span class="sxs-lookup"><span data-stu-id="bccb3-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="bccb3-125">Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve otomatik tamamlama seçenekleri olarak sunulan genişletmeler bakın:</span><span class="sxs-lookup"><span data-stu-id="bccb3-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
