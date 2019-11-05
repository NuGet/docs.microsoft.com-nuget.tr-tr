---
title: NuGet. exe sürümlerini bulmak için Tools. JSON
description: İçin uç nokta
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611028"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>NuGet. exe sürümlerini bulmak için Tools. JSON

Bugün, makinenizde bulunan NuGet. exe ' nin en son sürümünü komut dosyası biçiminde bir biçimde almanın birkaç yolu vardır. Örneğin, nuget.org adresinden [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) paketini indirebilir ve ayıklayabilirsiniz. Bu, zaten NuGet. exe ' ye sahip olmanızı gerektirdiğinden (`nuget.exe install`için) veya temel bir unzip aracı kullanarak. nupkg 'yi açmak ve içinde ikilileri bulmak için bazı karmaşıklığa sahiptir.

Zaten NuGet. exe ' ye sahipseniz `nuget.exe update -self`de kullanabilirsiniz, ancak bunun için aynı NuGet. exe kopyasının olması gerekir. Bu yaklaşım, sizi en son sürüme de güncelleştirir. Belirli bir sürümün kullanılmasına izin vermez.

`tools.json` uç noktası her ikisi de önyükleme sorununu çözüyor ve indireceğiniz NuGet. exe sürümünün denetimini vermek için kullanılabilir. Bu, bir NuGet. exe ' nin yayınlanan sürümünü bulup indirmek için CI/CD ortamlarında veya özel betikte kullanılabilir.

`tools.json` uç noktası, kimliği doğrulanmamış bir HTTP isteği (örn. `Invoke-WebRequest` PowerShell veya `wget`) kullanılarak getirilebilir. JSON seri hale getirici kullanılarak ayrıştırılabilir ve sonraki NuGet. exe indirme URL 'Leri, kimliği doğrulanmamış HTTP istekleri kullanılarak da getirilebilir.

Uç nokta `GET` yöntemi kullanılarak getirilebilir:

    GET https://dist.nuget.org/tools.json

Uç nokta için [JSON şemasına](https://json-schema.org/) buradan ulaşılabilir:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Yanıtıyla

Yanıt, NuGet. exe ' nin tüm kullanılabilir sürümlerini içeren bir JSON belgesidir.

Kök JSON nesnesi aşağıdaki özelliğe sahiptir:

Name      | Tür             | Gerekli
--------- | ---------------- | --------
nuget.exe | nesne dizisi | Yes

`nuget.exe` dizisindeki her bir nesne aşağıdaki özelliklere sahiptir:

Name     | Tür   | Gerekli | Notlar
-------- | ------ | -------- | -----
sürüm  | dize | Yes      | Bir SemVer 2.0.0 dizesi
'deki      | dize | Yes      | NuGet. exe ' nin bu sürümünü indirmek için mutlak URL
Aşama    | dize | Yes      | Bir sabit listesi dizesi
açma | dize | Yes      | Sürümün kullanılabilir hale getirilme yaklaşık ISO 8601 zaman damgası

Dizideki öğeler azalan, SemVer 2.0.0 sırasına göre sıralanır. Bu garanti, en yüksek sürüm numarasıyla ilgilenen bir istemcinin yükünü azaltmaya yöneliktir. Ancak bu, listenin kronolojik sırada sıralanmadığını ifade etmez. Örneğin, daha yüksek bir ana sürümden daha sonraki bir tarihte daha düşük bir ana sürüm servise alınmış ise, bu hizmet verilen sürüm listenin en üstünde görünmez. En son sürümün *zaman damgasıyla*serbest bırakılacağını istiyorsanız diziyi `uploaded` dize ile sıralayın. Bu, `uploaded` zaman damgası [ıso 8601](https://www.iso.org/iso-8601-date-and-time-format.html) biçiminde olduğundan, bir lexicografik sıralaması kullanılarak kronolojik olarak sıralanabilen (yani basit bir dize sıralaması) bu işe yarar.

`stage` özelliği, aracın bu sürümünün ne olduğunu gösterir. 

Aşama              | Açıklama
------------------ | ------
EarlyAccessPreview | Henüz [indirme web sayfasında](https://www.nuget.org/downloads) görünmez ve iş ortakları tarafından doğrulanması gerekir
Yayınlandı           | İndirme sitesinde kullanılabilir ancak geniş yayılmış tüketim için henüz önerilmez
ReleasedAndBlessed | İndirme sitesinde kullanılabilir ve tüketim için önerilir

En son önerilen sürüme sahip olmanın tek bir yaklaşımı, listenin `ReleasedAndBlessed``stage` değerine sahip ilk sürümü kullanmaktır. Sürümler SemVer 2.0.0 Order içinde sıralandığından bu işe yarar.

Nuget.org üzerindeki `NuGet.CommandLine` paketi genellikle yalnızca `ReleasedAndBlessed` sürümleriyle güncelleştirilir.

### <a name="sample-request"></a>Örnek istek

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [tools-json.json](./_data/tools-json.json)]
