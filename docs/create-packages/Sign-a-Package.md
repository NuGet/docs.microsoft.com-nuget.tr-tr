---
title: NuGet paketlerini imzalama
description: İmzalı Paketleri açıklar içerik bütünlüğü doğrulamasını etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a>NuGet paketlerini imzalama

Paket imzalama paket oluşturulduktan sonra değiştirilmediğinden emin yapan bir işlemdir.

## <a name="prerequisites"></a>Önkoşullar

1. Paketi (bir `.nupkg` dosyası) imzalamak için. Bkz: [paket oluşturma](creating-a-package.md).

1. nuget.exe 4.6.0 veya sonraki bir sürümü. Bkz: nasıl yapılır [NuGet CLI'yı yükleme](../install-nuget-client-tools.md#nugetexe-cli).

1. [Bir kod imzalama sertifikası](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

> [!Warning]
> nuget.org imzalı paketleri şu anda kabul etmiyor. Paketleri yayımlama özel akışları için oturum açabilirsiniz.

## <a name="sign-a-package"></a>Bir paket imzalama

Bir paketi imzalamak için kullanın [nuget oturum](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

Komut Başvurusu'nda açıklandığı gibi sertifika deposunda mevcut bir sertifika kullanmak ya da bir dosyadan bir sertifika kullanın.

### <a name="common-problems-when-signing-a-package"></a>Paket imzalama genel sorunlar

- Sertifika, kod imzalama için geçerli değil. Genişletilmiş Anahtar Kullanımı (EKU 1.3.6.1.5.5.7.3.3) belirtilen sertifika uygun sahip olmanız gerekir.
- Sertifika anahtar 2048 bit RSA SHA-256 imza algoritması ya da bir ortak gibi temel gereksinimleri karşılamadığı veya daha büyük.
- Sertifikanın süresi doldu veya iptal edildi.
- Zaman damgası sunucusu sertifika gereksinimlerini karşılamıyor.

> [!Note]
> İmzalı Paketleri imzalama sertifikasının süresi dolan imza geçerli kaldığı emin olmak için bir zaman damgası içermelidir. Oturum işlemi üreten bir [NU3002 uyarı](../reference/Errors-and-Warnings.md#nu3002) bir zaman damgası imzalarken.

## <a name="verify-a-signed-package"></a>İmzalı bir paket doğrulayın

Kullanım [nuget doğrulayın](../tools/cli-ref-verify.md) belirli bir paket imza ayrıntılarını görmek için:

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>İmzalı paketini yükle

İmzalı Paketleri yüklenmesi için belirli bir işlem gerekmez; İçerik imzalandığından bu yana değiştirildi, ancak yükleme olması bloke ve üreten bir [hata NU3008](../reference/Errors-and-Warnings.md#nu3008).

> [!Warning]
> Güvenilmeyen Sertifikalar ile imzalanan paketleri olarak kabul edilir olarak imzalanmamış ve uyarı veya hata imzasız herhangi bir paket gibi olmadan yüklenir.

## <a name="see-also"></a>Ayrıca bkz.

[Paketleri başvuru imzalı](../reference/Signed-Packages-Reference.md)
