---
title: "NuGet 4.0 RC sürüm notları | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.0 RTM için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 4.0 RTM sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2cdee8b736fa2c651da803be9a10a6114936134a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="40-rtm-release-notes"></a><span data-ttu-id="3e2cc-104">4.0 sürüm notları RTM</span><span class="sxs-lookup"><span data-stu-id="3e2cc-104">4.0 RTM Release Notes</span></span>

<span data-ttu-id="3e2cc-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.0 ile .NET Core için destek ekler, kalite düzeltmeler bir grup vardır ve performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-105">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="3e2cc-106">Bu sürüm ayrıca PackageReference desteği, NuGet komutlarını MSBuild hedefleri, arka plan paket geri yükler ve daha fazlasını olarak gibi çeşitli iyileştirmeler getirir.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-106">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3e2cc-107">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3e2cc-107">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="3e2cc-108">Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="3e2cc-108">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="3e2cc-109">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-109">Issue:</span></span>
<span data-ttu-id="3e2cc-110">Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-110">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="3e2cc-111">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="3e2cc-111">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-112">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-112">Workaround:</span></span>
<span data-ttu-id="3e2cc-113">Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-113">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="3e2cc-114">Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="3e2cc-114">While using Package Manager Console, 'Enter' key may not work</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-115">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-115">Issue:</span></span>
<span data-ttu-id="3e2cc-116">Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="3e2cc-117">Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="3e2cc-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="3e2cc-119">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-119">Workaround:</span></span>
<span data-ttu-id="3e2cc-120">Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="3e2cc-121">Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="3e2cc-122">.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3e2cc-122">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-123">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-123">Issue:</span></span>
<span data-ttu-id="3e2cc-124">Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-124">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="3e2cc-125">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="3e2cc-125">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-126">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-126">Workaround:</span></span>
<span data-ttu-id="3e2cc-127">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-127">There is no workaround at this time.</span></span>

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="3e2cc-128">Nuget Paket Yöneticisi’ni kullanarak DotNetCLITools’u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz</span><span class="sxs-lookup"><span data-stu-id="3e2cc-128">You will be unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-129">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-129">Issue:</span></span>
<span data-ttu-id="3e2cc-130">NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="3e2cc-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="3e2cc-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

* #### <a name="workaround"></a><span data-ttu-id="3e2cc-132">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-132">Workaround:</span></span>
<span data-ttu-id="3e2cc-133">Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="3e2cc-134">Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur</span><span class="sxs-lookup"><span data-stu-id="3e2cc-134">NuGet restore will fail when you set PackageId property for projects</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-135">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-135">Issue:</span></span>
<span data-ttu-id="3e2cc-136">.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-136">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="3e2cc-137">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="3e2cc-137">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-138">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-138">Workaround:</span></span>
<span data-ttu-id="3e2cc-139">Geri yükleme komutunu, komut satırını kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-139">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="3e2cc-140">Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="3e2cc-140">When your project does not have 'obj' folder, package restore may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-141">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-141">Issue:</span></span>
<span data-ttu-id="3e2cc-142">'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-142">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="3e2cc-143">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="3e2cc-143">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-144">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-144">Workaround:</span></span>
<span data-ttu-id="3e2cc-145">'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-145">Create 'obj' folder manually and the restore should work.</span></span> 

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="3e2cc-146">Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir</span><span class="sxs-lookup"><span data-stu-id="3e2cc-146">Manually updating packages using Update-Package in console may fail</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-147">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-147">Issue:</span></span>
<span data-ttu-id="3e2cc-148">Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-148">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="3e2cc-149">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="3e2cc-149">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-150">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-150">Workaround:</span></span>
<span data-ttu-id="3e2cc-151">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-151">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="3e2cc-152">Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir</span><span class="sxs-lookup"><span data-stu-id="3e2cc-152">Retargeting target framework version may lead to incomplete Intellisense</span></span>
#### <a name="issue"></a><span data-ttu-id="3e2cc-153">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-153">Issue:</span></span>
<span data-ttu-id="3e2cc-154">Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-154">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="3e2cc-155">Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-155">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="3e2cc-156">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="3e2cc-156">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-157">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-157">Workaround:</span></span>
<span data-ttu-id="3e2cc-158">El ile geri yükleme yapın.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-158">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="3e2cc-159">`msbuild /t:restore`bir proje hedeflerken başarısız olur. Başka bir proje hedefleme NET461 başvurur. NETStandard</span><span class="sxs-lookup"><span data-stu-id="3e2cc-159">`msbuild /t:restore` fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="3e2cc-160">Sorun:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-160">Issue:</span></span>
<span data-ttu-id="3e2cc-161">.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-161">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="3e2cc-162">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="3e2cc-162">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="3e2cc-163">Geçici çözüm:</span><span class="sxs-lookup"><span data-stu-id="3e2cc-163">Workaround:</span></span>
<span data-ttu-id="3e2cc-164">Şu anda bu sorunun geçici çözümü yoktur.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-164">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="3e2cc-165">NuGet 4.0 RTM zaman çerçevesinde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3e2cc-165">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="3e2cc-166">[NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md) -NuGet 4.0 RC için düzeltilen tüm sorunları listeler</span><span class="sxs-lookup"><span data-stu-id="3e2cc-166">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

