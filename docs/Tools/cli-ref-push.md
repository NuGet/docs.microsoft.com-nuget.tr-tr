---
title: NuGet CLI itme komutu
description: Nuget.exe itme komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 959b539fc20bc47f38946cb660375a6652582a0d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="d35f6-103">anında iletme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d35f6-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="d35f6-104">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli</span><span class="sxs-lookup"><span data-stu-id="d35f6-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="d35f6-105">Nuget.org için paketleri göndermek için nuget.exe v4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d35f6-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="d35f6-106">Bir paket için paket kaynağı iter ve onu yayımlar.</span><span class="sxs-lookup"><span data-stu-id="d35f6-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="d35f6-107">NuGet'ın varsayılan yapılandırması yükleyerek elde edilir `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), ardından her yükleme `Nuget.Config` veya `.nuget\Nuget.Config` dosyaları sürücüsünün kökünden başlayıp geçerli dizinde (bkz [yapılandırma NuGet davranışı](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="d35f6-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="d35f6-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d35f6-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="d35f6-109">Burada `<packagePath>` sunucuya göndermek için paketi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d35f6-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="d35f6-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="d35f6-110">Options</span></span>

| <span data-ttu-id="d35f6-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="d35f6-111">Option</span></span> | <span data-ttu-id="d35f6-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d35f6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d35f6-113">apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="d35f6-113">ApiKey</span></span> | <span data-ttu-id="d35f6-114">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d35f6-114">The API key for the target repository.</span></span> <span data-ttu-id="d35f6-115">Yoksa, yapılandırma dosyasında belirtilen bir kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d35f6-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="d35f6-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d35f6-116">ConfigFile</span></span> | <span data-ttu-id="d35f6-117">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d35f6-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d35f6-118">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d35f6-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d35f6-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="d35f6-119">DisableBuffering</span></span> | <span data-ttu-id="d35f6-120">Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna iletme zaman arabelleğe almayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="d35f6-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="d35f6-121">Uyarı: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d35f6-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="d35f6-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d35f6-122">ForceEnglishOutput</span></span> | <span data-ttu-id="d35f6-123">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="d35f6-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d35f6-124">Yardım</span><span class="sxs-lookup"><span data-stu-id="d35f6-124">Help</span></span> | <span data-ttu-id="d35f6-125">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d35f6-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="d35f6-126">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="d35f6-126">NonInteractive</span></span> | <span data-ttu-id="d35f6-127">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="d35f6-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d35f6-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="d35f6-128">NoSymbols</span></span> | <span data-ttu-id="d35f6-129">*(3.5 +)*  Simge paketi varsa, onu bir simge sunucuya gönderilir değil.</span><span class="sxs-lookup"><span data-stu-id="d35f6-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="d35f6-130">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d35f6-130">Source</span></span> | <span data-ttu-id="d35f6-131">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="d35f6-131">Specifies the server URL.</span></span> <span data-ttu-id="d35f6-132">NuGet UNC veya yerel klasöre kaynak tanımlar ve yalnızca HTTP kullanarak gönderilmesi yerine dosya var. kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d35f6-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="d35f6-133">Ayrıca, 3.4.2 NuGet ile başlayarak, bu zorunlu bir sürece parametredir `NuGet.Config` dosyayı belirtir bir *DefaultPushSource* değeri (bkz [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="d35f6-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="d35f6-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="d35f6-134">SymbolSource</span></span> | <span data-ttu-id="d35f6-135">*(3.5 +)*  Simgesiyle sunucu URL belirtir; nuget.smbsrc.net için nuget.org Ftp'den zaman kullanılır</span><span class="sxs-lookup"><span data-stu-id="d35f6-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="d35f6-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="d35f6-136">SymbolApiKey</span></span> | <span data-ttu-id="d35f6-137">*(3.5 +)*  URL belirtilen API anahtarını belirtir `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="d35f6-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="d35f6-138">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="d35f6-138">Timeout</span></span> | <span data-ttu-id="d35f6-139">Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d35f6-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="d35f6-140">300 saniye (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="d35f6-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="d35f6-141">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="d35f6-141">Verbosity</span></span> | <span data-ttu-id="d35f6-142">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="d35f6-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d35f6-143">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d35f6-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d35f6-144">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d35f6-144">Examples</span></span>

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
