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
# <a name="signing-nuget-packages"></a><span data-ttu-id="eaed8-103">NuGet paketleri imzalanıyor</span><span class="sxs-lookup"><span data-stu-id="eaed8-103">Signing NuGet Packages</span></span>

<span data-ttu-id="eaed8-104">İmzalı paketler, içerik değişikliklere karşı koruma sağlayan içerik bütünlüğü doğrulama denetimleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaed8-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="eaed8-105">Paket imzası Ayrıca paketin gerçek kaynağı ve tüketicinin paket özgünlük değeri hakkında tek bir kaynak kaynağı görevi görür.</span><span class="sxs-lookup"><span data-stu-id="eaed8-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="eaed8-106">Bu kılavuzda zaten [bir paket oluşturmuş](creating-a-package.md)olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eaed8-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="eaed8-107">Kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="eaed8-107">Get a code signing certificate</span></span>

<span data-ttu-id="eaed8-108">Geçerli sertifikalar [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. gibi bir genel sertifika yetkilisinden elde edilebilir. Windows tarafından güvenilen sertifika yetkililerinin tüm listesi, adresinden elde edilebilir [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list) .</span><span class="sxs-lookup"><span data-stu-id="eaed8-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](/security/trusted-root/participants-list).</span></span>

<span data-ttu-id="eaed8-109">Test amaçlı olarak, kendi kendine verilen sertifikaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="eaed8-110">Ancak, otomatik olarak verilen sertifikalar kullanılarak imzalanmış paketler NuGet.org tarafından kabul edilmez. [Test sertifikası oluşturma](#create-a-test-certificate) hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="eaed8-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="eaed8-111">Sertifika dosyasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="eaed8-111">Export the certificate file</span></span>

* <span data-ttu-id="eaed8-112">Sertifika Dışarı Aktarma Sihirbazı 'nı kullanarak, var olan bir sertifikayı ikili DER biçimine aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Sertifika Dışarı Aktarma Sihirbazı](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="eaed8-114">Sertifikayı [dışarı aktar-sertifika PowerShell komutunu](/powershell/module/pkiclient/export-certificate)kullanarak da dışa aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="eaed8-115">Paketi imzala</span><span class="sxs-lookup"><span data-stu-id="eaed8-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="eaed8-116">nuget.exe 4.6.0 veya üstünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="eaed8-117">dotnet.exe destek yakında kullanıma sunulacak [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="eaed8-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="eaed8-118">[NuGet işaretini](../reference/cli-reference/cli-ref-sign.md)kullanarak paketi imzala:</span><span class="sxs-lookup"><span data-stu-id="eaed8-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="eaed8-119">Sertifika sağlayıcısı çoğunlukla, `Timestamper` yukarıda görüntülenecek isteğe bağlı bağımsız değişken için kullanabileceğiniz bir zaman damgası sunucu URL 'si de sağlar.</span><span class="sxs-lookup"><span data-stu-id="eaed8-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="eaed8-120">Sağlayıcının belgelerine ve/veya bu hizmet URL 'sine yönelik desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="eaed8-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="eaed8-121">Sertifika deposunda bulunan bir sertifikayı kullanabilir veya bir dosyadaki sertifikayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="eaed8-122">[NuGet işareti](../reference/cli-reference/cli-ref-sign.md)için CLI başvurusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="eaed8-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="eaed8-123">İmzalı paketler, imzalama sertifikasının süresi dolduğunda imzanın geçerli kaldığından emin olmak için bir zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="eaed8-124">Aksi takdirde imza işlemi bir [Uyarı](../reference/errors-and-warnings/NU3002.md)üretir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="eaed8-125">[NuGet doğrulaması](../reference/cli-reference/cli-ref-verify.md)' nı kullanarak belirli bir paketin imza ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="eaed8-126">Sertifikayı NuGet.org 'e kaydetme</span><span class="sxs-lookup"><span data-stu-id="eaed8-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="eaed8-127">İmzalı bir paket yayımlamak için öncelikle sertifikayı NuGet.org ile kaydetmeniz gerekir. Bir ikili DER biçiminde bir dosya olarak sertifikaya ihtiyacınız vardır `.cer` .</span><span class="sxs-lookup"><span data-stu-id="eaed8-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="eaed8-128">NuGet.org ['de oturum açın](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .</span><span class="sxs-lookup"><span data-stu-id="eaed8-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="eaed8-129">`Account settings`(Veya `Manage Organization` **>** `Edit Organization` sertifikayı bir kuruluş hesabıyla kaydetmek istiyorsanız) bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="eaed8-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organization` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="eaed8-130">Bölümünü genişletin `Certificates` ve öğesini seçin `Register new` .</span><span class="sxs-lookup"><span data-stu-id="eaed8-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="eaed8-131">Daha önce aktarılmış olan sertifika dosyasına gidip seçin.</span><span class="sxs-lookup"><span data-stu-id="eaed8-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="eaed8-132">![Kayıtlı sertifikalar](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="eaed8-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="eaed8-133">**Not**</span><span class="sxs-lookup"><span data-stu-id="eaed8-133">**Note**</span></span>
* <span data-ttu-id="eaed8-134">Bir Kullanıcı birden çok sertifika gönderebilir ve aynı sertifika birden çok kullanıcı tarafından kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="eaed8-135">Bir Kullanıcı bir sertifikaya kaydolduktan sonra, gelecekteki tüm paket gönderimlerinin sertifikalardan biri ile imzalanması **gerekir** .</span><span class="sxs-lookup"><span data-stu-id="eaed8-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="eaed8-136">Bkz. [NuGet.org 'de paketiniz için imzalama gereksinimlerini yönetme](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="eaed8-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="eaed8-137">Kullanıcılar ayrıca, kayıtlı bir sertifikayı hesaptan kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="eaed8-138">Bir sertifika kaldırıldıktan sonra, bu sertifikayla imzalanmış yeni paketler gönderim sırasında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="eaed8-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="eaed8-139">Mevcut paketler etkilenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="eaed8-140">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="eaed8-140">Publish the package</span></span>

<span data-ttu-id="eaed8-141">Artık paketi NuGet.org 'e yayımlamaya hazırsınız. Bkz. [paketleri yayımlama](../nuget-org/Publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="eaed8-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="eaed8-142">Test sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="eaed8-142">Create a test certificate</span></span>

<span data-ttu-id="eaed8-143">Test amaçlı olarak, kendi kendine verilen sertifikaları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="eaed8-144">Kendi kendine verilen bir sertifika oluşturmak için [New-SelfSignedCertificate PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate)kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaed8-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="eaed8-145">Bu komut, geçerli kullanıcının kişisel sertifika deposunda bulunan bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eaed8-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="eaed8-146">`certmgr.msc`Yeni oluşturulan sertifikayı görmek için, çalıştırarak sertifika deposunu açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="eaed8-147">NuGet.org, otomatik olarak verilen sertifikalarla imzalanmış paketleri kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="eaed8-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="eaed8-148">NuGet.org 'de paketiniz için imzalama gereksinimlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="eaed8-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="eaed8-149">NuGet.org ['de oturum açın](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .</span><span class="sxs-lookup"><span data-stu-id="eaed8-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="eaed8-150">`Manage Packages`  
    ![ Paket İmzalayanları yapılandırma bölümüne git](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="eaed8-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="eaed8-151">Bir paketin tek sahibiyseniz, gerekli olan imzalamanıza karşı, paketlerinizi imzalamak ve NuGet.org 'e yayımlamak için kayıtlı sertifikalardan herhangi birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="eaed8-152">Bir paketin birden çok sahibi varsa, varsayılan olarak "Any" sahibinin sertifikaları paketi imzalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="eaed8-153">Paketin ortak sahibi olarak, "Any" i veya diğer tüm ikincil sahiplerle gerekli imzacı olacak şekilde geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eaed8-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="eaed8-154">Kayıtlı bir sertifikası olmayan bir sahip yaparsanız, imzasız paketlere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="eaed8-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="eaed8-155">Benzer şekilde, bir sahibin kayıtlı bir sertifikası olan bir paket için varsayılan "Any" seçeneği seçilmişse ve başka bir sahibe kayıtlı bir sertifika yoksa, NuGet.org, sahip olduğu imzalı bir paketi veya bir imzasız paketi kabul eder (sahiplerden birinde kayıtlı sertifika olmadığından).</span><span class="sxs-lookup"><span data-stu-id="eaed8-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="eaed8-156">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="eaed8-156">Related articles</span></span>

- [<span data-ttu-id="eaed8-157">Paket güven sınırlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="eaed8-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="eaed8-158">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="eaed8-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)