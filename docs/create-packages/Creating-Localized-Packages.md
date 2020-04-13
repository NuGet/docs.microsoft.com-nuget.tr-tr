---
title: Yerelleştirilmiş NuGet Paketi Nasıl Oluşturulur?
description: Tüm derlemeleri tek bir pakete ekleyerek veya ayrı derlemeler yayımlayarak yerelleştirilmiş NuGet paketleri oluşturmanın iki yolu hakkındaki ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610947"
---
# <a name="creating-localized-nuget-packages"></a>Yerelleştirilmiş NuGet paketleri oluşturma

Kitaplığın yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:

1. Tüm yerelleştirilmiş kaynak derlemelerini tek bir pakete ekleyin.
1. Katı bir dizi kuralı izleyerek ayrı yerelleştirilmiş uydu paketleri oluşturun.

Her iki yöntemin de avantajları ve dezavantajları vardır, aşağıdaki bölümlerde açıklandığı gibi.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Tek bir pakette yerelleştirilmiş kaynak derlemeleri

Yerelleştirilmiş kaynak derlemelerini tek bir pakete dahil etmek genellikle en basit yaklaşımdır. Bunu yapmak için, paket `lib` varsayılanı dışında desteklenen dil için klasörler oluşturun (en-us olarak kabul edilir). Bu klasörlerde kaynak derlemeleri ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.

Örneğin, aşağıdaki klasör yapısı destekler, Almanca (de), İtalyanca (it), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Dillerin tamamının hedef çerçeve klasörü `net40` altında listelenmiş olduğunu görebilirsiniz. Birden çok [çerçeveyi destekliyorsanız,](../create-packages/supporting-multiple-target-frameworks.md)her varyant için `lib` altında bir klasör vardır.

Bu klasörler yerinde, daha sonra tüm dosyaları `.nuspec`başvuru:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Bu yaklaşımı kullanan bir örnek paket [Microsoft.Data.OData 5.4.0'dır.](https://nuget.org/packages/Microsoft.Data.OData/5.4.0)

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Avantajları ve dezavantajları (yerelleştirilmiş kaynak derlemeleri)

Tüm dilleri tek bir pakette birleştirmenin birkaç dezavantajı vardır:

1. **Paylaşılan meta veriler**: NuGet paketi yalnızca `.nuspec` tek bir dosya içerebildiği için, yalnızca tek bir dil için meta veri sağlayabilirsiniz. Diğer bir de, NuGet yerelleştirilmiş meta verileri desteklemez.
1. **Paket boyutu**: Desteklediğiniz dil sayısına bağlı olarak, kitaplık önemli ölçüde büyüyebilir ve bu da paketin yüklenmesini ve geri yüklenmesini yavaşlatır.
1. **Eşzamanlı sürümler**: Yerelleştirilmiş dosyaları tek bir pakete dönüştürmek, her yerelleştirmeyi ayrı ayrı serbest bırakmak yerine, o paketteki tüm varlıkları aynı anda serbest bırakmanızı gerektirir. Ayrıca, herhangi bir yerelleştirme için herhangi bir güncelleştirme tüm paketin yeni bir sürümünü gerektirir.

Ancak, aynı zamanda birkaç faydası vardır:

1. **Basitlik**: Paketin tüketicileri, her dili ayrı ayrı yüklemek yerine desteklenen tüm dilleri tek bir yüklemede alır. Tek bir paketi de nuget.org bulmak daha kolaydır.
1. **Birleştirilmiş sürümler**: Kaynak derlemelerinin tümü birincil derlemeyle aynı pakette olduğundan, hepsi aynı sürüm numarasını paylaşır ve hatalı bir şekilde ayrılma riskiyle karşı çıkmaz.

## <a name="localized-satellite-packages"></a>Yerelleştirilmiş uydu paketleri

.NET Framework'ün uydu derlemelerini desteklemesine benzer şekilde, bu yöntem yerelleştirilmiş kaynakları ve IntelliSense XML dosyalarını uydu paketlerine ayırır.

Bunu yapın, birincil paketiniz adlandırma `{identifier}.{version}.nupkg` kuralını kullanır ve varsayılan dil (en-US gibi) için derlemeyi içerir. Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapıyı içerir:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Uydu derlemesi daha `{identifier}.{language}.{version}.nupkg`sonra adlandırma `ContosoUtilities.de.1.0.0.nupkg`kuralını kullanır, örneğin. Tanımlayıcı, birincil paketinkiyle tam olarak **eşleşmelidir.**

Bu ayrı bir paket olduğundan, `.nuspec` yerelleştirilmiş meta verileri içeren kendi dosyası vardır. Dosya adındaki `.nuspec` dilin dosya adındakullanılan dille **eşleşmesi gerektiğine** dikkat edin.

Uydu derlemesi ayrıca[] sürüm gösterimini kullanarak birincil paketin tam sürümünü bağımlılık olarak **bildirmelidir** (bkz. [Paket sürümü).](../concepts/package-versioning.md) Örneğin, `ContosoUtilities.de.1.0.0.nupkg` `ContosoUtilities.1.0.0.nupkg` `[1.0.0]` notasyonu kullanarak bir bağımlılık bildirmelidir. Uydu paketi, tabii ki, birincil paket daha farklı bir sürüm numarası olabilir.

Uydu paketinin yapısı daha sonra kaynak derlemesini ve XML IntelliSense `{language}` dosyasını paket dosya adıyla eşleşen bir alt klasöre içermelidir:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Not**: Gibi `ja-JP` belirli alt kültürler gerekli olmadıkça, her zaman gibi `ja`daha yüksek düzey dil tanımlayıcısı kullanın.

Uydu derlemesinde, NuGet **yalnızca** dosya `{language}` adıyla eşleşen klasördeki dosyaları tanır. Diğerleri göz ardı edilir.

Tüm bu kurallar karşılandığında, NuGet paketi uydu paketi olarak tanıyacak ve yerelleştirilmiş dosyaları `lib` ilk olarak paketlenmiş gibi birincil paketin klasörüne yükler. Uydu paketini kaldırmak, dosyalarını aynı klasörden kaldırır.

Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz. Örneğin, ASP.NET MVC paketleri kümesini inceleyin:

- [Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)
- [Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanca)
- [Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)
- [Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))
- [Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))

