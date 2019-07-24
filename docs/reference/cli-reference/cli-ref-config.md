---
title: NuGet CLı yapılandırma komutu
description: NuGet. exe yapılandırma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433314"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="bd584-103">config komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="bd584-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="bd584-104">**Uygulama hedefi:** &bullet; tüm **Desteklenen sürümler**: tümü</span><span class="sxs-lookup"><span data-stu-id="bd584-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="bd584-105">NuGet yapılandırma değerlerini alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bd584-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="bd584-106">Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="bd584-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="bd584-107">İzin verilen anahtar adları hakkında daha fazla bilgi için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="bd584-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="bd584-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bd584-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="bd584-109">Burada `<name>` ve`<value>` yapılandırmada ayarlanacak bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="bd584-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="bd584-110">İstediğiniz kadar çok çifti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd584-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="bd584-111">Bir değeri kaldırmak için, adı ve `=` işareti belirtin ancak değeri belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="bd584-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="bd584-112">İzin verilen anahtar adları için bkz. [NuGet yapılandırma dosyası başvurusu](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="bd584-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="bd584-113">NuGet 3.4 + ' `<value>` da [ortam değişkenlerini](cli-ref-environment-variables.md)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="bd584-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="bd584-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="bd584-114">Options</span></span>

| <span data-ttu-id="bd584-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="bd584-115">Option</span></span> | <span data-ttu-id="bd584-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bd584-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bd584-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="bd584-117">AsPath</span></span> | <span data-ttu-id="bd584-118">Yapılandırma değerini bir yol olarak döndürür, kullanıldığında yok sayılır `-Set` .</span><span class="sxs-lookup"><span data-stu-id="bd584-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="bd584-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bd584-119">ConfigFile</span></span> | <span data-ttu-id="bd584-120">Değiştirilecek NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="bd584-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="bd584-121">Belirtilmemişse, varsayılan dosya kullanılır-`%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.config/NuGet/NuGet.Config` (Mac/Linux) veya `~/.nuget/NuGet/NuGet.Config` (OS dağıtımına göre değişir).</span><span class="sxs-lookup"><span data-stu-id="bd584-121">If not specified, the default file is used -`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.config/NuGet/NuGet.Config`  (Mac/Linux) or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution).</span></span>|
| <span data-ttu-id="bd584-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bd584-122">ForceEnglishOutput</span></span> | <span data-ttu-id="bd584-123">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="bd584-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bd584-124">Help</span><span class="sxs-lookup"><span data-stu-id="bd584-124">Help</span></span> | <span data-ttu-id="bd584-125">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bd584-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="bd584-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bd584-126">NonInteractive</span></span> | <span data-ttu-id="bd584-127">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="bd584-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bd584-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="bd584-128">Verbosity</span></span> | <span data-ttu-id="bd584-129">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="bd584-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bd584-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bd584-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="bd584-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bd584-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
