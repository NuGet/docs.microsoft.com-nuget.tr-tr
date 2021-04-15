---
title: İmzalı paketler
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508806"
---
# <a name="signed-packages"></a>İmzalanmış paketler

*NuGet 4.6.0 + ve Visual Studio 2017 sürüm 15,6 ve üzeri*

NuGet paketleri, değiştirilen içeriğe karşı koruma sağlayan dijital bir imza içerebilir. Bu imza, paketin gerçek kaynağına özgünlük sağlamaları ekleyen bir X. 509.440 sertifikasından oluşturulur.

İmzalı paketler en güçlü uçtan uca doğrulama sağlar. İki farklı türde NuGet imzası vardır:
- **Yazar imzası**. Yazar imzası, paketin, paketin hangi depodan veya hangi taşıma yönteminden bağımsız olarak teslim edildiğini değil, yazar tarafından imzalanmasından bu yana paketin değiştirilmediğinden emin olur. Ayrıca, imzalama sertifikasının zaman içinde kaydedilmesi gerektiğinden, yazar imzalı paketler nuget.org yayımlama işlem hattına ek bir kimlik doğrulama mekanizması sağlar. Daha fazla bilgi için bkz. [sertifikaları kaydetme](#signature-requirements-on-nugetorg).
- **Depo imzası**. Depo imzaları, bu paketlerin İmzalandıkları özgün depodan farklı bir konumdan elde edilse bile, bir depodaki **Tüm** paketlere yönelik bir bütünlük garantisi sağlar.   

Yazar imzalı bir paket oluşturma hakkında ayrıntılı bilgi için bkz. [Imzalama paketleri](../create-packages/Sign-a-package.md) ve [NuGet Sign komutu](../reference/cli-reference/cli-ref-sign.md). [DotNet NuGet Verify](/dotnet/core/tools/dotnet-nuget-verify) veya [NuGet Verify](../reference/cli-reference/cli-ref-verify.md) komutlarını kullanarak paketlerin imzalarını doğrulayabilirsiniz.

> [!Important]
> Yazar imzalama paketleri şu anda yalnızca Windows üzerinde nuget.exe tarafından desteklenir. Ancak, nuget.org ' e yüklenen tüm paketler otomatik olarak depo imzalanır.

## <a name="certificate-requirements"></a>Sertifika gereksinimleri

Paket imzalama, `id-kp-codeSigning` Amaç [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] için geçerli olan özel bir sertifika türü olan bir kod imzalama sertifikası gerektirir. Ayrıca, sertifikanın RSA ortak anahtar uzunluğu 2048 bit veya üzeri olmalıdır.

## <a name="timestamp-requirements"></a>Zaman damgası gereksinimleri

İmzalı paketler, imza geçerliliğini paket imza sertifikasının geçerlilik süresinden daha fazla güvence altına almak için bir RFC 3161 zaman damgası içermelidir. Zaman damgasını imzalamak için kullanılan sertifika, `id-kp-timeStamping` Amaç [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] için geçerli olmalıdır. Ayrıca, sertifikanın RSA ortak anahtar uzunluğu 2048 bit veya üzeri olmalıdır.

Ek teknik ayrıntılar, [paket imzası teknik özellikleri](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) 'nde (GitHub) bulunabilir.

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org üzerindeki imza gereksinimleri

nuget.org, imzalı bir paketi kabul etmek için ek gereksinimlere sahiptir:

- Birincil imza bir yazar imzası olmalıdır.
- Birincil imza tek bir geçerli zaman damgasına sahip olmalıdır.
- Yazar imzası ve onun zaman damgası imzası için X. 509.440 sertifikaları:
  - Bir RSA ortak anahtarı 2048 bit veya daha büyük olmalıdır.
  - Nuget.org üzerinde paket doğrulama sırasında geçerli UTC saati başına geçerlilik süresi içinde olmalıdır.
  - , Windows 'ta varsayılan olarak güvenilen bir güvenilen kök yetkiliye zincirlenmelidir. Kendi kendine verilen sertifikalarla imzalanmış paketler reddedilir.
  - Amacı için geçerli olmalıdır: 
    - Yazar imza sertifikası kod imzalama için geçerli olmalıdır.
    - Zaman damgası sertifikası damgalama için geçerli olmalıdır.
  - İmza zamanında iptal edilmemelidir. (Bu, Gönderim zamanında bu şekilde bilmeyebilir, bu nedenle nuget.org düzenli olarak iptal durumunu denetler).
  
  
## <a name="related-articles"></a>İlgili makaleler:

- [NuGet paketleri imzalanıyor](../create-packages/Sign-a-Package.md)
- [DotNet CLı kullanarak imzalı paketleri doğrulama](/dotnet/core/tools/dotnet-nuget-verify)
- [nuget.exekullanarak imzalı paketleri doğrulama ](../reference/cli-reference/cli-ref-verify.md)
- [Paket güven sınırlarını yönetme](../consume-packages/installing-signed-packages.md)
