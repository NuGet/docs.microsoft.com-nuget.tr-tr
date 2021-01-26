---
title: nuget.org protokolleri
description: NuGet istemcileriyle etkileşimde bulunmak için gelişen nuget.org protokolleri.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773972"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="b39e7-103">nuget.org protokolleri</span><span class="sxs-lookup"><span data-stu-id="b39e7-103">nuget.org protocols</span></span>

<span data-ttu-id="b39e7-104">Nuget.org ile etkileşim kurmak için istemcilerin belirli protokolleri izlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b39e7-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="b39e7-105">Bu protokoller geliştiğinden, istemcilerin belirli nuget.org API 'Lerini çağırırken kullandıkları protokol sürümünü tanımlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b39e7-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="b39e7-106">Bu, nuget.org 'in eski istemciler için kırılmamış bir şekilde değişiklik almasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b39e7-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="b39e7-107">Bu sayfada belgelenen API 'Ler nuget.org 'e özgüdür ve diğer NuGet sunucu uygulamalarının bu API 'Leri tanıtmak için bir beklenmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="b39e7-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="b39e7-108">NuGet ekosistemi genelinde uygulanan NuGet API 'si hakkında daha fazla bilgi için bkz. [API 'ye genel bakış](overview.md).</span><span class="sxs-lookup"><span data-stu-id="b39e7-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="b39e7-109">Bu konuda, çeşitli protokoller ve mevcut olduğunda, bu konular listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b39e7-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="b39e7-110">NuGet protokol sürümü 4.1.0</span><span class="sxs-lookup"><span data-stu-id="b39e7-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="b39e7-111">4.1.0 protokolü, bir paketi nuget.org hesabına karşı doğrulamak için nuget.org dışındaki hizmetlerle etkileşimde bulunmak üzere Verify-Scope anahtarlarının kullanımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b39e7-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="b39e7-112">`4.1.0`Sürüm numarasının donuk bir dize olduğunu, ancak bu protokolü destekleyen resmi NuGet istemcisinin ilk sürümüyle kesişeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b39e7-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="b39e7-113">Doğrulama, Kullanıcı tarafından oluşturulan API anahtarlarının yalnızca nuget.org ile kullanılmasını ve üçüncü taraf bir hizmetten gelen diğer doğrulamanın veya doğrulamanın tek seferlik Use Verify-Scope anahtarları aracılığıyla işlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b39e7-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="b39e7-114">Bu doğrulama kapsamı anahtarları, paketin nuget.org üzerinde belirli bir kullanıcıya (hesap) ait olduğunu doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b39e7-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="b39e7-115">İstemci gereksinimi</span><span class="sxs-lookup"><span data-stu-id="b39e7-115">Client requirement</span></span>

<span data-ttu-id="b39e7-116">İstemciler, paketleri nuget.org 'e **göndermek** için API çağrıları yaparken istemcilerin aşağıdaki üstbilgiyi geçmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="b39e7-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="b39e7-117">`X-NuGet-Client-Version`Üstbilginin benzer anlamolduğuna, ancak yalnızca resmi NuGet istemcisi tarafından kullanılmak üzere ayrıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b39e7-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="b39e7-118">Üçüncü taraf istemcileri, `X-NuGet-Protocol-Version` üstbilgiyi ve değeri kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b39e7-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="b39e7-119">**Gönderme** protokolünün kendisi, [ `PackagePublish` kaynağın](package-publish-resource.md)belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b39e7-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="b39e7-120">Bir istemci dış hizmetlerle etkileşime geçtiğinde ve bir paketin belirli bir kullanıcıya (hesap) ait olup olmadığını doğrulaması gerekiyorsa, aşağıdaki Protokolü kullanmalı ve nuget.org adresinden API anahtarlarını değil Verify-Scope anahtarlarını kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b39e7-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="b39e7-121">Verify-Scope anahtarı istemek için API</span><span class="sxs-lookup"><span data-stu-id="b39e7-121">API to request a verify-scope key</span></span>

<span data-ttu-id="b39e7-122">Bu API, kendisine ait bir paketi doğrulamak üzere bir nuget.org yazarı için Validate-Scope anahtarını almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b39e7-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="b39e7-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="b39e7-123">Request parameters</span></span>

<span data-ttu-id="b39e7-124">Name</span><span class="sxs-lookup"><span data-stu-id="b39e7-124">Name</span></span>           | <span data-ttu-id="b39e7-125">İçinde</span><span class="sxs-lookup"><span data-stu-id="b39e7-125">In</span></span>     | <span data-ttu-id="b39e7-126">Tür</span><span class="sxs-lookup"><span data-stu-id="b39e7-126">Type</span></span>   | <span data-ttu-id="b39e7-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b39e7-127">Required</span></span> | <span data-ttu-id="b39e7-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="b39e7-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b39e7-129">ID</span><span class="sxs-lookup"><span data-stu-id="b39e7-129">ID</span></span>             | <span data-ttu-id="b39e7-130">URL</span><span class="sxs-lookup"><span data-stu-id="b39e7-130">URL</span></span>    | <span data-ttu-id="b39e7-131">string</span><span class="sxs-lookup"><span data-stu-id="b39e7-131">string</span></span> | <span data-ttu-id="b39e7-132">evet</span><span class="sxs-lookup"><span data-stu-id="b39e7-132">yes</span></span>      | <span data-ttu-id="b39e7-133">Kapsam anahtarını doğrula için istenen paket identidier</span><span class="sxs-lookup"><span data-stu-id="b39e7-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="b39e7-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="b39e7-134">VERSION</span></span>        | <span data-ttu-id="b39e7-135">URL</span><span class="sxs-lookup"><span data-stu-id="b39e7-135">URL</span></span>    | <span data-ttu-id="b39e7-136">string</span><span class="sxs-lookup"><span data-stu-id="b39e7-136">string</span></span> | <span data-ttu-id="b39e7-137">hayır</span><span class="sxs-lookup"><span data-stu-id="b39e7-137">no</span></span>       | <span data-ttu-id="b39e7-138">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="b39e7-138">The package version</span></span>
<span data-ttu-id="b39e7-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b39e7-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b39e7-140">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="b39e7-140">Header</span></span> | <span data-ttu-id="b39e7-141">string</span><span class="sxs-lookup"><span data-stu-id="b39e7-141">string</span></span> | <span data-ttu-id="b39e7-142">evet</span><span class="sxs-lookup"><span data-stu-id="b39e7-142">yes</span></span>      | <span data-ttu-id="b39e7-143">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b39e7-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="b39e7-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b39e7-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="b39e7-145">Verify Scope anahtarını doğrulamak için API</span><span class="sxs-lookup"><span data-stu-id="b39e7-145">API to verify the verify scope key</span></span>

<span data-ttu-id="b39e7-146">Bu API, nuget.org yazarına ait olan paketin doğrulama kapsamı anahtarını doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b39e7-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="b39e7-147">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="b39e7-147">Request parameters</span></span>

<span data-ttu-id="b39e7-148">Name</span><span class="sxs-lookup"><span data-stu-id="b39e7-148">Name</span></span>           | <span data-ttu-id="b39e7-149">İçinde</span><span class="sxs-lookup"><span data-stu-id="b39e7-149">In</span></span>     | <span data-ttu-id="b39e7-150">Tür</span><span class="sxs-lookup"><span data-stu-id="b39e7-150">Type</span></span>   | <span data-ttu-id="b39e7-151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b39e7-151">Required</span></span> | <span data-ttu-id="b39e7-152">Notlar</span><span class="sxs-lookup"><span data-stu-id="b39e7-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="b39e7-153">ID</span><span class="sxs-lookup"><span data-stu-id="b39e7-153">ID</span></span>             | <span data-ttu-id="b39e7-154">URL</span><span class="sxs-lookup"><span data-stu-id="b39e7-154">URL</span></span>    | <span data-ttu-id="b39e7-155">string</span><span class="sxs-lookup"><span data-stu-id="b39e7-155">string</span></span> | <span data-ttu-id="b39e7-156">evet</span><span class="sxs-lookup"><span data-stu-id="b39e7-156">yes</span></span>      | <span data-ttu-id="b39e7-157">Kapsam anahtarı doğrulaması istenen paket tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="b39e7-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="b39e7-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="b39e7-158">VERSION</span></span>        | <span data-ttu-id="b39e7-159">URL</span><span class="sxs-lookup"><span data-stu-id="b39e7-159">URL</span></span>    | <span data-ttu-id="b39e7-160">string</span><span class="sxs-lookup"><span data-stu-id="b39e7-160">string</span></span> | <span data-ttu-id="b39e7-161">hayır</span><span class="sxs-lookup"><span data-stu-id="b39e7-161">no</span></span>       | <span data-ttu-id="b39e7-162">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="b39e7-162">The package version</span></span>
<span data-ttu-id="b39e7-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b39e7-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b39e7-164">Üst bilgi</span><span class="sxs-lookup"><span data-stu-id="b39e7-164">Header</span></span> | <span data-ttu-id="b39e7-165">string</span><span class="sxs-lookup"><span data-stu-id="b39e7-165">string</span></span> | <span data-ttu-id="b39e7-166">evet</span><span class="sxs-lookup"><span data-stu-id="b39e7-166">yes</span></span>      | <span data-ttu-id="b39e7-167">Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b39e7-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="b39e7-168">Bu kapsam API anahtarının süresi bir günün saati veya ilk kullanımda olduğunda, ne olursa olsun.</span><span class="sxs-lookup"><span data-stu-id="b39e7-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="b39e7-169">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b39e7-169">Response</span></span>

<span data-ttu-id="b39e7-170">Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="b39e7-170">Status Code</span></span> | <span data-ttu-id="b39e7-171">Anlamı</span><span class="sxs-lookup"><span data-stu-id="b39e7-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="b39e7-172">200</span><span class="sxs-lookup"><span data-stu-id="b39e7-172">200</span></span>         | <span data-ttu-id="b39e7-173">API anahtarı geçerli</span><span class="sxs-lookup"><span data-stu-id="b39e7-173">The API key is valid</span></span>
<span data-ttu-id="b39e7-174">403</span><span class="sxs-lookup"><span data-stu-id="b39e7-174">403</span></span>         | <span data-ttu-id="b39e7-175">API anahtarı geçersiz veya pakete gönderim yetkisi yok</span><span class="sxs-lookup"><span data-stu-id="b39e7-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="b39e7-176">404</span><span class="sxs-lookup"><span data-stu-id="b39e7-176">404</span></span>         | <span data-ttu-id="b39e7-177">`ID`Ve `VERSION` (isteğe bağlı) tarafından başvurulan paket yok</span><span class="sxs-lookup"><span data-stu-id="b39e7-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
