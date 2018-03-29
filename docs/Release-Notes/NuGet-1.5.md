---
title: NuGet 1.5 sürüm notları | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.5 için sürüm notları.
keywords: Özellikler, dcr bilinen sorunlar, NuGet 1.5 sürüm notları, hata düzeltmeleri eklendi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: abb044bab5fdc8748b529a2f0072a7271a3674dd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-15-release-notes"></a>NuGet 1,5 sürüm notları

[NuGet 1.4 sürüm notları](../release-notes/nuget-1.4.md) | [NuGet 1.6 sürüm notları](../release-notes/nuget-1.6.md)

NuGet 1.5 30 Ağustos 2011'de serbest bırakıldı.

## <a name="features"></a>Özellikler

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Önceden yüklenmiş NuGet paketleri ile proje şablonları
Yeni bir ASP.NET MVC 3 proje şablonu oluştururken, projeye dahil jQuery betik kitaplıkları gerçekten var NuGet paketlerini yükleyerek yerleştirilir.

ASP.NET MVC 3 proje şablonu proje şablonu çağrıldığında yüklediğiniz NuGet paketlerini içerir. Bir proje şablonu ile NuGet paketleri dahil etmek için bu özelliği şimdi NuGet özelliğidir, _herhangi_ proje şablonu şimdi yararlanabilir.

Bu özellik hakkında daha fazla ayrıntı için bu okuma [blog gönderisi özelliğinin geliştirici tarafından](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Açık derleme başvuruları

Yeni eklenen `<references />` hangi derlemelerin içinde açıkça belirtmek için kullanılan öğe paket başvurulan.

Örneğin aşağıdakileri ekleyin:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Sonra yalnızca `xunit.dll` ve `xunit.extensions.dll` uygun başvurulacak [framework/profil alt](../reference/nuspec.md#explicit-assembly-references) , `lib` klasöründe diğer derlemelerden olsa bile klasör.

Bu öğe atlanır sonra her derleme başvurusu olduğu genel davranış uygulanır `lib` klasör.

__Bu özellik ne amaçla kullanılır?__

Bu özellik yalnızca tasarım zamanında derlemeleri destekler. Örneğin, kod sözleşmeleri kullanırken, sözleşme derlemeler böylece Visual Studio bunları bulabilir, ancak gerçekte projenin başvurulması değil ve içine kopyalanmaması gereken sözleşme derlemeleri büyütmek çalışma zamanı derlemeleri yanındaki olması gerekir `bin` klasörü.

Benzer şekilde, özellik için çalışma zamanı derlemeleri yanında bulunan, ancak proje başvuruları dışlanan araçları derlemelerini gereken XUnit gibi birim test çerçevelerini için kullanılabilir.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>.nuspec dosyaları dışarıda bırak yeteneği eklendi
`<file>` Öğesi içinde bir `.nuspec` dosyası, belirli bir dosya veya bir joker karakter kullanarak dosyaları eklemek için kullanılabilir. Joker karakter kullanırken, belirli bir alt kümesini eklenen dosyalar hariç tutulacak yolu yoktur. Örneğin, belirli bir dışında bir klasördeki tüm metin dosyalarını istediğinizi varsayalım.

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

Ya tüm yedekleme dosyaları gibi dosyaları kümesini dışarıda bırakmak için joker kullanın

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>İletişim kutusunu kullanarak paketleri kaldırma bağımlılıkları kaldırmak isteyip istemediğinizi sorar
Bir paket bağımlılıkları, NuGet ister, kaldırırken paketiyle birlikte paketin bağımlılıklarını kaldırılmasını izin verme.

![Bağımlı paketler kaldırma](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` komut geliştirme
`Get-Package` Komutu şimdi destekleyen bir `-ProjectName` parametresi. Bu nedenle komutu

    Get-Package –ProjectName A

A. projesinde yüklü olan tüm paketleri listeler

### <a name="support-for-proxies-that-require-authentication"></a>Kimlik doğrulaması gerektiren proxy'leri için destek
NuGet kimlik doğrulaması gerektiren bir proxy kullanırken, NuGet şimdi proxy kimlik bilgileri ister. Kimlik bilgilerini girme uzak depoya bağlanmak NuGet sağlar.

### <a name="support-for-repositories-that-require-authentication"></a>Kimlik doğrulaması gerektiren depoları için destek
NuGet artık destekler bağlanmasını [özel depoları](../hosting-packages/local-feeds.md) temel veya NTLM kimlik doğrulaması gerektirir.

Özet kimlik doğrulaması için destek gelecekteki bir sürümde eklenecek.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Nuget.org depo için performans iyileştirmeleri
Paket listesi ve daha hızlı arama yapmak için nuget.org Galeriye birkaç performans iyileştirmeleri yaptık.

### <a name="solution-dialog-project-filtering"></a>Çözüm iletişim proje filtreleme
Çözüm düzeyi iletişim kutusunda, yüklemek hangi projelerde isterken, biz yalnızca seçilen paketiyle uyumlu projeler gösterir.

### <a name="package-release-notes"></a>Paket sürüm notları
NuGet paketlerini artık sürüm notları için destek içerir. Sürüm yalnızca Göster yukarı görüntülerken notları _güncelleştirmeleri_ bir paket için bu nedenle değil kolaylaştırır ilk sürümünüzün eklemek için algılama.

![Güncelleştirmeleri sekme içindeki sürüm notları](./media/manage-nuget-packages-release-notes.png)

Bir paket için sürüm notları eklemek için yeni kullanmak `<releaseNotes />` NuSpec dosyanızı meta veri öğesi.

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt; geliştirme
`.nuspec` Dosya artık verir boş `<files />` herhangi bir dosya paketinde içermeyecek şekilde nuget.exe söyler öğesi.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.5 iş öğeleri sabit 107 toplam vardı. Bu 103 hata olarak işaretlendi.

İş tam listesi için öğeleri NuGet 1.5 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Eşitlenmeyeceği hata düzeltmeleri:

* [Sorun 1273](http://nuget.codeplex.com/workitem/1273): yapılan `packages.config` daha fazla sürüm denetimi paketleri alfabetik sıralama ve fazladan boşlukları kaldırmanın kolay.
* [Sorunu 844](http://nuget.codeplex.com/workitem/844): sürüm numaralarını şimdi normalleştirilmiş böylece `Install-Package 1.0` bir paketi sürümüyle çalışır `1.0.0`.
* [Sorunu 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe, kullanarak bir paket oluştururken `-Version` bayrağı geçersiz kılmaları `<version />` öğesi.
