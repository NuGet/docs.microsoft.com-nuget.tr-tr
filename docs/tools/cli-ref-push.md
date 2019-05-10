---
title: NuGet CLI anında iletme komutu
description: Nuget.exe anında iletme komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877952"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="cad20-103">anında iletme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cad20-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="cad20-104">**İçin geçerlidir:** paket yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli</span><span class="sxs-lookup"><span data-stu-id="cad20-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="cad20-105">Nuget.org için paketleri göndermeye nuget.exe verze 4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="cad20-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="cad20-106">Bir paket kaynağı için bir paket gönderir ve belgeyi yayımlar.</span><span class="sxs-lookup"><span data-stu-id="cad20-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="cad20-107">NuGet'ın varsayılan yapılandırmayı yükleyerek elde `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), ardından her yüklenirken `Nuget.Config` veya `.nuget\Nuget.Config` sürücüsünün kökünden başlayıp geçerli dizinde dosyaları (bkz [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="cad20-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="cad20-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="cad20-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="cad20-109">Burada `<packagePath>` sunucuya göndermek üzere paket tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cad20-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="cad20-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="cad20-110">Options</span></span>

| <span data-ttu-id="cad20-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="cad20-111">Option</span></span> | <span data-ttu-id="cad20-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cad20-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cad20-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="cad20-113">ApiKey</span></span> | <span data-ttu-id="cad20-114">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cad20-114">The API key for the target repository.</span></span> <span data-ttu-id="cad20-115">Yoksa, yapılandırma dosyasında belirtilen kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cad20-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="cad20-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cad20-116">ConfigFile</span></span> | <span data-ttu-id="cad20-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="cad20-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cad20-118">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cad20-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cad20-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="cad20-119">DisableBuffering</span></span> | <span data-ttu-id="cad20-120">Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna gönderirken arabelleğe almayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="cad20-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="cad20-121">Dikkat: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="cad20-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="cad20-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cad20-122">ForceEnglishOutput</span></span> | <span data-ttu-id="cad20-123">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="cad20-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cad20-124">Help</span><span class="sxs-lookup"><span data-stu-id="cad20-124">Help</span></span> | <span data-ttu-id="cad20-125">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="cad20-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="cad20-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cad20-126">NonInteractive</span></span> | <span data-ttu-id="cad20-127">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="cad20-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cad20-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="cad20-128">NoSymbols</span></span> | <span data-ttu-id="cad20-129">*(3.5 +)*  Bir sembol paketi varsa, bunu bir simge sunucusuna gönderilecek değil.</span><span class="sxs-lookup"><span data-stu-id="cad20-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="cad20-130">Source</span><span class="sxs-lookup"><span data-stu-id="cad20-130">Source</span></span> | <span data-ttu-id="cad20-131">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="cad20-131">Specifies the server URL.</span></span> <span data-ttu-id="cad20-132">NuGet, UNC veya yerel klasör kaynak tanımlar ve yalnızca HTTP kullanarak gönderme yerine dosya var. kopyalar.</span><span class="sxs-lookup"><span data-stu-id="cad20-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="cad20-133">Ayrıca, 3.4.2 NuGet ile başlayarak, zorunlu bir parametre sürece budur `NuGet.Config` dosyasını belirtir bir *DefaultPushSource* değeri (bkz [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="cad20-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="cad20-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="cad20-134">SymbolSource</span></span> | <span data-ttu-id="cad20-135">*(3.5 +)*  Sembol sunucusunun URL'sini belirtir; nuget.smbsrc.net nuget.org için gönderirken kullanılan</span><span class="sxs-lookup"><span data-stu-id="cad20-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="cad20-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="cad20-136">SymbolApiKey</span></span> | <span data-ttu-id="cad20-137">*(3.5 +)*  Belirtilen URL için API anahtarını belirtir `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="cad20-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="cad20-138">zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="cad20-138">Timeout</span></span> | <span data-ttu-id="cad20-139">Bir sunucuya göndermek için saniye cinsinden zaman aşımı belirtir.</span><span class="sxs-lookup"><span data-stu-id="cad20-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="cad20-140">300 saniyedir (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="cad20-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="cad20-141">Verbosity</span><span class="sxs-lookup"><span data-stu-id="cad20-141">Verbosity</span></span> | <span data-ttu-id="cad20-142">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="cad20-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cad20-143">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cad20-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cad20-144">Örnekler</span><span class="sxs-lookup"><span data-stu-id="cad20-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
