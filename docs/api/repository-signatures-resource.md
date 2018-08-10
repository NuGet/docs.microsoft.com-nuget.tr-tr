---
title: Depo imzaları, NuGet API'si | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Depo imzaları kaynak istemcilerin kendi depo imzalama özellikleri duyurmaktan paket kaynaklarını sağlar.
keywords: NuGet API'si depo imzaları, sertifikaları, imzalama nuget.org nuget.org paket imzalama
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 27c572a482fef791f19b3d32e816a41d8dc40b53
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020573"
---
# <a name="repository-signatures"></a><span data-ttu-id="e7c34-104">Depo imzaları</span><span class="sxs-lookup"><span data-stu-id="e7c34-104">Repository signatures</span></span>

<span data-ttu-id="e7c34-105">Paket kaynağı yayımlanan paketleri ekleme deposu imza destekliyorsa, paket kaynağı tarafından kullanılan İmzalama sertifikaları belirlemek bir istemci için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e7c34-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="e7c34-106">Bu kaynak, bir depo imzalanmış olup olmadığını paket değiştirilmediğini veya beklenmeyen bir imzalama sertifikası olan algılamak etmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e7c34-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="e7c34-107">Bu depo imza bilgileri getirmek için kullanılan kaynak `RepositorySignatures` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e7c34-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="e7c34-108">NuGet.org Duyurusu başlayacak `RepositorySignatures` yakın gelecekte kaynak.</span><span class="sxs-lookup"><span data-stu-id="e7c34-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="e7c34-109">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7c34-109">Versioning</span></span>

<span data-ttu-id="e7c34-110">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e7c34-110">The following `@type` value is used:</span></span>

<span data-ttu-id="e7c34-111">@type Değer</span><span class="sxs-lookup"><span data-stu-id="e7c34-111">@type value</span></span>                | <span data-ttu-id="e7c34-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="e7c34-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="e7c34-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="e7c34-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="e7c34-114">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="e7c34-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="e7c34-115">Temel URL</span><span class="sxs-lookup"><span data-stu-id="e7c34-115">Base URL</span></span>

