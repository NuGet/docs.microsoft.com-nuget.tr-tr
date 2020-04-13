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
# <a name="signing-nuget-packages"></a><span data-ttu-id="b2e98-103">NuGet Paketlerini İmzalama</span><span class="sxs-lookup"><span data-stu-id="b2e98-103">Signing NuGet Packages</span></span>

<span data-ttu-id="b2e98-104">İmzalı paketler, içerik tahrifatına karşı koruma sağlayan içerik bütünlüğü doğrulama denetimlerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="b2e98-105">Paket imzası aynı zamanda paketin gerçek kökeni hakkında tek bir doğruluk kaynağı olarak hizmet vermektedir ve tüketici için paket orijinalliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="b2e98-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="b2e98-106">Bu kılavuz, zaten [bir paket oluşturduğunuzu](creating-a-package.md)varsayar.</span><span class="sxs-lookup"><span data-stu-id="b2e98-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="b2e98-107">Kod imzalama sertifikası alma</span><span class="sxs-lookup"><span data-stu-id="b2e98-107">Get a code signing certificate</span></span>

<span data-ttu-id="b2e98-108">Geçerli sertifikalar [Symantec,](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3) [DigiCert,](https://www.digicert.com/code-signing/) [Go Daddy,](https://www.godaddy.com/web-security/code-signing-certificate) [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo,](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php) [Certum,](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml)vb. gibi bir kamu sertifika yetkilisinden alınabilir. Windows tarafından güvenilen sertifika yetkililerinin tam [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners)listesi.</span><span class="sxs-lookup"><span data-stu-id="b2e98-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="b2e98-109">Kendi kendine verilen sertifikaları sınama amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="b2e98-110">Ancak, kendi kendine verilen sertifikalar kullanılarak imzalanan paketler NuGet.org tarafından kabul edilmez. [Test sertifikası oluşturma](#create-a-test-certificate) hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="b2e98-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="b2e98-111">Sertifika dosyasını dışa aktarma</span><span class="sxs-lookup"><span data-stu-id="b2e98-111">Export the certificate file</span></span>

* <span data-ttu-id="b2e98-112">Varolan bir sertifikayı Sertifika Dışa Aktarma Sihirbazı'nı kullanarak ikili DER biçimine dışa aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![Sertifika Verme Sihirbazı](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="b2e98-114">Ayrıca [Dışa Aktarma Sertifikası PowerShell komutunu](/powershell/module/pkiclient/export-certificate)kullanarak sertifikayı dışa aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="b2e98-115">Paketi imzalayın</span><span class="sxs-lookup"><span data-stu-id="b2e98-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="b2e98-116">nuget.exe 4.6.0 veya sonrası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-116">Requires nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="b2e98-117">dotnet.exe desteği yakında geliyor - [#7939](https://github.com/NuGet/Home/issues/7939)</span><span class="sxs-lookup"><span data-stu-id="b2e98-117">dotnet.exe support is coming soon - [#7939](https://github.com/NuGet/Home/issues/7939)</span></span>

<span data-ttu-id="b2e98-118">[Nuget işaretini](../reference/cli-reference/cli-ref-sign.md)kullanarak paketi imzalayın:</span><span class="sxs-lookup"><span data-stu-id="b2e98-118">Sign the package using [nuget sign](../reference/cli-reference/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> <span data-ttu-id="b2e98-119">Sertifika sağlayıcısı genellikle yukarıda belirtilen `Timestamper` isteğe bağlı bağımsız değişken için kullanabileceğiniz bir zaman damgası sunucusu URL'si de sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2e98-119">The certificate provider often also provides a timestamping server URL which you can use for the `Timestamper` optional argument show above.</span></span> <span data-ttu-id="b2e98-120">Sağlayıcınızın bu hizmet URL'si için belgelerine ve/veya desteğine danışın.</span><span class="sxs-lookup"><span data-stu-id="b2e98-120">Consult with your provider's documentation and/or support for that service URL.</span></span>

* <span data-ttu-id="b2e98-121">Sertifika deposunda bulunan bir sertifikayı kullanabilir veya bir dosyadan sertifika kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-121">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="b2e98-122">[Nuget işareti](../reference/cli-reference/cli-ref-sign.md)için CLI başvurusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="b2e98-122">See CLI reference for [nuget sign](../reference/cli-reference/cli-ref-sign.md).</span></span>
* <span data-ttu-id="b2e98-123">İmzalanan paketler, imza sertifikasının süresi dolduğunda imzanın geçerli kalmasını sağlamak için bir zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="b2e98-124">Aksi takdirde işaret işlemi bir [uyarı](../reference/errors-and-warnings/NU3002.md)üretecek.</span><span class="sxs-lookup"><span data-stu-id="b2e98-124">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="b2e98-125">Nuget [doğrulamak](../reference/cli-reference/cli-ref-verify.md)kullanarak belirli bir paketin imza ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-125">You can see the signature details of a given package using [nuget verify](../reference/cli-reference/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="b2e98-126">Sertifikayı NuGet.org kaydedin</span><span class="sxs-lookup"><span data-stu-id="b2e98-126">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="b2e98-127">İmzalı bir paketi yayımlamak için önce sertifikayı NuGet.org kaydettirmelisiniz. Sertifikayı ikili DER `.cer` formatında bir dosya olarak almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-127">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="b2e98-128">NuGet.org [oturum açın.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)</span><span class="sxs-lookup"><span data-stu-id="b2e98-128">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="b2e98-129">Gidin `Account settings` (veya `Manage Organization` **>** `Edit Organziation` sertifikayı bir Kuruluş hesabına kaydettirmek istiyorsanız).</span><span class="sxs-lookup"><span data-stu-id="b2e98-129">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="b2e98-130">Bölümü `Certificates` genişletin `Register new`ve seçin.</span><span class="sxs-lookup"><span data-stu-id="b2e98-130">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="b2e98-131">Daha önce dışa aktarılan sertifika dosyasına göz atın ve seçin.</span><span class="sxs-lookup"><span data-stu-id="b2e98-131">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="b2e98-132">![Kayıtlı Sertifikalar](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="b2e98-132">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="b2e98-133">**Not**</span><span class="sxs-lookup"><span data-stu-id="b2e98-133">**Note**</span></span>
* <span data-ttu-id="b2e98-134">Bir kullanıcı birden çok sertifika gönderebilir ve aynı sertifika birden çok kullanıcı tarafından kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-134">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="b2e98-135">Bir kullanıcı bir sertifikayı kaydettikten sonra, gelecekteki tüm paket gönderimlerinin sertifikalardan biriyle imzalanması **gerekir.**</span><span class="sxs-lookup"><span data-stu-id="b2e98-135">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="b2e98-136">Bkz. [NuGet.org paketiniz için imza gereksinimlerini yönetin](#manage-signing-requirements-for-your-package-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="b2e98-136">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="b2e98-137">Kullanıcılar kayıtlı bir sertifikayı da hesaptan kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-137">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="b2e98-138">Sertifika kaldırıldıktan sonra, bu sertifikayla imzalanan yeni paketler gönderimsırasında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b2e98-138">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="b2e98-139">Varolan paketler etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="b2e98-139">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="b2e98-140">Paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="b2e98-140">Publish the package</span></span>

<span data-ttu-id="b2e98-141">Paketi NuGet.org yayınlamaya hazırsınız. Bkz. [Yayımlama paketleri.](../nuget-org/Publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="b2e98-141">You are now ready to publish the package to NuGet.org. See [Publishing packages](../nuget-org/Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="b2e98-142">Test sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2e98-142">Create a test certificate</span></span>

<span data-ttu-id="b2e98-143">Kendi kendine verilen sertifikaları sınama amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-143">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="b2e98-144">Kendi kendine verilen bir sertifika oluşturmak için [Yeni İmzalı Sertifika PowerShell komutunu](/powershell/module/pkiclient/new-selfsignedcertificate)kullanın.</span><span class="sxs-lookup"><span data-stu-id="b2e98-144">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate).</span></span>

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

<span data-ttu-id="b2e98-145">Bu komut, geçerli kullanıcının kişisel sertifika deposunda kullanılabilen bir sınama sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2e98-145">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="b2e98-146">Yeni oluşturulan sertifikayı görmek `certmgr.msc` için çalıştırarak sertifika mağazasını açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-146">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="b2e98-147">NuGet.org, kendi kendine verilen sertifikalarla imzalanmış paketleri kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="b2e98-147">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="b2e98-148">Paketiniz için imza gereksinimlerini NuGet.org</span><span class="sxs-lookup"><span data-stu-id="b2e98-148">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="b2e98-149">NuGet.org [oturum açın.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)</span><span class="sxs-lookup"><span data-stu-id="b2e98-149">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="b2e98-150">Paket `Manage Packages`  
    ![imzalayanları yapılandırmaya git](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="b2e98-150">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="b2e98-151">Bir paketin tek sahibisizseniz, gerekli imzalayan sizsiniz, yani paketlerinizi imzalamak ve NuGet.org yayınlamak için kayıtlı sertifikalardan herhangi birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-151">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="b2e98-152">Bir paketin birden çok sahibi varsa, varsayılan olarak, paketi imzalamak için "Herhangi bir" sahibinin sertifikaları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-152">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="b2e98-153">Paketin ortaklarından biri olarak, gerekli imzalayan kişi olmak için kendiniz veya başka bir ortak sahibiile "Any"yi geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e98-153">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="b2e98-154">Kayıtlı sertifikası olmayan bir sahip yaparsanız, imzasız paketlere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="b2e98-154">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="b2e98-155">Benzer şekilde, bir sahibin sertifikasının kayıtlı olduğu ve başka bir sahibinin kayıtlı sertifikası nın olmadığı bir paket için varsayılan "Herhangi bir" seçeneği seçilirse, NuGet.org, sahiplerinden biri tarafından kaydedilmiş imzalı bir paketi veya imzasız paketi kabul eder (çünkü sahiplerden birinin kayıtlı sertifikası yoktur).</span><span class="sxs-lookup"><span data-stu-id="b2e98-155">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="b2e98-156">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="b2e98-156">Related articles</span></span>

- [<span data-ttu-id="b2e98-157">Paket güven sınırlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b2e98-157">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="b2e98-158">İmzalı Paketler Referans</span><span class="sxs-lookup"><span data-stu-id="b2e98-158">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
