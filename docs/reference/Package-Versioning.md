---
title: NuGet paket sürümü başvurusu
description: Bir NuGet paketinin bağımlı olduğu diğer paketler için sürüm numaralarını ve aralıklarını belirtmeyle ilgili tam ayrıntılar ve bağımlılıkların yüklenme şekli.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019993"
---
# <a name="package-versioning"></a>Paket sürümü oluşturma

Belirli bir paket her zaman kendi paket tanımlayıcısını ve tam sürüm numarasını kullanmaya başvurulur. Örneğin, nuget.org üzerindeki [Entity Framework](https://www.nuget.org/packages/EntityFramework/) , sürüm *4.1.10311* ' den sürüm *6.1.3* (en son kararlı sürüm) ve *6.2.0-Beta1 gibi çeşitli yayın öncesi sürümler arasında değişen birkaç düzine özel pakete sahiptir* .

Bir paket oluştururken, isteğe bağlı bir yayın öncesi metin sonekine sahip belirli bir sürüm numarası atarsınız. Paketleri kullanırken, diğer yandan, tam sürüm numarasını veya bir dizi kabul edilebilir sürümü belirtebilirsiniz.

Bu konuda:

- Yayın öncesi son eklerini içeren [Sürüm temelleri](#version-basics) .
- [Sürüm aralıkları ve joker karakterler](#version-ranges-and-wildcards)
- [Normalleştirilmiş sürüm numaraları](#normalized-version-numbers)

## <a name="version-basics"></a>Sürüm temelleri

Belirli bir sürüm numarası, *ana. ikincil. Patch [-suffix]* biçiminde olduğundan, bileşenler aşağıdaki anlamlara sahiptir:

- *Birincil*: Yeni değişiklikler
- *İkincil*: Yeni özellikler, ancak geriye dönük olarak uyumlu
- *Düzeltme Eki*: Yalnızca geriye dönük uyumlu hata düzeltmeleri
- *-Sonek* (isteğe bağlı): ön sürüm sürümünü belirten bir dize ( [anlamsal sürüm oluşturma veya SemVer 1,0 kuralını](http://semver.org/spec/v1.0.0.html)takip eden).

**Örnekler:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org, tam sürüm numarası bulunmayan tüm paket karşıya yüklemeyi reddeder. Sürümün, `.nuspec` paketi oluşturmak için kullanılan proje dosyasında belirtilmesi gerekir.

### <a name="pre-release-versions"></a>Yayın öncesi sürümler

Teknik oluşturucular, yayın öncesi sürümü göstermek için herhangi bir dizeyi sonek olarak kullanabilir, böylece NuGet bu sürümü ön sürüm olarak değerlendirir ve başka yorum yapmaz. Diğer bir deyişle, NuGet herhangi bir kullanıcı arabiriminin dahil olduğu tüm sürüm dizesini, son ekin anlamı olan tüketiciye herhangi bir yorum bırakarak görüntüler.

Yani, paket geliştiricileri genellikle tanınan adlandırma kurallarını izler:

- `-alpha`: Alfa yayını, genellikle süren iş ve deneme için kullanılır.
- `-beta`: Beta sürümü, genellikle bir sonraki planlanmış yayın için özellik tamamlanmıştır, ancak bilinen hatalar içerebilir.
- `-rc`: Yayın Adayı, genellikle önemli hatalar oluşmadığı takdirde son derece nihai (kararlı) bir sürümdür.

> [!Note]
> NuGet 4.3.0 +, *1.0.1-Build. 23*' te olduğu gibi nokta gösterimi ile yayın öncesi numaralarını destekleyen [semver 2.0.0](http://semver.org/spec/v2.0.0.html)'i destekler. Nokta gösterimi 4.3.0 öncesi NuGet sürümleriyle desteklenmez. *1.0.1-build23*gibi bir biçim kullanabilirsiniz.

Paket başvuruları ve birden çok paket sürümü yalnızca sonek tarafından farklılık gösterdiği zaman, NuGet önce sonek olmadan bir sürüm seçer, ardından ön sürüm sürümüne ters alfabetik sırada öncelik uygular. Örneğin, aşağıdaki sürümler gösterilen tam sırada seçilebilir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>Anlamsal sürüm oluşturma 2.0.0

NuGet 4.3.0 + ve Visual Studio 2017 sürüm 15.3 + ile NuGet, [semantik sürümü oluşturma 2.0.0](http://semver.org/spec/v2.0.0.html)'yi destekler.

SemVer v 2.0.0 'in belirli semantiklerinden bazıları eski istemcilerde desteklenmez. NuGet, aşağıdaki deyimlerden herhangi biri geçerliyse, bir paket sürümünü SemVer v 2.0.0 'e özgü olarak kabul eder:

- Yayın öncesi etiketi noktayla ayrılmıştır, örneğin, *1.0.0-Alpha. 1*
- Sürümde derleme meta verileri vardır, örneğin, *1.0.0 + githash*

Nuget.org için bir paket, aşağıdaki deyimlerden herhangi biri doğruysa bir SemVer v 2.0.0 paketi olarak tanımlanır:

- Paketin kendi sürümü, yukarıda tanımlanan semver v 2.0.0 uyumludur ancak SemVer v 1.0.0 uyumlu değildir.
- Paketin bağımlılık sürümü aralıklarının herhangi birinin, yukarıda tanımlanan semver v 2.0.0 uyumlu ancak SemVer v 1.0.0 uyumlu olmayan en düşük veya en yüksek sürümü vardır; Örneğin, *[1.0.0-Alpha. 1,)* .

Nuget.org 'e özel bir SemVer v 2.0.0 paketi yüklerseniz, paket eski istemcilere görünmez ve yalnızca aşağıdaki NuGet istemcilerinin kullanımına açık olur:

- NuGet 4.3.0 +
- Visual Studio 2017 sürüm 15.3 +
- [NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) Ile Visual Studio 2015
- dotnet
  - dotnetcore. exe (.NET SDK 2.0.0 +)

Üçüncü taraf istemcileri:

- JetBrains Rider
- Paket sürüm 5.0 +

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>Sürüm aralıkları ve joker karakterler

NuGet, paket bağımlılıklarına başvururken, sürüm aralıklarını belirtmek için Aralık gösterimini kullanmayı destekler, şöyle özetlenir:

| İmle | Uygulanan kural | Açıklama |
|----------|--------------|-------------|
| 1.0 | x ≥ 1,0 | En düşük sürüm, dahil |
| (1.0,) | x > 1,0 | En düşük sürüm, özel |
| [1.0] | x = = 1,0 | Tam sürüm eşleşmesi |
| (,1.0] | x ≤ 1,0 | En yüksek sürüm, dahil |
| (,1.0) | x < 1,0 | En yüksek sürüm, özel |
| [1.0,2.0] | 1,0 ≤ x ≤ 2,0 | Tam Aralık, dahil |
| (1.0,2.0) | 1,0 < x < 2,0 | Tam Aralık, özel |
| [1.0,2.0) | 1,0 ≤ x < 2,0 | Karma kapsamlı en düşük ve en yüksek sürüm |
| (1.0)    | geçersiz | geçersiz |

Bu, packagereference biçimi kullanılırken, büyük/küçük, düzeltme eki uygulama ve \*bu sayının yayın öncesi sonek bölümleri için bir joker karakter gösterimi kullanılmasını da destekler. Bu `packages.config` biçimde joker karakterler desteklenmez.

> [!Note]
> PackageReference içindeki sürüm aralıkları yayın öncesi sürümleri içerir. Tasarım yaparak, kayan sürümler, kabul edilmediği takdirde ön sürüm sürümlerini çözmez. İlgili özellik isteğinin durumu için bkz. [sorun 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).

### <a name="examples"></a>Örnekler

Proje dosyaları, `packages.config` dosyalar ve `.nuspec` dosyalardaki paket bağımlılıkları için her zaman bir sürüm veya sürüm aralığı belirtin. Sürüm veya sürüm aralığı olmadan, NuGet 2.8. x ve önceki sürümleri bir bağımlılığı çözümlerken kullanılabilir en son paket sürümünü seçer, ancak NuGet 3. x ve sonraki sürümler en düşük paket sürümünü seçer. Bir sürüm veya sürüm aralığı belirtildiğinde bu belirsizlik önlenir.

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

**`packages.config`Başvurular:**

' `packages.config`De, her bağımlılık, paketler geri yüklenirken `version` kullanılan tam bir öznitelik ile listelenir. `allowedVersions` Özniteliği yalnızca paketin güncelleştirilemeyebilir sürümü kısıtlamak için güncelleştirme işlemleri sırasında kullanılır.

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

**`.nuspec` Dosyalardaki başvurular**

`version` Bir`<dependency>` öğesindeki özniteliği, bir bağımlılık için kabul edilebilir olan Aralık sürümlerini açıklar.

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
> Bu, NuGet 3,4 ve üzeri için bir son değişiklik değildir.

Yükleme, yeniden yükleme veya geri yükleme işlemleri sırasında bir depodan paket edinirken, NuGet 3.4 + sürüm numaralarını aşağıdaki gibi davranır:

- Önde gelen sıfırlar sürüm numaralarına kaldırılır:

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- Sürüm numarasının dördüncü bölümünde sıfır yok edilir

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`ve `restore` işlemler mümkün olduğunda sürümleri normalleştirin. Zaten oluşturulan paketler için, bu normalleştirme, paketlerdeki sürüm numaralarını etkilemez; Bağımlılıklar çözümlenirken yalnızca NuGet 'in sürümleri nasıl eşleştiğini etkiler.

Ancak, NuGet paket depoları, paket sürümü çoğaltmasını engellemek için bu değerleri NuGet ile aynı şekilde ele almalıdır. Bu nedenle, bir paketin *1,0* sürümünü içeren bir depo ayrıca ayrı ve farklı bir paket olarak sürüm *1.0.0* barındırmamalıdır.
