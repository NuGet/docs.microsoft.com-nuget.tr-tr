---
title: İmzalı paketlerin
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426173"
---
# <a name="signed-packages"></a><span data-ttu-id="20fb1-103">İmzalanmış paketler</span><span class="sxs-lookup"><span data-stu-id="20fb1-103">Signed packages</span></span>

<span data-ttu-id="20fb1-104">*NuGet 4.6.0+ ve Visual Studio 2017 sürüm 15.6 ve üzeri*</span><span class="sxs-lookup"><span data-stu-id="20fb1-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="20fb1-105">NuGet paketlerini, üzerinde oynanmış bir içerik karşı koruma sağlayan dijital bir imza içerebilir.</span><span class="sxs-lookup"><span data-stu-id="20fb1-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="20fb1-106">Bu imza de gerçek paket kaynağı için kimlik doğrulaması kanıtları ekleyen bir X.509 Sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="20fb1-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="20fb1-107">İmzalanmış paketleri güçlü bir uçtan uca doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="20fb1-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="20fb1-108">NuGet imzaları iki farklı tür vardır:</span><span class="sxs-lookup"><span data-stu-id="20fb1-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="20fb1-109">**Yazar imza**.</span><span class="sxs-lookup"><span data-stu-id="20fb1-109">**Author Signature**.</span></span> <span data-ttu-id="20fb1-110">Bir yazar imzası yazarı paketin olursa olsun gelen upraven'ın paket değiştirilmedi garanti eder, depo veya ne paket teslim yöntemi taşıma.</span><span class="sxs-lookup"><span data-stu-id="20fb1-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="20fb1-111">Ayrıca, imzalama sertifikasının önceden kayıtlı olması gerekir çünkü Yazar imzalanmış paketleri nuget.org yayımlama işlem hattı için ek kimlik doğrulama mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="20fb1-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="20fb1-112">Daha fazla bilgi için [kayıt sertifikaları](#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="20fb1-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="20fb1-113">**Depo imza**.</span><span class="sxs-lookup"><span data-stu-id="20fb1-113">**Repository Signature**.</span></span> <span data-ttu-id="20fb1-114">Depo imzaları sağlamak için bir bütünlük garantisi **tüm** bile bu paketleri nerede oldukları özgün deposu farklı bir konumdan elde edilen yazar, imzalanmış olup bir depoda paketleri imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="20fb1-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="20fb1-115">Bir yazar imzalı paket oluşturma hakkında daha fazla bilgi edinmek için bkz. [imzalama paketleri](../create-packages/Sign-a-package.md) ve [nuget oturum komutu](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="20fb1-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="20fb1-116">Paket imzalama, şu anda yalnızca nuget.exe Windows üzerinde kullanılırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="20fb1-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="20fb1-117">İmzalı paketlerin doğrulama şu anda yalnızca, Windows üzerinde nuget.exe veya Visual Studio kullanılırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="20fb1-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="20fb1-118">Sertifika gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="20fb1-118">Certificate requirements</span></span>

<span data-ttu-id="20fb1-119">Paket imzalama gerektiren bir kod imzalama sertifikası, özel bir türü için geçerli sertifika olan `id-kp-codeSigning` amaçlı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="20fb1-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="20fb1-120">Ayrıca, sertifika bir RSA ortak anahtar uzunluğu 2048 bit ya da daha yüksek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="20fb1-121">Zaman damgası gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="20fb1-121">Timestamp requirements</span></span>

<span data-ttu-id="20fb1-122">İmzalanmış paketleri paketi imzalama sertifikasının geçerlilik süresini aşan geçerlilik imzası emin olmak için bir RFC 3161 zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="20fb1-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="20fb1-123">Zaman damgası imzalamak için kullanılan sertifika geçerli olmalıdır `id-kp-timeStamping` amaçlı [[RFC 5280 bölüm 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span><span class="sxs-lookup"><span data-stu-id="20fb1-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="20fb1-124">Ayrıca, sertifika bir RSA ortak anahtar uzunluğu 2048 bit ya da daha yüksek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="20fb1-125">Ek teknik ayrıntılar bulunabilir [imza teknik özellikleri paketini](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span><span class="sxs-lookup"><span data-stu-id="20fb1-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="20fb1-126">Nuget.org imza gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="20fb1-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="20fb1-127">nuget.org imzalı paket kabul etmek için ek gereksinimlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="20fb1-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="20fb1-128">Bir yazar imza birincil imza olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="20fb1-129">Birincil bir imza geçerli tek bir zaman damgası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="20fb1-130">X.509 sertifikaları Yazar imza hem de zaman damgası imzası için:</span><span class="sxs-lookup"><span data-stu-id="20fb1-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="20fb1-131">2048 bit RSA ortak anahtarını olmalıdır veya büyük.</span><span class="sxs-lookup"><span data-stu-id="20fb1-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="20fb1-132">Paket doğrulaması nuget.org üzerindeki her zaman geçerli UTC saati, geçerlilik süresi içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20fb1-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="20fb1-133">Windows üzerinde varsayılan olarak güvenilen bir güvenilir kök yetkilisi zincir şeklinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="20fb1-134">Kendi kendine verilen sertifikalarla imzalanmış paketleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="20fb1-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="20fb1-135">Amacı için geçerli olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="20fb1-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="20fb1-136">İmzalama sertifikası yazar, kod imzalama için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="20fb1-137">Zaman damgası sertifika için zaman damgası geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20fb1-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="20fb1-138">Zaman imzalarken iptal edilmiş olmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="20fb1-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="20fb1-139">(Nuget.org iptal durumunu düzenli aralıklarla yeniden denetler şekilde bu gönderme sırasında knowable olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="20fb1-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="20fb1-140">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="20fb1-140">Related articles</span></span>

- [<span data-ttu-id="20fb1-141">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="20fb1-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="20fb1-142">Paket güven sınırları yönetme</span><span class="sxs-lookup"><span data-stu-id="20fb1-142">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
