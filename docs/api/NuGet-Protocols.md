---
title: nuget.org protokolleri
description: NuGet istemcileri ile etkileşim kurmak için gelişen nuget.org protokolleri.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547279"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="1ebaf-103">nuget.org protokolleri</span><span class="sxs-lookup"><span data-stu-id="1ebaf-103">nuget.org protocols</span></span>

<span data-ttu-id="1ebaf-104">Nuget.org ile etkileşim kurmak için istemcileri belirli protokoller izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="1ebaf-105">Bu protokollerin gelişen tutmak olduğundan, istemcileri belirli nuget.org API'leri çağırırken kullandıkları protokol sürümü tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="1ebaf-106">Bu değişiklikler, eski istemciler için bir hataya neden olmayan şekilde tanıtmak nuget.org sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="1ebaf-107">Bu sayfada belgelenen API'leri nuget.org için özeldir ve bu API'leri tanıtmak diğer NuGet sunucu uygulamaları için hiçbir beklentisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="1ebaf-108">Genel olarak NuGet ekosisteminde uygulanan NuGet API'si hakkında daha fazla bilgi için bkz [API'sine genel bakış](overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ebaf-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="1ebaf-109">Bu konu, çeşitli protokoller olarak ve varlığı için ne zaman geldikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="1ebaf-110">NuGet Protokolü sürüm 4.1.0</span><span class="sxs-lookup"><span data-stu-id="1ebaf-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="1ebaf-111">4.1.0 protokolü paketi nuget.org hesabına karşı doğrulamak için nuget.org dışındaki hizmetlerle etkileşim için doğrulama kapsamı anahtarları kullanımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="1ebaf-112">Unutmayın `4.1.0` sürüm numarası genel olmayan bir dizedir, ancak ilk sürümü bu protokolü desteklenen resmi bir NuGet istemcisi ile çakıştığı için gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="1ebaf-113">Nuget.org ile yalnızca kullanıcı tarafından oluşturulan API anahtarları kullanılır ve bu bir doğrulama veya bir üçüncü taraf hizmetinden doğrulama tek seferlik kullanım doğrulama kapsamı anahtarlar aracılığıyla işlenir doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="1ebaf-114">Bu doğrulama kapsamı anahtarları paket nuget.org üzerindeki belirli bir kullanıcı (hesap) ait olduğunu doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="1ebaf-115">İstemci gereksinimi</span><span class="sxs-lookup"><span data-stu-id="1ebaf-115">Client requirement</span></span>

<span data-ttu-id="1ebaf-116">İstemciler bir API çağrısına zaman aşağıdaki üst bilgi geçirmek için gerekli **anında iletme** nuget.org paketler:</span><span class="sxs-lookup"><span data-stu-id="1ebaf-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="1ebaf-117">Unutmayın `X-NuGet-Client-Version` üstbilgisi, benzer semantiğe sahip ancak yalnızca resmi bir NuGet istemcisi tarafından kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="1ebaf-118">Üçüncü taraf istemcileri kullanması gereken `X-NuGet-Protocol-Version` üstbilgiyi ve değeri.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="1ebaf-119">**Anında iletme** protokolün kendisini belgelerinde açıklanmıştır [ `PackagePublish` kaynak](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1ebaf-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="1ebaf-120">Dış hizmetler ve gereksinimlerini bir paket (hesap) belirli bir kullanıcıya ait olup olmadığını doğrulamak için bir istemci etkileşimde gerekirse, aşağıdaki protokolünü kullanan ve doğrulama kapsamı anahtarları ve nuget.org değil API anahtarlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="1ebaf-121">API doğrulama kapsamı anahtar istemek için</span><span class="sxs-lookup"><span data-stu-id="1ebaf-121">API to request a verify-scope key</span></span>

<span data-ttu-id="1ebaf-122">Bu API, bir nuget.org Yazar him/her tarafından sahip olunan bir paket doğrulamak için bir kapsam doğrulama anahtarını almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="1ebaf-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="1ebaf-123">Request parameters</span></span>

<span data-ttu-id="1ebaf-124">Ad</span><span class="sxs-lookup"><span data-stu-id="1ebaf-124">Name</span></span>           | <span data-ttu-id="1ebaf-125">İçindeki</span><span class="sxs-lookup"><span data-stu-id="1ebaf-125">In</span></span>     | <span data-ttu-id="1ebaf-126">Tür</span><span class="sxs-lookup"><span data-stu-id="1ebaf-126">Type</span></span>   | <span data-ttu-id="1ebaf-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1ebaf-127">Required</span></span> | <span data-ttu-id="1ebaf-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="1ebaf-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1ebaf-129">Kimlik</span><span class="sxs-lookup"><span data-stu-id="1ebaf-129">ID</span></span>             | <span data-ttu-id="1ebaf-130">URL</span><span class="sxs-lookup"><span data-stu-id="1ebaf-130">URL</span></span>    | <span data-ttu-id="1ebaf-131">dize</span><span class="sxs-lookup"><span data-stu-id="1ebaf-131">string</span></span> | <span data-ttu-id="1ebaf-132">Evet</span><span class="sxs-lookup"><span data-stu-id="1ebaf-132">yes</span></span>      | <span data-ttu-id="1ebaf-133">Doğrulama kapsamı anahtar istendiği paket identidier</span><span class="sxs-lookup"><span data-stu-id="1ebaf-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="1ebaf-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="1ebaf-134">VERSION</span></span>        | <span data-ttu-id="1ebaf-135">URL</span><span class="sxs-lookup"><span data-stu-id="1ebaf-135">URL</span></span>    | <span data-ttu-id="1ebaf-136">dize</span><span class="sxs-lookup"><span data-stu-id="1ebaf-136">string</span></span> | <span data-ttu-id="1ebaf-137">Yok</span><span class="sxs-lookup"><span data-stu-id="1ebaf-137">no</span></span>       | <span data-ttu-id="1ebaf-138">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="1ebaf-138">The package version</span></span>
<span data-ttu-id="1ebaf-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1ebaf-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1ebaf-140">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="1ebaf-140">Header</span></span> | <span data-ttu-id="1ebaf-141">dize</span><span class="sxs-lookup"><span data-stu-id="1ebaf-141">string</span></span> | <span data-ttu-id="1ebaf-142">Evet</span><span class="sxs-lookup"><span data-stu-id="1ebaf-142">yes</span></span>      | <span data-ttu-id="1ebaf-143">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1ebaf-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="1ebaf-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="1ebaf-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="1ebaf-145">API doğrulama kapsamı anahtar doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="1ebaf-145">API to verify the verify scope key</span></span>

<span data-ttu-id="1ebaf-146">Bu API, nuget.org yazarı tarafından sahip olunan bir paket için bir doğrulama kapsamı anahtar doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="1ebaf-147">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="1ebaf-147">Request parameters</span></span>

<span data-ttu-id="1ebaf-148">Ad</span><span class="sxs-lookup"><span data-stu-id="1ebaf-148">Name</span></span>           | <span data-ttu-id="1ebaf-149">İçindeki</span><span class="sxs-lookup"><span data-stu-id="1ebaf-149">In</span></span>     | <span data-ttu-id="1ebaf-150">Tür</span><span class="sxs-lookup"><span data-stu-id="1ebaf-150">Type</span></span>   | <span data-ttu-id="1ebaf-151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1ebaf-151">Required</span></span> | <span data-ttu-id="1ebaf-152">Notlar</span><span class="sxs-lookup"><span data-stu-id="1ebaf-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="1ebaf-153">Kimlik</span><span class="sxs-lookup"><span data-stu-id="1ebaf-153">ID</span></span>             | <span data-ttu-id="1ebaf-154">URL</span><span class="sxs-lookup"><span data-stu-id="1ebaf-154">URL</span></span>    | <span data-ttu-id="1ebaf-155">dize</span><span class="sxs-lookup"><span data-stu-id="1ebaf-155">string</span></span> | <span data-ttu-id="1ebaf-156">Evet</span><span class="sxs-lookup"><span data-stu-id="1ebaf-156">yes</span></span>      | <span data-ttu-id="1ebaf-157">Doğrulama kapsamı anahtar istendiği paket tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="1ebaf-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="1ebaf-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="1ebaf-158">VERSION</span></span>        | <span data-ttu-id="1ebaf-159">URL</span><span class="sxs-lookup"><span data-stu-id="1ebaf-159">URL</span></span>    | <span data-ttu-id="1ebaf-160">dize</span><span class="sxs-lookup"><span data-stu-id="1ebaf-160">string</span></span> | <span data-ttu-id="1ebaf-161">Yok</span><span class="sxs-lookup"><span data-stu-id="1ebaf-161">no</span></span>       | <span data-ttu-id="1ebaf-162">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="1ebaf-162">The package version</span></span>
<span data-ttu-id="1ebaf-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1ebaf-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1ebaf-164">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="1ebaf-164">Header</span></span> | <span data-ttu-id="1ebaf-165">dize</span><span class="sxs-lookup"><span data-stu-id="1ebaf-165">string</span></span> | <span data-ttu-id="1ebaf-166">Evet</span><span class="sxs-lookup"><span data-stu-id="1ebaf-166">yes</span></span>      | <span data-ttu-id="1ebaf-167">Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="1ebaf-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="1ebaf-168">Bu doğrulama kapsamı API anahtarı bir günün süresi veya ilk kez kullanıldığında, hangisi önce gerçekleşirse.</span><span class="sxs-lookup"><span data-stu-id="1ebaf-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="1ebaf-169">Yanıt</span><span class="sxs-lookup"><span data-stu-id="1ebaf-169">Response</span></span>

<span data-ttu-id="1ebaf-170">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="1ebaf-170">Status Code</span></span> | <span data-ttu-id="1ebaf-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ebaf-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="1ebaf-172">200</span><span class="sxs-lookup"><span data-stu-id="1ebaf-172">200</span></span>         | <span data-ttu-id="1ebaf-173">API anahtarı geçerlidir</span><span class="sxs-lookup"><span data-stu-id="1ebaf-173">The API key is valid</span></span>
<span data-ttu-id="1ebaf-174">403</span><span class="sxs-lookup"><span data-stu-id="1ebaf-174">403</span></span>         | <span data-ttu-id="1ebaf-175">API anahtarı geçersiz veya karşı paket göndermek için yetkili değil</span><span class="sxs-lookup"><span data-stu-id="1ebaf-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="1ebaf-176">404</span><span class="sxs-lookup"><span data-stu-id="1ebaf-176">404</span></span>         | <span data-ttu-id="1ebaf-177">Tarafından paket adlandırılan `ID` ve `VERSION` (isteğe bağlı) yok</span><span class="sxs-lookup"><span data-stu-id="1ebaf-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
