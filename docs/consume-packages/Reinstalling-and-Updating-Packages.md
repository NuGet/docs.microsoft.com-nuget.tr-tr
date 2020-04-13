---
title: NuGet Paketlerini Yeniden Yükleme ve Güncelleme
description: Visual Studio'daki bozuk paket başvurularında olduğu gibi paketleri yeniden yüklemek ve güncellemek için ne zaman gerekli olduğuna ilişkin ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 101c6d6b9d93da912f60c40b27559e80327154b8
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428704"
---
# <a name="how-to-reinstall-and-update-packages"></a>Paketleri yeniden yükleme ve güncelleştirme

Bir [Paketin Yeniden Yüklenmesi Için Ne Zaman](#when-to-reinstall-a-package)altında aşağıda açıklanan bir dizi durum vardır , bir pakete yapılan atıflar Visual Studio projesi nde bozulabilir. Bu gibi durumlarda, paketin aynı sürümünü kaldırma ve yeniden yükleme bu başvuruları çalışma düzenine geri yükler. Paketi güncelleştirmek, genellikle bir paketi çalışma düzenine geri yükleyen güncelleştirilmiş bir sürümü yüklemek anlamına gelir.

Visual Studio'da Package Manager Console, paketleri güncellemek ve yeniden yüklemek için birçok esnek seçenek sunar.

Paketleri n için güncelleştirin ve yeniden yüklemek aşağıdaki gibi gerçekleştirilir:

| Yöntem | Güncelleştir | Yeniden yükleme |
| --- | --- | --- |
| Paket Yöneticisi konsolu [(Update-Package kullanarak](#using-update-package)açıklanan) | `Update-Package` komutu | `Update-Package -reinstall` komutu |
| Paket Yöneticisi UI | **Güncelleştirmeler** sekmesinde, bir veya daha fazla paket seçin ve **Güncelleştir'i** seçin | **Yüklü** sekmede bir paket seçin, adını kaydedin ve sonra **Kaldır'ı**seçin. **Gözat** sekmesine geçin, paket adını arayın, seçin ve **sonra Yükle'yi**seçin). |
| nuget.exe CLI | `nuget update` komutu | Tüm paketler için paket klasörünü `nuget install`silin ve çalıştırın. Tek bir paket için paket klasörünü silin ve aynı paketi yeniden yüklemek için kullanın. `nuget install <id>` |

> [!NOTE]
> Dotnet CLI için eşdeğer yordam gerekli değildir. Benzer bir senaryoda, [dotnet CLI ile paketleri geri yükleyebilirsiniz.](package-restore.md#restore-using-the-dotnet-cli)

Bu makalede:

- [Paketi Ne Zaman Yeniden Yükleriz?](#when-to-reinstall-a-package)
- [Yükseltme sürümlerini zorlayarak](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Paketi Ne Zaman Yeniden Yükleriz?

1. **Paket geri yüklemesi sonrası bozuk başvurular**: Bir proje açtıysanız ve NuGet paketlerini geri yüklediyseniz, ancak yine de bozuk başvuruları görüyorsanız, bu paketlerin her birini yeniden yüklemeyi deneyin.
1. **Proje silinen dosyalar nedeniyle bozuldu**: NuGet paketlerden eklenen öğeleri kaldırmanızı engellemez, bu nedenle yanlışlıkla bir paketten yüklenen içeriği değiştirmek ve projenizi kırmak kolaydır. Projeyi geri yüklemek için etkilenen paketleri yeniden yükleyin.
1. **Paket güncelleştirmesi projeyi kırdı**: Bir pakete yapılan bir güncelleştirme projeyi bozarsa, hata genellikle güncelleştirilmiş olabilecek bir bağımlılık paketinden kaynaklanır. Bağımlılık durumunu geri yüklemek için, belirli bir paketi yeniden yükleyin.
1. **Proje yeniden hedefleme veya yükseltme**: Bir proje yeniden hedeflendiğinde veya yükseltildiğinde ve paket hedef çerçevedeki değişiklik nedeniyle yeniden yükleme gerektiriyorsa yararlı olabilir. NuGet, proje yeniden hedeflemeden hemen sonra bu gibi durumlarda bir yapı hatası gösterir ve sonraki yapı uyarıları paketin yeniden yüklenmesi gerekebileceğini bilmenizi sağlar. Proje yükseltme için NuGet, Proje Yükseltme Günlüğü'nde bir hata gösterir.
1. **Bir paketin geliştirilmesi sırasında yeniden yüklenmesi**: Paket yazarlarının genellikle davranışı sınamak için geliştirdikleri paketin aynı sürümünü yeniden yüklemeleri gerekir. Komut `Install-Package` yeniden yüklemeyi zorlamak için bir seçenek `Update-Package -reinstall` sağlamaz, bu nedenle bunun yerine kullanın.

## <a name="constraining-upgrade-versions"></a>Yükseltme sürümlerini zorlayarak

Varsayılan olarak, bir paketi yeniden yüklemek veya güncelleştirmek *her zaman* paket kaynağından mevcut en son sürümü yükler.

Ancak, `packages.config` yönetim biçimini kullanan projelerde, sürüm aralığını özellikle kısıtlayabilirsiniz. Örneğin, uygulamanızın yalnızca bir paketin 1.x sürümüyle çalıştığını, ancak 2.0 ve üzeri sürümlerle çalıştığını biliyorsanız, belki de paket API'sindeki büyük bir değişiklik nedeniyle, yükseltmeleri 1.x sürümlerine kısıtlamak isteyebilirsiniz. Bu, uygulamayı bozacak yanlışlıkla güncelleştirmeleri önler.

Kısıtlama ayarlamak için, `packages.config` metin düzenleyicisinde açın, söz konusu bağımlılığı `allowedVersions` bulun ve özniteliği sürüm aralığıyla ekleyin. Örneğin, güncelleştirmeleri sürüm 1.x'e `allowedVersions` kısıtlamak için: `[1,2)`

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Her durumda, [Paket sürümünde](../concepts/package-versioning.md#version-ranges)açıklanan gösterimi kullanın.

## <a name="using-update-package"></a>Güncelleme Paketi kullanma

Aşağıda açıklanan [hususlara](#considerations) dikkat etmek için Visual Studio Package Manager Console **(Tools** > **NuGet Package Manager** > **Package Manager Console)** ile [Ilgili Güncelleme Paketi komutunu](../reference/ps-reference/ps-ref-update-package.md) kullanarak herhangi bir paketi kolayca yeniden yükleyebilirsiniz.

```ps
Update-Package -Id <package_name> –reinstall
```

Bu komutu kullanmak, bir paketi kaldırmak ve aynı sürümü içeren NuGet galerisinde aynı paketi bulmaya çalışmaktan çok daha kolaydır. Anahtarın `-Id` isteğe bağlı olduğunu unutmayın.

Varsa, yeni `-reinstall` bir sürüme bir paket güncelleştirmeleri olmadan aynı komut. Söz konusu paket bir projede zaten yüklü değilse komut hata verir; diğer bir `Update-Package` şey, paketleri doğrudan yüklemez.

```ps
Update-Package <package_name>
```

Varsayılan olarak, `Update-Package` bir çözümdeki tüm projeleri etkiler. Eylemi belirli bir projeyle sınırlamak `-ProjectName` için, Çözüm Gezgini'nde göründüğü gibi projenin adını kullanarak anahtarı kullanın:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Projedeki tüm paketleri *güncelleştirmek* (veya `-reinstall`kullanarak `-ProjectName` yeniden yüklemek), belirli bir paket belirtmeden kullanın:

```ps
Update-Package -ProjectName MyProject
```

Bir çözümdeki tüm paketleri güncelleştirmek için, başka bağımsız değişkenler veya anahtarlar olmadan tek başına kullanmanız `Update-Package` gerekir. Tüm güncelleştirmeleri gerçekleştirmek önemli ölçüde zaman alabilir, çünkü bu formu dikkatle kullanın:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

[PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) kullanarak bir proje veya çözümdeki paketleri güncellemek her zaman paketin en son sürümüne güncellenir (yayın öncesi paketler hariç). Kullanılan `packages.config` projeler, istenirse, [Kısıtlı yükseltme sürümlerinde](#constraining-upgrade-versions)aşağıda açıklandığı gibi güncelleştirme sürümlerini sınırlayabilir.

Komutla ilgili tüm ayrıntılar için [Güncelleme-Paket](../reference/ps-reference/ps-ref-update-package.md) başvurusuna bakın.

### <a name="considerations"></a>Dikkat edilmesi gerekenler

Bir paketi yeniden yüklerken aşağıdakiler etkilenebilir:

1. **Proje hedef çerçevesi yeniden hedeflemesine göre paketleri yeniden yükleme**
    - Basit bir durumda, sadece işleri `Update-Package –reinstall <package_name>` kullanarak bir paket yeniden yükleyin. Eski bir hedef çerçeveye karşı yüklenen bir paket kaldırılır ve aynı paket projenin geçerli hedef çerçevesine karşı yüklenir.
    - Bazı durumlarda, yeni hedef çerçevesini desteklemeyen bir paket olabilir.
        - Bir paket taşınabilir sınıf kitaplıklarını (PCL'leri) destekliyorsa ve proje paket tarafından artık desteklenmeyen platformların birleşimine yeniden hedefleniyorsa, yeniden yüklendikten sonra pakete yapılan başvurular eksik olur.
        - Bu, doğrudan kullandığınız paketler veya bağımlılık olarak yüklenmiş paketler için su yüzüne çıkabilir. Kullandığınız paketin, bağımlılığı olmasa da yeni hedef çerçeveyi desteklemek için doğrudan kullanılması mümkündür.
        - Uygulama sonuçlarınızı yapı veya çalışma zamanı hatalarıyla yeniden hedefledikten sonra paketleri yeniden yüklemeniz, hedef çerçevenizi geri almanız veya yeni hedef çerçevenizi düzgün bir şekilde destekleyen alternatif paketleri aramanız gerekebilir.

1. **proje yeniden hedefleme veya yükseltme den sonra packages.config eklenen yeniden yükleme özniteliği gerektirir**
    - NuGet, paketlerin bir projeyi yeniden hedeflemeveya yükseltmeden etkilendiğini tespit `requireReinstallation="true"` ederse, `packages.config` etkilenen tüm paket başvurularına bir öznitelik ekler. Bu nedenle, Visual Studio'daki sonraki her yapı, bu paketler için yapı uyarıları yükseltir, böylece yeniden yüklemeyi hatırlayabilirsiniz.

1. **Bağımlılıkları olan paketleri yeniden yükleme**
    - `Update-Package –reinstall`özgün paketin aynı sürümünü yeniden yükler, ancak belirli sürüm kısıtlamaları sağlanmadıkça bağımlılıkların en son sürümünü yükler. Bu, yalnızca bir sorunu gidermek için gereken bağımlılıkları güncelleştirmenize olanak tanır. Ancak, bu bir bağımlılığı önceki bir sürüme geri `Update-Package <dependency_name>` yuvarlarsa, bağımlı paketi etkilemeden bu bir bağımlılığı yeniden yüklemek için kullanabilirsiniz.
    - `Update-Package –reinstall <packageName> -ignoreDependencies`özgün paketin aynı sürümünü yeniden yükler, ancak bağımlılıkları yeniden yüklemez. Paket bağımlılıklarının güncelleştirilmesi bozuk bir duruma neden olabileceğinde bunu kullanın

1. **Bağımlı sürümler söz konusu olduğunda paketleri yeniden yükleme**
    - Yukarıda açıklandığı gibi, bir paketi yeniden yüklemek, ona bağlı olan diğer yüklü paketlerin sürümlerini değiştirmez. O halde, bir bağımlılığı yeniden yüklemek bağımlı paketi bozabilir.
