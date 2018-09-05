---
title: Yerelleştirilmiş bir NuGet paketi oluşturma
description: Tek bir pakette tüm derlemelerin dahil olmak üzere veya ayrı derlemeler yayımlama NuGet paketleri oluşturmanın iki yolu hakkında ayrıntılı bilgi yerelleştirilmiş.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: b1c2511c1fbafc7f52029c23521fa55671b0b5c5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546901"
---
# <a name="creating-localized-nuget-packages"></a>Yerelleştirilmiş NuGet paketleri oluşturma

Bir kitaplık yerelleştirilmiş sürümlerini oluşturmak için iki yol vardır:

1. Tüm yerelleştirilmiş kaynaklar derlemelere tek bir pakette içerir.
1. Kuralları katı bir dizi ayrı yerelleştirilmiş uydu paketleri oluşturma.

Aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları, iki yöntem de sahiptir.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Tek bir paket içinde yerelleştirilmiş kaynak derlemeleri

Tek bir paket içinde yerelleştirilmiş kaynak derlemeleri de dahil olmak üzere genellikle en basit yaklaşımdır. Bunu yapmak için klasörler oluşturma `lib` için desteklenen dil paketi varsayılan dışındaki (tr varsayılır-us). Bu klasörlerde kaynak derlemeleri ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.

Örneğin, aşağıdaki klasör yapısını destekler, Almanca (de), İtalyanca (,), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant):

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

Dilleri tüm altında listelendiğini gördüğünüz `net40` hedef çerçeve klasörü. Size [birden çok çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md), altında bir klasöre sahip `lib` her değişken için.

Bu klasörleri yerinde sonra tüm dosyaları başvuru, `.nuspec`:

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

Bu yaklaşım kullanan bir örnek paket [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Avantajlar ve dezavantajlar (yerelleştirilmiş kaynak bütünleştirilmiş kodları)

Tüm diller, tek bir pakette paketleme bazı dezavantajları vardır:

1. **Meta veri paylaşılan**: yalnızca tek bir NuGet paketi içerebileceğinden `.nuspec` dosyası, yalnızca tek bir dil için meta verileri sağlayabilirsiniz. Diğer bir deyişle, NuGet desteği yerelleştirilmiş meta verileri sunmaz.
1. **Paket boyutu**: desteklediğiniz dilleri sayısına bağlı olarak, kitaplık, yükleme ve paket geri yükleme yavaşlatır önemli ölçüde büyük olabilir.
1. **Eşzamanlı yayınlar**: tek bir pakete yerelleştirilmiş dosyaları paketleme gerektirir, bu paket grubundaki tüm varlıkları eşzamanlı olarak ayrı ayrı her bir yerelleştirme yayınlayabilir olmak yerine yayın. Ayrıca, herhangi bir yerelleştirme için herhangi bir güncelleştirme tüm paketin yeni bir sürümü gerektirir.

Bununla birlikte, bazı avantajları da vardır:

1. **Basitlik**: desteklenen tüm dillerde ayrı ayrı her bir dil yüklemek zorunda yerine tek bir yükleme paketi tüketicileri alın. Tek bir pakette de nuget.org adresinden bulmak daha kolay olur.
1. **Sürümleri eşleşmiş**: tüm kaynak derlemeler birincil derlemeyle aynı pakette olduğundan, bunların tümü aynı sürüm numarasını paylaşır ve deneyebileceğinizi ayrılmış riskini çalıştırmayın.

## <a name="localized-satellite-packages"></a>Yerelleştirilmiş uydu paketleri

Benzer şekilde nasıl .NET Framework uydu derlemelerini destekler, bu yöntem yerelleştirilmiş kaynaklar ve IntelliSense XML dosyalarını uydu paketler ayırır.

Bunun için birincil paketinizi adlandırma kuralını kullanır `{identifier}.{version}.nupkg` ve derleme için varsayılan dil (örneğin, en-US) içerir. Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapısını içerir:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Ardından bir uydu derleme adlandırma kuralını kullanır `{identifier}.{language}.{version}.nupkg`, gibi `ContosoUtilities.de.1.0.0.nupkg`. Tanımlayıcı **gerekir** birincil paketi tam olarak eşleşmesi.

Bu ayrı bir paket olduğundan, kendi yoktur `.nuspec` yerelleştirilmiş meta veriler içeren dosya. Dikkatli olmanızı bu dilde `.nuspec` **gerekir** dosya adında kullanılanla eşleşmelidir.

Uydu derlemesi **gerekir** ayrıca birincil paketi tam bir sürümünü [] sürümü gösterimini kullanarak bir bağımlılık olarak bildirin (bkz [Paket sürümü oluşturma](../reference/package-versioning.md)). Örneğin, `ContosoUtilities.de.1.0.0.nupkg` bağımlılık bildirmeniz gerekir `ContosoUtilities.1.0.0.nupkg` kullanarak `[1.0.0]` gösterimi. Elbette, uydu paket birincil paketi farklı bir sürüm numarasından olabilir.

Uydu paket yapısı sonra kaynak derleme ve IntelliSense XML dosyası ile eşleşen bir alt içermelidir `{language}` paket dosya:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Not**: sürece gibi belirli subcultures `ja-JP` gerekliyse, her zaman daha yüksek düzey bir dil tanımlayıcısı, gibi kullanın `ja`.

Bir uydu derlemesine NuGet tanıyacağınız **yalnızca** eşleşen klasöründeki dosyalarla `{language}` dosya adında. Diğerleri yoksayılır.

Tüm bu kuralları karşılandığında, NuGet paketi bir uydu paketi olarak tanınması ve birincil pakete ait yerelleştirilmiş dosyaları yüklemek `lib` klasör gibi bunlar ilk olarak toplanmış. Uydu paketi dosyalarını aynı bu klasörden kaldırın.

Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz. Örneğin, ASP.NET MVC paketleri kümesini inceleyin:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanya)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)
- [Microsoft.AspNet.Mvc.zh Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))
- [Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))

