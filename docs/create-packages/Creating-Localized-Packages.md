---
title: Yerelleştirilmiş bir NuGet paketi oluşturma
description: Tüm derlemeleri tek bir pakette ekleyerek veya ayrı derlemeler yayımlayarak yerelleştirilmiş NuGet paketleri oluşturmanın iki yolu hakkında ayrıntılı bilgi.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: dbc3781bd17f815c6b32fc70b275469337148f41
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488828"
---
# <a name="creating-localized-nuget-packages"></a>Yerelleştirilmiş NuGet paketleri oluşturma

Bir kitaplığın yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:

1. Tüm yerelleştirilmiş kaynaklar derlemelerini tek bir pakete dahil edin.
1. Katı bir kural kümesini izleyerek ayrı yerelleştirilmiş uydu paketleri oluşturun.

Her iki yöntem de aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları vardır.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Tek bir pakette yerelleştirilmiş kaynak derlemeleri

Yerelleştirilmiş kaynak derlemelerini tek bir pakette içermek genellikle en basit yaklaşımdır. Bunu yapmak için, paket varsayılanını ( `lib` en-US olarak kabul edilir) dışında desteklenen bir dil için klasörler oluşturun. Bu klasörlerde, kaynak derlemelerini ve yerelleştirilmiş IntelliSense XML dosyalarını yerleştirebilirsiniz.

Örneğin, aşağıdaki klasör yapısı, Almanca (de), Italyanca (It), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant) destekler:

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

Dillerin, `net40` hedef Framework klasörünün altında listelendiğini görebilirsiniz. [Birden çok](../create-packages/supporting-multiple-target-frameworks.md)çerçeveyi destekliyorsanız, her çeşit için altında `lib` bir klasörünüz vardır.

Bu klasörlerle birlikte, içindeki `.nuspec`tüm dosyalara başvurun:

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

Bu yaklaşımı kullanan bir örnek paket, [Microsoft. Data. OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Avantajlar ve dezavantajlar (yerelleştirilen kaynak derlemeleri)

Tek bir paketteki tüm dillerin paket, birkaç dezavantaja sahiptir:

1. **Paylaşılan meta veriler**: Bir NuGet paketi yalnızca tek `.nuspec` bir dosya içerebildiğinden, meta verileri yalnızca tek bir dil için sağlayabilirsiniz. Diğer bir deyişle, NuGet yerelleştirilmiş meta verileri desteklemez ' i sunmaz.
1. **Paket boyutu**: Destekledikleri dillerin sayısına bağlı olarak, kitaplık önemli ölçüde büyük olabilir ve bu da paketi yüklemeyi ve geri yüklemeyi yavaşlatır.
1. **Eşzamanlı yayınlar**: Yerelleştirilmiş dosyaları tek bir pakette paketleme, her yerelleştirmeyi ayrı olarak serbest bırakmak yerine, bu paketteki tüm varlıkları aynı anda serbest bırakmanız gerekir. Ayrıca, herhangi bir Yerelleştirmede yapılan herhangi bir güncelleştirme paketin tamamının yeni bir sürümünü gerektirir.

Bununla birlikte, Ayrıca birkaç avantaj de vardır:

1. **Basitlik**: Paketin tüketicileri, her dili ayrı olarak yüklemek zorunda kalmak yerine, desteklenen tüm dilleri tek bir yüklemede alır. Tek bir paket de nuget.org üzerinde bulmayı daha kolay hale getirir.
1. **Bağlanmış sürümler**: Tüm kaynak derlemeleri birincil derlemeyle aynı pakette olduğundan, hepsi aynı sürüm numarasını paylaşır ve hatalı şekilde ayrılmasıyla bir risk çalıştırmaz.

## <a name="localized-satellite-packages"></a>Yerelleştirilmiş uydu paketleri

.NET Framework uydu derlemelerini desteklediğine benzer şekilde, bu yöntem yerelleştirilmiş kaynakları ve IntelliSense XML dosyalarını uydu paketlerine ayırır.

Bunu yaptığınızda, birincil paketiniz adlandırma kuralını `{identifier}.{version}.nupkg` kullanır ve varsayılan dil için derlemeyi içerir (örneğin, en-US). Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapıyı içerir:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Daha sonra bir uydu derlemesi, `{identifier}.{language}.{version}.nupkg` `ContosoUtilities.de.1.0.0.nupkg`gibi adlandırma kuralını kullanır. Tanımlayıcının, birincil paketin ile tam olarak eşleşmesi **gerekir** .

Bu ayrı bir paket olduğundan, yerelleştirilmiş meta verileri içeren kendi `.nuspec` dosyasına sahiptir. İçindeki `.nuspec` dilin dosya adında kullanılan bir ile eşleşmesi gerektiğini unutmayın.

Uydu derlemesi, [] sürümü gösterimini kullanarak birincil paketin bir bağımlılık olarak tam bir sürümünü de bildirmelidir (bkz. [paket sürümü oluşturma](../concepts/package-versioning.md)). Örneğin, `ContosoUtilities.de.1.0.0.nupkg` `ContosoUtilities.1.0.0.nupkg` gösterimini kullanarak`[1.0.0]` bir bağımlılık bildirmelidir. Uydu paketinin, birincil paketten farklı bir sürüm numarası olabilir.

Uydu paketinin yapısı, kaynak derlemesini ve xml IntelliSense dosyasını paket dosya adında eşleşen `{language}` bir alt klasöre dahil etmelidir:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Note**: gibi belirli alt kültürler `ja-JP` gerekli değilse, her zaman daha yüksek düzey `ja`dil tanımlayıcısını kullanın, örneğin.

Bir uydu derlemesinde, NuGet **yalnızca** dosya adında ile eşleşen `{language}` klasördeki dosyaları algılar. Diğerlerinin hepsi yok sayılır.

Bu kuralların hepsi karşılandığında, NuGet paketi bir uydu paketi olarak tanır ve yerelleştirilmiş dosyaları, özgün olarak paketlenmiş gibi birincil paketin `lib` klasörüne yükler. Uydu paketini kaldırmak, dosyalarını aynı klasörden kaldırır.

Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz. Bir örnek için, ASP.NET MVC paketlerinin kümesini inceleyin:

- [Microsoft. Aspnet. Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)
- [Microsoft.Aspnet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanca)
- [Microsoft. Aspnet. Mvc. ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)
- [Microsoft. Aspnet. Mvc. zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))
- [Microsoft. Aspnet. Mvc. zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))

