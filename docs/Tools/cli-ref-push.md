---
title: NuGet CLI itme komutu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe itme komut başvurusu"
keywords: nuget push reference, push command
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 095e81406df3db5fbfc6c5202362894b2c6d7cf8
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="d0610-104">anında iletme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d0610-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="d0610-105">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli</span><span class="sxs-lookup"><span data-stu-id="d0610-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="d0610-106">Nuget.org için paketleri göndermek için nuget.exe v4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d0610-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="d0610-107">Bir paket için paket kaynağı iter ve onu yayımlar.</span><span class="sxs-lookup"><span data-stu-id="d0610-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="d0610-108">NuGet'ın varsayılan yapılandırması yükleyerek elde edilir `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), ardından her yükleme `Nuget.Config` veya `.nuget\Nuget.Config` dosyaları sürücüsünün kökünden başlayıp geçerli dizinde (bkz [yapılandırma NuGet davranışı](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="d0610-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="d0610-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d0610-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="d0610-110">Burada `<packagePath>` sunucuya göndermek için paketi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d0610-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="d0610-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="d0610-111">Options</span></span>

| <span data-ttu-id="d0610-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="d0610-112">Option</span></span> | <span data-ttu-id="d0610-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d0610-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0610-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d0610-114">ApiKey</span></span> | <span data-ttu-id="d0610-115">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d0610-115">The API key for the target repository.</span></span> <span data-ttu-id="d0610-116">Yoksa, yapılandırma dosyasında belirtilen bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0610-116">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="d0610-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d0610-117">ConfigFile</span></span> | <span data-ttu-id="d0610-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d0610-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d0610-119">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0610-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d0610-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="d0610-120">DisableBuffering</span></span> | <span data-ttu-id="d0610-121">Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna iletme zaman arabelleğe almayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="d0610-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="d0610-122">Uyarı: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d0610-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="d0610-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d0610-123">ForceEnglishOutput</span></span> | <span data-ttu-id="d0610-124">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="d0610-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d0610-125">Yardım</span><span class="sxs-lookup"><span data-stu-id="d0610-125">Help</span></span> | <span data-ttu-id="d0610-126">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0610-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="d0610-127">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="d0610-127">NonInteractive</span></span> | <span data-ttu-id="d0610-128">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="d0610-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d0610-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="d0610-129">NoSymbols</span></span> | <span data-ttu-id="d0610-130">*(3.5 +)*  Simge paketi varsa, onu bir simge sunucuya gönderilir değil.</span><span class="sxs-lookup"><span data-stu-id="d0610-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="d0610-131">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d0610-131">Source</span></span> | <span data-ttu-id="d0610-132">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0610-132">Specifies the server URL.</span></span> <span data-ttu-id="d0610-133">NuGet UNC veya yerel klasöre kaynak tanımlar ve yalnızca HTTP kullanarak gönderilmesi yerine dosya var. kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d0610-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="d0610-134">Ayrıca, 3.4.2 NuGet ile başlayarak, bu zorunlu bir sürece parametredir `NuGet.Config` dosyayı belirtir bir *DefaultPushSource* değeri (bkz [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="d0610-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="d0610-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="d0610-135">SymbolSource</span></span> | <span data-ttu-id="d0610-136">*(3.5 +)*  Simgesiyle sunucu URL belirtir; nuget.smbsrc.net için nuget.org Ftp'den zaman kullanılır</span><span class="sxs-lookup"><span data-stu-id="d0610-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="d0610-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="d0610-137">SymbolApiKey</span></span> | <span data-ttu-id="d0610-138">*(3.5 +)*  URL belirtilen API anahtarını belirtir `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="d0610-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="d0610-139">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="d0610-139">Timeout</span></span> | <span data-ttu-id="d0610-140">Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d0610-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="d0610-141">300 saniye (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="d0610-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="d0610-142">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="d0610-142">Verbosity</span></span> | <span data-ttu-id="d0610-143">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="d0610-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d0610-144">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d0610-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d0610-145">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d0610-145">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
