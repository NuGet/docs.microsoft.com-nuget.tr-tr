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
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="98d68-103">nuget.org protokolleri</span><span class="sxs-lookup"><span data-stu-id="98d68-103">nuget.org Protocols</span></span>

<span data-ttu-id="98d68-104">Nuget.org ile etkileşim kurmak için istemcileri belirli protokoller izlemeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="98d68-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="98d68-105">Bu protokollerin gelişen tutmak için istemcileri belirli nuget.org API'leri çağrılırken kullandıkları Protokolü sürüm tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98d68-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="98d68-106">Bu değişiklikleri eski istemcileri için bir satır sonu olmayan biçimde tanıtmak nuget.org sağlar.</span><span class="sxs-lookup"><span data-stu-id="98d68-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="98d68-107">Bu sayfada belgelenen API'leri nuget.org için özeldir ve bu API'leri tanıtmak diğer NuGet sunucu uygulamaları için hiçbir Beklenti yoktur.</span><span class="sxs-lookup"><span data-stu-id="98d68-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="98d68-108">Kapsamlı NuGet ekosistemi uygulanan NuGet API'si hakkında daha fazla bilgi için bkz: [API genel bakış](overview.md).</span><span class="sxs-lookup"><span data-stu-id="98d68-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="98d68-109">Bu konu, çeşitli protokoller olarak ve varlığı için ne zaman geldikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="98d68-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="98d68-110">NuGet Protokolü sürüm 4.1.0'da</span><span class="sxs-lookup"><span data-stu-id="98d68-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="98d68-111">4.1.0'da Protokolü paketi nuget.org hesabı karşı doğrulama için nuget.org dışında Hizmetleri ile etkileşim kurmak için doğrulayın kapsam anahtarları kullanımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="98d68-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="98d68-112">Unutmayın `4.1.0` sürüm numarası donuk bir dizedir ancak bu protokolü desteklenen resmi NuGet istemci ilk sürümü ile çakıştığı için gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="98d68-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="98d68-113">Doğrulama işlemi kullanıcı tarafından oluşturulan API anahtarlar yalnızca nuget.org ile kullanılır ve bu bir doğrulama veya bir üçüncü taraf hizmetinden doğrulama bir kerelik kullanım doğrulayın kapsam anahtarlarıyla gerçekleştirilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="98d68-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="98d68-114">Bu doğrulama kapsam anahtarları paket nuget.org ağdaki belirli bir kullanıcı (hesap) ait olduğunu doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="98d68-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="98d68-115">İstemci gereksinimi</span><span class="sxs-lookup"><span data-stu-id="98d68-115">Client requirement</span></span>

<span data-ttu-id="98d68-116">İstemciler için API çağrıları yaptığınızda aşağıdaki üstbilgi geçirmek için gerekli **itme** nuget.org paketler:</span><span class="sxs-lookup"><span data-stu-id="98d68-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="98d68-117">Unutmayın `X-NuGet-Client-Version` üstbilgi benzer bir semantik vardır, ancak yalnızca resmi NuGet istemci tarafından kullanılmak üzere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="98d68-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="98d68-118">Üçüncü taraf istemcileri kullanması gereken `X-NuGet-Protocol-Version` üstbilgiyi ve değeri.</span><span class="sxs-lookup"><span data-stu-id="98d68-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="98d68-119">**İtme** protokolün kendini belgelerine açıklanan [ `PackagePublish` kaynak](package-publish-resource.md).</span><span class="sxs-lookup"><span data-stu-id="98d68-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="98d68-120">Bir istemci dış hizmetler ve belirli bir kullanıcıya (hesap) bir pakete ait olup olmadığını doğrulamak için gereksinimleri ile etkileşime giren, bunu aşağıdaki protokolünü kullanan ve doğrulama kapsam anahtarları ve nuget.org değil API anahtarlarından kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98d68-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="98d68-121">Doğrulama kapsam anahtarı istemek için API</span><span class="sxs-lookup"><span data-stu-id="98d68-121">API to request a verify-scope key</span></span>

<span data-ttu-id="98d68-122">Bu API him/her tarafından sahip olunan bir paket doğrulamak bir nuget.org yazar için bir doğrulama kapsam anahtarı almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98d68-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="98d68-123">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="98d68-123">Request parameters</span></span>

