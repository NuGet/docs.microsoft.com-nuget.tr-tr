---
title: NuGet 4.0 RC Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.0 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496599"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="196ff-103">NuGet 4.0 RTM Yayın Notları</span><span class="sxs-lookup"><span data-stu-id="196ff-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="196ff-104">[Visual Studio 2017,](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) .NET Core'a destek sağlayan, bir sürü kalite düzeltmesi olan ve performansı artıran NuGet 4.0 ile birlikte geliyor.</span><span class="sxs-lookup"><span data-stu-id="196ff-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="196ff-105">Bu sürüm aynı zamanda PackageReference desteği, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yüklemesi ve daha fazlası gibi çeşitli iyileştirmeler de getirir.</span><span class="sxs-lookup"><span data-stu-id="196ff-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="196ff-106">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="196ff-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="196ff-107">Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="196ff-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-108">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-108">Issue</span></span>

<span data-ttu-id="196ff-109">Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="196ff-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="196ff-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="196ff-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="196ff-111">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-111">Workaround</span></span>

<span data-ttu-id="196ff-112">Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="196ff-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="196ff-113">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="196ff-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-114">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-114">Issue</span></span>

<span data-ttu-id="196ff-115">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="196ff-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="196ff-116">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="196ff-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="196ff-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="196ff-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="196ff-118">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-118">Workaround</span></span>

<span data-ttu-id="196ff-119">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="196ff-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="196ff-120">Alternatif olarak, silme `project.lock.json` ve yeniden geri deneyin.</span><span class="sxs-lookup"><span data-stu-id="196ff-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="196ff-121">.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="196ff-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-122">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-122">Issue</span></span>

<span data-ttu-id="196ff-123">Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="196ff-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="196ff-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="196ff-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="196ff-125">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-125">Workaround</span></span>

<span data-ttu-id="196ff-126">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="196ff-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="196ff-127">Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz</span><span class="sxs-lookup"><span data-stu-id="196ff-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-128">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-128">Issue</span></span>

<span data-ttu-id="196ff-129">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="196ff-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="196ff-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="196ff-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="196ff-131">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-131">Workaround</span></span>

<span data-ttu-id="196ff-132">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="196ff-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="196ff-133">Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur</span><span class="sxs-lookup"><span data-stu-id="196ff-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-134">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-134">Issue</span></span>

<span data-ttu-id="196ff-135">.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="196ff-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="196ff-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="196ff-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="196ff-137">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-137">Workaround</span></span>

<span data-ttu-id="196ff-138">Geri yükleme komutunu, komut satırını kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="196ff-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="196ff-139">Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="196ff-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-140">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-140">Issue</span></span>

<span data-ttu-id="196ff-141">'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez.</span><span class="sxs-lookup"><span data-stu-id="196ff-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="196ff-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="196ff-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="196ff-143">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-143">Workaround</span></span>

<span data-ttu-id="196ff-144">'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="196ff-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="196ff-145">Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="196ff-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-146">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-146">Issue</span></span>

<span data-ttu-id="196ff-147">Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="196ff-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="196ff-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="196ff-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="196ff-149">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-149">Workaround</span></span>

<span data-ttu-id="196ff-150">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="196ff-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="196ff-151">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="196ff-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-152">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-152">Issue</span></span>

<span data-ttu-id="196ff-153">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="196ff-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="196ff-154">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="196ff-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="196ff-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="196ff-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="196ff-156">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-156">Workaround</span></span>

<span data-ttu-id="196ff-157">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="196ff-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="196ff-158">.NET461’i hedefleyen bir proje, .NETStandard’ı hedefleyen başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur</span><span class="sxs-lookup"><span data-stu-id="196ff-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="196ff-159">Sorun</span><span class="sxs-lookup"><span data-stu-id="196ff-159">Issue</span></span>

<span data-ttu-id="196ff-160">.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="196ff-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="196ff-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="196ff-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="196ff-162">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="196ff-162">Workaround</span></span>

