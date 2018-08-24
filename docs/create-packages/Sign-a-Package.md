---
title: NuGet paketlerini imzalama
description: İmzalı paketlerin açıklar içerik bütünlüğünü doğrulamayı etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793586"
---
# <a name="signing-nuget-packages"></a>NuGet paketlerini imzalama

Paket imzalama paket oluşturulduktan sonra değiştirilmediğinden emin yapan bir işlemdir.

## <a name="prerequisites"></a>Önkoşullar

1. Paket (bir `.nupkg` dosya) oturum açmak için. Bkz: [paket oluşturma](creating-a-package.md).

1. nuget.exe 4.6.0 veya üzeri. Bkz. nasıl [NuGet CLI'yı yükleme](../install-nuget-client-tools.md#nugetexe-cli).

1. [Bir kod imzalama sertifikası](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>Bir paket imzalama

Bir paketi imzalamak için kullanmak [nuget oturum](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Komut Başvurusu içinde açıklandığı gibi sertifika deposunda mevcut bir sertifika kullanın ya da bir dosyadan bir sertifika kullanın.

### <a name="common-problems-when-signing-a-package"></a>Paket imzalama karşılaşılan yaygın sorunlar

- Sertifika, kod imzalama için geçerli değil. Belirtilen sertifika genişletilmiş anahtar kullanımı (EKU 1.3.6.1.5.5.7.3.3) uygun olan emin olmanız gerekir.
- Sertifika anahtar 2048 bit RSA SHA-256'yı imza algoritması veya bir genel gibi temel gereksinimleri karşılamadığı veya büyük.
- Sertifikanın süresi doldu veya iptal edildi.
- Zaman damgası sunucusu, sertifika gereksinimleri karşılamıyor.

> [!Note]
> İmzalanmış paketleri imzalama sertifikasının süresi dolduğunda imzanın geçerli olacağı emin olmak için bir zaman damgasını içermelidir. Oturum işlemi üreten bir [NU3002 uyarı](../reference/errors-and-warnings/NU3002.md) bir zaman damgası oturum açarken.

## <a name="verify-a-signed-package"></a>İmzalı paket doğrulayın

Kullanım [nuget doğrulayın](../tools/cli-ref-verify.md) belirli bir paket imza ayrıntılarını görmek için:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>İmzalı paket yükleme

İmzalı paketlerin yüklenmesi için herhangi bir özel işlem gerektirmez; Ancak, içeriği imzalandıktan sonra değiştirilmiş, yükleme engellenir ve üreten bir [hata NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Güvenilmeyen Sertifikalar ile imzalanmış paketleri olarak kabul edilir olarak imzalanmamış ve uyarıları veya hataları gibi diğer herhangi bir işaretsiz paket olmadan yüklenir.

## <a name="see-also"></a>Ayrıca bkz.

[İmzalı paket başvurusu](../reference/Signed-Packages-Reference.md)
