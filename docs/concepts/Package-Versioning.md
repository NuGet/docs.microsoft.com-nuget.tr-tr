---
title: NuGet Paketi Sürüm Başvurusu
description: NuGet paketinin bağlı olduğu diğer paketler için sürüm numaralarını ve aralıklarını belirtme ve bağımlılıkların nasıl yüklendiği yle ilgili tam ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147454"
---
# <a name="package-versioning"></a>Paket sürümü oluşturma

Belirli bir paket her zaman paket tanımlayıcısı ve tam sürüm numarası kullanılarak adlandırılır. Örneğin, nuget.org'daki [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sürüm *4.1.10311'den* sürüm *6.1.3* 'e (en son kararlı sürüm) ve *6.2.0-beta1*gibi çeşitli ön sürüm sürümlerine kadar birkaç düzine özel paket mevcuttur.

Bir paket oluştururken, isteğe bağlı bir ön sürüm metin soneki yle belirli bir sürüm numarası atarsınız. Diğer taraftan, paketleri tüketirken, tam sürüm numarasını veya kabul edilebilir sürümler aralığını belirtebilirsiniz.

Bu konuda:

- Ön sürüm sonekleri de dahil olmak üzere [sürüm temelleri.](#version-basics)
- [Sürüm aralıkları](#version-ranges)
- [Normalleştirilmiş sürüm numaraları](#normalized-version-numbers)

## <a name="version-basics"></a>Sürüm temelleri

Belirli bir sürüm numarası *Major.Minor.Patch[-Soneki]* şeklindedir ve bileşenlerin aşağıdaki anlamları vardır:

- *Ana :* Son dakika değişiklikleri
- *Minor*: Yeni özellikler, ancak geriye dönük uyumlu
- *Yama*: Geriye uyumlu hata düzeltmeleri yalnızca
- *-Soneki* (isteğe bağlı): bir ön sürüm sürümünü gösteren bir dize takip tire [(Anlamsal Sürüm veya SemVer 1.0 kuralını](https://semver.org/spec/v1.0.0.html)takip eder).

**Örnekler:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org, tam sürüm numarası bulunmayan paket yüklemeyi reddeder. Sürüm, paketi oluşturmak `.nuspec` için kullanılan proje dosyasında belirtilmelidir.

### <a name="pre-release-versions"></a>Ön sürüm sürümleri

Teknik olarak konuşursak, paket oluşturucular, nuget ön sürüm gibi herhangi bir sürümü ele alır ve başka bir yorum yapmaması nedeniyle, sürüm öncesi sürümü belirtmek için herhangi bir dizeyi sonek olarak kullanabilirler. Diğer bir deyişle, NuGet, sonekin anlamının yorumunu tüketiciye bırakarak, tam sürüm dizesini ne olursa olsun, ilgili olduğunda görüntüler.

Yani, paket geliştiriciler genellikle tanınan adlandırma kuralları izleyin dedi:

- `-alpha`: Alfa salınımı, genellikle devam etmekte olan işler ve deneyler için kullanılır.
- `-beta`: Beta sürümü, genellikle bir sonraki planlanan sürüm için tamamlanmış özellik, ancak bilinen hataları içerebilir.
- `-rc`: Sürüm adayı, önemli hatalar ortaya çıkmadıkça genellikle nihai (kararlı) bir sürüm.

> [!Note]
> NuGet 4.3.0+ *1.0.1-build.23'te*olduğu gibi nokta gösterimi ile ön sürüm sayılarını destekleyen [SemVer 2.0.0'ı](https://semver.org/spec/v2.0.0.html)destekler. Nokta gösterimi 4.3.0'dan önce NuGet sürümleriyle desteklenmez. *1.0.1-build23*gibi bir form kullanabilirsiniz.

Paket başvurularını ve birden çok paket sürümünü yalnızca sonek ile farklı olarak çözerken, NuGet önce sonek olmayan bir sürüm seçer, ardından ön sürüm sürümlerine ters alfabetik sırayla öncelik uygular. Örneğin, aşağıdaki sürümler gösterilen tam sırada seçilir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Anlamsal Versiyon 2.0.0

NuGet 4.3.0+ ve Visual Studio 2017 sürüm 15.3+ ile [NuGet, Anlamsal Sürüm 2.0.0'ı](https://semver.org/spec/v2.0.0.html)destekler.

SemVer v2.0.0 bazı semantik eski istemcilerde desteklenmez. NuGet, aşağıdaki ifadelerden biri doğruysa, bir paket sürümünüSemVer v2.0.0'a özgü olarak kabul eder:

- Ön sürüm etiketi nokta ayrılmış, örneğin, *1.0.0-alfa.1*
- Sürüm, örneğin, *1.0.0+githash* yapı-meta verivardır

Nuget.org için, aşağıdaki ifadelerden biri doğruysa, bir paket SemVer v2.0.0 paketi olarak tanımlanır:

- Paketin kendi sürümü SemVer v2.0.0 uyumludur, ancak yukarıda tanımlandığı gibi SemVer v1.0.0 uyumlu değildir.
- Paketin bağımlılık sürüm aralıklarından herhangi biri, semver v2.0.0 uyumlu olan minimum veya maksimum bir sürüme sahiptir, ancak yukarıda tanımlanan SemVer v1.0.0 uyumlu değildir; örneğin, *[1.0.0-alfa.1, )*.

nuget.org'a semver v2.0.0'a özel bir paket yüklerseniz, paket eski istemciler tarafından görünmez ve yalnızca aşağıdaki NuGet istemcileri tarafından kullanılabilir:

- NuGet 4.3.0+
- Visual Studio 2017 sürümü 15.3+
- Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) ile
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

Üçüncü taraf istemciler:

- JetBrains Rider
- Paket sürüm 5.0+

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>Sürüm aralıkları

Paket bağımlılıklarına atıfta bulunulduğunda, NuGet aşağıdaki gibi özetlenen sürüm aralıklarını belirtmek için aralık gösterimini desteklemektedir:

| Gösterim | Uygulanan kural | Açıklama |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | Minimum sürüm, dahil |
| (1.0,) | x > 1.0 | Minimum sürüm, özel |
| [1.0] | x == 1.0 | Tam sürüm eşleşmesi |
| (,1.0] | x ≤ 1.0 | Maksimum sürüm, dahil |
| (,1.0) | x < 1.0 | Maksimum sürüm, özel |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Tam aralık, dahil |
| (1.0,2.0) | 1.0 < x < 2.0 | Tam aralık, özel |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Karışık dahil minimum ve münhasır maksimum sürüm |
| (1.0)    | geçersiz | geçersiz |

PackageReference biçimini kullanırken, NuGet, numaranın Büyük, \*Küçük, Yama ve ön sürüm sonek parçaları için kayan bir gösterim ihdası da destekler. Kayan sürümler `packages.config` biçimiyle desteklenmez.

> [!Note]
> PackageReference'daki sürüm aralıkları, ön sürüm sürümleri içerir. Tasarım gereği, kayan sürümler tercih edilmedikçe ön sürüm sürümlerini çözmez. İlgili özellik isteğinin durumu için [6434 sorununa](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)bakın.

### <a name="examples"></a>Örnekler

Proje dosyalarındaki, `packages.config` dosyalardaki ve `.nuspec` dosyalardaki paket bağımlılıkları için her zaman bir sürüm veya sürüm aralığı belirtin. Bir sürüm veya sürüm aralığı olmadan, NuGet 2.8.x ve daha önce bir bağımlılık çözerken en son kullanılabilir paket sürümünü seçer, NuGet 3.x ise ve daha sonra en düşük paket sürümünü seçer. Sürüm veya sürüm aralığının belirtilmesi bu belirsizliği önler.

#### <a name="references-in-project-files-packagereference"></a>Proje dosyalarındaki başvurular (PackageReference)

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Referanslar `packages.config`:**

Her `packages.config`bağımlılık, paketleri geri verirken kullanılan tam `version` bir öznitelikile listelenir. Öznitelik, `allowedVersions` yalnızca paketin güncelleştirilebileceği sürümleri kısıtlamak için güncelleştirme işlemleri sırasında kullanılır.

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**Dosyalardaki `.nuspec` başvurular**

Bir `version` `<dependency>` öğedeki öznitelik, bağımlılık için kabul edilebilir aralık sürümlerini açıklar.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>Normalleştirilmiş sürüm numaraları

> [!Note]
> Bu NuGet 3.4 ve sonrası için bir kırılma değişikliktir.

Yükleme, yeniden yükleme veya geri yükleme işlemleri sırasında bir depodan paket alırken, NuGet 3.4+ sürüm numaralarını aşağıdaki gibi davranır:

- Satır aralığı sıfırları sürüm numaralarından kaldırılır:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Sürüm numarasının dördüncü bölümünde ki sıfır atlanır

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- SemVer 2.0.0 yapı meta verileri kaldırılır

        1.0.7+r3456 is treated as 1.0.7

`pack`ve `restore` işlemler mümkün olduğunda sürümleri normalleştirir. Zaten oluşturulmuş paketler için bu normalleştirme, paketlerdeki sürüm numaralarını etkilemez; yalnızca NuGet'in bağımlılıkları çözerken sürümlerle nasıl eşleştiğini etkiler.

Ancak, NuGet paket depoları, paket sürümünün çoğaltılmasını önlemek için bu değerleri NuGet ile aynı şekilde ele almalıdır. Bu nedenle, bir paketin sürüm *1.0'ını* içeren bir depo, sürüm *1.0.0'ı* ayrı ve farklı bir paket olarak barındırmamalıdır.
