---
title: "NuGet CLI güncelleştirme komut | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Nuget.exe güncelleştirme komut başvurusu"
keywords: "nuget güncelleştirme başvuru, güncelleştirme paketi komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="c8c51-104">güncelleştirme komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c8c51-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="c8c51-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="c8c51-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="c8c51-106">Güncelleştirmeleri projesindeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine için.</span><span class="sxs-lookup"><span data-stu-id="c8c51-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="c8c51-107">Çalıştırmak için önerilen ['geri'](#restore) çalıştırmadan önce `update`.</span><span class="sxs-lookup"><span data-stu-id="c8c51-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="c8c51-108">(Tek tek bir paketi güncelleştirmeye [ `nuget install` ](cli-ref-install.md) servis talebi NuGet en son sürümünü yükler, bir sürüm numarası belirtmeden.)</span><span class="sxs-lookup"><span data-stu-id="c8c51-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="c8c51-109">Not: `update` (Mac OSX veya Linux) Mono altında çalışması CLI ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="c8c51-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="c8c51-110">Komutu kullanarak projeleri de çalışmıyor `project.json` veya PackageReference yönetim biçimleri.</span><span class="sxs-lookup"><span data-stu-id="c8c51-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="c8c51-111">`update` Komutu derleme başvurularını proje dosyasında aynı zamanda güncelleştirmeleri, olanlar başvuran sağlanan zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="c8c51-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="c8c51-112">Eklenen bütünleştirilmiş güncelleştirilmiş bir paket varsa, yeni bir başvurudur *değil* eklendi.</span><span class="sxs-lookup"><span data-stu-id="c8c51-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="c8c51-113">Yeni paket bağımlılıkları da eklenen derleme başvurularını yok.</span><span class="sxs-lookup"><span data-stu-id="c8c51-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="c8c51-114">Bu işlemlerin bir güncelleştirme bir parçası olarak dahil etmek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanılarak paketi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c8c51-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="c8c51-115">Bu komut, nuget.exe kendisini güncelleştirmek için de kullanılabilir kullanarak *-self* bayrağı.</span><span class="sxs-lookup"><span data-stu-id="c8c51-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="c8c51-116">Kullanım</span><span class="sxs-lookup"><span data-stu-id="c8c51-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="c8c51-117">Burada `<configPath>` ya da tanımlayan bir `packages.config` veya proje bağımlılıkları listeler çözüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="c8c51-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="c8c51-118">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="c8c51-118">Options</span></span>

| <span data-ttu-id="c8c51-119">Seçenek</span><span class="sxs-lookup"><span data-stu-id="c8c51-119">Option</span></span> | <span data-ttu-id="c8c51-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8c51-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8c51-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="c8c51-121">ConfigFile</span></span> | <span data-ttu-id="c8c51-122">*(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="c8c51-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="c8c51-123">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8c51-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="c8c51-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c8c51-124">FileConflictAction</span></span> | <span data-ttu-id="c8c51-125">*(2.5 +)*  Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar sorulduğunda gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c8c51-126">Değerler *üzerine yazma, yoksay, hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="c8c51-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="c8c51-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="c8c51-127">ForceEnglishOutput</span></span> | <span data-ttu-id="c8c51-128">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="c8c51-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="c8c51-129">Yardım</span><span class="sxs-lookup"><span data-stu-id="c8c51-129">Help</span></span> | <span data-ttu-id="c8c51-130">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c8c51-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="c8c51-131">Kimliği</span><span class="sxs-lookup"><span data-stu-id="c8c51-131">Id</span></span> | <span data-ttu-id="c8c51-132">Paketi güncelleştirmeye kimlikleri listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="c8c51-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="c8c51-133">MSBuildPath</span></span> | <span data-ttu-id="c8c51-134">*(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="c8c51-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="c8c51-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="c8c51-135">MSBuildVersion</span></span> | <span data-ttu-id="c8c51-136">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="c8c51-137">Değerleri, 4, 12, 14, 15 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="c8c51-138">MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="c8c51-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="c8c51-139">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="c8c51-139">NonInteractive</span></span> | <span data-ttu-id="c8c51-140">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="c8c51-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="c8c51-141">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="c8c51-141">PreRelease</span></span> | <span data-ttu-id="c8c51-142">Yayın öncesi sürümler için güncelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8c51-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="c8c51-143">Bu bayrak, yüklü olan yayın öncesi paket güncelleştirilirken gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="c8c51-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="c8c51-144">RepositoryPath</span></span> | <span data-ttu-id="c8c51-145">Paketleri yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="c8c51-146">Güvenli</span><span class="sxs-lookup"><span data-stu-id="c8c51-146">Safe</span></span> | <span data-ttu-id="c8c51-147">Yüklü paketin yüklü olarak yalnızca aynı birincil ve ikincil sürüm içinde kullanılabilir en yüksek sürüm ile güncelleştirmelerinin belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="c8c51-148">Kendi kendini</span><span class="sxs-lookup"><span data-stu-id="c8c51-148">Self</span></span> | <span data-ttu-id="c8c51-149">*(1.4 +)*  Nuget.exe en son sürüme; güncelleştirmeleri diğer tüm bağımsız değişkenleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="c8c51-150">Kaynak</span><span class="sxs-lookup"><span data-stu-id="c8c51-150">Source</span></span> | <span data-ttu-id="c8c51-151">Paket kaynaklarını listesini güncelleştirmeleri için kullanılacak (URL'ler olarak) belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="c8c51-152">Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="c8c51-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="c8c51-153">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="c8c51-153">Verbosity</span></span> | <span data-ttu-id="c8c51-154">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="c8c51-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="c8c51-155">Sürüm</span><span class="sxs-lookup"><span data-stu-id="c8c51-155">Version</span></span> | <span data-ttu-id="c8c51-156">Bir paket kimliği ile kullanıldığında, güncelleştirme paketi sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c8c51-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="c8c51-157">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c8c51-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c8c51-158">Örnekler</span><span class="sxs-lookup"><span data-stu-id="c8c51-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
