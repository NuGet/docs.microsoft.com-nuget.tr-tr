---
title: NuGet paketlerini imzalama
description: İmzalı paketlerin açıklar içerik bütünlüğünü doğrulamayı etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793586"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="e377b-103">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="e377b-103">Signing NuGet Packages</span></span>

<span data-ttu-id="e377b-104">Paket imzalama paket oluşturulduktan sonra değiştirilmediğinden emin yapan bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="e377b-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e377b-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e377b-105">Prerequisites</span></span>

1. <span data-ttu-id="e377b-106">Paket (bir `.nupkg` dosya) oturum açmak için.</span><span class="sxs-lookup"><span data-stu-id="e377b-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="e377b-107">Bkz: [paket oluşturma](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e377b-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="e377b-108">nuget.exe 4.6.0 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="e377b-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="e377b-109">Bkz. nasıl [NuGet CLI'yı yükleme](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="e377b-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="e377b-110">[Bir kod imzalama sertifikası](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="e377b-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="e377b-111">Bir paket imzalama</span><span class="sxs-lookup"><span data-stu-id="e377b-111">Sign a package</span></span>

<span data-ttu-id="e377b-112">Bir paketi imzalamak için kullanmak [nuget oturum](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="e377b-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="e377b-113">Komut Başvurusu içinde açıklandığı gibi sertifika deposunda mevcut bir sertifika kullanın ya da bir dosyadan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="e377b-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="e377b-114">Paket imzalama karşılaşılan yaygın sorunlar</span><span class="sxs-lookup"><span data-stu-id="e377b-114">Common problems when signing a package</span></span>

- <span data-ttu-id="e377b-115">Sertifika, kod imzalama için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="e377b-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="e377b-116">Belirtilen sertifika genişletilmiş anahtar kullanımı (EKU 1.3.6.1.5.5.7.3.3) uygun olan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e377b-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="e377b-117">Sertifika anahtar 2048 bit RSA SHA-256'yı imza algoritması veya bir genel gibi temel gereksinimleri karşılamadığı veya büyük.</span><span class="sxs-lookup"><span data-stu-id="e377b-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="e377b-118">Sertifikanın süresi doldu veya iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="e377b-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="e377b-119">Zaman damgası sunucusu, sertifika gereksinimleri karşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="e377b-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="e377b-120">İmzalanmış paketleri imzalama sertifikasının süresi dolduğunda imzanın geçerli olacağı emin olmak için bir zaman damgasını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e377b-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="e377b-121">Oturum işlemi üreten bir [NU3002 uyarı](../reference/errors-and-warnings/NU3002.md) bir zaman damgası oturum açarken.</span><span class="sxs-lookup"><span data-stu-id="e377b-121">The sign operation produce a [warning NU3002](../reference/errors-and-warnings/NU3002.md) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="e377b-122">İmzalı paket doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e377b-122">Verify a signed package</span></span>

<span data-ttu-id="e377b-123">Kullanım [nuget doğrulayın](../tools/cli-ref-verify.md) belirli bir paket imza ayrıntılarını görmek için:</span><span class="sxs-lookup"><span data-stu-id="e377b-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="e377b-124">İmzalı paket yükleme</span><span class="sxs-lookup"><span data-stu-id="e377b-124">Install a signed package</span></span>

<span data-ttu-id="e377b-125">İmzalı paketlerin yüklenmesi için herhangi bir özel işlem gerektirmez; Ancak, içeriği imzalandıktan sonra değiştirilmiş, yükleme engellenir ve üreten bir [hata NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="e377b-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked and produces an [error NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="e377b-126">Güvenilmeyen Sertifikalar ile imzalanmış paketleri olarak kabul edilir olarak imzalanmamış ve uyarıları veya hataları gibi diğer herhangi bir işaretsiz paket olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e377b-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="e377b-127">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e377b-127">See also</span></span>

[<span data-ttu-id="e377b-128">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="e377b-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
