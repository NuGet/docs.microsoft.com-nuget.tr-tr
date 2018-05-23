---
title: NuGet paketlerini imzalama
description: İmzalı Paketleri açıklar içerik bütünlüğü doğrulamasını etkinleştirmek için kullanılabilir.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9900db1970a89de129d9074e5900e0aa048101de
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="e7251-103">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="e7251-103">Signing NuGet Packages</span></span>

<span data-ttu-id="e7251-104">Paket imzalama paket oluşturulduktan sonra değiştirilmediğinden emin yapan bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="e7251-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7251-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e7251-105">Prerequisites</span></span>

1. <span data-ttu-id="e7251-106">Paketi (bir `.nupkg` dosyası) imzalamak için.</span><span class="sxs-lookup"><span data-stu-id="e7251-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="e7251-107">Bkz: [paket oluşturma](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e7251-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="e7251-108">nuget.exe 4.6.0 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="e7251-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="e7251-109">Bkz: nasıl yapılır [NuGet CLI'yı yükleme](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="e7251-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="e7251-110">[Bir kod imzalama sertifikası](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="e7251-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="e7251-111">Bir paket imzalama</span><span class="sxs-lookup"><span data-stu-id="e7251-111">Sign a package</span></span>

<span data-ttu-id="e7251-112">Bir paketi imzalamak için kullanın [nuget oturum](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="e7251-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="e7251-113">Komut Başvurusu'nda açıklandığı gibi sertifika deposunda mevcut bir sertifika kullanmak ya da bir dosyadan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="e7251-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="e7251-114">Paket imzalama genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="e7251-114">Common problems when signing a package</span></span>

- <span data-ttu-id="e7251-115">Sertifika, kod imzalama için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="e7251-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="e7251-116">Genişletilmiş Anahtar Kullanımı (EKU 1.3.6.1.5.5.7.3.3) belirtilen sertifika uygun sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7251-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="e7251-117">Sertifika anahtar 2048 bit RSA SHA-256 imza algoritması ya da bir ortak gibi temel gereksinimleri karşılamadığı veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="e7251-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="e7251-118">Sertifikanın süresi doldu veya iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="e7251-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="e7251-119">Zaman damgası sunucusu sertifika gereksinimlerini karşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="e7251-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="e7251-120">İmzalı Paketleri imzalama sertifikasının süresi dolan imza geçerli kaldığı emin olmak için bir zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e7251-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="e7251-121">Oturum işlemi üreten bir [NU3002 uyarı](../reference/Errors-and-Warnings.md#nu3002) bir zaman damgası imzalarken.</span><span class="sxs-lookup"><span data-stu-id="e7251-121">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="e7251-122">İmzalı bir paket doğrulayın</span><span class="sxs-lookup"><span data-stu-id="e7251-122">Verify a signed package</span></span>

<span data-ttu-id="e7251-123">Kullanım [nuget doğrulayın](../tools/cli-ref-verify.md) belirli bir paket imza ayrıntılarını görmek için:</span><span class="sxs-lookup"><span data-stu-id="e7251-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="e7251-124">İmzalı paketini yükle</span><span class="sxs-lookup"><span data-stu-id="e7251-124">Install a signed package</span></span>

<span data-ttu-id="e7251-125">İmzalı Paketleri yüklenmesi için belirli bir işlem gerekmez; İçerik imzalandığından bu yana değiştirildi, ancak yükleme olması bloke ve üreten bir [hata NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="e7251-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="e7251-126">Güvenilmeyen Sertifikalar ile imzalanan paketleri olarak kabul edilir olarak imzalanmamış ve uyarı veya hata imzasız herhangi bir paket gibi olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e7251-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="e7251-127">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e7251-127">See also</span></span>

[<span data-ttu-id="e7251-128">Paketleri başvuru imzalı</span><span class="sxs-lookup"><span data-stu-id="e7251-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
