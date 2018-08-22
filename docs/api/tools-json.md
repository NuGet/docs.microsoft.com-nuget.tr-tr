---
title: nuget.exe sürümlerini bulmak için tools.json
description: Uç nokta için
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2018
ms.locfileid: "40248917"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>nuget.exe sürümlerini bulmak için tools.json

Bugün, kodlanabilir bir biçimde makinenizde nuget.exe en son sürümünü almak için birkaç yolu vardır. Örneğin, size indirme ayıklayın ve [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org paketinden. Ya da nuget.exe sahip olduğunuz gerekir çünkü bu bazı karmaşıklığa sahiptir (için `nuget.exe install`) veya temel unzip aracını kullanarak .nupkg sıkıştırmasını açın ve ikili iç bulun.

Nuget.exe zaten varsa, ayrıca kullanabileceğiniz `nuget.exe update -self`, ancak bu aynı zamanda bir kopyasının nuget.exe sahip gerektirir. Bu yaklaşım ayrıca en son sürüme güncelleştirir. Belirli bir sürümü kullanımına izin vermez.

`tools.json` Uç noktası kullanılabilir hem önyükleme sorunu çözmek ve indirdiğiniz nuget.exe sürümünün denetiminin kendilerinde olmasına. Bu CI/CD ortamlarda veya özel komut dosyaları bulmak ve nuget.exe yayımlanan herhangi bir sürümünü indirmek için kullanılabilir.

`tools.json` Uç noktası getirilen kimliği doğrulanmamış bir HTTP isteği kullanarak (örneğin `Invoke-WebRequest` PowerShell'de veya `wget`). JSON seri durumdan çıkarıcının kullanarak ayrıştırılabilir ve HTTP isteklerini izleyen nuget.exe indirme URL'leri kullanarak da getirilebilir kimliği doğrulanmamış.

Uç nokta kullanarak getirilebilir `GET` yöntemi:

    GET https://dist.nuget.org/tools.json

[JSON şeması](http://json-schema.org/) için uç nokta şuradan ulaşabilirsiniz:

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>Yanıt

Tüm kullanılabilir sürümlerini nuget.exe içeren bir JSON belgesi yanıttır.

Kök JSON nesnesinin aşağıdaki özellik vardır:

Ad      | Tür             | Gerekli
--------- | ---------------- | --------
nuget.exe | Nesne dizisi | Evet

Her bir nesnenin `nuget.exe` dizi aşağıdaki özelliklere sahiptir:

Ad     | Tür   | Gerekli | Notlar
-------- | ------ | -------- | -----
sürüm  | dize | Evet      | Bir SemVer 2.0.0 dize
URL      | dize | Evet      | Nuget.exe bu sürümü karşıdan yüklemek için bir mutlak URL
Aşama    | dize | Evet      | Bir sabit dize
Karşıya yüklendi | dize | Evet      | Ne zaman sürümü kullanıma sunuldu, yaklaşık bir zaman damgası

Dizideki öğe azalan sırada, SemVer 2.0.0 sırada sıralanacaktır. Bu garanti yükünü en yeni sürümüne bakan bir istemci için tasarlanmıştır. 

`stage` Özelliği nasıl vettect aracının bu sürümü olduğunu gösterir. 

Aşama              | Açıklama
------------------ | ------
EarlyAccessPreview | Henüz üzerinde görünür [indirme web sayfasına](https://www.nuget.org/downloads) ve iş ortakları tarafından doğrulanması gerekir
Yayımlanan           | İndirme sitesinde kullanılabilir ancak değil ancak geniş yayılım tüketimi için önerilen
ReleasedAndBlessed | İndirme sitesinde kullanılabilir ve tüketimi için önerilir

Önerilen sürüm en son sahip olmak için bir basit yaklaşım ise ilk sürümü olan listesinde yapılacak `stage` değerini `ReleasedAndBlessed`.

`NuGet.CommandLine` Nuget.org üzerinde paket genellikle yalnızca güncelleştirilen ile `ReleasedAndBlessed` sürümleri.

### <a name="sample-request"></a>Örnek istek

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [tools-json.json](./_data/tools-json.json)]
