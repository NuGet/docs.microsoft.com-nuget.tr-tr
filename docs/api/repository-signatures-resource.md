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
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248448"
---
# <a name="repository-signatures"></a><span data-ttu-id="a990c-103">Depo imzaları</span><span class="sxs-lookup"><span data-stu-id="a990c-103">Repository signatures</span></span>

<span data-ttu-id="a990c-104">Paket kaynağı yayımlanan paketleri ekleme deposu imza destekliyorsa, paket kaynağı tarafından kullanılan İmzalama sertifikaları belirlemek bir istemci için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a990c-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="a990c-105">Bu kaynak, bir depo imzalanmış olup olmadığını paket değiştirilmediğini veya beklenmeyen bir imzalama sertifikası olan algılamak etmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a990c-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="a990c-106">Bu depo imza bilgileri getirmek için kullanılan kaynak `RepositorySignatures` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="a990c-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="a990c-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="a990c-107">Versioning</span></span>

<span data-ttu-id="a990c-108">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="a990c-108">The following `@type` value is used:</span></span>

<span data-ttu-id="a990c-109">@type Değer</span><span class="sxs-lookup"><span data-stu-id="a990c-109">@type value</span></span>                | <span data-ttu-id="a990c-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="a990c-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="a990c-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="a990c-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="a990c-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="a990c-112">The initial release</span></span>
<span data-ttu-id="a990c-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="a990c-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="a990c-114">Etkinleştirme sağlar `allRepositorySigned`</span><span class="sxs-lookup"><span data-stu-id="a990c-114">Allows enabling `allRepositorySigned`</span></span>

## <a name="base-url"></a><span data-ttu-id="a990c-115">Temel URL</span><span class="sxs-lookup"><span data-stu-id="a990c-115">Base URL</span></span>

