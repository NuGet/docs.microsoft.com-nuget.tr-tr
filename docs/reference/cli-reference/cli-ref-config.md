---
title: NuGet CLı yapılandırma komutu
description: nuget.exe config komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622882"
---
# <a name="config-command-nuget-cli"></a><span data-ttu-id="ec1b3-103">config komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="ec1b3-103">config command (NuGet CLI)</span></span>

<span data-ttu-id="ec1b3-104">**Uygulama hedefi:** tüm &bullet; **Desteklenen sürümler**: tümü</span><span class="sxs-lookup"><span data-stu-id="ec1b3-104">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="ec1b3-105">NuGet yapılandırma değerlerini alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-105">Gets or sets NuGet configuration values.</span></span> <span data-ttu-id="ec1b3-106">Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ec1b3-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="ec1b3-107">İzin verilen anahtar adları hakkında daha fazla bilgi için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-107">For details on allowable key names, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ec1b3-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ec1b3-108">Usage</span></span>

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

<span data-ttu-id="ec1b3-109">Burada `<name>` ve `<value>` yapılandırmada ayarlanacak bir anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-109">where `<name>` and `<value>` specify a key-value pair to be set in the configuration.</span></span> <span data-ttu-id="ec1b3-110">İstediğiniz kadar çok çifti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-110">You can specify as many pairs as desired.</span></span> <span data-ttu-id="ec1b3-111">Bir değeri kaldırmak için, adı ve `=` işareti belirtin ancak değeri belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-111">To remove a value, specify the name and the `=` sign but no value.</span></span>

<span data-ttu-id="ec1b3-112">İzin verilen anahtar adları için bkz. [NuGet yapılandırma dosyası başvurusu](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="ec1b3-112">For allowable key names, see the [NuGet config file reference](../nuget-config-file.md).</span></span>

<span data-ttu-id="ec1b3-113">NuGet 3.4 + ' da `<value>` [ortam değişkenlerini](cli-ref-environment-variables.md)kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-113">In NuGet 3.4+, `<value>` can use [environment variables](cli-ref-environment-variables.md).</span></span>

## <a name="options"></a><span data-ttu-id="ec1b3-114">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ec1b3-114">Options</span></span>


- **`AsPath`**

  <span data-ttu-id="ec1b3-115">Yapılandırma değerini bir yol olarak döndürür, kullanıldığında yok sayılır `-Set` .</span><span class="sxs-lookup"><span data-stu-id="ec1b3-115">Returns the config value as a path, ignored when `-Set` is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ec1b3-116">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec1b3-117">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ec1b3-118">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ec1b3-119">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ec1b3-120">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-Set`**

  <span data-ttu-id="ec1b3-121">Yapılandırma içinde ayarlanacak daha fazla anahtar-değer çiftinden biridir.</span><span class="sxs-lookup"><span data-stu-id="ec1b3-121">One on more key-value pairs to be set in config.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ec1b3-122">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ec1b3-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="ec1b3-123">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec1b3-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

### <a name="examples"></a><span data-ttu-id="ec1b3-124">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ec1b3-124">Examples</span></span>

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
