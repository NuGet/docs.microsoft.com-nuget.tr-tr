---
title: "Rapor kötüye URL şablonu, NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Rapor kötüye URL şablonu rapor kötüye bağlantısı kendi kullanıcı Arabiriminde görüntülenecek istemcilerin sağlar."
keywords: "NuGet API rapor kötüye, NuGet API dosya uyumlu, nuget.org rapor URL şablonu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: efbe5704e6e6028f9382fea3fe5ec453f573a2e9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="report-abuse-url-template"></a>Rapor kötüye URL şablonu

Belirli bir paket hakkında bildirmek için kullanıcı tarafından kullanılabilecek bir URL oluşturmak bir istemci mümkündür. Paket kaynağında Uygunsuz kullanım raporları paket kaynağına temsilci seçmek tüm istemci deneyimleri (hatta 3. taraf) etkinleştirmek istediğinde, bu yararlıdır.

Paket içeriğini getirmek için kullanılan kaynak `ReportAbuseUriTemplate` kaynak bulunan [Hizmeti dizini](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değerler kullanılır:

@type Değer                       | Notlar
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | İlk sürüm
ReportAbuseUriTemplate/3.0.0-rc   | Diğer adı `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL şablonu

Aşağıdaki API için URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri.

## <a name="http-methods"></a>HTTP yöntemleri

İstemci kullanıcı adına rapor kötüye URL'ye istekte amaçlanmamıştır rağmen web sayfası desteklemelidir `GET` yöntemi bir web tarayıcısında kolayca açılması için tıklatılan URL izin vermek için.

## <a name="construct-the-url"></a>URL oluşturmak

Verilen bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimi erişmek için kullanılan bir URL oluşturur. İstemci uygulaması, bu oluşturulan URL'si (veya tıklatılabilir bir bağlantı) URL bir web tarayıcısı açın ve tüm gerekli Uygunsuz kullanım raporu yapmak için vermeden kullanıcı görüntülemelidir. Uygunsuz kullanım raporu form uyarlamasını sunucu uygulaması tarafından belirlenir.

Değeri `@id` olan aşağıdaki yer tutucu belirteçleri birini içeren bir URL dizesi:

### <a name="url-placeholders"></a>URL yer tutucuları

Ad        | Tür    | Gerekli | Notlar
----------- | ------- | -------- | -----
`{id}`      | dize  | Yok       | Paket kimliği için bildirmek için
`{version}` | dize  | Yok       | Paket sürümü için bildirmek için

`{id}` Ve `{version}` büyük küçük harfe duyarlı ve sürüm olup olmadığı normalleştirmesini için hassas sunucu uygulaması tarafından yorumlanan değerleri olmalıdır.

Örneğin, nuget.org rapor kötüye şablonu şöyle görünür:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

İstemci uygulaması bir bağlantıyı rapor kötüye formun NuGet.Versioning 4.3.0 görüntülemek gerekirse, aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
