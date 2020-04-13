---
ms.openlocfilehash: c92f6e0c34347ee8555d416140d95ea2df5a3fbb
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610537"
---
Paket tanımlayıcısı ve sürüm numarası, pakette bulunan tam kodu benzersiz bir şekilde tanımladıkları için projedeki en önemli iki değerdir.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Teklik**: Tanımlayıcı, nuget.org veya pakete ev sahipliği yapan galeride benzersiz olmalıdır. Tanımlayıcıya karar vermeden önce, adın zaten kullanIlip kullanılmadığını kontrol etmek için ilgili galeride arama yapın. Çakışmaları önlemek için, iyi bir desen gibi tanımlayıcının ilk bölümü olarak şirket `Contoso.`adınızı kullanmaktır.
- **Ad alanı benzeri adlar**: Tire yerine nokta gösterimi kullanarak .NET'teki ad boşluklarına benzer bir desen izleyin. Örneğin, kullanmak `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`veya . Tüketiciler, paket tanımlayıcısı kodda kullanılan ad alanlarıyla eşleştiğinde de yararlı olur.
- **Örnek Paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir `.Sample` örnek kod paketi üretirseniz, tanımlayıcıya sonek `Contoso.Utility.UsefulStuff.Sample`olarak iliştirin. (Örnek paket elbette diğer pakete bağımlı olacaktır.) Örnek bir paket oluştururken, `contentFiles` `<IncludeAssets>`'deki değeri kullanın. Klasörde, `content` örnek kodu ' da `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`adlandırılan bir klasörde düzenleyin.

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, paketin sürümünü projeyle (veya derlemeye) uyacak şekilde ayarlayın, ancak bu kesinlikle gerekli değildir. Bir paketi tek bir derlemeyle sınırladiğinizde bu basit bir konudur. Genel olarak, NuGet'in derleme sürümlerini değil, bağımlılıkları çözerken paket sürümleriyle ilgili olduğunu unutmayın.
- Standart olmayan bir sürüm şeması kullanırken, [Paket sürümde](../../concepts/package-versioning.md)açıklandığı gibi NuGet sürüm kurallarını dikkate almayı unutmayın. NuGet çoğunlukla [semver 2 uyumludur.](../../concepts/package-versioning.md#semantic-versioning-200)

> Bağımlılık çözümü hakkında bilgi için [PackageReference ile Bağımlılık çözümü'ne](../../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)bakın. Sürüm yapmayı daha iyi anlamak için de yararlı olabilecek eski bilgiler için bu blog gönderileri serisine bakın.
>
> - [Bölüm 1: DLL Hell alma](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Bölüm 2: Çekirdek algoritması](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Bölüm 3: Bağlayıcı Yönlendirmelerle Birleşme](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)
