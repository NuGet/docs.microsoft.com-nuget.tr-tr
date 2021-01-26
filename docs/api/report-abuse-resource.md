---
title: Uygunsuz kullanım URL şablonunu bildir, NuGet API
description: Uygunsuz kullanım URL 'SI şablonu, istemcilerin Kullanıcı arabiriminde kötü bir rapor uygunsuz bağlantı görüntülemesini sağlar.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775226"
---
# <a name="report-abuse-url-template"></a>Uygunsuz kullanım URL şablonunu raporla

Bir istemcinin belirli bir paket hakkında uygunsuz kullanımı raporlamak için Kullanıcı tarafından kullanılabilecek bir URL oluşturması mümkündür. Bu, bir paket kaynağı tüm istemci deneyimlerini (hatta 3. taraf), çok kişili raporların paket kaynağına atamasını sağlamak istediğinde yararlıdır.

Bu URL 'YI oluşturmak için kullanılan kaynak, `ReportAbuseUriTemplate` [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@type deeri                       | Notlar
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-Beta | İlk yayın
ReportAbuseUriTemplate/3.0.0-RC   | Diğer adı `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL şablonu

Aşağıdaki API 'nin URL 'SI, `@id` belirtilen kaynak değerlerinden biriyle ilişkili özelliğin değeridir `@type` .

## <a name="http-methods"></a>HTTP yöntemleri

İstemci kullanıcı adına uygunsuz kullanım URL 'sine istek yapmaya yönelik değildir, ancak Web sayfası, `GET` tıklanan BIR URL 'nin bir Web tarayıcısında kolayca açılmasını sağlamak için yöntemini desteklemelidir.

## <a name="construct-the-url"></a>URL 'YI oluşturun

Bilinen bir paket KIMLIĞI ve sürümü verildiğinde, istemci uygulama bir Web arabirimine erişmek için kullanılan bir URL oluşturabilir. İstemci uygulamasının bu oluşturulmuş URL 'yi (veya tıklatılabilir bağlantıyı) kullanıcıya URL 'ye bir Web tarayıcısı açmasına ve gerekli uygunsuz kullanım raporu yapmasına izin vererek görüntülemesi gerekir. Uygunsuz kullanım raporu formunun uygulanması sunucu uygulamasına göre belirlenir.

Öğesinin değeri, `@id` aşağıdaki yer tutucu belirteçlerinden herhangi birini içeren BIR URL dizesidir:

### <a name="url-placeholders"></a>URL yer tutucuları

Ad        | Tür    | Gerekli | Notlar
----------- | ------- | -------- | -----
`{id}`      | string  | hayır       | Kötüye kullanımı raporlamak için paket KIMLIĞI
`{version}` | string  | hayır       | Kötüye kullanımı raporlamak için paket sürümü

`{id}` `{version}` Sunucu uygulamasının yorumlandığı ve değerleri, büyük/küçük harfe duyarsız olmalıdır ve sürüm normalleştirilip normalleştirilmemelidir.

Örneğin, NuGet. org 'ın uygunsuz kullanımı şablonu şöyle görünür:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

İstemci uygulamasının NuGet. sürümlendirme için uygunsuz kullanım formunun bir bağlantısını görüntülemesi gerekiyorsa, aşağıdaki URL 'YI oluşturur ve kullanıcıya sağlar:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
