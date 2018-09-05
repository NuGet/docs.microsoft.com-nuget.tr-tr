---
title: NuGet Packages.config dosyasının dosya başvurusu
description: Bazı proje türlerinde packages.config projede kullanılan NuGet paketleri listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 18566671b611899b28fcc8542cf53935f5ee2dfd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551776"
---
# <a name="packagesconfig-reference"></a>Packages.config başvurusu

`packages.config` Dosyası, proje tarafından başvurulan paketlerin listesini korumak için bazı proje türlerinde kullanılır. Bu proje bağımlılıklarınızı kolayca geri yüklemek NuGet sağlar, bu paketleri olmadan bir yapı sunucusu gibi farklı bir makineye taşınmasını proje.

Kullandıysanız, `packages.config` genellikle bir proje kök dizininde bulunur. İlk NuGet işlemi çalıştırılır, ancak ayrıca el ile herhangi bir komut çalıştırmadan önce aşağıdaki gibi oluşturulabilir otomatik olarak oluşturulur `nuget restore`.

Projeleri [PackageReference](../consume-packages/Package-References-in-Project-Files.md) kullanmayın `packages.config`.

## <a name="schema"></a>Şema

Şema basittir: olan tek bir standart XML üst bilgi aşağıdaki `<packages>` birini veya daha fazlasını içeren düğüm `<package>` öğeleri, her başvuru. Her `<package>` öğesi aşağıdaki özniteliklere sahip olabilir:

| Öznitelik | Gerekli | Açıklama |
| --- | --- | --- |
| kimlik | Evet | Newtonsoft.json veya Microsoft.AspNet.Mvc gibi paket tanımlayıcısı. | 
| sürüm | Evet | 3.1.1 veya 4.2.5.11-beta gibi yüklemek için paketi tam sürümü. Bir sürüm dizesi en az üç sayı olması gerekir; Dördüncü, yayın öncesi son olarak, isteğe bağlı. Aralıkları izin verilmez. | 
| targetFramework | Hayır | [Hedef çerçeve adı (TFM)](target-frameworks.md) paketi yüklerken uygulanacak. Bir paketi yüklendiğinde bu projenin hedef başlangıçta ayarlanır. Sonuç olarak, farklı `<package>` öğeleri farklı Tfm'ler sahip olabilir. Örneğin, .NET 4.5.2'nin hedefleyen bir proje oluşturursanız, yüklü paketleri bu noktada net452 TFM kullanın. Varsa, daha sonra .NET 4.6 için projeyi yeniden hedefle ve daha fazla paket ekleme olanlar TFM net46 birini kullanır. Projenin hedef arasında bir uyuşmazlık ve `targetFramework` öznitelikleri uyarılar üretir, bu durumda, etkilenen paketleri yeniden yükleyebilirsiniz. | 
| allowedVersions | Hayır | Bir paketi güncelleştirmesi sırasında uygulanan bu paket için izin verilen sürüm aralığı (bkz [Constraining yükseltme sürümlerinin](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Mevcut *değil* hangi paket yükleme sırasında yüklü etkileyebilir veya geri yükleme işlemi. Bkz: [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards) söz dizimi. PackageManager UI ayrıca izin verilen aralığın dışında tüm sürümler devre dışı bırakır. | 
| DevelopmentDependency | Hayır | Proje kendisini kullanan, bu ayar bir NuGet paketi oluşturur `true` için bir bağımlılık, paket kaybı paketi oluşturulduğunda eklenmesini engeller. Varsayılan, `false` değeridir. | 

## <a name="examples"></a>Örnekler

Aşağıdaki `packages.config` için iki bağımlılıkları gösterir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Aşağıdaki `packages.config` dokuz paketlere başvuruyor ancak `Microsoft.Net.Compilers` nedeniyle alıcı paket oluştururken dahil edilmez `developmentDependency` özniteliği. Newtonsoft.Json başvuru, aynı zamanda yalnızca 8.x ve 9.x sürümlere güncelleştirmeler kısıtlar.

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
