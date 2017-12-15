---
title: "NuGet Register-TabExpansion PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 8314ec69-ee8c-4933-84ef-e6d8a412d268
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Register-TabExpansion PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Register-TabExpansion"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 498b8638c81b800e5f20f7604b36e6af76da0283
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="6915b-104">Register-TabExpansion (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="6915b-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6915b-105">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="6915b-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="6915b-106">Sekme komutu girerken kullanıldığında genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekleri görünür olacağı şekilde bir sekme genişlemesi parametreler için belirtilen komut kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6915b-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="6915b-107">Komutu için önceki tüm genişletmeleri üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="6915b-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="6915b-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6915b-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="6915b-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="6915b-109">Parameters</span></span>

| <span data-ttu-id="6915b-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="6915b-110">Parameter</span></span> | <span data-ttu-id="6915b-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6915b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6915b-112">Ad</span><span class="sxs-lookup"><span data-stu-id="6915b-112">Name</span></span> | <span data-ttu-id="6915b-113">(Gerekli) Hangi genişletmeleri kaydetmek komutu.</span><span class="sxs-lookup"><span data-stu-id="6915b-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="6915b-114">-Name anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="6915b-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="6915b-115">Tanım</span><span class="sxs-lookup"><span data-stu-id="6915b-115">Definition</span></span> | <span data-ttu-id="6915b-116">(Gerekli) Sözdizimi değişkeninde açıklayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` nerede `<parameter>` değiştirmek için parametre ve her adıdır `<value>` belirli bir genişletme sağlar.</span><span class="sxs-lookup"><span data-stu-id="6915b-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="6915b-117">Tek ve çift tırnak işaretleri kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="6915b-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="6915b-118">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="6915b-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6915b-119">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="6915b-119">Common Parameters</span></span>

<span data-ttu-id="6915b-120">`Register-TabExpansion`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="6915b-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6915b-121">Örnekler</span><span class="sxs-lookup"><span data-stu-id="6915b-121">Examples</span></span>

<span data-ttu-id="6915b-122">Üç projeleri adları EventManager, yardımcı programlar ve SpecialParser içeren bir çözüm göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6915b-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="6915b-123">Geliştirici sık kullandığı `Update-Package` bu projelerin her biri ile farklı zamanlarda komutu.</span><span class="sxs-lookup"><span data-stu-id="6915b-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="6915b-124">Kendisi kullanışlı bulur `Update-Package` komutu sağlamak için otomatik tamamlama genişletmeleri `-ProjectName` kendisi her zaman bir proje adı yazın gerekmez şekilde bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="6915b-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="6915b-125">Aşağıdaki komutu için bir genişletme bu üç proje adları daha sonra kaydeder `-ProjectName` parametre:</span><span class="sxs-lookup"><span data-stu-id="6915b-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="6915b-126">Geliştirici ardından yazabilirsiniz `Update-Package -ProjectName `SEKME tuşuna basın ve otomatik tamamlama seçenekleri olarak sunulan genişletmeler bakın:</span><span class="sxs-lookup"><span data-stu-id="6915b-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)
