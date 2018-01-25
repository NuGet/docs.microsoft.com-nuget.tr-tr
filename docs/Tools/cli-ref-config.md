---
title: NuGet CLI config komutunu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe yapılandırma komut başvurusu"
keywords: "nuget config başvuru, config komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 31abc5c1ade0aff9a2f23ec89ec7082acedb3653
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="930bd-104">config komutunu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="930bd-104">config command (NuGet CLI)</span></span>

<span data-ttu-id="930bd-105">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="930bd-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="930bd-106">Alır veya NuGet yapılandırma değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="930bd-106">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="930bd-107">Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="930bd-107">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="930bd-108">İzin verilen anahtar adları hakkında daha fazla bilgi için başvurmak [NuGet yapılandırma dosyası başvurusu](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="930bd-108">For details on allowable key names, refer to the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="930bd-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="930bd-109">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="930bd-110">Burada `<name>` ve `<value>` yapılandırmada ayarlamak için bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="930bd-110">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="930bd-111">Sayıda çiftleri istendiği gibi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="930bd-111">You can specify as many pairs as desired.</span></span> <span data-ttu-id="930bd-112">Bir değer kaldırmak için ad belirtin ve `=` oturum ancak hiçbir değer.</span><span class="sxs-lookup"><span data-stu-id="930bd-112">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="930bd-113">İzin verilen anahtar adları için bkz: [NuGet yapılandırma dosyası başvurusu](../Schema/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="930bd-113">For allowable key names, see the [NuGet config file reference](../Schema/nuget-config-file.md).</span></span>

<span data-ttu-id="930bd-114">NuGet 3.4 + içinde `<value>` kullanabilirsiniz [ortam değişkenleri](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="930bd-114">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="930bd-115">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="930bd-115">Options</span></span>

| <span data-ttu-id="930bd-116">Seçenek</span><span class="sxs-lookup"><span data-stu-id="930bd-116">Option</span></span> | <span data-ttu-id="930bd-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="930bd-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="930bd-118">AsPath</span><span class="sxs-lookup"><span data-stu-id="930bd-118">AsPath</span></span> | <span data-ttu-id="930bd-119">Yapılandırma değeri bir yolu olarak döndürür yoksayıldı `-Set` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="930bd-119">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="930bd-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="930bd-120">ConfigFile</span></span> | <span data-ttu-id="930bd-121">Değiştirmek için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="930bd-121">The NuGet configuration file to modify.</span></span> <span data-ttu-id="930bd-122">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="930bd-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="930bd-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="930bd-123">ForceEnglishOutput</span></span> | <span data-ttu-id="930bd-124">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="930bd-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="930bd-125">Yardım</span><span class="sxs-lookup"><span data-stu-id="930bd-125">Help</span></span> | <span data-ttu-id="930bd-126">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="930bd-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="930bd-127">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="930bd-127">NonInteractive</span></span> | <span data-ttu-id="930bd-128">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="930bd-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="930bd-129">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="930bd-129">Verbosity</span></span> | <span data-ttu-id="930bd-130">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="930bd-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="930bd-131">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="930bd-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="930bd-132">Örnekler</span><span class="sxs-lookup"><span data-stu-id="930bd-132">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