### <a name="summary-of-required-conventions"></a>Gerekli kuralların Özeti

- Birincil paketin adlandırılmış olması gerekir`{identifier}.{version}.nupkg`
- Uydu paketinin adlandırılmış olması gerekir`{identifier}.{language}.{version}.nupkg`
- Uydu paketinin `.nuspec` dosya adıyla eşleşecek şekilde dilini belirtmesi gerekir.
- Uydu paketinin, `.nuspec` dosyasındaki [] gösterimini kullanarak, birincil öğesinin tam bir sürümüne bağımlılık bildirmesi gerekir. Aralıklar desteklenmez.
- Uydu paketinin dosya adında tam olarak eşleşen `lib\[{framework}\]{language}` `{language}` klasörü yerleştirmeleri gerekir.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Avantajlar ve dezavantajlar (uydu paketleri)

Uydu paketlerinin kullanılması birkaç avantaj sunar:

1. **Paket boyutu**: Birincil paketin genel parmak izi en aza indirilir ve tüketiciler yalnızca kullanmak istedikleri her dilin maliyetlerine neden olur.
1. **Ayrı meta veriler**: Her uydu paketinin kendi `.nuspec` dosyası ve bu nedenle kendi yerelleştirilmiş meta verileri vardır. Bu, nuget.org ' i yerelleştirilmiş koşullara göre arayarak bazı tüketicilerin paketleri daha kolay bulmasına izin verebilir.
1. **Ayrılmış yayınlar**: Uydu derlemeleri her seferinde değil, tek seferde yayımlanabilecek ve yerelleştirme çabalarınızı yaymanızı sağlar.

Ancak uydu paketleri kendi dezavantajlarına sahiptir:

1. **Dağınıklığı**: Tek bir paket yerine, nuget.org üzerinde karışık arama sonuçlarına ve bir Visual Studio projesindeki başvuruların uzun listesine yol açabilecek birçok paketiniz vardır.
1. **Katı kurallar**. Uydu paketleri, kuralları tam olarak izlemelidir veya yerelleştirilmiş sürümler doğru bir şekilde çekilmeyecektir.
1. **Sürüm oluşturma**: Her uydu paketinin, birincil pakette tam bir sürüm bağımlılığı olmalıdır. Bu, birincil paketin güncelleştirilmesi, kaynakların değişmese de tüm uydu paketlerinin güncelleştirilmesini gerektirebileceği anlamına gelir.
