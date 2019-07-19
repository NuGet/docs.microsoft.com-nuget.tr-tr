---
title: İmzalı paketler
description: NuGet paket imzalama gereksinimleri.
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: e02b2a241008b1b7096f20b351173fd3df7ed172
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317510"
---
# <a name="signed-packages"></a><span data-ttu-id="19deb-103">İmzalanmış paketler</span><span class="sxs-lookup"><span data-stu-id="19deb-103">Signed packages</span></span>

<span data-ttu-id="19deb-104">*NuGet 4.6.0 + ve Visual Studio 2017 sürüm 15,6 ve üzeri*</span><span class="sxs-lookup"><span data-stu-id="19deb-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="19deb-105">NuGet paketleri, değiştirilen içeriğe karşı koruma sağlayan dijital bir imza içerebilir.</span><span class="sxs-lookup"><span data-stu-id="19deb-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="19deb-106">Bu imza, paketin gerçek kaynağına özgünlük sağlamaları ekleyen bir X. 509.440 sertifikasından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="19deb-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="19deb-107">İmzalı paketler en güçlü uçtan uca doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="19deb-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="19deb-108">İki farklı türde NuGet imzası vardır:</span><span class="sxs-lookup"><span data-stu-id="19deb-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="19deb-109">**Yazar imzası**.</span><span class="sxs-lookup"><span data-stu-id="19deb-109">**Author Signature**.</span></span> <span data-ttu-id="19deb-110">Yazar imzası, paketin, paketin hangi depodan veya hangi taşıma yönteminden bağımsız olarak teslim edildiğini değil, yazar tarafından imzalanmasından bu yana paketin değiştirilmediğinden emin olur.</span><span class="sxs-lookup"><span data-stu-id="19deb-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="19deb-111">Ayrıca, imzalama sertifikasının zaman içinde kaydedilmesi gerektiğinden, yazar imzalı paketler nuget.org yayımlama işlem hattına ek bir kimlik doğrulama mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="19deb-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="19deb-112">Daha fazla bilgi için bkz. [sertifikaları kaydetme](#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="19deb-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="19deb-113">**Depo imzası**.</span><span class="sxs-lookup"><span data-stu-id="19deb-113">**Repository Signature**.</span></span> <span data-ttu-id="19deb-114">Depo imzaları, bu paketlerin İmzalandıkları özgün depodan farklı bir konumdan elde edilse bile, bir depodaki **Tüm** paketlere yönelik bir bütünlük garantisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="19deb-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="19deb-115">Yazar imzalı bir paket oluşturma hakkında ayrıntılı bilgi için bkz. [Imzalama paketleri](../create-packages/Sign-a-package.md) ve [NuGet Sign komutu](../reference/cli-reference/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="19deb-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="19deb-116">Paket imzalama Şu anda yalnızca Windows üzerinde NuGet. exe kullanıldığında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="19deb-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="19deb-117">İmzalanmış paketlerin doğrulanması Şu anda yalnızca NuGet. exe veya Windows üzerinde Visual Studio kullanırken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="19deb-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="19deb-118">Sertifika gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="19deb-118">Certificate requirements</span></span>

<span data-ttu-id="19deb-119">Paket imzalama, `id-kp-codeSigning` amaç [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] için geçerli olan özel bir sertifika türü olan bir kod imzalama sertifikası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="19deb-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="19deb-120">Ayrıca, sertifikanın RSA ortak anahtar uzunluğu 2048 bit veya üzeri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="19deb-121">Zaman damgası gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="19deb-121">Timestamp requirements</span></span>

<span data-ttu-id="19deb-122">İmzalı paketler, imza geçerliliğini paket imza sertifikasının geçerlilik süresinden daha fazla güvence altına almak için bir RFC 3161 zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="19deb-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="19deb-123">Zaman damgasını imzalamak için kullanılan sertifika, `id-kp-timeStamping` amaç [[RFC 5280 Section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="19deb-124">Ayrıca, sertifikanın RSA ortak anahtar uzunluğu 2048 bit veya üzeri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="19deb-125">Ek teknik ayrıntılar, [paket imzası teknik özellikleri](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) 'nde (GitHub) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="19deb-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="19deb-126">NuGet.org üzerindeki imza gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="19deb-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="19deb-127">nuget.org, imzalı bir paketi kabul etmek için ek gereksinimlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="19deb-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="19deb-128">Birincil imza bir yazar imzası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="19deb-129">Birincil imza tek bir geçerli zaman damgasına sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="19deb-130">Yazar imzası ve onun zaman damgası imzası için X. 509.440 sertifikaları:</span><span class="sxs-lookup"><span data-stu-id="19deb-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="19deb-131">Bir RSA ortak anahtarı 2048 bit veya daha büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="19deb-132">Nuget.org üzerinde paket doğrulama sırasında geçerli UTC saati başına geçerlilik süresi içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="19deb-133">, Windows 'ta varsayılan olarak güvenilen bir güvenilen kök yetkiliye zincirlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="19deb-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="19deb-134">Kendi kendine verilen sertifikalarla imzalanmış paketler reddedilir.</span><span class="sxs-lookup"><span data-stu-id="19deb-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="19deb-135">Amacı için geçerli olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="19deb-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="19deb-136">Yazar imza sertifikası kod imzalama için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="19deb-137">Zaman damgası sertifikası damgalama için geçerli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="19deb-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="19deb-138">İmza zamanında iptal edilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="19deb-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="19deb-139">(Bu, Gönderim zamanında bu şekilde bilmeyebilir, bu nedenle nuget.org düzenli olarak iptal durumunu denetler).</span><span class="sxs-lookup"><span data-stu-id="19deb-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="19deb-140">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="19deb-140">Related articles</span></span>

- [<span data-ttu-id="19deb-141">NuGet paketleri imzalanıyor</span><span class="sxs-lookup"><span data-stu-id="19deb-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="19deb-142">Paket güven sınırlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="19deb-142">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
