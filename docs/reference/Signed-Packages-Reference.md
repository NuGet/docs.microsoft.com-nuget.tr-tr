---
title: İmzalı paketlerin
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c36db9486ad787f19430c75fc38a2e9dd8ba6e37
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550427"
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

## <a name="get-a-code-signing-certificate"></a>Bir kod imzalama sertifikası alın

Geçerli sertifikalar gibi bir ortak sertifika yetkilisinden elde edilebilir:

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [Genel oturum](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

## <a name="create-a-test-certificate"></a>Bir test sertifikası oluştur

Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz. Kendi kendine verilen bir sertifika oluşturmak için kullanın [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate.md).

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

Bu komut, geçerli kullanıcının kişisel sertifika deposunda kullanılabilir bir test sertifikası oluşturur. Sertifika deposu çalıştırarak açabileceğiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.

> [!Warning]
> paketleri nuget.org kabul etmez ile şirket içinde verilen sertifikalara güvenmeyecektir.

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

## <a name="register-certificate-on-nugetorg"></a>Nuget.org sertifikayı kaydetme

İmzalı paket göndermek için bir sertifika ile nuget.org kaydetmeniz gerekir. Sertifikayı gereken bir `.cer` dosyayı ikili bir DER biçiminde. Sertifika Dışarı Aktarma Sihirbazı'nı kullanarak ikili bir DER biçimine var olan bir sertifikayı dışarı aktarabilirsiniz.

![Sertifika Dışarı Aktarma Sihirbazı](media/CertificateExportWizard.png)

İleri düzey kullanıcılar kullanarak sertifikayı dışarı aktarabilir [sertifika dışarı aktarma PowerShell komutunu](/powershell/module/pkiclient/export-certificate.md).

Nuget.org ile sertifikayı kaydetmek için Git `Certificates` bölümünde `Account settings` sayfasında (veya kuruluşun Ayarları sayfası) seçip `Register new certificate`.

![Kayıtlı sertifikaları](media/registered-certs.png)

> [!Tip]
> Bir kullanıcı birden çok sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.

Bir kullanıcı sonra bir sertifika kayıtlı tüm gelecekteki paket gönderimleri **gerekir** , imzalı bir sertifika.

Kullanıcılar ayrıca kayıtlı bir sertifika hesaptan kaldırın. Bir sertifika kaldırıldıktan sonra bu sertifika ile imzalanmış paketleri gönderimi başarısız. Var olan paketleri etkilenmez.

## <a name="configure-package-signing-requirements"></a>Paket imzalama gereksinimlerini yapılandırma

Bir paketi tek sahip siz olursunuz gerekli imzalayan vardır. Diğer bir deyişle, paketlerinizi imzalamak ve nuget.org için göndermek için herhangi bir kayıtlı sertifikaları kullanabilirsiniz.

Bir paket birden çok sahipleri, varsayılan olarak varsa, "Tüm" sahibinin sertifikalar paketi imzalamak için kullanılabilir. Paket bir ortak sahip olarak, kendiniz ile "tümü" ya da gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz. Kayıtlı herhangi bir sertifika yok. bir sahip yaparsanız, işaretsiz paketleri izin verilir. 

"Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından nuget.org imzalı bir paket, sahiplerinden biri kayıtlı bir imza ile kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.

![Paket İmzalayanları yapılandırın](media/configure-package-signers.png)
