---
title: NuGet project.json archive content
description: Çeşitli bitleri project.json içerik NuGet belgeleri diğer alanlarından kaldırıldı.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: d43f002b740b669de13f5872844ac0df97fc8fdc
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467782"
---
# <a name="projectjson-archive"></a>project.json archive

`project.json` Yönetim biçimi, NuGet ile tanıtılmıştır 3.x ve belirli proje türleri kullanılır. Bu bağımlılıklar doğrudan proje dosyasında listelenen PackageReference biçimi sunulmasıyla birlikte kullanım dışı bırakıldı.

Ayrıca bkz:

- [project.json schema](project-json.md)
- [Paket yazarlarının Project.JSON etkisi](project-json-impact.md)
- [project.json ve UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>project.json yönetim biçimi

*İlk olarak [paket geri yükleme](../what-is-nuget.md).*

Yönetim biçim listesinde:

- [`project.json`](project-json.md): *(kullanım dışı)* genel bir paket grafikte ilişkili bir dosya ile proje bağımlılıklarınızı listesini tutar bir JSON dosyası `project.lock.json`. Bu biçim ile değiştiriliyor PackageReference kullanım dışı bırakılmıştır.

## <a name="nuget-restore-on-mono"></a>Mono nuget geri yükleme

*İlk olarak [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md).*

Çalışan `project.json`.

## <a name="constraining-package-versions-with-restore"></a>Geri yükleme ile kısıtlayan paket sürümleri

*İlk olarak [paket geri yükleme](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*

- `project.json`: Doğrudan bağımlılık'ın sürüm numarasına sahip bir sürüm aralığı belirtin. Örneğin:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet CLI komutları

- `nuget install` ile çalışmıyor `project.json`.
- `nuget restore`: kullanarak projeleri ile `project.json`, oluşturur bir `project.lock.json` dosyası ve bir `<project>.nuget.props` gerekirse dosya. (Her iki dosya kaynak denetiminden atlanabilir.) `<projectPath>` İşaret edebilir bağımsız değişkeni bir `project.json` dosya ve işaret olarak aynı davranışa sahip bir `packages.config` ya da proje dosyası. Paket klasörler için öncelik sırasına `%userprofile%\.nuget\packages` kullanırken ilk aranır `project.json`.
- `nuget update`: Mono üzerinde bu komutu kullanarak projeleriyle çalışmıyor `project.json`.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference ile bağımlılık çözümlemesi

*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*

Ayrıca PackageReference davranışını uygular `project.json`. NuGet geri yükleme, bağımlılık grafiği adlı bir dosyaya yazar `project.lock.json` yanı sıra `project.json`.

## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#managing-dependency-assets).*

Kullanırken `project.json` biçimi, üst düzey proje bağımlılıkları akışına hangi varlıklarından denetleyebilirsiniz. Ayrıntılar için bkz [project.json](project-json.md).

## <a name="excluding-references"></a>Başvuruları hariç

*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#excluding-references).*

- `project.json`: ekleme `"exclude" : "all"` PackageC için bağımlılık olarak:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a>Uyumsuz paket hatalarını çözme

*İlk olarak [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*

Hataları çözümleme eklenen anlamına gelir:

- **Tavsiye**: geçici bir çözüm, paket yazarı ile çalışırken, proje hedefleme `netcore`, `netstandard`, ve `netcoreapp` diğer çerçeveler, böylece bu hedefleme paketleri izin vererek, uyumlu olarak belirtmek kullanılacak diğer çerçeveler. Bkz: [project.json içeri aktarır](project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Bu beklenmeyen davranışlara neden olabilir bir güncelleştirme üzerinde paket yazarı ile çalışarak paket uyumsuzlukları çözmek en iyi şekilde yeniden.

## <a name="target-frameworks"></a>Hedef çerçeveler

*İlk olarak [hedef çerçeveyi](../reference/target-frameworks.md).*

- [project.json](project-json.md): `frameworks` Düğüm karşı projenin derlenebilir framework sürümlerini belirtir.

## <a name="creating-a-package"></a>Paket oluşturma

*İlk olarak [paket oluşturma](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Ayar paket türü

.NET Core ile 1.x DotnetCliTool paketi, Visual Studio paketinde yerleştirir `project.json` `tools` yerine düğüm `dependencies` düğümü.

Paket türlerinin ayarlanır `project.json`.

- `project.json`: Paket türü içinde göstermek bir `packOptions.packageType` json özelliği:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild hedeflerini ve özellik ekleme

*İlk olarak [.NET standart NuGet paketleri ile Visual Studio 2015 oluşturma](../guides/create-net-standard-packages-vs2015.md).*

Kullanırken `project.json`, hedef projeye eklenmez ancak kullanılabilir hale getirilir `project.lock.json`.

### <a name="package-versioning"></a>Paket sürümü oluşturma

*İlk olarak [Paket sürümü oluşturma](../reference/package-versioning.md).*

Kullanırken `project.json` biçimi, NuGet ayrıca bir joker karakter gösterimi kullanılmasını destekler \*büyük, küçük, düzeltme eki ve sayının yayın öncesi son bölümü için.

### <a name="nugetconfig-reference"></a>NuGet.Config reference

*İlk olarak [NuGet.Config başvuru](../reference/nuget-config-file.md).*

`globalPackagesFolder` yalnızca geçerli `project.json`. (Not eklendi: PackageReference için de geçerlidir.)

### <a name="nuspec-file-reference"></a>nuspec dosya başvurusu

*İlk olarak [nuspec başvuru](../reference/nuspec.md).*

`<contentFiles>` Öğe yerine kullanılır `<files>` ile `project.json`.

### <a name="package-manager-options-control"></a>Paket Yöneticisi seçenekleri denetimi

*İlk olarak [Paket Yöneticisi kullanıcı Arabirimi başvurusu](../tools/package-manager-ui.md).*

Kullanarak projeleri `project.json` yönetim biçimi zobrazit pouze **Show Önizleme penceresini** seçeneği.

### <a name="visual-studio-templates"></a>Visual Studio şablonları

*İlk olarak [Visual Studio şablonları NuGet paketlerinde](../visual-studio-extensibility/visual-studio-templates.md).*

En iyi uygulamalar: şablonlar içermez bir `project.json` dosya ve ekleme veya tüm başvuruları veya NuGet paketleri yüklendiğinde eklenir içeriği.