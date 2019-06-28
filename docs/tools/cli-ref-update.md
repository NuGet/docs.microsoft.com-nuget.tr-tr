---
title: NuGet CLI güncelleştirme komutu
description: Nuget.exe güncelleştirme komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425915"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="ef650-103">Güncelleştirme komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ef650-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="ef650-104">**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="ef650-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ef650-105">Güncelleştirmeleri bir projedeki tüm paketleri (kullanarak `packages.config`), en son kullanılabilir sürümler için.</span><span class="sxs-lookup"><span data-stu-id="ef650-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ef650-106">Çalıştırmak için önerilen ['restore'](cli-ref-restore.md) çalıştırmadan önce `update`.</span><span class="sxs-lookup"><span data-stu-id="ef650-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="ef650-107">(Tek bir paket güncelleştirmek için [ `nuget install` ](cli-ref-install.md) büyük/küçük harf NuGet en son sürümünü yükler, bir sürüm numarası belirtmeden.)</span><span class="sxs-lookup"><span data-stu-id="ef650-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="ef650-108">Not: `update` Mono (Mac OSX veya Linux) altında veya PackageReference biçimi kullanılırken çalıştıran CLI ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ef650-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="ef650-109">`update` Komut proje dosyasındaki derleme başvurularını de güncelleştirir, bu başvuruları sağlanan zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="ef650-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="ef650-110">Güncelleştirilmiş bir paket eklenen bir derleme varsa, yeni bir başvurudur *değil* eklendi.</span><span class="sxs-lookup"><span data-stu-id="ef650-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="ef650-111">Yeni paket bağımlılıkları da derleme başvurularını eklenen yok.</span><span class="sxs-lookup"><span data-stu-id="ef650-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="ef650-112">Bu işlemler, bir güncelleştirmenin bir parçası dahil etmek için Visual Studio'da Paket Yöneticisi UI veya Paket Yöneticisi konsolu kullanarak paket güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ef650-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="ef650-113">Bu komut ayrıca nuget.exe kendisini güncelleştirmek için kullanılabilir kullanarak *-kendi kendine* bayrağı.</span><span class="sxs-lookup"><span data-stu-id="ef650-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="ef650-114">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ef650-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="ef650-115">Burada `<configPath>` ya da tanımlayan bir `packages.config` veya çözüm dosyası, proje bağımlılıkları listeler.</span><span class="sxs-lookup"><span data-stu-id="ef650-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="ef650-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ef650-116">Options</span></span>

| <span data-ttu-id="ef650-117">Seçenek</span><span class="sxs-lookup"><span data-stu-id="ef650-117">Option</span></span> | <span data-ttu-id="ef650-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef650-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef650-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ef650-119">ConfigFile</span></span> | <span data-ttu-id="ef650-120">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="ef650-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ef650-121">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef650-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ef650-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="ef650-122">FileConflictAction</span></span> | <span data-ttu-id="ef650-123">Üzerine ya da proje tarafından başvurulan mevcut dosyaları yoksaymak için sorulduğunda gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="ef650-124">Değerler *üzerine, Ignore hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="ef650-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="ef650-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ef650-125">ForceEnglishOutput</span></span> | <span data-ttu-id="ef650-126">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="ef650-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ef650-127">Help</span><span class="sxs-lookup"><span data-stu-id="ef650-127">Help</span></span> | <span data-ttu-id="ef650-128">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef650-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="ef650-129">Id</span><span class="sxs-lookup"><span data-stu-id="ef650-129">Id</span></span> | <span data-ttu-id="ef650-130">Paketi güncelleştirmeye kimlikleri listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="ef650-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="ef650-131">MSBuildPath</span></span> | <span data-ttu-id="ef650-132">*(4.0 +)*  Önceliği alma komutu ile kullanılacak MSBuild yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="ef650-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="ef650-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="ef650-133">MSBuildVersion</span></span> | <span data-ttu-id="ef650-134">*(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="ef650-135">Desteklenen değerler şunlardır: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15,8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="ef650-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="ef650-136">Yolunuza Msbuild'de çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar.</span><span class="sxs-lookup"><span data-stu-id="ef650-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="ef650-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ef650-137">NonInteractive</span></span> | <span data-ttu-id="ef650-138">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="ef650-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ef650-139">Yayın öncesi</span><span class="sxs-lookup"><span data-stu-id="ef650-139">PreRelease</span></span> | <span data-ttu-id="ef650-140">Yayın öncesi sürümler için güncelleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef650-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="ef650-141">Bu bayrak, zaten yüklü olan yayın öncesi paketleri güncelleştirirken gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ef650-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="ef650-142">Dosyasının repositorypath ayarı</span><span class="sxs-lookup"><span data-stu-id="ef650-142">RepositoryPath</span></span> | <span data-ttu-id="ef650-143">Paket yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="ef650-144">Güvenli</span><span class="sxs-lookup"><span data-stu-id="ef650-144">Safe</span></span> | <span data-ttu-id="ef650-145">Yüklü paketleri yüklü olarak, yalnızca aynı birincil ve ikincil sürüm içinde mevcut olan en yüksek sürüm güncelleştirir belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="ef650-146">Kendi kendine</span><span class="sxs-lookup"><span data-stu-id="ef650-146">Self</span></span> | <span data-ttu-id="ef650-147">En son sürüme güncelleştirme nuget.exe; diğer tüm bağımsız değişkenler yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="ef650-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="ef650-148">Source</span><span class="sxs-lookup"><span data-stu-id="ef650-148">Source</span></span> | <span data-ttu-id="ef650-149">Paket kaynaklarının listesi güncelleştirmeleri için kullanılacak (URL'ler) belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="ef650-150">Atlanırsa, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [ortak NuGet yapılandırmaları](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ef650-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="ef650-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ef650-151">Verbosity</span></span> | <span data-ttu-id="ef650-152">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="ef650-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="ef650-153">Sürüm</span><span class="sxs-lookup"><span data-stu-id="ef650-153">Version</span></span> | <span data-ttu-id="ef650-154">Bir paket kimliği ile kullanıldığında, güncelleştirilecek paket sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef650-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="ef650-155">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ef650-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ef650-156">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ef650-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
