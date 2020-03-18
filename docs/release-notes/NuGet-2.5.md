---
title: NuGet 2,5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,5 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428718"
---
# <a name="nuget-25-release-notes"></a><span data-ttu-id="78e8e-103">NuGet 2,5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="78e8e-103">NuGet 2.5 Release Notes</span></span>

<span data-ttu-id="78e8e-104">[NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md) | [NuGet 2,6 sürüm notları](../release-notes/nuget-2.6.md)</span><span class="sxs-lookup"><span data-stu-id="78e8e-104">[NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md)</span></span>

<span data-ttu-id="78e8e-105">NuGet 2,5, 25 Nisan 2013 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="78e8e-105">NuGet 2.5 was released on April 25, 2013.</span></span> <span data-ttu-id="78e8e-106">Bu sürüm çok büyük, 2,3 ve 2,4 sürümlerini atlamak için etmek zorunda kalırsak!</span><span class="sxs-lookup"><span data-stu-id="78e8e-106">This release was so big, we felt compelled to skip versions 2.3 and 2.4!</span></span> <span data-ttu-id="78e8e-107">Bu, yayında 160 ' den fazla [iş öğesi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ile NuGet için sahip olduğumuz en büyük sürümdür.</span><span class="sxs-lookup"><span data-stu-id="78e8e-107">To date, this is the largest release we've had for NuGet, with over [160 work items](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) in the release.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="78e8e-108">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="78e8e-108">Acknowledgements</span></span>

<span data-ttu-id="78e8e-109">NuGet 2,5 ' e yönelik önemli katkılarına yönelik olarak aşağıdaki dış katkıda bulunanlar için teşekkür ederiz:</span><span class="sxs-lookup"><span data-stu-id="78e8e-109">We would like to thank the following external contributors for their significant contributions to NuGet 2.5:</span></span>

