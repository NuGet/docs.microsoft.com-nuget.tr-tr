---
title: nuget.exe sürümlerini bulmak için tools.json
description: Uç nokta için
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852539"
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
nuget.exe | Nesne dizisi | evet

Her bir nesnenin `nuget.exe` dizi aşağıdaki özelliklere sahiptir:

Ad     | Tür   | Gerekli | Notlar
-------- | ------ | -------- | -----
sürüm  | dize | evet      | Bir SemVer 2.0.0 dize
url      | dize | evet      | Nuget.exe bu sürümü karşıdan yüklemek için bir mutlak URL
Aşama    | dize | evet      | Bir sabit dize
Karşıya yüklendi | dize | evet      | Ne zaman sürümü kullanıma sunuldu, yaklaşık bir ISO 8601 zaman

Dizideki öğe azalan sırada, SemVer 2.0.0 sırada sıralanacaktır. Bu garanti en yüksek sürüm numarasını ilgileniyor bir istemci yükünü azaltmak için tasarlanmıştır. Ancak bu liste kronolojik sırada sıralanır değil anlamına gelmez. Örneğin, daha düşük bir sürümle daha yüksek bir ana sürüm belirtilenden sonraki bir tarihte bakım yapılır, bu hizmet verilen sürüm listenin en üstünde görünmez. Tarafından yayımlanan en son sürümü istiyorsanız *zaman damgası*, yalnızca dizi tarafından sıralama `uploaded` dize. Bunun çalışmasının nedeni `uploaded` zaman damgası olan [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) lexicographical sıralama (yani basit dize sıralama) kullanarak tarih sırasına göre sıralanabilir biçimi.

`stage` Özelliği nasıl denetlenen Aracı'nın bu sürümü olduğunu gösterir. 

Aşama              | Açıklama
------------------ | ------
EarlyAccessPreview | Henüz üzerinde görünür [indirme web sayfasına](https://www.nuget.org/downloads) ve iş ortakları tarafından doğrulanması gerekir
Yayımlanan           | İndirme sitesinde kullanılabilir ancak değil ancak geniş yayılım tüketimi için önerilen
ReleasedAndBlessed | İndirme sitesinde kullanılabilir ve tüketimi için önerilir

Önerilen sürüm en son sahip olmak için bir basit yaklaşım ise ilk sürümü olan listesinde yapılacak `stage` değerini `ReleasedAndBlessed`. Sürümler SemVer 2.0.0 düzende sıralanır için bu çalışır.

`NuGet.CommandLine` Nuget.org üzerinde paket genellikle yalnızca güncelleştirilen ile `ReleasedAndBlessed` sürümleri.

### <a name="sample-request"></a>Örnek istek

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>Örnek yanıt

[!code-JSON [tools-json.json](./_data/tools-json.json)]
