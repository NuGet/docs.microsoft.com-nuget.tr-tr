---
title: NuGet 4.0 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.0 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: f1c5408f75966068e8fa11e63118426bbf562047
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045093"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="e8dc3-103">NuGet 4.0 RTM sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e8dc3-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="e8dc3-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.0 ile .NET Core için destek ekler, kalite düzeltmeler bir grup vardır ve performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="e8dc3-105">Bu sürüm ayrıca PackageReference desteği, NuGet komutlarını MSBuild hedefleri, arka plan paket geri yükler ve daha fazlasını olarak gibi çeşitli iyileştirmeler getirir.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e8dc3-106">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="e8dc3-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="e8dc3-107">Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="e8dc3-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-108">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-108">Issue</span></span>

<span data-ttu-id="e8dc3-109">Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="e8dc3-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="e8dc3-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-111">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-111">Workaround</span></span>

<span data-ttu-id="e8dc3-112">Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="e8dc3-113">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="e8dc3-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-114">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-114">Issue</span></span>

<span data-ttu-id="e8dc3-115">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="e8dc3-116">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="e8dc3-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="e8dc3-118">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-118">Workaround</span></span>

<span data-ttu-id="e8dc3-119">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="e8dc3-120">Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="e8dc3-121">.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e8dc3-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-122">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-122">Issue</span></span>

<span data-ttu-id="e8dc3-123">Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="e8dc3-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="e8dc3-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-125">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-125">Workaround</span></span>

<span data-ttu-id="e8dc3-126">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="e8dc3-127">Görüntüleme, ekleme ya da DotNetCLITools, Nuget Paket Yöneticisi'ni kullanarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e8dc3-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-128">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-128">Issue</span></span>

<span data-ttu-id="e8dc3-129">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="e8dc3-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="e8dc3-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-131">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-131">Workaround</span></span>

<span data-ttu-id="e8dc3-132">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="e8dc3-133">Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur</span><span class="sxs-lookup"><span data-stu-id="e8dc3-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-134">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-134">Issue</span></span>

<span data-ttu-id="e8dc3-135">.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="e8dc3-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="e8dc3-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-137">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-137">Workaround</span></span>

<span data-ttu-id="e8dc3-138">Geri yükleme komutunu, komut satırını kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="e8dc3-139">Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="e8dc3-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-140">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-140">Issue</span></span>

<span data-ttu-id="e8dc3-141">'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="e8dc3-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="e8dc3-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-143">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-143">Workaround</span></span>

<span data-ttu-id="e8dc3-144">'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="e8dc3-145">Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="e8dc3-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-146">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-146">Issue</span></span>

<span data-ttu-id="e8dc3-147">Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="e8dc3-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="e8dc3-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-149">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-149">Workaround</span></span>

<span data-ttu-id="e8dc3-150">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="e8dc3-151">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="e8dc3-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-152">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-152">Issue</span></span>

<span data-ttu-id="e8dc3-153">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="e8dc3-154">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="e8dc3-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="e8dc3-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-156">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-156">Workaround</span></span>

<span data-ttu-id="e8dc3-157">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="e8dc3-158">.NET461’i hedefleyen bir proje, .NETStandard’ı hedefleyen başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur</span><span class="sxs-lookup"><span data-stu-id="e8dc3-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="e8dc3-159">Sorun</span><span class="sxs-lookup"><span data-stu-id="e8dc3-159">Issue</span></span>

<span data-ttu-id="e8dc3-160">.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="e8dc3-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="e8dc3-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="e8dc3-162">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="e8dc3-162">Workaround</span></span>

<span data-ttu-id="e8dc3-163">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="e8dc3-164">NuGet 4.0 RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="e8dc3-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="e8dc3-165">[NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md) -NuGet 4.0 RC için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="e8dc3-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="e8dc3-166">Özellikler</span><span class="sxs-lookup"><span data-stu-id="e8dc3-166">Features</span></span>

