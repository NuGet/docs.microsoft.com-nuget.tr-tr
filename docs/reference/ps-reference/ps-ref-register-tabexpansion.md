---
title: NuGet Register-Tabgenişleme PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Register-Tabgenişleme PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384460"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="1b666-103">Register-Tabgenişleme (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="1b666-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1b666-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="1b666-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1b666-105">Belirtilen komutun parametreleri için bir sekme genişletmesi kaydeder, örneğin bir komut girerken Tab kullanıldığında, genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekler olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="1b666-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="1b666-106">Komutun önceki genişletmeleri üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="1b666-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="1b666-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1b666-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1b666-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1b666-108">Parameters</span></span>

| <span data-ttu-id="1b666-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="1b666-109">Parameter</span></span> | <span data-ttu-id="1b666-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1b666-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b666-111">Name</span><span class="sxs-lookup"><span data-stu-id="1b666-111">Name</span></span> | <span data-ttu-id="1b666-112">Istenir Expansions 'in kaydedileceği komut.</span><span class="sxs-lookup"><span data-stu-id="1b666-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="1b666-113">-Name anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1b666-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="1b666-114">Tanım</span><span class="sxs-lookup"><span data-stu-id="1b666-114">Definition</span></span> | <span data-ttu-id="1b666-115">Istenir Söz diziminde bağımsız değişkeni tanımlayan bir nesne, `<parameter>` değiştirilecek parametrenin adı `@{'<parameter>' = {'<value1>', '<value2>', ...}}` ve her `<value>` belirli bir genişletme sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b666-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="1b666-116">Hem tek hem de çift tırnak işareti kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="1b666-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="1b666-117">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="1b666-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1b666-118">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="1b666-118">Common Parameters</span></span>

<span data-ttu-id="1b666-119">`Register-TabExpansion`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1b666-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1b666-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1b666-120">Examples</span></span>

<span data-ttu-id="1b666-121">EventManager, yardımcı programlar ve SpecialParser olmak üzere üç proje adı içeren bir çözüm düşünün.</span><span class="sxs-lookup"><span data-stu-id="1b666-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="1b666-122">Geliştirici genellikle `Update-Package` komutunu bu projelerin her biriyle farklı zamanlarda kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b666-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="1b666-123">`Update-Package` komutunun, `-ProjectName` bağımsız değişkeni için otomatik tamamlama genişletmeleri sağlamasına uygun olduğunu tespit eder; böylece her seferinde bir proje adı yazmak zorunda kalmaz.</span><span class="sxs-lookup"><span data-stu-id="1b666-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="1b666-124">Aşağıdaki komut, bu üç proje adını `-ProjectName` parametresi için bir genişletme olarak kaydeder:</span><span class="sxs-lookup"><span data-stu-id="1b666-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="1b666-125">Geliştirici daha sonra `Update-Package -ProjectName `yazabilir, sekme tuşuna basabilir ve otomatik tamamlama seçenekleri olarak sunulan genişletmeleri görebilirler:</span><span class="sxs-lookup"><span data-stu-id="1b666-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register-Tabgenişletmesini kullanma örneği](media/Register-TabExpansion-Example.png)