<span data-ttu-id="e7c34-116">Aşağıdaki API'leri için giriş noktası URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="e7c34-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="e7c34-117">Bu konu başlığı altında yer tutucu URL'yi `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="e7c34-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="e7c34-118">Diğer kaynaklarının aksine unutmayın `{@id}` HTTPS üzerinden hizmet URL'si gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e7c34-119">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e7c34-119">HTTP methods</span></span>

<span data-ttu-id="e7c34-120">Depo imzaları kaynak desteği yalnızca HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="e7c34-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="e7c34-121">Depo imzaları dizini</span><span class="sxs-lookup"><span data-stu-id="e7c34-121">Repository signatures index</span></span>

<span data-ttu-id="e7c34-122">Depo imzaları dizin iki bilgi parçasını içerir:</span><span class="sxs-lookup"><span data-stu-id="e7c34-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="e7c34-123">Bu paket kaynak tarafından atılan bir depo olan alınıp alınmayacağını tüm paketleri kaynak bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="e7c34-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="e7c34-124">Paketleri imzalamak için paket kaynağı tarafından kullanılan sertifikalar listesi.</span><span class="sxs-lookup"><span data-stu-id="e7c34-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="e7c34-125">Çoğu durumda, sertifikaların listesini her zaman sadece eklenir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="e7c34-126">Önceki imzalama sertifikasının süresi doldu ve yeni bir imzalama sertifikası kullanmaya başlamak paket kaynağı gerektiğinde yeni sertifikalar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="e7c34-127">Listeden bir sertifika kaldırılırsa, kaldırılan imzalama sertifikası ile oluşturulan tüm paket imzaları artık istemci tarafından geçerli kabul edilmesi, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="e7c34-128">Bu durumda, paket imzası (ancak mutlaka paket) geçersiz.</span><span class="sxs-lookup"><span data-stu-id="e7c34-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="e7c34-129">Paketin imzasız olarak yüklemeden istemci ilkesini izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="e7c34-130">Sertifika iptalini (örneğin anahtar güvenliğinin aşılması) söz konusu olduğunda, paket kaynağı etkilenen sertifika tarafından imzalanmış tüm paketleri çekilmeye beklenir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to resign all packages signed by the affected certificate.</span></span> <span data-ttu-id="e7c34-131">Ayrıca, paket kaynağına etkilenen sertifika imzalama sertifikası listeden kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="e7c34-132">Aşağıdaki isteği, depo imzaları dizin getirir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="e7c34-133">Depo imzası aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi dizinidir:</span><span class="sxs-lookup"><span data-stu-id="e7c34-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="e7c34-134">Ad</span><span class="sxs-lookup"><span data-stu-id="e7c34-134">Name</span></span>                | <span data-ttu-id="e7c34-135">Tür</span><span class="sxs-lookup"><span data-stu-id="e7c34-135">Type</span></span>             | <span data-ttu-id="e7c34-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e7c34-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="e7c34-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="e7c34-137">allRepositorySigned</span></span> | <span data-ttu-id="e7c34-138">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="e7c34-138">boolean</span></span>          | <span data-ttu-id="e7c34-139">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-139">yes</span></span>
<span data-ttu-id="e7c34-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="e7c34-140">signingCertificates</span></span> | <span data-ttu-id="e7c34-141">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="e7c34-141">array of objects</span></span> | <span data-ttu-id="e7c34-142">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-142">yes</span></span>

<span data-ttu-id="e7c34-143">`allRepositorySigned` Paket kaynağı depo imzasına sahip bazı paketler varsa, Boole false olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e7c34-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="e7c34-144">Boole true olarak kullanılabilir tüm paketleri ayarlanmışsa kaynak belirtilen İmzalama sertifikaları biri tarafından üretilen bir depo imza içermelidir `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="e7c34-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="e7c34-145">Bir veya daha fazla İmzalama sertifikaları olmalıdır `signingCertificates` , dizi `allRepositorySigned` boolean ayarlanmışsa true.</span><span class="sxs-lookup"><span data-stu-id="e7c34-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="e7c34-146">Dizi boş ise ve `allRepositorySigned` ayarlamak istemci İlkesi tüketim paketlerin hala izin verebilir ancak true kaynağından tüm paketleri geçersiz düşünülmelidir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="e7c34-147">Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="e7c34-148">Ad</span><span class="sxs-lookup"><span data-stu-id="e7c34-148">Name</span></span>         | <span data-ttu-id="e7c34-149">Tür</span><span class="sxs-lookup"><span data-stu-id="e7c34-149">Type</span></span>   | <span data-ttu-id="e7c34-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e7c34-150">Required</span></span> | <span data-ttu-id="e7c34-151">Notlar</span><span class="sxs-lookup"><span data-stu-id="e7c34-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="e7c34-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="e7c34-152">contentUrl</span></span>   | <span data-ttu-id="e7c34-153">dize</span><span class="sxs-lookup"><span data-stu-id="e7c34-153">string</span></span> | <span data-ttu-id="e7c34-154">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-154">yes</span></span>      | <span data-ttu-id="e7c34-155">DER ile kodlanmış bir ortak sertifika için mutlak URL</span><span class="sxs-lookup"><span data-stu-id="e7c34-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="e7c34-156">parmak izi</span><span class="sxs-lookup"><span data-stu-id="e7c34-156">fingerprints</span></span> | <span data-ttu-id="e7c34-157">nesne</span><span class="sxs-lookup"><span data-stu-id="e7c34-157">object</span></span> | <span data-ttu-id="e7c34-158">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-158">yes</span></span>      |
<span data-ttu-id="e7c34-159">Konu</span><span class="sxs-lookup"><span data-stu-id="e7c34-159">subject</span></span>      | <span data-ttu-id="e7c34-160">dize</span><span class="sxs-lookup"><span data-stu-id="e7c34-160">string</span></span> | <span data-ttu-id="e7c34-161">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-161">yes</span></span>      | <span data-ttu-id="e7c34-162">Sertifikadan konu ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="e7c34-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="e7c34-163">yayınlayan</span><span class="sxs-lookup"><span data-stu-id="e7c34-163">issuer</span></span>       | <span data-ttu-id="e7c34-164">dize</span><span class="sxs-lookup"><span data-stu-id="e7c34-164">string</span></span> | <span data-ttu-id="e7c34-165">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-165">yes</span></span>      | <span data-ttu-id="e7c34-166">Sertifikayı verenin ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="e7c34-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="e7c34-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="e7c34-167">notBefore</span></span>    | <span data-ttu-id="e7c34-168">dize</span><span class="sxs-lookup"><span data-stu-id="e7c34-168">string</span></span> | <span data-ttu-id="e7c34-169">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-169">yes</span></span>      | <span data-ttu-id="e7c34-170">Sertifika geçerlilik döneminin başlangıç zaman damgası</span><span class="sxs-lookup"><span data-stu-id="e7c34-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="e7c34-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="e7c34-171">notAfter</span></span>     | <span data-ttu-id="e7c34-172">dize</span><span class="sxs-lookup"><span data-stu-id="e7c34-172">string</span></span> | <span data-ttu-id="e7c34-173">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-173">yes</span></span>      | <span data-ttu-id="e7c34-174">Sertifika geçerlilik bitiş zaman damgası</span><span class="sxs-lookup"><span data-stu-id="e7c34-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="e7c34-175">Unutmayın `contentUrl` HTTPS üzerinden sunulmasını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="e7c34-176">Bu URL, hiçbir özel URL deseni vardır ve bu depo imza dizin belgesi kullanarak dinamik olarak bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="e7c34-177">Bu nesnenin tüm özellikleri (aside gelen `contentUrl`) bulunan sertifika derivable olmalıdır `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="e7c34-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="e7c34-178">Bu derivable özellikler gidiş dönüş en aza indirmek için bir kolaylık olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e7c34-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="e7c34-179">`fingerprints` Nesne, aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e7c34-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="e7c34-180">Ad</span><span class="sxs-lookup"><span data-stu-id="e7c34-180">Name</span></span>                   | <span data-ttu-id="e7c34-181">Tür</span><span class="sxs-lookup"><span data-stu-id="e7c34-181">Type</span></span>   | <span data-ttu-id="e7c34-182">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e7c34-182">Required</span></span> | <span data-ttu-id="e7c34-183">Notlar</span><span class="sxs-lookup"><span data-stu-id="e7c34-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="e7c34-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="e7c34-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="e7c34-185">dize</span><span class="sxs-lookup"><span data-stu-id="e7c34-185">string</span></span> | <span data-ttu-id="e7c34-186">Evet</span><span class="sxs-lookup"><span data-stu-id="e7c34-186">yes</span></span>      | <span data-ttu-id="e7c34-187">SHA-256'yı parmak izi</span><span class="sxs-lookup"><span data-stu-id="e7c34-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="e7c34-188">Anahtar adı `2.16.840.1.101.3.4.2.1` SHA-256 karma algoritmasını OID.</span><span class="sxs-lookup"><span data-stu-id="e7c34-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="e7c34-189">Tüm karma değerlerini karma Özet küçük harf, onaltılık kodlanmış dize temsillerini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7c34-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e7c34-190">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="e7c34-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="e7c34-191">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="e7c34-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
