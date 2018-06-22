---
title: Paketleri imzalı
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449597"
---
# <a name="signed-packages"></a>İmzalı Paketleri

*NuGet 4.6.0+ ve Visual Studio 2017 15.6 ve sonraki sürümleri*

NuGet paketleri, üzerinde oynanmış içerik karşı koruma sağlayan dijital bir imza içerebilir. Bu imza, ayrıca paket gerçek kaynak için Orijinallik sağlamaları ekler bir X.509 Sertifika oluşturulur.

İmzalı paketleri en güçlü uçtan uca doğrulama sağlar. Bir yazar imzası Yazar paket bağımsız imzalıdan beri'nın paket değiştirilmemiş güvence altına alır, deposu veya ne paket teslim yöntemi taşıma.

Ayrıca, imzalama sertifikasının süresi öncesinde kaydedilmesi gerektiğinden Yazar imzalanan paketleri nuget.org yayımlama ardışık düzeni için ek kimlik doğrulama mekanizması sağlar. Daha fazla bilgi için bkz: [kayıt sertifikaları](#register-certificate-on-nugetorg).

İmzalı paket oluşturma hakkında daha fazla bilgi için bkz: [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).

> [!Important]
> Paket imzalama, şu anda yalnızca nuget.exe Windows kullanıldığında desteklenir. İmzalı paketlerin doğrulama şu anda yalnızca, Windows nuget.exe veya Visual Studio kullanıldığında desteklenir.

## <a name="certificate-requirements"></a>Sertifika gereksinimleri

Paketin imzalanması bir kod imzalama için geçerli olan sertifika bir özel tür sertifikası gerektirir `id-kp-codeSigning` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.

## <a name="get-a-code-signing-certificate"></a>Bir kod imzalama sertifikası alın

Gibi bir ortak sertifika yetkilisinden geçerli sertifikalar alınabilir:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Daddy gidin](https://www.godaddy.com/web-security/code-signing-certificate)
- [Genel oturum](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Bir test sertifikası oluşturma

Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz. Kendi kendine verilen bir sertifika oluşturmak için kullanmak [yeni SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

> [!Warning]
> nuget.org paketleri kabul etmiyor kendi kendine verilen sertifikaları ile imzalanmış.

## <a name="timestamp-requirements"></a>Zaman damgası gereksinimleri

İmzalı Paketleri sertifikanın geçerlilik süresi imzalama paket ötesinde imza doğruluğundan emin olmak için bir RFC 3161 zaman damgası içermelidir. Zaman damgası imzalamak için kullanılan sertifikanın geçerli `id-kp-timeStamping` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]. Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.

Ek teknik ayrıntılar bulunabilir [imza teknik belirtimlerin paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).

## <a name="signature-requirements-on-nugetorg"></a>Nuget.org imza gereksinimleri

nuget.org imzalı bir paket kabul etmek için ek gereksinimler vardır:

- Birincil imza Yazar imza olması gerekir.
- Birincil imza geçerli tek bir zaman damgası olmalıdır.
- X.509 sertifikaları Yazar imza ve zaman damgası imzası için:
  - Bir RSA ortak anahtar 2048 bit olmalıdır veya daha büyük.
  - Paket doğrulama nuget.org üzerinde her zaman geçerli UTC saati, geçerlilik süresi içinde olmalıdır.
  - Windows üzerinde varsayılan olarak güvenilen bir güvenilir kök yetkilisi zincir gerekir. Kendi kendine verilen sertifikalarla imzalanan paketleri reddedilir.
  - Amacı için geçerli olmalıdır: 
    - Sertifika imzalama yazar kod imzalama için geçerli olmalıdır.
    - Zaman damgası sertifika için zaman damgası geçerli olmalıdır.
  - Zaman imzalarken iptal edilmiş olmalıdır değil. (Nuget.org iptal durumunu düzenli aralıklarla yeniden denetler şekilde bu gönderimi zamanında knowable olmayabilir).

## <a name="register-certificate-on-nugetorg"></a>Nuget.org sertifikayı kaydetme

İmzalı bir paket göndermek için önce sertifika nuget.org ile kaydetmeniz gerekir. Sertifikası olarak gereken bir `.cer` ikili DER biçimi dosyasında. Sertifika Verme Sihirbazı'nı kullanarak bir ikili DER biçimine varolan bir sertifikayı dışarı aktarabilirsiniz.

![Sertifika Verme Sihirbazı](media/CertificateExportWizard.png)

İleri düzey kullanıcılar, sertifikayı kullanarak verebilirsiniz [sertifika verme PowerShell komutunu](/powershell/module/pkiclient/export-certificate.md).

Sertifika nuget.org ile kaydetmek için Git `Certificates` bölümünde `Account settings` (veya kuruluş ayarları sayfasını) seçip `Register new certificate`.

![Kayıtlı sertifikaları](media/registered-certs.png)

> [!Tip]
> Bir kullanıcı birden fazla sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.

Bir kullanıcının bir kez bir sertifika kayıtlı tüm gelecekteki paket gönderileri **gerekir** , imzalanmış bir sertifika.

Kullanıcılar ayrıca hesabından kayıtlı sertifika kaldırabilirsiniz. Bir sertifika kaldırıldıktan sonra bu sertifikayla imzalanan paketleri gönderimi başarısız. Mevcut paketleri etkilenmez.

## <a name="configure-package-signing-requirements"></a>Paket imzalama gereksinimlerini yapılandırma

Bir paketi tek sahibiyseniz, gerekli imzalayan demektir. Diğer bir deyişle, tüm kayıtlı sertifikaları paketlerinizi imzalamak ve nuget.org için göndermek için kullanabilirsiniz.

Bir paketi varsayılan olarak birden çok sahipleri, varsa, "Herhangi" sahibinin sertifikalar paketi imzalamak için kullanılabilir. Paket ortak sahibi olarak, "Tüm" kendiniz veya gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz. Kayıtlı herhangi bir sertifika yok bir sahibi yaparsanız, imzasız paketleri izin verilir. 

"Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından nuget.org imzalı bir paket sahiplerinden biri kayıtlı imzayla kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.

![Paket İmzalayanları yapılandırın](media/configure-package-signers.png)
