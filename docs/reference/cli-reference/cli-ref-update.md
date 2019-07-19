---
title: NuGet CLı güncelleştirme komutu
description: NuGet. exe Update komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328257"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="108ea-103">Update komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="108ea-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="108ea-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="108ea-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="108ea-105">Projedeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="108ea-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="108ea-106">Çalıştırılmadan önce `update` [' Restore '](cli-ref-restore.md) çalıştırmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="108ea-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="108ea-107">(Tek bir paketi güncelleştirmek için, sürüm [`nuget install`](cli-ref-install.md) numarası belirtmeden kullanın, bu durumda NuGet en son sürümü yüklerse.)</span><span class="sxs-lookup"><span data-stu-id="108ea-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="108ea-108">Not: `update` Mono (Mac OSX veya Linux) altında çalışan CLI ile veya packagereference biçimi kullanılırken çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="108ea-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="108ea-109">Bu başvurular zaten mevcut olduğundan, komutprojedosyasındakiderlemebaşvurularınıdagüncelleştirir.`update`</span><span class="sxs-lookup"><span data-stu-id="108ea-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="108ea-110">Güncelleştirilmiş bir pakette eklenen bir derleme varsa, yeni bir *başvuru eklenmez.*</span><span class="sxs-lookup"><span data-stu-id="108ea-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="108ea-111">Yeni paket bağımlılıklarına Ayrıca, derleme başvuruları da eklenmez.</span><span class="sxs-lookup"><span data-stu-id="108ea-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="108ea-112">Bu işlemleri bir güncelleştirmenin parçası olarak dahil etmek için, Paket Yöneticisi Kullanıcı arabirimini veya paket Yöneticisi konsolunu kullanarak Visual Studio 'da paketi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="108ea-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="108ea-113">Bu komut, *-self* bayrağını kullanarak NuGet. exe ' yi güncelleştirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="108ea-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="108ea-114">Kullanım</span><span class="sxs-lookup"><span data-stu-id="108ea-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="108ea-115">, projenin bağımlılıklarını listeleyen `packages.config` bir veya çözüm dosyası tanımlar.`<configPath>`</span><span class="sxs-lookup"><span data-stu-id="108ea-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="108ea-116">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="108ea-116">Options</span></span>

| <span data-ttu-id="108ea-117">Seçenek</span><span class="sxs-lookup"><span data-stu-id="108ea-117">Option</span></span> | <span data-ttu-id="108ea-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="108ea-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="108ea-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="108ea-119">ConfigFile</span></span> | <span data-ttu-id="108ea-120">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="108ea-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="108ea-121">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="108ea-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="108ea-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="108ea-122">FileConflictAction</span></span> | <span data-ttu-id="108ea-123">Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylemi belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="108ea-124">Değerler *üzerine yazılır, yok say, yok*.</span><span class="sxs-lookup"><span data-stu-id="108ea-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="108ea-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="108ea-125">ForceEnglishOutput</span></span> | <span data-ttu-id="108ea-126">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="108ea-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="108ea-127">Help</span><span class="sxs-lookup"><span data-stu-id="108ea-127">Help</span></span> | <span data-ttu-id="108ea-128">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="108ea-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="108ea-129">Id</span><span class="sxs-lookup"><span data-stu-id="108ea-129">Id</span></span> | <span data-ttu-id="108ea-130">Güncelleştirilecek paket kimliklerinin bir listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="108ea-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="108ea-131">MSBuildPath</span></span> | <span data-ttu-id="108ea-132">*(4.0 +)* Komutuyla birlikte kullanılacak MSBuild 'in yolunu belirtir `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="108ea-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="108ea-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="108ea-133">MSBuildVersion</span></span> | <span data-ttu-id="108ea-134">*(3.2 +)* Bu komutla kullanılacak MSBuild sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="108ea-135">Desteklenen değerler şunlardır 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="108ea-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="108ea-136">Varsayılan olarak, yolunuzda MSBuild çekilir, aksi takdirde en yüksek MSBuild 'in yüklü sürümü varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="108ea-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="108ea-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="108ea-137">NonInteractive</span></span> | <span data-ttu-id="108ea-138">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="108ea-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="108ea-139">Sp1'in</span><span class="sxs-lookup"><span data-stu-id="108ea-139">PreRelease</span></span> | <span data-ttu-id="108ea-140">Yayın öncesi sürümlere güncelleştirme yapılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="108ea-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="108ea-141">Zaten yüklü olan ön sürüm paketleri güncelleştirilirken bu bayrak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="108ea-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="108ea-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="108ea-142">RepositoryPath</span></span> | <span data-ttu-id="108ea-143">Paketlerin yüklendiği yerel klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="108ea-144">Güven</span><span class="sxs-lookup"><span data-stu-id="108ea-144">Safe</span></span> | <span data-ttu-id="108ea-145">Yüklü paket ile aynı ana ve alt sürüm içinde yalnızca en yüksek sürüme sahip güncelleştirmelerin yükleneceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="108ea-146">Self</span><span class="sxs-lookup"><span data-stu-id="108ea-146">Self</span></span> | <span data-ttu-id="108ea-147">NuGet. exe ' yi en son sürüme güncelleştirir; diğer tüm bağımsız değişkenler yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="108ea-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="108ea-148">Source</span><span class="sxs-lookup"><span data-stu-id="108ea-148">Source</span></span> | <span data-ttu-id="108ea-149">Güncelleştirmeler için kullanılacak paket kaynaklarının (URL 'Ler olarak) listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="108ea-150">Atlanırsa, komut yapılandırma dosyalarında belirtilen kaynakları kullanır, bkz. [ortak NuGet yapılandırmaları](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="108ea-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="108ea-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="108ea-151">Verbosity</span></span> | <span data-ttu-id="108ea-152">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="108ea-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="108ea-153">Sürüm</span><span class="sxs-lookup"><span data-stu-id="108ea-153">Version</span></span> | <span data-ttu-id="108ea-154">Tek bir paket KIMLIĞIYLE birlikte kullanıldığında, güncelleştirilecek paketin sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="108ea-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="108ea-155">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="108ea-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="108ea-156">Örnekler</span><span class="sxs-lookup"><span data-stu-id="108ea-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
