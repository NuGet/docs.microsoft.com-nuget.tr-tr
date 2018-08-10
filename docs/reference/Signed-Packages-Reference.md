---
title: İmzalı paketlerin
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020524"
---
# <a name="signed-packages"></a><span data-ttu-id="3d92f-103">İmzalanmış paketleri</span><span class="sxs-lookup"><span data-stu-id="3d92f-103">Signed packages</span></span>

<span data-ttu-id="3d92f-104">*NuGet 4.6.0+ ve Visual Studio 2017 sürüm 15.6 ve üzeri*</span><span class="sxs-lookup"><span data-stu-id="3d92f-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="3d92f-105">NuGet paketlerini, üzerinde oynanmış bir içerik karşı koruma sağlayan dijital bir imza içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="3d92f-106">Bu imza de gerçek paket kaynağı için kimlik doğrulaması kanıtları ekleyen bir X.509 Sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3d92f-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="3d92f-107">İmzalanmış paketleri güçlü bir uçtan uca doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d92f-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="3d92f-108">NuGet imzaları iki farklı tür vardır:</span><span class="sxs-lookup"><span data-stu-id="3d92f-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="3d92f-109">**Yazar imza**.</span><span class="sxs-lookup"><span data-stu-id="3d92f-109">**Author Signature**.</span></span> <span data-ttu-id="3d92f-110">Bir yazar imzası yazarı paketin olursa olsun gelen upraven'ın paket değiştirilmedi garanti eder, depo veya ne paket teslim yöntemi taşıma.</span><span class="sxs-lookup"><span data-stu-id="3d92f-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="3d92f-111">Ayrıca, imzalama sertifikasının önceden kayıtlı olması gerekir çünkü Yazar imzalanmış paketleri nuget.org yayımlama işlem hattı için ek kimlik doğrulama mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d92f-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="3d92f-112">Daha fazla bilgi için [kayıt sertifikaları](#register-certificate-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="3d92f-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="3d92f-113">**Depo imza**.</span><span class="sxs-lookup"><span data-stu-id="3d92f-113">**Repository Signature**.</span></span> <span data-ttu-id="3d92f-114">Depo imzaları sağlamak için bir bütünlük garantisi **tüm** bile bu paketleri nerede oldukları özgün deposu farklı bir konumdan elde edilen yazar, imzalanmış olup bir depoda paketleri imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="3d92f-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="3d92f-115">Bir yazar imzalı paket oluşturma hakkında daha fazla bilgi edinmek için bkz. [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="3d92f-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="3d92f-116">Paket imzalama, şu anda yalnızca nuget.exe Windows üzerinde kullanılırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="3d92f-117">İmzalı paketlerin doğrulama şu anda yalnızca, Windows üzerinde nuget.exe veya Visual Studio kullanılırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="3d92f-118">Sertifika gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="3d92f-118">Certificate requirements</span></span>

<span data-ttu-id="3d92f-119">Paket imzalama gerektiren bir kod imzalama sertifikası, özel bir türü için geçerli sertifika olan `id-kp-codeSigning` amaçlı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="3d92f-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="3d92f-120">Ayrıca, sertifika bir RSA ortak anahtar uzunluğu 2048 bit ya da daha yüksek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="3d92f-121">Bir kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="3d92f-121">Get a code signing certificate</span></span>

<span data-ttu-id="3d92f-122">Geçerli sertifikalar gibi bir ortak sertifika yetkilisinden elde edilebilir:</span><span class="sxs-lookup"><span data-stu-id="3d92f-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="3d92f-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="3d92f-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="3d92f-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="3d92f-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="3d92f-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="3d92f-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="3d92f-126">Genel oturum</span><span class="sxs-lookup"><span data-stu-id="3d92f-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="3d92f-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="3d92f-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="3d92f-128">Certum</span><span class="sxs-lookup"><span data-stu-id="3d92f-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="3d92f-129">Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="3d92f-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="3d92f-130">Bir test sertifikası oluştur</span><span class="sxs-lookup"><span data-stu-id="3d92f-130">Create a test certificate</span></span>

