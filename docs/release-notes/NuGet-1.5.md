---
title: NuGet 1,5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,5 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383355"
---
# <a name="nuget-15-release-notes"></a>NuGet 1,5 sürüm notları

[Nuget 1,4 sürüm notları](../release-notes/nuget-1.4.md) | [NuGet 1,6 sürüm notları](../release-notes/nuget-1.6.md)

NuGet 1,5, 30 Ağustos 2011 tarihinde yayınlanmıştır.

## <a name="features"></a>Özellikler

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Önceden yüklenmiş NuGet paketlerine sahip proje şablonları
Yeni bir ASP.NET MVC 3 proje şablonu oluştururken, projeye dahil edilen jQuery betik kitaplıkları, NuGet paketleri yüklenerek buraya yerleştirilir.

ASP.NET MVC 3 proje şablonu, proje şablonu çağrıldığında yüklenen bir NuGet paketleri kümesi içerir. Bir proje şablonu ile NuGet paketleri dahil etme özelliği artık _herhangi_ bir proje şablonunun avantajlarından yararlanabilme özelliği olan bir NuGet özelliğidir.

Bu özellik hakkında daha fazla bilgi için bu [blog gönderisini özelliğin geliştiricisi ile](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)okuyun.

### <a name="explicit-assembly-references"></a>Açık bütünleştirilmiş kod başvuruları

Paket içindeki hangi derlemelerin başvurulduğunu açıkça belirtmek için kullanılan yeni bir `<references />` öğesi eklendi.

Örneğin, aşağıdakileri eklerseniz:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Daha sonra, klasörde başka derlemeler olsa bile `lib` klasörünün uygun [Framework/profile alt](../reference/nuspec.md#explicit-assembly-references) klasöründen yalnızca `xunit.dll` ve `xunit.extensions.dll` başvurulur.

Bu öğe atlanmışsa, her bir derleme için `lib` klasöründeki her derlemeye başvurmak üzere normal davranış uygulanır.

__Bu özellik ne için kullanılır?__

Bu özellik yalnızca tasarım zamanı derlemelerini destekler. Örneğin, kod sözleşmeleri kullanılırken, Visual Studio 'Nun bunları bulabilmesi için, anlaşma derlemelerinin, iyileştirdikleri çalışma zamanı derlemelerinin yanında olması gerekir, ancak sözleşme derlemelerinin proje tarafından gerçekten başvurulması ve `bin` klasörüne kopyalanmaması gerekir.

Benzer şekilde, özelliği, araç derlemelerinin çalışma zamanı derlemelerinin yanında konumlandırılabilir, ancak proje başvurularından hariç tutulması gereken XUnit gibi birim testi çerçeveleri için de kullanılabilir.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>. Nuspec içindeki dosyaları dışarıda bırakma özelliği eklendi
Bir `.nuspec` dosyasındaki `<file>` öğesi, bir joker karakter kullanarak belirli bir dosyayı veya dosya kümesini eklemek için kullanılabilir. Joker karakter kullanırken, eklenen dosyaların belirli bir alt kümesini dışlayamazsınız. Örneğin, belirli bir klasörde yer alan tüm metin dosyalarını istediğiniz gibi düşünün.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Birden çok dosya belirtmek için noktalı virgül kullanın.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Ya da tüm yedekleme dosyaları gibi bir dosya kümesini dışlamak için bir joker karakter kullanın

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>İletişim kutusu kullanarak paketleri kaldırma bağımlılıklarını kaldırma istemleri
Bağımlılıklar içeren bir paket kaldırılırken, NuGet istemleri, paket ile birlikte paketin bağımlılıklarının kaldırılmasına izin verir.

![Bağımlı paketler kaldırılıyor](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` komut geliştirmesi
`Get-Package` komutu artık `-ProjectName` parametresini destekliyor. Bu nedenle komut

    Get-Package –ProjectName A

, A projesinde yüklü olan tüm paketleri listeler.

### <a name="support-for-proxies-that-require-authentication"></a>Kimlik doğrulaması gerektiren proxy 'Ler için destek
Kimlik doğrulaması gerektiren bir proxy 'nin arkasında NuGet kullanılırken, NuGet artık proxy kimlik bilgilerini ister. Kimlik bilgilerinin girilmesi, NuGet 'in uzak depoya bağlanmasına izin verir.

### <a name="support-for-repositories-that-require-authentication"></a>Kimlik doğrulaması gerektiren depolar için destek
NuGet artık temel veya NTLM kimlik doğrulaması gerektiren [özel depolara](../hosting-packages/local-feeds.md) bağlanmayı desteklemektedir.

Özet kimlik doğrulaması desteği gelecek bir sürüme eklenecektir.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org deposunda performans iyileştirmeleri
Paket listesini ve aramayı daha hızlı hale getirmek için nuget.org galerisinde çeşitli performans geliştirmeleri yaptık.

### <a name="solution-dialog-project-filtering"></a>Çözüm iletişim kutusu proje filtreleme
Çözüm düzeyi iletişim kutusunda, hangi projelerin yükleneceğini sorduktan sonra yalnızca seçili paketle uyumlu olan projeleri gösteririz.

### <a name="package-release-notes"></a>Paket sürüm notları
NuGet paketleri artık sürüm notları desteğini içerir. Sürüm notları yalnızca bir paket için _güncelleştirmeler_ görüntülenirken görünür, bu nedenle bunları ilk sürüme eklemek mantıklı değildir.

![Güncelleştirmeler sekmesi içinde sürüm notları](./media/manage-nuget-packages-release-notes.png)

Bir pakete sürüm notları eklemek için NuSpec dosyanızdaki yeni `<releaseNotes />` meta veri öğesini kullanın.

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec & ltfiles/&gt; iyileştirmesi
`.nuspec` dosyası artık, NuGet. exe ' nin pakete herhangi bir dosya içermediği anlamına gelen boş `<files />` öğesine izin veriyor.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1,5, Toplam 107 iş öğesine sahipti. 103 tanesi hata olarak işaretlendi.

NuGet 1,5 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)' ni görüntüleyin.

## <a name="bug-fixes-worth-noting"></a>Hata düzeltmeleri dikkat edilecek değer:

* [Sorun 1273](http://nuget.codeplex.com/workitem/1273): paketleri alfabetik olarak sıralayarak ve fazladan boşluk kaldırarak daha fazla sürüm denetimi `packages.config` yapıldı.
* [Sorun 844](http://nuget.codeplex.com/workitem/844): sürüm numaraları, `Install-Package 1.0` sürüm `1.0.0`bir pakette çalışacak şekilde normalleştirilmektedir.
* [Sorun 1060](http://nuget.codeplex.com/workitem/1060): NuGet. exe kullanarak bir paket oluştururken `-Version` bayrağı `<version />` öğesini geçersiz kılar.
