---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817484"
---
Paket tanımlayıcısı ve sürüm numarası, pakette bulunan tam kodu benzersiz bir şekilde tanımladıklarından, projedeki en önemli iki değer vardır.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: Tanımlayıcının nuget.org genelinde benzersiz olması veya paketi barındırdığı bir galeri olması gerekir. Bir tanımlayıcıya karar vermeden önce, adın zaten kullanımda olup olmadığını denetlemek için ilgili galeride arama yapın. Çakışmaları önlemek için iyi bir model, tanımlayıcı `Contoso.`ilk parçası olarak şirketinizin adını kullanmaktır.
- **Ad alanı benzeri adlar**: Kısa çizgi yerine nokta gösterimini kullanarak .NET 'teki ad alanlarına benzer bir model izleyin. Örneğin, `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` veya yerinekullanın.`Contoso_Utility_UsefulStuff` Tüketiciler ayrıca, paket tanımlayıcısı kodda kullanılan ad alanları ile eşleştiğinde yararlı olduğunu bulur.
- **Örnek paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir örnek kod paketi oluşturursanız, ' de `.Sample` `Contoso.Utility.UsefulStuff.Sample`olduğu gibi, tanımlayıcıda bir sonek olarak iliştirme. (Örnek paketin, diğer pakete bağımlılığı vardır.) Örnek bir paket oluştururken, içindeki `contentFiles` `<IncludeAssets>`değerini kullanın. Klasöründe, örnek kodu içinde `\Samples\Contoso.Utility.UsefulStuff.Sample`olarak adlandırılan `\Samples\<identifier>` bir klasörde düzenleyin. `content`

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, paketin sürümünü proje (veya bütünleştirilmiş kod) ile eşleşecek şekilde ayarlayın, ancak bu kesinlikle gerekli değildir. Bu, bir paketi tek bir derlemeyle sınırlandırdığınızda basit bir işlemdir. Genel olarak, NuGet 'in derleme sürümlerini değil, bağımlılıkları çözümlerken Paket sürümleriyle uğraşır olduğunu unutmayın.
- Standart olmayan bir sürüm düzeni kullanırken, [paket sürümü oluşturma](../../reference/package-versioning.md)bölümünde açıklandığı gibi NuGet sürüm oluşturma kurallarını dikkate aldığınızdan emin olun. NuGet genellikle [semver 2 uyumludur](../../reference/package-versioning.md#semantic-versioning-200).

> Bağımlılık çözümleme hakkında daha fazla bilgi için bkz. [PackageReference Ile bağımlılık çözünürlüğü](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Sürüm oluşturmayı daha iyi anlamak için de yararlı olabilecek eski bilgiler için, bu blog gönderilerine bakın.
>
> - [Bölüm 1: DLL Hell 'i alma](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Bölüm 2: Çekirdek algoritması](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Bölüm 3: Bağlama yeniden yönlendirmeleri aracılığıyla birleşme](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)