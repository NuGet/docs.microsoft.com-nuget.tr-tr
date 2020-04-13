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
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>Mantığı

[Lisans ifadelerinin](../reference/nuspec.md#license)getirilmesiyle, tek tek lisans tanımlayıcıları, özel durum tanımlayıcıları veya lisans ifadeleri için bir referans metni sağlayacak güvenilir bir hizmete sahip olmak için bir gereksinim ortaya çıkmıştır.
Bu hizmet için ek bir gereksinim, biz güvenli bir şekilde eski istemciler için geriye dönük uyumluluk sağlamak için kullanabilirsiniz, böylece çürüme bağlantı duyarlı değildir, istikrarlı bir URL şeması olmasıdır.

Licenses.nuget.org bu rolü yerine getirsin. Nuget.org, lisans ifadesini kullanarak lisanslarını belirten paketler için lisans metni referansını sağlamak için kullanır. `nuget pack`veya diğer [istemci araçlarıyla](../install-nuget-client-tools.md) paketleme, öğeyi [`licenseUrl`](../reference/nuspec.md#licenseurl) desteklemeyen eski istemcilerle geriye dönük `license` uyumluluk sağlamak için licenses.nuget.org işaret etmek için öğeyi ayarlar.

## <a name="protocol"></a>Protokol

Licenses.nuget.org tarayıcılarında insanlar tarafından görüntülenecek şekilde tasarlanmıştır, makine tarafından okunabilir yanıt lar sağlanmaz.
HTTPS protokolü kullanılmalıdır ve isteklerin belirli bir şekilde inşa edilmesi beklenmektedir. Yalnızca istekleri `GET` destekler.
Lisans ifadelerini veya lisans özel durum tanımlayıcılarını aşağıda belirtilen bir şekilde giriş olarak kabul eder. Lisans ifadelerinin tüm öğelerinin büyük/küçük harf duyarlı olduğunu ve bu nedenle licenses.nuget.org tüm girişlerin de büyük/küçük harf duyarlı olduğunu unutmayın.

### <a name="license-expressions"></a>Lisans ifadeleri

#### <a name="request"></a>İstek

Lisans ifadeleri (ifadenin tek bir lisanstan oluştuğu önemsiz durumlar da dahil olmak üzere) [URL kodlanması](https://tools.ietf.org/html/rfc3986#section-2.1) ve licenses.nuget.org isteğinde yol olarak kullanılması gerekir.

| Lisans ifadesi | Kullanılacak URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-sadece FLTK-istisna VEYA Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

Hizmet, yalnızca nuget.org tarafından kabul edilen lisans tanımlayıcılarını ve lisans özel durum tanımlayıcılarını destekler. Desteklenmeyen lisans tanımlayıcıları veya lisans özel durum tanımlayıcıları içeren veya lisans ifade sözdizimine uymayan tüm lisans ifadeleri geçersiz sayılır.

#### <a name="response"></a>Yanıt

Licenses.nuget.org, http 200 durum kodu ve lisans ifadesinin açıklamasını içeren bir web sayfası ile geçerli lisans ifadeleri içeren istekleri yanıtlar:

* verilen lisans ifadesi tek bir lisans tanımlayıcısı içeriyorsa, bu lisans başvuru metnini içeren bir web sayfası döndürülür;
* verilen lisans ifadesi bileşik bir lisans ifadesiyse, tek tek lisans veya lisans özel durum başvurularına bağlantılar içeren lisans ifadesini içeren bir web sayfası döndürülür.

Geçersiz bir lisans ifadesi içeren tüm istekler, HTTP 404 yanıtıyla sonuçlanır.

### <a name="license-exceptions"></a>Lisans istisnaları

#### <a name="request"></a>İstek

Lisans özel durum tanımlayıcıları URL kodlu olmalı ve licenses.nuget.org isteğinde bir yol olarak kullanılmalıdır. Tek bir istekte yalnızca tek bir lisans özel durum tanımlayıcısı sağlanabilir. URL'nin yol bölümünde lisans özel durum tanımlayıcısı dışında ek karakter bulunmaz.

| Lisans özel durum tanımlayıcısı | Kullanılacak URL |
|:---|:---|
|FLTK-istisna            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>Yanıt

Licenses.nuget.org, http 200 yanıtı ve belirtilen lisans özel durumu için başvuru metnini içeren bir web sayfası ile bilinen bir lisans özel durum tanımlayıcısı ile bir isteğe yanıt verir.

Desteklenmeyen lisans özel durum tanımlayıcısı içeren herhangi bir istek, HTTP 404 yanıtıyla sonuçlanır.