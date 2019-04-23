---
title: Depo imzaları, NuGet API'si | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Depo imzaları kaynak istemcilerin kendi depo imzalama özellikleri duyurmaktan paket kaynaklarını sağlar.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59931858"
---
# <a name="repository-signatures"></a><span data-ttu-id="2d890-103">Depo imzaları</span><span class="sxs-lookup"><span data-stu-id="2d890-103">Repository signatures</span></span>

<span data-ttu-id="2d890-104">Paket kaynağı yayımlanan paketleri ekleme deposu imza destekliyorsa, paket kaynağı tarafından kullanılan İmzalama sertifikaları belirlemek bir istemci için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="2d890-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="2d890-105">Bu kaynak, bir depo imzalanmış olup olmadığını paket değiştirilmediğini veya beklenmeyen bir imzalama sertifikası olan algılamak etmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2d890-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="2d890-106">Bu depo imza bilgileri getirmek için kullanılan kaynak `RepositorySignatures` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="2d890-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="2d890-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="2d890-107">Versioning</span></span>

<span data-ttu-id="2d890-108">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="2d890-108">The following `@type` value is used:</span></span>

<span data-ttu-id="2d890-109">@type Değer</span><span class="sxs-lookup"><span data-stu-id="2d890-109">@type value</span></span>                | <span data-ttu-id="2d890-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="2d890-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="2d890-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="2d890-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="2d890-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="2d890-112">The initial release</span></span>
<span data-ttu-id="2d890-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="2d890-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="2d890-114">NuGet v4.9 + istemcileri tarafından desteklenen</span><span class="sxs-lookup"><span data-stu-id="2d890-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="2d890-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="2d890-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="2d890-116">Çalışabilmelerini `allRepositorySigned`.</span><span class="sxs-lookup"><span data-stu-id="2d890-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="2d890-117">NuGet v5.0 + istemcileri tarafından desteklenen</span><span class="sxs-lookup"><span data-stu-id="2d890-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="2d890-118">Temel URL</span><span class="sxs-lookup"><span data-stu-id="2d890-118">Base URL</span></span>

