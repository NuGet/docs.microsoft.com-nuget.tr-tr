---
title: Rapor kötüye URL şablonu, NuGet API'si
description: Rapor kötüye URL şablonu, bunların kullanıcı Arabiriminde bir rapor kötüye bağlantı görüntüler etmesine olanak tanır.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549345"
---
# <a name="report-abuse-url-template"></a>Rapor kötüye URL şablonu

Uygunsuz kullanımı hakkında belirli bir paket için bir kullanıcı tarafından kullanılabilecek bir URL oluşturmak bir istemci mümkündür. Uygunsuz kullanım raporları paket kaynağına temsilci seçmek tüm istemci deneyimleri (hatta 3. taraf) etkinleştirmek bir paket kaynağı istediğinde, bu yararlıdır.

Bu URL'yi oluşturmak için kullanılan kaynak `ReportAbuseUriTemplate` kaynak bulunan [hizmet dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerleri kullanılır:

@type Değer                       | Notlar
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | İlk yayın
ReportAbuseUriTemplate/3.0.0-rc   | Diğer adı `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL şablonu

Aşağıdaki API URL'si değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri.

## <a name="http-methods"></a>HTTP yöntemleri

İstemci istekleri için rapor Uygunsuz kullanım bildirme URL'si kullanıcı adına yapmak için tasarlanmamıştır olsa da, web sayfası desteklemelidir `GET` bir web tarayıcısından kolayca açılması tıklanan URL izin vermek için yöntemi.

## <a name="construct-the-url"></a>URL'sini oluşturun

Verilen bir bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimine erişmek için kullanılan bir URL oluşturabilirsiniz. İstemci uygulaması, bu oluşturulan URL (veya tıklatılabilir bir bağlantı) URL'sine bir web tarayıcısı açın ve tüm gerekli kötüye rapor yapmak için bunları izin vererek kullanıcıya görüntülemelidir. Uygunsuz kullanım raporu form uygulaması sunucu uygulaması tarafından belirlenir.

Değerini `@id` herhangi bir aşağıdaki yer tutucu belirteçler içeren bir URL dize:

### <a name="url-placeholders"></a>URL yer tutucuları

Ad        | Tür    | Gerekli | Notlar
----------- | ------- | -------- | -----
`{id}`      | dize  | Yok       | Uygunsuz kullanımı için paket kimliği
`{version}` | dize  | Yok       | Uygunsuz kullanımı için için Paket sürümü

`{id}` Ve `{version}` sunucu uygulaması tarafından yorumlanan değerler büyük küçük harfe duyarlı ve duyarlı olup sürüm normalleştirilmiştir için olmalıdır.

Örneğin, nuget.org rapor kötüye şablonu şöyle görünür:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

İstemci uygulaması 4.3.0 NuGet.Versioning için rapor kötüye formuna bir bağlantı görüntülenecek gerekiyorsa aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
