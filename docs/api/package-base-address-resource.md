---
title: Paket içeriğini, NuGet API
description: Paket taban adresi paket yakalama için basit bir arabirimdir.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819183"
---
# <a name="package-content"></a>Paket içeriği

V3 API'sini kullanarak rastgele bir paketin içerik (.nupkg dosyasını) getirmek için bir URL oluşturmak mümkündür. Paket içeriğini getirmek için kullanılan kaynak `PackageBaseAddress` kaynak bulunan [Hizmeti dizini](service-index.md). Bu kaynak bulma listelenen bir paketin tüm sürümleri de etkinleştirir ya da listelenmemiş.

Bu kaynak genellikle ya da "paketi taban adresi" veya "düz kapsayıcı" olarak adlandırılır.

## <a name="versioning"></a>Sürüm oluşturma

Aşağıdaki `@type` değeri kullanılır:

@type Değer              | Notlar
------------------------ | -----
PackageBaseAddress/3.0.0 | İlk sürüm

## <a name="base-url"></a>Temel URL

Aşağıdaki API'leri için temel URL değeri `@id` özelliği daha önce bahsedilen kaynakla ilişkilendirilmiş `@type` değeri. Aşağıdaki belgede yer tutucu temel URL `{@id}` kullanılır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynak desteği HTTP yöntemleri bulunan tüm URL'leri `GET` ve `HEAD`.

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

İstemci bir paket kimliği bilir ve hangi sürümleri paket paketini bulmak istiyorsa kaynak kullanılabilir olan, tüm paket sürümlerini listeleme için tahmin edilebilir URL'sini istemcisi oluşturabilirsiniz. Bu liste, aşağıda belirtilen paket içeriği API için "dizin listeleme" olması amaçlanmıştır.

> [!Note]
> Bu liste, her iki listelenen hem de listelenmeyen paket sürümünü içerir.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>İstek parametreleri

Ad     | İçindeki     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | dize  | Evet      | Paket kimliği, küçük harf

`LOWER_ID` Tarafından uygulanan kurallarını kullanarak dönüştürüldükten istenen paket kimliği bir değerdir. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

### <a name="response"></a>Yanıt

Paket kaynağı sağlanan paket Kimliğini hiçbir sürümü varsa, 404 durum kodu döndürülür.

Paket kaynağı bir veya birden çok sürüm varsa, 200 durum kodu döndürülür. Yanıt gövdesi aşağıdaki özelliğine sahip bir JSON nesnesidir:

Ad     | Tür             | Gerekli | Notlar
-------- | ---------------- | -------- | -----
sürümler | Dize dizisi | Evet      | Paket kimlikleri kullanılabilir

Dizelerde `versions` dizi tüm dönüştürüldükten, [NuGet sürümü dizeleri normalleştirilmiş](../reference/package-versioning.md#normalized-version-numbers). Sürüm dizelerini SemVer 2.0.0 Yapı meta verileri içermez.

Bu dizide bulunan sürüm dizelerini için aynen kullanılabilir amacı olan `LOWER_VERSION` belirteçleri aşağıdaki uç noktalardan bulundu.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>(.Nupkg) paket içeriğini indirme

İstemci paketi Kimliğini ve sürümünü bilir ve paket içeriğini indirme istiyorsa, yalnızca aşağıdaki URL'yi oluşturmak ihtiyaç duydukları:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>İstek parametreleri

Ad          | İçindeki     | Tür   | Gerekli | Notlar
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | dize | Evet      | Paket kimliği, küçük harf
LOWER_VERSION | URL    | dize | Evet      | Normalleştirilmiş ve dönüştürüldükten Paket sürümü

Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallarını kullanarak dönüştürüldükten. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kurallarını](../reference/package-versioning.md#normalized-version-numbers). Bu, bu durumda SemVer 2.0.0 belirtimine göre izin yapı meta verilerin hariç tutulan anlamına gelir.

### <a name="response-body"></a>Yanıt gövdesi

Paketi paket kaynağında varsa, 200 durum kodu döndürülür. Yanıt gövdesi paket içeriğini olacaktır.

Paketi paket kaynağında bulunmadığı bir 404 durum kodu döndürülür.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Örnek yanıt

Newtonsoft.Json 9.0.1 .nupkg ikili akışın.

## <a name="download-package-manifest-nuspec"></a>Paket bildirimi (.nuspec) yükle

İstemci paketi Kimliğini ve sürümünü bilir ve paket bildirimi karşıdan istiyorsa, yalnızca aşağıdaki URL'yi oluşturmak ihtiyaç duydukları:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>İstek parametreleri

Ad          | İçindeki     | Tür    | Gerekli | Notlar
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | dize  | Evet      | Paket kimliği, küçük harf
LOWER_VERSION | URL    | tamsayı | Evet      | Normalleştirilmiş ve dönüştürüldükten Paket sürümü

Her ikisi de `LOWER_ID` ve `LOWER_VERSION` tarafından uygulanan kurallarını kullanarak dönüştürüldükten. NET'in [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) yöntemi.

`LOWER_VERSION` NuGet sürümü kullanılarak istenen paket sürümü normalleştirilmiş [normalleştirme kurallarını](../reference/package-versioning.md#normalized-version-numbers). Bu, bu durumda SemVer 2.0.0 belirtimine göre izin yapı meta verilerin hariç tutulan anlamına gelir.

### <a name="response-body"></a>Yanıt gövdesi

Paketi paket kaynağında varsa, 200 durum kodu döndürülür. Yanıt gövdesi içinde karşılık gelen .nupkg bulunan .nuspec olduğundan paket bildirimi olacaktır. .nuspec bir XML dosyasıdır.

Paketi paket kaynağında bulunmadığı bir 404 durum kodu döndürülür.

### <a name="sample-request"></a>Örnek istek

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Örnek yanıt

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
