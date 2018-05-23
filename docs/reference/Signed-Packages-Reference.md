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
---
# <a name="signed-packages"></a><span data-ttu-id="56329-103">İmzalı Paketleri</span><span class="sxs-lookup"><span data-stu-id="56329-103">Signed packages</span></span>

<span data-ttu-id="56329-104">*NuGet 4.6.0+ ve Visual Studio 2017 15.6 ve sonraki sürümleri*</span><span class="sxs-lookup"><span data-stu-id="56329-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="56329-105">NuGet paketleri, üzerinde oynanmış içerik karşı koruma sağlayan dijital bir imza içerebilir.</span><span class="sxs-lookup"><span data-stu-id="56329-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="56329-106">Bu imza, ayrıca paket gerçek kaynak için Orijinallik sağlamaları ekler bir X.509 Sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="56329-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="56329-107">İmzalı paketleri en güçlü uçtan uca doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="56329-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="56329-108">Bir yazar imzası Yazar paket bağımsız imzalıdan beri'nın paket değiştirilmemiş güvence altına alır, deposu veya ne paket teslim yöntemi taşıma.</span><span class="sxs-lookup"><span data-stu-id="56329-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="56329-109">Ayrıca, imzalama sertifikasının süresi öncesinde kaydedilmesi gerektiğinden Yazar imzalanan paketleri nuget.org yayımlama ardışık düzeni için ek kimlik doğrulama mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="56329-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="56329-110">Daha fazla bilgi için bkz: [kayıt sertifikaları](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="56329-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="56329-111">İmzalı paket oluşturma hakkında daha fazla bilgi için bkz: [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="56329-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="56329-112">Paket imzalama, şu anda yalnızca nuget.exe Windows kullanıldığında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="56329-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="56329-113">İmzalı paketlerin doğrulama şu anda yalnızca, Windows nuget.exe veya Visual Studio kullanıldığında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="56329-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="56329-114">Sertifika gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="56329-114">Certificate requirements</span></span>

<span data-ttu-id="56329-115">Paketin imzalanması bir kod imzalama için geçerli olan sertifika bir özel tür sertifikası gerektirir `id-kp-codeSigning` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="56329-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="56329-116">Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56329-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="56329-117">Bir kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="56329-117">Get a code signing certificate</span></span>

<span data-ttu-id="56329-118">Gibi bir ortak sertifika yetkilisinden geçerli sertifikalar alınabilir:</span><span class="sxs-lookup"><span data-stu-id="56329-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="56329-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="56329-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="56329-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="56329-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="56329-121">Daddy gidin</span><span class="sxs-lookup"><span data-stu-id="56329-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="56329-122">Genel oturum</span><span class="sxs-lookup"><span data-stu-id="56329-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="56329-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="56329-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="56329-124">Certum</span><span class="sxs-lookup"><span data-stu-id="56329-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="56329-125">Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="56329-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="56329-126">Bir test sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="56329-126">Create a test certificate</span></span>

