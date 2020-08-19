---
title: NuGet CLı güncelleştirme komutu
description: nuget.exe Update komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 84f939188ac190f6d539f8ee2b422049a274f178
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622583"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="ddef3-103">Update komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="ddef3-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="ddef3-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="ddef3-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ddef3-105">Projedeki tüm paketleri (kullanarak `packages.config` ) en son kullanılabilir sürümlerine güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ddef3-106">Çalıştırılmadan önce [' Restore '](cli-ref-restore.md) çalıştırmak önerilir `update` .</span><span class="sxs-lookup"><span data-stu-id="ddef3-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="ddef3-107">(Tek bir paketi güncelleştirmek için, [`nuget install`](cli-ref-install.md) sürüm numarası belirtmeden kullanın, bu durumda NuGet en son sürümü yüklerse.)</span><span class="sxs-lookup"><span data-stu-id="ddef3-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="ddef3-108">Not: `update` Mono (Mac OSX veya Linux) altında çalışan CLI ile veya PackageReference biçimi kullanılırken çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ddef3-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="ddef3-109">`update`Bu başvurular zaten mevcut olduğundan, komut proje dosyasındaki derleme başvurularını da güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="ddef3-110">Güncelleştirilmiş bir pakette eklenen bir derleme varsa, yeni bir *başvuru eklenmez.*</span><span class="sxs-lookup"><span data-stu-id="ddef3-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="ddef3-111">Yeni paket bağımlılıklarına Ayrıca, derleme başvuruları da eklenmez.</span><span class="sxs-lookup"><span data-stu-id="ddef3-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="ddef3-112">Bu işlemleri bir güncelleştirmenin parçası olarak dahil etmek için, Paket Yöneticisi Kullanıcı arabirimini veya paket Yöneticisi konsolunu kullanarak Visual Studio 'da paketi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ddef3-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="ddef3-113">Bu komut, *-self* bayrağını kullanarak nuget.exe kendisini güncelleştirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="ddef3-114">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ddef3-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="ddef3-115">`<configPath>` `packages.config` , projenin bağımlılıklarını listeleyen bir veya çözüm dosyası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ddef3-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="ddef3-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ddef3-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="ddef3-117">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="ddef3-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ddef3-118">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ddef3-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="ddef3-119">Bir paketten bir dosya hedef projede zaten mevcut olduğunda varsayılan eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-119">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="ddef3-120">`Overwrite`Dosyaları her zaman üzerine yazacak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ddef3-120">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="ddef3-121">`Ignore`Dosyaları atlamak için olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ddef3-121">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="ddef3-122">`PromptUser`Varsayılan olarak, bu eylem, `OverwriteAll` `IgnoreAll` kalan tüm dosyalar için uygulanacak olan veya sağlanmazsa her çakışan dosya için istemde bulunur.</span><span class="sxs-lookup"><span data-stu-id="ddef3-122">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="ddef3-123">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="ddef3-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="ddef3-124">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ddef3-124">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="ddef3-125">Güncelleştirilecek paket kimliklerinin bir listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-125">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="ddef3-126">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="ddef3-126">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="ddef3-127">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-127">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ddef3-128">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="ddef3-128">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="ddef3-129">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ddef3-129">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="ddef3-130">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="ddef3-130">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="ddef3-131">Yayın öncesi sürümlere güncelleştirme yapılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-131">Allows updating to prerelease versions.</span></span> <span data-ttu-id="ddef3-132">Zaten yüklü olan ön sürüm paketleri güncelleştirilirken bu bayrak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-132">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="ddef3-133">Paketlerin yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-133">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="ddef3-134">Yüklü paket ile aynı ana ve alt sürüm içinde yalnızca en yüksek sürüme sahip güncelleştirmelerin yükleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-134">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="ddef3-135">En son sürüme nuget.exe güncelleştirmeler; diğer tüm bağımsız değişkenler yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="ddef3-135">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="ddef3-136">Güncelleştirmeler için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-136">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="ddef3-137">Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ddef3-137">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="ddef3-138">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="ddef3-138">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="ddef3-139">Tek bir paket KIMLIĞIYLE birlikte kullanıldığında, güncelleştirilecek paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ddef3-139">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="ddef3-140">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ddef3-140">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ddef3-141">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ddef3-141">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
