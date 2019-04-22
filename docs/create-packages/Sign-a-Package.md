---
title: NuGet paketlerini imzalama
description: İmzalı paketlerin açıklar içerik bütünlüğünü doğrulamayı etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 8ff92e5a3ab2d5c13ee02a9e49709866e2ac0e87
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921578"
---
# <a name="signing-nuget-packages"></a>NuGet paketlerini imzalama

İmzalanmış paketleri içerik izinsiz kullanıma karşı koruma sağlayan içerik bütünlüğünü doğrulama denetimleri sağlar. Paket imzası, ayrıca tek gerçek kaynak paketi hakkında doğru kaynağı olarak görev yapar ve paket kimlik doğrulaması için tüketici artırır. Bu kılavuz, zaten sahip olduğunuzu varsayar [bir paket oluşturan](creating-a-package.md).

## <a name="get-a-code-signing-certificate"></a>Bir kod imzalama sertifikası alın

Geçerli sertifikalar elde edilebilir bir ortak sertifika yetkilisinden gibi [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [genel oturum](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).

Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz. Ancak, kendi kendine verilen sertifikaları kullanarak imzalanmış paketleri NuGet.org tarafından kabul edilmez. Daha fazla bilgi edinin [bir test sertifikası oluşturma](#create-a-test-certificate)

## <a name="export-the-certificate-file"></a>Sertifika dosyasını dışarı aktar

* Sertifika Dışarı Aktarma Sihirbazı'nı kullanarak ikili bir DER biçimine var olan bir sertifikayı dışarı aktarabilirsiniz.

  ![Sertifika Dışarı Aktarma Sihirbazı](../reference/media/CertificateExportWizard.png)

* Sertifikayı kullanarak da verebilirsiniz [sertifika dışarı aktarma PowerShell komutunu](/powershell/module/pkiclient/export-certificate).

## <a name="sign-the-package"></a>Paket imzalama

> [!note]
> Nuget.exe 4.6.0 gerektirir veya üzeri

Paket kullanarak oturum [nuget oturum](../tools/cli-ref-sign.md):

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> Sertifika sağlayıcısı için kullanabileceğiniz bir zaman damgası sunucu URL'si genellikle de sağlar. `Timestamper` yukarıdaki isteğe bağlı bağımsız değişkeni göster. Sağlayıcınızın belgeleri ve/veya ilgili hizmet URL'si için destek başvurun.

* Sertifika deposunda mevcut bir sertifikayı kullanın ya da bir dosyadan bir sertifika kullanın. CLI başvuru için bkz. [nuget oturum](../tools/cli-ref-sign.md).
* İmzalanmış paketleri imzalama sertifikasının süresi dolduğunda imzanın geçerli olacağı emin olmak için bir zaman damgasını içermelidir. Oturum işlemi başka oluşturacak bir [uyarı](../reference/errors-and-warnings/NU3002.md).
* Belirtilen paketi kullanarak bir imza ayrıntıları görebilirsiniz [nuget doğrulayın](../tools/cli-ref-verify.md).

## <a name="register-the-certificate-on-nugetorg"></a>NuGet.org sertifikayı kaydetme

İmzalı paket yayımlamak için sertifika NuGet.org ile kaydetmeniz gerekir. Sertifikayı gereken bir `.cer` dosyayı ikili bir DER biçiminde.

1. [Oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org için.
1. Git `Account settings` (veya `Manage Organization` **>** `Edit Organziation` sertifika bir kuruluş hesabı ile kaydetmek isterseniz).
1. Genişletin `Certificates` seçin ve bölüm `Register new`.
1. Göz atma ve daha önce dışarı aktarılan sertifika dosyasını seçin.
  ![Kayıtlı sertifikaları](../reference/media/registered-certs.png)

**Not**
* Bir kullanıcı birden çok sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.
* Bir kullanıcı sonra bir sertifika kayıtlı tüm gelecekteki paket gönderimleri **gerekir** , imzalı bir sertifika. Bkz: [paketinizi nuget.org gereksinimleri imzalama Yönet](#manage-signing-requirements-for-your-package-on-nugetorg)
* Kullanıcılar ayrıca kayıtlı bir sertifika hesaptan kaldırın. Bir sertifika kaldırıldıktan sonra bu sertifika ile imzalanmış yeni paketler gönderimi başarısız olur. Var olan paketleri etkilenmez.

## <a name="publish-the-package"></a>Paket yayımlama

NuGet.org için paket yayımlamak artık hazırsınız. Bkz: [paketleri yayımlama](Publish-a-package.md).

## <a name="create-a-test-certificate"></a>Bir test sertifikası oluştur

Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz. Kendi kendine verilen bir sertifika oluşturmak için kullanın [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate).

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
> Paketleri NuGet.org kabul etmez ile şirket içinde verilen sertifikalara güvenmeyecektir.

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>NuGet.org üzerinde paket imzalama gereksinimlerini yönetme
1. [Oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org için.

1. Git `Manage Packages`  
    ![paket İmzalayanları yapılandırın](../reference/media/configure-package-signers.png)

* Bir paketi tek sahip siz olursunuz, gerekli imzalayan olan herhangi bir kayıtlı sertifikaları imzalamak ve NuGet.org için paket yayımlamasına yani kullanabilirsiniz.

* Bir paket birden çok sahipleri, varsayılan olarak varsa, "Tüm" sahibinin sertifikalar paketi imzalamak için kullanılabilir. Paket bir ortak sahip olarak, kendiniz ile "tümü" ya da gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz. Kayıtlı herhangi bir sertifika yok. bir sahip yaparsanız, işaretsiz paketleri izin verilir. 

* "Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından NuGet.org imzalı bir paket, sahiplerinden biri kayıtlı bir imza ile kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.

## <a name="related-articles"></a>İlgili makaleler

- [İmzalı paketlerin yüklenmesi](../consume-packages/installing-signed-packages.md)
- [İmzalı paket başvurusu](../reference/Signed-Packages-Reference.md)