<span data-ttu-id="56329-127">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56329-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="56329-128">Kendi kendine verilen bir sertifika oluşturmak için kullanmak [yeni SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="56329-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="56329-129">Bu komut, geçerli kullanıcının kişisel sertifika deposunda bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="56329-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="56329-130">Sertifika deposu çalıştırarak açabilirsiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.</span><span class="sxs-lookup"><span data-stu-id="56329-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="56329-131">nuget.org paketleri kabul etmiyor kendi kendine verilen sertifikaları ile imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="56329-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="56329-132">Zaman damgası gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="56329-132">Timestamp requirements</span></span>

<span data-ttu-id="56329-133">İmzalı Paketleri sertifikanın geçerlilik süresi imzalama paket ötesinde imza doğruluğundan emin olmak için bir RFC 3161 zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="56329-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="56329-134">Zaman damgası imzalamak için kullanılan sertifikanın geçerli `id-kp-timeStamping` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="56329-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="56329-135">Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56329-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="56329-136">Ek teknik ayrıntılar bulunabilir [imza teknik belirtimlerin paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="56329-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="56329-137">Nuget.org imza gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="56329-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="56329-138">nuget.org imzalı bir paket kabul etmek için ek gereksinimler vardır:</span><span class="sxs-lookup"><span data-stu-id="56329-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="56329-139">Birincil imza Yazar imza olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="56329-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="56329-140">Birincil imza geçerli tek bir zaman damgası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56329-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="56329-141">X.509 sertifikaları Yazar imza ve zaman damgası imzası için:</span><span class="sxs-lookup"><span data-stu-id="56329-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="56329-142">Bir RSA ortak anahtar 2048 bit olmalıdır veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="56329-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="56329-143">Paket doğrulama nuget.org üzerinde her zaman geçerli UTC saati, geçerlilik süresi içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56329-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="56329-144">Windows üzerinde varsayılan olarak güvenilen bir güvenilir kök yetkilisi zincir gerekir.</span><span class="sxs-lookup"><span data-stu-id="56329-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="56329-145">Kendi kendine verilen sertifikalarla imzalanan paketleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="56329-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="56329-146">Amacı için geçerli olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="56329-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="56329-147">Sertifika imzalama yazar kod imzalama için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56329-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="56329-148">Zaman damgası sertifika için zaman damgası geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="56329-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="56329-149">Zaman imzalarken iptal edilmiş olmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="56329-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="56329-150">(Nuget.org iptal durumunu düzenli aralıklarla yeniden denetler şekilde bu gönderimi zamanında knowable olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="56329-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="56329-151">Nuget.org sertifikayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="56329-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="56329-152">İmzalı bir paket göndermek için önce sertifika nuget.org ile kaydetmeniz gerekir. Sertifikası olarak gereken bir `.cer` ikili DER biçimi dosyasında.</span><span class="sxs-lookup"><span data-stu-id="56329-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="56329-153">Sertifika Verme Sihirbazı'nı kullanarak bir ikili DER biçimine varolan bir sertifikayı dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56329-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Sertifika Verme Sihirbazı](media/CertificateExportWizard.png)

<span data-ttu-id="56329-155">İleri düzey kullanıcılar, sertifikayı kullanarak verebilirsiniz [sertifika verme PowerShell komutunu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="56329-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="56329-156">Sertifika nuget.org ile kaydetmek için Git `Certificates` bölümünde `Account settings` (veya kuruluş ayarları sayfasını) seçip `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="56329-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Kayıtlı sertifikaları](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="56329-158">Bir kullanıcı birden fazla sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56329-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="56329-159">Bir kullanıcının bir kez bir sertifika kayıtlı tüm gelecekteki paket gönderileri **gerekir** , imzalanmış bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="56329-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="56329-160">Kullanıcılar ayrıca hesabından kayıtlı sertifika kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56329-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="56329-161">Bir sertifika kaldırıldıktan sonra bu sertifikayla imzalanan paketleri gönderimi başarısız.</span><span class="sxs-lookup"><span data-stu-id="56329-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="56329-162">Mevcut paketleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="56329-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="56329-163">Paket imzalama gereksinimlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="56329-163">Configure package signing requirements</span></span>

<span data-ttu-id="56329-164">Bir paketi tek sahibiyseniz, gerekli imzalayan demektir.</span><span class="sxs-lookup"><span data-stu-id="56329-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="56329-165">Diğer bir deyişle, tüm kayıtlı sertifikaları paketlerinizi imzalamak ve nuget.org için göndermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56329-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="56329-166">Bir paketi varsayılan olarak birden çok sahipleri, varsa, "Herhangi" sahibinin sertifikalar paketi imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="56329-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="56329-167">Paket ortak sahibi olarak, "Tüm" kendiniz veya gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="56329-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="56329-168">Kayıtlı herhangi bir sertifika yok bir sahibi yaparsanız, imzasız paketleri izin verilir.</span><span class="sxs-lookup"><span data-stu-id="56329-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="56329-169">"Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından nuget.org imzalı bir paket sahiplerinden biri kayıtlı imzayla kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.</span><span class="sxs-lookup"><span data-stu-id="56329-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Paket İmzalayanları yapılandırın](media/configure-package-signers.png)