### <a name="summary-of-required-conventions"></a>Gerekli kuralları özeti

- Birincil paketi olarak adlandırılmalıdır `{identifier}.{version}.nupkg`
- Uydu paket olarak adlandırılmalıdır `{identifier}.{language}.{version}.nupkg`
- Uydu paketin `.nuspec` dosya adını eşleştirmek için dili belirtmeniz gerekir.
- [] Gösterim kullanılarak birincil tam bir sürümünü bir uydu paketi bir bağımlılık bildirmeniz gerekir, `.nuspec` dosya. Aralıkları desteklenmez.
- Uydu paket dosyaları yerleştirmelisiniz `lib\[{framework}\]{language}` tam olarak eşleşen bir klasör `{language}` dosya adında.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Avantajlar ve dezavantajlar (uydu paketler)

Uydu paketlerini kullanma, bazı avantajları vardır:

1. **Paket boyutu**: birincil paketin bütün kapladığı alanı en aza indirilir ve tüketiciler yalnızca, kullanmak istediğiniz her bir dilin maliyetleri doğurur.
1. **Ayrı bir meta veri**: her bir uydu paketi kendi bölümüne sahiptir `.nuspec` dosya ve bu nedenle kendi yerelleştirilmiş meta verileri için. Bu paketleri nuget.org yerelleştirilmiş koşullarıyla arayarak daha kolay bulmak bazı tüketiciler izin verebilirsiniz.
1. **Ayrılmış yayınlar**: uydu derlemeleri serbest bırakılabilir zamanla yerine tümünü tek seferde yerelleştirme çalışmalarınızı yayılan etmenize imkan sağlar.

Ancak, uydu paketleri kendi dezavantajları vardır:

1. **Dağınıklığı**: tek bir paket yerine derli toplu arama sonuçlarını nuget.org ve Visual Studio projede başvuruları uzun listesi yol açabilecek birçok paketleri vardır.
1. **Katı kuralları**. Uydu paketleri tam olarak kurallarına uymalıdır veya yerelleştirilmiş sürümleri düzgün çekilmesi olmaz.
1. **Sürüm oluşturma**: her bir uydu paketi birincil paketi bir tam sürüme bağımlılığı olmalıdır. Kaynakları değişmedi olsa bile bu birincil paketi güncelleştirme de tüm uydu paketlerin güncelleştirilmesi gerektiğini anlamına gelir.
