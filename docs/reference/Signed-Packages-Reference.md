---
title: İmzalı paketlerin
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977517"
---
# <a name="signed-packages"></a>İmzalanmış paketleri

*NuGet 4.6.0+ ve Visual Studio 2017 sürüm 15.6 ve üzeri*

NuGet paketlerini, üzerinde oynanmış bir içerik karşı koruma sağlayan dijital bir imza içerebilir. Bu imza de gerçek paket kaynağı için kimlik doğrulaması kanıtları ekleyen bir X.509 Sertifika oluşturulur.

İmzalanmış paketleri güçlü bir uçtan uca doğrulama sağlar. NuGet imzaları iki farklı tür vardır:
- **Yazar imza**. Bir yazar imzası yazarı paketin olursa olsun gelen upraven'ın paket değiştirilmedi garanti eder, depo veya ne paket teslim yöntemi taşıma. Ayrıca, imzalama sertifikasının önceden kayıtlı olması gerekir çünkü Yazar imzalanmış paketleri nuget.org yayımlama işlem hattı için ek kimlik doğrulama mekanizması sağlar. Daha fazla bilgi için [kayıt sertifikaları](#register-certificate-on-nugetorg).
- **Depo imza**. Depo imzaları sağlamak için bir bütünlük garantisi **tüm** bile bu paketleri nerede oldukları özgün deposu farklı bir konumdan elde edilen yazar, imzalanmış olup bir depoda paketleri imzalanmış.   

Bir yazar imzalı paket oluşturma hakkında daha fazla bilgi edinmek için bkz. [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).

> [!Important]
> Paket imzalama, şu anda yalnızca nuget.exe Windows üzerinde kullanılırken desteklenir. İmzalı paketlerin doğrulama şu anda yalnızca, Windows üzerinde nuget.exe veya Visual Studio kullanılırken desteklenir.

## <a name="certificate-requirements"></a>Sertifika gereksinimleri

Paket imzalama gerektiren bir kod imzalama sertifikası, özel bir türü için geçerli sertifika olan `id-kp-codeSigning` amaçlı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ayrıca, sertifika bir RSA ortak anahtar uzunluğu 2048 bit ya da daha yüksek olmalıdır.

## <a name="timestamp-requirements"></a>Zaman damgası gereksinimleri

İmzalanmış paketleri paketi imzalama sertifikasının geçerlilik süresini aşan geçerlilik imzası emin olmak için bir RFC 3161 zaman damgası içermelidir. Zaman damgası imzalamak için kullanılan sertifika geçerli olmalıdır `id-kp-timeStamping` amaçlı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ayrıca, sertifika bir RSA ortak anahtar uzunluğu 2048 bit ya da daha yüksek olmalıdır.

Ek teknik ayrıntılar bulunabilir [imza teknik özellikleri paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Nuget.org imza gereksinimleri

nuget.org imzalı paket kabul etmek için ek gereksinimlere sahiptir:

- Bir yazar imza birincil imza olmalıdır.
- Birincil bir imza geçerli tek bir zaman damgası olmalıdır.
- X.509 sertifikaları Yazar imza hem de zaman damgası imzası için:
  - 2048 bit RSA ortak anahtarını olmalıdır veya büyük.
  - Paket doğrulaması nuget.org üzerindeki her zaman geçerli UTC saati, geçerlilik süresi içinde olması gerekir.
  - Windows üzerinde varsayılan olarak güvenilen bir güvenilir kök yetkilisi zincir şeklinde olmalıdır. Kendi kendine verilen sertifikalarla imzalanmış paketleri reddedilir.
  - Amacı için geçerli olmalıdır: 
    - İmzalama sertifikası yazar, kod imzalama için geçerli olmalıdır.
    - Zaman damgası sertifika için zaman damgası geçerli olmalıdır.
  - Zaman imzalarken iptal edilmiş olmalıdır değil. (Nuget.org iptal durumunu düzenli aralıklarla yeniden denetler şekilde bu gönderme sırasında knowable olmayabilir).
  
  
## <a name="related-articles"></a>İlgili makaleler

- [NuGet paketlerini imzalama](../create-packages/Sign-a-Package.md)
- [İmzalı paketlerin yüklenmesi](../consume-packages/installing-signed-packages.md)
