---
title: NuGet Register-TabExpansion PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Register-TabExpansion PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237159"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="fbfee-103">Register-TabExpansion (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="fbfee-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fbfee-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="fbfee-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fbfee-105">Belirtilen komutun parametreleri için bir sekme genişletmesi kaydeder, örneğin bir komut girerken Tab kullanıldığında, genişletilmiş değerler söz konusu parametre için kullanılabilir seçenekler olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="fbfee-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="fbfee-106">Komutun önceki genişletmeleri üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="fbfee-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="fbfee-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="fbfee-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fbfee-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="fbfee-108">Parameters</span></span>

| <span data-ttu-id="fbfee-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="fbfee-109">Parameter</span></span> | <span data-ttu-id="fbfee-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fbfee-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fbfee-111">Ad</span><span class="sxs-lookup"><span data-stu-id="fbfee-111">Name</span></span> | <span data-ttu-id="fbfee-112">Istenir Expansions 'in kaydedileceği komut.</span><span class="sxs-lookup"><span data-stu-id="fbfee-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="fbfee-113">-Name anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fbfee-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="fbfee-114">Tanım</span><span class="sxs-lookup"><span data-stu-id="fbfee-114">Definition</span></span> | <span data-ttu-id="fbfee-115">Istenir Söz dizimi içindeki bağımsız değişkeni tanımlayan bir nesne `@{'<parameter>' = {'<value1>', '<value2>', ...}}` , `<parameter>` Değiştirilecek parametrenin adı, her biri `<value>` belirli bir genişletme sağlar.</span><span class="sxs-lookup"><span data-stu-id="fbfee-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="fbfee-116">Hem tek hem de çift tırnak işareti kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="fbfee-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="fbfee-117">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="fbfee-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fbfee-118">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="fbfee-118">Common Parameters</span></span>

<span data-ttu-id="fbfee-119">`Register-TabExpansion` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fbfee-119">`Register-TabExpansion` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fbfee-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fbfee-120">Examples</span></span>

<span data-ttu-id="fbfee-121">EventManager, yardımcı programlar ve SpecialParser olmak üzere üç proje adı içeren bir çözüm düşünün.</span><span class="sxs-lookup"><span data-stu-id="fbfee-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="fbfee-122">Geliştirici genellikle `Update-Package` komutu bu projelerin her biriyle farklı zamanlarda kullanır.</span><span class="sxs-lookup"><span data-stu-id="fbfee-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="fbfee-123">`Update-Package`Komutun `-ProjectName` her seferinde bir proje adı yazmasının gerekmemesi için bağımsız değişken için otomatik tamamlama genişletmeleri sağlamasına uygun olduğunu buluyor.</span><span class="sxs-lookup"><span data-stu-id="fbfee-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="fbfee-124">Aşağıdaki komut, bu üç proje adını parametresi için bir genişletme olarak kaydeder `-ProjectName` :</span><span class="sxs-lookup"><span data-stu-id="fbfee-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="fbfee-125">Daha sonra geliştirici yazabilir `Update-Package -ProjectName ` , sekme tuşuna basabilir ve otomatik tamamlama seçenekleri olarak sunulan genişletmeleri görebilirler:</span><span class="sxs-lookup"><span data-stu-id="fbfee-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register-TabExpansion kullanma örneği](media/Register-TabExpansion-Example.png)