- <span data-ttu-id="e8dc3-167">NuGet.Core.sln - dizeleri yerelleştirme [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="e8dc3-168">Nuget zorlar LSL modunda - web uygulama projeleri yüklemek için [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="e8dc3-169">Blok sürüme AutoReferenced PackageReference destek değişiklikleri kullanıcı Arabiriminde "yüklü SDK'sı" paketler için - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="e8dc3-170">PackageSpec.Version (PackageRef) - proje bağımlılıkları için doğru bir şekilde iletişim [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="e8dc3-171">Destek başvuruyu kaldırmak için `.csproj` commandline(s) - gelen [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="e8dc3-172">Geri yükleme PackageReference projeleri (normal ve xplat) ve basit çözüm yük - desteği [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="e8dc3-173">Destek içine başvurular eklemek için `.csproj` commandline(s) - gelen [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="e8dc3-174">Basit çözüm yük için NuGet geri yükleme desteği `packages.config` veya `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="e8dc3-175">Content dosyaları destek oluşturulan nuget hedefleri dosyasında - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="e8dc3-176">Mono CI Mac üzerinde nuget.exe doğrulama için kurmak MSBuild - kullanma [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="e8dc3-177">NuGet v2 NuGet.Core bağımlılıkları dışına - taşıma [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="e8dc3-178">Hatalar</span><span class="sxs-lookup"><span data-stu-id="e8dc3-178">Bugs</span></span>

- <span data-ttu-id="e8dc3-179">Visual Studio'da NuGet restore saygı projeleri - PackageId özelliği [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="e8dc3-180">Paket VSIX paketi - eklerken NuGet ProjectSystemCache hata [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="e8dc3-181">Paketi IncludeSource birden çok TFMs - projeyle kullanılıyorsa özel durum oluşturur [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="e8dc3-182">Çözüm genelinde Update'ten kullanma VS 2017 RC3 kilitlenme paket Yönetimi - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="e8dc3-183">Yeni yüklenen paket - kaldıramazsınız [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="e8dc3-184">İçin PackageRef geçirirken, karma çözümleri garip geri yükleme davranışını - sahip [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="e8dc3-185">En kısa sürede NuGet başlattıktan sonra oluşturma işlemi (yükleme, güncelleştirme, geri yükleme) neden olabilecek VS kilitlenmesine - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="e8dc3-186">UI askıda - NuGet.SolutionRestoreManager.RestoreManagerPackage başlatma kilitlenme [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="e8dc3-187">Paketi komutu sürüm öğesi - yerine özniteliği olarak ekleyin [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="e8dc3-188">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-188">dotnet</span></span>
  - <span data-ttu-id="e8dc3-189">dotnetcore geri yükleme foo.sln--başarısız SLN yapılandırmalarında (ancak, fark config) yinelenen projeleri geri yükleme grafiğinde - neden olduğunda [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="e8dc3-190">Yalnızca paketler - içerik [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="e8dc3-191">Varsayılan olarak paket biçimi Seçici seçeneği dışında - opt [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="e8dc3-192">Perf: CreateUAP_CSharp_VS.01.1.Create Proje 3,153.570 ms (%149.1) tarafından Duration_TotalElapsedTime gerileyen.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="e8dc3-193">Taban çizgisi 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="e8dc3-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild çözüm tarafından 1,5 sn Duration_TotalElapsedTime gerileyen.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="e8dc3-195">Taban çizgisi 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="e8dc3-196">Adaylığı başarısız çoklu TFM projelerinde - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="e8dc3-197">Perf: WebForms_DDRIT.1200.Close çözüm 3.000 sayısı (% 0,5) tarafından VM_ImagesInMemory_Total_devenv gerileyen.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="e8dc3-198">Taban çizgisi 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="e8dc3-199">vsfeedback - netcoreapp1.1 hedeflerken paketi uyarılar - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="e8dc3-200">Bir NuGet paketi için boş ASP.NET Core web uygulaması - eklenmeye çalışılırken PathTooLongException [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="e8dc3-201">Paketi çok sık sık--dotnet çalışır</span><span class="sxs-lookup"><span data-stu-id="e8dc3-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="e8dc3-202">Orada ile dotnetcore paketi başarısız olduğu hedef bağımlılık grafiği içeren hedef "Paketi" - Döngüsel bir bağımlılıkla [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="e8dc3-203">Paketi çalıştıran çok sık--oluşturmak NuGet paketi, tüm yapılandırmaları - içermez [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="e8dc3-204">NullReferenceException ekleme nuget C++ projesinde - packageref ile [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="e8dc3-205">Erişilebilirlik: Ekran okuyucusu - paketi yüklemek için projeleri seçmek için onay kutusunu ile Anlat değil [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="e8dc3-206">NuGet VS17 düzensiz aralıklarla hataya başarısız - VS hata 365798 - VSO/VSTS akışları bağlanma [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="e8dc3-207">Content dosyaları alırsanız yanlış konuma çıktı ise PackagePath "Content dosyaları" - olarak yolunu belirtir, [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="e8dc3-208">Paketi hedef ekler VersionSuffix - PackageVersion özelliğiyle [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="e8dc3-209">Paket yolu dotnet paketiyle - işe yaramazsa belirtme [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="e8dc3-210">Geri yükleme sırasında - NuGet çıkarır yinelenen içeri aktarmaları hakkında uyarılar bir grup [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="e8dc3-211">"NuGet Paket Yöneticisi Format" iletişim koyu tema altında - bozuk görünüyor seçin [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="e8dc3-212">VS kilitlenme yapı geri yükleme - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="e8dc3-213">Visual Studio kilitlenmeleri targetframeworks içinde TFM eklerseniz kaydedin, sonra oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="e8dc3-214">Süre - % 10 [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="e8dc3-215">nuget paketi, Proje başarıyla - paket üzerinde başarı iletisi çıktı değil [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="e8dc3-216">PackTask System.IO.Compression 4.1 değil olması nedeniyle başarısız bulunamadı - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="e8dc3-217">Paketi çalıştıran çok sık--PackTask sık sık başarısız dosya erişim çakışma - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="e8dc3-218">NuGet arka plan geri yükleme sırasında - çıktı penceresi açar [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="e8dc3-219">(Hangi kilitlenmesine neden) tehlikeli kodlama düzeni - ServiceProvider ortadan [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="e8dc3-220">Perf/UIHang - DownloadTimeoutStream okuma - artırmak [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="e8dc3-221">Visual Studio kilitlenmeleri NuGet geri yüklemesi bitmeden önce - bir projeyi kapatın çalışırsanız [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="e8dc3-222">PackTask ve paketleme ile ilgili sorunları `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="e8dc3-223">[vsfeedback] Yeni Proje (visual studio yeniden başlatma gerekir) - nuget paketlerini çözümlenemiyor [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="e8dc3-224">[vsfeedback] "Sürüm" açılan listesi kullanılabilir paket sürümlerinin kalmak için struggles içinde eşitleme seçili nuGet paketi ile birlikte... - gösteren [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="e8dc3-225">Nuget.Client kullanması gereken CPS JoinableTaskFactory ile CPS kullanılırken kilitlenmeleri - önlemek için [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="e8dc3-226">NuGet 3.5.0 değil paketi açılırken `.targets` - paketten [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="e8dc3-227">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-227">dotnet</span></span>
  - <span data-ttu-id="e8dc3-228">dotnetcore paketi başlığında desteklemediği `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="e8dc3-229">Hata iletişim kutusunda VS2017 RC - Install-Package sonuçlanıyor [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="e8dc3-230">Kullanıcı arabirimini CPS güncelleştirme nominate açılmıyor gibi .net core proje için bir paket güncelleştirme çalışmıyor için görünür.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="e8dc3-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="e8dc3-232">Çözümlenmemiş başvuru uyarısı - artırmak [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="e8dc3-233">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-233">dotnet</span></span>
  - <span data-ttu-id="e8dc3-234">dotnetcore paketi - ProjectReference kaybeder sürüm bilgilerini - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="e8dc3-235">UWP uygulaması oluşturma projesi oluşturun ve geçen toplam süre gerileme - yeniden [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="e8dc3-236">Başarıyla geri ileti geri yükleme sırasında bile hatasından sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="e8dc3-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="e8dc3-238">Nuget.CommandLine 3.4.4 Nuget.org için-yeniden yayımlayın [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="e8dc3-239">Projeleri geçirme üzerinde çıkarılıp `project.json` için `.csproj` ---geri yükleme başarısız - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="e8dc3-240">Yeni oluşturulan xunit Test projede - geri yükleme başarısız [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="e8dc3-241">Çekirdek projeleri askıda, UI - açık kilitlemek [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="e8dc3-242">derleme görevleri - hedefleri dosyasını düzeltmek [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="e8dc3-243">Hata listesi başvurulan proje - unload yapı çözümü sonra hata sahip [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="e8dc3-244">MSB4057: "_GenerateRestoreGraphProjectEntry" hedef projede mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="e8dc3-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="e8dc3-246">vsfeedback: çözüm için nuget Yöneticisi kullanıcı arabirimi çöküyor tüm projeleri - seçtiğinizde [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="e8dc3-247">nuget.exe msbuildpath başarısız eğik - olduğunda [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="e8dc3-248">vsfeedback: NuGet restore vermek LinqToTwitter proje için-birkaç proje başvurusu uyarıları [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="e8dc3-249">Gelen paket `.csproj` minClientVersion özniteliği - içermez [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="e8dc3-250">NuGet.Build.Tasks.Pack.dll sevk VS2017 içinde imzalı gecikme (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="e8dc3-251">VSFeedback: 3.7.1 - CMake ile oluşturulan bir VS 2015 projesi için geri yükleme başarısız [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="e8dc3-252">VSFeedback: Derleme sunabilir - daha ayrıntılı hata iletilerini geri yükleme hatalarını soyutlamaması [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="e8dc3-253">[VSFeedback] Web projesi için NuGet paketleri geri yüklenirken hata oluştu: değer null olamaz.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="e8dc3-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="e8dc3-255">Geçiş oluşturur "nesne başvurusu özel durumu NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker içinde - nesnenin" [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="e8dc3-256">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-256">dotnet</span></span>
  - <span data-ttu-id="e8dc3-257">dotnetcore pack Araçları Paketi karşı - oluşturulan sürümlerle [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="e8dc3-258">Yeni arka plan geri yükleme durum çubuğunda zaman geri yüklemek için - saniye sürer milisaniye Yazar [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="e8dc3-259">Üzerinde yazım hatası başarısız tüm proje başvuruları - çözümlemek [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="e8dc3-260">Paket başvuru senaryolarda - PCM iş akışlarını etkinleştirin [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="e8dc3-261">Yüklü paketler Yöneticisi kullanıcı Arabirimi - paketinde bulunamıyor [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="e8dc3-262">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-262">dotnet</span></span>
  - <span data-ttu-id="e8dc3-263">dotnetcore paketi başarısız ise PackagePath boş - olduğunda [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="e8dc3-264">Bir Çoklu kullanıcı senaryosunda - görev başarısız geri [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="e8dc3-265">NuGet paketi görevini kullanarak paket içerik türü değiştirilemiyor- [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="e8dc3-266">Content varsayılan Kopyala'dosyaları için MsBuild /t:pack - yanlış [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="e8dc3-267">Yükleme paketi geri yüklemesi çift günlüklerini geri yükleme paketleri iletisi - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="e8dc3-268">Guardrails - kaldırma geri yükleme "çalışma zamanları" bölümünün yalnızca geçerli projeye - uygulanması [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="e8dc3-269">Paketi görevi koyar içerik dosyalarının ikisi de ' içeriği /' ve ' Content dosyaları /'- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="e8dc3-270">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-270">dotnet</span></span>
  - <span data-ttu-id="e8dc3-271">dotnetcore pack3 çok etiket bölme - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="e8dc3-272">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-272">dotnet</span></span>
  - <span data-ttu-id="e8dc3-273">dotnetcore paketi: Paket projelerle sevk başvuran yinelenen alma uyarı - sonuçlarında [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="e8dc3-274">Geri yükleme VS günlüğü değil her zaman göster - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="e8dc3-275">nuget Yereller Yardım metni hala paketleri önbellek - belirtilen [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="e8dc3-276">Restore3 PackageReferences TargetFrameworks ile tüm çiftler.</span><span class="sxs-lookup"><span data-stu-id="e8dc3-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="e8dc3-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="e8dc3-278">Nuget Çekmeleri MSBuild beklenmeyen sürümü VS "15" Preview 4 istisnası</span><span class="sxs-lookup"><span data-stu-id="e8dc3-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="e8dc3-279">Komut İstemi - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="e8dc3-280">Hedefleri/özellik dosyaları geri yükleme başarısız - out yazma [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="e8dc3-281">VS 15 Komut İstemi'nde - çalıştırırken, geri yükleme sırasında NuGet MSBuild olarak aynı compat dolgular saygı değil [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="e8dc3-282">PackFromProjectWithDevelopmentDependencySet VS15 için - yeniden etkinleştirmek [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="e8dc3-283">Harmanlama NuGet - sorun [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="e8dc3-284">4.0.0.2067 RC2 ile - dağıtmayı CLI ve SDK depoları şekilde entegre [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="e8dc3-285">Yeni çekirdek konsol uygulaması, Kapat çözümü, çözüm açmak ve Kapat çözüm - oluşturduğunuzda, VS askıda [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="e8dc3-286">D15prerel.25916.01 karşı-kilitlenebilir açılış proje basarsa [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="e8dc3-287">Belge/Yardım iletisi - dotnet/nuget.exe Yereller düzeltme [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="e8dc3-288">Başında veya sonunda boşluk - sorunlarını PackTask incelemek [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="e8dc3-289">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-289">dotnet</span></span>
  - <span data-ttu-id="e8dc3-290">dotnetcore paketi obj değil depo - paket [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="e8dc3-291">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-291">dotnet</span></span>
  - <span data-ttu-id="e8dc3-292">dotnetcore paketi her zaman görünüyor ProjectReference sürümü 1.0.0 için - Ayarla [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="e8dc3-293">DotNet</span><span class="sxs-lookup"><span data-stu-id="e8dc3-293">dotnet</span></span>
  - <span data-ttu-id="e8dc3-294">dotnetcore paketi proje başvuruları ile başarısız olur ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="e8dc3-295">ProjectSystemCache.TryGetProjectNameByShortName - LockRecursionException [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="e8dc3-296">MSBuild özellikleri - boşlukları kırpma [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="e8dc3-297">Proje yükünü - oluşturulan iki proje olaylara birleştirmek [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="e8dc3-298">P2p kitaplıklarında `project.assets.json` dosyanız yanlış sürümü - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="e8dc3-299">Yanıt akışı ve kullanılabilir paket - nedeniyle kilitlenme geri [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="e8dc3-300">nuget.exe MSBuild hata çıktısı - büyük miktarda üzerinde telefonu kapatın [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="e8dc3-301">Derleme üzerinde geri yükleme karışım ilk kez başarısız için ikinci kez (VS senaryo sabit) - başarılı [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="e8dc3-302">Dcr</span><span class="sxs-lookup"><span data-stu-id="e8dc3-302">DCRs</span></span>

- <span data-ttu-id="e8dc3-303">VSIX v3 VSIX için - v2 VSIX geçirmek [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="e8dc3-304">NuGet yolu almak için bir mekanizma olmalıdır MSBuild - lock dosyasında [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="e8dc3-305">Yapı varlıklar TFM uyumluluk denetimi ve varlıklar - eklemek [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="e8dc3-306">Yeni ProjectCapability "Paketi" paketinde tanımlamak paketi etkinleştirme hedefleri ilgili özellikleri - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="e8dc3-307">Bir post yapı olarak "GeneratePackageOnBuild" MSBuild özellikte - söylediğinizde hedef paketi çalıştırmak [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="e8dc3-308">NuGet özelliği RestoreProjectStyle belirli NuGet proje - oluşturulacağı [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="e8dc3-309">Geçişli proje başvuruları değiştirmek için - geri yükleme uyum [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="e8dc3-310">Hedef dosyada olmayan UWP projeleri - NuGet özellikleri ekleme [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="e8dc3-311">UWP TargetPlatformVersion desteği - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="e8dc3-312">NuGet proje sistemine - proje başvuru meta verisi iletişim [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="e8dc3-313">İçin paketleme modu - kullanıcı Arabirimi eklemek [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="e8dc3-314">Eski `.csproj` NugetTargetMoniker ve proj/hedefleri - ayarlamak RuntimeIdentifiers gereken [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="e8dc3-315">Yükleme paketi-restore - otomatik çakışıyor [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="e8dc3-316">Bağlam menüsü QueryStatus değil durum VSPackage değil yüklendiğinde - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="e8dc3-317">Çözüm geri yükleme ve yapı geri hala iletişim kutuları - Göster [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="e8dc3-318">NuGet.Clients çözümü derleme - yalıtmak VSSDK sürümünde [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="e8dc3-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="e8dc3-319">GitHub sorunları RTM'de sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="e8dc3-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="e8dc3-320">Konu listesi 1</span><span class="sxs-lookup"><span data-stu-id="e8dc3-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="e8dc3-321">Konu listesi 2</span><span class="sxs-lookup"><span data-stu-id="e8dc3-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="e8dc3-322">Konu listesi 3</span><span class="sxs-lookup"><span data-stu-id="e8dc3-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="e8dc3-323">Konu listesi 4</span><span class="sxs-lookup"><span data-stu-id="e8dc3-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="e8dc3-324">Konu listesi 5</span><span class="sxs-lookup"><span data-stu-id="e8dc3-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
