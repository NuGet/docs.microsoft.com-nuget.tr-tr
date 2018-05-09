---
title: NuGet paketleri başvuru imzalı
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a><span data-ttu-id="3b9bf-103">İmzalı Paketleri</span><span class="sxs-lookup"><span data-stu-id="3b9bf-103">Signed packages</span></span>

<span data-ttu-id="3b9bf-104">*NuGet 4.6.0+ ve Visual Studio 2017 15.6 ve sonraki sürümleri*</span><span class="sxs-lookup"><span data-stu-id="3b9bf-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="3b9bf-105">NuGet paketleri, üzerinde oynanmış içerik karşı koruma sağlayan dijital bir imza içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="3b9bf-106">Bu imza, ayrıca paket gerçek kaynak için Orijinallik sağlamaları ekler bir X.509 Sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="3b9bf-107">İmzalı paketleri en güçlü uçtan uca doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="3b9bf-108">Bir yazar imzası Yazar paket bağımsız imzalıdan beri'nın paket değiştirilmemiş güvence altına alır, deposu veya ne paket teslim yöntemi taşıma.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="3b9bf-109">Kilitli ortamında talep tüketiciler belirli yazarının sertifikayla imzalanan paketleri gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-109">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="3b9bf-110">Ayrıca, imzalama sertifikasının süresi öncesinde kaydedilmesi gerektiğinden Yazar imzalanan paketleri nuget.org yayımlama ardışık düzeni için ek kimlik doğrulama mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-110">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="3b9bf-111">İmzalı paket oluşturma hakkında daha fazla bilgi için bkz: [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="3b9bf-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="3b9bf-112">nuget.org imzalı paketleri şu anda kabul etmiyor.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-112">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="3b9bf-113">Paketleri yayımlama özel akışları için oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-113">You can sign packages for publishing to custom feeds.</span></span>

> [!Important]
> <span data-ttu-id="3b9bf-114">Paket imzalama, şu anda yalnızca nuget.exe Windows kullanıldığında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-114">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="3b9bf-115">İmzalı paketlerin doğrulama şu anda yalnızca, Windows nuget.exe veya Visual Studio kullanıldığında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-115">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="3b9bf-116">Sertifika gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="3b9bf-116">Certificate requirements</span></span>

<span data-ttu-id="3b9bf-117">Paketin imzalanması bir kod imzalama için geçerli olan sertifika bir özel tür sertifikası gerektirir `id-kp-codeSigning` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="3b9bf-117">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="3b9bf-118">Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-118">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="3b9bf-119">Bir kod imzalama sertifikası alın</span><span class="sxs-lookup"><span data-stu-id="3b9bf-119">Get a code signing certificate</span></span>

<span data-ttu-id="3b9bf-120">Geçerli sertifikalar gibi ortak sertifika yetkililerinden alınabilir:</span><span class="sxs-lookup"><span data-stu-id="3b9bf-120">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="3b9bf-121">Symantec</span><span class="sxs-lookup"><span data-stu-id="3b9bf-121">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="3b9bf-122">DigiCert</span><span class="sxs-lookup"><span data-stu-id="3b9bf-122">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="3b9bf-123">Daddy gidin</span><span class="sxs-lookup"><span data-stu-id="3b9bf-123">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="3b9bf-124">Genel oturum</span><span class="sxs-lookup"><span data-stu-id="3b9bf-124">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="3b9bf-125">Comodo</span><span class="sxs-lookup"><span data-stu-id="3b9bf-125">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="3b9bf-126">Certum</span><span class="sxs-lookup"><span data-stu-id="3b9bf-126">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="3b9bf-127">Windows tarafından güvenilen sertifika yetkilileri tam listesi elde edilebilir [ http://aka.ms/trustcertpartners ](http://aka.ms/trustcertpartners).</span><span class="sxs-lookup"><span data-stu-id="3b9bf-127">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="3b9bf-128">Bir test sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b9bf-128">Create a test certificate</span></span>

<span data-ttu-id="3b9bf-129">Kendi kendine verilen sertifikaların test amacıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-129">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="3b9bf-130">Kendi kendine verilen bir sertifika oluşturmak için kullanmak [yeni SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-130">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="3b9bf-131">Bu komut, geçerli kullanıcının kişisel sertifika deposunda bir test sertifikası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-131">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="3b9bf-132">Sertifika deposu çalıştırarak açabilirsiniz `certmgr.msc` yeni oluşturulan sertifikayı görmek için.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-132">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="3b9bf-133">Zaman damgası gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="3b9bf-133">Timestamp requirements</span></span>

<span data-ttu-id="3b9bf-134">İmzalı Paketleri sertifikanın geçerlilik süresi imzalama paket ötesinde imza doğruluğundan emin olmak için bir RFC 3161 zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-134">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="3b9bf-135">Zaman damgası imzalamak için kullanılan sertifikanın geçerli `id-kp-timeStamping` amacı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="3b9bf-135">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="3b9bf-136">Ayrıca, sertifikanın bir RSA ortak anahtar uzunluğu 2048 bit veya üstü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3b9bf-136">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="3b9bf-137">Ek teknik ayrıntılar bulunabilir [imza teknik belirtimlerin paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="3b9bf-137">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