<span data-ttu-id="98d68-124">Ad</span><span class="sxs-lookup"><span data-stu-id="98d68-124">Name</span></span>           | <span data-ttu-id="98d68-125">İçindeki</span><span class="sxs-lookup"><span data-stu-id="98d68-125">In</span></span>     | <span data-ttu-id="98d68-126">Tür</span><span class="sxs-lookup"><span data-stu-id="98d68-126">Type</span></span>   | <span data-ttu-id="98d68-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="98d68-127">Required</span></span> | <span data-ttu-id="98d68-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="98d68-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="98d68-129">Kimlik</span><span class="sxs-lookup"><span data-stu-id="98d68-129">ID</span></span>             | <span data-ttu-id="98d68-130">URL</span><span class="sxs-lookup"><span data-stu-id="98d68-130">URL</span></span>    | <span data-ttu-id="98d68-131">dize</span><span class="sxs-lookup"><span data-stu-id="98d68-131">string</span></span> | <span data-ttu-id="98d68-132">Evet</span><span class="sxs-lookup"><span data-stu-id="98d68-132">yes</span></span>      | <span data-ttu-id="98d68-133">Doğrulama kapsam anahtarı istenen paket identidier</span><span class="sxs-lookup"><span data-stu-id="98d68-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="98d68-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="98d68-134">VERSION</span></span>        | <span data-ttu-id="98d68-135">URL</span><span class="sxs-lookup"><span data-stu-id="98d68-135">URL</span></span>    | <span data-ttu-id="98d68-136">dize</span><span class="sxs-lookup"><span data-stu-id="98d68-136">string</span></span> | <span data-ttu-id="98d68-137">Yok</span><span class="sxs-lookup"><span data-stu-id="98d68-137">no</span></span>       | <span data-ttu-id="98d68-138">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="98d68-138">The package version</span></span>
<span data-ttu-id="98d68-139">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="98d68-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="98d68-140">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="98d68-140">Header</span></span> | <span data-ttu-id="98d68-141">dize</span><span class="sxs-lookup"><span data-stu-id="98d68-141">string</span></span> | <span data-ttu-id="98d68-142">Evet</span><span class="sxs-lookup"><span data-stu-id="98d68-142">yes</span></span>      | <span data-ttu-id="98d68-143">Örneğin, `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="98d68-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="98d68-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="98d68-144">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="98d68-145">API doğrula kapsam anahtarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="98d68-145">API to verify the verify scope key</span></span>

<span data-ttu-id="98d68-146">Bu API, nuget.org yazar tarafından sahip olunan paket için bir doğrulama kapsam anahtar doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98d68-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="98d68-147">İstek parametreleri</span><span class="sxs-lookup"><span data-stu-id="98d68-147">Request parameters</span></span>

<span data-ttu-id="98d68-148">Ad</span><span class="sxs-lookup"><span data-stu-id="98d68-148">Name</span></span>           | <span data-ttu-id="98d68-149">İçindeki</span><span class="sxs-lookup"><span data-stu-id="98d68-149">In</span></span>     | <span data-ttu-id="98d68-150">Tür</span><span class="sxs-lookup"><span data-stu-id="98d68-150">Type</span></span>   | <span data-ttu-id="98d68-151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="98d68-151">Required</span></span> | <span data-ttu-id="98d68-152">Notlar</span><span class="sxs-lookup"><span data-stu-id="98d68-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="98d68-153">Kimlik</span><span class="sxs-lookup"><span data-stu-id="98d68-153">ID</span></span>             | <span data-ttu-id="98d68-154">URL</span><span class="sxs-lookup"><span data-stu-id="98d68-154">URL</span></span>    | <span data-ttu-id="98d68-155">dize</span><span class="sxs-lookup"><span data-stu-id="98d68-155">string</span></span> | <span data-ttu-id="98d68-156">Evet</span><span class="sxs-lookup"><span data-stu-id="98d68-156">yes</span></span>      | <span data-ttu-id="98d68-157">Doğrulama kapsam anahtarı istenen paket tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="98d68-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="98d68-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="98d68-158">VERSION</span></span>        | <span data-ttu-id="98d68-159">URL</span><span class="sxs-lookup"><span data-stu-id="98d68-159">URL</span></span>    | <span data-ttu-id="98d68-160">dize</span><span class="sxs-lookup"><span data-stu-id="98d68-160">string</span></span> | <span data-ttu-id="98d68-161">Yok</span><span class="sxs-lookup"><span data-stu-id="98d68-161">no</span></span>       | <span data-ttu-id="98d68-162">Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="98d68-162">The package version</span></span>
<span data-ttu-id="98d68-163">X-NuGet-apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="98d68-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="98d68-164">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="98d68-164">Header</span></span> | <span data-ttu-id="98d68-165">dize</span><span class="sxs-lookup"><span data-stu-id="98d68-165">string</span></span> | <span data-ttu-id="98d68-166">Evet</span><span class="sxs-lookup"><span data-stu-id="98d68-166">yes</span></span>      | <span data-ttu-id="98d68-167">Örneğin, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="98d68-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="98d68-168">Bu doğrulama kapsam API anahtarı bir günün süresi dolduğunda veya ilk kullanımda, hangisi daha önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="98d68-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="98d68-169">Yanıt</span><span class="sxs-lookup"><span data-stu-id="98d68-169">Response</span></span>

<span data-ttu-id="98d68-170">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="98d68-170">Status Code</span></span> | <span data-ttu-id="98d68-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="98d68-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="98d68-172">200</span><span class="sxs-lookup"><span data-stu-id="98d68-172">200</span></span>         | <span data-ttu-id="98d68-173">API anahtarını geçerlidir</span><span class="sxs-lookup"><span data-stu-id="98d68-173">The API key is valid</span></span>
<span data-ttu-id="98d68-174">403</span><span class="sxs-lookup"><span data-stu-id="98d68-174">403</span></span>         | <span data-ttu-id="98d68-175">API anahtarı geçersiz veya paket karşı göndermek için yetkili değil</span><span class="sxs-lookup"><span data-stu-id="98d68-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="98d68-176">404</span><span class="sxs-lookup"><span data-stu-id="98d68-176">404</span></span>         | <span data-ttu-id="98d68-177">Paket başvurduğu `ID` ve `VERSION` (isteğe bağlı) mevcut değil</span><span class="sxs-lookup"><span data-stu-id="98d68-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
