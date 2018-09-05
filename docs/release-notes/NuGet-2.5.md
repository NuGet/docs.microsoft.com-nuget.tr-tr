---
title: NuGet 2.5 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.5 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550489"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="d6e8b-103">NuGet 2.5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d6e8b-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="d6e8b-104">[2.2.1 NuGet sürüm notları](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="d6e8b-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="d6e8b-105">NuGet 2.5 25 Nisan 2013 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="d6e8b-106">Bu sürüm, bu nedenle büyük, biz sürüm 2.3 ve 2.4 atlamak compelled düşünmüştür!</span><span class="sxs-lookup"><span data-stu-id="d6e8b-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="d6e8b-107">Bugüne kadar bu vardı için NuGet, ile büyük sürümdür üzerinden [160 iş öğelerini](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) sürümde.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="d6e8b-108">Onayları</span><span class="sxs-lookup"><span data-stu-id="d6e8b-108">Acknowledgements</span></span>

<span data-ttu-id="d6e8b-109">Aşağıdaki harici Katkıda Bulunanlar, NuGet 2.5 önemli katkılar için teşekkür ederiz istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="d6e8b-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="d6e8b-111">[#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid ekleyin ve MonoTouch MonoMac bilinen hedef framework tanımlayıcılarının listesi.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="d6e8b-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="d6e8b-113">[#2865](https://nuget.codeplex.com/workitem/2865) -yazımını düzeltin `NuGet.targets` büyük küçük harfe duyarlı bir işletim sistemi için</span><span class="sxs-lookup"><span data-stu-id="d6e8b-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="d6e8b-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="d6e8b-115">Mono üzerinde derleme çözümü haline getirmiştir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="d6e8b-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="d6e8b-117">Mono üzerinde başarısız olan birim testlerini düzeltin.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="d6e8b-118">[Yazan Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="d6e8b-119">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe paketi komut MSBuild özellikleri yaymak değil</span><span class="sxs-lookup"><span data-stu-id="d6e8b-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="d6e8b-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="d6e8b-121">[#1511](https://nuget.codeplex.com/workitem/1511) - biçimlendirmesini korumak için işleme kodunu XML değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="d6e8b-122">[ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="d6e8b-123">Tanınan sözcükleri build.cmd başarılı olması izin vermek için özel sözlük eklendi.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="d6e8b-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="d6e8b-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="d6e8b-125">Birim testleri, yerelleştirilmiş VS'de çalıştırırken düzeltin.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="d6e8b-126">Jones'un Evans</span><span class="sxs-lookup"><span data-stu-id="d6e8b-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="d6e8b-127">Ayıklanan PackageService arabirimi</span><span class="sxs-lookup"><span data-stu-id="d6e8b-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="d6e8b-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="d6e8b-129">[#936](https://nuget.codeplex.com/workitem/936) -sevk işlemek proje bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="d6e8b-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="d6e8b-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="d6e8b-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -destek metin paket kaynağı kimlik bilgileri nuget.cofig dosyalarında depolarken Parolayı Temizle</span><span class="sxs-lookup"><span data-stu-id="d6e8b-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="d6e8b-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="d6e8b-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package düzeltin Yardım açıklaması</span><span class="sxs-lookup"><span data-stu-id="d6e8b-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="d6e8b-134">Ayrıca aşağıdaki kişiler ile NuGet 2.5 Beta/Onaylandı ve önce son sürümde düzeltilecek RC hataları bulmak için veriyoruz:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="d6e8b-135">[Tony duvar](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="d6e8b-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="d6e8b-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest 2,5 derlemeler ve en son NuGet 2.4 ile ayrılmış</span><span class="sxs-lookup"><span data-stu-id="d6e8b-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="d6e8b-137">Sürümündeki önemli özelliklere</span><span class="sxs-lookup"><span data-stu-id="d6e8b-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="d6e8b-138">Kullanıcıların içerik zaten mevcut dosyaların üzerine yaz</span><span class="sxs-lookup"><span data-stu-id="d6e8b-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="d6e8b-139">Her zaman, en çok istenen özelliklerden biri, bir NuGet paketi eklendiğinde diskte zaten mevcut içerik dosyalarının üzerine yazılmasını olmuştur.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="d6e8b-140">NuGet 2.5 ile başlayarak, bu çakışmaları tanımlanır ve bu dosyaları her zaman önceden atlandı ise dosyaların üzerine yazıp istenir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![İçerik dosyaların üzerine yaz](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="d6e8b-142">'nuget.exe Güncelleştirme' ve 'Yükle-hem de yeni bir seçenek artık paket' '-FileConflictAction' komut satırı senaryoları için bazı varsayılan ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="d6e8b-143">Bir paket dosyasından hedef projede zaten mevcut olduğunda, varsayılan eylem ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="d6e8b-144">Her zaman dosyaların üzerine yaz 'İçin üstüne yaz' ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="d6e8b-145">Dosyalarını atlamak için 'Yoksay' olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="d6e8b-146">Belirtilmezse, çakışan her dosya için ister.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="d6e8b-147">MSBuild hedeflerini ve özellik dosyalarının otomatik içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="d6e8b-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="d6e8b-148">NuGet paketini en üst düzeyinde yeni bir geleneksel klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="d6e8b-149">Eşler arası olarak `\lib`, `\content`, ve `\tools`, artık dahil edebilirsiniz bir `\build` paketinizdeki klasör.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="d6e8b-150">Bu klasör altında sabit adlara sahip iki dosya yerleştirebilirsiniz `{packageid}.targets` veya `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="d6e8b-151">Bu iki dosyayı doğrudan altında olabilir `build` veya diğer klasörler gibi çerçeveye özgü klasörlere.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="d6e8b-152">En iyi eşleşen çerçeve klasörü çekme için tam olarak aynı olduğu gibi bu kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="d6e8b-153">NuGet paketi \build dosyalarıyla yüklendiğinde bir MSBuild ekleyeceksiniz `<Import>` öğesini işaret eden proje dosyasında `.targets` ve `.props` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="d6e8b-154">`.props` Dosya, en üstüne eklenir, ancak `.targets` dosyasının alt kısmına eklenir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="d6e8b-155">Her bir platform kullanarak farklı başvuruları belirtin `<References/>` öğesi</span><span class="sxs-lookup"><span data-stu-id="d6e8b-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="d6e8b-156">2.5 önce içinde `.nuspec` dosyası, kullanıcı yalnızca belirtebilirsiniz tüm framework eklenmesi için başvuru dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="d6e8b-157">2.5 içinde bu yeni özellik ile kullanıcı yazabilirsiniz artık `<reference/>` öğesini her desteklenen platform, örneğin:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

<span data-ttu-id="d6e8b-158">Akışın nasıl NuGet göre projelerine başvurular ekler için işte `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="d6e8b-159">Bulma `lib` hedef çerçeve için uygun olan ve bu klasörden derlemelerin listesini alma klasörü</span><span class="sxs-lookup"><span data-stu-id="d6e8b-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="d6e8b-160">Ayrı olarak hedef çerçeve için uygun olan başvuruları grubunu bulun ve o gruptan derlemelerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="d6e8b-161">Belirtilen hedef Framework'ü olmadan başvuru grubu geri dönüş grubudur.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="d6e8b-162">İki listelerinin kesişimini bulun ve eklemek için başvuru olarak kullanın</span><span class="sxs-lookup"><span data-stu-id="d6e8b-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="d6e8b-163">Bu yeni özellik, aksi takdirde birden çok yinelenen derlemeleri gerçekleştirmek gerekir, farklı çerçeveler için derlemeleri kümelerine uygulamak için başvurular bu özelliği kullanmak paket yazarlarının sağlayacak `lib` klasörleri.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="d6e8b-164">Not: Bu özelliği kullanmak için nuget.exe paketi şu anda kullanmalısınız; NuGet paket Gezgini henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="d6e8b-165">Tüm paketleri aynı anda güncelleştirilmesini sağlayacak şekilde tüm düğme güncelleştir</span><span class="sxs-lookup"><span data-stu-id="d6e8b-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="d6e8b-166">Birçoğunuzun tüm paketleriniz güncelleştirmek için "Update-Package" PowerShell cmdlet'i hakkında bilmeniz; Şimdi de kullanıcı Arabirimi aracılığıyla bunu yapmanın kolay bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="d6e8b-167">Bu özelliği denemek için:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-167">To try this feature out:</span></span>

1. <span data-ttu-id="d6e8b-168">Yeni bir ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6e8b-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="d6e8b-169">'NuGet paketlerini Yönet' iletişim kutusunu başlatma</span><span class="sxs-lookup"><span data-stu-id="d6e8b-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="d6e8b-170">'Güncelleştirmeleri' seçin</span><span class="sxs-lookup"><span data-stu-id="d6e8b-170">Select 'Updates'</span></span>
1. <span data-ttu-id="d6e8b-171">'Tümünü Güncelleştir' düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="d6e8b-171">Click the 'Update All' button</span></span>

![İletişim kutusundaki tüm düğme güncelleştir](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="d6e8b-173">Nuget.exe paketi için geliştirilmiş proje başvurusu desteği</span><span class="sxs-lookup"><span data-stu-id="d6e8b-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="d6e8b-174">Artık nuget.exe paketi komut işlemleri, aşağıdaki kurallar ile projeye başvuruyor:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="d6e8b-175">Başvurulan projenin karşılık gelen varsa `.nuspec` dosya, örneğin adlı bir dosya var. `proj1.nuspec` aynı klasörde `proj1.csproj`, ardından bu proje paketi kimliğini kullanarak, bir bağımlılık olarak eklenir ve sürüm okuma `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="d6e8b-176">Aksi takdirde, dosyaları başvurulan projenin pakete paketlenir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="d6e8b-177">Ardından bu proje tarafından başvurulan projeler sames kuralları yinelemeli olarak kullanılarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="d6e8b-178">Tüm DLL `.pdb`, ve `.exe` dosyalar eklenir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="d6e8b-179">Tüm içerik dosyalarını eklenir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-179">All other content files are added.</span></span>
1. <span data-ttu-id="d6e8b-180">Tüm bağımlılıkları birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-180">All dependencies are merged.</span></span>

<span data-ttu-id="d6e8b-181">Başvurulan bir proje varsa, bağımlılık olarak değerlendirilmesini sağlar ve böylece bir `.nuspec` dosya, aksi takdirde, paketinin bir parçası haline gelir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="d6e8b-182">Buradan daha fazla ayrıntı: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="d6e8b-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="d6e8b-183">'En düşük NuGet sürümü' özelliği paketlere Ekle</span><span class="sxs-lookup"><span data-stu-id="d6e8b-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="d6e8b-184">'MinClientVersion' adlı yeni bir meta veri öznitelik, bir paketi kullanmak için gereken en düşük NuGet istemci sürümü artık belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="d6e8b-185">Bu özellik, bir paket nuget yalnızca belirli bir sürümü sonra çalışacağını belirtmek için paket yazarı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="d6e8b-186">Yeni `.nuspec` özellikleri eklendi NuGet 2.5 sonra paketleri en az bir NuGet sürümü talep mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="d6e8b-187">NuGet yüklü 2.5 kullanıcı varsa ve bir paket 2.6 gerektiren olarak tanımlandığında, görsel ipuçları paket yüklenebilir olması değil belirten kullanıcıya verilir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="d6e8b-188">Kullanıcı, ardından kendi NuGet sürümünü güncelleştirmek için yönlendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="d6e8b-189">Bu, burada paketleri yükleyin ancak tanınmayan şema sürümü tanımlanan belirten ardından başarısız başlamadan mevcut deneyimi elde edilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="d6e8b-190">Bağımlılıkları paket yükleme sırasında artık gereksiz bir şekilde güncelleştirilir</span><span class="sxs-lookup"><span data-stu-id="d6e8b-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="d6e8b-191">Projede zaten yüklü bir paket bağımlı bir paket yüklendiğinde bile var olan sürüm bağımlılığı karşıladı NuGet 2.5 önce bağımlılık yeni yüklemesinin bir parçası güncelleştirilecek.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="d6e8b-192">Bir bağımlılık sürümü zaten getirildiyse NuGet 2.5 ile başlayarak, bağımlılık diğer paket yüklemeleri sırasında güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="d6e8b-193">**Senaryo:**</span><span class="sxs-lookup"><span data-stu-id="d6e8b-193">**The scenario:**</span></span>

1. <span data-ttu-id="d6e8b-194">Kaynak deposu, sürüm 1.0.0 ve 1.0.2 ile paket B içerir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="d6e8b-195">Ayrıca, B'bir bağımlılığa sahip bir paketi içerir (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="d6e8b-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="d6e8b-196">Geçerli proje Paket B sürüm 1.0.0 yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="d6e8b-197">Şimdi paket A. yüklemek istediğiniz</span><span class="sxs-lookup"><span data-stu-id="d6e8b-197">Now you want to install package A.</span></span>

<span data-ttu-id="d6e8b-198">**2.2 ve eski NuGet içinde:**</span><span class="sxs-lookup"><span data-stu-id="d6e8b-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="d6e8b-199">Paket bir yükleme sırasında NuGet otomatik B 1.0.2 için var olan sürüm 1.0.0 zaten olan bağımlılık sürüm kısıtlamasını karşılayan olsa da güncelleştirilecektir > 1.0.0 =.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="d6e8b-200">**2,5 ve daha yeni NuGet içinde:**</span><span class="sxs-lookup"><span data-stu-id="d6e8b-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="d6e8b-201">Var olan sürüm 1.0.0 bağımlılık sürüm kısıtlamasını karşılayan algıladığından NuGet artık B güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="d6e8b-202">Bu değişiklikle ilgili daha fazla arka plan için ayrıntılı okuma [iş öğesi](http://nuget.codeplex.com/workitem/1681) yanı sıra ilgili [tartışma](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="d6e8b-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="d6e8b-203">nuget.exe http istekleri ile ayrıntılı ayrıntı çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="d6e8b-204">Nuget.exe giderirken veya yalnızca merak hangi HTTP isteklerinin yapılan işlemler sırasında '-ayrıntılı ayrıntı ' anahtar artık tüm HTTP isteklerini çıktı.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![Nuget.exe HTTP çıktısı](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="d6e8b-206">nuget.exe anında iletme UNC ve klasör kaynakları artık destekler.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="d6e8b-207">NuGet 2.5 önce bir UNC yolu veya yerel klasör, temel bir paket kaynağı için 'nuget.exe push' çalıştırmayı denedi, anında iletme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="d6e8b-208">Son eklenen hiyerarşik yapılandırma özelliğiyle UNC veya klasörün kaynak ya da bir HTTP tabanlı NuGet galerisinde hedeflemeniz gerektiği nuget.exe için ortak pazarlanmasının.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="d6e8b-209">Nuget.exe UNC veya klasörün kaynak tanımlıyorsa NuGet 2.5 ile başlayarak, kaynak dosya kopyalama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="d6e8b-210">Aşağıdaki komutu artık çalışır:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-210">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="d6e8b-211">nuget.exe açıkça belirtilen yapılandırma dosyalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="d6e8b-212">artık yapılandırma (Tümü 'Özellikler' ve 'paketi' hariç) erişen nuget.exe komut yeni bir destek '-ConfigFile' seçeneği, varsayılan yapılandırma dosyası % AppData%\nuget\Nuget.Config yerine kullanılacak özel bir yapılandırma dosyasını zorlar.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="d6e8b-213">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d6e8b-213">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="d6e8b-214">Yerel projeleri için destek</span><span class="sxs-lookup"><span data-stu-id="d6e8b-214">Support for Native projects</span></span>

<span data-ttu-id="d6e8b-215">NuGet 2.5 ile NuGet araçları artık Visual Studio'da yerel projeleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="d6e8b-216">En yerel paketler, yukarıdaki MSBuild Imports özelliğini yararlanacaktır tarafından oluşturulan bir araç kullanarak bekliyoruz [CoApp proje](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="d6e8b-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="d6e8b-217">Daha fazla bilgi için okuma [aracı hakkındaki ayrıntıları](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="d6e8b-218">Hedef Çerçeve adı "yerel" paketi bir yerel projeye yüklendiğinde \build, \content ve \tools dosyaları eklenip eklenmeyeceğini paketler için kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="d6e8b-219">\`Lib' klasörü yerel projeleri için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="d6e8b-219">The \`lib` folder is not used for native projects.</span></span>
