---
title: Yerelleştirilmiş bir NuGet paketi oluşturma | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Oluşturmanın iki yolu ayrıntıları da tüm derlemelerin tek bir pakete dahil etme veya ayrı derlemeler yayımlama NuGet paketleri yerelleştirilmiş.
keywords: NuGet paket yerelleştirme, yerelleştirilmiş paketleri, NuGet yerelleştirme kuralları oluşturma NuGet uydu derlemeleri
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 39ff6d300ec1a1f7941cad5953599f25f55117f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-localized-nuget-packages"></a>Yerelleştirilmiş NuGet paketleri oluşturma

Bir kitaplık yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:

1. Tüm yerelleştirilmiş kaynaklar derlemeleri tek bir paket içerir.
1. Ayrı yerelleştirilmiş uydu paketleri kuralları katı bir dizi izleyerek oluşturun.

Her iki yöntem aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları, sahiptir.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Tek bir pakette yerelleştirilmiş kaynak derlemeler

Yerelleştirilmiş kaynak grupları tek bir paket dahil olmak üzere genellikle en basit yaklaşımdır. Bunu yapmak için klasörler oluşturmanız `lib` için desteklenen dil paketi varsayılandan (tr varsayılır-us). Bu klasörlerde kaynak derlemeler ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.

Örneğin, aşağıdaki klasör yapısını destekler, Almanca (de), İtalyanca (,), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-atanır) ve Çince (Geleneksel) (zh-Hant):

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

Dilleri tüm altında listelendiğini görebilirsiniz `net40` hedef framework klasör. Kullanıcısıysanız [birden çok çerçeveyi destekleyen](../create-packages/supporting-multiple-target-frameworks.md), altında bir klasör sahip `lib` her değişken için.

Bu klasörler yerinde sonra tüm dosyalarda başvuru, `.nuspec`:

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

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Olumlu ve olumsuz yönleri (yerelleştirilmiş kaynak derlemeler)

Tek bir paketteki tüm diller paketleme birkaç sakıncaları vardır:

1. **Meta veri paylaşılan**: bir NuGet paketi yalnızca tek bir içerebileceğinden `.nuspec` dosya, yalnızca tek bir dil için meta verileri sağlayabilir. Diğer bir deyişle, NuGet yerelleştirilmiş meta verileri sunmaz.
1. **Paket boyutu**: desteklediğiniz dilleri sayısına bağlı olarak, kitaplık yükleme ve paket geri yükleme yavaşlatır oldukça büyük olabilir.
1. **Eşzamanlı sürümleri**: tek bir pakete yerelleştirilmiş dosyaları paketleme gerektirir, paketteki tüm varlıklar eşzamanlı olarak, her yerelleştirme ayrı olarak yayımlamayı bölümlemeye yerine bırakmadan olduğunu. Ayrıca, herhangi bir yerelleştirme için herhangi bir güncelleştirme tüm paketin yeni bir sürümünü gerektirir.

Ancak, aynı zamanda birkaç faydası vardır:

1. **Basitlik**: tüketicileri paketi Al desteklenen tüm dillerde her dil ayrıca yüklemek zorunda kalmadan yerine tek bir yükleme. Tek bir paket üzerinde nuget.org bulmak de kolaydır.
1. **Sürümleri eşleşmiş**: tüm kaynak derlemeler birincil derlemeyle aynı paketteki olduğundan, bunlar tüm aynı sürüm numarasına paylaşır ve yanlışlıkla ayrılmış riski çalıştırmayın.

## <a name="localized-satellite-packages"></a>Yerelleştirilmiş uydu paketleri

Benzer şekilde nasıl .NET Framework uydu derlemelerini destekler, bu yöntem yerelleştirilmiş kaynaklar ve IntelliSense XML dosyaları uydu paketlere ayırır.

Bunun için birincil paketinizi adlandırma kuralı kullanır `{identifier}.{version}.nupkg` ve varsayılan dil (örneğin, en-US) için derleme içerir. Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapısını içerir:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Ardından bir uydu derleme adlandırma kuralı kullanır `{identifier}.{language}.{version}.nupkg`, gibi `ContosoUtilities.de.1.0.0.nupkg`. Tanımlayıcı **gerekir** birincil paketi tam olarak eşleşmesi.

