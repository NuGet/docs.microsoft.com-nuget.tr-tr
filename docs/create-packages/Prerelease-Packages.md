---
title: NuGet paketlerini de yayın öncesi sürümleri
description: Yayın öncesi paketleri oluşturmaya yönelik Kılavuzlar
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 696f51905198defdbfd475ba7d010ac3e27ac557
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877937"
---
# <a name="building-pre-release-packages"></a>Yayın öncesi paketleri oluşturma

Güncelleştirilmiş bir paketin yeni bir sürüm numarasına sahip yayın her birinin ", örneğin Visual Studio'da Paket Yöneticisi UI gösterildiği gibi en son kararlı sürüm" olarak NuGet göz önünde bulundurur:

![Paket Yöneticisi UI en son kararlı sürüm gösteriliyor](media/Prerelease_01-LatestStable.png)

Kararlı bir sürüm üretimde kullanılacak güvenilir olarak değerlendirilmeyen biridir. En son kararlı sürüm ayrıca paket güncelleştirmesi veya paket geri yükleme sırasında yüklenecek olan bölümdür (açıklanan kısıtlamalarına tabi [Reinstalling ve paketlerin güncelleştirilmesi](../consume-packages/reinstalling-and-updating-packages.md)).

Yazılım sürüm yaşam döngüsünü desteklemek için NuGet 1.6 ve üzeri için yayın öncesi paketleri dağıtımını burada sürüm numarası gibi semantic versioning soneki içerir sağlıyor `-alpha`, `-beta`, veya `-rc`. Daha fazla bilgi için [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).

Bu tür sürümleri üç yolla belirtebilirsiniz:

- `.nuspec` Dosya: anlamsal Sürüm soneki dahil `version` öğesi:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- `.csproj` Dosya: anlamsal Sürüm soneki dahil `PackageVersion` öğesi:

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- Derleme özniteliklerinin: sürümüyle belirtin `AssemblyInformationalVersionAttribute`:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    Bu değer yerine belirtilen bir NuGet alır `AssemblyVersion` semantic versioning desteklemeyen özniteliği.

Kararlı bir sürüm hazır olduğunuzda, yalnızca soneki kaldırın ve paketin tüm yayın öncesi sürümlere göre önceliklidir. Yeniden bakın [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).

## <a name="installing-and-updating-pre-release-packages"></a>Yükleme ve güncelleştirme yayın öncesi paketleri

Varsayılan olarak, NuGet paketleri ile çalışırken, yayın öncesi sürümleri içermez, ancak bu davranışı şu şekilde değiştirebilirsiniz:

- **Visual Studio'da Paket Yöneticisi UI**: İçinde **NuGet paketlerini Yönet** kullanıcı Arabirimi, onay **ön sürümü dahil et** kutusunda:

    ![Visual Studio'da INCLUDE Ön onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    Ayarlama ya da bu kutuyu temizleyerek Paket Yöneticisi UI ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.

- **Paket Yöneticisi Konsolu**: Kullanım `-IncludePrerelease` anahtarı ile `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, ve `Update-Package` komutları. Başvurmak [PowerShell başvurusu](../tools/powershell-reference.md).

- **NuGet CLI**: Kullanım `-prerelease` anahtarı ile `install`, `update`, `delete`, ve `mirror` komutları. Başvurmak [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)

## <a name="semantic-versioning"></a>Semantic versioning

[Semantic Versioning veya SemVer kuralı](http://semver.org/spec/v1.0.0.html) arka plandaki kod anlamını iletmek için sürüm numaraları dizelerde nasıl açıklar.

Bu kural, her sürüm üç bölümden `Major.Minor.Patch`, aşağıdaki anlama sahip:

- `Major`: Yeni değişiklikler
- `Minor`: Geriye dönük olarak uyumlu ancak yeni özellikler
- `Patch`: Geriye dönük yalnızca uyumlu hata düzeltmeleri

Yayın öncesi sürümleri düzeltme numarası sonra kısa çizgi ve bir dize ekleyerek belirtilir. Kullanabileceğiniz teknik terimlerle açıklamak gerekirse, *herhangi* kısa çizgi ve NuGet paketi yayın öncesi değerlendirir sonra dize. NuGet, kendileri için anlam yorumlama tüketicilerin bırakarak geçerli kullanıcı arabiriminde, daha sonra tam sürüm numarası görüntüler.

Bunu aklınızda, aşağıdaki gibi tanınmış adlandırma kurallarına uymuyor genellikle iyi olur:

- `-alpha`: Genellikle, iş ilerleme ve deneme için kullanılan alfa sürümü
- `-beta`: Beta sürümü, genellikle bir özellik için bir sonraki tam sürüm planlı, ancak bilinen hataları içerebilir.
- `-rc`: Sürüm Adayı, genellikle büyük olasılıkla son sürüm (stable) sürece önemli hatalar ortaya çıkmaya başladı.

> [!Note]
> NuGet 4.3.0+ destekler [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), olarak nokta gösterimi, yayın öncesi sürüm numaralarıyla destekleyen `1.0.1-build.23`. Nokta gösterimi 4.3.0 önce NuGet sürümü ile desteklenmiyor. NuGet önceki sürümlerinde, bir form gibi kullanabileceğinizi `1.0.1-build23` ancak bu her zaman yayın öncesi bir sürümü kabul.

Ancak kullanmak istediğiniz sonekleri NuGet bunları öncelik ters alfabetik sırada verecektir:

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

Gösterildiği gibi tüm soneki olmadan sürümü her zaman yayın öncesi sürümleri üzerinde öncelikli olur. Ayrıca çift haneli kullanıyor olabileceğiniz yayın öncesi etiketlerle sayısal sonekleri kullanırsanız sayıları (veya daha fazla), 2f3b beta01 ve beta05 olduğu gibi doğru sayı daha büyük ulaştıklarında sıralaması emin olmak için unutmayın.
