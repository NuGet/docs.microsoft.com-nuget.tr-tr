---
title: NuGet CLI config komutu
description: Nuget.exe yapılandırma komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 414eb8386f949347772f33170de881534dc71482
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="825ed-103">config komutunu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="825ed-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="825ed-104">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="825ed-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="825ed-105">Alır veya NuGet yapılandırma değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="825ed-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="825ed-106">Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="825ed-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="825ed-107">İzin verilen anahtar adları hakkında daha fazla bilgi için başvurmak [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="825ed-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="825ed-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="825ed-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="825ed-109">Burada `<name>` ve `<value>` yapılandırmada ayarlamak için bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="825ed-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="825ed-110">Sayıda çiftleri istendiği gibi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="825ed-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="825ed-111">Bir değer kaldırmak için ad belirtin ve `=` oturum ancak hiçbir değer.</span><span class="sxs-lookup"><span data-stu-id="825ed-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="825ed-112">İzin verilen anahtar adları için bkz: [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="825ed-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="825ed-113">NuGet 3.4 + içinde `<value>` kullanabilirsiniz [ortam değişkenleri](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="825ed-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="825ed-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="825ed-114">Options</span></span>

| <span data-ttu-id="825ed-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="825ed-115">Option</span></span> | <span data-ttu-id="825ed-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="825ed-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="825ed-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="825ed-117">AsPath</span></span> | <span data-ttu-id="825ed-118">Yapılandırma değeri bir yolu olarak döndürür yoksayıldı `-Set` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="825ed-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="825ed-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="825ed-119">ConfigFile</span></span> | <span data-ttu-id="825ed-120">Değiştirmek için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="825ed-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="825ed-121">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="825ed-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="825ed-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="825ed-122">ForceEnglishOutput</span></span> | <span data-ttu-id="825ed-123">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="825ed-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="825ed-124">Yardım</span><span class="sxs-lookup"><span data-stu-id="825ed-124">Help</span></span> | <span data-ttu-id="825ed-125">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="825ed-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="825ed-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="825ed-126">NonInteractive</span></span> | <span data-ttu-id="825ed-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="825ed-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="825ed-128">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="825ed-128">Verbosity</span></span> | <span data-ttu-id="825ed-129">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="825ed-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="825ed-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="825ed-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="825ed-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="825ed-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
