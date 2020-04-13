---
title: NuGet paketlerinde ön sürüm sürümleri
description: Sürüm öncesi paketler oluşturma kılavuzu
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610708"
---
# <a name="building-pre-release-packages"></a>Ön sürüm paketleri oluşturma

Yeni bir sürüm numarası na sahip güncelleştirilmiş bir paket yayımladiğinizde, NuGet bunu örneğin Visual Studio'daki Paket Yöneticisi UI'sinde gösterildiği gibi "en son kararlı sürüm" olarak kabul eder:

![Paket Yöneticisi UI en son kararlı sürümü gösteren](media/Prerelease_01-LatestStable.png)

Kararlı bir sürüm, üretimde kullanılacak kadar güvenilir kabul edilen bir sürümdür. En son kararlı sürüm aynı zamanda paket güncelleştirme olarak veya paket geri yükleme sırasında yüklenecek olansürümdür [(paketleri yeniden yükleme ve güncelleştirmede](../consume-packages/reinstalling-and-updating-packages.md)açıklandığı gibi kısıtlamalara tabidir).

Yazılım sürüm yaşam döngüsünü desteklemek için, NuGet 1.6 ve daha sonra sürüm numarası gibi `-alpha`semantik bir sürüm soneki `-beta`içeren `-rc`ön sürüm paketlerinin dağıtımına izin verir , , veya . Daha fazla bilgi için [Paket sürümüne](../concepts/package-versioning.md#pre-release-versions)bakın.

Bu tür sürümleri aşağıdaki yollardan birini kullanarak belirtebilirsiniz:

- **Projenizde [`PackageReference`](../consume-packages/package-references-in-project-files.md) **: `.csproj` dosyanın [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) öğesine anlamsal sürüm soneki ekleyin:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **Projenizde bir [`packages.config`](../reference/packages-config.md) dosya varsa:** [`.nuspec`](../reference/nuspec.md) dosyanın [`version`](../reference/nuspec.md#version) öğesine anlamsal sürüm soneki ekleyin:

    ```xml
    <version>1.0.1-alpha</version>
    ```

Kararlı bir sürüm yayınlamaya hazır olduğunuzda, soneği kaldırmanız ve paketin ön sürümsürümlerinden önce gelen bir şey olması. Yine, [Bkz. Paket sürüm.](../concepts/package-versioning.md#pre-release-versions)

## <a name="installing-and-updating-pre-release-packages"></a>Sürüm öncesi paketlerin yüklenmesi ve güncellenmesi

Varsayılan olarak, NuGet paketleri ile çalışırken ön sürüm sürümleri içermez, ancak aşağıdaki gibi bu davranışı değiştirebilirsiniz:

- **Visual Studio'da Paket Yöneticisi UI**: **NuGet Paketlerini** Yönet'te, **Ön Sürüm Ekle** kutusunu işaretleyin:

    ![Visual Studio'ya yayın öncesi onay kutusu ekle](media/Prerelease_02-CheckPrerelease.png)

    Bu kutuyu ayarlamak veya temizlemek, Paket Yöneticisi Arabirimi'ni ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.

- **Paket Yöneticisi Konsolu** `-IncludePrerelease` : `Find-Package`Anahtarı `Get-Package` `Install-Package`, `Sync-Package`, `Update-Package` , ve komutlarla kullanın. [PowerShell Referans](../reference/powershell-reference.md)bakın.

- **NuGet CLI**: `-prerelease` Anahtarı `install`, `update` `delete`, `mirror` , ve komutlarla kullanın. [NuGet CLI referansına](../reference/nuget-exe-cli-reference.md) bakın

## <a name="semantic-versioning"></a>Anlamsal sürüm

[Anlamsal Sürüm veya SemVer kuralı,](https://semver.org/spec/v1.0.0.html) temel kodun anlamını iletmek için sürüm numaralarındaki dizeleri nasıl kullanılacağını açıklar.

Bu sözleşmede, her sürümün `Major.Minor.Patch`üç bölümü vardır, aşağıdaki anlamı ile:

- `Major`: Son dakika değişiklikleri
- `Minor`: Yeni özellikler, ancak geriye uyumlu
- `Patch`: Geriye uyumlu hata düzeltmeleri yalnızca

Ön sürüm sürümleri daha sonra yama numarasından sonra bir tire ve dize ekleyerek gösterilir. Teknik olarak konuşursak, tire ve NuGet ön sürüm olarak paketi ele alacak sonra *herhangi bir* dize kullanabilirsiniz. NuGet daha sonra geçerli UI'de tam sürüm numarasını görüntüler ve tüketicilerin anlamını kendileri için yorumlamalarına neden olur.

Bunu göz önünde bulundurarak, genellikle aşağıdaki gibi tanınan adlandırma kuralları takip etmek iyidir:

- `-alpha`: Alfa salınımı, genellikle devam aşamasındaki işler ve deneyler için kullanılır
- `-beta`: Beta sürümü, genellikle bir sonraki planlanan sürüm için tamamlanmış özellik, ancak bilinen hataları içerebilir.
- `-rc`: Sürüm adayı, önemli hatalar ortaya çıkmadıkça genellikle nihai (kararlı) bir sürüm.

> [!Note]
> NuGet 4.3.0+ gibi nokta gösterimi ile ön sürüm numaraları destekleyen [Semantik Sürüm v2.0.0](https://semver.org/spec/v2.0.0.html)destekler `1.0.1-build.23`. Nokta gösterimi 4.3.0'dan önce NuGet sürümleriyle desteklenmez. NuGet önceki sürümlerinde, gibi `1.0.1-build23` bir form kullanabilirsiniz ama bu her zaman bir ön sürüm olarak kabul edildi.

Ancak kullandığınız sonekler ne olursa olsun, NuGet onlara ters alfabetik sırayla öncelik verecektir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

Gösterildiği gibi, herhangi bir sonek olmayan sürüm her zaman ön sürüm sürümlerine göre öncelikli olacaktır.

Lider 0s semver2 ile gerekli değildir, ancak eski sürüm şema ile vardır. Çift basamaklı sayılar (veya daha fazla) kullanabilen ön sürüm etiketlerine sahip sayısal sonekler kullanıyorsanız, sayılar büyüdükçe doğru şekilde sıralandığından emin olmak için beta.01 ve beta.05'teki gibi önde gelen sıfırları kullanın. Bu öneri yalnızca eski sürüm şeması için geçerlidir.