1. <span data-ttu-id="78e8e-110">[Daniel Plaıted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span><span class="sxs-lookup"><span data-stu-id="78e8e-110">[Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))</span></span>
    - <span data-ttu-id="78e8e-111">[#2847](https://nuget.codeplex.com/workitem/2847) , bilinen hedef çerçeve tanımlayıcıları listesine monoandroid, MonoTouch ve monomac 'i ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78e8e-111">[#2847](https://nuget.codeplex.com/workitem/2847) - Add MonoAndroid, MonoTouch, and MonoMac to the list of known target framework identifiers.</span></span>
2. <span data-ttu-id="78e8e-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span><span class="sxs-lookup"><span data-stu-id="78e8e-112">[Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))</span></span>
    - <span data-ttu-id="78e8e-113">[#2865](https://nuget.codeplex.com/workitem/2865) -büyük/küçük harfe duyarlı bir işletim sistemi için `NuGet.targets` yazımını onarma</span><span class="sxs-lookup"><span data-stu-id="78e8e-113">[#2865](https://nuget.codeplex.com/workitem/2865) - Fix spelling of `NuGet.targets` for a case-sensitive OS</span></span>
3. <span data-ttu-id="78e8e-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="78e8e-114">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="78e8e-115">Çözümü mono üzerinde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78e8e-115">Make the solution build on Mono.</span></span>
4. <span data-ttu-id="78e8e-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span><span class="sxs-lookup"><span data-stu-id="78e8e-116">[Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))</span></span>
    - <span data-ttu-id="78e8e-117">Mono üzerinde başarısız olan birim testlerini düzeltir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-117">Fix unit tests failing on Mono.</span></span>
5. <span data-ttu-id="78e8e-118">[Kayvier Dadgen@OliIsCoola](https://www.codeplex.com/site/users/view/OliIsCool) [ ](https://twitter.com/oliiscool)</span><span class="sxs-lookup"><span data-stu-id="78e8e-118">[Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))</span></span>
    - <span data-ttu-id="78e8e-119">[#2920](https://nuget.codeplex.com/workitem/2920) -NuGet. exe paketi komutu özellikleri MSBuild 'e yayılmaz</span><span class="sxs-lookup"><span data-stu-id="78e8e-119">[#2920](https://nuget.codeplex.com/workitem/2920) - nuget.exe pack command does not propagate Properties to MSBuild</span></span>
6. <span data-ttu-id="78e8e-120">[MIROSLAV Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span><span class="sxs-lookup"><span data-stu-id="78e8e-120">[Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))</span></span>
    - <span data-ttu-id="78e8e-121">[#1511](https://nuget.codeplex.com/workitem/1511) -biçimlendirmeyi korumak için XML işleme kodu değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="78e8e-121">[#1511](https://nuget.codeplex.com/workitem/1511) - Modified XML handling code to preserve formatting.</span></span>
7. <span data-ttu-id="78e8e-122">[Adam Canph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="78e8e-122">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="78e8e-123">Build. cmd ' nin başarılı olmasını sağlamak için özel sözlüğe tanınan sözcükler eklendi.</span><span class="sxs-lookup"><span data-stu-id="78e8e-123">Added recognized words to custom dictionary to allow build.cmd to succeed.</span></span>
8. [<span data-ttu-id="78e8e-124">Bruno Roggeri</span><span class="sxs-lookup"><span data-stu-id="78e8e-124">Bruno Roggeri</span></span>](https://www.codeplex.com/site/users/view/broggeri)
    - <span data-ttu-id="78e8e-125">Yerelleştirilmiş Ile çalışırken birim testlerini düzeltir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-125">Fix unit tests when running in localized VS.</span></span>
9. [<span data-ttu-id="78e8e-126">Gareth Evans</span><span class="sxs-lookup"><span data-stu-id="78e8e-126">Gareth Evans</span></span>](https://www.codeplex.com/site/users/view/garethevans)
    - <span data-ttu-id="78e8e-127">PackageService 'ten arabirim ayıklandı</span><span class="sxs-lookup"><span data-stu-id="78e8e-127">Extracted interface from PackageService</span></span>
10. <span data-ttu-id="78e8e-128">[MAXIME deneme Gidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span><span class="sxs-lookup"><span data-stu-id="78e8e-128">[Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))</span></span>
     - <span data-ttu-id="78e8e-129">Paketleme sırasında Proje bağımlılıklarını [#936](https://nuget.codeplex.com/workitem/936) işle</span><span class="sxs-lookup"><span data-stu-id="78e8e-129">[#936](https://nuget.codeplex.com/workitem/936) - Handle project dependencies when packing</span></span>
11. <span data-ttu-id="78e8e-130">[Xavier Ayrışıcı](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span><span class="sxs-lookup"><span data-stu-id="78e8e-130">[Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))</span></span>
     - <span data-ttu-id="78e8e-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -paket kaynağı kimlik bilgilerini NuGet. cofıg dosyalarında depolarken şifresiz metin parolasını destekler</span><span class="sxs-lookup"><span data-stu-id="78e8e-131">[#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) - Support Clear Text Password when storing package source credentials in nuget.cofig files</span></span>
12. <span data-ttu-id="78e8e-132">[James Manş](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span><span class="sxs-lookup"><span data-stu-id="78e8e-132">[James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))</span></span>
     - <span data-ttu-id="78e8e-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -çözüm al-Package yardım açıklaması</span><span class="sxs-lookup"><span data-stu-id="78e8e-133">[#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) - Fix Get-Package help description</span></span>

<span data-ttu-id="78e8e-134">Son sürümden önce onaylanan ve düzeltilen NuGet 2,5 Beta/RC ile hataları bulmak için aşağıdaki bireyler de bizim için de teşekkür ederiz:</span><span class="sxs-lookup"><span data-stu-id="78e8e-134">We also appreciate the following individuals for finding bugs with NuGet 2.5 Beta/RC that were approved and fixed before the final release:</span></span>

1. <span data-ttu-id="78e8e-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ,[@CodeChief](https://twitter.com/codechief))</span><span class="sxs-lookup"><span data-stu-id="78e8e-135">[Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))</span></span>
    - <span data-ttu-id="78e8e-136">[#3200](https://nuget.codeplex.com/workitem/3200) -MSTest, son NuGet 2,4 ve 2,5 Derlemeleriyle kesildi</span><span class="sxs-lookup"><span data-stu-id="78e8e-136">[#3200](https://nuget.codeplex.com/workitem/3200) - MSTest broken with lastest NuGet 2.4 and 2.5 builds</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="78e8e-137">Yayındaki önemli özellikler</span><span class="sxs-lookup"><span data-stu-id="78e8e-137">Notable features in the release</span></span>

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a><span data-ttu-id="78e8e-138">Kullanıcıların zaten var olan içerik dosyalarının üzerine yazmasına izin ver</span><span class="sxs-lookup"><span data-stu-id="78e8e-138">Allow users to overwrite content files that already exist</span></span>

<span data-ttu-id="78e8e-139">Her zaman en çok istenen özelliklerden biri, bir NuGet paketine dahil edildiğinde diskte zaten bulunan içerik dosyalarının üzerine yazılmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="78e8e-139">One of the most requested features of all time has been the ability to overwrite content files that already exist on disk when included in a NuGet package.</span></span> <span data-ttu-id="78e8e-140">NuGet 2,5 ' den itibaren bu çakışmalar tanımlanır ve dosyaların üzerine yazmanız istenir, ancak daha önce bu dosyalar her zaman atlanır.</span><span class="sxs-lookup"><span data-stu-id="78e8e-140">Starting with NuGet 2.5, these conflicts are identified and you are prompted to overwrite the files, whereas previously these files were always skipped.</span></span>

![İçerik dosyalarının üzerine yaz](./media/NuGet-2.5/overwrite-file.png)

<span data-ttu-id="78e8e-142">' NuGet. exe Update ' ve ' Install-Package ' artık komut satırı senaryoları için bazı varsayılan değer ayarlamak üzere '-FileConflictAction ' adlı yeni bir seçeneğe sahip.</span><span class="sxs-lookup"><span data-stu-id="78e8e-142">'nuget.exe update' and 'Install-Package' now both have a new option '-FileConflictAction' to set some default for command-line scenarios.</span></span>

<span data-ttu-id="78e8e-143">Hedef projede bir paketten bir dosya zaten mevcut olduğunda varsayılan bir eylem ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78e8e-143">Set a default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="78e8e-144">Dosyaların üzerine her zaman yazılacak ' üzerine yaz ' olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78e8e-144">Set to 'Overwrite' to always overwrite files.</span></span> <span data-ttu-id="78e8e-145">Dosyaları atlamak için ' Yoksay ' olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78e8e-145">Set to 'Ignore' to skip files.</span></span> <span data-ttu-id="78e8e-146">Belirtilmemişse, her çakışan dosya istenir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-146">If not specified, it will prompt for each conflicting file.</span></span>

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a><span data-ttu-id="78e8e-147">MSBuild hedeflerini ve props dosyalarını otomatik içe aktarma</span><span class="sxs-lookup"><span data-stu-id="78e8e-147">Automatic import of MSBuild targets and props files</span></span>

<span data-ttu-id="78e8e-148">NuGet paketinin en üst düzeyinde yeni bir geleneksel klasör oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="78e8e-148">A new conventional folder has been created at the top level of the NuGet package.</span></span>  <span data-ttu-id="78e8e-149">`\lib`, `\content`ve `\tools`için bir eş olarak, artık paketinize bir `\build` klasörü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78e8e-149">As a peer to `\lib`, `\content`, and `\tools`, you can now include a `\build` folder in your package.</span></span>  <span data-ttu-id="78e8e-150">Bu klasör altında, sabit adlara, `{packageid}.targets` veya `{packageid}.props`sahip iki dosya yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78e8e-150">Under this folder, you can place two files with fixed names, `{packageid}.targets` or `{packageid}.props`.</span></span> <span data-ttu-id="78e8e-151">Bu iki dosya doğrudan `build` veya diğer klasörlerde olduğu gibi çerçeveye özgü klasörler altında olabilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-151">These two files can be either directly under `build` or under framework-specific folders just like the other folders.</span></span> <span data-ttu-id="78e8e-152">En iyi eşleşen çerçeve klasörünü çekmeye yönelik kural, bunlar ile tamamen aynıdır.</span><span class="sxs-lookup"><span data-stu-id="78e8e-152">The rule for picking the best-matched framework folder is exactly the same as in those.</span></span>

<span data-ttu-id="78e8e-153">NuGet, \Build dosyalarını içeren bir paket yüklediğinde, proje dosyasında `.targets` ve `.props` dosyalarını işaret eden bir MSBuild `<Import>` öğesi ekler.</span><span class="sxs-lookup"><span data-stu-id="78e8e-153">When NuGet installs a package with \build files, it will add an MSBuild `<Import>` element in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="78e8e-154">`.props` dosyası en üste eklenir, ancak `.targets` dosyası en alta eklenir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-154">The `.props` file is added at the top, whereas the `.targets` file is added to the bottom.</span></span>

### <a name="specify-different-references-per-platform-using-references-element"></a><span data-ttu-id="78e8e-155">`<References/>` öğesi kullanarak her platform için farklı başvurular belirtin</span><span class="sxs-lookup"><span data-stu-id="78e8e-155">Specify different references per platform using `<References/>` element</span></span>

<span data-ttu-id="78e8e-156">2,5 öncesinde, `.nuspec` dosyasında, Kullanıcı yalnızca tüm Framework için eklenmek üzere başvuru dosyalarını belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-156">Before 2.5, in `.nuspec` file, user can only specify the reference files, to be added for all framework.</span></span> <span data-ttu-id="78e8e-157">Artık 2,5 sürümündeki bu yeni özellik sayesinde, Kullanıcı desteklenen her platformun her biri için `<reference/>` öğesini yazabilir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="78e8e-157">Now with this new feature in 2.5, user can author the `<reference/>` element for each of the supported platform, for example:</span></span>

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

<span data-ttu-id="78e8e-158">NuGet 'in `.nuspec` dosyasına göre projelere nasıl başvurular eklediği Flow aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="78e8e-158">Here is the flow for how NuGet adds references to projects based on the `.nuspec` file:</span></span>

1. <span data-ttu-id="78e8e-159">Hedef Framework için uygun olan `lib` klasörünü bulun ve bu klasörden derlemelerin listesini alın</span><span class="sxs-lookup"><span data-stu-id="78e8e-159">Find the `lib` folder that is appropriate for the target framework and get the list of assemblies from that folder</span></span>
1. <span data-ttu-id="78e8e-160">Hedef çerçeve için uygun olan başvurular grubunu ayrı olarak bulun ve bu gruptaki derlemelerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="78e8e-160">Separately find the references group that is appropriate for the target framework and get the list of assemblies from that group.</span></span> <span data-ttu-id="78e8e-161">Hedef çerçevesi olmayan başvuru grubu, geri dönüş grubudur.</span><span class="sxs-lookup"><span data-stu-id="78e8e-161">Reference group without target framework specified is the fallback group.</span></span>
1. <span data-ttu-id="78e8e-162">İki listenin kesişimini bulun ve bunları eklemek için başvurular olarak kullanın</span><span class="sxs-lookup"><span data-stu-id="78e8e-162">Find the intersection of the two lists, and use that as the references to add</span></span>

<span data-ttu-id="78e8e-163">Bu yeni özellik, paket yazarlarının farklı çerçevelere derlemelerin alt kümelerini uygulamak için başvurular özelliğini kullanmasına izin verir, aksi takdirde birden çok `lib` klasöründe yinelenen derlemeler taşıması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-163">This new feature will allow package authors to use the References feature to apply subsets of assemblies to different frameworks when they would otherwise need to carry duplicate assemblies in multiple `lib` folders.</span></span>

<span data-ttu-id="78e8e-164">Note: Bu özelliği kullanmak için şu anda NuGet. exe paketini kullanmanız gerekir; NuGet Paket Gezgini henüz desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-164">Note: you must presently use nuget.exe pack to use this feature; NuGet Package Explorer does not yet support it.</span></span>

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a><span data-ttu-id="78e8e-165">Tüm paketlerin tek seferde güncelleştirilmesini sağlamak için Tümünü Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="78e8e-165">Update All button to allow updating all packages at once</span></span>

<span data-ttu-id="78e8e-166">Tüm paketlerinizi güncelleştirmek için "Update-Package" PowerShell cmdlet 'i hakkında daha fazla bilgi sahibi olabilirsiniz. Şimdi de bunu Kullanıcı arabirimi aracılığıyla yapmanın kolay bir yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="78e8e-166">Many of you know about the "Update-Package" PowerShell cmdlet to update all of your packages; now there's an easy way to do this through the UI as well.</span></span>

<span data-ttu-id="78e8e-167">Bu özelliği denemek için:</span><span class="sxs-lookup"><span data-stu-id="78e8e-167">To try this feature out:</span></span>

1. <span data-ttu-id="78e8e-168">Yeni bir ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="78e8e-168">Create a new ASP.NET MVC application</span></span>
1. <span data-ttu-id="78e8e-169">' NuGet Paketlerini Yönet ' iletişim kutusunu başlatın</span><span class="sxs-lookup"><span data-stu-id="78e8e-169">Launch the 'Manage NuGet Packages' dialog</span></span>
1. <span data-ttu-id="78e8e-170">' Updates ' öğesini seçin</span><span class="sxs-lookup"><span data-stu-id="78e8e-170">Select 'Updates'</span></span>
1. <span data-ttu-id="78e8e-171">' Tümünü Güncelleştir ' düğmesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="78e8e-171">Click the 'Update All' button</span></span>

![İletişim kutusundaki Tümünü Güncelleştir düğmesi](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a><span data-ttu-id="78e8e-173">NuGet. exe paketi için geliştirilmiş proje başvurusu desteği</span><span class="sxs-lookup"><span data-stu-id="78e8e-173">Improved project reference support for nuget.exe Pack</span></span>

<span data-ttu-id="78e8e-174">Şimdi NuGet. exe paketi komutu başvurulan projeleri aşağıdaki kurallarla işler:</span><span class="sxs-lookup"><span data-stu-id="78e8e-174">Now nuget.exe pack command processes referenced projects with the following rules:</span></span>

1. <span data-ttu-id="78e8e-175">Başvurulan projenin karşılık gelen `.nuspec` dosyası varsa, örneğin, `proj1.csproj`ile aynı klasörde `proj1.nuspec` adlı bir dosya varsa, bu proje, `.nuspec` dosyasından okunan kimliği ve sürümü kullanarak pakete bir bağımlılık olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-175">If the referenced project has corresponding `.nuspec` file, e.g. there is a file called `proj1.nuspec` in the same folder as `proj1.csproj`, then this project is added as a dependency to the package, using the id and version read from the `.nuspec` file.</span></span>
1. <span data-ttu-id="78e8e-176">Aksi takdirde, başvurulan projenin dosyaları pakete paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-176">Otherwise, the files of the referenced project are bundled into the package.</span></span> <span data-ttu-id="78e8e-177">Ardından, bu proje tarafından başvurulan projeler yinelemeli olarak, sames kuralları kullanılarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-177">Then projects referenced by this project will be processed using the sames rules recursively.</span></span>
1. <span data-ttu-id="78e8e-178">Tüm DLL, `.pdb`ve `.exe` dosyaları eklenir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-178">All DLL, `.pdb`, and `.exe` files are added.</span></span>
1. <span data-ttu-id="78e8e-179">Diğer tüm içerik dosyaları eklenir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-179">All other content files are added.</span></span>
1. <span data-ttu-id="78e8e-180">Tüm bağımlılıklar birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-180">All dependencies are merged.</span></span>

<span data-ttu-id="78e8e-181">Bu, başvurulan bir projenin bir `.nuspec` dosyası varsa bağımlılık olarak işlenmesine izin verir, aksi takdirde paketin bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="78e8e-181">This allows a referenced project to be treated as a dependency if there is a `.nuspec` file, otherwise, it becomes part of the package.</span></span>

<span data-ttu-id="78e8e-182">Daha ayrıntılı bilgi: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span><span class="sxs-lookup"><span data-stu-id="78e8e-182">More details here: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)</span></span>

### <a name="add-a-minimum-nuget-version-property-to-packages"></a><span data-ttu-id="78e8e-183">Paketlere ' en az NuGet sürümü ' özelliği Ekle</span><span class="sxs-lookup"><span data-stu-id="78e8e-183">Add a 'Minimum NuGet Version' property to packages</span></span>

<span data-ttu-id="78e8e-184">' MinClientVersion ' adlı yeni bir meta veri özniteliği artık bir paketi kullanmak için gereken en düşük NuGet istemci sürümünü gösteriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-184">A new metadata attribute called 'minClientVersion' can now indicate the minimum NuGet client version required to consume a package.</span></span>

<span data-ttu-id="78e8e-185">Bu özellik paket yazarının, bir paketin yalnızca belirli bir NuGet sürümünden sonra çalıştığını belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="78e8e-185">This feature helps package author to specify that a package will work only after a particular version of NuGet.</span></span> <span data-ttu-id="78e8e-186">Yeni `.nuspec` Özellikler NuGet 2,5 sonrasında eklendikçe, paketler en düşük bir NuGet sürümü talep edebilecektir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-186">As new `.nuspec` features are added after NuGet 2.5, packages will be able to claim a minimum NuGet version.</span></span>

```xml
<metadata minClientVersion="2.6">
```

<span data-ttu-id="78e8e-187">Kullanıcının NuGet 2,5 ' i yüklüyse ve bir paket 2,6 gerektiren olarak tanımlanmışsa, paketin yüklenemeyeceğini belirten kullanıcıya görsel ipuçları verilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-187">If the user has NuGet 2.5 installed and a package is identified as requiring 2.6, visual cues will be given to the user indicating the package will not be installable.</span></span> <span data-ttu-id="78e8e-188">Daha sonra Kullanıcı NuGet sürümlerini güncelleştirmek üzere kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="78e8e-188">The user will then be guided to update their version of NuGet.</span></span>

<span data-ttu-id="78e8e-189">Bu, paketlerin yüklenmeye başlayacağı, ancak tanınmayan bir şema sürümünün tanımlandığını belirten başarısız olan deneyimde geliştirecek.</span><span class="sxs-lookup"><span data-stu-id="78e8e-189">This will improve upon the existing experience where packages begin to install but then fail indicating an unrecognized schema version was identified.</span></span>

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a><span data-ttu-id="78e8e-190">Bağımlılıklar artık paket yüklemesi sırasında gereksiz şekilde güncelleştirilmiyor</span><span class="sxs-lookup"><span data-stu-id="78e8e-190">Dependencies are no longer unnecessarily updated during package installation</span></span>

<span data-ttu-id="78e8e-191">NuGet 2,5 ' den önce, projede zaten yüklü olan bir pakete bağımlı olan bir paket yüklendiğinde, mevcut sürüm bağımlılığı karşılasa bile, bağımlılık yeni yüklemenin bir parçası olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-191">Before NuGet 2.5, when a package was installed that depended on a package already installed in the project, the dependency would be updated as part of the new installation, even if the existing version satisfied the dependency.</span></span>

<span data-ttu-id="78e8e-192">NuGet 2,5 ' den itibaren, bir bağımlılık sürümü zaten karşılandıysanız, diğer paket yüklemeleri sırasında bağımlılık güncellenmez.</span><span class="sxs-lookup"><span data-stu-id="78e8e-192">Starting with NuGet 2.5, if a dependency version is already satisfied, the dependency will not be updated during other package installations.</span></span>

<span data-ttu-id="78e8e-193">**Senaryo:**</span><span class="sxs-lookup"><span data-stu-id="78e8e-193">**The scenario:**</span></span>

1. <span data-ttu-id="78e8e-194">Kaynak Depo, 1.0.0 ve 1.0.2 sürümü ile B paketini içerir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-194">The source repository contains package B with version 1.0.0 and 1.0.2.</span></span> <span data-ttu-id="78e8e-195">Ayrıca B (> = 1.0.0) öğesine bağımlılığı olan paketi de içerir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-195">It also contains package A which has a dependency on B (>= 1.0.0).</span></span>
1. <span data-ttu-id="78e8e-196">Geçerli projede zaten Package B sürümü 1.0.0 yüklü olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="78e8e-196">Assume that the current project already has package B version 1.0.0 installed.</span></span> <span data-ttu-id="78e8e-197">Şimdi A paketini yüklemek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="78e8e-197">Now you want to install package A.</span></span>

<span data-ttu-id="78e8e-198">**NuGet 2,2 ve üzeri sürümlerde:**</span><span class="sxs-lookup"><span data-stu-id="78e8e-198">**In NuGet 2.2 and older:**</span></span>

* <span data-ttu-id="78e8e-199">A paketini yüklerken, 1.0.2 var olan sürüm 1.0.0 = 1.0.0 olan bağımlılık sürümü > kısıtlamasını zaten karşılayıp karşılamadığını, NuGet, B 'yi 'e otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-199">When installing package A, NuGet will auto-update B to 1.0.2, even though the existing version 1.0.0 already satisfies the dependency version constraint, which is >= 1.0.0.</span></span>

<span data-ttu-id="78e8e-200">**NuGet 2,5 ve üzeri sürümlerde:**</span><span class="sxs-lookup"><span data-stu-id="78e8e-200">**In NuGet 2.5 and newer:**</span></span>

* <span data-ttu-id="78e8e-201">Mevcut sürüm 1.0.0 'in bağımlılık sürümü kısıtlamasını karşılayıp karşılamadığını algıladığı için NuGet artık B 'yi güncelleştirmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-201">NuGet will no longer update B, because it detects that the existing version 1.0.0 satisfies the dependency version constraint.</span></span>

<span data-ttu-id="78e8e-202">Bu değişiklik hakkında daha fazla arka plan için, ayrıntılı [iş öğesini](http://nuget.codeplex.com/workitem/1681) ve ilgili [tartışma iş parçacığını](http://nuget.codeplex.com/discussions/436712)okuyun.</span><span class="sxs-lookup"><span data-stu-id="78e8e-202">For more background on this change, read the detailed [work item](http://nuget.codeplex.com/workitem/1681) as well as the related [discussion thread](http://nuget.codeplex.com/discussions/436712).</span></span>

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a><span data-ttu-id="78e8e-203">NuGet. exe http isteklerinin ayrıntılı ayrıntı düzeyine çıkışını verir</span><span class="sxs-lookup"><span data-stu-id="78e8e-203">nuget.exe outputs http requests with detailed verbosity</span></span>

<span data-ttu-id="78e8e-204">NuGet. exe sorunlarını gidermekte veya işlemler sırasında HTTP isteklerinin ne olduğunu merak ediyorsanız, '-ayrıntı ayrıntılı ' anahtar şimdi yapılan tüm HTTP isteklerinin çıktısını alacak.</span><span class="sxs-lookup"><span data-stu-id="78e8e-204">If you are troubleshooting nuget.exe or just curious what HTTP requests are made during operations, the '-verbosity detailed' switch will now output all HTTP requests made.</span></span>

![NuGet. exe ' den HTTP çıkışı](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a><span data-ttu-id="78e8e-206">NuGet. exe Push artık UNC ve klasör kaynaklarını destekliyor</span><span class="sxs-lookup"><span data-stu-id="78e8e-206">nuget.exe push now supports UNC and folder sources</span></span>

<span data-ttu-id="78e8e-207">NuGet 2,5 ' den önce, bir UNC yoluna veya yerel klasöre göre bir paket kaynağına ' NuGet. exe Push ' çalıştırmayı denediyseniz, gönderim başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="78e8e-207">Before NuGet 2.5, if you attempted to run 'nuget.exe push' to a package source based on a UNC path or local folder, the push would fail.</span></span> <span data-ttu-id="78e8e-208">Son eklenen hiyerarşik yapılandırma özelliği sayesinde, NuGet. exe ' nin bir UNC/klasör kaynağını veya HTTP tabanlı bir NuGet galerisini hedeflemesini gerektiren ortak hale geldi.</span><span class="sxs-lookup"><span data-stu-id="78e8e-208">With the recently added hierarchical configuration feature, it had become common for nuget.exe to need to target either a UNC/folder source, or an HTTP-based NuGet Gallery.</span></span>

<span data-ttu-id="78e8e-209">NuGet 2,5 ' den itibaren, NuGet. exe bir UNC/klasör kaynağını tanımlarsa, kaynağa dosya kopyalama işlemi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-209">Starting with NuGet 2.5, if nuget.exe identifies a UNC/folder source, it will perform the file copy to the source.</span></span>

<span data-ttu-id="78e8e-210">Aşağıdaki komut şimdi çalışacaktır:</span><span class="sxs-lookup"><span data-stu-id="78e8e-210">The following command will now work:</span></span>

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a><span data-ttu-id="78e8e-211">NuGet. exe, açıkça belirtilen yapılandırma dosyalarını destekler</span><span class="sxs-lookup"><span data-stu-id="78e8e-211">nuget.exe supports explicitly-specified Config files</span></span>

<span data-ttu-id="78e8e-212">yapılandırmaya erişim izni veren NuGet. exe komutları (tüm ' spec ' ve ' Pack ' hariç) artık,%AppData%\nuget\Nuget.Config. adresindeki varsayılan yapılandırma dosyası yerine belirli bir yapılandırma dosyasını zorlayan yeni bir '-ConfigFile ' seçeneğini destekliyor.</span><span class="sxs-lookup"><span data-stu-id="78e8e-212">nuget.exe commands that access configuration (all except 'spec' and 'pack') now support a new '-ConfigFile' option, which forces a specific config file to be used in place of the default config file at %AppData%\nuget\Nuget.Config.</span></span>

<span data-ttu-id="78e8e-213">Örnek:</span><span class="sxs-lookup"><span data-stu-id="78e8e-213">Example:</span></span>

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a><span data-ttu-id="78e8e-214">Yerel projeler için destek</span><span class="sxs-lookup"><span data-stu-id="78e8e-214">Support for Native projects</span></span>

<span data-ttu-id="78e8e-215">NuGet 2,5 ile NuGet araçları artık Visual Studio 'daki yerel projeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="78e8e-215">With NuGet 2.5, the NuGet tooling is now available for Native projects in Visual Studio.</span></span> <span data-ttu-id="78e8e-216">Birçok yerel paketin, [Coapp projesi](http://coapp.org)tarafından oluşturulan bir aracı kullanarak yukarıdaki MSBuild içeri aktarma özelliğinden yararlanacağız.</span><span class="sxs-lookup"><span data-stu-id="78e8e-216">We expect most native packages will utilize the MSBuild imports feature above, using a tool created by the [CoApp project](http://coapp.org).</span></span> <span data-ttu-id="78e8e-217">Daha fazla bilgi için coapp.org Web sitesindeki [araçla ilgili ayrıntıları](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) okuyun.</span><span class="sxs-lookup"><span data-stu-id="78e8e-217">For more information, read [the details about the tool](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) on the coapp.org website.</span></span>

<span data-ttu-id="78e8e-218">"Yerel" hedef çerçeve adı, paketler yerel bir projeye yüklendiğinde \Build, \content ve \Tools dosyalarına dosya eklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="78e8e-218">The target framework name of "native" is introduced for packages to include files in \build, \content, and \tools when the package is installed into a native project.</span></span>  <span data-ttu-id="78e8e-219">\`lib ' klasörü yerel projeler için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="78e8e-219">The \`lib\` folder is not used for native projects.</span></span>
