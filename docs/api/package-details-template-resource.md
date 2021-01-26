---
title: Paket ayrıntıları URL şablonu, NuGet API 'SI
description: Paket ayrıntıları URL 'SI şablonu, istemcilerin Kullanıcı arabiriminde daha fazla paket ayrıntılarına görüntülenmesini sağlar
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773953"
---
# <a name="package-details-url-template"></a>Paket ayrıntıları URL şablonu

Bir istemcinin, Web tarayıcılarında daha fazla paket ayrıntılarını görmek için Kullanıcı tarafından kullanılabilecek bir URL oluşturması mümkündür. Bu, bir paket kaynağı, NuGet istemci uygulamasının gösterdiği işlem kapsamında sığmayan bir paket hakkında ek bilgiler göstermek istediğinde yararlıdır.

Bu URL 'YI oluşturmak için kullanılan kaynak, `PackageDetailsUriTemplate` [hizmet dizininde](service-index.md)bulunan kaynaktır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerler kullanılır:

@type deeri                     | Notlar
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | İlk yayın

## <a name="url-template"></a>URL şablonu

Aşağıdaki API 'nin URL 'SI, `@id` belirtilen kaynak değerlerinden biriyle ilişkili özelliğin değeridir `@type` .

## <a name="http-methods"></a>HTTP yöntemleri

İstemci, Kullanıcı adına paket ayrıntıları URL 'sine istek yapmaya yönelik değildir, ancak Web sayfası, `GET` tıklanan BIR URL 'nin bir Web tarayıcısında kolayca açılmasını sağlamak için yöntemini desteklemelidir.

## <a name="construct-the-url"></a>URL 'YI oluşturun

Bilinen bir paket KIMLIĞI ve sürümü verildiğinde, istemci uygulama bir Web arabirimine erişmek için kullanılan bir URL oluşturabilir. İstemci uygulamasının bu oluşturulmuş URL 'yi (veya tıklatılabilir bağlantıyı) kullanıcıya URL 'ye bir Web tarayıcısı açmasına ve paket hakkında daha fazla bilgi edinmesine izin verecek şekilde görüntülemesi gerekir. Paket ayrıntıları sayfasının içeriği sunucu uygulamasına göre belirlenir.

URL 'nin mutlak bir URL olması ve düzenin (protokol) HTTPS olması gerekir.

Hizmet dizinindeki öğesinin değeri, `@id` aşağıdaki yer tutucu belirteçlerinden herhangi birini içeren BIR URL dizesidir:

### <a name="url-placeholders"></a>URL yer tutucuları

Ad        | Tür    | Gerekli | Notlar
----------- | ------- | -------- | -----
`{id}`      | string  | hayır       | Ayrıntıları almak için paket KIMLIĞI
`{version}` | string  | hayır       | Ayrıntıları alınacak paket sürümü

Sunucu, `{id}` `{version}` herhangi bir büyük harf ile değer kabul etmelidir. Buna ek olarak, sunucu, sürümünün [normalleştirilme](../concepts/package-versioning.md#normalized-version-numbers)olup olmadığına duyarlı olmamalıdır. Diğer bir deyişle, sunucu kabul edilmelidir, ayrıca Normalleştirilmemiş sürümleri kabul etmelidir.

Örneğin, NuGet. org 'ın paket ayrıntıları şablonu şöyle görünür:

```http
https://www.nuget.org/packages/{id}/{version}
```

İstemci uygulamasının NuGet. sürümlendirme 4.3.0 için paket ayrıntılarına bir bağlantı görüntülemesi gerekiyorsa, aşağıdaki URL 'YI oluşturur ve kullanıcıya sağlar:

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
