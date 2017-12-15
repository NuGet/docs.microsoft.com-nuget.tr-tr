---
title: nuget.org protokolleri | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "NuGet istemcileri ile etkileşim kurmak için gelişen nuget.org protokoller."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="6335a-103">nuget.org protokolleri</span><span class="sxs-lookup"><span data-stu-id="6335a-103">nuget.org Protocols</span></span>

<span data-ttu-id="6335a-104">Nuget.org ile etkileşim kurmak için istemcileri belirli protokoller izlemeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="6335a-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="6335a-105">Bu protokollerin gelişen tutmak için istemcileri belirli nuget.org API'leri çağrılırken kullandıkları Protokolü sürüm tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6335a-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="6335a-106">Bu değişiklikleri eski istemcileri için bir satır sonu olmayan biçimde tanıtmak nuget.org sağlar.</span><span class="sxs-lookup"><span data-stu-id="6335a-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="6335a-107">Bu sayfada belgelenen API'leri nuget.org için özeldir ve bu API'leri tanıtmak diğer NuGet sunucu uygulamaları için hiçbir Beklenti yoktur.</span><span class="sxs-lookup"><span data-stu-id="6335a-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="6335a-108">Kapsamlı NuGet ekosistemi uygulanan NuGet API'si hakkında daha fazla bilgi için bkz: [API genel bakış](overview.md).</span><span class="sxs-lookup"><span data-stu-id="6335a-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="6335a-109">Bu konu, çeşitli protokoller olarak ve varlığı için ne zaman geldikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="6335a-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="6335a-110">NuGet Protokolü sürüm 4.1.0'da</span><span class="sxs-lookup"><span data-stu-id="6335a-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="6335a-111">4.1.0'da Protokolü paketi nuget.org hesabı karşı doğrulama için nuget.org dışında Hizmetleri ile etkileşim kurmak için doğrulayın kapsam anahtarları kullanımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6335a-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="6335a-112">Unutmayın `4.1.0` sürüm numarası donuk bir dizedir ancak bu protokolü desteklenen resmi NuGet istemci ilk sürümü ile çakıştığı için gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="6335a-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="6335a-113">Doğrulama işlemi kullanıcı tarafından oluşturulan API anahtarlar yalnızca nuget.org ile kullanılır ve bu bir doğrulama veya bir üçüncü taraf hizmetinden doğrulama bir kerelik kullanım doğrulayın kapsam anahtarlarıyla gerçekleştirilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="6335a-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="6335a-114">Bu doğrulama kapsam anahtarları paket nuget.org ağdaki belirli bir kullanıcı (hesap) ait olduğunu doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6335a-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="6335a-115">İstemci gereksinimi</span><span class="sxs-lookup"><span data-stu-id="6335a-115">Client requirement</span></span>

<span data-ttu-id="6335a-116">İstemciler için API çağrıları yaptığınızda aşağıdaki üstbilgi geçirmek için gerekli **itme** nuget.org paketler:</span><span class="sxs-lookup"><span data-stu-id="6335a-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="6335a-117">Unutmayın önceden varolan `X-NuGet-Client-Version` üstbilgi aynı amacı vardır, ancak artık kullanılmıyor ve artık kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6335a-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="6335a-118">**İtme** protokolün kendini belgelerine açıklanan [ `PackagePublish` kaynak](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="6335a-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="6335a-119">Bir istemci dış hizmetler ve belirli bir kullanıcıya (hesap) bir pakete ait olup olmadığını doğrulamak için gereksinimleri ile etkileşime giren, bunu aşağıdaki protokolünü kullanan ve doğrulama kapsam anahtarları ve nuget.org değil API anahtarlarından kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6335a-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="6335a-120">Doğrulama kapsam anahtarı istemek için API</span><span class="sxs-lookup"><span data-stu-id="6335a-120">API to request a verify-scope key</span></span>

<span data-ttu-id="6335a-121">Bu API him/her tarafından sahip olunan bir paket doğrulamak bir nuget.org yazar için bir doğrulama kapsam anahtarı almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6335a-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="6335a-122">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="6335a-122">Request parameters</span></span>

