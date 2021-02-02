---
title: NuGet packages.config dosya başvurusu
description: Bazı proje türlerinde, packages.config projede kullanılan NuGet paketlerinin listesini tutar.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: da682197d4a156f9dff8ce169aab449a5392ef41
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99260309"
---
# <a name="packagesconfig-reference"></a>packages.config başvurusu

`packages.config`Dosya, proje tarafından başvurulan paketlerin listesini sürdürmek için bazı proje türlerinde kullanılır. Bu, projenin, bir yapı sunucusu gibi farklı bir makineye (bu paketlerin hepsi olmadan) aktarılması durumunda projenin bağımlılıklarını kolayca geri yüklemesine olanak tanır.

Kullanılıyorsa, `packages.config` genellikle proje kökünde bulunur. İlk NuGet işlemi çalıştırıldığında otomatik olarak oluşturulur, ancak gibi herhangi bir komut çalıştırılmadan önce el ile de oluşturulabilirler `nuget restore` .

[Packagereference](../consume-packages/Package-References-in-Project-Files.md) kullanan projeler kullanmaz `packages.config` .

## <a name="schema"></a>Şema

Şema basittir: standart XML üst bilgisinin ardından `<packages>` her başvuru için bir veya daha fazla öğe içeren tek bir düğümdür `<package>` . Her `<package>` öğe aşağıdaki özniteliklere sahip olabilir:

| Öznitelik | Gerekli | Açıklama |
| --- | --- | --- |
| kimlik | Yes | Paketin tanımlayıcısı, örneğin Newtonsoft.json veya Microsoft. AspNet. Mvc. | 
| sürüm | Yes | Yüklenecek paketin tam sürümü (örneğin, 3.1.1 veya 4.2.5.11-Beta). Sürüm dizesinin en az üç numarası olmalıdır; Dördüncü, ön sürüm ön eki olduğu gibi isteğe bağlıdır. Aralıklara izin verilmez. | 
| targetFramework | Hayır | Paket yüklenirken uygulanacak [hedef çerçeve bilinen adı (tfd)](target-frameworks.md) . Bu, başlangıçta bir paket yüklendiğinde projenin hedefine ayarlanır. Sonuç olarak, farklı `<package>` öğelerin farklı TFMs 'leri olabilir. Örneğin, .NET 4.5.2 'i hedefleyen bir proje oluşturursanız, bu noktada yüklenen paketler, net452 ' nin TFı 'sini kullanır. Projeyi daha sonra .NET 4,6 ' e yeniden hedeflemeniz ve daha fazla paket eklerseniz, bunlar net46 tfd kullanır. Projenin hedefi ve öznitelikleri arasında bir uyumsuzluk `targetFramework` uyarı oluşturur ve bu durumda etkilenen paketleri yeniden yükleyebilirsiniz. | 
| allowedVersions | Hayır | Bu paket için, paket güncelleştirmesi sırasında uygulanan bir izin verilen sürüm aralığı (bkz. [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Yükleme veya geri yükleme işlemi sırasında hangi paketin *yükleneceğini etkilemez.* Sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges) bölümüne bakın. PackageManager UI, izin verilen Aralık dışındaki tüm sürümleri de devre dışı bırakır. | 
| developmentDependency | Hayır | Kullanan projenin kendisi bir NuGet paketi oluşturursa, bunu bir bağımlılık için olarak ayarlamak, bu `true` paketin, tüketen paket oluşturulduğunda eklenmesini engeller. Varsayılan değer: `false`. | 

## <a name="examples"></a>Örnekler

Aşağıdaki `packages.config` iki bağımlılığı ifade eder:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Aşağıdakiler `packages.config` dokuz pakete başvurur, ancak `Microsoft.Net.Compilers` öznitelik nedeniyle tüketen paket oluşturulurken dahil edilmez `developmentDependency` . Ayrıca Newtonsoft.Jsbaşvurusu, güncelleştirmeleri yalnızca 8. x ve 9. x sürümleri ile sınırlar.

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
