---
title: Paket ayrıntıları URL şablonu, NuGet API 'SI
description: Paket ayrıntıları URL 'SI şablonu, istemcilerin Kullanıcı arabiriminde daha fazla paket ayrıntılarına görüntülenmesini sağlar
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610952"
---
# <a name="package-details-url-template"></a>Paket ayrıntıları URL şablonu

Bir istemcinin, Web tarayıcılarında daha fazla paket ayrıntılarını görmek için Kullanıcı tarafından kullanılabilecek bir URL oluşturması mümkündür. Bu, bir paket kaynağı, NuGet istemci uygulamasının gösterdiği işlem kapsamında sığmayan bir paket hakkında ek bilgiler göstermek istediğinde yararlıdır.

Bu URL 'YI oluşturmak için kullanılan kaynak, [hizmet dizininde](service-index.md)bulunan `PackageDetailsUriTemplate` kaynağıdır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değerleri kullanılır:

@type değeri                     | Notlar
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | İlk yayın

## <a name="url-template"></a>URL şablonu

Aşağıdaki API 'nin URL 'SI, belirtilen kaynak `@type` değerlerinden biriyle ilişkili `@id` özelliğinin değeridir.

## <a name="http-methods"></a>HTTP yöntemleri

İstemci, Kullanıcı adına paket ayrıntıları URL 'sine istek yapmaya yönelik değildir, ancak Web sayfası, tıklanan bir URL 'nin bir Web tarayıcısında kolayca açılmasını sağlamak için `GET` yöntemini desteklemelidir.

## <a name="construct-the-url"></a>URL 'YI oluşturun

Bilinen bir paket KIMLIĞI ve sürümü verildiğinde, istemci uygulama bir Web arabirimine erişmek için kullanılan bir URL oluşturabilir. İstemci uygulamasının bu oluşturulmuş URL 'yi (veya tıklatılabilir bağlantıyı) kullanıcıya URL 'ye bir Web tarayıcısı açmasına ve paket hakkında daha fazla bilgi edinmesine izin verecek şekilde görüntülemesi gerekir. Paket ayrıntıları sayfasının içeriği sunucu uygulamasına göre belirlenir.

URL 'nin mutlak bir URL olması ve düzenin (protokol) HTTPS olması gerekir.

Hizmet dizinindeki `@id` değeri, aşağıdaki yer tutucu belirteçlerinden herhangi birini içeren bir URL dizesidir:

### <a name="url-placeholders"></a>URL yer tutucuları

Name        | Tür    | Gerekli | Notlar
----------- | ------- | -------- | -----
`{id}`      | dize  | eşleşen       | Ayrıntıları almak için paket KIMLIĞI
`{version}` | dize  | eşleşen       | Ayrıntıları alınacak paket sürümü

Sunucu, herhangi bir büyük küçük harf ile `{id}` ve `{version}` değerlerini kabul etmelidir. Buna ek olarak, sunucu, sürümünün [normalleştirilme](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)olup olmadığına duyarlı olmamalıdır. Diğer bir deyişle, sunucu kabul edilmelidir, ayrıca Normalleştirilmemiş sürümleri kabul etmelidir.

Örneğin, NuGet. org 'ın paket ayrıntıları şablonu şöyle görünür:

    https://www.nuget.org/packages/{id}/{version}

İstemci uygulamasının NuGet. sürümlendirme 4.3.0 için paket ayrıntılarına bir bağlantı görüntülemesi gerekiyorsa, aşağıdaki URL 'YI oluşturur ve kullanıcıya sağlar:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