<span data-ttu-id="6335a-123">Ad</span><span class="sxs-lookup"><span data-stu-id="6335a-123">Name</span></span>           | <span data-ttu-id="6335a-124">İçindeki</span><span class="sxs-lookup"><span data-stu-id="6335a-124">In</span></span>     | <span data-ttu-id="6335a-125">Tür</span><span class="sxs-lookup"><span data-stu-id="6335a-125">Type</span></span>   | <span data-ttu-id="6335a-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6335a-126">Required</span></span> | <span data-ttu-id="6335a-127">Notlar</span><span class="sxs-lookup"><span data-stu-id="6335a-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6335a-128">Kimlik</span><span class="sxs-lookup"><span data-stu-id="6335a-128">ID</span></span>             | <span data-ttu-id="6335a-129">URL</span><span class="sxs-lookup"><span data-stu-id="6335a-129">URL</span></span>    | <span data-ttu-id="6335a-130">dize</span><span class="sxs-lookup"><span data-stu-id="6335a-130">string</span></span> | <span data-ttu-id="6335a-131">Evet</span><span class="sxs-lookup"><span data-stu-id="6335a-131">yes</span></span>      | <span data-ttu-id="6335a-132">Doğrulama kapsam anahtarı istenen paket identidier</span><span class="sxs-lookup"><span data-stu-id="6335a-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="6335a-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="6335a-133">VERSION</span></span>        | <span data-ttu-id="6335a-134">URL</span><span class="sxs-lookup"><span data-stu-id="6335a-134">URL</span></span>    | <span data-ttu-id="6335a-135">dize</span><span class="sxs-lookup"><span data-stu-id="6335a-135">string</span></span> | <span data-ttu-id="6335a-136">Yok</span><span class="sxs-lookup"><span data-stu-id="6335a-136">no</span></span>       | <span data-ttu-id="6335a-137">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="6335a-137">The package version</span></span>
<span data-ttu-id="6335a-138">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="6335a-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6335a-139">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="6335a-139">Header</span></span> | <span data-ttu-id="6335a-140">dize</span><span class="sxs-lookup"><span data-stu-id="6335a-140">string</span></span> | <span data-ttu-id="6335a-141">Evet</span><span class="sxs-lookup"><span data-stu-id="6335a-141">yes</span></span>      | <span data-ttu-id="6335a-142">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="6335a-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="6335a-143">Yanıt</span><span class="sxs-lookup"><span data-stu-id="6335a-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="6335a-144">API doğrula kapsam anahtarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="6335a-144">API to verify the verify scope key</span></span>

<span data-ttu-id="6335a-145">Bu API, nuget.org yazar tarafından sahip olunan paket için bir doğrulama kapsam anahtar doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6335a-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="6335a-146">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="6335a-146">Request parameters</span></span>

<span data-ttu-id="6335a-147">Ad</span><span class="sxs-lookup"><span data-stu-id="6335a-147">Name</span></span>           | <span data-ttu-id="6335a-148">İçindeki</span><span class="sxs-lookup"><span data-stu-id="6335a-148">In</span></span>     | <span data-ttu-id="6335a-149">Tür</span><span class="sxs-lookup"><span data-stu-id="6335a-149">Type</span></span>   | <span data-ttu-id="6335a-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6335a-150">Required</span></span> | <span data-ttu-id="6335a-151">Notlar</span><span class="sxs-lookup"><span data-stu-id="6335a-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="6335a-152">Kimlik</span><span class="sxs-lookup"><span data-stu-id="6335a-152">ID</span></span>             | <span data-ttu-id="6335a-153">URL</span><span class="sxs-lookup"><span data-stu-id="6335a-153">URL</span></span>    | <span data-ttu-id="6335a-154">dize</span><span class="sxs-lookup"><span data-stu-id="6335a-154">string</span></span> | <span data-ttu-id="6335a-155">Evet</span><span class="sxs-lookup"><span data-stu-id="6335a-155">yes</span></span>      | <span data-ttu-id="6335a-156">Doğrulama kapsam anahtarı istenen paket tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="6335a-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="6335a-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="6335a-157">VERSION</span></span>        | <span data-ttu-id="6335a-158">URL</span><span class="sxs-lookup"><span data-stu-id="6335a-158">URL</span></span>    | <span data-ttu-id="6335a-159">dize</span><span class="sxs-lookup"><span data-stu-id="6335a-159">string</span></span> | <span data-ttu-id="6335a-160">Yok</span><span class="sxs-lookup"><span data-stu-id="6335a-160">no</span></span>       | <span data-ttu-id="6335a-161">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="6335a-161">The package version</span></span>
<span data-ttu-id="6335a-162">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="6335a-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6335a-163">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="6335a-163">Header</span></span> | <span data-ttu-id="6335a-164">dize</span><span class="sxs-lookup"><span data-stu-id="6335a-164">string</span></span> | <span data-ttu-id="6335a-165">Evet</span><span class="sxs-lookup"><span data-stu-id="6335a-165">yes</span></span>      | <span data-ttu-id="6335a-166">Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="6335a-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="6335a-167">Bu doğrulama kapsam API anahtarı bir günün süresi dolduğunda veya ilk kullanımda, hangisi daha önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="6335a-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="6335a-168">Yanıt</span><span class="sxs-lookup"><span data-stu-id="6335a-168">Response</span></span>

<span data-ttu-id="6335a-169">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="6335a-169">Status Code</span></span> | <span data-ttu-id="6335a-170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6335a-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="6335a-171">200</span><span class="sxs-lookup"><span data-stu-id="6335a-171">200</span></span>         | <span data-ttu-id="6335a-172">API anahtarını geçerlidir</span><span class="sxs-lookup"><span data-stu-id="6335a-172">The API key is valid</span></span>
<span data-ttu-id="6335a-173">403</span><span class="sxs-lookup"><span data-stu-id="6335a-173">403</span></span>         | <span data-ttu-id="6335a-174">API anahtarı geçersiz veya paket karşı göndermek için yetkili değil</span><span class="sxs-lookup"><span data-stu-id="6335a-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="6335a-175">404</span><span class="sxs-lookup"><span data-stu-id="6335a-175">404</span></span>         | <span data-ttu-id="6335a-176">Paket başvurduğu `ID` ve `VERSION` (isteğe bağlı) mevcut değil</span><span class="sxs-lookup"><span data-stu-id="6335a-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