<span data-ttu-id="2d890-119">Aşağıdaki API'leri için giriş noktası URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="2d890-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="2d890-120">Bu konu başlığı altında yer tutucu URL'yi `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="2d890-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="2d890-121">Diğer kaynaklarının aksine unutmayın `{@id}` HTTPS üzerinden hizmet URL'si gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2d890-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="2d890-122">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="2d890-122">HTTP methods</span></span>

<span data-ttu-id="2d890-123">Depo imzaları kaynak desteği yalnızca HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="2d890-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="2d890-124">Depo imzaları dizini</span><span class="sxs-lookup"><span data-stu-id="2d890-124">Repository signatures index</span></span>

<span data-ttu-id="2d890-125">Depo imzaları dizin iki bilgi parçasını içerir:</span><span class="sxs-lookup"><span data-stu-id="2d890-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="2d890-126">Bu paket kaynak tarafından atılan bir depo olan alınıp alınmayacağını tüm paketleri kaynak bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="2d890-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="2d890-127">Paketleri imzalamak için paket kaynağı tarafından kullanılan sertifikalar listesi.</span><span class="sxs-lookup"><span data-stu-id="2d890-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="2d890-128">Çoğu durumda, sertifikaların listesini her zaman sadece eklenir.</span><span class="sxs-lookup"><span data-stu-id="2d890-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="2d890-129">Önceki imzalama sertifikasının süresi doldu ve yeni bir imzalama sertifikası kullanmaya başlamak paket kaynağı gerektiğinde yeni sertifikalar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="2d890-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="2d890-130">Listeden bir sertifika kaldırılırsa, kaldırılan imzalama sertifikası ile oluşturulan tüm paket imzaları artık istemci tarafından geçerli kabul edilmesi, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2d890-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="2d890-131">Bu durumda, paket imzası (ancak mutlaka paket) geçersiz.</span><span class="sxs-lookup"><span data-stu-id="2d890-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="2d890-132">Paketin imzasız olarak yüklemeden istemci ilkesini izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="2d890-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="2d890-133">(Örneğin anahtar güvenliğinin aşılması) sertifika iptal olması durumunda, etkilenen bir sertifika tarafından imzalanmış tüm paketleri yeniden imzalamak için paket kaynağı bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="2d890-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="2d890-134">Ayrıca, paket kaynağına etkilenen sertifika imzalama sertifikası listeden kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d890-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="2d890-135">Aşağıdaki isteği, depo imzaları dizin getirir.</span><span class="sxs-lookup"><span data-stu-id="2d890-135">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="2d890-136">Depo imzası aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi dizinidir:</span><span class="sxs-lookup"><span data-stu-id="2d890-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="2d890-137">Ad</span><span class="sxs-lookup"><span data-stu-id="2d890-137">Name</span></span>                | <span data-ttu-id="2d890-138">Tür</span><span class="sxs-lookup"><span data-stu-id="2d890-138">Type</span></span>             | <span data-ttu-id="2d890-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2d890-139">Required</span></span> | <span data-ttu-id="2d890-140">Notlar</span><span class="sxs-lookup"><span data-stu-id="2d890-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="2d890-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="2d890-141">allRepositorySigned</span></span> | <span data-ttu-id="2d890-142">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="2d890-142">boolean</span></span>          | <span data-ttu-id="2d890-143">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-143">yes</span></span>      | <span data-ttu-id="2d890-144">Olmalıdır `false` 4.7.0 ve 4.9.0 kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2d890-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="2d890-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="2d890-145">signingCertificates</span></span> | <span data-ttu-id="2d890-146">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="2d890-146">array of objects</span></span> | <span data-ttu-id="2d890-147">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-147">yes</span></span>      | 

<span data-ttu-id="2d890-148">`allRepositorySigned` Paket kaynağı depo imzasına sahip bazı paketler varsa, Boole false olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="2d890-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="2d890-149">Boole true olarak kullanılabilir tüm paketleri ayarlanmışsa kaynak belirtilen İmzalama sertifikaları biri tarafından üretilen bir depo imza içermelidir `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="2d890-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="2d890-150">`allRepositorySigned` Boole 4.7.0 ve 4.9.0 kaynaklar üzerinde false olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2d890-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="2d890-151">NuGet v4.7 v4.8 ve v4.9 istemcileri olan kaynaklardan paketleri yükleyemiyor `allRepositorySigned` true olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="2d890-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="2d890-152">Bir veya daha fazla İmzalama sertifikaları olmalıdır `signingCertificates` , dizi `allRepositorySigned` boolean ayarlanmışsa true.</span><span class="sxs-lookup"><span data-stu-id="2d890-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="2d890-153">Dizi boş ise ve `allRepositorySigned` ayarlamak istemci İlkesi tüketim paketlerin hala izin verebilir ancak true kaynağından tüm paketleri geçersiz düşünülmelidir.</span><span class="sxs-lookup"><span data-stu-id="2d890-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="2d890-154">Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="2d890-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="2d890-155">Ad</span><span class="sxs-lookup"><span data-stu-id="2d890-155">Name</span></span>         | <span data-ttu-id="2d890-156">Tür</span><span class="sxs-lookup"><span data-stu-id="2d890-156">Type</span></span>   | <span data-ttu-id="2d890-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2d890-157">Required</span></span> | <span data-ttu-id="2d890-158">Notlar</span><span class="sxs-lookup"><span data-stu-id="2d890-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="2d890-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="2d890-159">contentUrl</span></span>   | <span data-ttu-id="2d890-160">dize</span><span class="sxs-lookup"><span data-stu-id="2d890-160">string</span></span> | <span data-ttu-id="2d890-161">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-161">yes</span></span>      | <span data-ttu-id="2d890-162">DER ile kodlanmış bir ortak sertifika için mutlak URL</span><span class="sxs-lookup"><span data-stu-id="2d890-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="2d890-163">parmak izi</span><span class="sxs-lookup"><span data-stu-id="2d890-163">fingerprints</span></span> | <span data-ttu-id="2d890-164">nesne</span><span class="sxs-lookup"><span data-stu-id="2d890-164">object</span></span> | <span data-ttu-id="2d890-165">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-165">yes</span></span>      |
<span data-ttu-id="2d890-166">Konu</span><span class="sxs-lookup"><span data-stu-id="2d890-166">subject</span></span>      | <span data-ttu-id="2d890-167">dize</span><span class="sxs-lookup"><span data-stu-id="2d890-167">string</span></span> | <span data-ttu-id="2d890-168">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-168">yes</span></span>      | <span data-ttu-id="2d890-169">Sertifikadan konu ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="2d890-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="2d890-170">yayınlayan</span><span class="sxs-lookup"><span data-stu-id="2d890-170">issuer</span></span>       | <span data-ttu-id="2d890-171">dize</span><span class="sxs-lookup"><span data-stu-id="2d890-171">string</span></span> | <span data-ttu-id="2d890-172">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-172">yes</span></span>      | <span data-ttu-id="2d890-173">Sertifikayı verenin ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="2d890-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="2d890-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="2d890-174">notBefore</span></span>    | <span data-ttu-id="2d890-175">dize</span><span class="sxs-lookup"><span data-stu-id="2d890-175">string</span></span> | <span data-ttu-id="2d890-176">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-176">yes</span></span>      | <span data-ttu-id="2d890-177">Sertifika geçerlilik döneminin başlangıç zaman damgası</span><span class="sxs-lookup"><span data-stu-id="2d890-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="2d890-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="2d890-178">notAfter</span></span>     | <span data-ttu-id="2d890-179">dize</span><span class="sxs-lookup"><span data-stu-id="2d890-179">string</span></span> | <span data-ttu-id="2d890-180">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-180">yes</span></span>      | <span data-ttu-id="2d890-181">Sertifika geçerlilik bitiş zaman damgası</span><span class="sxs-lookup"><span data-stu-id="2d890-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="2d890-182">Unutmayın `contentUrl` HTTPS üzerinden sunulmasını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2d890-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="2d890-183">Bu URL, hiçbir özel URL deseni vardır ve bu depo imza dizin belgesi kullanarak dinamik olarak bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d890-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="2d890-184">Bu nesnenin tüm özellikleri (aside gelen `contentUrl`) bulunan sertifika derivable olmalıdır `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="2d890-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="2d890-185">Bu derivable özellikler gidiş dönüş en aza indirmek için bir kolaylık olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2d890-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="2d890-186">`fingerprints` Nesne, aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="2d890-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="2d890-187">Ad</span><span class="sxs-lookup"><span data-stu-id="2d890-187">Name</span></span>                   | <span data-ttu-id="2d890-188">Tür</span><span class="sxs-lookup"><span data-stu-id="2d890-188">Type</span></span>   | <span data-ttu-id="2d890-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2d890-189">Required</span></span> | <span data-ttu-id="2d890-190">Notlar</span><span class="sxs-lookup"><span data-stu-id="2d890-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="2d890-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="2d890-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="2d890-192">dize</span><span class="sxs-lookup"><span data-stu-id="2d890-192">string</span></span> | <span data-ttu-id="2d890-193">evet</span><span class="sxs-lookup"><span data-stu-id="2d890-193">yes</span></span>      | <span data-ttu-id="2d890-194">SHA-256'yı parmak izi</span><span class="sxs-lookup"><span data-stu-id="2d890-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="2d890-195">Anahtar adı `2.16.840.1.101.3.4.2.1` SHA-256 karma algoritmasını OID.</span><span class="sxs-lookup"><span data-stu-id="2d890-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="2d890-196">Tüm karma değerlerini karma Özet küçük harf, onaltılık kodlanmış dize temsillerini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d890-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="2d890-197">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="2d890-197">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="2d890-198">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="2d890-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
