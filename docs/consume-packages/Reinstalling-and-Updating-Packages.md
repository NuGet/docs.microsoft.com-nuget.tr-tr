---
title: Yeniden yüklemeyi ve NuGet paketlerini güncelleştirme
description: Visual Studio'da bozuk paket referanslarını gibi ile yeniden yükleyin ve paketleri, güncelleştirmek için gerekli olduğu zaman ayrıntılar.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: fc2c1a58f787da61041c644085058355de4f12ea
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-reinstall-and-update-packages"></a>Yeniden yükleme ve güncelleştirme paketleri

Altında aşağıda açıklandığı gibi durumlarda bir dizi vardır [ne zaman bir paket yeniden](#when-to-reinstall-a-package), burada bir pakete başvuruları Visual Studio projesi içinde bozuk alabilirsiniz. Bu durumlarda, paketin aynı sürümü kaldırılıp bu başvuruları çalışma sırayı geri yükler. Paket güncelleştirme yalnızca bir paketi çalışma siparişe genellikle geri yükler güncelleştirilmiş bir sürümünü yükleme anlamına gelir.

Güncelleştirme ve paketleri yeniden şu şekilde gerçekleştirilir:

| Yöntem | Güncelleştirme | Yeniden yükleme |
| --- | --- | --- |
| Paket Yöneticisi Konsolu (açıklanan [kullanarak güncelleştirme paketi](#using-update-package)) | `Update-Package` komutu | `Update-Package -reinstall` komutu |
| Paket Yöneticisi kullanıcı Arabirimi | Üzerinde **güncelleştirmeleri** sekmesinde bir veya daha fazla paket seçin ve Seç **güncelleştirme** | Üzerinde **yüklü** sekmesinde, bir paket seçin, adıyla kaydedin ve ardından **kaldırma**. Geçiş **Gözat** sekmesinde, arama için paket adı, onu seçin ve sonra seçin **yükleme**). |
| nuget.exe CLI | `nuget update` komutu | Tüm paketler için paket klasörü silin ve ardından çalıştırın `nuget install`. Tek bir paket için paket klasörünü silin ve kullanmak `nuget install <id>` aynı yeniden yüklemek için. |

Bu makalede:

- [Bir paketi yeniden zamanı](#when-to-reinstall-a-package)
- [Kısıtlayan yükseltme sürümleri](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Bir paketi yeniden zamanı

1. **Paket geri yüklendikten sonra başvuruları bozuk**: Proje açılır ve NuGet paketleri, ancak hala bozuk bakın başvuruları geri, her bu paketlerin yeniden yüklemeyi deneyin.
1. **Proje nedeniyle silinen dosyaların bozulur**: NuGet engellemez, projenizin bölün ve yanlışlıkla bir paketten yüklü içeriği değiştirmek kolaydır, paketleri eklenen öğeler kaldırılıyor. Proje geri yüklemek için etkilenen paketler yeniden yükleyin.
1. **Paket güncelleştirme ihlal proje**: bir paket için bir güncelleştirme proje bozarsa, hata da güncelleştirilmiş bağımlılık paketi tarafından genellikle neden olur. Bağımlılık durumunu geri yüklemek için özel pakette yeniden yükleyin.
1. **Proje yeniden hedefleme veya yükseltme**: Bu proje güncellendiyse yükseltilmiş veya kaldırılmış ve paketi hedef framework değişikliği nedeniyle yeniden gerektiriyorsa yararlı olabilir. Sonraki derleme uyarıları paketin yeniden yüklenmesi gerekebilir size bildirmek ve bu gibi durumlarda bir derleme hatası projeyi yeniden hedefleme hemen sonra NuGet gösterir. Proje yükseltme için NuGet proje yükseltme günlüğüne bir hata gösterir.
1. **Geliştirme sırasında bir paket yeniden**: paketi yazarları çoğunlukla gerekir geliştirme paket aynı sürümünü yeniden yüklemek davranış test etmek için. `Install-Package` Komutunu kullanın, bir yeniden yükleme zorlamak için bir seçenek sağlamaz `Update-Package -reinstall` yerine.

## <a name="constraining-upgrade-versions"></a>Kısıtlayan yükseltme sürümleri

Varsayılan olarak yeniden yüklemek veya bir paketin güncelleştirilmesi, *her zaman* paket kaynağından en son sürümünü yükler.

Kullanarak projelerinde `packages.config` yönetim biçimi, ancak özellikle sürüm aralığı kısıtlayabilirsiniz. Uygulamanızı çalıştığını biliyorsanız, örneğin, yalnızca sürümüyle 1.x bir paketin ancak değil 2.0 ve üzeri sürümlerde, belki de API paketindeki önemli bir değişiklik nedeniyle, ardından 1.x sürümlerine yükseltme sınırlamak istersiniz. Bu, uygulamanızın çalışmamasına neden yanlışlıkla güncelleştirmelerini engeller.

Bir kısıtlama belirlemek için açık `packages.config` bir metin düzenleyicisinde söz konusu bağımlılık bulmak ve eklemek `allowedVersions` sürüm aralığı özniteliğiyle. Örneğin, güncelleştirmeleri sınırlamak için 1.x, sürüme Ayarla `allowedVersions` için `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Güncelleştirme paketini kullanma

Dikkatli olmak [konuları](#considerations) aşağıda açıklandığı gibi kolayca kullanarak herhangi bir paket yeniden [güncelleştirme paketi komut](../Tools/ps-ref-update-package.md) Visual Studio Paket Yöneticisi konsolunda (**Araçları**  >  **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**):

```ps
Update-Package -Id <package_name> –reinstall
```

Bu komutu kullanarak bir paket kaldırarak ve aynı sürümle NuGet galerisinde aynı paketin bulmaya çalışırken daha kolaydır. Unutmayın `-Id` anahtarı isteğe bağlı değil.

Aynı komut olmadan `-reinstall` bir paket varsa daha yeni bir sürüme güncelleştirir. Söz konusu paketi projede zaten yüklü değilse, komutu bir hata verir; diğer bir deyişle, `Update-Package` paketleri doğrudan yüklemez.

```ps
Update-Package <package_name>
```

Varsayılan olarak, `Update-Package` bir çözümdeki tüm projeleri etkiler. Belirli bir proje eyleme sınırlandırmak için kullanmak `-ProjectName` anahtarını, Çözüm Gezgini'nde göründüğü gibi projesinin adı kullanma:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

İçin *güncelleştirme* projesindeki tüm paketleri (veya kullanarak yeniden `-reinstall`), kullanın `-ProjectName` herhangi belirli bir paket belirtmeden:

```ps
Update-Package -ProjectName MyProject
```

Bir çözümde tüm paketler güncelleştirmek için yalnızca kullanın `Update-Package` başka bir bağımsız değişken veya anahtarları kendisiyle tarafından. Tüm güncelleştirmeleri gerçekleştirmek için uzun bir süre sürebileceğinden dikkatli bir şekilde, bu formu kullanın:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Bir proje veya çözümünü kullanarak paketleri güncelleştiriliyor [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) her zaman (ön sürüm paketlerini hariç) paketin en son sürüme güncelleştirir. Projeleri kullanan `packages.config` isterseniz, güncelleştirme sürümleri aşağıda açıklandığı gibi sınırlandırabilir [Constraining yükseltme sürümleri](#constraining-upgrade-versions).

Komutu hakkında ayrıntılar için bkz: [güncelleştirme paketini](../Tools/ps-ref-update-package.md) başvuru.

### <a name="considerations"></a>Dikkat Edilecekler

Aşağıda bir paket yeniden yükleme yaparken etkilenebilir:

1. **Proje hedef çerçevesi yeniden hedefleme göre paketler yeniden yükleme**
    - Bir paketi kullanarak basit bir durumda, yalnızca yeniden yüklemeyi `Update-Package –reinstall <package_name>` çalışır. Eski bir hedef framework karşı yüklenmiş bir paketin kaldırıldığını ve aynı paketin proje geçerli hedef Framework'teki karşı yüklü.
    - Bazı durumlarda, yeni hedef Framework'ü desteklemiyor bir paket olabilir.
        - Taşınabilir sınıf kitaplıkları (PCLs) bir paket destekler ve proje artık paketi tarafından desteklenen platformlar birleşimi için güncellendiyse, paket başvurular yeniden yükledikten sonra eksilir.
        - Bu bağımlılıklar olarak yüklü olan paketleri veya doğrudan kullanmakta olduğunuz paketleri için yüzey. Bu, bağımlılık çalışmazken yeni hedef Framework'ü doğrudan desteklemek için kullanıyorsanız paket için mümkündür.
        - Uygulamanızı yeniden hedefleme, yapı veya çalışma zamanı hataları sonuçları sonra paketler yeniden yüklemeyi, hedef Framework'ü veya düzgün şekilde, yeni hedef Framework'ü destekleyen alternatif paketleri Ara geri dönmek gerekebilir.

1. **Packages.config içinde proje yeniden hedefleme veya yükseltmeden sonra eklenen requireReinstallation özniteliği**
    - NuGet paketleri yeniden hedefleme veya bir proje yükseltme etkilendi olmadığını algılar, ekler bir `requireReinstallation="true"` özniteliğini `packages.config` paket referanslarını etkilenen tüm için. Bunları yeniden unutmayın şekilde bu nedenle, Visual Studio sonraki her yapı bu paketleri için derleme uyarıları başlatır.

1. **Bağımlılıklar paketlerle yeniden yükleme**
    - `Update-Package –reinstall` özgün paketin aynı sürümünü yeniden yükler, ancak belirli bir sürüm kısıtlamaları belirtilmediği sürece bağımlılıklarını en son sürümünü yükler. Bu, yalnızca bir sorunu düzeltmek için gerekli olarak bağımlılıklar güncelleştirmenize olanak sağlar. Ancak, bu bağımlılık bir önceki sürüme geri alındığında, kullanabileceğiniz `Update-Package <dependency_name>` bağımlı paketi etkilemeden, bir bağımlılık yeniden yüklemek için.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` özgün paketin aynı sürümünü yeniden yükler ancak bağımlılıkları yeniden değil. Paket bağımlılıklarını güncelleştirme bozuk durumda neden olabilir, bu kullanın

1. **Bağımlı sürümleri dahil edildiğinde paketler yeniden yükleme**
    - Yukarıda açıklandığı şekilde, bir paket yeniden bağımlı herhangi bir yüklü paketleri sürümlerini değiştirmez. Mümkündür sonra bir bağımlılık yeniden yüklemeyi bağımlı paketi bozar.