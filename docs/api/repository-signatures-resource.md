---
title: Depo Imzaları, NuGet API | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: Depo imzaları kaynağı, istemci paket kaynaklarının depo imzalama yeteneklerini duyurmasını sağlar.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775329"
---
# <a name="repository-signatures"></a><span data-ttu-id="20350-103">Depo imzaları</span><span class="sxs-lookup"><span data-stu-id="20350-103">Repository signatures</span></span>

<span data-ttu-id="20350-104">Bir paket kaynağı yayımlanan paketlere depo imzaları eklemeyi destekliyorsa, istemci, paket kaynağı tarafından kullanılan imzalama sertifikalarını tespit etmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="20350-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="20350-105">Bu kaynak, istemcilerin depo imzalı bir paketin değiştirilmediğini veya beklenmedik bir imzalama sertifikasına sahip olup olmadığını algılamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="20350-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="20350-106">Bu depo imza bilgilerini getirmek için kullanılan kaynak, `RepositorySignatures` [hizmet dizininde](service-index.md)bulunan kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="20350-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="20350-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="20350-107">Versioning</span></span>

<span data-ttu-id="20350-108">Aşağıdaki `@type` değer kullanılır:</span><span class="sxs-lookup"><span data-stu-id="20350-108">The following `@type` value is used:</span></span>

<span data-ttu-id="20350-109">@type deeri</span><span class="sxs-lookup"><span data-stu-id="20350-109">@type value</span></span>                | <span data-ttu-id="20350-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="20350-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="20350-111">Imza/4.7.0</span><span class="sxs-lookup"><span data-stu-id="20350-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="20350-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="20350-112">The initial release</span></span>
<span data-ttu-id="20350-113">Imza/4.9.0</span><span class="sxs-lookup"><span data-stu-id="20350-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="20350-114">NuGet v 4.9 + istemcileri tarafından desteklenir</span><span class="sxs-lookup"><span data-stu-id="20350-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="20350-115">Imza/5.0.0</span><span class="sxs-lookup"><span data-stu-id="20350-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="20350-116">Etkinleştirmeye izin verir `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="20350-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="20350-117">NuGet v 5.0 + istemcileri tarafından desteklenir</span><span class="sxs-lookup"><span data-stu-id="20350-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="20350-118">Temel URL</span><span class="sxs-lookup"><span data-stu-id="20350-118">Base URL</span></span>

<span data-ttu-id="20350-119">Aşağıdaki API 'Ler için giriş noktası URL 'SI, `@id` belirtilen kaynak değeriyle ilişkili özelliğin değeridir `@type` .</span><span class="sxs-lookup"><span data-stu-id="20350-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="20350-120">Bu konu, yer tutucu URL 'sini kullanır `{@id}` .</span><span class="sxs-lookup"><span data-stu-id="20350-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="20350-121">Diğer kaynakların aksine, `{@id}` URL 'nın https üzerinden sunulması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="20350-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="20350-122">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="20350-122">HTTP methods</span></span>

<span data-ttu-id="20350-123">Depo imzaları kaynağında bulunan tüm URL 'Ler yalnızca HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="20350-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="20350-124">Depo imzaları dizini</span><span class="sxs-lookup"><span data-stu-id="20350-124">Repository signatures index</span></span>

