---
title: "NuGet 2.5 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c193f1e3-d114-427f-9425-9930cc8e4db3
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.5 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.5 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8d3bebbbe550645fcffad078538134427103cf98
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-25-release-notes"></a>NuGet 2,5 sürüm notları

[NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md) | [NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md)

NuGet 2.5 25 Nisan 2013'te yayımlanmıştır. Bu sürüm kadar büyük, biz 2.3 ve 2.4 sürümleri atlamak compelled Keçeli! Biz vardı NuGet için ile büyük yayın budur bugüne kadar üzerinden [160 iş öğelerini](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) sürümde.

## <a name="acknowledgements"></a>Katkıda Bulunanlar

Aşağıdaki dış Katkıda Bulunanlar, önemli ölçüde katkıda NuGet 2.5 için teşekkür ederiz ister misiniz:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -MonoAndroid eklemek, MonoTouch ve bilinen hedef framework tanımlayıcıları listesine MonoMac.
1. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -yazımını düzeltme `NuGet.targets` büyük küçük harfe duyarlı bir işletim sistemi için
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Mono üzerinde yapı çözümü haline getirmiştir.
1. [Barış Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Mono üzerinde başarısız olan birim testleri düzeltin.
1. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe paketi komutu MSBuild özelliklerine yayılması değil
1. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - biçimlendirmesini korumak için işleme kodunu XML değiştirdi.
1. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Tanınan sözcükler başarılı olması build.cmd izin vermek için özel sözlüğe eklendi.
1. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Birim testleri yerelleştirilmiş VS üzerinde çalışırken düzeltin.
1. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService ayıklanan arabirimi
1. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
    - [#936](https://nuget.codeplex.com/workitem/936) -sevk proje bağımlılıkları işleme
1. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
    - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -destek metin paket kaynağı kimlik bilgileri nuget.cofig dosyalarında depolarken Parolayı Temizle
1. [Ahmet Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
    - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -Get-paket düzeltme Yardım açıklaması

Ayrıca şu kişilere hataları ile NuGet 2.5 Beta/onaylanmış ve son yayımlanmasından önce sabit RC bulmak için değer veriyoruz:

1. [Tony duvar](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) - 2.5 yapılar ve en son NuGet 2.4 ile ayrılmış mstest'i

# <a name="notable-features-in-the-release"></a>Sürümdeki dikkat çekici özellikleri

## <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Kullanıcıların zaten içerik dosyalarının üzerine izin ver

Her zaman en çok istenen özelliklerden biri, bir NuGet paketi eklendiğinde diskte zaten içerik dosyalarının üzerine özelliği kaldırıldı. NuGet 2.5 ile başlayarak, bu çakışmaları tanımlanır ve daha önce bu dosyaları her zaman Atlanan ise, dosyaların üzerine istenir.

![İçerik dosyalarının üzerine yaz](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' ve 'Install-hem de yeni bir seçeneğiniz artık Package' '-FileConflictAction' komut satırı senaryoları için bazı varsayılan ayarlamak için.

Bir dosyadan bir paketi hedef projede zaten mevcut olduğunda bir varsayılan eylem ayarlayın. Her zaman dosyaları üzerine yazmak için 'İçin üzerine yaz' ayarlayın. Dosyalarını atlamak için 'Yoksay' olarak ayarlayın. Belirtilmezse, çakışan her dosya için sorar.

## <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild hedefleri ve özellik dosyalarının otomatik alma

Yeni bir geleneksel klasör NuGet paketi en üst düzeyde oluşturuldu.  Bir eşler arası olarak `\lib`, `\content`, ve `\tools`, şimdi dahil edebileceğiniz bir `\build` paketinizi klasöründe.  Bu klasörü altında sabit adlarıyla iki dosya yerleştirebilirsiniz `{packageid}.targets` veya `{packageid}.props`. Bu iki dosya ya da doğrudan altında olabilir `build` veya diğer klasörler gibi çerçeveye özel klasörler altında. En iyi eşleşen çerçeve klasörünün çekme için tam olarak ile aynı olan kuralıdır.

NuGet \build dosyalarıyla bir paketi yüklendiğinde, bir MSBuild ekleyecek `<Import>` öğesi işaret proje dosyasında `.targets` ve `.props` dosyaları. `.props` Dosya, en üstte eklenir, ancak `.targets` dosya altına eklenir.

## <a name="specify-different-references-per-platform-using-references-element"></a>Platform kullanarak başına farklı başvurular belirtin `<References/>` öğesi

2.5 önce içinde `.nuspec` dosyası, kullanıcı yalnızca belirtebilir tüm çerçevesi için eklenecek başvuru dosyalar. 2.5 yeni bu özellik ile kullanıcı yazabilirsiniz artık `<reference/>` öğesini her desteklenen platform için örneğin:

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

Nasıl NuGet göre projelere başvurular ekler için akış işte `.nuspec` dosyası:

1. Bul `lib` hedef çerçeve için uygun olan ve bu klasörden derleme listesini al klasör
1. Ayrı olarak hedef çerçeve için uygun olan başvurular grubunu bulun ve o gruptan derleme listesini alın. Belirtilen hedef çerçevede olmadan başvuru grubu geri dönüş grubudur.
1. İki listelerinin kesişimini bulur ve eklemek için referans olarak kullanın

Bu yeni özellik, aksi takdirde birden çok yinelenen derlemeleri taşımak gerekir, derlemeler kümelerine farklı çerçeveleri uygulamak için başvurular bu özelliği kullanmak paketi yazarları sağlayacak `lib` klasörler.

Not: Bu özelliği kullanmak için nuget.exe paketi şu anda kullanmalısınız; Bu NuGet paketi Gezgini henüz desteklemiyor.

## <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Tüm paketler aynı anda güncelleştirme sağlamak için tüm düğmesini güncelleştir

Birçoğu tüm paketlerinizi güncelleştirmek için "Güncelleştirme paketi" PowerShell cmdlet hakkında bilmeniz; Şimdi UI aracılığıyla bunu yapmanın kolay bir yolu yoktur.

Bu özelliği denemek için:

1. Yeni bir ASP.NET MVC uygulaması oluşturma
1. 'NuGet paketlerini Yönet' iletişim kutusu başlatma
1. 'Güncelleştirmeleri' seçin
1. 'Tümünü Güncelleştir' düğmesini tıklatın

![İletişim kutusu tüm düğmesini güncelleştir](./media/NuGet-2.5/update-all.png)

## <a name="improved-project-reference-support-for-nugetexe-pack"></a>Geliştirilmiş proje başvurusu nuget.exe paketi desteği

Şimdi nuget.exe paketi komutu işlemleri aşağıdaki kuralları projelerle başvurulan:

1. Başvuruda bulunulan proje karşılık gelen varsa `.nuspec` dosya, örneğin adlı bir dosya yoktur `proj1.nuspec` aynı klasörde `proj1.csproj`, daha sonra bu proje kimliğini kullanarak paket için bağımlılık olarak eklenir ve sürüm okuma `.nuspec` dosya.
1. Aksi takdirde, başvurulan proje dosyalarını pakete paketlenmiştir. Ardından bu proje tarafından başvurulan projeleri sames kuralları yinelemeli kullanılarak işlenir.
1. Tüm DLL `.pdb`, ve `.exe` dosyaları eklenir.
1. Tüm içerik dosyalarının eklenir.
1. Tüm bağımlılıkları birleştirilir.

Varsa bir bağımlılık olarak kabul edilmesi başvuruda bulunulan bir proje böylece bir `.nuspec` dosya, aksi takdirde, paketin bir parçası haline gelir.

Daha fazla ayrıntıları buraya: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

## <a name="add-a-minimum-nuget-version-property-to-packages"></a>'En az NuGet sürümü' özelliği paketlere Ekle

'MinClientVersion' adlı yeni bir meta veri öznitelik şimdi bir paketi kullanmak için gereken en düşük NuGet istemci sürümünün olduğunu gösteriyor olabilir.

Bu özellik, bir paket yalnızca NuGet belirli bir sürümünden sonra çalışacağını belirtmek için paket yazarına yardımcı olur. Yeni `.nuspec` özellikleri, NuGet 2.5 sonra paketleri kurulamayacak en az bir NuGet sürümü talep eklenir.

```xml
<metadata minClientVersion="2.6">
```

NuGet yüklü 2.5 kullanıcı varsa ve bir paket 2.6 gerektiren olarak tanımlanır, görsel ipuçları paket yüklenebilir olmaz belirten kullanıcıya verilir. Kullanıcı, kendi NuGet sürümünü güncelleştirmek için sonra yönlendirilecektir.

Bu, burada paketleri yüklemek, ancak tanınmayan şema sürümü tanımlanan belirten başarısız başlamadan varolan deneyimi artırır.

## <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Bağımlılıklar artık gereksiz yere paket yükleme sırasında güncelleştirilir

Projede yüklü bir paket bağımlı bir paket yüklendiğinde mevcut sürümü bağımlılık memnun olsa bile NuGet 2.5 önce bağımlılık Yeni yüklemenin bir parçası güncelleştirilmesi.

Bağımlılık sürümünü zaten sağlanıyorsa NuGet 2.5 ile başlayarak, bağımlılık diğer paket yüklemeleri sırasında güncelleştirilmez.

**Senaryo:**

1. Kaynak deposu Paket B 1.0.0 ve 1.0.2 sürümüyle içerir. Ayrıca b'de bir bağımlılığa sahip bir paket içerir (> = 1.0.0).
1. Geçerli projenin Paket B sürümü 1.0.0 yüklü olduğunu varsayalım. Paket A. yüklemek istediğiniz şimdi

**2.2 ve eski NuGet içinde:**

* Paket bir yükleme sırasında NuGet otomatik B 1.0.2 için var olan sürümü 1.0.0 zaten olan bağımlılık sürümü kısıtlamasına uyan olsa bile güncelleştirilecektir > 1.0.0 =.

**2.5 ve daha yeni NuGet içinde:**

* Var olan sürümü 1.0.0 bağımlılık sürümü kısıtlamasına uyan algıladığından NuGet artık B güncelleştirin.

Bu değişiklik hakkında daha fazla arka plan için ayrıntılı okuma [iş öğesi](http://nuget.codeplex.com/workitem/1681) yanı sıra ilgili [tartışma iş parçacığı](http://nuget.codeplex.com/discussions/436712).

## <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe http isteklerini ile ayrıntılı ayrıntı çıkarır.

Nuget.exe sorun giderme ya da yalnızca merak hangi HTTP isteklerinin yapılma işlemler sırasında '-ayrıntılı ayrıntı ' anahtar şimdi yapılan tüm HTTP istekleri çıktı.

![HTTP nuget.exe çıktısı](./media/NuGet-2.5/verbosity.png)

## <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe itme şimdi UNC ve klasör kaynakları destekler

Bir UNC yolu veya yerel klasör, temel alan bir paket kaynağı için 'nuget.exe push' çalıştırmayı deneyen, NuGet 2.5 önce gönderme başarısız olur. Son eklenen hiyerarşik yapılandırma özelliğiyle, UNC/klasör kaynak ya da bir HTTP tabanlı NuGet galerisinde hedeflemek gerek nuget.exe için yaygın hale.

Nuget.exe bir UNC/klasör kaynağı tanımlarsa NuGet 2.5 ile başlayarak, kaynak dosya kopyalama işlemini gerçekleştirecek.

Aşağıdaki komut artık çalışır:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

## <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe açıkça belirtilen yapılandırma dosyalarını destekler

Yapılandırma (Tümü 'Özellikler' ve 'paketi' dışında) şimdi erişim nuget.exe komutları desteği yeni bir '-ConfigFile' % AppData%\nuget\Nuget.Config varsayılan yapılandırma dosyası yerine kullanılacak özel yapılandırma dosyası zorlar seçeneği.

Örnek:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

## <a name="support-for-native-projects"></a>Yerel projeleri için desteği

NuGet 2.5 ile NuGet araç artık Visual Studio'da yerel projeleri için kullanılabilir. En yerel paketleri yukarıdaki MSBuild içeri aktarmalar özelliğini kullanan tarafından oluşturulan bir aracı kullanarak bekliyoruz [CoApp proje](http://coapp.org). Daha fazla bilgi için okuma [aracı hakkındaki ayrıntıları](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) coapp.org Web sitesinde.

"Yerel" hedef framework adını, paket yerel bir projeye yüklendiğinde \build, \content ve \tools dosyaları dahil edilecek paketler için sunulmuştur.  \`Lib' klasörüne yerel projeleri için kullanılmaz.
