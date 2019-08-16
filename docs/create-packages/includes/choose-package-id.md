---
ms.openlocfilehash: 7ebe3c0f75b8de158879119bce4df26217849251
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488962"
---
Paket tanımlayıcısı ve sürüm numarası, pakette bulunan tam kodu benzersiz bir şekilde tanımladıklarından, projedeki en önemli iki değer vardır.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: Tanımlayıcının nuget.org genelinde benzersiz olması veya paketi barındırdığı bir galeri olması gerekir. Bir tanımlayıcıya karar vermeden önce, adın zaten kullanımda olup olmadığını denetlemek için ilgili galeride arama yapın. Çakışmaları önlemek için iyi bir model, tanımlayıcı `Contoso.`ilk parçası olarak şirketinizin adını kullanmaktır.
- **Ad alanı benzeri adlar**: Kısa çizgi yerine nokta gösterimini kullanarak .NET 'teki ad alanlarına benzer bir model izleyin. Örneğin, `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` veya yerinekullanın.`Contoso_Utility_UsefulStuff` Tüketiciler ayrıca, paket tanımlayıcısı kodda kullanılan ad alanları ile eşleştiğinde yararlı olduğunu bulur.
- **Örnek paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir örnek kod paketi oluşturursanız, ' de `.Sample` `Contoso.Utility.UsefulStuff.Sample`olduğu gibi, tanımlayıcıda bir sonek olarak iliştirme. (Örnek paketin, diğer pakete bağımlılığı vardır.) Örnek bir paket oluştururken, içindeki `contentFiles` `<IncludeAssets>`değerini kullanın. Klasöründe, örnek kodu içinde `\Samples\Contoso.Utility.UsefulStuff.Sample`olarak adlandırılan `\Samples\<identifier>` bir klasörde düzenleyin. `content`

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, paketin sürümünü proje (veya bütünleştirilmiş kod) ile eşleşecek şekilde ayarlayın, ancak bu kesinlikle gerekli değildir. Bu, bir paketi tek bir derlemeyle sınırlandırdığınızda basit bir işlemdir. Genel olarak, NuGet 'in derleme sürümlerini değil, bağımlılıkları çözümlerken Paket sürümleriyle uğraşır olduğunu unutmayın.
- Standart olmayan bir sürüm düzeni kullanırken, [paket sürümü oluşturma](../../concepts/package-versioning.md)bölümünde açıklandığı gibi NuGet sürüm oluşturma kurallarını dikkate aldığınızdan emin olun. NuGet genellikle [semver 2 uyumludur](../../concepts/package-versioning.md#semantic-versioning-200).

> Bağımlılık çözümleme hakkında daha fazla bilgi için bkz. [PackageReference Ile bağımlılık çözünürlüğü](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference). Sürüm oluşturmayı daha iyi anlamak için de yararlı olabilecek eski bilgiler için, bu blog gönderilerine bakın.
>
> - [Bölüm 1: DLL Hell 'i alma](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Bölüm 2: Çekirdek algoritması](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Bölüm 3: Bağlama yeniden yönlendirmeleri aracılığıyla birleşme](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)