<span data-ttu-id="20350-125">Depo imzaları dizini iki parça bilgi içerir:</span><span class="sxs-lookup"><span data-stu-id="20350-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="20350-126">Kaynakta bulunan tüm paketlerin, bu paket kaynağı tarafından imzalanmış depo olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="20350-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="20350-127">Paket kaynağı tarafından paketleri imzalamak için kullanılan sertifikaların listesi.</span><span class="sxs-lookup"><span data-stu-id="20350-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="20350-128">Çoğu durumda, sertifika listesi yalnızca öğesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="20350-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="20350-129">Önceki imza sertifikasının süresi dolduğunda ve paket kaynağının yeni bir imzalama sertifikası kullanmaya başlaması gerektiğinde listeye yeni sertifikalar eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="20350-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="20350-130">Bir sertifika listeden kaldırılırsa, bu, kaldırılan imzalama sertifikasıyla oluşturulan tüm paket imzalarının artık istemci tarafından geçerli kabul edilmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="20350-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="20350-131">Bu durumda, paket imzası (ancak paket olması gerekmez) geçersiz olur.</span><span class="sxs-lookup"><span data-stu-id="20350-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="20350-132">İstemci ilkesi, paketin imzasız olarak yüklenmesine izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="20350-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="20350-133">Sertifika iptali durumunda (örn. Anahtar Uzlaşması), paket kaynağının etkilenen sertifika tarafından imzalanan tüm paketlerin yeniden imzalanması beklenir.</span><span class="sxs-lookup"><span data-stu-id="20350-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="20350-134">Ayrıca, paket kaynağının etkilenen sertifikayı imzalama sertifikası listesinden kaldırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20350-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="20350-135">Aşağıdaki istek depo imzaları dizinini getirir.</span><span class="sxs-lookup"><span data-stu-id="20350-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="20350-136">Depo imza dizini, aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesidir:</span><span class="sxs-lookup"><span data-stu-id="20350-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="20350-137">Ad</span><span class="sxs-lookup"><span data-stu-id="20350-137">Name</span></span>                | <span data-ttu-id="20350-138">Tür</span><span class="sxs-lookup"><span data-stu-id="20350-138">Type</span></span>             | <span data-ttu-id="20350-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="20350-139">Required</span></span> | <span data-ttu-id="20350-140">Notlar</span><span class="sxs-lookup"><span data-stu-id="20350-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="20350-141">Alldepotorsigned</span><span class="sxs-lookup"><span data-stu-id="20350-141">allRepositorySigned</span></span> | <span data-ttu-id="20350-142">boolean</span><span class="sxs-lookup"><span data-stu-id="20350-142">boolean</span></span>          | <span data-ttu-id="20350-143">evet</span><span class="sxs-lookup"><span data-stu-id="20350-143">yes</span></span>      | <span data-ttu-id="20350-144">`false`4.7.0 ve 4.9.0 kaynaklarında olmalıdır</span><span class="sxs-lookup"><span data-stu-id="20350-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="20350-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="20350-145">signingCertificates</span></span> | <span data-ttu-id="20350-146">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="20350-146">array of objects</span></span> | <span data-ttu-id="20350-147">evet</span><span class="sxs-lookup"><span data-stu-id="20350-147">yes</span></span>      | 

