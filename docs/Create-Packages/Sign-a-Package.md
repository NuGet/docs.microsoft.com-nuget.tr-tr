---
title: NuGet paketlerini imzalama | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: İmzalı Paketleri açıklar içerik bütünlüğü doğrulamasını etkinleştirmek için kullanılabilir.
keywords: İmzalama, NuGet güvenlik, imzalı paketleri oluşturma NuGet paketi
ms.reviewer:
- karann-msft
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61d90066e8cf75c8f49c7cc9390d45e1cd8afd0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
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
