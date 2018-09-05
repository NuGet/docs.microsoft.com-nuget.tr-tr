---
title: Yeniden yükleme ve NuGet paketlerini güncelleştirme
description: Bozuk bir paket başvuruları gibi Visual Studio ile yeniden yükleyin ve güncelleştirme paketleri, gerekli olduğunda ilgili ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: c58cf38bab45793bef820e2c52914a91d745ec77
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551789"
---
# <a name="how-to-reinstall-and-update-packages"></a>Yeniden yükleme ve güncelleştirme paketleri

Birçok durumda, altında aşağıda açıklanan [bir paketi yeniden yüklemek ne zaman](#when-to-reinstall-a-package), burada bir paket başvuruları içinde bir Visual Studio Proje bozuk alabilirsiniz. Bu durumlarda, aynı paket sürümünü kaldırıp yeniden yüklemeyi bu başvuruları çalışma düzenine geri yükler. Paket güncelleştirme yalnızca genellikle bir paket çalışma düzenine geri yükler güncelleştirilmiş bir sürümünü yükleme anlamına gelir.

Paketleri yeniden yükleme ve güncelleştirme gibi gerçekleştirilir:

| Yöntem | Güncelleştirme | Yeniden yükleyin |
| --- | --- | --- |
| Paket Yöneticisi Konsolu (açıklanan [Update-Package kullanarak](#using-update-package)) | `Update-Package` Komutu | `Update-Package -reinstall` Komutu |
| Paket Yöneticisi UI | Üzerinde **güncelleştirmeleri** sekmesinde bir veya daha fazla paket seçin ve seçin **güncelleştirme** | Üzerinde **yüklü** sekmesinde, bir paket seçin, kayıt adının ve sonra seçin **kaldırma**. Geçiş **Gözat** sekmesinde, paket adı için arama yapın, seçin ve ardından seçin **yükleme**). |
| nuget.exe CLI | `nuget update` Komutu | Tüm paketler için paket klasörü silin ve ardından çalıştırın `nuget install`. Tek bir paket için paket klasörü silin ve kullanmak `nuget install <id>` aynı yeniden yüklemek için. |

Bu makalede:

- [Ne zaman bir paketi yeniden yüklemek için](#when-to-reinstall-a-package)
- [Kısıtlama yükseltme sürümleri](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Ne zaman bir paketi yeniden yüklemek için

1. **Paket geri yüklemeden sonra başvuruları bozuk**: bir proje ve NuGet paketleri, ancak yine de bozuk bakın başvuruları geri, her biri bu paketleri yeniden yüklemeyi deneyin.
1. **Project silinen dosyalar nedeniyle bozulur**: NuGet engellemez, yanlışlıkla bir paketinden yüklenen içeriği değiştirmek projenizin kırmayı denerken kolaydır paketlerden, eklenen öğeleri kaldırmasını. Proje geri yüklemek için etkilenen paketleri yeniden yükleyin.
1. **Paket güncelleştirmesi, proje kesildi**: başarısız bir güncelleştirme paketi için bir proje keserse, genellikle da güncelleştirilmiş olabilir bir bağımlılık paketini tarafından kaynaklanır. Bağımlılık durumunu geri yüklemek için belirli bir paketin yeniden yükleyin.
1. **Proje yeniden hedefleme veya yükseltme**: Bu bir proje yeniden hedeflendi ya da yükseltilmiş ve paketin hedef framework değişikliği nedeniyle yeniden gerektiriyorsa yararlı olabilir. Sonraki derleme uyarıları paketin yeniden yüklenmesi gerekebilir size bildirmek ve NuGet, proje yeniden hedefleme hemen sonra bu gibi durumlarda, bir yapı hatası gösterir. Proje yükseltme için NuGet proje yükseltme günlüğüne bir hata gösterir.
1. **Geliştirme sırasında bir paket yeniden**: Paket yazarlarının genellikle gerekir geliştirmekte paket aynı sürümünü yeniden yüklemek davranış test etmek için. `Install-Package` Komutu, bir yeniden yükleme zorlamak, bu nedenle kullanın seçeneği sağlamaz `Update-Package -reinstall` yerine.

## <a name="constraining-upgrade-versions"></a>Kısıtlama yükseltme sürümleri

Varsayılan olarak yeniden yüklemek veya bir paket güncelleştirmek *her zaman* paket kaynağından en son sürümünü yükler.

Kullanarak projelerinde `packages.config` yönetim biçimi, ancak özellikle sürüm aralığı kısıtlayabilirsiniz. Uygulamanızın çalıştığını biliyorsanız, örneğin, yalnızca sürümüyle 1.x paketi ancak değil 2.0 ve üzeri sürümlerde, belki de API paketindeki büyük bir değişiklik nedeniyle, ardından 1.x sürümüne yükseltmeleri sınırlamak istersiniz. Bu uygulama kesmek yanlışlıkla güncelleştirmelerini engeller.

Bir kısıtlama belirlemek için açık `packages.config` bir metin düzenleyicisinde söz konusu bağımlılık bulun ve ekleme `allowedVersions` özniteliği ile bir sürüm aralığı. Örneğin, güncelleştirmeleri sınırlamak için 1.x sürümüne ayarlı `allowedVersions` için `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Her durumda, açıklanan gösterimi kullanan [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Güncelleştirme paketini kullanma

Oluşturduğunu, olan [konuları](#considerations) aşağıda açıklandığı gibi kolayca kullanarak herhangi bir paket yeniden [Update-Package komut](../Tools/ps-ref-update-package.md) Visual Studio Paket Yöneticisi konsolunda (**araçları**  >  **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**):

```ps
Update-Package -Id <package_name> –reinstall
```

Bu komutu kullanarak bir paket kaldırarak ve ardından NuGet galerisindeki aynı sürümle aynı paket bulmaya çalışan daha kolaydır. Unutmayın `-Id` anahtar isteğe bağlıdır.

Aynı komut olmadan `-reinstall` varsa, yeni bir sürüme bir paketi güncelleştirir. Komutu, söz konusu paketin bir projede zaten yüklü değilse hata verir; diğer bir deyişle, `Update-Package` paketleri doğrudan yüklemez.

```ps
Update-Package <package_name>
```

Varsayılan olarak, `Update-Package` bir çözümdeki tüm projeleri etkiler. Belirli bir projeye eylem sınırlamak için kullanın `-ProjectName` geçiş, Çözüm Gezgini'nde göründüğü gibi proje adını kullanarak:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

İçin *güncelleştirme* bir projedeki tüm paketler (ya da kullanarak yeniden `-reinstall`), kullanın `-ProjectName` herhangi belirli bir paket belirtmeden:

```ps
Update-Package -ProjectName MyProject
```

Bir çözümdeki tüm paketleri güncelleştir için yalnızca kullanın `Update-Package` diğer bağımsız değişkenler veya anahtarlarının seçemez. Tüm güncelleştirmeleri gerçekleştirmek için büyük miktarda zaman zaman alabildiğinden bu formu dikkatlice kullanın:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Bir proje veya çözümü kullanarak paketler güncelleştiriliyor [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) her zaman en son sürüme (yayın öncesi paketleri hariç) paketi güncelleştirir. Projeleri `packages.config` isterseniz, güncelleştirme sürümleri aşağıda açıklanan şekilde sınırlandırabilir [Constraining yükseltme sürümlerinin](#constraining-upgrade-versions).

Komutunda tüm ayrıntılar için bkz. [Update-Package](../Tools/ps-ref-update-package.md) başvuru.

### <a name="considerations"></a>Dikkat Edilecekler

Aşağıdaki bir paket yeniden yükleme sırasında etkilenebilir:

1. **Proje hedef framework yeniden hedefleme göre paketleri yeniden yükleme**
    - Basit bir durumda, yalnızca bir paketini kullanarak yeniden `Update-Package –reinstall <package_name>` çalışır. Karşı eski bir hedef çerçeve yüklü olan bir paket kaldırılır ve aynı paketin geçerli projenin hedef çatısını karşı yüklü.
    - Bazı durumlarda, bir paketi yeni hedef Framework'ü desteklemiyor olabilir.
        - Taşınabilir sınıf kitaplıkları (PCLs) bir paket destekliyorsa ve projeyi yeniden hedeflendi bir birleşimi artık paket tarafından desteklenen platformlar için paket başvuruları eksik yeniden yükledikten sonra olur.
        - Bu paketler, doğrudan kullanıyorsanız veya bağımlılıkları olarak yüklü paketleri ortaya çıkabilir. Bağımlılık çalışmazken doğrudan yeni hedef Framework'ü desteklemek için kullanmakta olduğunuz paket için mümkündür.
        - Uygulamanızı yeniden hedefleme, derleme veya çalışma zamanı hataları oluşur sonra paketleri yeniden yükleme, hedef Framework'ü veya düzgün bir şekilde, yeni hedef Framework'ü destekleyen alternatif paketleri Ara geri dönmek gerekebilir.

1. **Proje yeniden hedefleme veya yükseltmeden sonra Packages.config dosyasının içinde eklenen requireReinstallation özniteliği**
    - NuGet paketleri yeniden hedefleme veya bir proje yükseltme etkilenmiştir olmadığını algılar, ekler bir `requireReinstallation="true"` özniteliğini `packages.config` etkilenen tüm için paket başvuruları. Bunları yeniden anımsamak için bu nedenle, sonraki her yapı Visual Studio bu paketleri için derleme uyarıları başlatır.

1. **Bağımlılıkları olan paketleri yeniden yükleme**
    - `Update-Package –reinstall` asıl Paket sürümüyle aynı sürümü yükler, ancak belirli bir sürüm kısıtlamaları belirtilmediği sürece, bağımlılıkları en son sürümünü yükler. Bu yalnızca bir sorunu düzeltmek için gerekli bağımlılıkları güncelleştirmenizi sağlar. Ancak, bu bir bağımlılık önceki bir sürüme geri alır, kullanabileceğiniz `Update-Package <dependency_name>` bağımlı paketi etkilemeden bu bir bağımlılık yeniden yüklemek için.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` asıl Paket sürümüyle aynı sürümü yükler ancak bağımlılıkları yeniden değil. Paket bağımlılıkları güncelleştirme bozuk durumda neden olabilir, bunu kullanın.

1. **Bağımlı sürümleri söz konusu olduğunda paketleri yeniden yükleme**
    - Yukarıda açıklandığı gibi bir paketi yeniden yüklemeyi bağımlı herhangi bir yüklü paketleri sürümlerini değiştirmez. Mümkündür ve ardından bağımlı paketi bir bağımlılık yeniden yüklemeyi uğratabilir.