<span data-ttu-id="3d92f-131">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d92f-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="3d92f-132">Kendi kendine verilen bir sertifika oluşturmak için kullanın [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="3d92f-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="3d92f-133">Bu komut, geçerli kullanıcının kişisel sertifika deposunda kullanılabilir bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d92f-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="3d92f-134">Sertifika deposu çalıştırarak açabileceğiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.</span><span class="sxs-lookup"><span data-stu-id="3d92f-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="3d92f-135">paketleri nuget.org kabul etmez ile şirket içinde verilen sertifikalara güvenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="3d92f-136">Zaman damgası gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="3d92f-136">Timestamp requirements</span></span>

<span data-ttu-id="3d92f-137">İmzalanmış paketleri paketi imzalama sertifikasının geçerlilik süresini aşan geçerlilik imzası emin olmak için bir RFC 3161 zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="3d92f-138">Zaman damgası imzalamak için kullanılan sertifika geçerli olmalıdır `id-kp-timeStamping` amaçlı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="3d92f-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="3d92f-139">Ayrıca, sertifika bir RSA ortak anahtar uzunluğu 2048 bit ya da daha yüksek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="3d92f-140">Ek teknik ayrıntılar bulunabilir [imza teknik özellikleri paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="3d92f-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="3d92f-141">Nuget.org imza gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="3d92f-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="3d92f-142">nuget.org imzalı paket kabul etmek için ek gereksinimlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3d92f-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="3d92f-143">Bir yazar imza birincil imza olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="3d92f-144">Birincil bir imza geçerli tek bir zaman damgası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="3d92f-145">X.509 sertifikaları Yazar imza hem de zaman damgası imzası için:</span><span class="sxs-lookup"><span data-stu-id="3d92f-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="3d92f-146">2048 bit RSA ortak anahtarını olmalıdır veya büyük.</span><span class="sxs-lookup"><span data-stu-id="3d92f-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="3d92f-147">Paket doğrulaması nuget.org üzerindeki her zaman geçerli UTC saati, geçerlilik süresi içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="3d92f-148">Windows üzerinde varsayılan olarak güvenilen bir güvenilir kök yetkilisi zincir şeklinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="3d92f-149">Kendi kendine verilen sertifikalarla imzalanmış paketleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="3d92f-150">Amacı için geçerli olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="3d92f-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="3d92f-151">İmzalama sertifikası yazar, kod imzalama için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="3d92f-152">Zaman damgası sertifika için zaman damgası geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="3d92f-153">Zaman imzalarken iptal edilmiş olmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="3d92f-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="3d92f-154">(Nuget.org iptal durumunu düzenli aralıklarla yeniden denetler şekilde bu gönderme sırasında knowable olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="3d92f-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="3d92f-155">Nuget.org sertifikayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="3d92f-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="3d92f-156">İmzalı paket göndermek için bir sertifika ile nuget.org kaydetmeniz gerekir. Sertifikayı gereken bir `.cer` dosyayı ikili bir DER biçiminde.</span><span class="sxs-lookup"><span data-stu-id="3d92f-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="3d92f-157">Sertifika Dışarı Aktarma Sihirbazı'nı kullanarak ikili bir DER biçimine var olan bir sertifikayı dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d92f-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![Sertifika Dışarı Aktarma Sihirbazı](media/CertificateExportWizard.png)

<span data-ttu-id="3d92f-159">İleri düzey kullanıcılar kullanarak sertifikayı dışarı aktarabilir [sertifika dışarı aktarma PowerShell komutunu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="3d92f-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="3d92f-160">Nuget.org ile sertifikayı kaydetmek için Git `Certificates` bölümünde `Account settings` sayfasında (veya kuruluşun Ayarları sayfası) seçip `Register new certificate`.</span><span class="sxs-lookup"><span data-stu-id="3d92f-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![Kayıtlı sertifikaları](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="3d92f-162">Bir kullanıcı birden çok sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d92f-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="3d92f-163">Bir kullanıcı sonra bir sertifika kayıtlı tüm gelecekteki paket gönderimleri **gerekir** , imzalı bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="3d92f-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="3d92f-164">Kullanıcılar ayrıca kayıtlı bir sertifika hesaptan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3d92f-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="3d92f-165">Bir sertifika kaldırıldıktan sonra bu sertifika ile imzalanmış paketleri gönderimi başarısız.</span><span class="sxs-lookup"><span data-stu-id="3d92f-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="3d92f-166">Var olan paketleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="3d92f-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="3d92f-167">Paket imzalama gereksinimlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3d92f-167">Configure package signing requirements</span></span>

<span data-ttu-id="3d92f-168">Bir paketi tek sahip siz olursunuz gerekli imzalayan vardır.</span><span class="sxs-lookup"><span data-stu-id="3d92f-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="3d92f-169">Diğer bir deyişle, paketlerinizi imzalamak ve nuget.org için göndermek için herhangi bir kayıtlı sertifikaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d92f-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="3d92f-170">Bir paket birden çok sahipleri, varsayılan olarak varsa, "Tüm" sahibinin sertifikalar paketi imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="3d92f-171">Paket bir ortak sahip olarak, kendiniz ile "tümü" ya da gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d92f-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="3d92f-172">Kayıtlı herhangi bir sertifika yok. bir sahip yaparsanız, işaretsiz paketleri izin verilir.</span><span class="sxs-lookup"><span data-stu-id="3d92f-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="3d92f-173">"Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından nuget.org imzalı bir paket, sahiplerinden biri kayıtlı bir imza ile kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.</span><span class="sxs-lookup"><span data-stu-id="3d92f-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![Paket İmzalayanları yapılandırın](media/configure-package-signers.png)
