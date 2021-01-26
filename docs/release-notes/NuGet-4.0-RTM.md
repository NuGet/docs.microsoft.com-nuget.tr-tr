---
title: NuGet 4,0 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,0 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776274"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="6b7f0-103">NuGet 4,0 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6b7f0-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="6b7f0-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , .NET Core desteği ekleyen NuGet 4,0 ile birlikte gelir, bir dizi kalite düzeltmesine sahiptir ve performansı geliştirir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="6b7f0-105">Bu sürümde, PackageReference için destek, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yüklemeleri ve daha fazlası gibi çeşitli geliştirmeler de yer alır.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6b7f0-106">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="6b7f0-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="6b7f0-107">Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-108">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-108">Issue</span></span>

<span data-ttu-id="6b7f0-109">Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="6b7f0-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="6b7f0-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-111">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-111">Workaround</span></span>

<span data-ttu-id="6b7f0-112">Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="6b7f0-113">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-114">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-114">Issue</span></span>

<span data-ttu-id="6b7f0-115">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="6b7f0-116">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="6b7f0-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="6b7f0-118">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-118">Workaround</span></span>

<span data-ttu-id="6b7f0-119">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="6b7f0-120">Alternatif olarak, ' yi silmeyi `project.lock.json` ve geri yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="6b7f0-121">.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="6b7f0-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-122">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-122">Issue</span></span>

<span data-ttu-id="6b7f0-123">Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="6b7f0-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="6b7f0-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-125">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-125">Workaround</span></span>

<span data-ttu-id="6b7f0-126">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="6b7f0-127">NuGet Paket Yöneticisi 'Ni kullanarak Dotnetclıtools 'u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz</span><span class="sxs-lookup"><span data-stu-id="6b7f0-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-128">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-128">Issue</span></span>

<span data-ttu-id="6b7f0-129">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="6b7f0-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="6b7f0-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-131">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-131">Workaround</span></span>

<span data-ttu-id="6b7f0-132">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="6b7f0-133">Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur</span><span class="sxs-lookup"><span data-stu-id="6b7f0-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-134">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-134">Issue</span></span>

<span data-ttu-id="6b7f0-135">.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="6b7f0-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="6b7f0-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-137">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-137">Workaround</span></span>

<span data-ttu-id="6b7f0-138">Geri yükleme komutunu, komut satırını kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="6b7f0-139">Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-140">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-140">Issue</span></span>

<span data-ttu-id="6b7f0-141">'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="6b7f0-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="6b7f0-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-143">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-143">Workaround</span></span>

<span data-ttu-id="6b7f0-144">'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="6b7f0-145">Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-146">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-146">Issue</span></span>

<span data-ttu-id="6b7f0-147">Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="6b7f0-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="6b7f0-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-149">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-149">Workaround</span></span>

<span data-ttu-id="6b7f0-150">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="6b7f0-151">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-152">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-152">Issue</span></span>

<span data-ttu-id="6b7f0-153">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="6b7f0-154">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="6b7f0-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="6b7f0-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-156">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-156">Workaround</span></span>

<span data-ttu-id="6b7f0-157">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="6b7f0-158">.NET461’i hedefleyen bir proje, .NETStandard’ı hedefleyen başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur</span><span class="sxs-lookup"><span data-stu-id="6b7f0-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="6b7f0-159">Sorun</span><span class="sxs-lookup"><span data-stu-id="6b7f0-159">Issue</span></span>

<span data-ttu-id="6b7f0-160">.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="6b7f0-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="6b7f0-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="6b7f0-162">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="6b7f0-162">Workaround</span></span>

<span data-ttu-id="6b7f0-163">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="6b7f0-164">NuGet 4,0 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="6b7f0-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="6b7f0-165">[Nuget 4,0 RC sürüm notları](../release-notes/nuget-4.0-RC.md) -NUGET 4,0 RC için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="6b7f0-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="6b7f0-166">Özellikler</span><span class="sxs-lookup"><span data-stu-id="6b7f0-166">Features</span></span>

