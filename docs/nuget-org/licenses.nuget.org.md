---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427553"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="11d44-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="11d44-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="11d44-103">Mantığı</span><span class="sxs-lookup"><span data-stu-id="11d44-103">Rationale</span></span>

<span data-ttu-id="11d44-104">[Lisans ifadelerinin](../reference/nuspec.md#license)getirilmesiyle, tek tek lisans tanımlayıcıları, özel durum tanımlayıcıları veya lisans ifadeleri için bir referans metni sağlayacak güvenilir bir hizmete sahip olmak için bir gereksinim ortaya çıkmıştır.</span><span class="sxs-lookup"><span data-stu-id="11d44-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="11d44-105">Bu hizmet için ek bir gereksinim, biz güvenli bir şekilde eski istemciler için geriye dönük uyumluluk sağlamak için kullanabilirsiniz, böylece çürüme bağlantı duyarlı değildir, istikrarlı bir URL şeması olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="11d44-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="11d44-106">Licenses.nuget.org bu rolü yerine getirsin.</span><span class="sxs-lookup"><span data-stu-id="11d44-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="11d44-107">Nuget.org, lisans ifadesini kullanarak lisanslarını belirten paketler için lisans metni referansını sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="11d44-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="11d44-108">`nuget pack`veya diğer [istemci araçlarıyla](../install-nuget-client-tools.md) paketleme, öğeyi [`licenseUrl`](../reference/nuspec.md#licenseurl) desteklemeyen eski istemcilerle geriye dönük `license` uyumluluk sağlamak için licenses.nuget.org işaret etmek için öğeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="11d44-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="11d44-109">Protokol</span><span class="sxs-lookup"><span data-stu-id="11d44-109">Protocol</span></span>

<span data-ttu-id="11d44-110">Licenses.nuget.org tarayıcılarında insanlar tarafından görüntülenecek şekilde tasarlanmıştır, makine tarafından okunabilir yanıt lar sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="11d44-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="11d44-111">HTTPS protokolü kullanılmalıdır ve isteklerin belirli bir şekilde inşa edilmesi beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="11d44-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="11d44-112">Yalnızca istekleri `GET` destekler.</span><span class="sxs-lookup"><span data-stu-id="11d44-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="11d44-113">Lisans ifadelerini veya lisans özel durum tanımlayıcılarını aşağıda belirtilen bir şekilde giriş olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="11d44-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="11d44-114">Lisans ifadelerinin tüm öğelerinin büyük/küçük harf duyarlı olduğunu ve bu nedenle licenses.nuget.org tüm girişlerin de büyük/küçük harf duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="11d44-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="11d44-115">Lisans ifadeleri</span><span class="sxs-lookup"><span data-stu-id="11d44-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="11d44-116">İstek</span><span class="sxs-lookup"><span data-stu-id="11d44-116">Request</span></span>

<span data-ttu-id="11d44-117">Lisans ifadeleri (ifadenin tek bir lisanstan oluştuğu önemsiz durumlar da dahil olmak üzere) [URL kodlanması](https://tools.ietf.org/html/rfc3986#section-2.1) ve licenses.nuget.org isteğinde yol olarak kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="11d44-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="11d44-118">Lisans ifadesi</span><span class="sxs-lookup"><span data-stu-id="11d44-118">License expression</span></span> | <span data-ttu-id="11d44-119">Kullanılacak URL</span><span class="sxs-lookup"><span data-stu-id="11d44-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="11d44-120">MIT</span><span class="sxs-lookup"><span data-stu-id="11d44-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="11d44-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="11d44-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="11d44-122">(LGPL-2.0-sadece FLTK-istisna VEYA Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="11d44-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="11d44-123">Hizmet, yalnızca nuget.org tarafından kabul edilen lisans tanımlayıcılarını ve lisans özel durum tanımlayıcılarını destekler. Desteklenmeyen lisans tanımlayıcıları veya lisans özel durum tanımlayıcıları içeren veya lisans ifade sözdizimine uymayan tüm lisans ifadeleri geçersiz sayılır.</span><span class="sxs-lookup"><span data-stu-id="11d44-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="11d44-124">Yanıt</span><span class="sxs-lookup"><span data-stu-id="11d44-124">Response</span></span>

<span data-ttu-id="11d44-125">Licenses.nuget.org, http 200 durum kodu ve lisans ifadesinin açıklamasını içeren bir web sayfası ile geçerli lisans ifadeleri içeren istekleri yanıtlar:</span><span class="sxs-lookup"><span data-stu-id="11d44-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="11d44-126">verilen lisans ifadesi tek bir lisans tanımlayıcısı içeriyorsa, bu lisans başvuru metnini içeren bir web sayfası döndürülür;</span><span class="sxs-lookup"><span data-stu-id="11d44-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="11d44-127">verilen lisans ifadesi bileşik bir lisans ifadesiyse, tek tek lisans veya lisans özel durum başvurularına bağlantılar içeren lisans ifadesini içeren bir web sayfası döndürülür.</span><span class="sxs-lookup"><span data-stu-id="11d44-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="11d44-128">Geçersiz bir lisans ifadesi içeren tüm istekler, HTTP 404 yanıtıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="11d44-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="11d44-129">Lisans istisnaları</span><span class="sxs-lookup"><span data-stu-id="11d44-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="11d44-130">İstek</span><span class="sxs-lookup"><span data-stu-id="11d44-130">Request</span></span>

<span data-ttu-id="11d44-131">Lisans özel durum tanımlayıcıları URL kodlu olmalı ve licenses.nuget.org isteğinde bir yol olarak kullanılmalıdır. Tek bir istekte yalnızca tek bir lisans özel durum tanımlayıcısı sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="11d44-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="11d44-132">URL'nin yol bölümünde lisans özel durum tanımlayıcısı dışında ek karakter bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="11d44-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="11d44-133">Lisans özel durum tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="11d44-133">License exception identifier</span></span> | <span data-ttu-id="11d44-134">Kullanılacak URL</span><span class="sxs-lookup"><span data-stu-id="11d44-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="11d44-135">FLTK-istisna</span><span class="sxs-lookup"><span data-stu-id="11d44-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="11d44-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="11d44-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="11d44-137">Yanıt</span><span class="sxs-lookup"><span data-stu-id="11d44-137">Response</span></span>

<span data-ttu-id="11d44-138">Licenses.nuget.org, http 200 yanıtı ve belirtilen lisans özel durumu için başvuru metnini içeren bir web sayfası ile bilinen bir lisans özel durum tanımlayıcısı ile bir isteğe yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="11d44-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="11d44-139">Desteklenmeyen lisans özel durum tanımlayıcısı içeren herhangi bir istek, HTTP 404 yanıtıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="11d44-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>