---
title: NuGet paketi sürüm başvurusu
description: Sürüm numaraları ve diğer paketleri bağımlı bir NuGet paketi ve bağımlılıkları nasıl yüklendiğini aralıkları belirtme hakkında tam ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549779"
---
# <a name="package-versioning"></a>Paket sürümü oluşturma

Belirli bir paket her zaman paket tanımlayıcısını ve bir tam sürüm numarası kullanılarak olarak adlandırılır. Örneğin, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org adresinden birkaç düzine belirli paketleri sürümden değişen kullanılabilir olan *4.1.10311* sürüme *6.1.3* (en son kararlı sürüm) ve yayın öncesi sürümleri çeşitli *6.2.0-beta1*.

Bir paket oluştururken, bir isteğe bağlı yayın öncesi metni soneki ile belirli bir sürüm numarası atayın. Öte yandan, paket tüketildiğinde, bir tam sürüm numarası veya kabul edilebilir bir sürüm aralığı belirtebilirsiniz.

Bu konuda:

- [Sürüm Temelleri](#version-basics) yayın öncesi son ekleri dahil olmak üzere.
- [Sürüm aralıklarını ve joker karakterler](#version-ranges-and-wildcards)
- [Normalleştirilmiş sürüm numaraları](#normalized-version-numbers)

## <a name="version-basics"></a>Sürüm temelleri

Belirli bir sürüm numarasını biçimindedir *ana.İkincil.yama [-soneki]*, aşağıdaki anlamlara sahip olduğu bileşenler:

- *Ana*: bozucu değişiklikler
- *Küçük*: yeni özellikler, ancak geriye dönük uyumluluk
- *Düzeltme Eki*: yalnızca geriye dönük olarak uyumlu hata düzeltmeleri
- *-Soneki* (isteğe bağlı): bir tire yayın öncesi bir sürümü belirten bir dize tarafından izlenen (aşağıdaki [Semantic Versioning veya SemVer 1.0 kuralı](http://semver.org/spec/v1.0.0.html)).

**Örnekler:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org bir tam sürüm numarası eksik paketin karşıya yüklenmesi reddeder. Sürüm belirtilmelidir `.nuspec` ya da proje dosyası paketi oluşturmak için kullanılır.

### <a name="pre-release-versions"></a>Yayın öncesi sürümleri

Teknik terimlerle açıklamak gerekirse, paket creators herhangi bir dize sonek olarak NuGet gibi bir sürüm yayın öncesi değerlendirir ve diğer bir yorumu yayın öncesi bir sürümü belirtmek için kullanabilirsiniz. Diğer bir deyişle, tam sürüm ne olursa olsun kullanıcı Arabiriminde dize NuGet görüntüler dahil, tüketiciye soneki'nın anlamı herhangi bir yorumu çıkılıyor.

Bu, paket geliştiriciler genellikle tanınan adlandırma kurallarına uymuyor olduğu söylenebilir:

- `-alpha`: Yayın alfa, genellikle iş ilerleme ve deneme için kullanılır.
- `-beta`: Beta sürümü, genellikle bir özellik için bir sonraki tam sürüm planlı, ancak bilinen hataları içerebilir.
- `-rc`: Genellikle büyük olasılıkla son sürüm Sürüm Adayı (stable) sürece önemli hatalar ortaya çıkmaya başladı.

> [!Note]
> NuGet 4.3.0+ destekler [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), olarak nokta gösterimi, yayın öncesi sürüm numaralarıyla destekleyen *1.0.1-build.23*. Nokta gösterimi 4.3.0 önce NuGet sürümü ile desteklenmiyor. Bir form gibi kullanabileceğiniz *1.0.1-build23*.

Paket başvuruları ve birden çok paket sürümü yalnızca soneki farklılık çözülürken NuGet sürümü bir soneki olmayan ilk seçer ve ardından yayın öncesi sürümler ters alfabetik düzende öncelik geçerlidir. Örneğin, aşağıdaki sürümleri gösterilen sırada seçilir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Semantic Versioning 2.0.0

NuGet 4.3.0+ ve Visual Studio 2017 sürüm 15.3 + ile NuGet destekler [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).

Belirli bir SemVer v2.0.0 semantikleri, eski istemcilere desteklenmez. NuGet Paket sürümü aşağıdaki deyimleri true ise SemVer v2.0.0 belirli olmasını göz önünde bulundurur:

- Yayın öncesi etiketi, örneğin, noktayla ayrılmış *1.0.0-alpha.1*
- Derleme meta veri, örneğin, sürüme sahip *1.0.0+githash*

Nuget.org için aşağıdaki ifadeler doğru ise bir paket bir SemVer v2.0.0 paketi olarak tanımlanır:

- Paketin kendi SemVer v2.0.0 uyumlu ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan sürümüdür.
- Paket bağımlılık sürüm aralıklardan herhangi biriyle uyumlu SemVer v2.0.0 ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan bir minimum veya maksimum sürümüne sahip; Örneğin, *[1.0.0-alpha.1,)*.

Nuget.org için bir SemVer v2.0.0 özgü paketini karşıya yükleyin, paketin eski istemcilere görünmez ve yalnızca aşağıdaki NuGet istemcileri için kullanılabilir:

- NuGet 4.3.0+
- Visual Studio 2017 sürüm 15.3 +
- Visual Studio 2015 ile [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- DotNet
  - dotnetcore.exe (.NET SDK'sı 2.0.0+)

Üçüncü taraf istemcileri:

- JetBrains Rider
- Paket sürüm 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Sürüm aralıklarını ve joker karakterler

Paket bağımlılıklarını söz konusu olduğunda NuGet sürüm aralıklarını, aşağıdaki şekilde özetlenen belirtmek için aralığı gösterimi kullanılarak destekler:

| Gösterim | Uygulanan kural | Açıklama |
|----------|--------------|-------------|
| 1.0 | x ≥ 1.0 | En düşük sürüm, kapsamlı |
| (1.0,) | x > 1.0 | En düşük sürümü, özel |
| [1.0] | x 1.0 == | Tam sürümü eşleşmiyor |
| (,1.0] | x ≤ 1.0 | En yüksek sürümü, kapsamlı |
| (,1.0) | < 1.0 x | Özel olarak, en yüksek sürüm |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Kapsamlı tam aralığı |
| (1.0,2.0) | 1.0 < < 2.0 x | Özel tam aralığı |
| [1.0,2.0) | 1.0 ≤ < 2.0 x | Karma dahil en düşük ve özel en yüksek sürüm |
| (1.0)    | geçersiz | geçersiz |

PackageReference biçimini kullanırken bir joker karakter gösterimini kullanarak NuGet da destekler \*büyük, küçük, düzeltme eki ve sayının yayın öncesi son bölümü için. İle joker karakterler desteklenmez `packages.config` biçimi.

> [!Note]
> Yayın öncesi sürümleri, sürüm aralıklarını çözerken dahil edilmez. Yayın öncesi sürümler *olan* joker karakter kullanırken dahil (\*). Sürüm aralığı *[1.0,2.0]*, örneğin, 2.0 beta, ancak joker karakter gösterimi içermez _2.0-*_ yapar. Bkz: [sorun 912](https://github.com/NuGet/Home/issues/912) daha fazla yayın öncesi jokerler tartışma.

### <a name="examples"></a>Örnekler

Proje dosyalarında her zaman bir sürüm veya sürüm aralığı için Paket bağımlılıklarını belirtin `packages.config` dosyaları ve `.nuspec` dosyaları. Bir sürüm veya sürüm aralığı, NuGet olmadan 2.8.x daha önce en son kullanılabilir Paket sürümü bir bağımlılık çözülürken ise seçerse NuGet 3.x ve daha sonra en düşük Paket sürümü seçer. Bir sürüm veya sürüm aralığı bu belirsizliğin ortadan kaldırır. belirtme.

#### <a name="references-in-project-files-packagereference"></a>Proje dosyalarında (PackageReference) başvuruları

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

**Başvurularının `packages.config`:**

İçinde `packages.config`, her bağımlılık bir tam olarak listelenen `version` paketler geri yüklenirken kullanılan özniteliği. `allowedVersions` Özniteliği yalnızca güncelleştirme işlemleri sırasında paket güncelleştirilmesi sürümleri sınırlamak için kullanılır.

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

**Başvurularının `.nuspec` dosyaları**

`version` Özniteliğini bir `<dependency>` öğesi, bir bağımlılık için kabul edilebilir aralık sürümlerini açıklar.

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
> Bir değişiklik NuGet 3.4 ve üzeri budur.

Paketleri yükleme sırasında bir depodan edinme yeniden yükleyin veya geri yükleme işlemleri, NuGet 3.4 + sürüm numaraları gibi davranır:

- Sürüm numaraları 2f3b kaldırılır:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Sürüm numarasının dördüncü bölümünde sıfır atlanacak

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

Bu normalleştirme paketleri sürüm numaraları etkilemez. Bu, yalnızca nasıl NuGet sürümlerini bağımlılıkları çözümlenirken eşleşen etkiler.

Ancak, NuGet paket depolarınızın bu değerleri Paket sürümü çoğaltma önlemek için aynı şekilde NuGet olarak ele almanız gerekir. Bu nedenle sürümünü içeren bir depo *1.0* paketi sürümü ayrıca barındırmamalıdır *1.0.0* ayrı ve farklı bir paket olarak.
