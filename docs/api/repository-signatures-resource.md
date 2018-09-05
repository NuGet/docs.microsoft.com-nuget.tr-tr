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
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547987"
---
# <a name="repository-signatures"></a><span data-ttu-id="96239-103">Depo imzaları</span><span class="sxs-lookup"><span data-stu-id="96239-103">Repository signatures</span></span>

<span data-ttu-id="96239-104">Paket kaynağı yayımlanan paketleri ekleme deposu imza destekliyorsa, paket kaynağı tarafından kullanılan İmzalama sertifikaları belirlemek bir istemci için mümkündür.</span><span class="sxs-lookup"><span data-stu-id="96239-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="96239-105">Bu kaynak, bir depo imzalanmış olup olmadığını paket değiştirilmediğini veya beklenmeyen bir imzalama sertifikası olan algılamak etmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="96239-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="96239-106">Bu depo imza bilgileri getirmek için kullanılan kaynak `RepositorySignatures` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="96239-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="96239-107">NuGet.org Duyurusu başlayacak `RepositorySignatures` yakın gelecekte kaynak.</span><span class="sxs-lookup"><span data-stu-id="96239-107">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="96239-108">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="96239-108">Versioning</span></span>

<span data-ttu-id="96239-109">Aşağıdaki `@type` değeri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="96239-109">The following `@type` value is used:</span></span>

<span data-ttu-id="96239-110">@type Değer</span><span class="sxs-lookup"><span data-stu-id="96239-110">@type value</span></span>                | <span data-ttu-id="96239-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="96239-111">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="96239-112">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="96239-112">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="96239-113">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="96239-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="96239-114">Temel URL</span><span class="sxs-lookup"><span data-stu-id="96239-114">Base URL</span></span>

<span data-ttu-id="96239-115">Aşağıdaki API'leri için giriş noktası URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri.</span><span class="sxs-lookup"><span data-stu-id="96239-115">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="96239-116">Bu konu başlığı altında yer tutucu URL'yi `{@id}`.</span><span class="sxs-lookup"><span data-stu-id="96239-116">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="96239-117">Diğer kaynaklarının aksine unutmayın `{@id}` HTTPS üzerinden hizmet URL'si gereklidir.</span><span class="sxs-lookup"><span data-stu-id="96239-117">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="96239-118">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="96239-118">HTTP methods</span></span>

<span data-ttu-id="96239-119">Depo imzaları kaynak desteği yalnızca HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.</span><span class="sxs-lookup"><span data-stu-id="96239-119">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="96239-120">Depo imzaları dizini</span><span class="sxs-lookup"><span data-stu-id="96239-120">Repository signatures index</span></span>

