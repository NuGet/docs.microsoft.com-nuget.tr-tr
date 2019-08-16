---
title: NuGet Packages. config dosyası başvurusu
description: Bazı proje türlerinde, Packages. config projede kullanılan NuGet paketlerinin listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 2fd1640295ca35304358565808a89d752cfd8abf
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488639"
---
# <a name="packagesconfig-reference"></a>Packages. config başvurusu

`packages.config` Dosya, proje tarafından başvurulan paketlerin listesini sürdürmek için bazı proje türlerinde kullanılır. Bu, NuGet 'in projenin bağımlılıklarını kolayca geri yüklemesine olanak tanır, çünkü proje bir yapı sunucusu gibi farklı bir makineye taşınır.

Kullanılıyorsa, `packages.config` genellikle proje kökünde bulunur. İlk NuGet işlemi çalıştırıldığında otomatik olarak oluşturulur, ancak gibi herhangi bir komut `nuget restore`çalıştırılmadan önce el ile de oluşturulabilirler.

[Packagereference](../consume-packages/Package-References-in-Project-Files.md) kullanan projeler kullanmaz `packages.config`.

## <a name="schema"></a>Şema

Şema basittir: standart XML üst bilgisinin ardından her başvuru için bir veya `<packages>` daha fazla `<package>` öğe içeren tek bir düğümdür. Her `<package>` öğe aşağıdaki özniteliklere sahip olabilir:

| Öznitelik | Gerekli | Açıklama |
| --- | --- | --- |
| kimlik | Evet | , Newtonsoft. JSON veya Microsoft. AspNet. Mvc gibi paketin tanımlayıcısı. | 
| sürüm | Evet | Yüklenecek paketin tam sürümü (örneğin, 3.1.1 veya 4.2.5.11-Beta). Sürüm dizesinin en az üç numarası olmalıdır; Dördüncü, ön sürüm ön eki olduğu gibi isteğe bağlıdır. Aralıklara izin verilmez. | 
| targetFramework | Hayır | Paket yüklenirken uygulanacak [hedef çerçeve bilinen adı (tfd)](target-frameworks.md) . Bu, başlangıçta bir paket yüklendiğinde projenin hedefine ayarlanır. Sonuç olarak, farklı `<package>` öğelerin farklı tfms 'leri olabilir. Örneğin, .NET 4.5.2 'i hedefleyen bir proje oluşturursanız, bu noktada yüklenen paketler, net452 ' nin TFı 'sini kullanır. Projeyi daha sonra .NET 4,6 ' e yeniden hedeflemeniz ve daha fazla paket eklerseniz, bunlar net46 tfd kullanır. Projenin hedefi ve `targetFramework` öznitelikleri arasında bir uyumsuzluk uyarı oluşturur ve bu durumda etkilenen paketleri yeniden yükleyebilirsiniz. | 
| allowedVersions | Hayır | Bu paket için, paket güncelleştirmesi sırasında uygulanan bir izin verilen sürüm aralığı (bkz. [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Yükleme veya geri yükleme işlemi sırasında hangi paketin yükleneceğini etkilemez. Sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges-and-wildcards) bölümüne bakın. PackageManager UI, izin verilen Aralık dışındaki tüm sürümleri de devre dışı bırakır. | 
| developmentDependency | Hayır | Kullanan projenin kendisi bir NuGet paketi oluşturursa, bunu bir bağımlılık için olarak `true` ayarlamak, bu paketin, tüketen paket oluşturulduğunda eklenmesini engeller. Varsayılan, `false` değeridir. | 

## <a name="examples"></a>Örnekler

Aşağıdaki `packages.config` iki bağımlılığı ifade eder:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Aşağıdakiler `packages.config` dokuz pakete başvurur, ancak `Microsoft.Net.Compilers` `developmentDependency` öznitelik nedeniyle tüketen paket oluşturulurken dahil edilmez. Newtonsoft. JSON başvurusu, güncelleştirmeleri yalnızca 8. x ve 9. x sürümleriyle sınırlandırır.

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
