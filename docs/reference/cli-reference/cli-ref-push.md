---
title: NuGet CLı Push komutu
description: NuGet. exe Push komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328293"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="3be60-103">Push komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="3be60-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="3be60-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** All; 4.1.0 + NuGet.org için gereklidir</span><span class="sxs-lookup"><span data-stu-id="3be60-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="3be60-105">Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../../api/nuget-protocols.md)uygulayan NuGet. exe v 4.1.0 + kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3be60-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="3be60-106">Paketi bir paket kaynağına iter ve yayınlar.</span><span class="sxs-lookup"><span data-stu-id="3be60-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="3be60-107">NuGet 'in varsayılan yapılandırması `%AppData%\NuGet\NuGet.Config` , (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) yüklenir, ardından sürücü kökünden başlayıp geçerli dizinde `.nuget\Nuget.Config` sona ermek üzere herhangi bir `Nuget.Config` veya dosya yükleniyor (bkz. [ortak NuGet yapılandırma](../../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="3be60-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="3be60-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="3be60-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="3be60-109">, sunucuya göndermek için paketi tanımlar.`<packagePath>`</span><span class="sxs-lookup"><span data-stu-id="3be60-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="3be60-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="3be60-110">Options</span></span>

| <span data-ttu-id="3be60-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="3be60-111">Option</span></span> | <span data-ttu-id="3be60-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3be60-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3be60-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="3be60-113">ApiKey</span></span> | <span data-ttu-id="3be60-114">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3be60-114">The API key for the target repository.</span></span> <span data-ttu-id="3be60-115">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3be60-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="3be60-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3be60-116">ConfigFile</span></span> | <span data-ttu-id="3be60-117">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="3be60-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3be60-118">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3be60-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3be60-119">Disablearabelleğe alma</span><span class="sxs-lookup"><span data-stu-id="3be60-119">DisableBuffering</span></span> | <span data-ttu-id="3be60-120">Bellek kullanımlarını azaltmak için bir HTTP (s) sunucusuna gönderilirken arabelleğe almayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="3be60-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="3be60-121">Dikkat: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="3be60-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="3be60-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3be60-122">ForceEnglishOutput</span></span> | <span data-ttu-id="3be60-123">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="3be60-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3be60-124">Help</span><span class="sxs-lookup"><span data-stu-id="3be60-124">Help</span></span> | <span data-ttu-id="3be60-125">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3be60-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="3be60-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3be60-126">NonInteractive</span></span> | <span data-ttu-id="3be60-127">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="3be60-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3be60-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="3be60-128">NoSymbols</span></span> | <span data-ttu-id="3be60-129">*(3,5 +)* Bir semboller paketi varsa, bir sembol sunucusuna itilecektir.</span><span class="sxs-lookup"><span data-stu-id="3be60-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="3be60-130">Source</span><span class="sxs-lookup"><span data-stu-id="3be60-130">Source</span></span> | <span data-ttu-id="3be60-131">Sunucu URL 'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3be60-131">Specifies the server URL.</span></span> <span data-ttu-id="3be60-132">NuGet bir UNC veya yerel klasör kaynağını tanımlar ve dosyayı HTTP kullanarak göndermek yerine buraya kopyalar.</span><span class="sxs-lookup"><span data-stu-id="3be60-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="3be60-133">Ayrıca, NuGet 3.4.2 ile başlayarak, `NuGet.Config` dosya bir *defaultpushsource* değeri belirtmediği müddetçe bu zorunlu bir parametredir (bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="3be60-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="3be60-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="3be60-134">SkipDuplicate</span></span> | <span data-ttu-id="3be60-135">*(5.1 +)* Bir paket ve sürüm zaten varsa, bunu atlayın ve varsa gönderim içindeki bir sonraki pakete devam edin.</span><span class="sxs-lookup"><span data-stu-id="3be60-135">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="3be60-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="3be60-136">SymbolSource</span></span> | <span data-ttu-id="3be60-137">*(3,5 +)* Sembol sunucusu URL 'sini belirtir; nuget.org 'e gönderilirken nuget.smbsrc.net kullanılır</span><span class="sxs-lookup"><span data-stu-id="3be60-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="3be60-138">Sembolapikey</span><span class="sxs-lookup"><span data-stu-id="3be60-138">SymbolApiKey</span></span> | <span data-ttu-id="3be60-139">*(3,5 +)* İçinde `-SymbolSource`BELIRTILEN URL için API anahtarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3be60-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="3be60-140">zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="3be60-140">Timeout</span></span> | <span data-ttu-id="3be60-141">Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3be60-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="3be60-142">Varsayılan değer 300 saniyedir (5 dakika).</span><span class="sxs-lookup"><span data-stu-id="3be60-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="3be60-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3be60-143">Verbosity</span></span> | <span data-ttu-id="3be60-144">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="3be60-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3be60-145">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3be60-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3be60-146">Örnekler</span><span class="sxs-lookup"><span data-stu-id="3be60-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
