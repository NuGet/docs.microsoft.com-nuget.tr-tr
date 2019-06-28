---
title: NuGet CLI config komutu
description: Nuget.exe config komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426068"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="645ea-103">config komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="645ea-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="645ea-104">**İçin geçerlidir:** tüm &bullet; **desteklenen sürümler**: tüm</span><span class="sxs-lookup"><span data-stu-id="645ea-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="645ea-105">Alır veya NuGet yapılandırma değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="645ea-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="645ea-106">Ek kullanım için bkz: [ortak NuGet yapılandırmaları](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="645ea-106">For additional usage, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="645ea-107">İzin verilen anahtar adları hakkında daha fazla bilgi için başvurmak [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="645ea-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="645ea-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="645ea-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="645ea-109">Burada `<name>` ve `<value>` yapılandırmada ayarlamak için bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="645ea-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="645ea-110">İstediğiniz gibi çok çiftleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="645ea-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="645ea-111">Bir değer kaldırmak için adını belirtin ve `=` oturum ancak herhangi bir değer.</span><span class="sxs-lookup"><span data-stu-id="645ea-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="645ea-112">İzin verilen anahtar adları için bkz [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="645ea-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="645ea-113">NuGet 3.4 + içinde `<value>` kullanabilirsiniz [ortam değişkenlerini](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="645ea-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="645ea-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="645ea-114">Options</span></span>

| <span data-ttu-id="645ea-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="645ea-115">Option</span></span> | <span data-ttu-id="645ea-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="645ea-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="645ea-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="645ea-117">AsPath</span></span> | <span data-ttu-id="645ea-118">Yapılandırma değeri bir yolu olarak döndürür yoksayıldı `-Set` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="645ea-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="645ea-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="645ea-119">ConfigFile</span></span> | <span data-ttu-id="645ea-120">Değiştirmek için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="645ea-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="645ea-121">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="645ea-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="645ea-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="645ea-122">ForceEnglishOutput</span></span> | <span data-ttu-id="645ea-123">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="645ea-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="645ea-124">Help</span><span class="sxs-lookup"><span data-stu-id="645ea-124">Help</span></span> | <span data-ttu-id="645ea-125">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="645ea-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="645ea-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="645ea-126">NonInteractive</span></span> | <span data-ttu-id="645ea-127">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="645ea-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="645ea-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="645ea-128">Verbosity</span></span> | <span data-ttu-id="645ea-129">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="645ea-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="645ea-130">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="645ea-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="645ea-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="645ea-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
