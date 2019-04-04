---
title: NuGet paketlerini imzalama
description: İmzalı paketlerin açıklar içerik bütünlüğünü doğrulamayı etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 8ff92e5a3ab2d5c13ee02a9e49709866e2ac0e87
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921578"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="523bc-103">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="523bc-103">Signing NuGet Packages</span></span>

<span data-ttu-id="523bc-104">İmzalanmış paketleri içerik izinsiz kullanıma karşı koruma sağlayan içerik bütünlüğünü doğrulama denetimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="523bc-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="523bc-105">Paket imzası, ayrıca tek gerçek kaynak paketi hakkında doğru kaynağı olarak görev yapar ve paket kimlik doğrulaması için tüketici artırır.</span><span class="sxs-lookup"><span data-stu-id="523bc-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="523bc-106">Bu kılavuz, zaten sahip olduğunuzu varsayar [bir paket oluşturan](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="523bc-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="523bc-107">Bir kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="523bc-107">Get a code signing certificate</span></span>

<span data-ttu-id="523bc-108">Geçerli sertifikalar elde edilebilir bir ortak sertifika yetkilisinden gibi [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [genel oturum](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="523bc-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="523bc-109">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523bc-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="523bc-110">Ancak, kendi kendine verilen sertifikaları kullanarak imzalanmış paketleri NuGet.org tarafından kabul edilmez. Daha fazla bilgi edinin [bir test sertifikası oluşturma](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="523bc-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="523bc-111">Sertifika dosyasını dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="523bc-111">Export the certificate file</span></span>

* <span data-ttu-id="523bc-112">Sertifika Dışarı Aktarma Sihirbazı'nı kullanarak ikili bir DER biçimine var olan bir sertifikayı dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523bc-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Sertifika Dışarı Aktarma Sihirbazı](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="523bc-114">Sertifikayı kullanarak da verebilirsiniz [sertifika dışarı aktarma PowerShell komutunu](/powershell/module/pkiclient/export-certificate).</span><span class="sxs-lookup"><span data-stu-id="523bc-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="523bc-115">Paket imzalama</span><span class="sxs-lookup"><span data-stu-id="523bc-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="523bc-116">Nuget.exe 4.6.0 gerektirir veya üzeri</span><span class="sxs-lookup"><span data-stu-id="523bc-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="523bc-117">Paket kullanarak oturum [nuget oturum](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="523bc-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="523bc-118">Sertifika sağlayıcısı için kullanabileceğiniz bir zaman damgası sunucu URL'si genellikle de sağlar. `Timestamper` yukarıdaki isteğe bağlı bağımsız değişkeni göster.</span><span class="sxs-lookup"><span data-stu-id="523bc-118">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="523bc-119">Sağlayıcınızın belgeleri ve/veya ilgili hizmet URL'si için destek başvurun.</span><span class="sxs-lookup"><span data-stu-id="523bc-119">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="523bc-120">Sertifika deposunda mevcut bir sertifikayı kullanın ya da bir dosyadan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="523bc-120">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="523bc-121">CLI başvuru için bkz. [nuget oturum](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="523bc-121">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="523bc-122">İmzalanmış paketleri imzalama sertifikasının süresi dolduğunda imzanın geçerli olacağı emin olmak için bir zaman damgasını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="523bc-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="523bc-123">Oturum işlemi başka oluşturacak bir [uyarı](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="523bc-123">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="523bc-124">Belirtilen paketi kullanarak bir imza ayrıntıları görebilirsiniz [nuget doğrulayın](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="523bc-124">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="523bc-125">NuGet.org sertifikayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="523bc-125">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="523bc-126">İmzalı paket yayımlamak için sertifika NuGet.org ile kaydetmeniz gerekir. Sertifikayı gereken bir `.cer` dosyayı ikili bir DER biçiminde.</span><span class="sxs-lookup"><span data-stu-id="523bc-126">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="523bc-127">[Oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org için.</span><span class="sxs-lookup"><span data-stu-id="523bc-127">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="523bc-128">Git `Account settings` (veya `Manage Organization` **>** `Edit Organziation` sertifika bir kuruluş hesabı ile kaydetmek isterseniz).</span><span class="sxs-lookup"><span data-stu-id="523bc-128">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="523bc-129">Genişletin `Certificates` seçin ve bölüm `Register new`.</span><span class="sxs-lookup"><span data-stu-id="523bc-129">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="523bc-130">Göz atma ve daha önce dışarı aktarılan sertifika dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="523bc-130">Browse and select the certficate file that was exported earlier.</span></span>
  ![Kayıtlı sertifikaları](../reference/media/registered-certs.png)

**<span data-ttu-id="523bc-132">Not</span><span class="sxs-lookup"><span data-stu-id="523bc-132">Note</span></span>**
* <span data-ttu-id="523bc-133">Bir kullanıcı birden çok sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523bc-133">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="523bc-134">Bir kullanıcı sonra bir sertifika kayıtlı tüm gelecekteki paket gönderimleri **gerekir** , imzalı bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="523bc-134">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="523bc-135">Bkz: [paketinizi nuget.org gereksinimleri imzalama Yönet](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="523bc-135">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="523bc-136">Kullanıcılar ayrıca kayıtlı bir sertifika hesaptan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="523bc-136">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="523bc-137">Bir sertifika kaldırıldıktan sonra bu sertifika ile imzalanmış yeni paketler gönderimi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="523bc-137">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="523bc-138">Var olan paketleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="523bc-138">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="523bc-139">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="523bc-139">Publish the package</span></span>

<span data-ttu-id="523bc-140">NuGet.org için paket yayımlamak artık hazırsınız. Bkz: [paketleri yayımlama](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="523bc-140">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="523bc-141">Bir test sertifikası oluştur</span><span class="sxs-lookup"><span data-stu-id="523bc-141">Create a test certificate</span></span>

<span data-ttu-id="523bc-142">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523bc-142">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="523bc-143">Kendi kendine verilen bir sertifika oluşturmak için kullanın [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="523bc-143">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="523bc-144">Bu komut, geçerli kullanıcının kişisel sertifika deposunda kullanılabilir bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="523bc-144">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="523bc-145">Sertifika deposu çalıştırarak açabileceğiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.</span><span class="sxs-lookup"><span data-stu-id="523bc-145">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="523bc-146">Paketleri NuGet.org kabul etmez ile şirket içinde verilen sertifikalara güvenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="523bc-146">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="523bc-147">NuGet.org üzerinde paket imzalama gereksinimlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="523bc-147">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="523bc-148">[Oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org için.</span><span class="sxs-lookup"><span data-stu-id="523bc-148">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="523bc-149">Git `Manage Packages` 
   ![paket İmzalayanları yapılandırın](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="523bc-149">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="523bc-150">Bir paketi tek sahip siz olursunuz, gerekli imzalayan olan herhangi bir kayıtlı sertifikaları imzalamak ve NuGet.org için paket yayımlamasına yani kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523bc-150">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="523bc-151">Bir paket birden çok sahipleri, varsayılan olarak varsa, "Tüm" sahibinin sertifikalar paketi imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="523bc-151">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="523bc-152">Paket bir ortak sahip olarak, kendiniz ile "tümü" ya da gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="523bc-152">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="523bc-153">Kayıtlı herhangi bir sertifika yok. bir sahip yaparsanız, işaretsiz paketleri izin verilir.</span><span class="sxs-lookup"><span data-stu-id="523bc-153">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="523bc-154">"Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından NuGet.org imzalı bir paket, sahiplerinden biri kayıtlı bir imza ile kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.</span><span class="sxs-lookup"><span data-stu-id="523bc-154">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="523bc-155">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="523bc-155">Related articles</span></span>

- [<span data-ttu-id="523bc-156">İmzalı paketlerin yüklenmesi</span><span class="sxs-lookup"><span data-stu-id="523bc-156">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="523bc-157">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="523bc-157">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
