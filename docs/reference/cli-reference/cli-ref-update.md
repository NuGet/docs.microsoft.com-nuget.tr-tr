---
title: NuGet CLI update komutu
description: nuget.exe update komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323654"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="8d7d6-103">update komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8d7d6-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="8d7d6-104">**Uygulama: paket** tüketimi &bullet; **Desteklenen sürümler:** hepsi</span><span class="sxs-lookup"><span data-stu-id="8d7d6-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8d7d6-105">Bir proje içinde tüm paketleri `packages.config` (kullanarak) en son kullanılabilir sürümlerine güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="8d7d6-106">çalıştırmadan önce ['restore' çalıştırması](cli-ref-restore.md) `update` önerilir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="8d7d6-107">(Tek bir paketi güncelleştirmek için, sürüm numarası belirtmeden kullanın; bu [`nuget install`](cli-ref-install.md) durumda NuGet en son sürümü yüklüdür.)</span><span class="sxs-lookup"><span data-stu-id="8d7d6-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="8d7d6-108">Not: Mono (Mac OSX veya Linux) altında çalışan CLI ile veya `update` PackageReference biçimi kullanırken çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="8d7d6-109">Komut `update` ayrıca, bu başvuruların zaten mevcut olduğu durumda proje dosyasında derleme başvurularını da günceller.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="8d7d6-110">Güncelleştirilmiş bir paketin ekli bir derlemesi varsa, yeni bir *başvuru eklenmez.*</span><span class="sxs-lookup"><span data-stu-id="8d7d6-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="8d7d6-111">Yeni paket bağımlılıklarında da derleme başvuruları eklenmez.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="8d7d6-112">Bu işlemleri bir güncelleştirmenin parçası olarak eklemek için Paket Yöneticisi kullanıcı arabirimini veya Visual Studio Konsolu'nu kullanarak paketi Paket Yöneticisi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="8d7d6-113">Bu komut, *-self* bayrağını nuget.exe kendi kendini güncelleştirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="8d7d6-114">Kullanım</span><span class="sxs-lookup"><span data-stu-id="8d7d6-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="8d7d6-115">burada, `<configPath>` projenin `packages.config` bağımlılıklarını listeleen bir veya çözüm dosyası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="8d7d6-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="8d7d6-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8d7d6-117">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8d7d6-118">Belirtilmezse `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="8d7d6-119">Kullanmak üzere bağımlılık paketlerinin sürümünü belirtir; bu sürüm, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="8d7d6-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8d7d6-120">*En* düşük (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="8d7d6-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8d7d6-121">*HighestPatch:* En düşük ana, en düşük ikincil, en yüksek düzeltme ekini olan sürüm</span><span class="sxs-lookup"><span data-stu-id="8d7d6-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8d7d6-122">*HighestMinor:* en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="8d7d6-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8d7d6-123">*En yüksek*: en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="8d7d6-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="8d7d6-124">*Yoksay:* Hiçbir bağımlılık paketi kullanılmaz</span><span class="sxs-lookup"><span data-stu-id="8d7d6-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="8d7d6-125">Bir paketten bir dosya hedef projede zaten mevcut olduğunda varsayılan eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="8d7d6-126">Her zaman `Overwrite` dosyaların üzerine yaz olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="8d7d6-127">Dosyaları atlamak `Ignore` için olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="8d7d6-128">Varsayılan eylem, veya sağlanıyorsa çakışan her dosyayı ister ve bu da `PromptUser` kalan tüm dosyalar için geçerli `OverwriteAll` `IgnoreAll` olur.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8d7d6-129">*(3,5+)* Bu nuget.exe sabit, İngilizce tabanlı bir kültür kullanarak çalıştırmaya güçler.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8d7d6-130">Komutun yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="8d7d6-131">Güncelleştirilen paket kimliklerinin listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="8d7d6-132">*(4.0+)* komutuyla birlikte kullanmak üzere MSBuild'in yolunu belirtir ve önceliğe sahip `-MSBuildVersion` olur.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="8d7d6-133">*(3.2+)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="8d7d6-134">Desteklenen değerler: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="8d7d6-135">Varsayılan olarak, yolunuz msBuild seçerek, aksi takdirde msbuild'in en yüksek yüklü sürümüne varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8d7d6-136">Kullanıcı girişi veya onay istemlerini bastırıyor.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="8d7d6-137">Sürümleri ön sürüme güncelleştirmeye izin verir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="8d7d6-138">Zaten yüklü olan ön sürümü paketleri güncelleştiriliyorken bu bayrak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="8d7d6-139">Paketlerin yüklü olduğu yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="8d7d6-140">Yalnızca yüklü paketle aynı ana ve ikincil sürümde bulunan en yüksek sürüme sahip güncelleştirmelerin yük olacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="8d7d6-141">En `nuget.exe` son sürüme güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="8d7d6-142">`-Source` kullanılabilir, ancak diğer tüm bağımsız değişkenler yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="8d7d6-143">Kaynak sağlanamıyorsa, `nuget.org` ayarlardan bağımsız olarak güncelleştirmeleri `NuGet.Config` denetler.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="8d7d6-144">Güncelleştirmeler için kullanmak üzere paket kaynaklarının listesini (URL olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="8d7d6-145">Atlanırsa, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz. [Ortak NuGet yapılandırmaları.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="8d7d6-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8d7d6-146">Çıktıda görüntülenen ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="8d7d6-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="8d7d6-147">Bir paket kimliği ile birlikte kullanılırken, güncelleştirilen paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="8d7d6-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="8d7d6-148">Ayrıca [bkz. Ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d7d6-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8d7d6-149">Örnekler</span><span class="sxs-lookup"><span data-stu-id="8d7d6-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