<span data-ttu-id="196ff-163">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="196ff-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="196ff-164">NuGet 4.0 RTM zaman diliminde düzeltilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="196ff-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="196ff-165">[NuGet 4.0 RC Yayın Notları](../release-notes/nuget-4.0-RC.md) - NuGet 4.0 RC için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="196ff-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="196ff-166">Özellikler</span><span class="sxs-lookup"><span data-stu-id="196ff-166">Features</span></span>

- <span data-ttu-id="196ff-167">NuGet.Core.sln'de dizeleri [yerelleştirin](https://github.com/NuGet/Home/issues/2041) - #2041</span><span class="sxs-lookup"><span data-stu-id="196ff-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="196ff-168">Nuget kuvvetleri LSL modunda web uygulama projeleri yüklemek için - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="196ff-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="196ff-169">"sdk yüklü" paketler için UI sürüm değişikliklerini engellemek için AutoReferenced PackageReference desteği - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="196ff-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="196ff-170">Doğru herhangi bir proje bağımlılıkları (PackageRef) için PackageSpec.Version iletişim - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="196ff-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="196ff-171">komut satırından(lar)a `.csproj` başvuruları kaldırmak için destek - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="196ff-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="196ff-172">PackageReference projeleri (normal ve xplat) ve Hafif Çözüm Yükü için destek geri [yüklemesi](https://github.com/NuGet/Home/issues/4003) - #4003</span><span class="sxs-lookup"><span data-stu-id="196ff-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="196ff-173">commandline(lar) `.csproj` içine referanseklemek için destek - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="196ff-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="196ff-174">Destek NuGet geri yükleme `packages.config` için `project.json`  - hafif çözüm yükü için veya [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="196ff-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="196ff-175">contentFiles nuget oluşturulan hedefler dosyasında destek - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="196ff-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="196ff-176">MSBuild kullanarak Mac'te nuget.exe doğrulaması için mono ci [-#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="196ff-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="196ff-177">Move NuGet off v2 NuGet.Core bağımlılıkları - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="196ff-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="196ff-178">Hatalar</span><span class="sxs-lookup"><span data-stu-id="196ff-178">Bugs</span></span>

- <span data-ttu-id="196ff-179">NuGet geri Visual Studio projelerin PackageId özelliğine saygı duymaz - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="196ff-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="196ff-180">VSIX paketine paket eklerken NuGet ProjectSystemCache hatası - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="196ff-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="196ff-181">IncludeSource birden fazla TFM'si olan bir projede kullanılıyorsa paket özel durum atar - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="196ff-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="196ff-182">VS 2017 RC3, Solution genelindeki paket yönetiminden gelen güncellemeyi kullanarak çöküyor - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="196ff-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="196ff-183">Yeni yüklenen paketi kaldıramıyorum - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="196ff-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="196ff-184">PackageRef'e geçiş yaparken, karma çözümler garip geri yükleme davranışına sahiptir - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="196ff-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="196ff-185">NuGet işlemine başladıktan kısa bir süre sonra bina (yükleme, güncelleme, geri yükleme), VS'nin Hang'a neden olabilir - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="196ff-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="196ff-186">UI Hang - NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371) başlatma Deadlock</span><span class="sxs-lookup"><span data-stu-id="196ff-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="196ff-187">paket komutu ekle öğe yerine öznitelik olarak sürüm eklemelidir - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="196ff-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="196ff-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-188">dotnet</span></span>
  - <span data-ttu-id="196ff-189">dotnetcore Geri Yükleme foo.sln - SLN yapılandırmaları geri yükleme grafiğiyineleme (ama diff config) projelere neden olduğunda başarısız olur - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="196ff-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="196ff-190">İçerik sadece paketler - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="196ff-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="196ff-191">Varsayılan olarak paket biçimi seçici seçeneğini devre dışı bırakma - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="196ff-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="196ff-192">Perf: CreateUAP_CSharp_VS.01.1.Create projesi Duration_TotalElapsedTime 3.153.570 ms (%149.1) geriledi.</span><span class="sxs-lookup"><span data-stu-id="196ff-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="196ff-193">Taban Çizgisi 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="196ff-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="196ff-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Çözüm 1.5sec tarafından Duration_TotalElapsedTime geriledi.</span><span class="sxs-lookup"><span data-stu-id="196ff-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="196ff-195">Temel 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="196ff-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="196ff-196">Çoklu TFM projelerinde adaylık başarısız oldu - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="196ff-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="196ff-197">Perf: WebForms_DDRIT.1200.Close Solution VM_ImagesInMemory_Total_devenv 3.000 Sayı (%0.5) geriledi.</span><span class="sxs-lookup"><span data-stu-id="196ff-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="196ff-198">Taban çizgisi 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="196ff-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="196ff-199">vsfeedback - netcoreapp1.1 hedeflenirken paketleri uyarılar - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="196ff-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="196ff-200">PathTooLongException boş ASP.NET Core web uygulamasına bir NuGet paketi eklemeye çalışırken - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="196ff-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="196ff-201">Sürü çok sık çalışır -- dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="196ff-202">dotnetcore paketi ile başarısız hedef "Paketi" içeren hedef bağımlılık grafiğinde dairesel bir bağımlılık var - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="196ff-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="196ff-203">Paket çok sık çalışır -- Generate NuGet paketi tüm yapılandırmaları içermez - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="196ff-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="196ff-204">NullReferenceExceptionC++ projesinde packageref ile nuget ekleme - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="196ff-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="196ff-205">Erişilebilirlik : Ekran okuyucupaketi yüklemek için projeleri seçmek için onay kutusunu anlatmaz - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="196ff-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="196ff-206">NuGet VS17, VSO/VSTS beslemelerine ( VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="196ff-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="196ff-207">contentFiles, PackagePath yolu "contentFiles" olarak belirtirse çıktıyı yanlış konuma getirin - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="196ff-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="196ff-208">Pack hedef SürümSuffix ile PackageVersion özelliği ekler - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="196ff-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="196ff-209">Paket yolunu belirtme dotnet paketiile çalışmaz - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="196ff-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="196ff-210">NuGet geri yükleme sırasında yinelenen içeri almalar hakkında bir sürü uyarı çıktısı #4304 [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="196ff-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="196ff-211">"NuGet Package Manager Format" iletişim kutusunu seçin karanlık tema altında kötü görünüyor - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="196ff-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="196ff-212">VS çarpışma inşa geri yükleme - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="196ff-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="196ff-213">Hedef çerçevelere TFM eklerseniz Visual Studio kilitlenir, kaydedin, sonra oluşturun.</span><span class="sxs-lookup"><span data-stu-id="196ff-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="196ff-214">Zaman% 10 - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="196ff-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="196ff-215">nuget paketi başarıyla bir proje ambalaj başarı mesajı çıktı değil - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="196ff-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="196ff-216">PackTask System.IO.Compression 4.1 bulunamadı nedeniyle başarısız olur - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="196ff-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="196ff-217">Paket çok sık çalışır - PackTask sık sık dosya erişim çakışması ile başarısız olur - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="196ff-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="196ff-218">NuGet arka plan geri yükleme sırasında çıkış penceresini açar - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="196ff-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="196ff-219">ServiceProvider'ı tehlikeli kodlama deseni olarak ortadan kaldırın (askıda kalmasına neden olabilir) - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="196ff-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="196ff-220">Perf /UIHang - DownloadTimeoutStream geliştirin okur - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="196ff-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="196ff-221">NuGet geri yüklemesi tamamlanmadan önce bir projeyi kapatmaya çalışırsanız Visual Studio kilitlenir - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="196ff-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="196ff-222">PackTask ve ambalaj `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250) ile ilgili sorunlar</span><span class="sxs-lookup"><span data-stu-id="196ff-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="196ff-223">[vsfeedback] Yeni projede nuget paketleri çözemez (visual studio yeniden başlatmaihtiyacı) - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="196ff-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="196ff-224">[vsfeedback] Kullanılabilir paket sürümlerini gösteren "Sürüm" açılır, seçilen nuGet paketi ile senkronize kalmak için mücadele eder... - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="196ff-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="196ff-225">Nuget.Client kilitlenmeleri önlemek için CPS ile etkileşimde cps JoinableTaskFactory kullanmalıdır - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="196ff-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="196ff-226">NuGet 3.5.0 `.targets` paketten ambalajı açılmaz - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="196ff-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="196ff-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-227">dotnet</span></span>
  - <span data-ttu-id="196ff-228">dotnetcore paketi `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150) başlık desteklemiyor</span><span class="sxs-lookup"><span data-stu-id="196ff-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="196ff-229">VS2017 RC'de hata iletişim kutusunda yükleme-Paket sonuçları - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="196ff-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="196ff-230">.net çekirdek projesi için bir paketi güncelleştirme, kullanıcı arabirimi tarafından CPS güncelleştirmesini alamadığı için işe yaramıyor gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="196ff-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="196ff-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="196ff-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="196ff-232">Çözülmemiş başvuru uyarısını geliştirin - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="196ff-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="196ff-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-233">dotnet</span></span>
  - <span data-ttu-id="196ff-234">dotnetcore paketi - ProjectReference sürüm bilgilerini kaybeder - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="196ff-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="196ff-235">UWP uygulaması oluşturma & toplam geçen süre gerilemelerini yeniden oluşturma - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="196ff-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="196ff-236">Başarılı geri yükleme iletisi geri yükleme sırasında hata sonra bile görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="196ff-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="196ff-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="196ff-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="196ff-238">yeniden Yayımla Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="196ff-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="196ff-239">Geçir'de, projeler `project.json` `.csproj` --- geri yükleme başarısız olur - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="196ff-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="196ff-240">Yeni oluşturulan xunit Test projesinde başarısız olan geri yükleme - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="196ff-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="196ff-241">Çekirdek projeler asabilir, açık ui kilitlemek - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="196ff-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="196ff-242">yapı görevleri için hedefler dosyayı düzeltme - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="196ff-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="196ff-243">Hata listesinde başvurulan projeyi boşaltan yapı çözümünden sonra hata var - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="196ff-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="196ff-244">MSB4057: Projede "_GenerateRestoreGraphProjectEntry" hedefi yok.</span><span class="sxs-lookup"><span data-stu-id="196ff-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="196ff-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="196ff-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="196ff-246">vsfeedback: tüm projeleri seçtiğinizde çözüm çöküyor için nuget manager ui - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="196ff-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="196ff-247">nuget.exe msbuildpath bir iz çizgi olduğunda başarısız olur - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="196ff-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="196ff-248">vsfeedback: NuGet geri LinqToTwitter projesi için çeşitli proje referans uyarıları vermek geri - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="196ff-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="196ff-249">Paket `.csproj` minClientVersion özniteliği içermez - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="196ff-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="196ff-250">NuGet.Build.Tasks.Pack.dll sevk gecikmesi VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="196ff-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="196ff-251">VSFeedback: CMake 3.7.1 ile oluşturulan VS 2015 projesi için geri yükleme başarısız oldu - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="196ff-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="196ff-252">VSFeedback: Geri yükleme hataları oluşturmak verebilir daha tam hata iletileri gizleyebilirsiniz - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="196ff-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="196ff-253">[VSFeedback] Web sitesi projesi için NuGet paketlerini geri alırken hata oluştu: Değer null olamaz.</span><span class="sxs-lookup"><span data-stu-id="196ff-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="196ff-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="196ff-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="196ff-255">Geçiş NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker "Nesne başvuru Özel Durum" atar - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="196ff-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="196ff-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-256">dotnet</span></span>
  - <span data-ttu-id="196ff-257">dotnetcore paketi paketi karşı inşa edilmiş sürümleri ile araçları paketi gerekir - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="196ff-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="196ff-258">Yeni arka plan geri yüklemesi, saniyeler zaman zaman durum çubuğuna milisaniye yazar - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="196ff-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="196ff-259">Yazım hatası tüm proje referansları çözmek için başarısız oldu - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="196ff-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="196ff-260">Paket başvuru senaryolarında PCM iş akışlarını etkinleştirin - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="196ff-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="196ff-261">Paket yöneticisi UI yüklü paketleri bulamıyorum - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="196ff-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="196ff-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-262">dotnet</span></span>
  - <span data-ttu-id="196ff-263">PackagePath boş olduğunda dotnetcore paketi başarısız olur - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="196ff-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="196ff-264">Geri yükleme görevi çok kullanıcılı bir senaryoda başarısız olur - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="196ff-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="196ff-265">NuGet Pack Task kullanarak ambalajlarken İçerik türünü değiştiremezsiniz - [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="196ff-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="196ff-266">İçerik Dosyalarının Varsayılan Kopyası MsBuild /t:pack için yanlış - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="196ff-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="196ff-267">Paketi geri yükleyin çift günlükleri geri paketleri mesajı - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="196ff-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="196ff-268">Guardrails kaldırın - "runtimes" bölümünün geri yükleme sadece geçerli proje için geçerli olmalıdır - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="196ff-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="196ff-269">Paket görevi içerik dosyalarını hem 'içerik/' hem de 'contentFiles/' olarak koyar - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="196ff-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="196ff-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-270">dotnet</span></span>
  - <span data-ttu-id="196ff-271">dotnetcore pack3 ekstra etiket bölme yok - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="196ff-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="196ff-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-272">dotnet</span></span>
  - <span data-ttu-id="196ff-273">dotnetcore paketi: paket referansları ile ambalaj projeleri yinelenen ithalat uyarısı sonuçları - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="196ff-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="196ff-274">VS'de günlük geri yükleme her zaman görünmüyor - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="196ff-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="196ff-275">nuget yerliler metin hala belirtilen paketleri önbellek yardım - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="196ff-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="196ff-276">TargetFrameworks ile Restore3 çiftler PackageReferences.</span><span class="sxs-lookup"><span data-stu-id="196ff-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="196ff-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="196ff-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="196ff-278">Nuget VS MSBuild beklenmedik sürümünü seçer "15" Önizleme 4 dev.</span><span class="sxs-lookup"><span data-stu-id="196ff-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="196ff-279">komut istemi - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="196ff-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="196ff-280">Başarısız geri yüklemede hedef/sahne dosyalarını yazma - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="196ff-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="196ff-281">Geri yükleme sırasında NuGet VS 15 komut istemi çalışırken MSBuild ile aynı compat shims saygı yok - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="196ff-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="196ff-282">VS15 için PackFromProjectWithDevelopmentDependencySet'i yeniden etkinleştirin - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="196ff-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="196ff-283">NuGet ile sorunları karıştırın - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="196ff-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="196ff-284">4.0.0.2067'yi CLI ve SDK depolarına entegre edin - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="196ff-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="196ff-285">Yeni Core Console App, Close Solution, Open Solution ve Close Solution Oluştururken VS Askıda Kalır - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="196ff-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="196ff-286">D15prerel.25916.01 karşı asmak açılış projesi isabet - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="196ff-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="196ff-287">dotnet/nuget.exe locals doc/help message 'ı düzelt [- #3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="196ff-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="196ff-288">PackTask'ı izleme veya önde gelen beyaz alanla ilgili sorunlar için denetleyin - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="196ff-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="196ff-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-289">dotnet</span></span>
  - <span data-ttu-id="196ff-290">dotnetcore paketi obj değil bin ambalaj - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="196ff-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="196ff-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-291">dotnet</span></span>
  - <span data-ttu-id="196ff-292">dotnetcore paketi her zaman 1.0.0 ProjectReference sürümünü ayarlamak gibi görünüyor - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="196ff-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="196ff-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="196ff-293">dotnet</span></span>
  - <span data-ttu-id="196ff-294">dotnetcore paketi proje referansları ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865) ile başarısız</span><span class="sxs-lookup"><span data-stu-id="196ff-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="196ff-295">ProjectSystemCache.TryGetProjectNameByShortName içinde LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="196ff-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="196ff-296">MSBuild özelliklerinden beyaz boşluğu kırpın - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="196ff-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="196ff-297">Proje yükü yle toplanan iki proje olayını birleştirin - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="196ff-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="196ff-298">Dosyadaki P2P kitaplıklarında `project.assets.json` yanlış Sürüm var - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="196ff-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="196ff-299">Yanıt vermeyen besleme ve kullanılamayan paket nedeniyle kilitlenmeyi geri yükleme - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="196ff-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="196ff-300">nuget.exe MSBuild hata çıkışı büyük miktarda asmak olabilir - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="196ff-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="196ff-301">Blend için geri yükleme-on-build ilk kez başarısız olur, ikinci kez başarılı (VS senaryo sabit) - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="196ff-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="196ff-302">DCRs</span><span class="sxs-lookup"><span data-stu-id="196ff-302">DCRs</span></span>

- <span data-ttu-id="196ff-303">v2 vsix v3 vsix için vsix göç - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="196ff-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="196ff-304">NuGet MSBuild kilit dosyasına yol almak için bir mekanizma olmalıdır - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="196ff-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="196ff-305">TFM uyumluluk denetimine ve varlıklar dosyasına yapı varlıkları ekleme - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="196ff-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="196ff-306">Paketle ilgili yetenekleri etkinleştirmek için Paket hedeflerinde yeni bir ProjectCapability "Pack" tanımlayın - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="196ff-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="196ff-307">"GeneratePackageOnBuild" MSBuild özelliği koşullu bir sonrası inşa hedef olarak Çalıştır ın - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="196ff-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="196ff-308">Belirli NuGet projesi oluşturmak için NuGet özelliği RestoreProjectStyle'ı kullanın - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="196ff-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="196ff-309">Geçişli Proje Başvuruları değişikliği için Geri Yükleme'yi [uyarla](https://github.com/NuGet/Home/issues/4076) - #4076</span><span class="sxs-lookup"><span data-stu-id="196ff-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="196ff-310">UWP olmayan projeler için hedef dosyaya NuGet özellikleri ekleme - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="196ff-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="196ff-311">UWP TargetPlatformVersion desteği - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="196ff-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="196ff-312">Proje referans meta verilerini NuGet proje sistemine [iletin](https://github.com/NuGet/Home/issues/3922) - #3922</span><span class="sxs-lookup"><span data-stu-id="196ff-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="196ff-313">Paketleme modu için UI ekle - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="196ff-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="196ff-314">Eski `.csproj` proj / hedefler ayarlanmış NugetTargetMoniker ve RuntimeIdentifiers ihtiyacı - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="196ff-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="196ff-315">Yükleme paketi otomatik geri yükleme ile çakışabilir - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="196ff-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="196ff-316">Bağlam menüsü QueryStatus VSPackage yüklenmediği zaman gerçekleşmez - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="196ff-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="196ff-317">Çözüm Geri Yükle ve Oluştur Geri Yükleme hala iletişim lerini gösterir - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="196ff-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="196ff-318">NuGet.Clients çözüm yapısında VSSDK sürümünü yalıt - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="196ff-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="196ff-319">RTM'de düzeltilen GitHub sorunlarına bağlantılar</span><span class="sxs-lookup"><span data-stu-id="196ff-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="196ff-320">Sorunlar listesi 1</span><span class="sxs-lookup"><span data-stu-id="196ff-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="196ff-321">Sorunlar listesi 2</span><span class="sxs-lookup"><span data-stu-id="196ff-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="196ff-322">Sorunlar listesi 3</span><span class="sxs-lookup"><span data-stu-id="196ff-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="196ff-323">Sorunlar listesi 4</span><span class="sxs-lookup"><span data-stu-id="196ff-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="196ff-324">Sorunlar listesi 5</span><span class="sxs-lookup"><span data-stu-id="196ff-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
