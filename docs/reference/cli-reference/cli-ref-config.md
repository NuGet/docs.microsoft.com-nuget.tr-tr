---
title: NuGet CLı yapılandırma komutu
description: NuGet. exe yapılandırma komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 51c4c9937483e7f8a57356515c06a60c0f9e6f62
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328359"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="57935-103">config komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="57935-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="57935-104">**Uygulama hedefi:** &bullet; tüm **Desteklenen sürümler**: tümü</span><span class="sxs-lookup"><span data-stu-id="57935-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="57935-105">NuGet yapılandırma değerlerini alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57935-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="57935-106">Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="57935-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="57935-107">İzin verilen anahtar adları hakkında daha fazla bilgi için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="57935-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="57935-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="57935-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="57935-109">Burada `<name>` ve`<value>` yapılandırmada ayarlanacak bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="57935-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="57935-110">İstediğiniz kadar çok çifti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57935-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="57935-111">Bir değeri kaldırmak için, adı ve `=` işareti belirtin ancak değeri belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="57935-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="57935-112">İzin verilen anahtar adları için bkz. [NuGet yapılandırma dosyası başvurusu](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="57935-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="57935-113">NuGet 3.4 + ' `<value>` da [ortam değişkenlerini](cli-ref-environment-variables.md)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="57935-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="57935-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="57935-114">Options</span></span>

| <span data-ttu-id="57935-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="57935-115">Option</span></span> | <span data-ttu-id="57935-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="57935-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57935-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="57935-117">AsPath</span></span> | <span data-ttu-id="57935-118">Yapılandırma değerini bir yol olarak döndürür, kullanıldığında yok sayılır `-Set` .</span><span class="sxs-lookup"><span data-stu-id="57935-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="57935-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="57935-119">ConfigFile</span></span> | <span data-ttu-id="57935-120">Değiştirilecek NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="57935-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="57935-121">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57935-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="57935-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="57935-122">ForceEnglishOutput</span></span> | <span data-ttu-id="57935-123">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="57935-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="57935-124">Help</span><span class="sxs-lookup"><span data-stu-id="57935-124">Help</span></span> | <span data-ttu-id="57935-125">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="57935-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="57935-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="57935-126">NonInteractive</span></span> | <span data-ttu-id="57935-127">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="57935-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="57935-128">Verbosity</span><span class="sxs-lookup"><span data-stu-id="57935-128">Verbosity</span></span> | <span data-ttu-id="57935-129">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="57935-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="57935-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="57935-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="57935-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="57935-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
