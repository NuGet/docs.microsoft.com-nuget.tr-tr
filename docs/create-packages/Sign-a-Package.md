---
title: NuGet paketleri imzalanıyor
description: İmzalanan paketlerin, içerik bütünlüğü doğrulamasını etkinleştirmek için nasıl kullanılabileceğini açıklar.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 64b28c29ae3b533bde7c8f41dd38a4ab0a5afef7
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550381"
---
# <a name="signing-nuget-packages"></a>NuGet paketleri imzalanıyor

İmzalı paketler, içerik değişikliklere karşı koruma sağlayan içerik bütünlüğü doğrulama denetimleri sağlar. Paket imzası Ayrıca paketin gerçek kaynağı ve tüketicinin paket özgünlük değeri hakkında tek bir kaynak kaynağı görevi görür. Bu kılavuzda zaten [bir paket oluşturmuş](creating-a-package.md)olduğunuz varsayılmaktadır.

## <a name="get-a-code-signing-certificate"></a>Kod imzalama sertifikası alın

Geçerli sertifikalar [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. gibi bir genel sertifika yetkilisinden elde edilebilir. Windows tarafından güvenilen sertifika yetkililerinin tüm listesi, adresinden elde edilebilir [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .

Test amaçlı olarak, kendi kendine verilen sertifikaları kullanabilirsiniz. Ancak, otomatik olarak verilen sertifikalar kullanılarak imzalanmış paketler NuGet.org tarafından kabul edilmez. [Test sertifikası oluşturma](#create-a-test-certificate) hakkında daha fazla bilgi edinin

## <a name="export-the-certificate-file"></a>Sertifika dosyasını dışarı aktarma

* Sertifika Dışarı Aktarma Sihirbazı 'nı kullanarak, var olan bir sertifikayı ikili DER biçimine aktarabilirsiniz.

  ![Sertifika Dışarı Aktarma Sihirbazı](../reference/media/CertificateExportWizard.png)

* Sertifikayı [dışarı aktar-sertifika PowerShell komutunu](/powershell/module/pkiclient/export-certificate)kullanarak da dışa aktarabilirsiniz.

## <a name="sign-the-package"></a>Paketi imzala

> [!note]
> nuget.exe 4.6.0 veya üstünü gerektirir. dotnet.exe destek yakında kullanıma sunulacak [#7939](https://github.com/NuGet/Home/issues/7939)

[NuGet işaretini](../reference/cli-reference/cli-ref-sign.md)kullanarak paketi imzala:

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Sertifika sağlayıcısı çoğunlukla, `Timestamper` yukarıda görüntülenecek isteğe bağlı bağımsız değişken için kullanabileceğiniz bir zaman damgası sunucu URL 'si de sağlar. Sağlayıcının belgelerine ve/veya bu hizmet URL 'sine yönelik desteğe başvurun.

* Sertifika deposunda bulunan bir sertifikayı kullanabilir veya bir dosyadaki sertifikayı kullanabilirsiniz. [NuGet işareti](../reference/cli-reference/cli-ref-sign.md)için CLI başvurusuna bakın.
* İmzalı paketler, imzalama sertifikasının süresi dolduğunda imzanın geçerli kaldığından emin olmak için bir zaman damgası içermelidir. Aksi takdirde imza işlemi bir [Uyarı](../reference/errors-and-warnings/NU3002.md)üretir.
* [NuGet doğrulaması](../reference/cli-reference/cli-ref-verify.md)' nı kullanarak belirli bir paketin imza ayrıntılarını görebilirsiniz.

## <a name="register-the-certificate-on-nugetorg"></a>Sertifikayı NuGet.org 'e kaydetme

İmzalı bir paket yayımlamak için öncelikle sertifikayı NuGet.org ile kaydetmeniz gerekir. Bir ikili DER biçiminde bir dosya olarak sertifikaya ihtiyacınız vardır `.cer` .

1. NuGet.org ['de oturum açın](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .
1. `Account settings`(Veya `Manage Organization` **>** `Edit Organization` sertifikayı bir kuruluş hesabıyla kaydetmek istiyorsanız) bölümüne gidin.
1. Bölümünü genişletin `Certificates` ve öğesini seçin `Register new` .
1. Daha önce aktarılmış olan sertifika dosyasına gidip seçin.
  ![Kayıtlı sertifikalar](../reference/media/registered-certs.png)

**Not**
* Bir Kullanıcı birden çok sertifika gönderebilir ve aynı sertifika birden çok kullanıcı tarafından kaydedilebilir.
* Bir Kullanıcı bir sertifikaya kaydolduktan sonra, gelecekteki tüm paket gönderimlerinin sertifikalardan biri ile imzalanması **gerekir** . Bkz. [NuGet.org 'de paketiniz için imzalama gereksinimlerini yönetme](#manage-signing-requirements-for-your-package-on-nugetorg)
* Kullanıcılar ayrıca, kayıtlı bir sertifikayı hesaptan kaldırabilir. Bir sertifika kaldırıldıktan sonra, bu sertifikayla imzalanmış yeni paketler gönderim sırasında başarısız olur. Mevcut paketler etkilenmemektedir.

## <a name="publish-the-package"></a>Paketi Yayımla

Artık paketi NuGet.org 'e yayımlamaya hazırsınız. Bkz. [paketleri yayımlama](../nuget-org/Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Test sertifikası oluşturma

Test amaçlı olarak, kendi kendine verilen sertifikaları kullanabilirsiniz. Kendi kendine verilen bir sertifika oluşturmak için [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate)kullanın.

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

Bu komut, geçerli kullanıcının kişisel sertifika deposunda bulunan bir test sertifikası oluşturur. `certmgr.msc`Yeni oluşturulan sertifikayı görmek için, çalıştırarak sertifika deposunu açabilirsiniz.

> [!Warning]
> NuGet.org, otomatik olarak verilen sertifikalarla imzalanmış paketleri kabul etmez.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>NuGet.org 'de paketiniz için imzalama gereksinimlerini yönetme
1. NuGet.org ['de oturum açın](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .

1. `Manage Packages`  
    ![ Paket İmzalayanları yapılandırma bölümüne git](../reference/media/configure-package-signers.png)

* Bir paketin tek sahibiyseniz, gerekli olan imzalamanıza karşı, paketlerinizi imzalamak ve NuGet.org 'e yayımlamak için kayıtlı sertifikalardan herhangi birini kullanabilirsiniz.

* Bir paketin birden çok sahibi varsa, varsayılan olarak "Any" sahibinin sertifikaları paketi imzalamak için kullanılabilir. Paketin ortak sahibi olarak, "Any" i veya diğer tüm ikincil sahiplerle gerekli imzacı olacak şekilde geçersiz kılabilirsiniz. Kayıtlı bir sertifikası olmayan bir sahip yaparsanız, imzasız paketlere izin verilir. 

* Benzer şekilde, bir sahibin kayıtlı bir sertifikası olan bir paket için varsayılan "Any" seçeneği seçilmişse ve başka bir sahibe kayıtlı bir sertifika yoksa, NuGet.org, sahip olduğu imzalı bir paketi veya bir imzasız paketi kabul eder (sahiplerden birinde kayıtlı sertifika olmadığından).

## <a name="related-articles"></a>İlgili makaleler:

- [Paket güven sınırlarını yönetme](../consume-packages/installing-signed-packages.md)
- [İmzalı paket başvurusu](../reference/Signed-Packages-Reference.md)