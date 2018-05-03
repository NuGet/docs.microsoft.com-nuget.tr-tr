---
title: NuGet CLI güncelleştirme komutu
description: Nuget.exe güncelleştirme komut başvurusu
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="fd1a6-103">güncelleştirme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fd1a6-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="fd1a6-104">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="fd1a6-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="fd1a6-105">Güncelleştirmeleri projesindeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine için.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="fd1a6-106">Çalıştırmak için önerilen ['geri'](cli-ref-restore.md) çalıştırmadan önce `update`.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="fd1a6-107">(Tek tek bir paketi güncelleştirmeye [ `nuget install` ](cli-ref-install.md) servis talebi NuGet en son sürümünü yükler, bir sürüm numarası belirtmeden.)</span><span class="sxs-lookup"><span data-stu-id="fd1a6-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="fd1a6-108">Not: `update` Mono (Mac OSX veya Linux) altında veya PackageReference biçimi kullanılırken çalıştıran CLI ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="fd1a6-109">`update` Komutu derleme başvurularını proje dosyasında aynı zamanda güncelleştirmeleri, olanlar başvuran sağlanan zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="fd1a6-110">Eklenen bütünleştirilmiş güncelleştirilmiş bir paket varsa, yeni bir başvurudur *değil* eklendi.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="fd1a6-111">Yeni paket bağımlılıkları da eklenen derleme başvurularını yok.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="fd1a6-112">Bu işlemlerin bir güncelleştirme bir parçası olarak dahil etmek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanılarak paketi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="fd1a6-113">Bu komut, nuget.exe kendisini güncelleştirmek için de kullanılabilir kullanarak *-self* bayrağı.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="fd1a6-114">Kullanım</span><span class="sxs-lookup"><span data-stu-id="fd1a6-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="fd1a6-115">Burada `<configPath>` ya da tanımlayan bir `packages.config` veya proje bağımlılıkları listeler çözüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="fd1a6-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="fd1a6-116">Options</span></span>

| <span data-ttu-id="fd1a6-117">Seçenek</span><span class="sxs-lookup"><span data-stu-id="fd1a6-117">Option</span></span> | <span data-ttu-id="fd1a6-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fd1a6-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd1a6-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fd1a6-119">ConfigFile</span></span> | <span data-ttu-id="fd1a6-120">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fd1a6-121">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="fd1a6-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="fd1a6-122">FileConflictAction</span></span> | <span data-ttu-id="fd1a6-123">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar sorulduğunda gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="fd1a6-124">Değerler *üzerine yazma, yoksay, hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="fd1a6-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fd1a6-125">ForceEnglishOutput</span></span> | <span data-ttu-id="fd1a6-126">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fd1a6-127">Yardım</span><span class="sxs-lookup"><span data-stu-id="fd1a6-127">Help</span></span> | <span data-ttu-id="fd1a6-128">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="fd1a6-129">Kimliği</span><span class="sxs-lookup"><span data-stu-id="fd1a6-129">Id</span></span> | <span data-ttu-id="fd1a6-130">Paketi güncelleştirmeye kimlikleri listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="fd1a6-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="fd1a6-131">MSBuildPath</span></span> | <span data-ttu-id="fd1a6-132">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="fd1a6-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="fd1a6-133">MSBuildVersion</span></span> | <span data-ttu-id="fd1a6-134">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="fd1a6-135">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="fd1a6-136">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="fd1a6-137">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="fd1a6-137">NonInteractive</span></span> | <span data-ttu-id="fd1a6-138">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fd1a6-139">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="fd1a6-139">PreRelease</span></span> | <span data-ttu-id="fd1a6-140">Yayın öncesi sürümler için güncelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="fd1a6-141">Bu bayrak, yüklü olan yayın öncesi paket güncelleştirilirken gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="fd1a6-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="fd1a6-142">RepositoryPath</span></span> | <span data-ttu-id="fd1a6-143">Paketleri yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="fd1a6-144">Güvenli</span><span class="sxs-lookup"><span data-stu-id="fd1a6-144">Safe</span></span> | <span data-ttu-id="fd1a6-145">Yüklü paketin yüklü olarak yalnızca aynı birincil ve ikincil sürüm içinde kullanılabilir en yüksek sürüm ile güncelleştirmelerinin belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="fd1a6-146">Kendi kendini</span><span class="sxs-lookup"><span data-stu-id="fd1a6-146">Self</span></span> | <span data-ttu-id="fd1a6-147">Nuget.exe en son sürüme güncelleştirir; diğer tüm bağımsız değişkenleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="fd1a6-148">Kaynak</span><span class="sxs-lookup"><span data-stu-id="fd1a6-148">Source</span></span> | <span data-ttu-id="fd1a6-149">Paket kaynaklarını listesini güncelleştirmeleri için kullanılacak (URL'ler olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="fd1a6-150">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fd1a6-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="fd1a6-151">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="fd1a6-151">Verbosity</span></span> | <span data-ttu-id="fd1a6-152">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="fd1a6-153">Sürüm</span><span class="sxs-lookup"><span data-stu-id="fd1a6-153">Version</span></span> | <span data-ttu-id="fd1a6-154">Bir paket kimliği ile kullanıldığında, güncelleştirme paketi sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="fd1a6-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="fd1a6-155">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fd1a6-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fd1a6-156">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fd1a6-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
