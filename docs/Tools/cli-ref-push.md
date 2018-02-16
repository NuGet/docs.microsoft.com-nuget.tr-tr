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
ms.openlocfilehash: df8ef42f650a20b92a281fff3e597ac8d484544e
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="a9aca-104">anında iletme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a9aca-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="a9aca-105">**Uygulandığı öğe:** paketini yayımlama &bullet; **desteklenen sürümler:** tüm; 4.1.0+ nuget.org için gerekli</span><span class="sxs-lookup"><span data-stu-id="a9aca-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="a9aca-106">Nuget.org için paketleri göndermek için nuget.exe v4.1.0 gerekli uygulayan + kullanmalısınız [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a9aca-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="a9aca-107">Bir paket için paket kaynağı iter ve onu yayımlar.</span><span class="sxs-lookup"><span data-stu-id="a9aca-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="a9aca-108">NuGet'ın varsayılan yapılandırması yükleyerek elde edilir `%AppData%\NuGet\NuGet.Config`, herhangi bir yükleme sonra `Nuget.Config` veya `.nuget\Nuget.Config` dosyaları sürücüsünün kökünden başlayıp geçerli dizinde (bkz [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="a9aca-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="a9aca-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="a9aca-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="a9aca-110">Burada `<packagePath>` sunucuya göndermek için paketi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a9aca-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="a9aca-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="a9aca-111">Options</span></span>

| <span data-ttu-id="a9aca-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="a9aca-112">Option</span></span> | <span data-ttu-id="a9aca-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a9aca-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9aca-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="a9aca-114">ApiKey</span></span> | <span data-ttu-id="a9aca-115">Hedef depo API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="a9aca-115">The API key for the target repository.</span></span> <span data-ttu-id="a9aca-116">Mevcut bir belirtilen varsa *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a9aca-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a9aca-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a9aca-117">ConfigFile</span></span> | <span data-ttu-id="a9aca-118">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a9aca-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a9aca-119">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a9aca-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a9aca-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="a9aca-120">DisableBuffering</span></span> | <span data-ttu-id="a9aca-121">Bellek kullanımları azaltmak için bir HTTP (s) sunucusuna iletme zaman arabelleğe almayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="a9aca-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="a9aca-122">Uyarı: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="a9aca-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="a9aca-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a9aca-123">ForceEnglishOutput</span></span> | <span data-ttu-id="a9aca-124">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="a9aca-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a9aca-125">Yardım</span><span class="sxs-lookup"><span data-stu-id="a9aca-125">Help</span></span> | <span data-ttu-id="a9aca-126">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a9aca-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="a9aca-127">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="a9aca-127">NonInteractive</span></span> | <span data-ttu-id="a9aca-128">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="a9aca-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a9aca-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="a9aca-129">NoSymbols</span></span> | <span data-ttu-id="a9aca-130">*(3.5 +)*  Simge paketi varsa, onu bir simge sunucuya gönderilir değil.</span><span class="sxs-lookup"><span data-stu-id="a9aca-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="a9aca-131">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a9aca-131">Source</span></span> | <span data-ttu-id="a9aca-132">Sunucu URL'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="a9aca-132">Specifies the server URL.</span></span> <span data-ttu-id="a9aca-133">NuGet UNC veya yerel klasöre kaynak tanımlar ve yalnızca HTTP kullanarak gönderilmesi yerine dosya var. kopyalar.</span><span class="sxs-lookup"><span data-stu-id="a9aca-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="a9aca-134">Ayrıca, 3.4.2 NuGet ile başlayarak, bu zorunlu bir sürece parametredir `NuGet.Config` dosyayı belirtir bir *DefaultPushSource* değeri (bkz [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="a9aca-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="a9aca-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="a9aca-135">SymbolSource</span></span> | <span data-ttu-id="a9aca-136">*(3.5 +)*  Simgesiyle sunucu URL belirtir; nuget.smbsrc.net için nuget.org Ftp'den zaman kullanılır</span><span class="sxs-lookup"><span data-stu-id="a9aca-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="a9aca-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="a9aca-137">SymbolApiKey</span></span> | <span data-ttu-id="a9aca-138">*(3.5 +)*  URL belirtilen API anahtarını belirtir `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="a9aca-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="a9aca-139">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="a9aca-139">Timeout</span></span> | <span data-ttu-id="a9aca-140">Bir sunucuya gönderilmesi için saniye olarak zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a9aca-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="a9aca-141">300 saniye (5 dakika) varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a9aca-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="a9aca-142">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="a9aca-142">Verbosity</span></span> | <span data-ttu-id="a9aca-143">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="a9aca-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a9aca-144">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a9aca-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a9aca-145">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a9aca-145">Examples</span></span>

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
