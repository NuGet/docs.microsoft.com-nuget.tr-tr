---
title: nuget.exe sürümlerini keşfetmek için tools.js
description: İçin uç nokta
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773823"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>nuget.exe sürümlerini keşfetmek için tools.js

Bugün, makinenizde nuget.exe en son sürümünü bir komut dosyası biçiminde almak için birkaç yol vardır. Örneğin, [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) NuGet.org adresinden paketi indirebilir ve ayıklayabilirsiniz. Bu, zaten nuget.exe (için) sahip olmanızı gerektirdiğinden `nuget.exe install` ya da temel bir unzip aracı kullanarak. nupkg 'yi açmak ve içinde ikilileri bulmak için bazı karmaşıklığa sahiptir.

Zaten nuget.exe varsa, bunu da kullanabilirsiniz `nuget.exe update -self` , ancak bunun için de nuget.exe bir kopyasının olması gerekir. Bu yaklaşım, sizi en son sürüme de güncelleştirir. Belirli bir sürümün kullanılmasına izin vermez.

`tools.json`Uç nokta her ikisi de önyükleme sorununu çözüyor ve indireceğiniz nuget.exe sürümünün denetimini sağlamak için kullanılabilir. Bu, CI/CD ortamlarında veya nuget.exe yayınlanan herhangi bir sürümünü bulup indirmek için özel betiklerin içinde kullanılabilir.

`tools.json`Uç nokta, kimliği doğrulanmamış BIR http isteği (örn. `Invoke-WebRequest` PowerShell veya) kullanılarak getirilebilir `wget` . JSON seri hale getirici kullanılarak ayrıştırılabilir ve sonraki nuget.exe indirme URL 'Leri, kimliği doğrulanmamış HTTP istekleri kullanılarak da getirilebilir.

Uç nokta, yöntemi kullanılarak getirilebilir `GET` :

```
GET https://dist.nuget.org/tools.json
```

Uç nokta için [JSON şemasına](https://json-schema.org/) buradan ulaşılabilir:

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a>Yanıt

Yanıt, tüm kullanılabilir nuget.exe sürümlerini içeren bir JSON belgesidir.

Kök JSON nesnesi aşağıdaki özelliğe sahiptir:

Ad      | Tür             | Gerekli
--------- | ---------------- | --------
nuget.exe | nesne dizisi | evet

Dizideki her bir nesne `nuget.exe` aşağıdaki özelliklere sahiptir:

Ad     | Tür   | Gerekli | Notlar
-------- | ------ | -------- | -----
sürüm  | string | evet      | Bir SemVer 2.0.0 dizesi
url      | string | evet      | Bu nuget.exe sürümünü indirmek için mutlak URL
sahna    | string | evet      | Bir sabit listesi dizesi
açma | string | evet      | Sürümün kullanılabilir hale getirilme yaklaşık ISO 8601 zaman damgası

Dizideki öğeler azalan, SemVer 2.0.0 sırasına göre sıralanır. Bu garanti, en yüksek sürüm numarasıyla ilgilenen bir istemcinin yükünü azaltmaya yöneliktir. Ancak bu, listenin kronolojik sırada sıralanmadığını ifade etmez. Örneğin, daha yüksek bir ana sürümden daha sonraki bir tarihte daha düşük bir ana sürüm servise alınmış ise, bu hizmet verilen sürüm listenin en üstünde görünmez. En son sürümün *zaman damgasıyla* serbest bırakılacağını istiyorsanız diziyi dize ile sıralayın `uploaded` . Bu, `uploaded` zaman damgası [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) biçiminde olduğundan, bir lexicografik sıralaması kullanılarak kronolojik olarak sıralanabilen (basit bir dize sıralaması) bu işe yarar.

`stage`Özelliği, aracın bu sürümünün ne olduğunu gösterir. 

Aşama              | Anlamı
------------------ | ------
EarlyAccessPreview | Henüz [indirme web sayfasında](https://www.nuget.org/downloads) görünmez ve iş ortakları tarafından doğrulanması gerekir
Yayınlandı           | İndirme sitesinde kullanılabilir ancak geniş yayılmış tüketim için henüz önerilmez
ReleasedAndBlessed | İndirme sitesinde kullanılabilir ve tüketim için önerilir

En son, önerilen sürüme sahip olmanın bir basit yaklaşımı, bu değeri içeren listedeki ilk sürümü kullanmaktır `stage` `ReleasedAndBlessed` . Sürümler SemVer 2.0.0 Order içinde sıralandığından bu işe yarar.

`NuGet.CommandLine`NuGet.org üzerindeki paket genellikle yalnızca `ReleasedAndBlessed` sürümleriyle güncelleştirilir.

### <a name="sample-request"></a>Örnek istek

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [tools-json.json](./_data/tools-json.json)]
