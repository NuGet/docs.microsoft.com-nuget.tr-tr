---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610537"
---
Paket tanımlayıcısı ve sürüm numarası, pakette bulunan tam kodu benzersiz bir şekilde tanımladıklarından, projedeki en önemli iki değer vardır.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: tanımlayıcı, NuGet.org genelinde benzersiz olmalıdır veya paketi barındıran Galeri. Bir tanımlayıcıya karar vermeden önce, adın zaten kullanımda olup olmadığını denetlemek için ilgili galeride arama yapın. Çakışmaları önlemek için, `Contoso.` gibi, tanımlayıcının ilk parçası olarak şirketinizin adını kullanmak iyi bir modeldir.
- **Ad alanı benzeri adlar**: kısa çizgi yerine nokta gösterimini kullanarak .net 'teki ad alanlarına benzer bir model izleyin. Örneğin, `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`yerine `Contoso.Utility.UsefulStuff` kullanın. Tüketiciler ayrıca, paket tanımlayıcısı kodda kullanılan ad alanları ile eşleştiğinde yararlı olduğunu bulur.
- **Örnek paketler**: başka bir paketin nasıl kullanılacağını gösteren bir örnek kod paketi oluşturursanız, `Contoso.Utility.UsefulStuff.Sample` ' de olduğu gibi `.Sample` ' i tanımlayıcıda sonek olarak ekleyin. (Örnek paketin, diğer pakete bağımlılığı vardır.) Örnek bir paket oluştururken, `<IncludeAssets>``contentFiles` değerini kullanın. `content` klasöründe, örnek kodu `\Samples\Contoso.Utility.UsefulStuff.Sample`gibi `\Samples\<identifier>` adlı bir klasörde düzenleyin.

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, paketin sürümünü proje (veya bütünleştirilmiş kod) ile eşleşecek şekilde ayarlayın, ancak bu kesinlikle gerekli değildir. Bu, bir paketi tek bir derlemeyle sınırlandırdığınızda basit bir işlemdir. Genel olarak, NuGet 'in derleme sürümlerini değil, bağımlılıkları çözümlerken Paket sürümleriyle uğraşır olduğunu unutmayın.
- Standart olmayan bir sürüm düzeni kullanırken, [paket sürümü oluşturma](../../concepts/package-versioning.md)bölümünde açıklandığı gibi NuGet sürüm oluşturma kurallarını dikkate aldığınızdan emin olun. NuGet genellikle [semver 2 uyumludur](../../concepts/package-versioning.md#semantic-versioning-200).

> Bağımlılık çözümleme hakkında daha fazla bilgi için bkz. [PackageReference Ile bağımlılık çözünürlüğü](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Sürüm oluşturmayı daha iyi anlamak için de yararlı olabilecek eski bilgiler için, bu blog gönderilerine bakın.
>
> - [1. Bölüm: DLL Hell üzerinde alma](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [2. Bölüm: çekirdek algoritması](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3. kısım: bağlama yeniden yönlendirmeleri aracılığıyla birleşme](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
