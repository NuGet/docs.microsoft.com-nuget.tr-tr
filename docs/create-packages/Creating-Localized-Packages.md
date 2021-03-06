---
title: Yerelleştirilmiş bir NuGet paketi oluşturma
description: Tüm derlemeleri tek bir pakette ekleyerek veya ayrı derlemeler yayımlayarak yerelleştirilmiş NuGet paketleri oluşturmanın iki yolu hakkında ayrıntılı bilgi.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774757"
---
# <a name="creating-localized-nuget-packages"></a>Yerelleştirilmiş NuGet paketleri oluşturma

Bir kitaplığın yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:

1. Tüm yerelleştirilmiş kaynaklar derlemelerini tek bir pakete dahil edin.
1. Katı bir kural kümesini izleyerek ayrı yerelleştirilmiş uydu paketleri oluşturun.

Her iki yöntem de aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları vardır.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Tek bir pakette yerelleştirilmiş kaynak derlemeleri

Yerelleştirilmiş kaynak derlemelerini tek bir pakette içermek genellikle en basit yaklaşımdır. Bunu yapmak için, `lib` paket varsayılanını (en-US olarak kabul edilir) dışında desteklenen bir dil için klasörler oluşturun. Bu klasörlerde, kaynak derlemelerini ve yerelleştirilmiş IntelliSense XML dosyalarını yerleştirebilirsiniz.

Örneğin, aşağıdaki klasör yapısı, Almanca (de), Italyanca (It), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant) destekler:

```
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
```

Dillerin, `net40` hedef Framework klasörünün altında listelendiğini görebilirsiniz. [Birden çok çerçeveyi destekliyorsanız](../create-packages/supporting-multiple-target-frameworks.md), her çeşit için altında bir klasörünüz vardır `lib` .

Bu klasörlerle birlikte, içindeki tüm dosyalara başvurun `.nuspec` :

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

Bu yaklaşımı kullanan bir örnek paket, [Microsoft. Data. OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Avantajlar ve dezavantajlar (yerelleştirilen kaynak derlemeleri)

Tek bir paketteki tüm dillerin paket, birkaç dezavantaja sahiptir:

1. **Paylaşılan meta veriler**: bir NuGet paketi yalnızca tek bir dosya içerebildiğinden `.nuspec` , meta verileri yalnızca tek bir dil için sağlayabilirsiniz. Diğer bir deyişle, NuGet yerelleştirilmiş meta verileri desteklemez ' i sunmaz.
1. **Paket boyutu**: desteklemenizin dil sayısına bağlı olarak, kitaplık önemli ölçüde büyük olabilir ve bu da paketi yüklemeyi ve geri yüklemeyi yavaşlatır.
1. **Eşzamanlı yayınlar**: yerelleştirilmiş dosyaları tek bir pakette paketleme, her yerelleştirmeyi ayrı olarak serbest bırakmak yerine, bu paketteki tüm varlıkları aynı anda serbest bırakmanız gerekir. Ayrıca, herhangi bir Yerelleştirmede yapılan herhangi bir güncelleştirme paketin tamamının yeni bir sürümünü gerektirir.

Bununla birlikte, Ayrıca birkaç avantaj de vardır:

1. **Basitlik**: paketin tüketicileri, her dili ayrı olarak yüklemek zorunda kalmak yerine, desteklenen tüm dilleri tek bir yüklemede alır. Tek bir paket de nuget.org üzerinde bulmayı daha kolay hale getirir.
1. **Bağlanmış sürümler**: tüm kaynak derlemeleri birincil derlemeyle aynı pakette olduğundan, hepsi aynı sürüm numarasını paylaşır ve hatalı bir şekilde ayrılmasıyla bir risk çalıştırmaz.

## <a name="localized-satellite-packages"></a>Yerelleştirilmiş uydu paketleri

.NET Framework uydu derlemelerini desteklediğine benzer şekilde, bu yöntem yerelleştirilmiş kaynakları ve IntelliSense XML dosyalarını uydu paketlerine ayırır.

Bunu yaptığınızda, birincil paketiniz adlandırma kuralını kullanır `{identifier}.{version}.nupkg` ve varsayılan dil için derlemeyi içerir (örneğin, en-US). Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapıyı içerir:

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

Daha sonra bir uydu derlemesi, gibi adlandırma kuralını kullanır `{identifier}.{language}.{version}.nupkg` `ContosoUtilities.de.1.0.0.nupkg` . Tanımlayıcının, birincil paketin ile tam olarak eşleşmesi **gerekir** .

Bu ayrı bir paket olduğundan, `.nuspec` yerelleştirilmiş meta verileri içeren kendi dosyasına sahiptir. İçindeki dilin `.nuspec` dosya adında kullanılan bir ile eşleşmesi **gerektiğini unutmayın** .

Uydu derlemesi, [] sürümü gösterimini kullanarak birincil paketin bir bağımlılık olarak tam bir sürümünü **de bildirmelidir (** bkz. [paket sürümü oluşturma](../concepts/package-versioning.md)). Örneğin, `ContosoUtilities.de.1.0.0.nupkg` gösterimini kullanarak bir bağımlılık bildirmelidir `ContosoUtilities.1.0.0.nupkg` `[1.0.0]` . Uydu paketinin, birincil paketten farklı bir sürüm numarası olabilir.

Uydu paketinin yapısı, kaynak derlemesini ve XML IntelliSense dosyasını paket dosya adında eşleşen bir alt klasöre dahil etmelidir `{language}` :

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

**Note**: gibi belirli alt kültürler gerekli değilse, `ja-JP` her zaman daha yüksek düzey dil tanımlayıcısını kullanın, örneğin `ja` .

Bir uydu derlemesinde, NuGet **yalnızca** dosya adında ile eşleşen klasördeki dosyaları algılar `{language}` . Diğerlerinin hepsi yok sayılır.

Bu kuralların hepsi karşılandığında, NuGet paketi bir uydu paketi olarak tanır ve yerelleştirilmiş dosyaları `lib` , özgün olarak paketlenmiş gibi birincil paketin klasörüne yükler. Uydu paketini kaldırmak, dosyalarını aynı klasörden kaldırır.

Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz. Bir örnek için, ASP.NET MVC paketlerinin kümesini inceleyin:

- [Microsoft. Aspnet. Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)
- [Microsoft.Aspnet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanca)
- [Microsoft. Aspnet. Mvc. ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)
- [Microsoft. Aspnet. Mvc. zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))
- [Microsoft. Aspnet. Mvc. zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))

