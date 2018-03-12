---
title: NuGet paketlerini imzalama | Microsoft Docs
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "İmzalı Paketleri açıklar içerik bütünlüğü doğrulamasını etkinleştirmek için kullanılabilir."
keywords: "İmzalama, NuGet güvenlik, imzalı paketleri oluşturma NuGet paketi"
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: 226b2af13a4559dfc7266e941617dca25ccd2245
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="c21e8-104">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="c21e8-104">Signing NuGet Packages</span></span>

<span data-ttu-id="c21e8-105">Paket imzalama paket oluşturulduktan sonra değiştirilmediğinden emin yapan bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="c21e8-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c21e8-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c21e8-106">Prerequisites</span></span>

1. <span data-ttu-id="c21e8-107">Paketi (bir `.nupkg` dosyası) imzalamak için.</span><span class="sxs-lookup"><span data-stu-id="c21e8-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="c21e8-108">Bkz: [paket oluşturma](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="c21e8-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="c21e8-109">nuget.exe 4.6.0 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c21e8-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="c21e8-110">Bkz: nasıl yapılır [NuGet CLI'yı yükleme](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="c21e8-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="c21e8-111">[Bir kod imzalama sertifikası](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="c21e8-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="c21e8-112">NuGet.org imzalı paketleri şu anda kabul etmiyor.</span><span class="sxs-lookup"><span data-stu-id="c21e8-112">NuGet.org does not currently accept signed packages.</span></span> <span data-ttu-id="c21e8-113">Paketleri yayımlama özel akışları için oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c21e8-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="c21e8-114">Bir paket imzalama</span><span class="sxs-lookup"><span data-stu-id="c21e8-114">Sign a package</span></span>

<span data-ttu-id="c21e8-115">Bir paketi imzalamak için kullanın [nuget oturum](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="c21e8-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="c21e8-116">Komut Başvurusu'nda açıklandığı gibi sertifika deposunda mevcut bir sertifika kullanmak ya da bir dosyadan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="c21e8-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="c21e8-117">Paket imzalama genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="c21e8-117">Common problems when signing a package</span></span>

- <span data-ttu-id="c21e8-118">Sertifika, kod imzalama için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="c21e8-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="c21e8-119">Genişletilmiş Anahtar Kullanımı (EKU 1.3.6.1.5.5.7.3.3) belirtilen sertifika uygun sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c21e8-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="c21e8-120">Sertifika anahtar 2048 bit RSA SHA-256 imza algoritması ya da bir ortak gibi temel gereksinimleri karşılamadığı veya daha büyük.</span><span class="sxs-lookup"><span data-stu-id="c21e8-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="c21e8-121">Sertifikanın süresi doldu veya iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="c21e8-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="c21e8-122">Zaman damgası sunucusu sertifika gereksinimlerini karşılamıyor.</span><span class="sxs-lookup"><span data-stu-id="c21e8-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="c21e8-123">İmzalı Paketleri imzalama sertifikasının süresi dolan imza geçerli kaldığı emin olmak için bir zaman damgası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c21e8-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="c21e8-124">Oturum işlemi üreten bir [NU3002 uyarı](../reference/Errors-and-Warnings.md#nu3002) bir zaman damgası imzalarken.</span><span class="sxs-lookup"><span data-stu-id="c21e8-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="c21e8-125">İmzalı bir paket doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c21e8-125">Verify a signed package</span></span>

<span data-ttu-id="c21e8-126">Kullanım [nuget doğrulayın](../tools/cli-ref-verify.md) belirli bir paket imza ayrıntılarını görmek için:</span><span class="sxs-lookup"><span data-stu-id="c21e8-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="c21e8-127">İmzalı paketini yükle</span><span class="sxs-lookup"><span data-stu-id="c21e8-127">Install a signed package</span></span>

<span data-ttu-id="c21e8-128">İmzalı Paketleri yüklenmesi için belirli bir işlem gerekmez; İçerik imzalandığından bu yana değiştirildi, ancak yükleme olması bloke ve üreten bir [hata NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="c21e8-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="c21e8-129">Güvenilmeyen Sertifikalar ile imzalanan paketleri olarak kabul edilir olarak imzalanmamış ve uyarı veya hata imzasız herhangi bir paket gibi olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="c21e8-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="c21e8-130">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c21e8-130">See also</span></span>

[<span data-ttu-id="c21e8-131">Paketleri başvuru imzalı</span><span class="sxs-lookup"><span data-stu-id="c21e8-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