### <a name="summary-of-required-conventions"></a>Gerekli sözleşmelerin özeti

- Birincil paket adlandırılmalıdır`{identifier}.{version}.nupkg`
- Bir uydu paketi adlandırılmalıdır`{identifier}.{language}.{version}.nupkg`
- Uydu paketinin `.nuspec` dosya adıyla eşleşecek dilini belirtmesi gerekir.
- Uydu paketi, `.nuspec` dosyasındaki [] gösterimini kullanarak birincil ürünün tam sürümüne bağımlılık beyan etmelidir. Aralıklar desteklenmez.
- Uydu paketi, dosya adına `lib\[{framework}\]{language}` tam olarak `{language}` uyan dosyaları klasöre yerleştirmelidir.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Avantajları ve dezavantajları (uydu paketleri)

Uydu paketlerinin kullanılmasının birkaç faydası vardır:

1. **Paket boyutu**: Birincil paketin genel ayak izi en aza indirgendi ve tüketiciler yalnızca kullanmak istedikleri her dilin maliyetine maruz kaldılar.
1. **Ayrı meta veriler**: Her `.nuspec` uydu paketinin kendi dosyası ve dolayısıyla kendi yerelleştirilmiş meta verileri vardır çünkü. Bu, bazı tüketicilerin yerelleştirilmiş terimlerle nuget.org arayarak paketleri daha kolay bulmalarını sağlayabilir.
1. **Ayrılmış sürümler**: Uydu derlemeleri zaman içinde, hepsi bir kerede değil, serbest bırakılabilir ve yerelleştirme çabalarınızı yaymanızı sağlar.

Ancak, uydu paketlerinin kendi dezavantajları vardır:

1. **Yığılmayı**: Tek bir paket yerine, nuget.org'da karmaşık arama sonuçlarına ve Visual Studio projesinde uzun bir referans listesine yol açabilecek birçok paketiniz var.
1. **Katı kurallar.** Uydu paketleri nin kurallara tam olarak uyması gerekir veya yerelleştirilmiş sürümler düzgün olarak alınmamalıdır.
1. **Sürüm :** Her uydu paketinin birincil pakete tam bir sürüm bağımlılığı olmalıdır. Bu, kaynaklar değişmemiş olsa bile birincil paketin güncelleştirilmesi nin tüm uydu paketlerinin güncelleştirilmesini gerektirebileceği anlamına gelir.