### <a name="summary-of-required-conventions"></a>Gerekli kuralların Özeti

- Birincil paketin adlandırılmış olması gerekir `{identifier}.{version}.nupkg`
- Uydu paketinin adlandırılmış olması gerekir `{identifier}.{language}.{version}.nupkg`
- Uydu paketinin `.nuspec` dosya adıyla eşleşecek şekilde dilini belirtmesi gerekir.
- Uydu paketinin, dosyasındaki [] gösterimini kullanarak, birincil öğesinin tam bir sürümüne bağımlılık bildirmesi gerekir `.nuspec` . Aralıklar desteklenmez.
- Uydu paketinin dosya `lib\[{framework}\]{language}` adında tam olarak eşleşen klasörü yerleştirmeleri gerekir `{language}` .

### <a name="advantages-and-disadvantages-satellite-packages"></a>Avantajlar ve dezavantajlar (uydu paketleri)

Uydu paketlerinin kullanılması birkaç avantaj sunar:

1. **Paket boyutu**: birincil paketin genel parmak izi en aza indirilir ve tüketiciler yalnızca kullanmak istedikleri her dilin maliyetlerine neden olur.
1. **Ayrı meta veriler**: her uydu paketinin kendi `.nuspec` dosyası ve dolayısıyla kendi yerelleştirilmiş meta verileri vardır. Bu, nuget.org ' i yerelleştirilmiş koşullara göre arayarak bazı tüketicilerin paketleri daha kolay bulmasına izin verebilir.
1. **Ayrılmış yayınlar**: uydu derlemeleri her seferinde değil tek seferde yayımlanabilecek ve yerelleştirme çabalarınızı yaymanızı sağlar.

Ancak uydu paketleri kendi dezavantajlarına sahiptir:

1. **Dağınıklık**: tek bir paket yerine, NuGet.org üzerinde karışık arama sonuçlarına ve bir Visual Studio projesindeki bir dizi başvuruya yönelik uzun bir listeye yol açabilecek çok sayıda paketiniz olabilir.
1. **Katı kurallar**. Uydu paketleri, kuralları tam olarak izlemelidir veya yerelleştirilmiş sürümler doğru bir şekilde çekilmeyecektir.
1. **Sürüm oluşturma**: her uydu paketinin, birincil pakette tam bir sürüm bağımlılığı olmalıdır. Bu, birincil paketin güncelleştirilmesi, kaynakların değişmese de tüm uydu paketlerinin güncelleştirilmesini gerektirebileceği anlamına gelir.
