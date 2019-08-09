---
title: NuGet paketlerini yeniden yükleme ve güncelleştirme
description: Visual Studio 'daki bozuk paket başvurularına göre paketlerin yeniden yüklenmesi ve güncelleştirilmesi için gerekli olduğu zaman hakkındaki ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: bc077220e05b14180baac9611fda9234675ad640
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860534"
---
# <a name="how-to-reinstall-and-update-packages"></a>Paketleri yeniden yükleme ve güncelleştirme

Bir paketi [yeniden yüklemek için](#when-to-reinstall-a-package)aşağıda açıklanan bazı durumlar vardır. Bu, bir pakete yapılan başvuruların bir Visual Studio projesi içinde bozulmasına neden olabilir. Bu durumlarda, paketin aynı sürümünün kaldırılması ve yeniden yüklenmesi bu başvuruları çalışma sırasına geri yükler. Bir paketin güncelleştirilmesi, genellikle bir paketi çalışma sırasına geri yükleyen güncelleştirilmiş bir sürümü yükleme anlamına gelir.

Visual Studio 'da Paket Yöneticisi konsolu paketleri güncelleştirmek ve yeniden yüklemek için birçok esnek seçenek sağlar.

Paketlerin güncelleştirilmesi ve yeniden yüklenmesi şu şekilde gerçekleştirilir:

| Yöntem | Güncelleştirme | Yeniden yükleyin |
| --- | --- | --- |
| Paket Yöneticisi Konsolu ( [Update-Package kullanma](#using-update-package)bölümünde açıklanmıştır) | `Update-Package`komutundaki | `Update-Package -reinstall`komutundaki |
| Paket Yöneticisi UI | **Güncelleştirmeler** sekmesinde bir veya daha fazla paket seçin ve **Güncelleştir** ' i seçin. | **Yüklü** sekmesinde bir paket seçin, adını kaydedin ve **Kaldır**' ı seçin. **Araştır** sekmesine geçin, paket adını arayın, seçin ve sonra da **Install**öğesini seçin. |
| nuget.exe CLI | `nuget update`komutundaki | Tüm paketler için paket klasörünü silip çalıştırın `nuget install`. Tek bir paket için paket klasörünü silin ve aynısını yeniden yüklemek `nuget install <id>` için kullanın. |

> [!NOTE]
> DotNet CLı için eşdeğer yordam gerekli değildir. Benzer bir senaryoda, [DotNet CLI ile paketleri geri yükleyebilirsiniz](package-restore.md#restore-using-the-dotnet-cli).

Bu makalede:

- [Bir paketin ne zaman yeniden yüklenmesi](#when-to-reinstall-a-package)
- [Yükseltme sürümlerini kısıtlama](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Bir paketin ne zaman yeniden yüklenmesi

1. **Paket geri yüklemeden sonra bozuk başvurular**: Bir projeyi açtıysanız ve NuGet paketlerini geri yüklediyseniz ancak hala bozuk başvurular görüyorsanız, bu paketlerin her birini yeniden yüklemeyi deneyin.
1. **Silinen dosyalar nedeniyle proje bozuk**: NuGet, paketlerden eklenen öğeleri kaldırmanızı engellemez, bu nedenle bir paketten yüklenmiş içerikleri yanlışlıkla değiştirmek ve projenizi bölmek kolaydır. Projeyi geri yüklemek için etkilenen paketleri yeniden yükleyin.
1. **Paket güncelleştirmesi projeyi**bir daha Yerleştir: Bir paketteki güncelleştirme bir projeyi kesintiye uğramıyorsa, hata genellikle güncelleştirilmiş bir bağımlılık paketi tarafından meydana gelir. Bağımlılığın durumunu geri yüklemek için söz konusu paketi yeniden yükleyin.
1. **Proje yeniden hedefleme veya Yükselt**: Bu, bir proje yeniden hedeflendiğinde veya yükseltildiğinde ve hedef çerçevesindeki değişiklik nedeniyle paketin yeniden yüklenmesi gerekiyorsa yararlı olabilir. NuGet, proje yeniden hedefledikten hemen sonra bu tür durumlarda derleme hatası gösterir ve sonraki derleme uyarıları paketin yeniden yüklenmesi gerekebileceklerini bilmenizi sağlar. Proje yükseltmesinde, NuGet proje yükseltme günlüğünde bir hata gösterir.
1. **Bir paketi geliştirme sırasında yeniden yükleme**: Paket yazarları, davranışı test etmek için genellikle geliştirdikleri paketin aynı sürümünü yeniden yüklemeniz gerekir. Komut yeniden yükleme zorlaması için bir seçenek sağlamıyor, bunun yerine kullanın `Update-Package -reinstall`. `Install-Package`

## <a name="constraining-upgrade-versions"></a>Yükseltme sürümlerini kısıtlama

Varsayılan olarak, bir paketi yeniden yüklemek veya güncelleştirmek, *her zaman* paket kaynağından kullanılabilir olan en son sürümü yüklenir.

Ancak, `packages.config` yönetim biçimini kullanan projelerde, sürüm aralığını özellikle kısıtlayabilirsiniz. Örneğin, uygulamanızın yalnızca bir paketin 1. x sürümüyle ve 2,0 ve üzerinde değil, paket API 'sindeki önemli bir değişiklik nedeniyle, yükseltmelerini 1. x sürümlerine kısıtlamak isteyebilirsiniz. Bu, uygulamayı kesen yanlışlıkla yapılan güncelleştirmeleri önler.

Bir kısıtlama ayarlamak için, bir `packages.config` metin düzenleyicisinde açın, söz konusu bağımlılığı bulun ve `allowedVersions` özniteliği bir sürüm aralığı ile ekleyin. Örneğin, güncelleştirmeleri 1. x sürümüyle kısıtlamak için şu şekilde `allowedVersions` `[1,2)`ayarlayın:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Her durumda, [paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards)bölümünde açıklanan gösterimi kullanın.

## <a name="using-update-package"></a>Update-Package kullanma

Aşağıda açıklanan [hususlar göz önünde bulundurmanız](#considerations) , Visual Studio Paket Yöneticisi konsolundaki [Update-Package komutunu](../reference/ps-reference/ps-ref-update-package.md) kullanarak herhangi bir paketi kolayca yeniden yükleyebilirsiniz (**Araçlar** > **NuGet Paket Yöneticisi**  >  **Paket Yöneticisi konsolu**).

```ps
Update-Package -Id <package_name> –reinstall
```

Bu komutun kullanılması, bir paketi kaldırıp aynı paketi aynı sürüme sahip NuGet galerisinde bulmaya çalışırken çok daha kolaydır. `-Id` Anahtarın isteğe bağlı olduğunu unutmayın.

Varsa, bir paketi `-reinstall` daha yeni bir sürüme güncelleştirmeksizin aynı komut. Söz konusu paket bir projede zaten yüklenmemişse, komut bir hata verir; diğer bir deyişle `Update-Package` , paketleri doğrudan yüklemez.

```ps
Update-Package <package_name>
```

Varsayılan olarak, `Update-Package` bir Çözümdeki tüm projeleri etkiler. Eylemi belirli bir projeyle sınırlandırmak için, Çözüm Gezgini ' de göründüğü `-ProjectName` gibi projenin adını kullanarak anahtarını kullanın:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Bir projedeki tüm paketleri *güncelleştirmek* için (veya kullanarak `-reinstall`yeniden yükleme), belirli bir paketi belirtmeden kullanın: `-ProjectName`

```ps
Update-Package -ProjectName MyProject
```

Bir Çözümdeki tüm paketleri güncelleştirmek için, yalnızca diğer bağımsız `Update-Package` değişkenler veya anahtarlar olmadan kendisini kullanın. Tüm güncelleştirmeleri gerçekleştirmek için önemli bir zaman sürebileceğinden bu formu dikkatle kullanın:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Bir proje veya çözüm içinde, [Packagereference](../Consume-Packages/Package-References-in-Project-Files.md) kullanan bir projedeki paketleri güncelleştirmek, paketin en son sürümüne (yayın öncesi paketler hariç) güncelleştirilir. İsterseniz kullanan `packages.config` projeler, güncelleştirme sürümlerini [kısıtlama sürümlerinde](#constraining-upgrade-versions)aşağıda açıklanan şekilde sınırlandırabilir.

Komutuyla ilgili tüm ayrıntılar için bkz. [Update-Package](../reference/ps-reference/ps-ref-update-package.md) Reference.

### <a name="considerations"></a>Dikkat Edilecekler

Bir paket yeniden yüklenirken aşağıdakiler etkilenebilir:

1. **Paketleri proje hedef çerçevesi yeniden hedeflemeye göre yeniden yükleme**
    - Basit bir durumda, çalışma kullanarak `Update-Package –reinstall <package_name>` bir paketi yeniden yüklemek yeterlidir. Eski bir hedef çerçeveye karşı yüklenen bir paket kaldırılır ve projenin geçerli hedef çerçevesine karşı aynı paket yüklenir.
    - Bazı durumlarda, yeni hedef Framework 'ü desteklemeyen bir paket olabilir.
        - Bir paket taşınabilir sınıf kitaplıklarını (PCLs) destekliyorsa ve proje, artık paket tarafından desteklenmeyen platformların bir birleşimine yeniden hedeflendiğinde, paket başvuruları yeniden yüklendikten sonra eksik olur.
        - Bu, doğrudan kullandığınız paketlere veya bağımlılıklar olarak yüklenen paketlere yönelik yüzeysel olabilir. Yeni hedef çerçevesini desteklemek için doğrudan kullandığınız paket, bağımlılığı olmasa da mümkündür.
        - Uygulamanızın yeniden hedeflenmesi sonrasında paketlerin yeniden yüklenmesi, derleme veya çalışma zamanı hatalarıyla sonuçlanırsa, hedef çatısını döndürmeniz veya yeni hedef çatısını düzgün şekilde destekleyen alternatif paketleri aramanız gerekebilir.

1. **proje yeniden hedefledikten veya yükseltildikten sonra Packages. config dosyasına eklenen talep ırereınstallation özniteliği**
    - NuGet bir projeyi yeniden hedefleyerek veya yükseltirken paketlerin etkilendiğini algılarsa, içindeki `requireReinstallation="true"` `packages.config` tüm etkilenen paket başvurularına bir özniteliği ekler. Bu nedenle, Visual Studio 'daki her bir sonraki derleme bu paketlere yönelik derleme uyarıları oluşturur, böylece bunları yeniden yüklemeyi anımsayabilir.

1. **Bağımlılıkları olan paketleri yeniden yükleme**
    - `Update-Package –reinstall`özgün paketin aynı sürümünü yeniden yükler, ancak belirli sürüm kısıtlamaları sağlanmadığı takdirde bağımlılıkların en son sürümünü yükler. Bu, bir sorunu çözebilmeniz için yalnızca gerektiğinde bağımlılıkları güncelleştirmenize olanak tanır. Ancak, bu, önceki bir sürüme bağımlılık kaydederse, bağımlı paketi etkilemeden bu bağımlılığı yeniden `Update-Package <dependency_name>` yüklemek için kullanabilirsiniz.
    - `Update-Package –reinstall <packageName> -ignoreDependencies`özgün paketin aynı sürümünü yeniden yükler, ancak bağımlılıkları yeniden yüklemez. Paket bağımlılıklarını güncelleştirirken bunu kullan durumu bozulmuş duruma gelebilir

1. **Bağımlı sürümler dahil edildiğinde paketleri yeniden yükleme**
    - Yukarıda açıklandığı gibi, bir paketin yeniden yüklenmesi kendisine bağımlı olan diğer yüklü paketlerin sürümlerini değiştirmez. Daha sonra, bir bağımlılığı yeniden yüklemek bağımlı paketi bozabilir.
