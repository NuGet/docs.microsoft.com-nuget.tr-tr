---
title: NuGet CLı Push komutu
description: nuget.exe Push komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d53a2e7f41219e68e59b195d1d5a9d1f62ad7c63
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622853"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="65582-103">Push komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="65582-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="65582-104">**Uygulama hedefi:** paket yayımlaması &bullet; **Desteklenen sürümler:** All; 4.1.0 + NuGet.org için gereklidir</span><span class="sxs-lookup"><span data-stu-id="65582-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="65582-105">Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../../api/nuget-protocols.md)uygulayan nuget.exe v 4.1.0 + kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65582-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../../api/nuget-protocols.md).</span></span>

<span data-ttu-id="65582-106">Paketi bir paket kaynağına iter ve yayınlar.</span><span class="sxs-lookup"><span data-stu-id="65582-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="65582-107">NuGet 'in varsayılan yapılandırması `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) yüklenir, ardından `Nuget.Config` `.nuget\Nuget.Config` sürücü kökünden başlayıp geçerli dizinde (bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md)) başlayarak veya dosya yüklendikten sonra alınır</span><span class="sxs-lookup"><span data-stu-id="65582-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="65582-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="65582-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="65582-109">, `<packagePath>` sunucuya göndermek için paketi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="65582-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="65582-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="65582-110">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="65582-111">Hedef depo için API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="65582-111">The API key for the target repository.</span></span> <span data-ttu-id="65582-112">Mevcut değilse, yapılandırma dosyasında belirtilen bir tane kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65582-112">If not present,  the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="65582-113">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="65582-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="65582-114">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65582-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DisableBuffering`**

  <span data-ttu-id="65582-115">Bellek kullanımlarını azaltmak için bir HTTP (s) sunucusuna gönderilirken arabelleğe almayı devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="65582-115">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="65582-116">Dikkat: Bu seçenek kullanıldığında, tümleşik Windows kimlik doğrulaması çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="65582-116">Caution: when this option is used, integrated Windows authentication might not work.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="65582-117">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="65582-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="65582-118">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="65582-118">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="65582-119">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="65582-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoServiceEndpoint`**

  <span data-ttu-id="65582-120">`api/v2/packages`Kaynak URL 'ye eklemez.</span><span class="sxs-lookup"><span data-stu-id="65582-120">Does not append `api/v2/packages` to the source URL.</span></span>

- **`-NoSymbols`**

  <span data-ttu-id="65582-121">*(3,5 +)* Bir semboller paketi varsa, bir sembol sunucusuna itilecektir.</span><span class="sxs-lookup"><span data-stu-id="65582-121">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="65582-122">Sunucu URL 'sini belirtir.</span><span class="sxs-lookup"><span data-stu-id="65582-122">Specifies the server URL.</span></span> <span data-ttu-id="65582-123">NuGet bir UNC veya yerel klasör kaynağını tanımlar ve dosyayı HTTP kullanarak göndermek yerine buraya kopyalar.</span><span class="sxs-lookup"><span data-stu-id="65582-123">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="65582-124">Ayrıca, NuGet 3.4.2 ile başlayarak, `NuGet.Config` dosya bir *Defaultpushsource* değeri belirtmediği müddetçe bu zorunlu bir parametredir (bkz. [NuGet davranışını yapılandırma](../../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="65582-124">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md)).</span></span>

- **`-SkipDuplicate`**

  <span data-ttu-id="65582-125">*(5.1 +)* Bir paket ve sürüm zaten varsa, bunu atlayın ve varsa gönderim içindeki bir sonraki pakete devam edin.</span><span class="sxs-lookup"><span data-stu-id="65582-125">*(5.1+)* If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span>

- **`-SymbolSource`**

  <span data-ttu-id="65582-126">*(3,5 +)* Sembol sunucusu URL 'sini belirtir; nuget.org 'e gönderilirken nuget.smbsrc.net kullanılır</span><span class="sxs-lookup"><span data-stu-id="65582-126">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span>

- **`-SymbolApiKey`**

  <span data-ttu-id="65582-127">*(3,5 +)* İçinde belirtilen URL için API anahtarını belirtir `-SymbolSource` .</span><span class="sxs-lookup"><span data-stu-id="65582-127">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span>

- **`-Timeout`**

  <span data-ttu-id="65582-128">Bir sunucuya göndermek için saniye cinsinden zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="65582-128">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="65582-129">Varsayılan değer 300 saniyedir (5 dakika).</span><span class="sxs-lookup"><span data-stu-id="65582-129">The default is 300 seconds (5 minutes).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="65582-130">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="65582-130">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


<span data-ttu-id="65582-131">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="65582-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="65582-132">Örnekler</span><span class="sxs-lookup"><span data-stu-id="65582-132">Examples</span></span>

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