<span data-ttu-id="3e2cc-167">**Hata:**</span><span class="sxs-lookup"><span data-stu-id="3e2cc-167">**Bug:**</span></span>

* <span data-ttu-id="3e2cc-168">Visual Studio'da NuGet restore saygı projeleri - PackageId özelliği [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-168">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

* <span data-ttu-id="3e2cc-169">Paket VSIX paketi - eklerken NuGet ProjectSystemCache hata [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-169">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

* <span data-ttu-id="3e2cc-170">Paketi IncludeSource birden çok TFMs - projeyle kullanılıyorsa özel durum oluşturur [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-170">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

* <span data-ttu-id="3e2cc-171">Çözüm genelinde Update'ten kullanma VS 2017 RC3 kilitlenme paket Yönetimi - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-171">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

* <span data-ttu-id="3e2cc-172">Yeni yüklenen paket - kaldıramazsınız [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-172">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

* <span data-ttu-id="3e2cc-173">İçin PackageRef geçirirken, karma çözümleri garip geri yükleme davranışını - sahip [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-173">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

* <span data-ttu-id="3e2cc-174">En kısa sürede NuGet başlattıktan sonra oluşturma işlemi (yükleme, güncelleştirme, geri yükleme) neden olabilecek VS kilitlenmesine - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-174">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

* <span data-ttu-id="3e2cc-175">UI askıda - NuGet.SolutionRestoreManager.RestoreManagerPackage başlatma kilitlenme [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-175">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

* <span data-ttu-id="3e2cc-176">Paketi komutu sürüm öğesi - yerine özniteliği olarak ekleyin [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-176">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

* <span data-ttu-id="3e2cc-177">Foo.sln--dotnet geri yükleme başarısız olur SLN yapılandırmalarında (ancak, fark config) yinelenen projeleri geri yükleme grafiğinde - neden [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-177">Dotnet Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

* <span data-ttu-id="3e2cc-178">Yalnızca paketler - içerik [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-178">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

* <span data-ttu-id="3e2cc-179">Varsayılan olarak paket biçimi Seçici seçeneği dışında - opt [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-179">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

* <span data-ttu-id="3e2cc-180">Perf: CreateUAP_CSharp_VS.01.1.Create Proje 3,153.570 ms (%149.1) tarafından Duration_TotalElapsedTime gerileyen.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-180">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="3e2cc-181">Taban çizgisi 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-181">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

* <span data-ttu-id="3e2cc-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild çözüm tarafından 1,5 sn Duration_TotalElapsedTime gerileyen.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-182">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="3e2cc-183">Taban çizgisi 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-183">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

* <span data-ttu-id="3e2cc-184">Adaylığı başarısız çoklu TFM projelerinde - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-184">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

* <span data-ttu-id="3e2cc-185">Perf: WebForms_DDRIT.1200.Close çözüm 3.000 sayısı (% 0,5) tarafından VM_ImagesInMemory_Total_devenv gerileyen.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-185">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="3e2cc-186">Taban çizgisi 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-186">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

* <span data-ttu-id="3e2cc-187">vsfeedback - netcoreapp1.1 hedeflerken paketi uyarılar - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-187">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

* <span data-ttu-id="3e2cc-188">Bir NuGet paketi için boş ASP.NET Core web uygulaması - eklenmeye çalışılırken PathTooLongException [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-188">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

* <span data-ttu-id="3e2cc-189">Paketi çalıştıran çok sık--orada ile dotnet paketi başarısız olduğu hedef bağımlılık grafiği içeren hedef "Paketi" - Döngüsel bir bağımlılıkla [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-189">Pack runs too often -- dotnet pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

* <span data-ttu-id="3e2cc-190">Paketi çalıştıran çok sık--oluşturmak NuGet paketi, tüm yapılandırmaları - içermez [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-190">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

* <span data-ttu-id="3e2cc-191">NullReferenceException ekleme nuget C++ projesinde - packageref ile [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-191">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

* <span data-ttu-id="3e2cc-192">Erişilebilirlik: Ekran okuyucusu - paketi yüklemek için projeleri seçmek için onay kutusunu ile Anlat değil [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-192">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

* <span data-ttu-id="3e2cc-193">NuGet VS17 düzensiz aralıklarla hataya başarısız - VS hata 365798 - VSO/VSTS akışları bağlanma [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-193">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

* <span data-ttu-id="3e2cc-194">Content dosyaları alırsanız yanlış konuma çıktı ise PackagePath "Content dosyaları" - olarak yolunu belirtir, [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-194">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

* <span data-ttu-id="3e2cc-195">Paketi hedef ekler VersionSuffix - PackageVersion özelliğiyle [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-195">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

* <span data-ttu-id="3e2cc-196">Paket yolu dotnet paketiyle - işe yaramazsa belirtme [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-196">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

* <span data-ttu-id="3e2cc-197">Geri yükleme sırasında - NuGet çıkarır yinelenen içeri aktarmaları hakkında uyarılar bir grup [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-197">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

* <span data-ttu-id="3e2cc-198">"NuGet Paket Yöneticisi Format" iletişim koyu tema altında - bozuk görünüyor seçin [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-198">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

* <span data-ttu-id="3e2cc-199">VS kilitlenme yapı geri yükleme - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-199">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

* <span data-ttu-id="3e2cc-200">Visual Studio kilitlenmeleri targetframeworks içinde TFM eklerseniz kaydedin, sonra oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-200">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="3e2cc-201">Süre - % 10 [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-201">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

* <span data-ttu-id="3e2cc-202">nuget paketi, Proje başarıyla - paket üzerinde başarı iletisi çıktı değil [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-202">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

* <span data-ttu-id="3e2cc-203">PackTask System.IO.Compression 4.1 değil olması nedeniyle başarısız bulunamadı - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-203">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

* <span data-ttu-id="3e2cc-204">Paketi çalıştıran çok sık--PackTask sık sık başarısız dosya erişim çakışma - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-204">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

* <span data-ttu-id="3e2cc-205">NuGet arka plan geri yükleme sırasında - çıktı penceresi açar [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-205">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

* <span data-ttu-id="3e2cc-206">(Hangi kilitlenmesine neden) tehlikeli kodlama düzeni - ServiceProvider ortadan [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-206">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

* <span data-ttu-id="3e2cc-207">Perf/UIHang - DownloadTimeoutStream okuma - artırmak [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-207">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

* <span data-ttu-id="3e2cc-208">Visual Studio kilitlenmeleri NuGet geri yüklemesi bitmeden önce - bir projeyi kapatın çalışırsanız [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-208">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

* <span data-ttu-id="3e2cc-209">PackTask ve paketleme ile ilgili sorunları `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-209">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

* <span data-ttu-id="3e2cc-210">[vsfeedback] Yeni Proje (visual studio yeniden başlatma gerekir) - nuget paketlerini çözümlenemiyor [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-210">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

* <span data-ttu-id="3e2cc-211">[vsfeedback] "Sürüm" açılan listesi kullanılabilir paket sürümlerinin kalmak için struggles içinde eşitleme seçili nuGet paketi ile birlikte... - gösteren [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-211">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

* <span data-ttu-id="3e2cc-212">Nuget.Client kullanması gereken CPS JoinableTaskFactory ile CPS kullanılırken kilitlenmeleri - önlemek için [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-212">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

* <span data-ttu-id="3e2cc-213">NuGet 3.5.0 değil paketi açılırken `.targets` - paketten [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-213">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

* <span data-ttu-id="3e2cc-214">DotNet paketi başlığında desteklemediği `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-214">dotnet pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

* <span data-ttu-id="3e2cc-215">Hata iletişim kutusunda VS2017 RC - Install-Package sonuçlanıyor [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-215">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

* <span data-ttu-id="3e2cc-216">Kullanıcı arabirimini CPS güncelleştirme nominate açılmıyor gibi .net core proje için bir paket güncelleştirme çalışmıyor için görünür.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-216">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="3e2cc-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-217"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

* <span data-ttu-id="3e2cc-218">Çözümlenmemiş başvuru uyarısı - artırmak [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-218">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

* <span data-ttu-id="3e2cc-219">DotNet paketi - ProjectReference kaybeder sürüm bilgilerini - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-219">dotnet pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

* <span data-ttu-id="3e2cc-220">UWP uygulaması oluşturma projesi oluşturun ve geçen toplam süre gerileme - yeniden [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-220">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

* <span data-ttu-id="3e2cc-221">Başarıyla geri ileti geri yükleme sırasında bile hatasından sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-221">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="3e2cc-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-222"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

* <span data-ttu-id="3e2cc-223">Nuget.CommandLine 3.4.4 Nuget.org için-yeniden yayımlayın [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-223">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

* <span data-ttu-id="3e2cc-224">Projeleri geçirme üzerinde çıkarılıp `project.json` için `.csproj` ---geri yükleme başarısız - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-224">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

* <span data-ttu-id="3e2cc-225">Yeni oluşturulan xunit Test projede - geri yükleme başarısız [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-225">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

* <span data-ttu-id="3e2cc-226">Çekirdek projeleri askıda, UI - açık kilitlemek [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-226">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

* <span data-ttu-id="3e2cc-227">derleme görevleri - hedefleri dosyasını düzeltmek [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-227">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

* <span data-ttu-id="3e2cc-228">Hata listesi başvurulan proje - unload yapı çözümü sonra hata sahip [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-228">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

* <span data-ttu-id="3e2cc-229">MSB4057: "_GenerateRestoreGraphProjectEntry" hedef projede mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-229">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="3e2cc-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-230"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

* <span data-ttu-id="3e2cc-231">vsfeedback: çözüm için nuget Yöneticisi kullanıcı arabirimi çöküyor tüm projeleri - seçtiğinizde [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-231">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

* <span data-ttu-id="3e2cc-232">nuget.exe msbuildpath başarısız eğik - olduğunda [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-232">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

* <span data-ttu-id="3e2cc-233">vsfeedback: NuGet restore vermek LinqToTwitter proje için-birkaç proje başvurusu uyarıları [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-233">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

* <span data-ttu-id="3e2cc-234">Gelen paket `.csproj` minClientVersion özniteliği - içermez [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-234">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

* <span data-ttu-id="3e2cc-235">NuGet.Build.Tasks.Pack.dll sevk VS2017 içinde imzalı gecikme (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-235">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

* <span data-ttu-id="3e2cc-236">VSFeedback: 3.7.1 - CMake ile oluşturulan bir VS 2015 projesi için geri yükleme başarısız [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-236">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

* <span data-ttu-id="3e2cc-237">VSFeedback: Derleme sunabilir - daha ayrıntılı hata iletilerini geri yükleme hatalarını soyutlamaması [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-237">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

* <span data-ttu-id="3e2cc-238">[VSFeedback] Web projesi için NuGet paketleri geri yüklenirken hata oluştu: değer null olamaz.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-238">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="3e2cc-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-239"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

* <span data-ttu-id="3e2cc-240">Geçiş oluşturur "nesne başvurusu özel durumu NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker içinde - nesnenin" [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-240">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

* <span data-ttu-id="3e2cc-241">DotNet pack Araçları Paketi karşı - oluşturulan sürümlerle [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-241">dotnet pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

* <span data-ttu-id="3e2cc-242">Yeni arka plan geri yükleme durum çubuğunda zaman geri yüklemek için - saniye sürer milisaniye Yazar [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-242">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

* <span data-ttu-id="3e2cc-243">Üzerinde yazım hatası başarısız tüm proje başvuruları - çözümlemek [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-243">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

* <span data-ttu-id="3e2cc-244">Paket başvuru senaryolarda - PCM iş akışlarını etkinleştirin [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-244">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

* <span data-ttu-id="3e2cc-245">Yüklü paketler Yöneticisi kullanıcı Arabirimi - paketinde bulunamıyor [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-245">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

* <span data-ttu-id="3e2cc-246">DotNet paketi başarısız ise PackagePath boş - olduğunda [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-246">dotnet pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

* <span data-ttu-id="3e2cc-247">Bir Çoklu kullanıcı senaryosunda - görev başarısız geri [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-247">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

* <span data-ttu-id="3e2cc-248">NuGet paketi görevini kullanarak paket içerik türü değiştirilemiyor- [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-248">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

* <span data-ttu-id="3e2cc-249">Content varsayılan Kopyala'dosyaları için MsBuild /t:pack - yanlış [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-249">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

* <span data-ttu-id="3e2cc-250">Yükleme paketi geri yüklemesi çift günlüklerini geri yükleme paketleri iletisi - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-250">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

* <span data-ttu-id="3e2cc-251">Guardrails - kaldırma geri yükleme "çalışma zamanları" bölümünün yalnızca geçerli projeye - uygulanması [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-251">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

* <span data-ttu-id="3e2cc-252">Paketi görevi koyar içerik dosyalarının ikisi de ' içeriği /' ve ' Content dosyaları /'- [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-252">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

* <span data-ttu-id="3e2cc-253">DotNet pack3 çok etiket bölme - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-253">dotnet pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

* <span data-ttu-id="3e2cc-254">DotNet paketi: Paket projelerle sevk başvuran yinelenen alma uyarı - sonuçlarında [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-254">dotnet pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

* <span data-ttu-id="3e2cc-255">Geri yükleme VS günlüğü değil her zaman göster - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-255">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

* <span data-ttu-id="3e2cc-256">nuget Yereller Yardım metni hala paketleri önbellek - belirtilen [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-256">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

* <span data-ttu-id="3e2cc-257">Restore3 PackageReferences TargetFrameworks ile tüm çiftler.</span><span class="sxs-lookup"><span data-stu-id="3e2cc-257">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="3e2cc-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-258"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

* <span data-ttu-id="3e2cc-259">Nuget Çekmeleri MSBuild beklenmeyen sürümü VS "15" Preview 4 istisnası</span><span class="sxs-lookup"><span data-stu-id="3e2cc-259">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="3e2cc-260">Komut İstemi - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-260">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

* <span data-ttu-id="3e2cc-261">Hedefleri/özellik dosyaları geri yükleme başarısız - out yazma [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-261">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

* <span data-ttu-id="3e2cc-262">VS 15 Komut İstemi'nde - çalıştırırken, geri yükleme sırasında NuGet MSBuild olarak aynı compat dolgular saygı değil [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-262">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

* <span data-ttu-id="3e2cc-263">PackFromProjectWithDevelopmentDependencySet VS15 için - yeniden etkinleştirmek [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-263">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

* <span data-ttu-id="3e2cc-264">Harmanlama NuGet - sorun [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-264">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

* <span data-ttu-id="3e2cc-265">4.0.0.2067 RC2 ile - dağıtmayı CLI ve SDK depoları şekilde entegre [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-265">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

* <span data-ttu-id="3e2cc-266">Yeni çekirdek konsol uygulaması, Kapat çözümü, çözüm açmak ve Kapat çözüm - oluşturduğunuzda, VS askıda [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-266">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

* <span data-ttu-id="3e2cc-267">D15prerel.25916.01 karşı-kilitlenebilir açılış proje basarsa [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-267">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

* <span data-ttu-id="3e2cc-268">Belge/Yardım iletisi - dotnet/nuget.exe Yereller düzeltme [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-268">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

* <span data-ttu-id="3e2cc-269">Başında veya sonunda boşluk - sorunlarını PackTask incelemek [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-269">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

* <span data-ttu-id="3e2cc-270">DotNet paketi obj değil depo - paket [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-270">dotnet pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

* <span data-ttu-id="3e2cc-271">DotNet paketi her zaman görünüyor ProjectReference sürümü 1.0.0 için - Ayarla [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-271">dotnet pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

* <span data-ttu-id="3e2cc-272">DotNet paketi proje başvuruları ile başarısız olur ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-272">dotnet pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

* <span data-ttu-id="3e2cc-273">ProjectSystemCache.TryGetProjectNameByShortName - LockRecursionException [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-273">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

* <span data-ttu-id="3e2cc-274">MSBuild özellikleri - boşlukları kırpma [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-274">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

* <span data-ttu-id="3e2cc-275">Proje yükünü - oluşturulan iki proje olaylara birleştirmek [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-275">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

* <span data-ttu-id="3e2cc-276">P2p kitaplıklarında `project.assets.json` dosyanız yanlış sürümü - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-276">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

* <span data-ttu-id="3e2cc-277">Yanıt akışı ve kullanılabilir paket - nedeniyle kilitlenme geri [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-277">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

* <span data-ttu-id="3e2cc-278">nuget.exe MSBuild hata çıktısı - büyük miktarda üzerinde telefonu kapatın [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-278">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

* <span data-ttu-id="3e2cc-279">Derleme üzerinde geri yükleme karışım ilk kez başarısız için ikinci kez (VS senaryo sabit) - başarılı [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-279">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

<span data-ttu-id="3e2cc-280">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="3e2cc-280">**DCR:**</span></span>

* <span data-ttu-id="3e2cc-281">VSIX v3 VSIX için - v2 VSIX geçirmek [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-281">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

* <span data-ttu-id="3e2cc-282">NuGet yolu almak için bir mekanizma olmalıdır MSBuild - lock dosyasında [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-282">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

* <span data-ttu-id="3e2cc-283">Yapı varlıklar TFM uyumluluk denetimi ve varlıklar - eklemek [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-283">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

* <span data-ttu-id="3e2cc-284">Yeni ProjectCapability "Paketi" paketinde tanımlamak paketi etkinleştirme hedefleri ilgili özellikleri - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-284">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

* <span data-ttu-id="3e2cc-285">Bir post yapı olarak "GeneratePackageOnBuild" MSBuild özellikte - söylediğinizde hedef paketi çalıştırmak [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-285">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

* <span data-ttu-id="3e2cc-286">NuGet özelliği RestoreProjectStyle belirli NuGet proje - oluşturulacağı [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-286">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

* <span data-ttu-id="3e2cc-287">Geçişli proje başvuruları değiştirmek için - geri yükleme uyum [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-287">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

* <span data-ttu-id="3e2cc-288">Hedef dosyada olmayan UWP projeleri - NuGet özellikleri ekleme [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-288">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

* <span data-ttu-id="3e2cc-289">UWP TargetPlatformVersion desteği - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-289">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

* <span data-ttu-id="3e2cc-290">NuGet proje sistemine - proje başvuru meta verisi iletişim [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-290">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

* <span data-ttu-id="3e2cc-291">İçin paketleme modu - kullanıcı Arabirimi eklemek [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-291">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

* <span data-ttu-id="3e2cc-292">Eski `.csproj` NugetTargetMoniker ve proj/hedefleri - ayarlamak RuntimeIdentifiers gereken [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-292">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

* <span data-ttu-id="3e2cc-293">Yükleme paketi-restore - otomatik çakışıyor [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-293">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

* <span data-ttu-id="3e2cc-294">Bağlam menüsü QueryStatus değil durum VSPackage değil yüklendiğinde - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-294">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

* <span data-ttu-id="3e2cc-295">Çözüm geri yükleme ve yapı geri hala iletişim kutuları - Göster [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-295">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

* <span data-ttu-id="3e2cc-296">NuGet.Clients çözümü derleme - yalıtmak VSSDK sürümünde [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-296">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

<span data-ttu-id="3e2cc-297">**Özellik:**</span><span class="sxs-lookup"><span data-stu-id="3e2cc-297">**Feature:**</span></span>

* <span data-ttu-id="3e2cc-298">NuGet.Core.sln - dizeleri yerelleştirme [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-298">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

* <span data-ttu-id="3e2cc-299">Nuget zorlar LSL modunda - web uygulama projeleri yüklemek için [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-299">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

* <span data-ttu-id="3e2cc-300">Blok sürüme AutoReferenced PackageReference destek değişiklikleri kullanıcı Arabiriminde "yüklü SDK'sı" paketler için - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-300">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

* <span data-ttu-id="3e2cc-301">PackageSpec.Version (PackageRef) - proje bağımlılıkları için doğru bir şekilde iletişim [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-301">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

* <span data-ttu-id="3e2cc-302">Destek başvuruyu kaldırmak için `.csproj` commandline(s) - gelen [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-302">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

* <span data-ttu-id="3e2cc-303">Geri yükleme PackageReference projeleri (normal ve xplat) ve basit çözüm yük - desteği [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-303">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

* <span data-ttu-id="3e2cc-304">Destek içine başvurular eklemek için `.csproj` commandline(s) - gelen [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-304">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

* <span data-ttu-id="3e2cc-305">Basit çözüm yük için NuGet geri yükleme desteği `packages.config` veya `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-305">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

* <span data-ttu-id="3e2cc-306">Content dosyaları destek oluşturulan nuget hedefleri dosyasında - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-306">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

* <span data-ttu-id="3e2cc-307">Mono CI Mac üzerinde nuget.exe doğrulama için kurmak MSBuild - kullanma [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-307">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

* <span data-ttu-id="3e2cc-308">NuGet v2 NuGet.Core bağımlılıkları dışına - taşıma [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="3e2cc-308">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>


## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="3e2cc-309">GitHub sorunları RTM'de sabit bağlantılar</span><span class="sxs-lookup"><span data-stu-id="3e2cc-309">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="3e2cc-310">Konu listesi 1</span><span class="sxs-lookup"><span data-stu-id="3e2cc-310">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[<span data-ttu-id="3e2cc-311">Konu listesi 2</span><span class="sxs-lookup"><span data-stu-id="3e2cc-311">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[<span data-ttu-id="3e2cc-312">Konu listesi 3</span><span class="sxs-lookup"><span data-stu-id="3e2cc-312">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[<span data-ttu-id="3e2cc-313">Konu listesi 4</span><span class="sxs-lookup"><span data-stu-id="3e2cc-313">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[<span data-ttu-id="3e2cc-314">Konu listesi 5</span><span class="sxs-lookup"><span data-stu-id="3e2cc-314">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")