<span data-ttu-id="96239-121">Depo imzaları dizin iki bilgi parçasını içerir:</span><span class="sxs-lookup"><span data-stu-id="96239-121">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="96239-122">Bu paket kaynak tarafından atılan bir depo olan alınıp alınmayacağını tüm paketleri kaynak bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="96239-122">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="96239-123">Paketleri imzalamak için paket kaynağı tarafından kullanılan sertifikalar listesi.</span><span class="sxs-lookup"><span data-stu-id="96239-123">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="96239-124">Çoğu durumda, sertifikaların listesini her zaman sadece eklenir.</span><span class="sxs-lookup"><span data-stu-id="96239-124">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="96239-125">Önceki imzalama sertifikasının süresi doldu ve yeni bir imzalama sertifikası kullanmaya başlamak paket kaynağı gerektiğinde yeni sertifikalar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="96239-125">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="96239-126">Listeden bir sertifika kaldırılırsa, kaldırılan imzalama sertifikası ile oluşturulan tüm paket imzaları artık istemci tarafından geçerli kabul edilmesi, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="96239-126">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="96239-127">Bu durumda, paket imzası (ancak mutlaka paket) geçersiz.</span><span class="sxs-lookup"><span data-stu-id="96239-127">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="96239-128">Paketin imzasız olarak yüklemeden istemci ilkesini izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="96239-128">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="96239-129">(Örneğin anahtar güvenliğinin aşılması) sertifika iptal olması durumunda, etkilenen bir sertifika tarafından imzalanmış tüm paketleri yeniden imzalamak için paket kaynağı bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="96239-129">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="96239-130">Ayrıca, paket kaynağına etkilenen sertifika imzalama sertifikası listeden kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96239-130">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="96239-131">Aşağıdaki isteği, depo imzaları dizin getirir.</span><span class="sxs-lookup"><span data-stu-id="96239-131">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="96239-132">Depo imzası aşağıdaki özelliklere sahip bir nesne içeren bir JSON belgesi dizinidir:</span><span class="sxs-lookup"><span data-stu-id="96239-132">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="96239-133">Ad</span><span class="sxs-lookup"><span data-stu-id="96239-133">Name</span></span>                | <span data-ttu-id="96239-134">Tür</span><span class="sxs-lookup"><span data-stu-id="96239-134">Type</span></span>             | <span data-ttu-id="96239-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96239-135">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="96239-136">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="96239-136">allRepositorySigned</span></span> | <span data-ttu-id="96239-137">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="96239-137">boolean</span></span>          | <span data-ttu-id="96239-138">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-138">yes</span></span>
<span data-ttu-id="96239-139">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="96239-139">signingCertificates</span></span> | <span data-ttu-id="96239-140">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="96239-140">array of objects</span></span> | <span data-ttu-id="96239-141">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-141">yes</span></span>

