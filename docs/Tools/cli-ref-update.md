---
title: NuGet CLI güncelleştirme komut | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Reference for the nuget.exe update command
keywords: nuget güncelleştirme başvuru, güncelleştirme paketi komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1ea04f2fa2a753065ee4f17cbb926e37acf129e0
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="9044f-104">güncelleştirme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9044f-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="9044f-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="9044f-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9044f-106">Güncelleştirmeleri projesindeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine için.</span><span class="sxs-lookup"><span data-stu-id="9044f-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="9044f-107">Çalıştırmak için önerilen ['geri'](cli-ref-restore.md) çalıştırmadan önce `update`.</span><span class="sxs-lookup"><span data-stu-id="9044f-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="9044f-108">(Tek tek bir paketi güncelleştirmeye [ `nuget install` ](cli-ref-install.md) servis talebi NuGet en son sürümünü yükler, bir sürüm numarası belirtmeden.)</span><span class="sxs-lookup"><span data-stu-id="9044f-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="9044f-109">Not: `update` Mono (Mac OSX veya Linux) altında veya PackageReference biçimi kullanılırken çalıştıran CLI ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="9044f-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="9044f-110">`update` Komutu derleme başvurularını proje dosyasında aynı zamanda güncelleştirmeleri, olanlar başvuran sağlanan zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="9044f-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="9044f-111">Eklenen bütünleştirilmiş güncelleştirilmiş bir paket varsa, yeni bir başvurudur *değil* eklendi.</span><span class="sxs-lookup"><span data-stu-id="9044f-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="9044f-112">Yeni paket bağımlılıkları da eklenen derleme başvurularını yok.</span><span class="sxs-lookup"><span data-stu-id="9044f-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="9044f-113">Bu işlemlerin bir güncelleştirme bir parçası olarak dahil etmek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanılarak paketi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9044f-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="9044f-114">Bu komut, nuget.exe kendisini güncelleştirmek için de kullanılabilir kullanarak *-self* bayrağı.</span><span class="sxs-lookup"><span data-stu-id="9044f-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="9044f-115">Kullanım</span><span class="sxs-lookup"><span data-stu-id="9044f-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="9044f-116">Burada `<configPath>` ya da tanımlayan bir `packages.config` veya proje bağımlılıkları listeler çözüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="9044f-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="9044f-117">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="9044f-117">Options</span></span>

| <span data-ttu-id="9044f-118">Seçenek</span><span class="sxs-lookup"><span data-stu-id="9044f-118">Option</span></span> | <span data-ttu-id="9044f-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9044f-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9044f-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9044f-120">ConfigFile</span></span> | <span data-ttu-id="9044f-121">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="9044f-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9044f-122">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9044f-122">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9044f-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="9044f-123">FileConflictAction</span></span> | <span data-ttu-id="9044f-124">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar sorulduğunda gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="9044f-125">Değerler *üzerine yazma, yoksay, hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="9044f-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="9044f-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9044f-126">ForceEnglishOutput</span></span> | <span data-ttu-id="9044f-127">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="9044f-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9044f-128">Yardım</span><span class="sxs-lookup"><span data-stu-id="9044f-128">Help</span></span> | <span data-ttu-id="9044f-129">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9044f-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="9044f-130">Kimliği</span><span class="sxs-lookup"><span data-stu-id="9044f-130">Id</span></span> | <span data-ttu-id="9044f-131">Paketi güncelleştirmeye kimlikleri listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="9044f-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="9044f-132">MSBuildPath</span></span> | <span data-ttu-id="9044f-133">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="9044f-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="9044f-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="9044f-134">MSBuildVersion</span></span> | <span data-ttu-id="9044f-135">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="9044f-136">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9044f-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="9044f-137">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="9044f-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="9044f-138">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="9044f-138">NonInteractive</span></span> | <span data-ttu-id="9044f-139">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="9044f-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9044f-140">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="9044f-140">PreRelease</span></span> | <span data-ttu-id="9044f-141">Yayın öncesi sürümler için güncelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="9044f-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="9044f-142">Bu bayrak, yüklü olan yayın öncesi paket güncelleştirilirken gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9044f-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="9044f-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="9044f-143">RepositoryPath</span></span> | <span data-ttu-id="9044f-144">Paketleri yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="9044f-145">Güvenli</span><span class="sxs-lookup"><span data-stu-id="9044f-145">Safe</span></span> | <span data-ttu-id="9044f-146">Yüklü paketin yüklü olarak yalnızca aynı birincil ve ikincil sürüm içinde kullanılabilir en yüksek sürüm ile güncelleştirmelerinin belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="9044f-147">Kendi kendini</span><span class="sxs-lookup"><span data-stu-id="9044f-147">Self</span></span> | <span data-ttu-id="9044f-148">Nuget.exe en son sürüme güncelleştirir; diğer tüm bağımsız değişkenleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="9044f-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="9044f-149">Kaynak</span><span class="sxs-lookup"><span data-stu-id="9044f-149">Source</span></span> | <span data-ttu-id="9044f-150">Paket kaynaklarını listesini güncelleştirmeleri için kullanılacak (URL'ler olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="9044f-151">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="9044f-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="9044f-152">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="9044f-152">Verbosity</span></span> | <span data-ttu-id="9044f-153">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="9044f-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="9044f-154">Sürüm</span><span class="sxs-lookup"><span data-stu-id="9044f-154">Version</span></span> | <span data-ttu-id="9044f-155">Bir paket kimliği ile kullanıldığında, güncelleştirme paketi sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9044f-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="9044f-156">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9044f-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9044f-157">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9044f-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
