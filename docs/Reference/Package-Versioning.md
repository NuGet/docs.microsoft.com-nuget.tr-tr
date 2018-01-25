---
title: "NuGet paketi sürüm başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Sürüm numaraları ve diğer paketleri, bağlı bir NuGet paketi ve bağımlılıkları nasıl yükleneceğini aralıklarını belirtme hakkında tam ayrıntılar."
keywords: "sürüm oluşturma, NuGet Paket bağımlılıklarını, NuGet bağımlılık sürümleri, NuGet sürüm numaralarını, NuGet Paket sürümü, sürüm aralıkları, sürüm belirtimleri, normalleştirilmiş sürüm numaraları"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="package-versioning"></a>Paket sürümü oluşturma

Belirli bir paket her zaman paket tanımlayıcısını ve tam bir sürüm numarası kullanılarak olarak adlandırılır. Örneğin, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org üzerinde çeşitli düzine belirli paketler sürümünden arasında değişen kullanılabilir olan *4.1.10311* sürümüne *6.1.3* (en son kararlı yayın) ve yayın öncesi sürümleri çeşitli *6.2.0-beta1*.

Bir paket oluştururken, bir isteğe bağlı bir yayım öncesi metin sonekiyle özel sürüm numarası atayın. Diğer taraftan, paketleri kullanırken, bir tam sürüm numarası veya kabul edilebilir sürüm aralığı belirtebilirsiniz.

Bu konuda:

- [Sürüm Temelleri](#version-basics) yayın öncesi sonekleri dahil olmak üzere.
- [Sürüm aralıkları ve joker karakterler](#version-ranges-and-wildcards)
- [Normalleştirilmiş sürüm numaraları](#normalized-version-numbers)

## <a name="version-basics"></a>Sürüm temelleri

Belirli bir sürüm numarasını biçimindedir *Major.Minor.Patch [-soneki]*, burada bileşenleri şu anlama gelir:

- *Ana*: yeni değişiklikler
- *İkincil*: geriye dönük olarak uyumlu ancak yeni özellikler
- *Düzeltme Eki*: yalnızca geriye dönük olarak uyumlu hata düzeltmeleri
- *-Soneki* (isteğe bağlı): bir tire izlenen bir yayım öncesi sürümünü belirten bir dizeyle (aşağıdaki [anlamsal sürüm oluşturma veya SemVer 1.0 kuralı](http://semver.org/spec/v1.0.0.html)).

**Örnekler:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org tam bir sürüm numarası eksik paketini karşıya yükleme reddeder. Sürüm belirtilmelidir `.nuspec` veya paketi oluşturmak üzere kullanılan proje dosyası.

### <a name="pre-release-versions"></a>Yayın öncesi sürümleri

Teknik olarak konuşarak paket oluşturucuları herhangi bir dize sonek olarak NuGet herhangi bir sürüm yayın öncesi değerlendirir ve diğer bir yorumlama yapar gibi bir yayın öncesi sürüm belirtmek için kullanabilirsiniz. Diğer bir deyişle, tam sürüm ne olursa olsun kullanıcı Arabiriminde dize NuGet görüntüler eklendiyse, tüketiciye soneki 's anlamı herhangi yorumu çıkılıyor.

Bu, paket geliştiriciler genellikle tanınan adlandırma kurallarına uygun olduğu söylenebilir:

- `-alpha`: Genelde iş ilerleme ve deneme için kullanılan alfa sürüm.
- `-beta`: Beta sürümü, genellikle bir özellik için sonraki tam planlanmış serbest bırakma, ancak bilinen hataları içerebilir.
- `-rc`: Sürüm Adayı, genellikle büyük olasılıkla son bir yayın (stable) önemli hatalar ortaya çıkan sürece.

> [!Note]
> NuGet 4.3.0+ destekleyen [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), olarak noktalı gösterim ön sürüm numaralarıyla destekleyen *1.0.1-build.23*. Noktalı gösterim 4.3.0 önce NuGet sürümleriyle desteklenmiyor. Bir form gibi kullanabilirsiniz *1.0.1-build23*.

Paket referanslarını ve birden çok paket sürümü yalnızca soneki ile farklı çözülürken NuGet sonek olmayan bir sürümünü ilk seçer ve ardından yayın öncesi sürümler ters alfabetik sırada öncelik uygular. Örneğin, aşağıdaki sürümleri gösterilen sırada seçilen:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Anlamsal sürüm oluşturma 2.0.0

NuGet 4.3.0+ ve Visual Studio 2017 sürüm 15.3 + ile NuGet destekleyen [anlamsal sürüm oluşturma 2.0.0](http://semver.org/spec/v2.0.0.html).

SemVer v2.0.0 belirli semantiği eski istemciler desteklenmez. NuGet aşağıdaki ifadelerden true ise SemVer v2.0.0 belirli olması için bir paket sürümü göz önünde bulundurur:

- Noktalı virgülle ayrılmış, örneğin, yayın öncesi etiket *1.0.0-alpha.1*
- Yapı-meta verileri, örneğin, sürümde *1.0.0+githash*

Aşağıdaki ifadeler doğru ise nuget.org için bir paket SemVer v2.0.0 paket olarak tanımlanır:

- Paketin kendi SemVer v2.0.0 uyumlu ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan sürümüdür.
- Paketin bağımlılık sürümü aralıklardan herhangi biriyle uyumlu SemVer v2.0.0 ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan bir minimum veya maksimum sürümüne sahiptir; Örneğin, *[1.0.0-alpha.1,)*.

Nuget.org için SemVer v2.0.0 özgü paketini karşıya yükleyin, paketin eski istemcileri için görünmez ve yalnızca aşağıdaki NuGet istemcileri için kullanılabilir şöyledir:

- NuGet 4.3.0+
- Visual Studio 2017 sürüm 15.3 +
- Visual Studio 2015 ile birlikte [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet.exe (.NET SDK 2.0.0+)

Üçüncü taraf istemciler:

- JetBrains Rider
- Paket sürüm 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Sürüm aralıkları ve joker karakterler

Paket bağımlılıklarını söz konusu olduğunda NuGet sürümü aralıkları, aşağıdaki şekilde özetlenmiştir belirtmek için aralığı gösterimini kullanarak destekler:

| Gösterimi | Uygulanan kural | Açıklama |
|----------|--------------|-------------|
| 1.0 | 1.0 ≤ x | En düşük sürüm, (bunlar dahil) |
| (1.0,) | 1.0 < x | En düşük sürüm, özel |
| [1.0] | x == 1.0 | Tam sürümü eşleşmiyor |
| (,1.0] | x ≤ 1.0 | En yüksek sürüm, (bunlar dahil) |
| (,1.0) | x < 1.0 | Özel olarak, en yüksek sürüm |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Tam aralık, (bunlar dahil) |
| (1.0,2.0) | 1.0 < < 2.0 x | Tam aralık, özel |
| [1.0,2.0) | 1.0 ≤ < 2.0 x | Karma (bunlar dahil) en düşük ve özel en yüksek sürüm |
| (1.0)    | geçersiz | geçersiz |

PackageReference biçimi kullanıldığında, bir joker karakter gösterimini kullanarak NuGet de destekler \*, birincil, ikincil, düzeltme eki ve sayının yayın öncesi soneki bölümleri için. İle joker karakterler desteklenmez `packages.config` biçimi.

> [!Note]
> Yayın öncesi sürümleri, sürüm aralıkları çözülürken dahil edilmez. Yayın öncesi sürümler *olan* bir joker karakter kullanırken dahil (\*). Sürüm aralığı *[1.0,2.0]*, örneğin, 2.0 beta ancak joker gösterimi içermez _2.0-*_ yapar. Bkz: [sorun 912](https://github.com/NuGet/Home/issues/912) yayın öncesi joker karakterler hakkında daha fazla açıklama için.

### <a name="examples"></a>Örnekler

Her zaman bir sürümü ya da sürüm aralığı Paket bağımlılıklarını için proje dosyalarında belirtin `packages.config` dosyaları ve `.nuspec` dosyaları. Sürüm veya sürüm aralığı, NuGet olmadan 2.8.x ve daha önce en son kullanılabilir Paket sürümü bir bağımlılık çözülürken ancak seçer NuGet 3.x ve daha sonra en düşük Paket sürümü seçer. Bir sürümün ya da bu belirsizlik aralığı önler sürümünün belirtme.

#### <a name="references-in-project-files-packagereference"></a>Proje dosyaları (PackageReference) başvuruları

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**Başvurur `packages.config`:**

İçinde `packages.config`, her bağımlılık bir tam listelenen `version` paketleri geri yüklenirken kullanılan özniteliği. `allowedVersions` Özniteliği için paket güncelleştirilmesi sürümleri sınırlamak için yalnızca güncelleştirme işlemleri sırasında kullanılır.

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

**Başvurur `.nuspec` dosyaları**

`version` Özniteliğini bir `<dependency>` öğesi için bir bağımlılık kabul edilebilir aralık sürümlerini açıklar.

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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
> Önemli bir değişiklik NuGet 3.4 ve daha sonra budur.

Yükleme sırasında bir depodan paketler alma yeniden yükleyin veya geri yükleme işlemleri, NuGet 3.4 + sürüm numaraları gibi davranır:

- Sürüm numaraları 2f3b kaldırılır:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Sürüm numarasını dördüncü bir parçası olarak sıfır atlanacak

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Bu normalleştirme paketlerde kendilerini sürüm numaraları etkilemez; Bu, yalnızca nasıl NuGet sürümleri bağımlılıkları çözümlenirken eşleşen etkiler.

Ancak, NuGet paketi depoları bu değerleri Paket sürümü çoğaltılmasını önlemek için aynı şekilde NuGet ele almanız gerekir. Bu nedenle sürümünü içeren bir havuz *1.0* paketi sürümünü de barındırmamalıdır *1.0.0* ayrı ve farklı bir paket olarak.
