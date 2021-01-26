---
title: Paket Içeriği, NuGet API 'SI
description: Paket taban adresi, paketin kendisini getirmeye yönelik basit bir arabirimdir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773935"
---
# <a name="package-content"></a>Paket Içeriği

V3 API kullanarak rastgele bir paketin içeriğini (. nupkg dosyası) getirmek için bir URL oluşturmak mümkündür. Paket içeriğini getirmek için kullanılan kaynak, `PackageBaseAddress` [hizmet dizininde](service-index.md)bulunan kaynaktır. Bu kaynak Ayrıca, listelenen veya listelenmemiş bir paketin tüm sürümlerinin bulunmasına da izin verebilir.

Bu kaynak genellikle "paket temel adresi" ya da "düz kapsayıcı" olarak adlandırılır.

## <a name="versioning"></a>Sürüm Oluşturma

Aşağıdaki `@type` değer kullanılır:

@type deeri              | Notlar
------------------------ | -----
PackageBaseAddress/3.0.0 | İlk yayın

## <a name="base-url"></a>Temel URL

Aşağıdaki API 'Lerin temel URL 'SI, `@id` belirtilen kaynak değeriyle ilişkili özelliğin değeridir `@type` . Aşağıdaki belgede, yer tutucu temel URL 'SI `{@id}` kullanılacaktır.

## <a name="http-methods"></a>HTTP yöntemleri

Kayıt kaynağında bulunan tüm URL 'Ler HTTP yöntemlerini `GET` ve ' i destekler `HEAD` .

## <a name="enumerate-package-versions"></a>Paket sürümlerini listeleme

İstemci bir paket KIMLIĞINI biliyor ve paket kaynağının hangi paket sürümlerini kullanılabilir olduğunu keşfetmesini istiyorsa, istemci tüm paket sürümlerini numaralandırmak için öngörülebilir bir URL oluşturabilir. Bu liste, aşağıda bahsedilen paket içeriği API 'SI için bir "Dizin listeleme" anlamına gelir.

> [!Note]
> Bu liste hem listelenmiş hem de listelenmemiş paket sürümlerini içerir.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>İstek parametreleri

Name     | İçinde     | Tür    | Gerekli | Notlar
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | evet      | Paket KIMLIĞI, küçük harf

`LOWER_ID`Değer, tarafından uygulanan kurallar kullanılarak istenen paket kimliği küçük harf olarak belirlenir. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) yöntemi.

### <a name="response"></a>Yanıt

Paket kaynağında belirtilen paket KIMLIĞI sürümü yoksa, 404 durum kodu döndürülür.

Paket kaynağında bir veya daha fazla sürüm varsa, 200 durum kodu döndürülür. Yanıt gövdesi, aşağıdaki özelliğe sahip bir JSON nesnesidir:

Ad     | Tür             | Gerekli | Notlar
-------- | ---------------- | -------- | -----
versions | dize dizisi | evet      | Kullanılabilir sürümler

`versions`Dizideki dizeler, tüm küçük harf, [normalleştirilmiş NuGet sürüm dizeleridir](../concepts/package-versioning.md#normalized-version-numbers). Sürüm dizeleri herhangi bir SemVer 2.0.0 derleme meta verisi içermiyor.

Amaç, bu dizide bulunan sürüm dizelerinin `LOWER_VERSION` aşağıdaki uç noktalarında bulunan belirteçler için tam olarak kullanılabileceği şekilde kullanılabilir.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Paket içeriğini indir (. nupkg)

İstemci bir paket KIMLIĞI ve sürümünü biliyor ve paket içeriğini indirmek istiyorsa, yalnızca aşağıdaki URL 'yi oluşturmak gerekir:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>İstek parametreleri

Name          | İçinde     | Tür   | Gerekli | Notlar
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | evet      | Paket KIMLIĞI, küçük harf
LOWER_VERSION | URL    | string | evet      | Paket sürümü, normalleştirilmiş ve küçük harfleri

Her ikisi de `LOWER_ID` `LOWER_VERSION` tarafından uygulanan kurallar kullanılarak küçük harfe dönüştürülür. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
yöntemidir.

, `LOWER_VERSION` NuGet 'in sürüm [normalleştirme kuralları](../concepts/package-versioning.md#normalized-version-numbers)kullanılarak istenen paket sürümü normalleştirilir. Bu, SemVer 2.0.0 belirtiminin izin verdiği derleme meta verilerinin bu durumda dışlanması gerektiği anlamına gelir.

### <a name="response-body"></a>Yanıt gövdesi

Paket, paket kaynağında varsa, 200 durum kodu döndürülür. Yanıt gövdesi, paket içeriğinin kendisi olacaktır.

Paket, paket kaynağında yoksa, 404 durum kodu döndürülür.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Örnek yanıt

9.0.1 üzerinde Newtonsoft.Jsiçin. nupkg olan ikili akış.

## <a name="download-package-manifest-nuspec"></a>Paket bildirimini indir (. nuspec)

İstemci bir paket KIMLIĞI ve sürümünü biliyor ve paket bildirimini indirmek istiyorsa, yalnızca aşağıdaki URL 'yi oluşturmak gerekir:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>İstek parametreleri

Name          | İçinde     | Tür   | Gerekli | Notlar
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | evet      | Paket KIMLIĞI, küçük harf
LOWER_VERSION | URL    | string | evet      | Paket sürümü, normalleştirilmiş ve küçük harfleri

Her ikisi de `LOWER_ID` `LOWER_VERSION` tarafından uygulanan kurallar kullanılarak küçük harfe dönüştürülür. NET 'in [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) yöntemi.

, `LOWER_VERSION` NuGet 'in sürüm [normalleştirme kuralları](../concepts/package-versioning.md#normalized-version-numbers)kullanılarak istenen paket sürümü normalleştirilir. Bu, SemVer 2.0.0 belirtiminin izin verdiği derleme meta verilerinin bu durumda dışlanması gerektiği anlamına gelir.

### <a name="response-body"></a>Yanıt gövdesi

Paket, paket kaynağında varsa, 200 durum kodu döndürülür. Yanıt gövdesi, karşılık gelen. nupkg 'da bulunan. nuspec olan paket bildirimi olacaktır. . Nuspec bir XML belgesidir.

Paket, paket kaynağında yoksa, 404 durum kodu döndürülür.

### <a name="sample-request"></a>Örnek istek

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Örnek yanıt

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
