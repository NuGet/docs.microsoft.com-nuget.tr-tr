---
title: Paketleri başvuru imzalı | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Paketleri özellik açıklaması imzalanmış.
keywords: NuGet paket oturum, imza sertifikası
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a2a338596f7d98ded11da6fb02bafba3521249ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="signed-packages"></a><span data-ttu-id="abd8d-104">İmzalı Paketleri</span><span class="sxs-lookup"><span data-stu-id="abd8d-104">Signed packages</span></span>

<span data-ttu-id="abd8d-105">*NuGet 4.6.0+ ve Visual Studio 2017 15.6 ve sonraki sürümleri*</span><span class="sxs-lookup"><span data-stu-id="abd8d-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="abd8d-106">NuGet paketleri, üzerinde oynanmış içerik karşı koruma sağlayan dijital bir imza içerebilir.</span><span class="sxs-lookup"><span data-stu-id="abd8d-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="abd8d-107">Bu imza, ayrıca paket gerçek kaynak için Orijinallik sağlamaları ekler bir X.509 Sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="abd8d-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="abd8d-108">İmzalı paketleri en güçlü uçtan uca doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="abd8d-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="abd8d-109">Bir yazar imzası Yazar paket bağımsız imzalıdan beri'nın paket değiştirilmemiş güvence altına alır, deposu veya ne paket teslim yöntemi taşıma.</span><span class="sxs-lookup"><span data-stu-id="abd8d-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="abd8d-110">Kilitli ortamında talep tüketiciler belirli yazarının sertifikayla imzalanan paketleri gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="abd8d-110">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="abd8d-111">Ayrıca, imzalama sertifikasının süresi öncesinde kaydedilmesi gerektiğinden Yazar imzalanan paketleri nuget.org yayımlama ardışık düzeni için ek kimlik doğrulama mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="abd8d-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="abd8d-112">İmzalı paket oluşturma hakkında daha fazla bilgi için bkz: [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="abd8d-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="abd8d-113">nuget.org imzalı paketleri şu anda kabul etmiyor.</span><span class="sxs-lookup"><span data-stu-id="abd8d-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="abd8d-114">Paketleri yayımlama özel akışları için oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abd8d-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="abd8d-115">Sertifika gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="abd8d-115">Certificate requirements</span></span>

<span data-ttu-id="abd8d-116">Paketin imzalanması bir kod imzalama için geçerli olan sertifika bir özel tür sertifikası gerektirir `id-kp-codeSigning` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="abd8d-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="abd8d-117">Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="abd8d-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="abd8d-118">Bir kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="abd8d-118">Get a code signing certificate</span></span>

<span data-ttu-id="abd8d-119">Geçerli sertifikalar gibi ortak sertifika yetkililerinden alınabilir:</span><span class="sxs-lookup"><span data-stu-id="abd8d-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="abd8d-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="abd8d-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="abd8d-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="abd8d-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="abd8d-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="abd8d-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="abd8d-123">Genel oturum</span><span class="sxs-lookup"><span data-stu-id="abd8d-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="abd8d-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="abd8d-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="abd8d-125">Certum</span><span class="sxs-lookup"><span data-stu-id="abd8d-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="abd8d-126">Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="abd8d-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="abd8d-127">Bir test sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="abd8d-127">Create a test certificate</span></span>

<span data-ttu-id="abd8d-128">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="abd8d-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="abd8d-129">Kendi kendine verilen bir sertifika oluşturmak için kullanmak [yeni SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="abd8d-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="abd8d-130">Bu komut, geçerli kullanıcının kişisel sertifika deposunda bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="abd8d-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="abd8d-131">Sertifika deposu çalıştırarak açabilirsiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.</span><span class="sxs-lookup"><span data-stu-id="abd8d-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="abd8d-132">Zaman damgası gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="abd8d-132">Timestamp requirements</span></span>

<span data-ttu-id="abd8d-133">İmzalı Paketleri sertifikanın geçerlilik süresi imzalama paket ötesinde imza doğruluğundan emin olmak için bir RFC 3161 zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="abd8d-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="abd8d-134">Zaman damgası imzalamak için kullanılan sertifikanın geçerli `id-kp-timeStamping` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="abd8d-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="abd8d-135">Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="abd8d-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="abd8d-136">Ek teknik ayrıntılar bulunabilir [imza teknik belirtimlerin paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="abd8d-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