- <span data-ttu-id="6b7f0-167">NuGet. Core. sln- [#2041](https://github.com/NuGet/Home/issues/2041) dizeleri yerelleştirin</span><span class="sxs-lookup"><span data-stu-id="6b7f0-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="6b7f0-168">NuGet, Web uygulaması projelerini LSL modunda yüklemeye zorlar- [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="6b7f0-169">"SDK yüklü" paketlere yönelik kullanıcı arabiriminde sürüm değişikliklerini engellemek için, oto başvurulan PackageReference desteği- [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="6b7f0-170">Herhangi bir proje bağımlılığı için PackageSpec. Version doğru şekilde iletişim kurar (PackageRef)- [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="6b7f0-171">`.csproj`komut satırı (ler) e- [#4101](https://github.com/NuGet/Home/issues/4101) başvuruları kaldırma desteği</span><span class="sxs-lookup"><span data-stu-id="6b7f0-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="6b7f0-172">PackageReference projeleri (normal ve xplat) ve hafif çözüm yükü- [#4003](https://github.com/NuGet/Home/issues/4003) için geri yükleme desteği</span><span class="sxs-lookup"><span data-stu-id="6b7f0-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="6b7f0-173">`.csproj`komut satırı (ler) e- [#3751](https://github.com/NuGet/Home/issues/3751) başvuru ekleme desteği</span><span class="sxs-lookup"><span data-stu-id="6b7f0-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="6b7f0-174">`packages.config`Veya `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711) için hafif çözüm yükü için NuGet geri yüklemeyi destekleme</span><span class="sxs-lookup"><span data-stu-id="6b7f0-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="6b7f0-175">NuGet tarafından oluşturulan hedef dosya [#3683](https://github.com/NuGet/Home/issues/3683) ContentFiles desteği</span><span class="sxs-lookup"><span data-stu-id="6b7f0-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="6b7f0-176">MSBuild- [#3646](https://github.com/NuGet/Home/issues/3646) kullanarak Mac 'te nuget.exe doğrulaması IÇIN mono CI oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b7f0-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="6b7f0-177">NuGet 'i v2 NuGet. Core bağımlılıklarından Taşı- [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="6b7f0-178">Hatalar</span><span class="sxs-lookup"><span data-stu-id="6b7f0-178">Bugs</span></span>

- <span data-ttu-id="6b7f0-179">Visual Studio 'da NuGet geri yükleme projelerin PackageID özelliğine uymuyor- [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="6b7f0-180">VSIX paketine paket eklenirken NuGet ProjectSystemCache hatası- [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="6b7f0-181">Includesource birden çok TFMs içeren bir projede kullanılıyorsa, paket özel durum oluşturur [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="6b7f0-182">VS 2017 RC3, çözüm genelinde paket yönetimi 'nden güncelleştirme kullanma ile kilitleniyor- [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="6b7f0-183">Yeni yüklenen paket [#4435](https://github.com/NuGet/Home/issues/4435) kaldırılamıyor</span><span class="sxs-lookup"><span data-stu-id="6b7f0-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="6b7f0-184">PackageRef 'e geçiş yaparken, karma çözümlerin garip geri yükleme davranışı vardır- [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="6b7f0-185">NuGet işlemini başlattıktan hemen sonra oluşturma (yükleme, güncelleştirme, geri yükleme), askıda kalmasına neden olabilir [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="6b7f0-186">UI askıda-kilitlenme NuGet. SolutionRestoreManager. RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371) başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="6b7f0-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="6b7f0-187">Add Package komutu, element- [#4325](https://github.com/NuGet/Home/issues/4325) yerine Attribute olarak eklenmelidir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="6b7f0-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-188">dotnet</span></span>
  - <span data-ttu-id="6b7f0-189">dotnetcore geri yükleme foo. sln--SLN içindeki yapılandırma, restore Graph 'te yinelenen (ancak fark yapılandırması) projelere neden olduğunda başarısız olur- [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="6b7f0-190">Yalnızca içerik paketleri- [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="6b7f0-191">Varsayılan olarak, paket biçimi seçici seçeneğini devre dışı bırak- [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="6b7f0-192">Perf: CreateUAP_CSharp_VS. 01.1.3.153,570 MS (149,1%) tarafından proje gerilediğini Duration_TotalElapsedTime oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="6b7f0-193">Taban çizgisi 26129,02- [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="6b7f0-194">Perf: ManagedLangs_CS_DDRIT .0300. yeniden derleme çözümü Duration_TotalElapsedTime 1.5 sn tarafından yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="6b7f0-195">Taban çizgisi 26105- [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="6b7f0-196">Birden çok TFA projesinde aday başarısız oldu- [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="6b7f0-197">Perf: WebForms_DDRIT .1200. Close çözüm gerilediğini VM_ImagesInMemory_Total_devenv 3,000 sayı (0,5%).</span><span class="sxs-lookup"><span data-stu-id="6b7f0-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="6b7f0-198">Taban çizgisi 26123,04- [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="6b7f0-199">vsfeedback-netcoreapp 1.1 'i hedeflerken paket uyarıları- [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="6b7f0-200">Boş ASP.NET Core Web uygulamasına bir NuGet paketi eklenmeye çalışılırken PathTooLongException- [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="6b7f0-201">Paket çok sık çalışır--DotNet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="6b7f0-202">dotnetcore paketi, target "Pack" ile ilgili hedef bağımlılık grafiğinde döngüsel bağımlılık olduğundan başarısız oluyor [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="6b7f0-203">Paket çok sık çalışır--NuGet paketi oluşturma tüm konfigürasyonları içermez- [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="6b7f0-204">C++ projesinde packageref ile NuGet ekleme- [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="6b7f0-205">Erişilebilirlik: ekran okuyucusu, paketi [#4366](https://github.com/NuGet/Home/issues/4366) paketi yükleyecek projeleri seçme onay kutusunu göstermez</span><span class="sxs-lookup"><span data-stu-id="6b7f0-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="6b7f0-206">NuGet VS17 sporadsoysal, VSO/VSTS akışlarına bağlanma başarısız oluyor-VS hatası 365798- [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="6b7f0-207">PackagePath yolu "contentFiles" olarak belirtiyorsa contentFiles yanlış konuma çıkış alır- [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="6b7f0-208">Paket hedefi bir PackageVersion özelliğini VersionSuffix ile ekler- [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="6b7f0-209">Paket yolunun belirtilmesi DotNet Pack ile çalışmıyor- [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="6b7f0-210">NuGet geri yükleme sırasında yinelenen içeri aktarmalar hakkında bir uyarı verir- [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="6b7f0-211">"NuGet Paket Yöneticisi biçimi" iletişim kutusu Koyu tema altında hatalı görünüyor- [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="6b7f0-212">Derleme geri yükleme sırasında VS kilitlenmesi- [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="6b7f0-213">TargetFramework 'e tfd eklerseniz, bu durumda Visual Studio kilitlenmeleri, kaydedebilir ve derdir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="6b7f0-214">%10 zaman [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="6b7f0-215">NuGet paketi bir projeyi başarıyla paketleme sırasında başarı iletisini çıktı değil- [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="6b7f0-216">System. ıO. Compression 4,1 bulunamadığı için Pacbir SK başarısız oldu- [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="6b7f0-217">Paket çok sık çalışır; dosya erişimi çakışmasıyla birlikte Packısk sık başarısız olur- [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="6b7f0-218">NuGet arka plan geri yükleme sırasında çıkış penceresini açar- [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="6b7f0-219">ServiceProvider tehlikeli kodlama düzeniyle (askıda kalmasına neden olabilir) kaldırın [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="6b7f0-220">Perf/Uıaskıda-#4266 DownloadTimeoutStream okumaları- [](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="6b7f0-221">NuGet geri yükleme işlemi tamamlanmadan önce bir projeyi kapatmaya çalışırsanız, Visual Studio kilitlenmeler- [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="6b7f0-222">Pacbir SK ve paketleme `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250) sorunları</span><span class="sxs-lookup"><span data-stu-id="6b7f0-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="6b7f0-223">[vsfeedback] Yeni projedeki NuGet paketleri çözümlenemiyor (Visual Studio 'nun yeniden başlatılması gerekiyor)- [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="6b7f0-224">[vsfeedback] Kullanılabilir paket sürümlerini gösteren "sürüm" açılan penceresinde, seçili nuGet paketiyle eşitlenmiş halde kalmak için bir sorun var...- [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="6b7f0-225">NuGet. Client, [#4185](https://github.com/NuGet/Home/issues/4185) kilitlenmeleri engellemek için CPS ile etkileşerek CPS JoinableTaskFactory kullanmalıdır</span><span class="sxs-lookup"><span data-stu-id="6b7f0-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="6b7f0-226">NuGet 3.5.0 paketten paketten `.targets` açma- [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="6b7f0-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-227">dotnet</span></span>
  - <span data-ttu-id="6b7f0-228">dotnetcore paketi `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150) başlığını desteklemiyor</span><span class="sxs-lookup"><span data-stu-id="6b7f0-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="6b7f0-229">VS2017 RC 'de hata iletişim kutusunda Install-Package sonuçları [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="6b7f0-230">.NET Core projesi için bir paketi güncelleştirme, Kullanıcı arabirimi aday 'dan CPS güncelleştirmesini almamasına yönelik olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="6b7f0-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="6b7f0-232">Çözümlenmemiş başvuruyu İyileştirme Uyarısı- [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="6b7f0-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-233">dotnet</span></span>
  - <span data-ttu-id="6b7f0-234">dotnetcore paketi-ProjectReference sürüm bilgilerini kaybeder- [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="6b7f0-235">UWP uygulaması oluşturma proje oluşturma & toplam geçen süre gerilemesi- [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="6b7f0-236">Geri yükleme sırasında hata sonrasında bile başarılı geri yükleme iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="6b7f0-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="6b7f0-238">NuGet. CommandLine 3.4.4 to Nuget.org- [#2931](https://github.com/NuGet/Home/issues/2931) yeniden yayımlayın</span><span class="sxs-lookup"><span data-stu-id="6b7f0-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="6b7f0-239">Geçiş sırasında projeler `project.json` `.csproj` ---geri yükleme başarısız olur- [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="6b7f0-240">Yeni oluşturulan xUnit Test projesinde geri yükleme başarısız oldu- [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="6b7f0-241">Temel projeler askıda kalabilir, açık [#4269](https://github.com/NuGet/Home/issues/4269) Kullanıcı arabirimini kilitleyebilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="6b7f0-242">derleme görevleri için hedef dosyasını düzeltir- [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="6b7f0-243">Hata listesi, başvurulan projeyi kaldırmak için derleme çözümünü tamamladıktan sonra hata oluştu- [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="6b7f0-244">MSB4057: "_GenerateRestoreGraphProjectEntry" hedefi projede yok.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="6b7f0-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="6b7f0-246">vsfeedback: tüm projeler ' i seçtiğinizde çözüm kilitlenmeleri için NuGet Yöneticisi Kullanıcı arabirimi- [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="6b7f0-247">Sondaki eğik çizgi olduğunda MSBuildPath nuget.exe başarısız olur [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="6b7f0-248">vsfeedback: NuGet geri yüklemesi, LinqToTwitter projesi için çeşitli proje başvurusu uyarıları sağlar- [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="6b7f0-249">Paketi `.csproj` , minClientVersion özniteliğini içermez- [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="6b7f0-250">VS2017 içinde oturum açılan NuGet.Build.Tasks.Pack.dll gönderilen gecikme (d15rel 26014,00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="6b7f0-251">VSFeedback: CMake 3.7.1 ile oluşturulan VS 2015 projesinde geri yükleme başarısız oluyor [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="6b7f0-252">VSFeedback: geri yükleme hataları, derleme [#4113](https://github.com/NuGet/Home/issues/4113) verebilmesi için daha fazla tam hata iletisi içerebilir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="6b7f0-253">[VSFeedback] Web sitesi projesi için NuGet paketleri geri yüklenirken hata oluştu: değer null olamaz.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="6b7f0-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="6b7f0-255">Geçiş, NuGet. PackageManagement. VisualStudio. SolutionRestoreWorker- [#4067](https://github.com/NuGet/Home/issues/4067) Içinde "nesne başvurusu özel durumu" oluşturur</span><span class="sxs-lookup"><span data-stu-id="6b7f0-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="6b7f0-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-256">dotnet</span></span>
  - <span data-ttu-id="6b7f0-257">dotnetcore Pack, paketin [#4063](https://github.com/NuGet/Home/issues/4063) karşı derlenme sürümlerine sahip araçları paketlemelidir.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="6b7f0-258">Yeni arka plan geri yükleme, geri yükleme için saniye sürerse süreyi durum çubuğuna yazar- [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="6b7f0-259">Typo on, tüm proje başvurularını çözümleyemedi- [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="6b7f0-260">Paket başvuru senaryolarında PCM iş akışlarını Etkinleştir- [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="6b7f0-261">Paket Yöneticisi Kullanıcı arabiriminde yüklü paketler bulunamıyor- [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="6b7f0-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-262">dotnet</span></span>
  - <span data-ttu-id="6b7f0-263">PackagePath boş olduğunda dotnetcore paketi başarısız olur- [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="6b7f0-264">Birden çok Kullanıcı senaryosunda geri yükleme görevi başarısız oluyor- [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="6b7f0-265">NuGet paketi kullanılırken Içerik türü değiştirilemez- [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="6b7f0-266">MsBuild/t: Pack- [#3894](https://github.com/NuGet/Home/issues/3894) Için varsayılan ContentFiles kopyası hatalı</span><span class="sxs-lookup"><span data-stu-id="6b7f0-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="6b7f0-267">Paketi Yükle geri yükleme paket geri yükleme geri yükleme paketleri iletisi- [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="6b7f0-268">Guardrayları kaldır-"çalışma zamanları" bölümünün geri yüklenmesi yalnızca geçerli projeye uygulanmalıdır- [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="6b7f0-269">Paket görevi, içerik dosyalarını hem ' content/' hem de ' contentFiles/' öğesine koyar- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="6b7f0-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-270">dotnet</span></span>
  - <span data-ttu-id="6b7f0-271">dotnetcore Pack3, ek etiket bölme [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="6b7f0-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-272">dotnet</span></span>
  - <span data-ttu-id="6b7f0-273">dotnetcore paketi: paket başvuruları olan paketleme projeleri, yinelenen içeri aktarma uyarısı ile sonuçlanır. [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="6b7f0-274">VS 'de geri yükleme günlüğü her zaman [#3633](https://github.com/NuGet/Home/issues/3633) gösterme</span><span class="sxs-lookup"><span data-stu-id="6b7f0-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="6b7f0-275">NuGet Yereller yardım metni hala bahsedilen paketler cache- [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="6b7f0-276">TargetFramework ile Restore3 bağles Packagereferles.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="6b7f0-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="6b7f0-278">NuGet, VS "15" Preview 4 dev sürümünde MSBuild 'in beklenmedik sürümünü seçer.</span><span class="sxs-lookup"><span data-stu-id="6b7f0-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="6b7f0-279">komut istemi- [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="6b7f0-280">Başarısız geri yükleme sırasında hedef/özellik dosyalarını yaz- [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="6b7f0-281">Geri yükleme sırasında NuGet, VS 15 komut isteminde çalışırken MSBuild ile aynı uyumlu değildir- [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="6b7f0-282">VS15- [#3272](https://github.com/NuGet/Home/issues/3272) Için PackFromProjectWithDevelopmentDependencySet 'i yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="6b7f0-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="6b7f0-283">NuGet ile sorunları Blend- [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="6b7f0-284">4.0.0.2067 ile birlikte çalışmak için CLı ve SDK depolarıyla tümleştirin- [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="6b7f0-285">Yeni çekirdek konsol uygulaması oluşturduğunuzda, çözümü kapatıp çözümü açıp çözümü kapattığınızda VS askıda kalıyor. [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="6b7f0-286">D15prerel. 25916.01- [#3982](https://github.com/NuGet/Home/issues/3982) karşı projenin açılmasını kapatma</span><span class="sxs-lookup"><span data-stu-id="6b7f0-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="6b7f0-287">DotNet/nuget.exe Yereller belgesi/yardım iletisi- [#3919](https://github.com/NuGet/Home/issues/3919) düzeltir</span><span class="sxs-lookup"><span data-stu-id="6b7f0-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="6b7f0-288">Sondaki veya önde gelen boşluklar ile ilgili sorunlar için Paclorsk 'yi inceleyin- [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="6b7f0-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-289">dotnet</span></span>
  - <span data-ttu-id="6b7f0-290">dotnetcore paketi obj 'den Not [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="6b7f0-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-291">dotnet</span></span>
  - <span data-ttu-id="6b7f0-292">dotnetcore paketi her zaman ProjectReference sürümünü 1.0.0- [#3874](https://github.com/NuGet/Home/issues/3874) olarak ayarlanmış görünüyor</span><span class="sxs-lookup"><span data-stu-id="6b7f0-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="6b7f0-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="6b7f0-293">dotnet</span></span>
  - <span data-ttu-id="6b7f0-294">dotnetcore paketi proje başvuruları ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865) başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="6b7f0-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="6b7f0-295">ProjectSystemCache. TryGetProjectNameByShortName- [#3861](https://github.com/NuGet/Home/issues/3861) Içindeki LockRecursionException özel durumu</span><span class="sxs-lookup"><span data-stu-id="6b7f0-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="6b7f0-296">MSBuild özelliklerinden boşluğu Kırp- [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="6b7f0-297">Proje yükleme- [#3759](https://github.com/NuGet/Home/issues/3759) oluşturulan iki proje olayını birleştirin</span><span class="sxs-lookup"><span data-stu-id="6b7f0-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="6b7f0-298">Dosyadaki P2P kitaplıklarının `project.assets.json` sürümü yanlış [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="6b7f0-299">Yanıt vermeyen akış ve kullanılamıyor paketi nedeniyle kilitlenme geri yükleme- [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="6b7f0-300">nuget.exe, büyük miktarda MSBuild hata çıkışı üzerinden askıda kalabilir [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="6b7f0-301">Blend için geri yükleme, ilk kez başarısız oldu, ikinci kez başarılı oldu (VS senaryosu düzeltildi)- [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="6b7f0-302">DCR</span><span class="sxs-lookup"><span data-stu-id="6b7f0-302">DCRs</span></span>

- <span data-ttu-id="6b7f0-303">VSIX 'i v2 VSIX 'ten v3 VSIX 'e geçirin- [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="6b7f0-304">NuGet, MSBuild- [#3351](https://github.com/NuGet/Home/issues/3351) kilit dosyasının yolunu almak için bir mekanizmaya sahip olmalıdır</span><span class="sxs-lookup"><span data-stu-id="6b7f0-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="6b7f0-305">TFD uyumluluk denetimi ve varlık dosyasına derleme varlıkları ekleme- [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="6b7f0-306">Pakette ilgili özellikleri etkinleştirmek için paket hedeflerinde yeni bir ProjectCapability "Pack" tanımlayın- [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="6b7f0-307">Paketi "GeneratePackageOnBuild" MSBuild özelliğinde koşullu bir post derlemesi hedefi olarak Çalıştır- [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="6b7f0-308">Belirli bir NuGet projesi oluşturmak için, RestoreProjectStyle NuGet özelliğini kullanın- [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="6b7f0-309">Geçişli proje başvuruları değişikliğini uyarlayın- [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="6b7f0-310">UWP olmayan projeler için hedef dosyada NuGet özellikleri ekleme- [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="6b7f0-311">UWP TargetPlatformVersion desteği- [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="6b7f0-312">Proje başvurusu meta verilerini NuGet proje sistemiyle iletişim [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="6b7f0-313">Paketleme modu için Kullanıcı arabirimi ekleme- [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="6b7f0-314">Eski adı `.csproj` , PROJ/targets- [#3854](https://github.com/NuGet/Home/issues/3854) ayarlanan Nugettargetbilinen ad ve runtimetanımlayıcılarına ihtiyaç duyuyor</span><span class="sxs-lookup"><span data-stu-id="6b7f0-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="6b7f0-315">Yükleme paketi, otomatik geri yükleme ile çakışabilir [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="6b7f0-316">VSPackage yüklü olmadığında bağlam menüsü QueryStatus gerçekleşmiyor- [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="6b7f0-317">Çözüm geri yükleme ve derleme geri yükleme hala iletişim kutularını göster- [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="6b7f0-318">NuGet 'de VSSDK sürümünü yalıtın. clients çözüm derlemesi- [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="6b7f0-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="6b7f0-319">RTM 'de düzeltilen GitHub sorunlarına bağlantılar</span><span class="sxs-lookup"><span data-stu-id="6b7f0-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="6b7f0-320">Sorun listesi 1</span><span class="sxs-lookup"><span data-stu-id="6b7f0-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="6b7f0-321">Sorun listesi 2</span><span class="sxs-lookup"><span data-stu-id="6b7f0-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="6b7f0-322">Sorun listesi 3</span><span class="sxs-lookup"><span data-stu-id="6b7f0-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="6b7f0-323">Sorun listesi 4</span><span class="sxs-lookup"><span data-stu-id="6b7f0-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="6b7f0-324">Sorun listesi 5</span><span class="sxs-lookup"><span data-stu-id="6b7f0-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
