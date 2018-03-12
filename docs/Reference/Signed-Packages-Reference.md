---
title: "Paketleri başvuru imzalı | Microsoft Docs"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Paketleri özellik açıklaması imzalanmış."
keywords: "NuGet paket oturum, imza sertifikası"
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4763b0dde0153f9e8ea840d5e788b5a3d96b9bd8
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="signed-packages"></a>İmzalı Paketleri

*NuGet 4.6.0+ ve Visual Studio 2017 15.6 ve sonraki sürümleri*

NuGet paketleri, üzerinde oynanmış içerik karşı koruma sağlayan dijital bir imza içerebilir. Bu imza, ayrıca paket gerçek kaynak için Orijinallik sağlamaları ekler bir X.509 Sertifika oluşturulur.

İmzalı paketleri en güçlü uçtan uca doğrulama sağlar. Bir yazar imzası Yazar paket bağımsız imzalıdan beri'nın paket değiştirilmemiş güvence altına alır, deposu veya ne paket teslim yöntemi taşıma.

Kilitli ortamında talep tüketiciler belirli yazarının sertifikayla imzalanan paketleri gerektirebilir.

Ayrıca, imzalama sertifikasının süresi öncesinde kaydedilmesi gerektiğinden Yazar imzalanan paketleri nuget.org yayımlama ardışık düzeni için ek kimlik doğrulama mekanizması sağlar.

İmzalı paket oluşturma hakkında daha fazla bilgi için bkz: [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).

> [!Important]
> nuget.org imzalı paketleri şu anda kabul etmiyor. Paketleri yayımlama özel akışları için oturum açabilirsiniz.

## <a name="certificate-requirements"></a>Sertifika gereksinimleri

Paketin imzalanması bir kod imzalama için geçerli olan sertifika bir özel tür sertifikası gerektirir `id-kp-codeSigning` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.

## <a name="get-a-code-signing-certificate"></a>Bir kod imzalama sertifikası alın

Geçerli sertifikalar gibi ortak sertifika yetkililerinden alınabilir:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Genel oturum](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Bir test sertifikası oluşturma

Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz. Kendi kendine verilen bir sertifika oluşturmak için kullanmak [yeni SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell komutu.

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

Bu komut, geçerli kullanıcının kişisel sertifika deposunda bir test sertifikası oluşturur. Sertifika deposu çalıştırarak açabilirsiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.

## <a name="timestamp-requirements"></a>Zaman damgası gereksinimleri

İmzalı Paketleri sertifikanın geçerlilik süresi imzalama paket ötesinde imza doğruluğundan emin olmak için bir RFC 3161 zaman damgası içermelidir. Zaman damgası imzalamak için kullanılan sertifikanın geçerli `id-kp-timeStamping` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.

Ek teknik ayrıntılar bulunabilir [imza teknik belirtimlerin paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).
