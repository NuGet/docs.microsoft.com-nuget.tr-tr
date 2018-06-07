---
title: NuGet packages.config dosyası başvurusu
description: Bazı proje türleri packages.config projesinde kullanılan NuGet paketleri listesini tutar.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2019ce5961a8237fbda855cd7d5b42948808be3a
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817843"
---
# <a name="packagesconfig-reference"></a>Packages.config başvurusu

`packages.config` Dosyası, projenin başvurduğu paketlerin listesini korumak için bazı proje türleri kullanılır. Bu projenin bağımlılıkları kolayca geri yüklemek NuGet sağlar, bu tüm paketler olmadan yapı sunucu gibi başka bir makine aktarılmasını projesi.

Kullandıysanız, `packages.config` genellikle bir proje kök dizininde bulunur. İlk NuGet işlemi çalıştırılır, ancak aynı zamanda el ile gibi herhangi bir komut çalıştırmadan önce oluşturulabilir otomatik olarak oluşturulur `nuget restore`.

Projeleri kullanan [PackageReference](../consume-packages/Package-References-in-Project-Files.md) kullanmayın `packages.config`.

## <a name="schema"></a>Şema

Şema basittir: olan tek bir standart XML üst bilgisini aşağıdaki `<packages>` bir veya daha fazla içeren düğümü `<package>` öğeleri, her başvurusu için bir. Her `<package>` öğesi aşağıdaki özniteliklere sahiptir:

| Öznitelik | Gerekli | Açıklama |
| --- | --- | --- |
| kimlik | Evet | Newtonsoft.json veya Microsoft.AspNet.Mvc gibi paket tanımlayıcısı. | 
| sürüm | Evet | 3.1.1 veya 4.2.5.11-beta gibi yüklemek için paket tam sürümü. Bir sürüm dizesi en az üç sayı olması gerekir; bir yayın öncesi soneki olarak dördüncü isteğe bağlıdır. Aralıkları izin verilmiyor. | 
| targetFramework | Hayır | [Framework bilinen ad (TFM) hedef](target-frameworks.md) paket yüklerken uygulanacak. Bir paketi yüklendiğinde bu projenin hedef başlangıçta ayarlanır. Sonuç olarak, farklı `<package>` öğeleri farklı TFMs sahip olabilir. Örneğin, .NET 4.5.2 hedefleyen bir proje oluşturduğunuzda, yüklü olan paketleri o noktada net452 TFM kullanın. Varsa, daha sonra .NET 4.6 projeyi yeniden hedefleyin ve daha fazla paket ekleme olanlar net46 TFM kullanır. Projenin hedef arasında bir uyuşmazlık ve `targetFramework` öznitelikleri uyarılar üretir, bu durumda etkilenen paketler yeniden yükleyebilirsiniz. | 
| allowedVersions | Hayır | Paket güncelleştirme sırasında uygulanan bu paket için izin verilen sürüm aralığı (bkz [Constraining yükseltme sürümleri](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Mevcut *değil* hangi paket yükleme sırasında yüklü etkilemez ya da geri yükleme işlemi. Bkz: [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards) sözdizimi için. PackageManager UI izin verilen aralığın dışında tüm sürümleri de devre dışı bırakır. | 
| DevelopmentDependency | Hayır | Proje kendisini kullanma, bu ayar bir NuGet paketi oluşturur `true` için bir bağımlılık paket kaybı paketi oluşturulduğunda eklenmesini engeller. Varsayılan, `false` değeridir. | 

## <a name="examples"></a>Örnekler

Aşağıdaki `packages.config` iki bağımlılıkları başvuruyor:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Aşağıdaki `packages.config` dokuz paketlerine başvuruyor ancak `Microsoft.Net.Compilers` nedeniyle tüketim paket oluştururken dahil edilmez `developmentDependency` özniteliği. Newtonsoft.Json referansı güncelleştirmeleri yalnızca 8.x ve 9.x sürümleri için de kısıtlar.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
