---
title: "NuGet 2.5 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.5 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.5 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4fb696a1f4d76bdd3461df6af461f279f9f0a8b0
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="82e76-104">NuGet 2,5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="82e76-104">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="82e76-105">[NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="82e76-105">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="82e76-106">NuGet 2.5 25 Nisan 2013'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="82e76-106">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="82e76-107">Bu sürüm kadar büyük, biz 2.3 ve 2.4 sürümleri atlamak compelled Keçeli!</span><span class="sxs-lookup"><span data-stu-id="82e76-107">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="82e76-108">Biz vardı NuGet için ile büyük yayın budur bugüne kadar üzerinden [160 iş öğelerini](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) sürümde.</span><span class="sxs-lookup"><span data-stu-id="82e76-108">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="82e76-109">Katkıda Bulunanlar</span><span class="sxs-lookup"><span data-stu-id="82e76-109">Acknowledgements</span></span>

<span data-ttu-id="82e76-110">Aşağıdaki dış Katkıda Bulunanlar, önemli ölçüde katkıda NuGet 2.5 için teşekkür ederiz ister misiniz:</span><span class="sxs-lookup"><span data-stu-id="82e76-110">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="82e76-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="82e76-111">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="82e76-112">[#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid eklemek, MonoTouch ve bilinen hedef framework tanımlayıcıları listesine MonoMac.</span><span class="sxs-lookup"><span data-stu-id="82e76-112">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
1. <span data-ttu-id="82e76-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="82e76-113">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="82e76-114">[#2865](https://nuget.codeplex.com/workitem/2865) -yazımını düzeltme `NuGet.targets` büyük küçük harfe duyarlı bir işletim sistemi için</span><span class="sxs-lookup"><span data-stu-id="82e76-114">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
1. <span data-ttu-id="82e76-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="82e76-115">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="82e76-116">Mono üzerinde yapı çözümü haline getirmiştir.</span><span class="sxs-lookup"><span data-stu-id="82e76-116">Make the solution build on Mono.</span></span>
1. <span data-ttu-id="82e76-117">[Barış Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="82e76-117">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="82e76-118">Mono üzerinde başarısız olan birim testleri düzeltin.</span><span class="sxs-lookup"><span data-stu-id="82e76-118">Fix unit tests failing on Mono.</span></span>
1. <span data-ttu-id="82e76-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span><span class="sxs-lookup"><span data-stu-id="82e76-119">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="82e76-120">[#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe paketi komutu MSBuild özelliklerine yayılması değil</span><span class="sxs-lookup"><span data-stu-id="82e76-120">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
1. <span data-ttu-id="82e76-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="82e76-121">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="82e76-122">[#1511](https://nuget.codeplex.com/workitem/1511) - biçimlendirmesini korumak için işleme kodunu XML değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="82e76-122">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
1. <span data-ttu-id="82e76-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="82e76-123">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="82e76-124">Tanınan sözcükler başarılı olması build.cmd izin vermek için özel sözlüğe eklendi.</span><span class="sxs-lookup"><span data-stu-id="82e76-124">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
1. [<span data-ttu-id="82e76-125">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="82e76-125">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="82e76-126">Birim testleri yerelleştirilmiş VS üzerinde çalışırken düzeltin.</span><span class="sxs-lookup"><span data-stu-id="82e76-126">Fix unit tests when running in localized VS.</span></span>
1. [<span data-ttu-id="82e76-127">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="82e76-127">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="82e76-128">PackageService ayıklanan arabirimi</span><span class="sxs-lookup"><span data-stu-id="82e76-128">Extracted interface from PackageService</span></span>
1. <span data-ttu-id="82e76-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="82e76-129">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
    - <span data-ttu-id="82e76-130">[#936](https://nuget.codeplex.com/workitem/936) -sevk proje bağımlılıkları işleme</span><span class="sxs-lookup"><span data-stu-id="82e76-130">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
1. <span data-ttu-id="82e76-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="82e76-131">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
    - <span data-ttu-id="82e76-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -destek metin paket kaynağı kimlik bilgileri nuget.cofig dosyalarında depolarken Parolayı Temizle</span><span class="sxs-lookup"><span data-stu-id="82e76-132">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
1. <span data-ttu-id="82e76-133">[Ahmet Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="82e76-133">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
    - <span data-ttu-id="82e76-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-paket düzeltme Yardım açıklaması</span><span class="sxs-lookup"><span data-stu-id="82e76-134">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="82e76-135">Ayrıca şu kişilere hataları ile NuGet 2.5 Beta/onaylanmış ve son yayımlanmasından önce sabit RC bulmak için değer veriyoruz:</span><span class="sxs-lookup"><span data-stu-id="82e76-135">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="82e76-136">[Tony duvar](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="82e76-136">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="82e76-137">[#3200](https://nuget.codeplex.com/workitem/3200) - 2.5 yapılar ve en son NuGet 2.4 ile ayrılmış mstest'i</span><span class="sxs-lookup"><span data-stu-id="82e76-137">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="82e76-138">Sürümdeki dikkat çekici özellikleri</span><span class="sxs-lookup"><span data-stu-id="82e76-138">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="82e76-139">Kullanıcıların zaten içerik dosyalarının üzerine izin ver</span><span class="sxs-lookup"><span data-stu-id="82e76-139">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="82e76-140">Her zaman en çok istenen özelliklerden biri, bir NuGet paketi eklendiğinde diskte zaten içerik dosyalarının üzerine özelliği kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="82e76-140">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="82e76-141">NuGet 2.5 ile başlayarak, bu çakışmaları tanımlanır ve daha önce bu dosyaları her zaman Atlanan ancak dosyaların üzerine istenir.</span><span class="sxs-lookup"><span data-stu-id="82e76-141">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![İçerik dosyalarının üzerine yaz](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="82e76-143">'nuget.exe update' ve 'Install-hem de yeni bir seçeneğiniz artık Package' '-FileConflictAction' komut satırı senaryoları için bazı varsayılan ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="82e76-143">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="82e76-144">Bir dosyadan bir paketi hedef projede zaten mevcut olduğunda bir varsayılan eylem ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="82e76-144">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="82e76-145">Her zaman dosyaları üzerine yazmak için 'İçin üzerine yaz' ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="82e76-145">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="82e76-146">Dosyalarını atlamak için 'Yoksay' olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="82e76-146">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="82e76-147">Belirtilmezse, çakışan her dosya için sorar.</span><span class="sxs-lookup"><span data-stu-id="82e76-147">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="82e76-148">MSBuild hedefleri ve özellik dosyalarının otomatik alma</span><span class="sxs-lookup"><span data-stu-id="82e76-148">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="82e76-149">Yeni bir geleneksel klasör NuGet paketi en üst düzeyde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="82e76-149">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="82e76-150">Bir eşler arası olarak `\lib`, `\content`, ve `\tools`, şimdi dahil edebileceğiniz bir `\build` paketinizi klasöründe.</span><span class="sxs-lookup"><span data-stu-id="82e76-150">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="82e76-151">Bu klasörü altında sabit adlarıyla iki dosya yerleştirebilirsiniz `{packageid}.targets` veya `{packageid}.props`.</span><span class="sxs-lookup"><span data-stu-id="82e76-151">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="82e76-152">Bu iki dosya ya da doğrudan altında olabilir `build` veya diğer klasörler gibi çerçeveye özel klasörler altında.</span><span class="sxs-lookup"><span data-stu-id="82e76-152">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="82e76-153">En iyi eşleşen çerçeve klasörünün çekme için tam olarak ile aynı olan kuralıdır.</span><span class="sxs-lookup"><span data-stu-id="82e76-153">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="82e76-154">NuGet \build dosyalarıyla bir paketi yüklendiğinde, bir MSBuild ekleyecek `<Import>` öğesi işaret proje dosyasında `.targets` ve `.props` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="82e76-154">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="82e76-155">`.props` Dosya, en üstte eklenir, ancak `.targets` dosya altına eklenir.</span><span class="sxs-lookup"><span data-stu-id="82e76-155">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="82e76-156">Platform kullanarak başına farklı başvurular belirtin `<References/>` öğesi</span><span class="sxs-lookup"><span data-stu-id="82e76-156">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="82e76-157">2.5 önce içinde `.nuspec` dosyası, kullanıcı yalnızca belirtebilir tüm çerçevesi için eklenecek başvuru dosyalar.</span><span class="sxs-lookup"><span data-stu-id="82e76-157">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="82e76-158">2.5 yeni bu özellik ile kullanıcı yazabilirsiniz artık `<reference/>` öğesini her desteklenen platform için örneğin:</span><span class="sxs-lookup"><span data-stu-id="82e76-158">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="82e76-159">Nasıl NuGet göre projelere başvurular ekler için akış işte `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="82e76-159">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="82e76-160">Bul `lib` hedef çerçeve için uygun olan ve bu klasörden derleme listesini al klasör</span><span class="sxs-lookup"><span data-stu-id="82e76-160">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="82e76-161">Ayrı olarak hedef çerçeve için uygun olan başvurular grubunu bulun ve o gruptan derleme listesini alın.</span><span class="sxs-lookup"><span data-stu-id="82e76-161">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="82e76-162">Belirtilen hedef çerçevede olmadan başvuru grubu geri dönüş grubudur.</span><span class="sxs-lookup"><span data-stu-id="82e76-162">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="82e76-163">İki listelerinin kesişimini bulur ve eklemek için referans olarak kullanın</span><span class="sxs-lookup"><span data-stu-id="82e76-163">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="82e76-164">Bu yeni özellik, aksi takdirde birden çok yinelenen derlemeleri taşımak gerekir, derlemeler kümelerine farklı çerçeveleri uygulamak için başvurular bu özelliği kullanmak paketi yazarları sağlayacak `lib` klasörler.</span><span class="sxs-lookup"><span data-stu-id="82e76-164">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="82e76-165">Not: Bu özelliği kullanmak için nuget.exe paketi şu anda kullanmalısınız; Bu NuGet paketi Gezgini henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="82e76-165">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="82e76-166">Tüm paketler aynı anda güncelleştirme sağlamak için tüm düğmesini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="82e76-166">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="82e76-167">Birçoğu tüm paketlerinizi güncelleştirmek için "Güncelleştirme paketi" PowerShell cmdlet hakkında bilmeniz; Şimdi UI aracılığıyla bunu yapmanın kolay bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="82e76-167">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="82e76-168">Bu özelliği denemek için:</span><span class="sxs-lookup"><span data-stu-id="82e76-168">To try this feature out:</span></span>

1. <span data-ttu-id="82e76-169">Yeni bir ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="82e76-169">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="82e76-170">'NuGet paketlerini Yönet' iletişim kutusu başlatma</span><span class="sxs-lookup"><span data-stu-id="82e76-170">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="82e76-171">'Güncelleştirmeleri' seçin</span><span class="sxs-lookup"><span data-stu-id="82e76-171">Select 'Updates'</span></span>
1. <span data-ttu-id="82e76-172">'Tümünü Güncelleştir' düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="82e76-172">Click the 'Update All' button</span></span>

![İletişim kutusu tüm düğmesini güncelleştir](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="82e76-174">Geliştirilmiş proje başvurusu nuget.exe paketi desteği</span><span class="sxs-lookup"><span data-stu-id="82e76-174">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="82e76-175">Şimdi nuget.exe paketi komutu işlemleri aşağıdaki kuralları projelerle başvurulan:</span><span class="sxs-lookup"><span data-stu-id="82e76-175">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="82e76-176">Başvuruda bulunulan proje karşılık gelen varsa `.nuspec` dosya, örneğin adlı bir dosya yoktur `proj1.nuspec` aynı klasörde `proj1.csproj`, daha sonra bu proje kimliğini kullanarak paket için bağımlılık olarak eklenir ve sürüm okuma `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="82e76-176">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="82e76-177">Aksi takdirde, başvurulan proje dosyalarını pakete paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="82e76-177">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="82e76-178">Ardından bu proje tarafından başvurulan projeleri sames kuralları yinelemeli kullanılarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="82e76-178">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="82e76-179">Tüm DLL `.pdb`, ve `.exe` dosyaları eklenir.</span><span class="sxs-lookup"><span data-stu-id="82e76-179">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="82e76-180">Tüm içerik dosyalarının eklenir.</span><span class="sxs-lookup"><span data-stu-id="82e76-180">All other content files are added.</span></span>
1. <span data-ttu-id="82e76-181">Tüm bağımlılıkları birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="82e76-181">All dependencies are merged.</span></span>

<span data-ttu-id="82e76-182">Varsa bir bağımlılık olarak kabul edilmesi başvuruda bulunulan bir proje böylece bir `.nuspec` dosya, aksi takdirde, paketin bir parçası haline gelir.</span><span class="sxs-lookup"><span data-stu-id="82e76-182">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="82e76-183">Daha fazla ayrıntıları buraya: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="82e76-183">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="82e76-184">'En az NuGet sürümü' özelliği paketlere Ekle</span><span class="sxs-lookup"><span data-stu-id="82e76-184">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="82e76-185">'MinClientVersion' adlı yeni bir meta veri öznitelik şimdi bir paketi kullanmak için gereken en düşük NuGet istemci sürümünün olduğunu gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="82e76-185">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="82e76-186">Bu özellik, bir paket yalnızca NuGet belirli bir sürümünden sonra çalışacağını belirtmek için paket yazarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="82e76-186">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="82e76-187">Yeni `.nuspec` özellikleri, NuGet 2.5 sonra paketleri kurulamayacak en az bir NuGet sürümü talep eklenir.</span><span class="sxs-lookup"><span data-stu-id="82e76-187">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="82e76-188">NuGet yüklü 2.5 kullanıcı varsa ve bir paket 2.6 gerektiren olarak tanımlanır, görsel ipuçları paket yüklenebilir olmaz belirten kullanıcıya verilir.</span><span class="sxs-lookup"><span data-stu-id="82e76-188">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="82e76-189">Kullanıcı, kendi NuGet sürümünü güncelleştirmek için sonra yönlendirilecektir.</span><span class="sxs-lookup"><span data-stu-id="82e76-189">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="82e76-190">Bu, burada paketleri yüklemek, ancak tanınmayan şema sürümü tanımlanan belirten başarısız başlamadan varolan deneyimi artırır.</span><span class="sxs-lookup"><span data-stu-id="82e76-190">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="82e76-191">Bağımlılıklar artık gereksiz yere paket yükleme sırasında güncelleştirilir</span><span class="sxs-lookup"><span data-stu-id="82e76-191">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="82e76-192">Projede yüklü bir paket bağımlı bir paket yüklendiğinde mevcut sürümü bağımlılık memnun olsa bile NuGet 2.5 önce bağımlılık Yeni yüklemenin bir parçası güncelleştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="82e76-192">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="82e76-193">Bağımlılık sürümünü zaten sağlanıyorsa NuGet 2.5 ile başlayarak, bağımlılık diğer paket yüklemeleri sırasında güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="82e76-193">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="82e76-194">**Senaryo:**</span><span class="sxs-lookup"><span data-stu-id="82e76-194">**The scenario:**</span></span>

1. <span data-ttu-id="82e76-195">Kaynak deposu Paket B 1.0.0 ve 1.0.2 sürümüyle içerir.</span><span class="sxs-lookup"><span data-stu-id="82e76-195">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="82e76-196">Ayrıca b'de bir bağımlılığa sahip bir paket içerir (> = 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="82e76-196">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="82e76-197">Geçerli projenin Paket B sürümü 1.0.0 yüklü olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="82e76-197">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="82e76-198">Paket A. yüklemek istediğiniz şimdi</span><span class="sxs-lookup"><span data-stu-id="82e76-198">Now you want to install package A.</span></span>

<span data-ttu-id="82e76-199">**2.2 ve eski NuGet içinde:**</span><span class="sxs-lookup"><span data-stu-id="82e76-199">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="82e76-200">Paket bir yükleme sırasında NuGet otomatik B 1.0.2 için var olan sürümü 1.0.0 zaten olan bağımlılık sürümü kısıtlamasına uyan olsa bile güncelleştirilecektir > 1.0.0 =.</span><span class="sxs-lookup"><span data-stu-id="82e76-200">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="82e76-201">**2.5 ve daha yeni NuGet içinde:**</span><span class="sxs-lookup"><span data-stu-id="82e76-201">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="82e76-202">Var olan sürümü 1.0.0 bağımlılık sürümü kısıtlamasına uyan algıladığından NuGet artık B güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="82e76-202">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="82e76-203">Bu değişiklik hakkında daha fazla arka plan için ayrıntılı okuma [iş öğesi](http://nuget.codeplex.com/workitem/1681) yanı sıra ilgili [tartışma iş parçacığı](http://nuget.codeplex.com/discussions/436712).</span><span class="sxs-lookup"><span data-stu-id="82e76-203">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="82e76-204">nuget.exe http isteklerini ile ayrıntılı ayrıntı çıkarır.</span><span class="sxs-lookup"><span data-stu-id="82e76-204">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="82e76-205">Nuget.exe sorun giderme ya da yalnızca merak hangi HTTP isteklerinin yapılma işlemler sırasında '-ayrıntılı ayrıntı ' anahtar şimdi yapılan tüm HTTP istekleri çıktı.</span><span class="sxs-lookup"><span data-stu-id="82e76-205">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![HTTP nuget.exe çıktısı](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="82e76-207">nuget.exe itme şimdi UNC ve klasör kaynakları destekler</span><span class="sxs-lookup"><span data-stu-id="82e76-207">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="82e76-208">Bir UNC yolu veya yerel klasör, temel alan bir paket kaynağı için 'nuget.exe push' çalıştırmayı deneyen, NuGet 2.5 önce gönderme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="82e76-208">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="82e76-209">Son eklenen hiyerarşik yapılandırma özelliğiyle, UNC/klasör kaynak ya da bir HTTP tabanlı NuGet galerisinde hedeflemek gerek nuget.exe için yaygın hale.</span><span class="sxs-lookup"><span data-stu-id="82e76-209">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="82e76-210">Nuget.exe bir UNC/klasör kaynağı tanımlarsa NuGet 2.5 ile başlayarak, kaynak dosya kopyalama işlemini gerçekleştirecek.</span><span class="sxs-lookup"><span data-stu-id="82e76-210">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="82e76-211">Aşağıdaki komut artık çalışır:</span><span class="sxs-lookup"><span data-stu-id="82e76-211">The following command will now work:</span></span>

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="82e76-212">nuget.exe açıkça belirtilen yapılandırma dosyalarını destekler</span><span class="sxs-lookup"><span data-stu-id="82e76-212">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="82e76-213">Yapılandırma (Tümü 'Özellikler' ve 'paketi' dışında) şimdi erişim nuget.exe komutları desteği yeni bir '-ConfigFile' % AppData%\nuget\Nuget.Config varsayılan yapılandırma dosyası yerine kullanılacak özel yapılandırma dosyası zorlar seçeneği.</span><span class="sxs-lookup"><span data-stu-id="82e76-213">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="82e76-214">Örnek:</span><span class="sxs-lookup"><span data-stu-id="82e76-214">Example:</span></span>

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="82e76-215">Yerel projeleri için desteği</span><span class="sxs-lookup"><span data-stu-id="82e76-215">Support for Native projects</span></span>

<span data-ttu-id="82e76-216">NuGet 2.5 ile NuGet araç artık Visual Studio'da yerel projeleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="82e76-216">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="82e76-217">En yerel paketleri yukarıdaki MSBuild içeri aktarmalar özelliğini kullanan tarafından oluşturulan bir aracı kullanarak bekliyoruz [CoApp proje](http://coapp.org).</span><span class="sxs-lookup"><span data-stu-id="82e76-217">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="82e76-218">Daha fazla bilgi için okuma [aracı hakkındaki ayrıntıları](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="82e76-218">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="82e76-219">"Yerel" hedef framework adını, paket yerel bir projeye yüklendiğinde \build, \content ve \tools dosyaları dahil edilecek paketler için sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="82e76-219">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="82e76-220">\`Lib' klasörüne yerel projeleri için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="82e76-220">The \`lib` folder is not used for native projects.</span></span>
