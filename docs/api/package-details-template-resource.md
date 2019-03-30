---
title: Paket Ayrıntıları URL şablonu, NuGet API'si
description: Paket Ayrıntıları URL şablonu, bunların kullanıcı arabiriminde bir web bağlantısı için daha fazla paket ayrıntılarını görüntülemek istemcilerin
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638089"
---
# <a name="package-details-url-template"></a>Paket Ayrıntıları URL şablonu

Web tarayıcısında daha fazla paket ayrıntılarını görmek için kullanıcı tarafından kullanılan bir URL oluşturmak bir istemci mümkündür. Paket kaynağı olmayan bir çözüm paketi hakkında ek bilgi ne NuGet istemci uygulaması gösterir, kapsam içinde gösterilecek istediğinde, bu yararlıdır.

Bu URL'yi oluşturmak için kullanılan kaynak `PackageDetailsUriTemplate` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerleri kullanılır:

@type Değer                     | Notlar
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | İlk yayın

## <a name="url-template"></a>URL şablonu

Aşağıdaki API URL'si değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri.

## <a name="http-methods"></a>HTTP yöntemleri

İstemci isteğinde Paket Ayrıntıları URL'sini kullanıcı adına yönelik değildir ancak web sayfası desteklemelidir `GET` bir web tarayıcısından kolayca açılması tıklanan URL izin vermek için yöntemi.

## <a name="construct-the-url"></a>URL'sini oluşturun

Verilen bir bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimine erişmek için kullanılan bir URL oluşturabilirsiniz. İstemci uygulama, bunları izin vererek kullanıcıya URL'sine bir web tarayıcısı açın ve paket hakkında daha fazla bilgi için bu oluşturulmuş URL (veya tıklatılabilir bir bağlantı) görüntülemelidir. Paket Ayrıntıları sayfasına içeriğini sunucu uygulaması tarafından belirlenir.

URL, mutlak bir URL olmalıdır ve (Protokolü) şeması HTTPS olmalıdır.

Değerini `@id` hizmetinde aşağıdaki yer tutucu belirteçler birini içeren bir URL dizesi dizinidir:

### <a name="url-placeholders"></a>URL yer tutucuları

Ad        | Tür    | Gerekli | Notlar
----------- | ------- | -------- | -----
`{id}`      | dize  | Yok       | Bilgi almak için paket kimliği
`{version}` | dize  | Yok       | Bilgi almak için Paket sürümü

Sunucu kabul etmelidir `{id}` ve `{version}` tüm büyük/küçük harf değerleri. Ayrıca, sunucu sürümü olup duyarlı olmamalıdır [normalleştirilmiş](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). Diğer bir deyişle, sunucunun kabul etmelidir normale olmayan sürümleri de kabul.

Örneğin, nuget.org Paket Ayrıntıları şablon şöyle görünür:

    https://www.nuget.org/packages/{id}/{version}

İstemci uygulama bir bağlantı için NuGet.Versioning 4.3.0 için Paket ayrıntılarını görüntülemek gerekiyorsa, aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
