---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427553"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="d293f-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="d293f-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="d293f-103">Stratejinin</span><span class="sxs-lookup"><span data-stu-id="d293f-103">Rationale</span></span>

<span data-ttu-id="d293f-104">Sunulmasıyla birlikte [lisans ifadeleri](../reference/nuspec.md#license), başvuru metin ayrı lisans tanımlayıcıları, özel durum tanımlayıcıları veya lisans ifadeleri sağlayacağını güvenilir bir hizmet için bir gereksinim ortaya çıktı.</span><span class="sxs-lookup"><span data-stu-id="d293f-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="d293f-105">Bu hizmet için ek bir gereksinim rot, bağlantı açık değil ve böylece güvenli bir şekilde, geriye dönük uyumluluk için eski istemcileri sağlamak için kullanabiliriz kararlı bir URL şeması sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="d293f-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="d293f-106">Bu rol Licenses.nuget.org karşılar.</span><span class="sxs-lookup"><span data-stu-id="d293f-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="d293f-107">Nuget.org lisansa lisansı ifade kullanarak belirttiğiniz paketleri için lisans metin başvurusu sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d293f-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="d293f-108">`nuget pack` ya da diğer paket [istemci araçları](../install-nuget-client-tools.md) ayarlamak [ `licenseUrl` ](../reference/nuspec.md#licenseurl) geriye doğru desteklemeyen eski istemciler uyum sağlamak için licenses.nuget.org işaret edecek şekilde öğe `license` öğe.</span><span class="sxs-lookup"><span data-stu-id="d293f-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="d293f-109">Protokol</span><span class="sxs-lookup"><span data-stu-id="d293f-109">Protocol</span></span>

<span data-ttu-id="d293f-110">Licenses.nuget.org tarayıcılarını kişiler tarafından görüntülenmesine yönelik, makine tarafından okunabilir yanıt sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d293f-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="d293f-111">HTTPS protokolü kullanılmalıdır ve istekleri belirli bir biçimde oluşturulmuş beklenir.</span><span class="sxs-lookup"><span data-stu-id="d293f-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="d293f-112">Yalnızca destekler `GET` istekleri.</span><span class="sxs-lookup"><span data-stu-id="d293f-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="d293f-113">Bu lisans deyimlerde ya da lisans özel durum tanımlayıcıları aşağıda belirtilen şekilde girdi olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="d293f-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="d293f-114">Lütfen unutmayın, lisans ifadelerin tüm öğeleri büyük/küçük harfe duyarlıdır ve bu nedenle tüm licenses.nuget.org de büyük küçük harfe duyarlı giriştir.</span><span class="sxs-lookup"><span data-stu-id="d293f-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="d293f-115">Lisans ifadeleri</span><span class="sxs-lookup"><span data-stu-id="d293f-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="d293f-116">İstek</span><span class="sxs-lookup"><span data-stu-id="d293f-116">Request</span></span>

<span data-ttu-id="d293f-117">Lisans ifadeleri (Önemsiz durumları ifade tek bir lisans oluşuyorsa dahil) sahip olmasını [URL kodlamalı](https://tools.ietf.org/html/rfc3986#section-2.1) ve licenses.nuget.org isteğinde bir yol olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d293f-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="d293f-118">Lisans ifadesi</span><span class="sxs-lookup"><span data-stu-id="d293f-118">License expression</span></span> | <span data-ttu-id="d293f-119">Kullanılacak URL'si</span><span class="sxs-lookup"><span data-stu-id="d293f-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="d293f-120">MIT</span><span class="sxs-lookup"><span data-stu-id="d293f-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="d293f-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="d293f-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="d293f-122">(LGPL 2.0-ile yalnızca FLTK özel durumu veya Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="d293f-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="d293f-123">Hizmet, yalnızca lisans tanımlayıcıları ve nuget.org tarafından kabul edilen lisans özel durum tanımlayıcıları destekler. Desteklenmeyen lisans tanımlayıcıları veya lisans özel durum tanımlayıcıları içeren veya lisans ifadesi söz dizimi için uygun değil tüm lisans ifadeleri geçersiz olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d293f-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="d293f-124">Yanıt</span><span class="sxs-lookup"><span data-stu-id="d293f-124">Response</span></span>

<span data-ttu-id="d293f-125">Licenses.nuget.org geçerli lisans ifadelerle bir HTTP 200 durum kodu ve lisansı ifade açıklamasını içeren bir web sayfası içeren isteklere yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="d293f-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="d293f-126">Lisans ifade sağlandıysa bu lisans başvuru metni içeren bir web sayfası döndürülen bir tek bir lisans tanımlayıcısı içeriyor;</span><span class="sxs-lookup"><span data-stu-id="d293f-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="d293f-127">sağlandıysa lisans ifade bir bileşik lisans ifadesi, tek bir lisans veya lisans özel durumu başvuruları için bağlantılarla birlikte lisans ifadesi içeren bir web sayfası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d293f-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="d293f-128">Bir HTTP 404 yanıt geçersiz lisans ifade sonucu içeren tüm istekleri.</span><span class="sxs-lookup"><span data-stu-id="d293f-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="d293f-129">Lisans özel durumları</span><span class="sxs-lookup"><span data-stu-id="d293f-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="d293f-130">İstek</span><span class="sxs-lookup"><span data-stu-id="d293f-130">Request</span></span>

<span data-ttu-id="d293f-131">Lisans özel durum tanımlayıcıları, URL kodlamalı ve licenses.nuget.org isteğine bir yolu olarak kullanılan olması gerekir. Tek bir istekte yalnızca bir tek bir lisans özel durum tanımlayıcısı sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d293f-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="d293f-132">Lisans özel durum tanımlayıcısı yanı sıra herhangi bir ek karakter URL'nin yol kısmı sunabilir.</span><span class="sxs-lookup"><span data-stu-id="d293f-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="d293f-133">Lisans özel durum tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="d293f-133">License exception identifier</span></span> | <span data-ttu-id="d293f-134">Kullanılacak URL'si</span><span class="sxs-lookup"><span data-stu-id="d293f-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="d293f-135">FLTK özel durumu</span><span class="sxs-lookup"><span data-stu-id="d293f-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="d293f-136">openvpn openssl durum</span><span class="sxs-lookup"><span data-stu-id="d293f-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="d293f-137">Yanıt</span><span class="sxs-lookup"><span data-stu-id="d293f-137">Response</span></span>

<span data-ttu-id="d293f-138">Licenses.nuget.org bir HTTP 200 yanıtı ve belirtilen lisans özel durum başvuru metni içeren bir web sayfası ile bilinen lisans özel durum tanımlayıcıya sahip bir isteğe yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="d293f-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="d293f-139">Desteklenmeyen lisans özel durum tanımlayıcı içeren herhangi bir istek, bir HTTP 404 yanıt olarak sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="d293f-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>