<span data-ttu-id="a990c-116">Aşağıdaki API'leri için giriş noktası URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="a990c-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="a990c-117">Bu konu başlığı altında yer tutucu URL'yi `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="a990c-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="a990c-118">Diğer kaynaklarının aksine unutmayın `{@id}` HTTPS üzerinden hizmet URL'si gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a990c-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a990c-119">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="a990c-119">HTTP methods</span></span>

<span data-ttu-id="a990c-120">Depo imzaları kaynak desteği yalnızca HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="a990c-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="a990c-121">Depo imzaları dizini</span><span class="sxs-lookup"><span data-stu-id="a990c-121">Repository signatures index</span></span>

<span data-ttu-id="a990c-122">Depo imzaları dizin iki bilgi parçasını içerir:</span><span class="sxs-lookup"><span data-stu-id="a990c-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="a990c-123">Bu paket kaynak tarafından atılan bir depo olan alınıp alınmayacağını tüm paketleri kaynak bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a990c-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="a990c-124">Paketleri imzalamak için paket kaynağı tarafından kullanılan sertifikalar listesi.</span><span class="sxs-lookup"><span data-stu-id="a990c-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="a990c-125">Çoğu durumda, sertifikaların listesini her zaman sadece eklenir.</span><span class="sxs-lookup"><span data-stu-id="a990c-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="a990c-126">Önceki imzalama sertifikasının süresi doldu ve yeni bir imzalama sertifikası kullanmaya başlamak paket kaynağı gerektiğinde yeni sertifikalar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="a990c-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="a990c-127">Listeden bir sertifika kaldırılırsa, kaldırılan imzalama sertifikası ile oluşturulan tüm paket imzaları artık istemci tarafından geçerli kabul edilmesi, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a990c-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="a990c-128">Bu durumda, paket imzası (ancak mutlaka paket) geçersiz.</span><span class="sxs-lookup"><span data-stu-id="a990c-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="a990c-129">Paketin imzasız olarak yüklemeden istemci ilkesini izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="a990c-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="a990c-130">(Örneğin anahtar güvenliğinin aşılması) sertifika iptal olması durumunda, etkilenen bir sertifika tarafından imzalanmış tüm paketleri yeniden imzalamak için paket kaynağı bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="a990c-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="a990c-131">Ayrıca, paket kaynağına etkilenen sertifika imzalama sertifikası listeden kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a990c-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="a990c-132">Aşağıdaki isteği, depo imzaları dizin getirir.</span><span class="sxs-lookup"><span data-stu-id="a990c-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="a990c-133">Depo imzası aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi dizinidir:</span><span class="sxs-lookup"><span data-stu-id="a990c-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="a990c-134">Ad</span><span class="sxs-lookup"><span data-stu-id="a990c-134">Name</span></span>                | <span data-ttu-id="a990c-135">Tür</span><span class="sxs-lookup"><span data-stu-id="a990c-135">Type</span></span>             | <span data-ttu-id="a990c-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a990c-136">Required</span></span> | <span data-ttu-id="a990c-137">Notlar</span><span class="sxs-lookup"><span data-stu-id="a990c-137">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="a990c-138">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="a990c-138">allRepositorySigned</span></span> | <span data-ttu-id="a990c-139">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="a990c-139">boolean</span></span>          | <span data-ttu-id="a990c-140">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-140">yes</span></span>      | <span data-ttu-id="a990c-141">Olmalıdır `false` 4.7.0 üzerinde kaynak</span><span class="sxs-lookup"><span data-stu-id="a990c-141">Must be `false` on 4.7.0 resource</span></span>
<span data-ttu-id="a990c-142">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="a990c-142">signingCertificates</span></span> | <span data-ttu-id="a990c-143">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="a990c-143">array of objects</span></span> | <span data-ttu-id="a990c-144">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-144">yes</span></span>      | 

<span data-ttu-id="a990c-145">`allRepositorySigned` Paket kaynağı depo imzasına sahip bazı paketler varsa, Boole false olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a990c-145">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="a990c-146">Boole true olarak kullanılabilir tüm paketleri ayarlanmışsa kaynak belirtilen İmzalama sertifikaları biri tarafından üretilen bir depo imza içermelidir `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="a990c-146">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="a990c-147">`allRepositorySigned` Boole 4.7.0 üzerinde false olmalıdır kaynak.</span><span class="sxs-lookup"><span data-stu-id="a990c-147">The `allRepositorySigned` boolean must be false on the 4.7.0 resource.</span></span> <span data-ttu-id="a990c-148">NuGet v4.7 ve v4.8 istemcileri olan kaynaklardan paketleri yükleyemiyor `allRepositorySigned` true olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="a990c-148">NuGet v4.7 and v4.8 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="a990c-149">Bir veya daha fazla İmzalama sertifikaları olmalıdır `signingCertificates` , dizi `allRepositorySigned` boolean ayarlanmışsa true.</span><span class="sxs-lookup"><span data-stu-id="a990c-149">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="a990c-150">Dizi boş ise ve `allRepositorySigned` ayarlamak istemci İlkesi tüketim paketlerin hala izin verebilir ancak true kaynağından tüm paketleri geçersiz düşünülmelidir.</span><span class="sxs-lookup"><span data-stu-id="a990c-150">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="a990c-151">Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="a990c-151">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="a990c-152">Ad</span><span class="sxs-lookup"><span data-stu-id="a990c-152">Name</span></span>         | <span data-ttu-id="a990c-153">Tür</span><span class="sxs-lookup"><span data-stu-id="a990c-153">Type</span></span>   | <span data-ttu-id="a990c-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a990c-154">Required</span></span> | <span data-ttu-id="a990c-155">Notlar</span><span class="sxs-lookup"><span data-stu-id="a990c-155">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="a990c-156">contentUrl</span><span class="sxs-lookup"><span data-stu-id="a990c-156">contentUrl</span></span>   | <span data-ttu-id="a990c-157">dize</span><span class="sxs-lookup"><span data-stu-id="a990c-157">string</span></span> | <span data-ttu-id="a990c-158">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-158">yes</span></span>      | <span data-ttu-id="a990c-159">DER ile kodlanmış bir ortak sertifika için mutlak URL</span><span class="sxs-lookup"><span data-stu-id="a990c-159">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="a990c-160">parmak izi</span><span class="sxs-lookup"><span data-stu-id="a990c-160">fingerprints</span></span> | <span data-ttu-id="a990c-161">nesne</span><span class="sxs-lookup"><span data-stu-id="a990c-161">object</span></span> | <span data-ttu-id="a990c-162">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-162">yes</span></span>      |
<span data-ttu-id="a990c-163">Konu</span><span class="sxs-lookup"><span data-stu-id="a990c-163">subject</span></span>      | <span data-ttu-id="a990c-164">dize</span><span class="sxs-lookup"><span data-stu-id="a990c-164">string</span></span> | <span data-ttu-id="a990c-165">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-165">yes</span></span>      | <span data-ttu-id="a990c-166">Sertifikadan konu ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="a990c-166">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="a990c-167">yayınlayan</span><span class="sxs-lookup"><span data-stu-id="a990c-167">issuer</span></span>       | <span data-ttu-id="a990c-168">dize</span><span class="sxs-lookup"><span data-stu-id="a990c-168">string</span></span> | <span data-ttu-id="a990c-169">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-169">yes</span></span>      | <span data-ttu-id="a990c-170">Sertifikayı verenin ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="a990c-170">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="a990c-171">notBefore</span><span class="sxs-lookup"><span data-stu-id="a990c-171">notBefore</span></span>    | <span data-ttu-id="a990c-172">dize</span><span class="sxs-lookup"><span data-stu-id="a990c-172">string</span></span> | <span data-ttu-id="a990c-173">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-173">yes</span></span>      | <span data-ttu-id="a990c-174">Sertifika geçerlilik döneminin başlangıç zaman damgası</span><span class="sxs-lookup"><span data-stu-id="a990c-174">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="a990c-175">notAfter</span><span class="sxs-lookup"><span data-stu-id="a990c-175">notAfter</span></span>     | <span data-ttu-id="a990c-176">dize</span><span class="sxs-lookup"><span data-stu-id="a990c-176">string</span></span> | <span data-ttu-id="a990c-177">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-177">yes</span></span>      | <span data-ttu-id="a990c-178">Sertifika geçerlilik bitiş zaman damgası</span><span class="sxs-lookup"><span data-stu-id="a990c-178">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="a990c-179">Unutmayın `contentUrl` HTTPS üzerinden sunulmasını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a990c-179">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="a990c-180">Bu URL, hiçbir özel URL deseni vardır ve bu depo imza dizin belgesi kullanarak dinamik olarak bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a990c-180">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="a990c-181">Bu nesnenin tüm özellikleri (aside gelen `contentUrl`) bulunan sertifika derivable olmalıdır `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="a990c-181">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="a990c-182">Bu derivable özellikler gidiş dönüş en aza indirmek için bir kolaylık olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a990c-182">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="a990c-183">`fingerprints` Nesne, aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a990c-183">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="a990c-184">Ad</span><span class="sxs-lookup"><span data-stu-id="a990c-184">Name</span></span>                   | <span data-ttu-id="a990c-185">Tür</span><span class="sxs-lookup"><span data-stu-id="a990c-185">Type</span></span>   | <span data-ttu-id="a990c-186">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a990c-186">Required</span></span> | <span data-ttu-id="a990c-187">Notlar</span><span class="sxs-lookup"><span data-stu-id="a990c-187">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="a990c-188">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="a990c-188">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="a990c-189">dize</span><span class="sxs-lookup"><span data-stu-id="a990c-189">string</span></span> | <span data-ttu-id="a990c-190">evet</span><span class="sxs-lookup"><span data-stu-id="a990c-190">yes</span></span>      | <span data-ttu-id="a990c-191">SHA-256'yı parmak izi</span><span class="sxs-lookup"><span data-stu-id="a990c-191">The SHA-256 fingerprint</span></span>

<span data-ttu-id="a990c-192">Anahtar adı `2.16.840.1.101.3.4.2.1` SHA-256 karma algoritmasını OID.</span><span class="sxs-lookup"><span data-stu-id="a990c-192">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="a990c-193">Tüm karma değerlerini karma Özet küçük harf, onaltılık kodlanmış dize temsillerini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a990c-193">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a990c-194">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="a990c-194">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="a990c-195">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="a990c-195">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
