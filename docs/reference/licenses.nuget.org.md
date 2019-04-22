---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921565"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="58654-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="58654-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="58654-103">Stratejinin</span><span class="sxs-lookup"><span data-stu-id="58654-103">Rationale</span></span>

<span data-ttu-id="58654-104">Sunulmasıyla birlikte [lisans ifadeleri](nuspec.md#license), başvuru metin ayrı lisans tanımlayıcıları, özel durum tanımlayıcıları veya lisans ifadeleri sağlayacağını güvenilir bir hizmet için bir gereksinim ortaya çıktı.</span><span class="sxs-lookup"><span data-stu-id="58654-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="58654-105">Bu hizmet için ek bir gereksinim rot, bağlantı açık değil ve böylece güvenli bir şekilde, geriye dönük uyumluluk için eski istemcileri sağlamak için kullanabiliriz kararlı bir URL şeması sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="58654-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="58654-106">Bu rol Licenses.nuget.org karşılar.</span><span class="sxs-lookup"><span data-stu-id="58654-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="58654-107">Nuget.org lisansa lisansı ifade kullanarak belirttiğiniz paketleri için lisans metin başvurusu sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="58654-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="58654-108">`nuget pack` ya da diğer paket [istemci araçları](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) ayarlamak [ `licenseUrl` ](nuspec.md#licenseurl) geriye doğru desteklemeyen eski istemciler uyum sağlamak için licenses.nuget.org işaret edecek şekilde öğe `license` öğe.</span><span class="sxs-lookup"><span data-stu-id="58654-108">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="58654-109">Protokol</span><span class="sxs-lookup"><span data-stu-id="58654-109">Protocol</span></span>

<span data-ttu-id="58654-110">Licenses.nuget.org tarayıcılarını kişiler tarafından görüntülenmesine yönelik, makine tarafından okunabilir yanıt sağlanır.</span><span class="sxs-lookup"><span data-stu-id="58654-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="58654-111">HTTPS protokolü kullanılmalıdır ve istekleri belirli bir biçimde oluşturulmuş beklenir.</span><span class="sxs-lookup"><span data-stu-id="58654-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="58654-112">Yalnızca destekler `GET` istekleri.</span><span class="sxs-lookup"><span data-stu-id="58654-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="58654-113">Bu lisans deyimlerde ya da lisans özel durum tanımlayıcıları aşağıda belirtilen şekilde girdi olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="58654-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="58654-114">Lütfen unutmayın, lisans ifadelerin tüm öğeleri büyük/küçük harfe duyarlıdır ve bu nedenle tüm licenses.nuget.org de büyük küçük harfe duyarlı giriştir.</span><span class="sxs-lookup"><span data-stu-id="58654-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="58654-115">Lisans ifadeleri</span><span class="sxs-lookup"><span data-stu-id="58654-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="58654-116">İstek</span><span class="sxs-lookup"><span data-stu-id="58654-116">Request</span></span>

<span data-ttu-id="58654-117">Lisans ifadeleri (Önemsiz durumları ifade tek bir lisans oluşuyorsa dahil) sahip olmasını [URL kodlamalı](https://tools.ietf.org/html/rfc3986#section-2.1) ve licenses.nuget.org isteğinde bir yol olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58654-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="58654-118">Lisans ifadesi</span><span class="sxs-lookup"><span data-stu-id="58654-118">License expression</span></span> | <span data-ttu-id="58654-119">Kullanılacak URL'si</span><span class="sxs-lookup"><span data-stu-id="58654-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="58654-120">MIT</span><span class="sxs-lookup"><span data-stu-id="58654-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="58654-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="58654-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="58654-122">(LGPL 2.0-ile yalnızca FLTK özel durumu veya Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="58654-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="58654-123">Hizmet, yalnızca lisans tanımlayıcıları ve nuget.org tarafından kabul edilen lisans özel durum tanımlayıcıları destekler. Desteklenmeyen lisans tanımlayıcıları veya lisans özel durum tanımlayıcıları içeren veya lisans ifadesi söz dizimi için uygun değil tüm lisans ifadeleri geçersiz olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="58654-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="58654-124">Yanıt</span><span class="sxs-lookup"><span data-stu-id="58654-124">Response</span></span>

<span data-ttu-id="58654-125">Licenses.nuget.org geçerli lisans ifadelerle bir HTTP 200 durum kodu ve lisansı ifade açıklamasını içeren bir web sayfası içeren isteklere yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="58654-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="58654-126">Lisans ifade sağlandıysa bu lisans başvuru metni içeren bir web sayfası döndürülen bir tek bir lisans tanımlayıcısı içeriyor;</span><span class="sxs-lookup"><span data-stu-id="58654-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="58654-127">sağlandıysa lisans ifade bir bileşik lisans ifadesi, tek bir lisans veya lisans özel durumu başvuruları için bağlantılarla birlikte lisans ifadesi içeren bir web sayfası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="58654-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="58654-128">Bir HTTP 404 yanıt geçersiz lisans ifade sonucu içeren tüm istekleri.</span><span class="sxs-lookup"><span data-stu-id="58654-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="58654-129">Lisans özel durumları</span><span class="sxs-lookup"><span data-stu-id="58654-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="58654-130">İstek</span><span class="sxs-lookup"><span data-stu-id="58654-130">Request</span></span>

<span data-ttu-id="58654-131">Lisans özel durum tanımlayıcıları, URL kodlamalı ve licenses.nuget.org isteğine bir yolu olarak kullanılan olması gerekir. Tek bir istekte yalnızca bir tek bir lisans özel durum tanımlayıcısı sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="58654-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="58654-132">Lisans özel durum tanımlayıcısı yanı sıra herhangi bir ek karakter URL'nin yol kısmı sunabilir.</span><span class="sxs-lookup"><span data-stu-id="58654-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="58654-133">Lisans özel durum tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="58654-133">License exception identifier</span></span> | <span data-ttu-id="58654-134">Kullanılacak URL'si</span><span class="sxs-lookup"><span data-stu-id="58654-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="58654-135">FLTK özel durumu</span><span class="sxs-lookup"><span data-stu-id="58654-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="58654-136">openvpn openssl durum</span><span class="sxs-lookup"><span data-stu-id="58654-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="58654-137">Yanıt</span><span class="sxs-lookup"><span data-stu-id="58654-137">Response</span></span>

<span data-ttu-id="58654-138">Licenses.nuget.org bir HTTP 200 yanıtı ve belirtilen lisans özel durum başvuru metni içeren bir web sayfası ile bilinen lisans özel durum tanımlayıcıya sahip bir isteğe yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="58654-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="58654-139">Desteklenmeyen lisans özel durum tanımlayıcı içeren herhangi bir istek, bir HTTP 404 yanıt olarak sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="58654-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>