<span data-ttu-id="20350-148">`allRepositorySigned`Paket kaynağında depo imzası olmayan bazı paketler varsa, Boole değeri false olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="20350-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="20350-149">Boole değeri true olarak ayarlanırsa, kaynakta bulunan tüm paketlerin, içinde bahsedilen imzalama sertifikalarından biri tarafından üretilmiş bir depo imzası olması gerekir `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="20350-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="20350-150">`allRepositorySigned`4.7.0 ve 4.9.0 kaynaklarında Boole değeri false olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20350-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="20350-151">NuGet v 4.7, v 4.8 ve v 4.9 istemcileri, `allRepositorySigned` doğru olarak ayarlanmış kaynaklardan paket yükleyemez.</span><span class="sxs-lookup"><span data-stu-id="20350-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="20350-152">`signingCertificates`Boole değeri true olarak ayarlandıysa dizide bir veya daha fazla imzalama sertifikası olması gerekir `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="20350-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="20350-153">Dizi boşsa ve `allRepositorySigned` true olarak ayarlanırsa, bir istemci ilkesi paketlerin tüketimine izin verebilir olmasına rağmen kaynaktaki tüm paketlerin geçersiz kabul edilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="20350-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="20350-154">Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="20350-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="20350-155">Ad</span><span class="sxs-lookup"><span data-stu-id="20350-155">Name</span></span>         | <span data-ttu-id="20350-156">Tür</span><span class="sxs-lookup"><span data-stu-id="20350-156">Type</span></span>   | <span data-ttu-id="20350-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="20350-157">Required</span></span> | <span data-ttu-id="20350-158">Notlar</span><span class="sxs-lookup"><span data-stu-id="20350-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="20350-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="20350-159">contentUrl</span></span>   | <span data-ttu-id="20350-160">string</span><span class="sxs-lookup"><span data-stu-id="20350-160">string</span></span> | <span data-ttu-id="20350-161">evet</span><span class="sxs-lookup"><span data-stu-id="20350-161">yes</span></span>      | <span data-ttu-id="20350-162">DER kodlu ortak sertifikaya yönelik mutlak URL</span><span class="sxs-lookup"><span data-stu-id="20350-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="20350-163">parmak izlerini</span><span class="sxs-lookup"><span data-stu-id="20350-163">fingerprints</span></span> | <span data-ttu-id="20350-164">object</span><span class="sxs-lookup"><span data-stu-id="20350-164">object</span></span> | <span data-ttu-id="20350-165">evet</span><span class="sxs-lookup"><span data-stu-id="20350-165">yes</span></span>      |
<span data-ttu-id="20350-166">subject</span><span class="sxs-lookup"><span data-stu-id="20350-166">subject</span></span>      | <span data-ttu-id="20350-167">string</span><span class="sxs-lookup"><span data-stu-id="20350-167">string</span></span> | <span data-ttu-id="20350-168">evet</span><span class="sxs-lookup"><span data-stu-id="20350-168">yes</span></span>      | <span data-ttu-id="20350-169">Sertifikadan konu ayırt edici adı</span><span class="sxs-lookup"><span data-stu-id="20350-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="20350-170">yayınlayan</span><span class="sxs-lookup"><span data-stu-id="20350-170">issuer</span></span>       | <span data-ttu-id="20350-171">string</span><span class="sxs-lookup"><span data-stu-id="20350-171">string</span></span> | <span data-ttu-id="20350-172">evet</span><span class="sxs-lookup"><span data-stu-id="20350-172">yes</span></span>      | <span data-ttu-id="20350-173">Sertifikanın verenin ayırt edici adı</span><span class="sxs-lookup"><span data-stu-id="20350-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="20350-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="20350-174">notBefore</span></span>    | <span data-ttu-id="20350-175">string</span><span class="sxs-lookup"><span data-stu-id="20350-175">string</span></span> | <span data-ttu-id="20350-176">evet</span><span class="sxs-lookup"><span data-stu-id="20350-176">yes</span></span>      | <span data-ttu-id="20350-177">Sertifikanın geçerlilik döneminin başlangıç zaman damgası</span><span class="sxs-lookup"><span data-stu-id="20350-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="20350-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="20350-178">notAfter</span></span>     | <span data-ttu-id="20350-179">string</span><span class="sxs-lookup"><span data-stu-id="20350-179">string</span></span> | <span data-ttu-id="20350-180">evet</span><span class="sxs-lookup"><span data-stu-id="20350-180">yes</span></span>      | <span data-ttu-id="20350-181">Sertifikanın geçerlilik döneminin bitiş zaman damgası</span><span class="sxs-lookup"><span data-stu-id="20350-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="20350-182">`contentUrl`Https üzerinden sunulması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="20350-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="20350-183">Bu URL 'nin belirli bir URL kalıbı yok ve bu depo imzaları Dizin belgesi kullanılarak dinamik olarak bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20350-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="20350-184">Bu nesnedeki tüm özelliklerin (bir kenara `contentUrl` ), konumunda bulunan sertifikadan alınabilir olması gerekir `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="20350-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="20350-185">Bu derikaydedilebilir özellikler, gidiş dönüşlerin en aza indirilmesine yönelik kolaylık olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="20350-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="20350-186">`fingerprints`Nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="20350-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="20350-187">Ad</span><span class="sxs-lookup"><span data-stu-id="20350-187">Name</span></span>                   | <span data-ttu-id="20350-188">Tür</span><span class="sxs-lookup"><span data-stu-id="20350-188">Type</span></span>   | <span data-ttu-id="20350-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="20350-189">Required</span></span> | <span data-ttu-id="20350-190">Notlar</span><span class="sxs-lookup"><span data-stu-id="20350-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="20350-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="20350-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="20350-192">string</span><span class="sxs-lookup"><span data-stu-id="20350-192">string</span></span> | <span data-ttu-id="20350-193">evet</span><span class="sxs-lookup"><span data-stu-id="20350-193">yes</span></span>      | <span data-ttu-id="20350-194">SHA-256 parmak izi</span><span class="sxs-lookup"><span data-stu-id="20350-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="20350-195">Anahtar adı, `2.16.840.1.101.3.4.2.1` SHA-256 karma ALGORITMASıNıN OID 'dir.</span><span class="sxs-lookup"><span data-stu-id="20350-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="20350-196">Tüm karma değerleri, karma özetinin küçük, onaltılı kodlanmış dize temsilleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20350-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="20350-197">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="20350-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="20350-198">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="20350-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
