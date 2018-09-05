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
# <a name="nuget-25-release-notes"></a>NuGet 2.5 sürüm notları

[2.2.1 NuGet sürüm notları](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md)

NuGet 2.5 25 Nisan 2013 tarihinde yayınlanmıştır. Bu sürüm, bu nedenle büyük, biz sürüm 2.3 ve 2.4 atlamak compelled düşünmüştür! Bugüne kadar bu vardı için NuGet, ile büyük sürümdür üzerinden [160 iş öğelerini](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) sürümde.

## <a name="acknowledgements"></a>Onayları

Aşağıdaki harici Katkıda Bulunanlar, NuGet 2.5 önemli katkılar için teşekkür ederiz istiyoruz:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid ekleyin ve MonoTouch MonoMac bilinen hedef framework tanımlayıcılarının listesi.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -yazımını düzeltin `NuGet.targets` büyük küçük harfe duyarlı bir işletim sistemi için
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Mono üzerinde derleme çözümü haline getirmiştir.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Mono üzerinde başarısız olan birim testlerini düzeltin.
5. [Yazan Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe paketi komut MSBuild özellikleri yaymak değil
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - biçimlendirmesini korumak için işleme kodunu XML değiştirdi.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Tanınan sözcükleri build.cmd başarılı olması izin vermek için özel sözlük eklendi.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Birim testleri, yerelleştirilmiş VS'de çalıştırırken düzeltin.
9. [Jones'un Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Ayıklanan PackageService arabirimi
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -sevk işlemek proje bağımlılıkları
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -destek metin paket kaynağı kimlik bilgileri nuget.cofig dosyalarında depolarken Parolayı Temizle
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-Package düzeltin Yardım açıklaması

Ayrıca aşağıdaki kişiler ile NuGet 2.5 Beta/Onaylandı ve önce son sürümde düzeltilecek RC hataları bulmak için veriyoruz:

1. [Tony duvar](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - MSTest 2,5 derlemeler ve en son NuGet 2.4 ile ayrılmış

## <a name="notable-features-in-the-release"></a>Sürümündeki önemli özelliklere

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Kullanıcıların içerik zaten mevcut dosyaların üzerine yaz

Her zaman, en çok istenen özelliklerden biri, bir NuGet paketi eklendiğinde diskte zaten mevcut içerik dosyalarının üzerine yazılmasını olmuştur. NuGet 2.5 ile başlayarak, bu çakışmaları tanımlanır ve bu dosyaları her zaman önceden atlandı ise dosyaların üzerine yazıp istenir.

![İçerik dosyaların üzerine yaz](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe Güncelleştirme' ve 'Yükle-hem de yeni bir seçenek artık paket' '-FileConflictAction' komut satırı senaryoları için bazı varsayılan ayarlamak için.

Bir paket dosyasından hedef projede zaten mevcut olduğunda, varsayılan eylem ayarlayın. Her zaman dosyaların üzerine yaz 'İçin üstüne yaz' ayarlayın. Dosyalarını atlamak için 'Yoksay' olarak ayarlayın. Belirtilmezse, çakışan her dosya için ister.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild hedeflerini ve özellik dosyalarının otomatik içeri aktarma

NuGet paketini en üst düzeyinde yeni bir geleneksel klasörü oluşturuldu.  Eşler arası olarak `\lib`, `\content`, ve `\tools`, artık dahil edebilirsiniz bir `\build` paketinizdeki klasör.  Bu klasör altında sabit adlara sahip iki dosya yerleştirebilirsiniz `{packageid}.targets` veya `{packageid}.props`. Bu iki dosyayı doğrudan altında olabilir `build` veya diğer klasörler gibi çerçeveye özgü klasörlere. En iyi eşleşen çerçeve klasörü çekme için tam olarak aynı olduğu gibi bu kuralıdır.

NuGet paketi \build dosyalarıyla yüklendiğinde bir MSBuild ekleyeceksiniz `<Import>` öğesini işaret eden proje dosyasında `.targets` ve `.props` dosyaları. `.props` Dosya, en üstüne eklenir, ancak `.targets` dosyasının alt kısmına eklenir.

### <a name="specify-different-references-per-platform-using-references-element"></a>Her bir platform kullanarak farklı başvuruları belirtin `<References/>` öğesi

2.5 önce içinde `.nuspec` dosyası, kullanıcı yalnızca belirtebilirsiniz tüm framework eklenmesi için başvuru dosyaları. 2.5 içinde bu yeni özellik ile kullanıcı yazabilirsiniz artık `<reference/>` öğesini her desteklenen platform, örneğin:

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

Akışın nasıl NuGet göre projelerine başvurular ekler için işte `.nuspec` dosyası:

1. Bulma `lib` hedef çerçeve için uygun olan ve bu klasörden derlemelerin listesini alma klasörü
1. Ayrı olarak hedef çerçeve için uygun olan başvuruları grubunu bulun ve o gruptan derlemelerin listesini alın. Belirtilen hedef Framework'ü olmadan başvuru grubu geri dönüş grubudur.
1. İki listelerinin kesişimini bulun ve eklemek için başvuru olarak kullanın

Bu yeni özellik, aksi takdirde birden çok yinelenen derlemeleri gerçekleştirmek gerekir, farklı çerçeveler için derlemeleri kümelerine uygulamak için başvurular bu özelliği kullanmak paket yazarlarının sağlayacak `lib` klasörleri.

Not: Bu özelliği kullanmak için nuget.exe paketi şu anda kullanmalısınız; NuGet paket Gezgini henüz desteklemiyor.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Tüm paketleri aynı anda güncelleştirilmesini sağlayacak şekilde tüm düğme güncelleştir

Birçoğunuzun tüm paketleriniz güncelleştirmek için "Update-Package" PowerShell cmdlet'i hakkında bilmeniz; Şimdi de kullanıcı Arabirimi aracılığıyla bunu yapmanın kolay bir yolu yoktur.

Bu özelliği denemek için:

1. Yeni bir ASP.NET MVC uygulaması oluşturma
1. 'NuGet paketlerini Yönet' iletişim kutusunu başlatma
1. 'Güncelleştirmeleri' seçin
1. 'Tümünü Güncelleştir' düğmesini tıklatın

![İletişim kutusundaki tüm düğme güncelleştir](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Nuget.exe paketi için geliştirilmiş proje başvurusu desteği

Artık nuget.exe paketi komut işlemleri, aşağıdaki kurallar ile projeye başvuruyor:

1. Başvurulan projenin karşılık gelen varsa `.nuspec` dosya, örneğin adlı bir dosya var. `proj1.nuspec` aynı klasörde `proj1.csproj`, ardından bu proje paketi kimliğini kullanarak, bir bağımlılık olarak eklenir ve sürüm okuma `.nuspec` dosya.
1. Aksi takdirde, dosyaları başvurulan projenin pakete paketlenir. Ardından bu proje tarafından başvurulan projeler sames kuralları yinelemeli olarak kullanılarak işlenir.
1. Tüm DLL `.pdb`, ve `.exe` dosyalar eklenir.
1. Tüm içerik dosyalarını eklenir.
1. Tüm bağımlılıkları birleştirilir.

Başvurulan bir proje varsa, bağımlılık olarak değerlendirilmesini sağlar ve böylece bir `.nuspec` dosya, aksi takdirde, paketinin bir parçası haline gelir.

Buradan daha fazla ayrıntı: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>'En düşük NuGet sürümü' özelliği paketlere Ekle

'MinClientVersion' adlı yeni bir meta veri öznitelik, bir paketi kullanmak için gereken en düşük NuGet istemci sürümü artık belirtebilirsiniz.

Bu özellik, bir paket nuget yalnızca belirli bir sürümü sonra çalışacağını belirtmek için paket yazarı yardımcı olur. Yeni `.nuspec` özellikleri eklendi NuGet 2.5 sonra paketleri en az bir NuGet sürümü talep mümkün olacaktır.

```xml
<metadata minClientVersion="2.6">
```

NuGet yüklü 2.5 kullanıcı varsa ve bir paket 2.6 gerektiren olarak tanımlandığında, görsel ipuçları paket yüklenebilir olması değil belirten kullanıcıya verilir. Kullanıcı, ardından kendi NuGet sürümünü güncelleştirmek için yönlendirilecektir.

Bu, burada paketleri yükleyin ancak tanınmayan şema sürümü tanımlanan belirten ardından başarısız başlamadan mevcut deneyimi elde edilmesini sağlar.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Bağımlılıkları paket yükleme sırasında artık gereksiz bir şekilde güncelleştirilir

Projede zaten yüklü bir paket bağımlı bir paket yüklendiğinde bile var olan sürüm bağımlılığı karşıladı NuGet 2.5 önce bağımlılık yeni yüklemesinin bir parçası güncelleştirilecek.

Bir bağımlılık sürümü zaten getirildiyse NuGet 2.5 ile başlayarak, bağımlılık diğer paket yüklemeleri sırasında güncelleştirilmez.

**Senaryo:**

1. Kaynak deposu, sürüm 1.0.0 ve 1.0.2 ile paket B içerir. Ayrıca, B'bir bağımlılığa sahip bir paketi içerir (> = 1.0.0).
1. Geçerli proje Paket B sürüm 1.0.0 yüklü olduğunu varsayar. Şimdi paket A. yüklemek istediğiniz

**2.2 ve eski NuGet içinde:**

* Paket bir yükleme sırasında NuGet otomatik B 1.0.2 için var olan sürüm 1.0.0 zaten olan bağımlılık sürüm kısıtlamasını karşılayan olsa da güncelleştirilecektir > 1.0.0 =.

**2,5 ve daha yeni NuGet içinde:**

* Var olan sürüm 1.0.0 bağımlılık sürüm kısıtlamasını karşılayan algıladığından NuGet artık B güncelleştirin.

Bu değişiklikle ilgili daha fazla arka plan için ayrıntılı okuma [iş öğesi](http://nuget.codeplex.com/workitem/1681) yanı sıra ilgili [tartışma](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe http istekleri ile ayrıntılı ayrıntı çıkarır.

Nuget.exe giderirken veya yalnızca merak hangi HTTP isteklerinin yapılan işlemler sırasında '-ayrıntılı ayrıntı ' anahtar artık tüm HTTP isteklerini çıktı.

![Nuget.exe HTTP çıktısı](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe anında iletme UNC ve klasör kaynakları artık destekler.

NuGet 2.5 önce bir UNC yolu veya yerel klasör, temel bir paket kaynağı için 'nuget.exe push' çalıştırmayı denedi, anında iletme başarısız olur. Son eklenen hiyerarşik yapılandırma özelliğiyle UNC veya klasörün kaynak ya da bir HTTP tabanlı NuGet galerisinde hedeflemeniz gerektiği nuget.exe için ortak pazarlanmasının.

Nuget.exe UNC veya klasörün kaynak tanımlıyorsa NuGet 2.5 ile başlayarak, kaynak dosya kopyalama gerçekleştirir.

Aşağıdaki komutu artık çalışır:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe açıkça belirtilen yapılandırma dosyalarını destekler.

artık yapılandırma (Tümü 'Özellikler' ve 'paketi' hariç) erişen nuget.exe komut yeni bir destek '-ConfigFile' seçeneği, varsayılan yapılandırma dosyası % AppData%\nuget\Nuget.Config yerine kullanılacak özel bir yapılandırma dosyasını zorlar.

Örnek:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Yerel projeleri için destek

NuGet 2.5 ile NuGet araçları artık Visual Studio'da yerel projeleri için kullanılabilir. En yerel paketler, yukarıdaki MSBuild Imports özelliğini yararlanacaktır tarafından oluşturulan bir araç kullanarak bekliyoruz [CoApp proje](http://coapp.org). Daha fazla bilgi için okuma [aracı hakkındaki ayrıntıları](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org Web sitesinde.

Hedef Çerçeve adı "yerel" paketi bir yerel projeye yüklendiğinde \build, \content ve \tools dosyaları eklenip eklenmeyeceğini paketler için kullanıma sunulmuştur.  \`Lib' klasörü yerel projeleri için kullanılmaz.