<span data-ttu-id="96239-142">`allRepositorySigned` Paket kaynağı depo imzasına sahip bazı paketler varsa, Boole false olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="96239-142">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="96239-143">Boole true olarak kullanılabilir tüm paketleri ayarlanmışsa kaynak belirtilen İmzalama sertifikaları biri tarafından üretilen bir depo imza içermelidir `signingCertificates`.</span><span class="sxs-lookup"><span data-stu-id="96239-143">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="96239-144">Bir veya daha fazla İmzalama sertifikaları olmalıdır `signingCertificates` , dizi `allRepositorySigned` boolean ayarlanmışsa true.</span><span class="sxs-lookup"><span data-stu-id="96239-144">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="96239-145">Dizi boş ise ve `allRepositorySigned` ayarlamak istemci İlkesi tüketim paketlerin hala izin verebilir ancak true kaynağından tüm paketleri geçersiz düşünülmelidir.</span><span class="sxs-lookup"><span data-stu-id="96239-145">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="96239-146">Bu dizideki her öğe, aşağıdaki özelliklere sahip bir JSON nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="96239-146">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="96239-147">Ad</span><span class="sxs-lookup"><span data-stu-id="96239-147">Name</span></span>         | <span data-ttu-id="96239-148">Tür</span><span class="sxs-lookup"><span data-stu-id="96239-148">Type</span></span>   | <span data-ttu-id="96239-149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96239-149">Required</span></span> | <span data-ttu-id="96239-150">Notlar</span><span class="sxs-lookup"><span data-stu-id="96239-150">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="96239-151">contentUrl</span><span class="sxs-lookup"><span data-stu-id="96239-151">contentUrl</span></span>   | <span data-ttu-id="96239-152">dize</span><span class="sxs-lookup"><span data-stu-id="96239-152">string</span></span> | <span data-ttu-id="96239-153">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-153">yes</span></span>      | <span data-ttu-id="96239-154">DER ile kodlanmış bir ortak sertifika için mutlak URL</span><span class="sxs-lookup"><span data-stu-id="96239-154">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="96239-155">parmak izi</span><span class="sxs-lookup"><span data-stu-id="96239-155">fingerprints</span></span> | <span data-ttu-id="96239-156">nesne</span><span class="sxs-lookup"><span data-stu-id="96239-156">object</span></span> | <span data-ttu-id="96239-157">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-157">yes</span></span>      |
<span data-ttu-id="96239-158">Konu</span><span class="sxs-lookup"><span data-stu-id="96239-158">subject</span></span>      | <span data-ttu-id="96239-159">dize</span><span class="sxs-lookup"><span data-stu-id="96239-159">string</span></span> | <span data-ttu-id="96239-160">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-160">yes</span></span>      | <span data-ttu-id="96239-161">Sertifikadan konu ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="96239-161">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="96239-162">yayınlayan</span><span class="sxs-lookup"><span data-stu-id="96239-162">issuer</span></span>       | <span data-ttu-id="96239-163">dize</span><span class="sxs-lookup"><span data-stu-id="96239-163">string</span></span> | <span data-ttu-id="96239-164">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-164">yes</span></span>      | <span data-ttu-id="96239-165">Sertifikayı verenin ayırt edici ad</span><span class="sxs-lookup"><span data-stu-id="96239-165">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="96239-166">notBefore</span><span class="sxs-lookup"><span data-stu-id="96239-166">notBefore</span></span>    | <span data-ttu-id="96239-167">dize</span><span class="sxs-lookup"><span data-stu-id="96239-167">string</span></span> | <span data-ttu-id="96239-168">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-168">yes</span></span>      | <span data-ttu-id="96239-169">Sertifika geçerlilik döneminin başlangıç zaman damgası</span><span class="sxs-lookup"><span data-stu-id="96239-169">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="96239-170">notAfter</span><span class="sxs-lookup"><span data-stu-id="96239-170">notAfter</span></span>     | <span data-ttu-id="96239-171">dize</span><span class="sxs-lookup"><span data-stu-id="96239-171">string</span></span> | <span data-ttu-id="96239-172">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-172">yes</span></span>      | <span data-ttu-id="96239-173">Sertifika geçerlilik bitiş zaman damgası</span><span class="sxs-lookup"><span data-stu-id="96239-173">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="96239-174">Unutmayın `contentUrl` HTTPS üzerinden sunulmasını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="96239-174">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="96239-175">Bu URL, hiçbir özel URL deseni vardır ve bu depo imza dizin belgesi kullanarak dinamik olarak bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96239-175">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="96239-176">Bu nesnenin tüm özellikleri (aside gelen `contentUrl`) bulunan sertifika derivable olmalıdır `contentUrl`.</span><span class="sxs-lookup"><span data-stu-id="96239-176">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="96239-177">Bu derivable özellikler gidiş dönüş en aza indirmek için bir kolaylık olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="96239-177">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="96239-178">`fingerprints` Nesne, aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="96239-178">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="96239-179">Ad</span><span class="sxs-lookup"><span data-stu-id="96239-179">Name</span></span>                   | <span data-ttu-id="96239-180">Tür</span><span class="sxs-lookup"><span data-stu-id="96239-180">Type</span></span>   | <span data-ttu-id="96239-181">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96239-181">Required</span></span> | <span data-ttu-id="96239-182">Notlar</span><span class="sxs-lookup"><span data-stu-id="96239-182">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="96239-183">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="96239-183">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="96239-184">dize</span><span class="sxs-lookup"><span data-stu-id="96239-184">string</span></span> | <span data-ttu-id="96239-185">Evet</span><span class="sxs-lookup"><span data-stu-id="96239-185">yes</span></span>      | <span data-ttu-id="96239-186">SHA-256'yı parmak izi</span><span class="sxs-lookup"><span data-stu-id="96239-186">The SHA-256 fingerprint</span></span>

<span data-ttu-id="96239-187">Anahtar adı `2.16.840.1.101.3.4.2.1` SHA-256 karma algoritmasını OID.</span><span class="sxs-lookup"><span data-stu-id="96239-187">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="96239-188">Tüm karma değerlerini karma Özet küçük harf, onaltılık kodlanmış dize temsillerini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96239-188">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="96239-189">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="96239-189">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="96239-190">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="96239-190">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