Bu ayrı bir paket olduğundan, kendi yoktur `.nuspec` yerelleştirilmiş meta verileri içeren dosya. Dikkatli olmanızı, dilde `.nuspec` **gerekir** filename kullanılanla aynı.

Uydu derlemesi **gerekir** [] sürüm gösterimini kullanarak bir bağımlılık olarak birincil paketi tam bir sürümünü de bildirme (bkz [paket sürüm](../reference/package-versioning.md)). Örneğin, `ContosoUtilities.de.1.0.0.nupkg` bir bağımlılık üzerindeki bildirilmelidir `ContosoUtilities.1.0.0.nupkg` kullanarak `[1.0.0]` gösterimi. Elbette, uydu paket birincil paketi farklı sürüm numarasından olabilir.

Uydu paketin yapısı sonra kaynak assembly ve IntelliSense dosya ile eşleşen bir alt klasöre içermelidir `{language}` paketi dosya:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Not**: sürece gibi belirli subcultures `ja-JP` gerekliyse, her zaman daha yüksek düzey dil tanımlayıcısını gibi kullanmak `ja`.

Bir uydu derlemede NuGet algılar **yalnızca** eşleşen klasöründeki dosyaları `{language}` dosya. Diğerleri yoksayılır.

Tüm bu kuralları karşılandığında, NuGet paketi uydu paket olarak tanımak ve yerelleştirilmiş dosyaları birincil paket yüklemek `lib` klasörü, bunlar ilk olarak toplanmış olur. Uydu paketi kaldırma dosyalarından aynı bu klasörden kaldırın.

Desteklenen her dil için aynı şekilde ek uydu derlemelerini oluşturursunuz. Örneğin, ASP.NET MVC paket kümesini inceleyin:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)
- [Microsoft.AspNet.Mvc.zh atanır](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))
- [Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))

### <a name="summary-of-required-conventions"></a>Gerekli kuralları özeti

- Birincil paketi olarak adlandırılmalıdır `{identifier}.{version}.nupkg`
- Uydu paket olarak adlandırılmalıdır `{identifier}.{language}.{version}.nupkg`
- Uydu paketin `.nuspec` filename eşleşecek şekilde dili belirtmeniz gerekir.
- Bir uydu paketi bir bağımlılık [] noktalı gösterim kullanılarak birincil tam bir sürümünü bildirmelidir kendi `.nuspec` dosya. Aralıkları desteklenmez.
- Uydu paket dosyalarında yerleştirmelisiniz `lib\[{framework}\]{language}` tam olarak eşleşen klasör `{language}` dosya.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Olumlu ve olumsuz yönleri (uydu paketleri)

Uydu paketleri kullanma birkaç faydası vardır:

1. **Paket boyutu**: birincil paketinin genel ayak en aza indirilir ve tüketicilerin yalnızca bunlar kullanmak istediğiniz her bir dilin maliyetinden doğurur.
1. **Ayrı meta veri**: Her uydu paket kendi sahip `.nuspec` dosyası ve bu nedenle yerelleştirilmiş metaverileri olduğundan. Bu yerelleştirilmiş koşullarla nuget.org arayarak paketleri daha kolay bulmak bazı tüketiciler izin verebilirsiniz.
1. **Ayrılmış sürümleri**: uydu derlemelerini serbest bırakılabilir zamanla yerine tüm aynı anda yerelleştirme çabalarınız yayılan olanak sağlar.

Ancak, uydu paketleri kendi kümesi dezavantajları vardır:

1. **Dağınıklığı**: yerine tek bir paket, yığın arama sonuçlarını nuget.org ve Visual Studio projede başvuruları uzun bir listesi neden olabilecek birçok paketleri sahiptir.
1. **Katı kuralları**. Uydu paketleri kurallarına tam olarak uymalıdır veya yerelleştirilmiş sürümleri düzgün çekilmesi olmaz.
1. **Sürüm oluşturma**: Her uydu paket bir tam sürüm bağımlılığı birincil paketi sahip olmalıdır. Kaynakları değişmedi olsa bile bu birincil paketi güncellemeden tüm uydu paketleri de güncelleştirme gerektirebileceği anlamına gelir.
