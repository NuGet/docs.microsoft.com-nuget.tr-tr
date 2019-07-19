---
title: NuGet paketlerindeki yayın öncesi sürümler
description: Yayın öncesi paketleri oluşturma kılavuzu
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: deedebfc6ac03b374c44e2c07a191da26a7dd68c
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317662"
---
# <a name="building-pre-release-packages"></a>Yayın öncesi paketleri oluşturma

Güncelleştirilmiş bir paketi yeni bir sürüm numarasıyla serbest bıraktığınızda, NuGet bir "en son kararlı yayın" olarak, örneğin Visual Studio içindeki paket yöneticisi Kullanıcı arabiriminde gösterildiği gibi kabul eder:

![En son kararlı yayını gösteren Paket Yöneticisi Kullanıcı arabirimi](media/Prerelease_01-LatestStable.png)

Kararlı bir yayın, üretimde kullanılmak üzere yeterince güvenilir olarak kabul edilen bir sürümdür. En son kararlı sürüm aynı zamanda bir paket güncelleştirmesi olarak veya paket geri yükleme sırasında ( [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)bölümünde açıklandığı gibi kısıtlamalara tabidir) yüklenir.

NuGet 1,6 ve üzeri, yazılım sürümü yaşam döngüsünü desteklemek için yayın öncesi paketlerin dağıtımına izin verir; burada sürüm numarası,, veya `-alpha` `-rc`gibi bir anlamsal sürüm oluşturma soneki `-beta`içerir. Daha fazla bilgi için bkz. [paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).

Aşağıdaki yollarla bu tür sürümleri belirtebilirsiniz:

- **Projeniz kullanıyorsa [`PackageReference`](../consume-packages/package-references-in-project-files.md)** : `.csproj` dosyanın [öğesineanlamsürümüsonekinidahilet:`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion)

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Projenizde bir [`packages.config`](../reference/packages-config.md) dosya varsa**: [`.nuspec`](../reference/nuspec.md) dosyanın [`version`](../reference/nuspec.md#version) öğesine anlam sürümü sonekini ekleyin:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Kararlı bir sürümü bırakmaya hazırsanız, soneki kaldırmanız yeterlidir ve paketin herhangi bir yayın öncesi sürümüne göre öncelikli olması gerekir. Yeniden, bkz. [paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Yayın öncesi paketleri yükleme ve güncelleştirme

Varsayılan olarak, NuGet, paketlerle çalışırken yayın öncesi sürümleri içermez, ancak bu davranışı aşağıdaki şekilde değiştirebilirsiniz:

- **Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi**: **NuGet Paketlerini Yönet** Kullanıcı arabiriminde, **ön sürümü dahil et** kutusunu işaretleyin:

    ![Visual Studio 'da ön sürümü dahil et onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    Bu kutuyu ayarlama veya Temizleme, Paket Yöneticisi Kullanıcı arabirimini ve yükleyebileceğiniz sürümlerin listesini yeniler.

- **Paket Yöneticisi konsolu**: `Find-Package`, `-IncludePrerelease` ,,`Install-Package`Ve komutlarıyla`Update-Package` anahtarı kullanın. `Get-Package` `Sync-Package` [PowerShell başvurusuna](../reference/powershell-reference.md)bakın.

- **NUGET CLI**: `install` `-prerelease` , ,`update`Vekomutlarıyla anahtarıkullanın`mirror` . `delete` [NUGET CLI başvurusuna](../reference/nuget-exe-cli-reference.md) bakın

## <a name="semantic-versioning"></a>Anlamsal sürüm oluşturma

[Anlamsal sürüm oluşturma veya SemVer kuralı](http://semver.org/spec/v1.0.0.html) , temel alınan kodun anlamını iletmek için sürüm numaralarında dizelerin nasıl kullanılacağını açıklar.

Bu kurala göre, her sürüm üç bölümden `Major.Minor.Patch`oluşur ve aşağıdaki anlamı vardır:

- `Major`: Yeni değişiklikler
- `Minor`: Yeni özellikler, ancak geriye dönük olarak uyumlu
- `Patch`: Yalnızca geriye dönük uyumlu hata düzeltmeleri

Yayın öncesi sürümler daha sonra düzeltme numarasından sonra bir tire ve dize eklenerek gösterilir. Teknik açıdan, kısa çizgiden sonra *herhangi bir* dizeyi kullanabilirsiniz ve NuGet paketi yayın öncesi olarak kabul eder. Daha sonra NuGet, geçerli kullanıcı arabirimindeki tam sürüm numarasını görüntüleyerek tüketicilere göre anlamı yorumlamak için tüketicileri bırakır.

Bu göz önünde bulundurularak, aşağıdaki gibi tanınan adlandırma kurallarını izlemek genellikle yararlı olur:

- `-alpha`: Genellikle süren iş ve deneme için kullanılan Alpha yayını.
- `-beta`: Beta sürümü, genellikle bir sonraki planlanmış yayın için özellik tamamlanmıştır, ancak bilinen hatalar içerebilir.
- `-rc`: Yayın Adayı, genellikle önemli hatalar oluşmadığı takdirde son derece nihai (kararlı) bir sürümdür.

> [!Note]
> NuGet 4.3.0 +, ' de `1.0.1-build.23`olduğu gibi nokta gösterimi ile yayın öncesi numaralarını destekleyen [anlamsal sürüm oluşturma v 2.0.0](http://semver.org/spec/v2.0.0.html)'yi destekler. Nokta gösterimi 4.3.0 öncesi NuGet sürümleriyle desteklenmez. NuGet 'in önceki sürümlerinde, gibi `1.0.1-build23` bir form kullanabilirsiniz, ancak bu her zaman yayın öncesi sürüm olarak kabul edilir.

Ancak kullandığınız son ekler, NuGet 'e ters alfabetik sırada öncelik verecektir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

Gösterildiği gibi, herhangi bir sonek olmadan sürüm, yayın öncesi sürümlerden her zaman öncelikli olur. Ayrıca, Çift basamaklı sayılar (veya daha fazla) kullanan serbest bırakma etiketleriyle sayısal sonekler kullanırsanız, sayılar daha büyük olduğunda doğru sıraladıklarından emin olmak için beta01 ve beta05 içinde önde gelen sıfırları kullanın.
