---
title: NuGet Paketlerini İmzalama
description: İmzalı paketlerin içerik bütünlüğü doğrulamasını etkinleştirmek için nasıl kullanılabileceğini açıklar.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429005"
---
# <a name="signing-nuget-packages"></a>NuGet Paketlerini İmzalama

İmzalı paketler, içerik tahrifatına karşı koruma sağlayan içerik bütünlüğü doğrulama denetimlerine izin verir. Paket imzası aynı zamanda paketin gerçek kökeni hakkında tek bir doğruluk kaynağı olarak hizmet vermektedir ve tüketici için paket orijinalliğini destekler. Bu kılavuz, zaten [bir paket oluşturduğunuzu](creating-a-package.md)varsayar.

## <a name="get-a-code-signing-certificate"></a>Kod imzalama sertifikası alma

Geçerli sertifikalar [Symantec,](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3) [DigiCert,](https://www.digicert.com/code-signing/) [Go Daddy,](https://www.godaddy.com/web-security/code-signing-certificate) [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo,](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php) [Certum,](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. gibi bir kamu sertifika yetkilisinden alınabilir. Windows tarafından güvenilen sertifika yetkililerinin tam [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)listesi.

Kendi kendine verilen sertifikaları sınama amacıyla kullanabilirsiniz. Ancak, kendi kendine verilen sertifikalar kullanılarak imzalanan paketler NuGet.org tarafından kabul edilmez. [Test sertifikası oluşturma](#create-a-test-certificate) hakkında daha fazla bilgi edinin

## <a name="export-the-certificate-file"></a>Sertifika dosyasını dışa aktarma

* Varolan bir sertifikayı Sertifika Dışa Aktarma Sihirbazı'nı kullanarak ikili DER biçimine dışa aktarabilirsiniz.

  ![Sertifika Verme Sihirbazı](../reference/media/CertificateExportWizard.png)

* Ayrıca [Dışa Aktarma Sertifikası PowerShell komutunu](/powershell/module/pkiclient/export-certificate)kullanarak sertifikayı dışa aktarabilirsiniz.

## <a name="sign-the-package"></a>Paketi imzalayın

> [!note]
> nuget.exe 4.6.0 veya sonrası gerektirir. dotnet.exe desteği yakında geliyor - [#7939](https://github.com/NuGet/Home/issues/7939)

[Nuget işaretini](../reference/cli-reference/cli-ref-sign.md)kullanarak paketi imzalayın:

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Sertifika sağlayıcısı genellikle yukarıda belirtilen `Timestamper` isteğe bağlı bağımsız değişken için kullanabileceğiniz bir zaman damgası sunucusu URL'si de sağlar. Sağlayıcınızın bu hizmet URL'si için belgelerine ve/veya desteğine danışın.

* Sertifika deposunda bulunan bir sertifikayı kullanabilir veya bir dosyadan sertifika kullanabilirsiniz. [Nuget işareti](../reference/cli-reference/cli-ref-sign.md)için CLI başvurusuna bakın.
* İmzalanan paketler, imza sertifikasının süresi dolduğunda imzanın geçerli kalmasını sağlamak için bir zaman damgası içermelidir. Aksi takdirde işaret işlemi bir [uyarı](../reference/errors-and-warnings/NU3002.md)üretecek.
* Nuget [doğrulamak](../reference/cli-reference/cli-ref-verify.md)kullanarak belirli bir paketin imza ayrıntılarını görebilirsiniz.

## <a name="register-the-certificate-on-nugetorg"></a>Sertifikayı NuGet.org kaydedin

İmzalı bir paketi yayımlamak için önce sertifikayı NuGet.org kaydettirmelisiniz. Sertifikayı ikili DER `.cer` formatında bir dosya olarak almanız gerekir.

1. NuGet.org [oturum açın.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)
1. Gidin `Account settings` (veya `Manage Organization` **>** `Edit Organziation` sertifikayı bir Kuruluş hesabına kaydettirmek istiyorsanız).
1. Bölümü `Certificates` genişletin `Register new`ve seçin.
1. Daha önce dışa aktarılan sertifika dosyasına göz atın ve seçin.
  ![Kayıtlı Sertifikalar](../reference/media/registered-certs.png)

**Not**
* Bir kullanıcı birden çok sertifika gönderebilir ve aynı sertifika birden çok kullanıcı tarafından kaydedilebilir.
* Bir kullanıcı bir sertifikayı kaydettikten sonra, gelecekteki tüm paket gönderimlerinin sertifikalardan biriyle imzalanması **gerekir.** Bkz. [NuGet.org paketiniz için imza gereksinimlerini yönetin](#manage-signing-requirements-for-your-package-on-nugetorg)
* Kullanıcılar kayıtlı bir sertifikayı da hesaptan kaldırabilir. Sertifika kaldırıldıktan sonra, bu sertifikayla imzalanan yeni paketler gönderimsırasında başarısız olur. Varolan paketler etkilenmez.

## <a name="publish-the-package"></a>Paketi yayımlama

Paketi NuGet.org yayınlamaya hazırsınız. Bkz. [Yayımlama paketleri.](../nuget-org/Publish-a-package.md)

## <a name="create-a-test-certificate"></a>Test sertifikası oluşturma

Kendi kendine verilen sertifikaları sınama amacıyla kullanabilirsiniz. Kendi kendine verilen bir sertifika oluşturmak için [Yeni İmzalı Sertifika PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate)kullanın.

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

Bu komut, geçerli kullanıcının kişisel sertifika deposunda kullanılabilen bir sınama sertifikası oluşturur. Yeni oluşturulan sertifikayı görmek `certmgr.msc` için çalıştırarak sertifika mağazasını açabilirsiniz.

> [!Warning]
> NuGet.org, kendi kendine verilen sertifikalarla imzalanmış paketleri kabul etmez.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>Paketiniz için imza gereksinimlerini NuGet.org
1. NuGet.org [oturum açın.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)

1. Paket `Manage Packages`  
    ![imzalayanları yapılandırmaya git](../reference/media/configure-package-signers.png)

* Bir paketin tek sahibisizseniz, gerekli imzalayan sizsiniz, yani paketlerinizi imzalamak ve NuGet.org yayınlamak için kayıtlı sertifikalardan herhangi birini kullanabilirsiniz.

* Bir paketin birden çok sahibi varsa, varsayılan olarak, paketi imzalamak için "Herhangi bir" sahibinin sertifikaları kullanılabilir. Paketin ortaklarından biri olarak, gerekli imzalayan kişi olmak için kendiniz veya başka bir ortak sahibiile "Any"yi geçersiz kılabilirsiniz. Kayıtlı sertifikası olmayan bir sahip yaparsanız, imzasız paketlere izin verilir. 

* Benzer şekilde, bir sahibin sertifikasının kayıtlı olduğu ve başka bir sahibinin kayıtlı sertifikası nın olmadığı bir paket için varsayılan "Herhangi bir" seçeneği seçilirse, NuGet.org, sahiplerinden biri tarafından kaydedilmiş imzalı bir paketi veya imzasız paketi kabul eder (çünkü sahiplerden birinin kayıtlı sertifikası yoktur).

## <a name="related-articles"></a>İlgili makaleler:

- [Paket güven sınırlarını yönetme](../consume-packages/installing-signed-packages.md)
- [İmzalı Paketler Referans](../reference/Signed-Packages-Reference.md)
