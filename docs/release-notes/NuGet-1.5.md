---
title: NuGet 1,5 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.5 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548731"
---
# <a name="nuget-15-release-notes"></a>NuGet 1,5 sürüm notları

[1.4 NuGet sürüm notları](../release-notes/nuget-1.4.md) | [1.6 NuGet sürüm notları](../release-notes/nuget-1.6.md)

NuGet 1.5 30 Ağustos 2011'de yayınlanmıştır.

## <a name="features"></a>Özellikler

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Önceden yüklenmiş NuGet paketleri ile proje şablonları
Yeni bir ASP.NET MVC 3 proje şablonu oluştururken, projeye dahil jQuery betik kitaplıkları gerçekten var NuGet paketlerini yükleyerek yerleştirilir.

ASP.NET MVC 3 proje şablonu proje şablonu çağrıldığında yükleneceğini NuGet paketleri kümesi içerir. Bir proje şablonu ile NuGet paketlerini içerecek şekilde bu özelliği artık NuGet özelliğidir, _herhangi_ proje şablonu artık yararlanabilir.

Bu özellik hakkında daha fazla ayrıntı için bu okuma [özelliğinin geliştirici tarafından blog gönderisi](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Açık derleme başvuruları

Yeni eklenen `<references />` içinde hangi derlemelerin açıkça belirtmek için kullanılan öğe paket başvurulması gerekir.

Örneğin şunu ekleyin:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Ardından yalnızca `xunit.dll` ve `xunit.extensions.dll` uygun başvurulacağını [framework/PROFILE alt](../reference/nuspec.md#explicit-assembly-references) , `lib` klasör klasöründe diğer derlemeler olsa bile.

Bu öğe atlanır sonra her derleme başvurusu olan genel davranış uygulanır `lib` klasör.

__Bu özellik ne için kullanılır?__

Bu özellik yalnızca tasarım zamanı derlemelerini destekler. Örneğin, kod sözleşmeleri kullanırken, sözleşme derlemeleri böylece Visual Studio bunları bulabilirsiniz ancak sözleşme derlemeler proje tarafından gerçekten başvurulmaması gereken ve içine kopyalanmaması gereken büyütmek çalışma zamanı derlemeleri yanında olmasına gerek `bin` klasör.

Benzer şekilde, özellik için gereken çalışma zamanı derlemeleri yanında bulunan, ancak proje başvurularından'hariç tutulan araçları derlemelerini XUnit gibi birim test çerçeveler için kullanılabilir.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>.nuspec dosyaları dışarıda bırak özelliği eklendi
`<file>` Öğesi içinde bir `.nuspec` dosyası, belirli bir dosyayı veya bir joker karakter kullanarak dosyaları eklemek için kullanılabilir. Joker karakter kullanırken, belirli bir alt kümesini eklenen dosyalar hariç tutmak için hiçbir yolu yoktur. Örneğin, belirli bir dışında bir klasördeki tüm metin dosyalarını istediğinizi varsayalım.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Birden çok dosyayı belirtmek için noktalı virgül kullanın.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Veya tüm yedekleme dosyaları gibi dosyaları hariç tutmak için bir joker kullanın

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>İletişim kutusunu kullanarak paketlerini kaldırma bağımlılıkları kaldırmak isteyip istemediğinizi sorar
Bir paket bağımlılığı olan bir paketin bağımlılıkları paketin birlikte kaldırılmasını sağlayan NuGet ister kaldırırken.

![Bağımlı paket kaldırılıyor](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` komut geliştirme
`Get-Package` Komutu artık bir `-ProjectName` parametresi. Bu nedenle komutu

    Get-Package –ProjectName A

A. projesinde yüklü tüm paketleri listeler

### <a name="support-for-proxies-that-require-authentication"></a>Kimlik doğrulaması gerektiren bir proxy için destek
NuGet kimlik doğrulaması gerektiren bir proxy kullanırken, NuGet artık proxy kimlik bilgileri istenir. Kimlik bilgilerini girme uzak depoya bağlanmak NuGet sağlar.

### <a name="support-for-repositories-that-require-authentication"></a>Kimlik doğrulaması gerektiren depoları için destek
NuGet artık destekliyor bağlanma [özel depo](../hosting-packages/local-feeds.md) temel veya NTLM kimlik doğrulaması gerektirir.

Özet kimlik doğrulaması için destek, gelecek sürümlerin birinde eklenecektir.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org depoya performans geliştirmeleri
Nuget.org Galerisine paket listeleme ve daha hızlı arama yapmak için birkaç performans geliştirmeleri yaptık.

### <a name="solution-dialog-project-filtering"></a>Çözüm, proje iletişim filtreleme
Çözüm düzeyinde iletişim kutusunda, hangi projelerin yüklemek isterken, yalnızca seçilen paket ile uyumlu olan projeler göstereceğiz.

### <a name="package-release-notes"></a>Paket sürüm notları
NuGet paketlerini artık sürüm notları için destek içerir. Yayın yalnızca show yukarı görüntülerken notları _güncelleştirmeleri_ bir paket için bu nedenle, değil mantıklı ilk sürümünüzü eklemek.

![Güncelleştirmeler sekmesini içinde sürüm notları](./media/manage-nuget-packages-release-notes.png)

Bir paket için sürüm notları eklemek için yeni kullanın `<releaseNotes />` soubor NuSpec meta veri öğesi.

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt; geliştirme
`.nuspec` Dosya artık sağlayan boş `<files />` herhangi bir dosya paketinde içermeyecek şekilde nuget.exe belirten öğe.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.5, iş öğelerini sabit 107 toplam vardı. Bu 103 hataları olarak işaretlenmiş.

Tam bir listesi için iş öğeleri NuGet 1.5 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Önemli hata düzeltmeleri:

* [Sorunu 1273](http://nuget.codeplex.com/workitem/1273): yapılan `packages.config` paketleri alfabetik sıralama ve fazladan boşlukları kaldırmanın kolay daha fazla sürüm denetimi.
* [Sorun 844](http://nuget.codeplex.com/workitem/844): sürüm numaraları artık normalleştirilmiş böylece `Install-Package 1.0` bir paket sürümü ile çalışır `1.0.0`.
* [Sorun 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe kullanarak bir paket oluştururken `-Version` bayrağı geçersiz kılmaları `<version />` öğesi.
