---
title: NuGet paketlerini imzalama
description: İmzalı paketlerin açıklar içerik bütünlüğünü doğrulamayı etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977569"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="726f1-103">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="726f1-103">Signing NuGet Packages</span></span>

<span data-ttu-id="726f1-104">İmzalanmış paketleri içerik izinsiz kullanıma karşı koruma sağlayan içerik bütünlüğünü doğrulama denetimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="726f1-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="726f1-105">Paket imzası, ayrıca tek gerçek kaynak paketi hakkında doğru kaynağı olarak görev yapar ve paket kimlik doğrulaması için tüketici artırır.</span><span class="sxs-lookup"><span data-stu-id="726f1-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="726f1-106">Bu kılavuz, zaten sahip olduğunuzu varsayar [bir paket oluşturan](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="726f1-107">Bir kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="726f1-107">Get a code signing certificate</span></span>

<span data-ttu-id="726f1-108">Geçerli sertifikalar elde edilebilir bir ortak sertifika yetkilisinden gibi [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [genel oturum](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="726f1-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="726f1-109">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="726f1-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="726f1-110">Ancak, kendi kendine verilen sertifikaları kullanarak imzalanmış paketleri NuGet.org tarafından kabul edilmez. Daha fazla bilgi edinin [bir test sertifikası oluşturma](#create-a-test-certificate)</span><span class="sxs-lookup"><span data-stu-id="726f1-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="726f1-111">Sertifika dosyasını dışarı aktar</span><span class="sxs-lookup"><span data-stu-id="726f1-111">Export the certificate file</span></span>

* <span data-ttu-id="726f1-112">Sertifika Dışarı Aktarma Sihirbazı'nı kullanarak ikili bir DER biçimine var olan bir sertifikayı dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="726f1-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Sertifika Dışarı Aktarma Sihirbazı](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="726f1-114">Sertifikayı kullanarak da verebilirsiniz [sertifika dışarı aktarma PowerShell komutunu](/powershell/module/pkiclient/export-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="726f1-115">Paket imzalama</span><span class="sxs-lookup"><span data-stu-id="726f1-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="726f1-116">Nuget.exe 4.6.0 gerektirir veya üzeri</span><span class="sxs-lookup"><span data-stu-id="726f1-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="726f1-117">Paket kullanarak oturum [nuget oturum](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="726f1-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="726f1-118">Sertifika deposunda mevcut bir sertifikayı kullanın ya da bir dosyadan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="726f1-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="726f1-119">CLI başvuru için bkz. [nuget oturum](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="726f1-120">İmzalanmış paketleri imzalama sertifikasının süresi dolduğunda imzanın geçerli olacağı emin olmak için bir zaman damgasını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="726f1-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="726f1-121">Oturum işlemi başka oluşturacak bir [uyarı](../reference/errors-and-warnings/NU3002.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="726f1-122">Belirtilen paketi kullanarak bir imza ayrıntıları görebilirsiniz [nuget doğrulayın](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="726f1-123">NuGet.org sertifikayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="726f1-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="726f1-124">İmzalı paket yayımlamak için sertifika NuGet.org ile kaydetmeniz gerekir. Sertifikayı gereken bir `.cer` dosyayı ikili bir DER biçiminde.</span><span class="sxs-lookup"><span data-stu-id="726f1-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="726f1-125">[Oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org için.</span><span class="sxs-lookup"><span data-stu-id="726f1-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="726f1-126">Git `Account settings` (veya `Manage Organization` **>** `Edit Organziation` sertifika bir kuruluş hesabı ile kaydetmek isterseniz).</span><span class="sxs-lookup"><span data-stu-id="726f1-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="726f1-127">Genişletin `Certificates` seçin ve bölüm `Register new`.</span><span class="sxs-lookup"><span data-stu-id="726f1-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="726f1-128">Göz atma ve daha önce dışarı aktarılan sertifika dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="726f1-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="726f1-129">![Kayıtlı sertifikaları](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="726f1-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="726f1-130">**Not**</span><span class="sxs-lookup"><span data-stu-id="726f1-130">**Note**</span></span>
* <span data-ttu-id="726f1-131">Bir kullanıcı birden çok sertifika ve aynı sertifikayı birden çok kullanıcı tarafından kaydedilebilir gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="726f1-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="726f1-132">Bir kullanıcı sonra bir sertifika kayıtlı tüm gelecekteki paket gönderimleri **gerekir** , imzalı bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="726f1-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="726f1-133">Bkz: [paketinizi nuget.org gereksinimleri imzalama Yönet](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="726f1-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="726f1-134">Kullanıcılar ayrıca kayıtlı bir sertifika hesaptan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="726f1-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="726f1-135">Bir sertifika kaldırıldıktan sonra bu sertifika ile imzalanmış yeni paketler gönderimi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="726f1-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="726f1-136">Var olan paketleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="726f1-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="726f1-137">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="726f1-137">Publish the package</span></span>

<span data-ttu-id="726f1-138">NuGet.org için paket yayımlamak artık hazırsınız. Bkz: [paketleri yayımlama](Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="726f1-139">Bir test sertifikası oluştur</span><span class="sxs-lookup"><span data-stu-id="726f1-139">Create a test certificate</span></span>

<span data-ttu-id="726f1-140">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="726f1-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="726f1-141">Kendi kendine verilen bir sertifika oluşturmak için kullanın [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span><span class="sxs-lookup"><span data-stu-id="726f1-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="726f1-142">Bu komut, geçerli kullanıcının kişisel sertifika deposunda kullanılabilir bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="726f1-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="726f1-143">Sertifika deposu çalıştırarak açabileceğiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.</span><span class="sxs-lookup"><span data-stu-id="726f1-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="726f1-144">Paketleri NuGet.org kabul etmez ile şirket içinde verilen sertifikalara güvenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="726f1-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="726f1-145">NuGet.org üzerinde paket imzalama gereksinimlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="726f1-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="726f1-146">[Oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) NuGet.org için.</span><span class="sxs-lookup"><span data-stu-id="726f1-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="726f1-147">Git `Manage Packages`  
    ![paket İmzalayanları yapılandırın](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="726f1-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="726f1-148">Bir paketi tek sahip siz olursunuz, gerekli imzalayan olan herhangi bir kayıtlı sertifikaları imzalamak ve NuGet.org için paket yayımlamasına yani kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="726f1-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="726f1-149">Bir paket birden çok sahipleri, varsayılan olarak varsa, "Tüm" sahibinin sertifikalar paketi imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="726f1-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="726f1-150">Paket bir ortak sahip olarak, kendiniz ile "tümü" ya da gerekli imzalayan olmasını herhangi diğer ortak sahibi geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="726f1-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="726f1-151">Kayıtlı herhangi bir sertifika yok. bir sahip yaparsanız, işaretsiz paketleri izin verilir.</span><span class="sxs-lookup"><span data-stu-id="726f1-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="726f1-152">"Tüm" seçeneğinin işaretli bir sahip bir sertifika kayıtlı olduğu bir paket ve başka bir sahip için varsayılan kayıtlı herhangi bir sertifika yoksa, benzer şekilde, ardından NuGet.org imzalı bir paket, sahiplerinden biri kayıtlı bir imza ile kabul eder ya da İmzasız (sahiplerinden biri kayıtlı herhangi bir sertifika olmadığından) paketi.</span><span class="sxs-lookup"><span data-stu-id="726f1-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="726f1-153">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="726f1-153">Related articles</span></span>

- [<span data-ttu-id="726f1-154">İmzalı paketlerin yüklenmesi</span><span class="sxs-lookup"><span data-stu-id="726f1-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="726f1-155">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="726f1-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
