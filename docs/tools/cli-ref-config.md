---
title: NuGet CLI config komutu
description: Nuget.exe yapılandırma komut başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818171"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="00f6a-103">config komutunu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="00f6a-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="00f6a-104">**Uygulandığı öğe:** tüm &bullet; **desteklenen sürümleri**: tüm</span><span class="sxs-lookup"><span data-stu-id="00f6a-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="00f6a-105">Alır veya NuGet yapılandırma değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="00f6a-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="00f6a-106">Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="00f6a-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="00f6a-107">İzin verilen anahtar adları hakkında daha fazla bilgi için başvurmak [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="00f6a-107">For details on allowable key names, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="00f6a-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="00f6a-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="00f6a-109">Burada `<name>` ve `<value>` yapılandırmada ayarlamak için bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="00f6a-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="00f6a-110">Sayıda çiftleri istendiği gibi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00f6a-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="00f6a-111">Bir değer kaldırmak için ad belirtin ve `=` oturum ancak hiçbir değer.</span><span class="sxs-lookup"><span data-stu-id="00f6a-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="00f6a-112">İzin verilen anahtar adları için bkz: [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="00f6a-112">For allowable key names, see the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

<span data-ttu-id="00f6a-113">NuGet 3.4 + içinde `<value>` kullanabilirsiniz [ortam değişkenleri](cli-ref-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="00f6a-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="00f6a-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="00f6a-114">Options</span></span>

| <span data-ttu-id="00f6a-115">Seçenek</span><span class="sxs-lookup"><span data-stu-id="00f6a-115">Option</span></span> | <span data-ttu-id="00f6a-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="00f6a-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="00f6a-117">AsPath</span><span class="sxs-lookup"><span data-stu-id="00f6a-117">AsPath</span></span> | <span data-ttu-id="00f6a-118">Yapılandırma değeri bir yolu olarak döndürür yoksayıldı `-Set` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="00f6a-118">Returns the config value as a path, ignored when `-Set` is used.</span></span> |
| <span data-ttu-id="00f6a-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="00f6a-119">ConfigFile</span></span> | <span data-ttu-id="00f6a-120">Değiştirmek için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="00f6a-120">The NuGet configuration file to modify.</span></span> <span data-ttu-id="00f6a-121">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="00f6a-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="00f6a-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="00f6a-122">ForceEnglishOutput</span></span> | <span data-ttu-id="00f6a-123">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="00f6a-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="00f6a-124">Yardım</span><span class="sxs-lookup"><span data-stu-id="00f6a-124">Help</span></span> | <span data-ttu-id="00f6a-125">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="00f6a-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="00f6a-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="00f6a-126">NonInteractive</span></span> | <span data-ttu-id="00f6a-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="00f6a-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="00f6a-128">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="00f6a-128">Verbosity</span></span> | <span data-ttu-id="00f6a-129">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="00f6a-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="00f6a-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="00f6a-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="00f6a-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="00f6a-131">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
