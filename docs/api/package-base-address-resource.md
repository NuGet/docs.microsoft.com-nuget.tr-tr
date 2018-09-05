---
title: Paket içeriğini, NuGet API'si
description: Paket temel adres, paket yakalama için basit bir arabirimdir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547160"
---
# <a name="package-content"></a>Paket içeriği

V3 API'sini kullanarak rastgele bir paketin içerik (.nupkg dosyası) getirmek için bir URL oluşturmak mümkündür. Paket içeriğini getirmek için kullanılan kaynak `PackageBaseAddress` kaynak bulunan [hizmet dizini](service-index.md). Bu kaynak ayrıca listelenen, bir paketin tüm sürümlerini bulunmasını sağlar veya listeden kaldırıldı.

Bu kaynak genellikle ya da "Paket taban adresi" veya "düz kapsayıcı" olarak adlandırılır.

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer              | Notlar
------------------------ | -----
PackageBaseAddress/3.0.0 | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` yukarıda sözü edilen kaynakla ilişkilendirilmiş özelliği `@type` değeri. Aşağıdaki belgede, yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'ler `GET` ve `HEAD`.

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

İstemci bildiği bir paket kimliği ve paket sürümleri, paketi bulmak istediği kaynak kullanılabilir olan, istemci paket sürümlerini tüm numaralandırmak için tahmin edilebilir bir URL oluşturabilirsiniz. Bu liste, aşağıda belirtilen paket içeriği API için "dizin listeleme" olması için tasarlanmıştır.

> [!Note]
> Bu liste, her iki listelenen ve listelenmemiş paket sürümlerini içerir.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>İstek parametreleri

Ad     | İçindeki     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | dize  | Evet      | Paket kimliği, küçük harf

`LOWER_ID` Tarafından uygulanan kurallar kullanarak küçük harfli istenen paket kimliği bir değerdir. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

### <a name="response"></a>Yanıt

Paket kaynağı, sağlanan paket kimliği hiçbir sürümü varsa, bir 404 durum kodu döndürülür.

Paket kaynağı, bir veya daha fazla sürümü varsa, bir 200 durum kodu döndürülür. Yanıt gövdesi, aşağıdaki özelliklerle bir JSON nesnesidir:

Ad     | Tür             | Gerekli | Notlar
-------- | ---------------- | -------- | -----
sürümler | dize dizisi | Evet      | ' % S'paketi kimliklerini kullanılabilir

Dizelerde `versions` dizi tüm küçük harfli, [NuGet sürüm dizeleri normalleştirilmiş](../reference/package-versioning.md#normalized-version-numbers). Sürüm dizeleri SemVer 2.0.0 derleme meta verileri içermez.

Bu dizinin içinde bulunan sürüm dizeleri için verbatim kullanılabilir amacı olan `LOWER_VERSION` belirteçleri aşağıdaki uç noktaların bulunamadı.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>(.Nupkg) paket içeriğini indirme

İstemci paketi Kimliğini ve sürümünü bilir ve paket içeriğini indirme istediği, yalnızca aşağıdaki URL'yi oluşturmak için ihtiyaçları:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>İstek parametreleri

Ad          | İçindeki     | Tür   | Gerekli | Notlar
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | dize | Evet      | Paket kimliği, küçük harf
LOWER_VERSION | URL    | dize | Evet      | Normalleştirilmiş ve küçük harf yapılmış Paket sürümü

Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallar kullanarak küçük harf yapılmış. NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
yöntem.

`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kuralları](../reference/package-versioning.md#normalized-version-numbers). Başka bir deyişle, bu durumda SemVer 2.0.0 belirtimine göre izin verilen derleme meta verilerin tutulması gerekir.

### <a name="response-body"></a>Yanıt gövdesi

Paketin paket kaynak var, 200 durum kodu döndürülür. Yanıt gövdesi, paket içeriğini olacaktır.

Paketin paket kaynak mevcut değilse bir 404 durum kodu döndürülür.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Örnek yanıt

Newtonsoft.Json 9.0.1 için .nupkg ikili akışın.

## <a name="download-package-manifest-nuspec"></a>Paket bildirimi (.nuspec) indirin

İstemci paketi Kimliğini ve sürümünü bilir ve paket bildirimi indirmek ister bunlar yalnızca aşağıdaki URL'yi oluşturmak gerekir:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>İstek parametreleri

Ad          | İçindeki     | Tür    | Gerekli | Notlar
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | dize  | Evet      | Paket kimliği, küçük harf
LOWER_VERSION | URL    | tamsayı | Evet      | Normalleştirilmiş ve küçük harf yapılmış Paket sürümü

Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallar kullanarak küçük harf yapılmış. NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kuralları](../reference/package-versioning.md#normalized-version-numbers). Başka bir deyişle, bu durumda SemVer 2.0.0 belirtimine göre izin verilen derleme meta verilerin tutulması gerekir.

### <a name="response-body"></a>Yanıt gövdesi

Paketin paket kaynak var, 200 durum kodu döndürülür. Yanıt gövdesi içinde karşılık gelen .nupkg bulunan .nuspec olan paket bildirimi olacaktır. .nuspec bir XML dosyasıdır.

Paketin paket kaynak mevcut değilse bir 404 durum kodu döndürülür.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Örnek yanıt

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
