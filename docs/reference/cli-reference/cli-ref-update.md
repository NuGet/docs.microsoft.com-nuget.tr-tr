---
title: NuGet CLı güncelleştirme komutu
description: nuget.exe Update komutuna yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236795"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="1c1ab-103">Update komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="1c1ab-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="1c1ab-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="1c1ab-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1c1ab-105">Projedeki tüm paketleri (kullanarak `packages.config` ) en son kullanılabilir sürümlerine güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="1c1ab-106">Çalıştırılmadan önce [' Restore '](cli-ref-restore.md) çalıştırmak önerilir `update` .</span><span class="sxs-lookup"><span data-stu-id="1c1ab-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="1c1ab-107">(Tek bir paketi güncelleştirmek için, [`nuget install`](cli-ref-install.md) sürüm numarası belirtmeden kullanın, bu durumda NuGet en son sürümü yüklerse.)</span><span class="sxs-lookup"><span data-stu-id="1c1ab-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="1c1ab-108">Not: `update` Mono (Mac OSX veya Linux) altında çalışan CLI ile veya PackageReference biçimi kullanılırken çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="1c1ab-109">`update`Bu başvurular zaten mevcut olduğundan, komut proje dosyasındaki derleme başvurularını da güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="1c1ab-110">Güncelleştirilmiş bir pakette eklenen bir derleme varsa, yeni bir *başvuru eklenmez.*</span><span class="sxs-lookup"><span data-stu-id="1c1ab-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="1c1ab-111">Yeni paket bağımlılıklarına Ayrıca, derleme başvuruları da eklenmez.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="1c1ab-112">Bu işlemleri bir güncelleştirmenin parçası olarak dahil etmek için, Paket Yöneticisi Kullanıcı arabirimini veya paket Yöneticisi konsolunu kullanarak Visual Studio 'da paketi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="1c1ab-113">Bu komut, *-self* bayrağını kullanarak nuget.exe kendisini güncelleştirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="1c1ab-114">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1c1ab-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="1c1ab-115">`<configPath>` `packages.config` , projenin bağımlılıklarını listeleyen bir veya çözüm dosyası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="1c1ab-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="1c1ab-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="1c1ab-117">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1c1ab-118">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="1c1ab-119">Kullanılacak bağımlılık paketlerinin sürümünü belirtir; Bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="1c1ab-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="1c1ab-120">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="1c1ab-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="1c1ab-121">*HighestPatch* : en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="1c1ab-121">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="1c1ab-122">*HighestMinor* : en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="1c1ab-122">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="1c1ab-123">*En yüksek* : en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="1c1ab-123">*Highest* : the highest version</span></span></li><li><span data-ttu-id="1c1ab-124">*Yoksay* : bağımlılık paketleri kullanılmayacak</span><span class="sxs-lookup"><span data-stu-id="1c1ab-124">*Ignore* : No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="1c1ab-125">Bir paketten bir dosya hedef projede zaten mevcut olduğunda varsayılan eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="1c1ab-126">`Overwrite`Dosyaları her zaman üzerine yazacak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="1c1ab-127">`Ignore`Dosyaları atlamak için olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="1c1ab-128">`PromptUser`Varsayılan olarak, bu eylem, `OverwriteAll` `IgnoreAll` kalan tüm dosyalar için uygulanacak olan veya sağlanmazsa her çakışan dosya için istemde bulunur.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="1c1ab-129">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="1c1ab-130">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="1c1ab-131">Güncelleştirilecek paket kimliklerinin bir listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="1c1ab-132">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="1c1ab-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="1c1ab-133">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="1c1ab-134">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="1c1ab-135">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="1c1ab-136">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="1c1ab-137">Yayın öncesi sürümlere güncelleştirme yapılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="1c1ab-138">Zaten yüklü olan ön sürüm paketleri güncelleştirilirken bu bayrak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="1c1ab-139">Paketlerin yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="1c1ab-140">Yüklü paket ile aynı ana ve alt sürüm içinde yalnızca en yüksek sürüme sahip güncelleştirmelerin yükleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="1c1ab-141">En son sürüme nuget.exe güncelleştirmeler; diğer tüm bağımsız değişkenler yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="1c1ab-142">Güncelleştirmeler için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="1c1ab-143">Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="1c1ab-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="1c1ab-144">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="1c1ab-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="1c1ab-145">Tek bir paket KIMLIĞIYLE birlikte kullanıldığında, güncelleştirilecek paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1c1ab-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="1c1ab-146">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1c1ab-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1c1ab-147">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1c1ab-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
