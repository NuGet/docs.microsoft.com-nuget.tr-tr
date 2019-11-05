---
title: NuGet paketlerindeki yayın öncesi sürümler
description: Yayın öncesi paketleri oluşturma kılavuzu
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610708"
---
# <a name="building-pre-release-packages"></a>Yayın öncesi paketleri oluşturma

Güncelleştirilmiş bir paketi yeni bir sürüm numarasıyla serbest bıraktığınızda, NuGet bir "en son kararlı yayın" olarak, örneğin Visual Studio içindeki paket yöneticisi Kullanıcı arabiriminde gösterildiği gibi kabul eder:

![En son kararlı yayını gösteren Paket Yöneticisi Kullanıcı arabirimi](media/Prerelease_01-LatestStable.png)

Kararlı bir yayın, üretimde kullanılmak üzere yeterince güvenilir olarak kabul edilen bir sürümdür. En son kararlı sürüm aynı zamanda bir paket güncelleştirmesi olarak veya paket geri yükleme sırasında ( [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)bölümünde açıklandığı gibi kısıtlamalara tabidir) yüklenir.

NuGet 1,6 ve üzeri, yazılım sürümü yaşam döngüsünü desteklemek için yayın öncesi paketlerin dağıtımına izin verir; burada sürüm numarası, `-alpha`, `-beta`veya `-rc`gibi bir anlamsal sürüm oluşturma soneki içerir. Daha fazla bilgi için bkz. [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions).

Aşağıdaki yollarla bu tür sürümleri belirtebilirsiniz:

- **Projeniz [`PackageReference`](../consume-packages/package-references-in-project-files.md)kullanıyorsa,** `.csproj` dosyanın [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) öğesine anlamsal sürüm sonekini dahil edin:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Projenizde bir [`packages.config`](../reference/packages-config.md) dosyası varsa**: [`.nuspec`](../reference/nuspec.md) dosyasının [`version`](../reference/nuspec.md#version) öğesine anlamsal sürüm sonekini ekleyin:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Kararlı bir sürümü bırakmaya hazırsanız, soneki kaldırmanız yeterlidir ve paketin herhangi bir yayın öncesi sürümüne göre öncelikli olması gerekir. Yeniden, bkz. [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Yayın öncesi paketleri yükleme ve güncelleştirme

Varsayılan olarak, NuGet, paketlerle çalışırken yayın öncesi sürümleri içermez, ancak bu davranışı aşağıdaki şekilde değiştirebilirsiniz:

- **Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi**: **NuGet Paketlerini Yönet** Kullanıcı arabiriminde, **ön sürümü dahil et** kutusunu işaretleyin:

    ![Visual Studio 'da ön sürümü dahil et onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    Bu kutuyu ayarlama veya Temizleme, Paket Yöneticisi Kullanıcı arabirimini ve yükleyebileceğiniz sürümlerin listesini yeniler.

- **Paket Yöneticisi konsolu**: `-IncludePrerelease` anahtarını `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`ve `Update-Package` komutlarıyla kullanın. [PowerShell başvurusuna](../reference/powershell-reference.md)bakın.

- **NUGET CLI**: `install`, `update`, `delete`ve `mirror` komutlarıyla `-prerelease` anahtarını kullanın. [NUGET CLI başvurusuna](../reference/nuget-exe-cli-reference.md) bakın

## <a name="semantic-versioning"></a>Anlamsal sürüm oluşturma

[Anlamsal sürüm oluşturma veya SemVer kuralı](https://semver.org/spec/v1.0.0.html) , temel alınan kodun anlamını iletmek için sürüm numaralarında dizelerin nasıl kullanılacağını açıklar.

Bu durumda, her sürüm üç bölümden oluşur ve aşağıdaki anlamı `Major.Minor.Patch`:

- `Major`: değişiklikler kesiliyor
- `Minor`: yeni özellikler, ancak geriye dönük olarak uyumlu
- `Patch`: yalnızca geriye dönük uyumlu hata düzeltmeleri

Yayın öncesi sürümler daha sonra düzeltme numarasından sonra bir tire ve dize eklenerek gösterilir. Teknik açıdan, kısa çizgiden sonra *herhangi bir* dizeyi kullanabilirsiniz ve NuGet paketi yayın öncesi olarak kabul eder. Daha sonra NuGet, geçerli kullanıcı arabirimindeki tam sürüm numarasını görüntüleyerek tüketicilere göre anlamı yorumlamak için tüketicileri bırakır.

Bu göz önünde bulundurularak, aşağıdaki gibi tanınan adlandırma kurallarını izlemek genellikle yararlı olur:

- `-alpha`: genellikle süren iş ve deneme için kullanılan Alpha sürümü
- `-beta`: beta sürümü, genellikle bir sonraki planlı yayın için bir özelliktir, ancak bilinen hatalar içerebilir.
- `-rc`: yayın adayı, genellikle önemli hatalar oluşmadığı takdirde son derece nihai (kararlı) bir sürümdür.

> [!Note]
> NuGet 4.3.0 +, `1.0.1-build.23`gibi nokta gösterimi ile yayın öncesi numaraları destekleyen [anlamsal sürüm oluşturma v 2.0.0](https://semver.org/spec/v2.0.0.html)'yi destekler. Nokta gösterimi 4.3.0 öncesi NuGet sürümleriyle desteklenmez. NuGet 'in önceki sürümlerinde `1.0.1-build23` gibi bir form kullanabilirsiniz, ancak bu her zaman yayın öncesi sürüm olarak kabul edilir.

Ancak kullandığınız son ekler, NuGet 'e ters alfabetik sırada öncelik verecektir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Gösterildiği gibi, herhangi bir sonek olmadan sürüm, yayın öncesi sürümlerden her zaman öncelikli olur.

Önde gelen 0s, semver2 için gerekli değildir, ancak eski sürüm şemasıyla bulunur. Çift basamaklı sayılar (veya daha fazla) kullanan serbest bırakma etiketleriyle sayısal sonekler kullanırsanız, sayılar daha büyük olduğunda doğru sıraladıklarından emin olmak için Beta. 01 ve Beta. 05 ' de önde gelen sıfırları kullanın. Bu öneri yalnızca eski sürüm şeması için geçerlidir.
