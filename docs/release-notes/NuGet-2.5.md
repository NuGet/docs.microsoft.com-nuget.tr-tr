---
title: NuGet 2,5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,5 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237095"
---
# <a name="nuget-25-release-notes"></a>NuGet 2,5 sürüm notları

[NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md)  |  [NuGet 2,6 sürüm notları](../release-notes/nuget-2.6.md)

NuGet 2,5, 25 Nisan 2013 ' de yayımlanmıştır. Bu sürüm çok büyük, 2,3 ve 2,4 sürümlerini atlamak için etmek zorunda kalırsak! Bu, yayında 160 ' den fazla [iş öğesi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) ile NuGet için sahip olduğumuz en büyük sürümdür.

## <a name="acknowledgements"></a>Teşekkürler

NuGet 2,5 ' e yönelik önemli katkılarına yönelik olarak aşağıdaki dış katkıda bulunanlar için teşekkür ederiz:

1. [DANIEL Plaıted](https://www.codeplex.com/site/users/view/dsplaisted) ( [@dsplaisted](https://twitter.com/dsplaisted) )
    - [#2847](https://nuget.codeplex.com/workitem/2847) , bilinen hedef çerçeve tanımlayıcıları listesine monoandroid, MonoTouch ve monomac 'i ekleyin.
2. [Andres G. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ( [@knocte](https://twitter.com/knocte) )
    - [#2865](https://nuget.codeplex.com/workitem/2865) - `NuGet.targets` büyük/küçük harfe duyarlı bir işletim sistemi için yazımı çözme
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - Çözümü mono üzerinde oluşturun.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ( [@atheken](https://twitter.com/atheken) )
    - Mono üzerinde başarısız olan birim testlerini düzeltir.
5. [Kayvier Dadgena,](https://www.codeplex.com/site/users/view/OliIsCool) ( [@OliIsCool](https://twitter.com/oliiscool) )
    - [#2920](https://nuget.codeplex.com/workitem/2920) -nuget.exe Pack komutu özellikleri MSBuild 'e yayılmaz
6. [MIROSLAV Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#1511](https://nuget.codeplex.com/workitem/1511) -biçimlendirmeyi korumak için XML işleme kodu değiştirildi.
7. [Adam Canph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - Build. cmd ' nin başarılı olmasını sağlamak için özel sözlüğe tanınan sözcükler eklendi.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Yerelleştirilmiş Ile çalışırken birim testlerini düzeltir.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - PackageService 'ten arabirim ayıklandı
10. [MAXIME deneme Gidou](https://www.codeplex.com/site/users/view/brugidou) ( [@brugidou](https://twitter.com/brugidou) )
     - Paketleme sırasında Proje bağımlılıklarını [#936](https://nuget.codeplex.com/workitem/936) işle
11. [Xavier Ayrışıcı](https://www.codeplex.com/site/users/view/XavierDecoster) ( [@XavierDecoster](https://twitter.com/xavierdecoster) )
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -paket kaynağı kimlik bilgilerini NuGet. cofıg dosyalarında depolarken şifresiz metin parolasını destekler
12. [James Manş](http://www.codeplex.com/site/users/view/jmanning) ( [@manningj](https://twitter.com/manningj) )
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -düzeltir Get-Package yardım açıklaması

Son sürümden önce onaylanan ve düzeltilen NuGet 2,5 Beta/RC ile hataları bulmak için aşağıdaki bireyler de bizim için de teşekkür ederiz:

1. [(](https://www.codeplex.com/site/users/view/CodeChief) [@CodeChief](https://twitter.com/codechief) )
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest, son NuGet 2,4 ve 2,5 Derlemeleriyle kesildi

## <a name="notable-features-in-the-release"></a>Yayındaki önemli özellikler

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Kullanıcıların zaten var olan içerik dosyalarının üzerine yazmasına izin ver

Her zaman en çok istenen özelliklerden biri, bir NuGet paketine dahil edildiğinde diskte zaten bulunan içerik dosyalarının üzerine yazılmasına olanak sağlar. NuGet 2,5 ' den itibaren bu çakışmalar tanımlanır ve dosyaların üzerine yazmanız istenir, ancak daha önce bu dosyalar her zaman atlanır.

![İçerik dosyalarının üzerine yaz](./media/NuGet-2.5/overwrite-file.png)

' nuget.exe Update ' ve ' Install-Package ' artık, komut satırı senaryoları için bazı varsayılan değer ayarlamak üzere '-FileConflictAction ' adlı yeni bir seçeneğe sahip.

Hedef projede bir paketten bir dosya zaten mevcut olduğunda varsayılan bir eylem ayarlayın. Dosyaların üzerine her zaman yazılacak ' üzerine yaz ' olarak ayarlayın. Dosyaları atlamak için ' Yoksay ' olarak ayarlayın. Belirtilmemişse, her çakışan dosya istenir.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>MSBuild hedeflerini ve props dosyalarını otomatik içe aktarma

NuGet paketinin en üst düzeyinde yeni bir geleneksel klasör oluşturulmuştur.  , Ve için bir eşdüzey olarak, `\lib` `\content` `\tools` artık `\build` paketinize bir klasör ekleyebilirsiniz.  Bu klasör altında, sabit adlarla iki dosya yerleştirebilirsiniz `{packageid}.targets` `{packageid}.props` . Bu iki dosya doğrudan `build` diğer klasörler gibi çerçeveye özgü klasörler altında ya da altında olabilir. En iyi eşleşen çerçeve klasörünü çekmeye yönelik kural, bunlar ile tamamen aynıdır.

NuGet, \Build dosyalarını içeren bir paket yüklediğinde, `<Import>` ve dosyalarını gösteren proje dosyasına bir MSBuild öğesi ekler `.targets` `.props` . Dosya `.props` en üste eklenir, ancak `.targets` Dosya en alta eklenir.

### <a name="specify-different-references-per-platform-using-references-element"></a>Öğe kullanarak platform başına farklı başvurular belirtin `<References/>`

2,5 öncesinde, `.nuspec` Kullanıcı, tüm Framework için eklenmek üzere yalnızca başvuru dosyalarını belirtebilir. Artık 2,5 sürümündeki bu yeni özellik sayesinde, Kullanıcı `<reference/>` desteklenen her platformun her biri için öğesini yazabilir, örneğin:

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

NuGet 'in dosyaya göre projelere nasıl başvurular eklediği Flow aşağıda verilmiştir `.nuspec` :

1. `lib`Hedef Framework için uygun olan klasörü bulun ve bu klasörden derlemelerin listesini alın
1. Hedef çerçeve için uygun olan başvurular grubunu ayrı olarak bulun ve bu gruptaki derlemelerin listesini alın. Hedef çerçevesi olmayan başvuru grubu, geri dönüş grubudur.
1. İki listenin kesişimini bulun ve bunları eklemek için başvurular olarak kullanın

Bu yeni özellik, paket yazarlarının farklı çerçevelere derlemelerin alt kümelerini uygulamak için başvurular özelliğini kullanmasına izin verir, aksi takdirde birden çok klasörde yinelenen derlemeler taşıması gerekir `lib` .

Note: Bu özelliği kullanmak için şu anda nuget.exe paketini kullanmanız gerekir; NuGet Paket Gezgini henüz desteklememektedir.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Tüm paketlerin tek seferde güncelleştirilmesini sağlamak için Tümünü Güncelleştir

Tüm paketlerinizi güncelleştirmek için "Update-Package" PowerShell cmdlet 'i hakkında daha fazla bilgi sahibi olabilirsiniz. Şimdi de bunu Kullanıcı arabirimi aracılığıyla yapmanın kolay bir yolu vardır.

Bu özelliği denemek için:

1. Yeni bir ASP.NET MVC uygulaması oluşturma
1. ' NuGet Paketlerini Yönet ' iletişim kutusunu başlatın
1. ' Updates ' öğesini seçin
1. ' Tümünü Güncelleştir ' düğmesine tıklayın

![İletişim kutusundaki Tümünü Güncelleştir düğmesi](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>nuget.exe Pack için geliştirilmiş proje başvurusu desteği

Şimdi, şu kurallara sahip başvurulan projeleri nuget.exe Pack komutu işlemlerine sahiptir:

1. Başvurulan projenin karşılık gelen `.nuspec` bir dosyası varsa, örneğin aynı klasörde adlı bir dosya varsa `proj1.nuspec` `proj1.csproj` , bu proje, dosyadan okunan kimliği ve sürümü kullanarak pakete bir bağımlılık olarak eklenir `.nuspec` .
1. Aksi takdirde, başvurulan projenin dosyaları pakete paketlenmiştir. Ardından, bu proje tarafından başvurulan projeler yinelemeli olarak, sames kuralları kullanılarak işlenir.
1. Tüm DLL, `.pdb` ve `.exe` dosyaları eklenir.
1. Diğer tüm içerik dosyaları eklenir.
1. Tüm bağımlılıklar birleştirilir.

Bu, başvurulan bir projenin bir dosya varsa bağımlılık olarak işlenmesine izin verir `.nuspec` , aksi takdirde paketin bir parçası olur.

Daha ayrıntılı bilgi: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Paketlere ' en az NuGet sürümü ' özelliği Ekle

' MinClientVersion ' adlı yeni bir meta veri özniteliği artık bir paketi kullanmak için gereken en düşük NuGet istemci sürümünü gösteriyor olabilir.

Bu özellik paket yazarının, bir paketin yalnızca belirli bir NuGet sürümünden sonra çalıştığını belirtmesini sağlar. `.nuspec`Nuget 2,5 sonrasında yeni özellikler eklendikçe, paketler en düşük bir NuGet sürümü talep edebilecektir.

```xml
<metadata minClientVersion="2.6">
```

Kullanıcının NuGet 2,5 ' i yüklüyse ve bir paket 2,6 gerektiren olarak tanımlanmışsa, paketin yüklenemeyeceğini belirten kullanıcıya görsel ipuçları verilir. Daha sonra Kullanıcı NuGet sürümlerini güncelleştirmek üzere kullanılacaktır.

Bu, paketlerin yüklenmeye başlayacağı, ancak tanınmayan bir şema sürümünün tanımlandığını belirten başarısız olan deneyimde geliştirecek.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Bağımlılıklar artık paket yüklemesi sırasında gereksiz şekilde güncelleştirilmiyor

NuGet 2,5 ' den önce, projede zaten yüklü olan bir pakete bağımlı olan bir paket yüklendiğinde, mevcut sürüm bağımlılığı karşılasa bile, bağımlılık yeni yüklemenin bir parçası olarak güncelleştirilir.

NuGet 2,5 ' den itibaren, bir bağımlılık sürümü zaten karşılandıysanız, diğer paket yüklemeleri sırasında bağımlılık güncellenmez.

**Senaryo:**

1. Kaynak Depo, 1.0.0 ve 1.0.2 sürümü ile B paketini içerir. Ayrıca B (>= 1.0.0) öğesine bağımlılığı olan paketi de içerir.
1. Geçerli projede zaten Package B sürümü 1.0.0 yüklü olduğunu varsayalım. Şimdi A paketini yüklemek istiyorsunuz.

**NuGet 2,2 ve üzeri sürümlerde:**

* A paketini yüklerken, 1.0.2 var olan sürüm 1.0.0 = 1.0.0 olan bağımlılık sürümü >kısıtlamasını zaten karşılayıp karşılamadığını, NuGet, B 'yi 'e otomatik olarak güncelleştirir.

**NuGet 2,5 ve üzeri sürümlerde:**

* Mevcut sürüm 1.0.0 'in bağımlılık sürümü kısıtlamasını karşılayıp karşılamadığını algıladığı için NuGet artık B 'yi güncelleştirmeyecektir.

Bu değişiklik hakkında daha fazla arka plan için, ayrıntılı [iş öğesini](http://nuget.codeplex.com/workitem/1681) ve ilgili [tartışma iş parçacığını](http://nuget.codeplex.com/discussions/436712)okuyun.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>nuget.exe ayrıntılı ayrıntı düzeyine sahip http istekleri çıkışı verir

Sorun giderme nuget.exe veya işlemler sırasında HTTP isteklerinin ne olduğunu merak ediyorsanız, '-ayrıntı detaylı ' anahtar artık yapılan tüm HTTP isteklerinin çıktısını almış olur.

![nuget.exe 'den HTTP çıkışı](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>nuget.exe Push artık UNC ve klasör kaynaklarını destekliyor

NuGet 2,5 ' den önce, bir UNC yoluna veya yerel klasöre göre bir paket kaynağına ' nuget.exe Push ' çalıştırmayı denediyseniz, gönderim başarısız olur. Son eklenen hiyerarşik yapılandırma özelliği sayesinde, nuget.exe bir UNC/klasör kaynağını veya HTTP tabanlı bir NuGet galerisini hedeflemesini gerektiren bir yaygın hale geldi.

NuGet 2,5 ' den başlayarak bir UNC/klasör kaynağını nuget.exe, kaynağa dosya kopyalama işlemi gerçekleştirilir.

Aşağıdaki komut şimdi çalışacaktır:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>nuget.exe, açıkça belirtilen yapılandırma dosyalarını destekler

Yapılandırmaya erişen nuget.exe komutları (tüm ' spec ' ve ' Pack ' hariç), artık% AppData% \nuget\Nuget.Config konumundaki varsayılan yapılandırma dosyasının yerine belirli bir yapılandırma dosyasını zorlayan yeni bir '-ConfigFile ' seçeneğini destekliyor.

Örnek:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Yerel projeler için destek

NuGet 2,5 ile NuGet araçları artık Visual Studio 'daki yerel projeler için kullanılabilir. Birçok yerel paketin, [Coapp projesi](http://coapp.org)tarafından oluşturulan bir aracı kullanarak yukarıdaki MSBuild içeri aktarma özelliğinden yararlanacağız. Daha fazla bilgi için coapp.org Web sitesindeki [araçla ilgili ayrıntıları](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) okuyun.

"Yerel" hedef çerçeve adı, paketler yerel bir projeye yüklendiğinde \Build, \content ve \Tools dosyalarına dosya eklemek için kullanılır.  \`LIB ' klasörü yerel projeler için kullanılmıyor.
