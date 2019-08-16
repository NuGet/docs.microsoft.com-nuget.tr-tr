---
title: NuGet projesi. JSON Arşivi içeriği
description: Çeşitli proje. JSON içeriği NuGet belgelerinin diğer alanlarından kaldırılmıştır.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 87116669c1e685ffd0dbe4142c2f7e357c413497
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488253"
---
# <a name="projectjson-archive"></a>Project. JSON Arşivi

`project.json` Yönetim biçimi NuGet 3. x ile tanıtılmıştır ve belirli proje türleri için kullanılır. Bağımlılıklar doğrudan bir proje dosyasında listelendiğinde, PackageReference biçiminin sunumundan kullanım dışı bırakılmıştır.

Ayrıca bkz.:

- [Project. JSON şeması](project-json.md)
- [paket yazarları üzerinde Project. JSON etkisi](project-json-impact.md)
- [project.json ve UWP](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a>project.json yönetim biçimi

*[Paket geri yükleme](../what-is-nuget.md)' de başlangıçta.*

Yönetim biçimleri listesinde:

- [`project.json`](project-json.md): *(kullanım dışı)* proje bağımlılıklarının bir listesini, `project.lock.json`ilişkili bir dosyadaki genel bir paket Graf ile koruyan bir JSON dosyası. Bu biçim, PackageReference 'ın yararına kullanım dışı bırakılmıştır.

## <a name="nuget-restore-on-mono"></a>Mono 'da NuGet geri yükleme

*Başlangıçta [NuGet istemci araçları 'Nı yükler](../install-nuget-client-tools.md).*

İle birlikte `project.json`kullanılır.

## <a name="constraining-package-versions-with-restore"></a>Paket sürümlerini restore ile kısıtlama

*[Paket geri yükleme](../consume-packages/package-restore.md#constrain-package-versions-with-restore)' de başlangıçta.*

- `project.json`: Bağımlılık sürüm numarasıyla doğrudan bir sürüm aralığı belirtin. Örneğin:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a>NuGet CLı komutları

- `nuget install`ile `project.json`çalışmaz.
- `nuget restore`: kullanan `project.json`projelerle, gerekirse bir `project.lock.json` dosya ve `<project>.nuget.props` dosya oluşturur. (Her iki dosya da kaynak denetiminden atlanabilir.) Bağımsız değişkeni bir `project.json` dosyayı işaret edebilir ve bir `packages.config` veya proje dosyasına işaret eden aynı davranışa sahiptir. `<projectPath>` Paket klasörlerinin öncelik sırasına göre, `%userprofile%\.nuget\packages` kullanılırken `project.json`ilk olarak aranır.
- `nuget update`: Mono 'da, bu komut kullanılarak `project.json`projelerle çalışmaz.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference ile bağımlılık çözümlemesi

*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference).*

PackageReference davranışı için `project.json`de geçerlidir. NuGet geri yükleme, bağımlılık grafiğini, adlı `project.lock.json` `project.json`bir dosyaya yazar.

## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#managing-dependency-assets).*

`project.json` Biçimini kullanırken, hangi varlıkların bağımlılıklardan en üst düzey projeye akabildiğini denetleyebilirsiniz. Ayrıntılar için bkz. [Project. JSON](project-json.md).

## <a name="excluding-references"></a>Başvuruları dışlama

*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#excluding-references).*

- `project.json`: PackageC `"exclude" : "all"` için bağımlılığa ekleyin:

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

*İlk olarak [bağımlılık çözünürlüğünde](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).*

Hatanın çözümlenme yöntemi:

- **Önerilmez**: paket yazarıyla `netcore` `netstandard`çalışırken geçici bir çözüm olarak,,, ve diğer çerçeveleri uyumlu olarak belirtebilir ve `netcoreapp` bu sayede, bu diğer çerçeveleri hedefleyen paketlere izin verebilir kullanılacak çerçeveler. Bkz. [Project. JSON içeri aktarmaları](project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback). Bu, beklenmeyen davranışlara neden olabilir, bu nedenle bir güncelleştirmede paket yazarıyla çalışarak paket uyumsuzluklarını çözmeniz en iyisidir.

## <a name="target-frameworks"></a>Hedef çerçeveler

*Başlangıçta [hedef çerçeveler](../reference/target-frameworks.md).*

- [Project. JSON](project-json.md): `frameworks` Düğüm, projenin derlenebilecek çerçeve sürümlerini belirtir.

## <a name="creating-a-package"></a>Paket oluşturma

*Başlangıçta [paket oluşturma](../create-packages/creating-a-package.md)*

### <a name="setting-a-package-type"></a>Paket türünü ayarlama

.NET Core 1. x ile bir dotnetclientool paketi yüklendiğinde, Visual Studio paketi `project.json` `tools` `dependencies` düğüm yerine düğümüne koyar.

Paket türleri içinde `project.json`ayarlanır.

- `project.json`: Paket türünü JSON `packOptions.packageType` özelliği içinde belirtin:

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild için hedef ve özellik ekleme

*İlk olarak [Visual Studio 2015 ile .NET Standard NuGet paketleri oluşturun](../guides/create-net-standard-packages-vs2015.md).*

Kullanırken `project.json`, hedefler projeye eklenmez, `project.lock.json`ancak aracılığıyla kullanılabilir hale getirilir.

### <a name="package-versioning"></a>Paket sürümü oluşturma

*[Paket sürümü oluşturma](../concepts/package-versioning.md)' da başlangıçta.*

`project.json` Biçim kullanılırken, NuGet Ayrıca sayının büyük, küçük, yama ve yayın \*öncesi sonek bölümlerinin bir joker karakter gösterimini kullanmayı da destekler.

### <a name="nugetconfig-reference"></a>NuGet. config başvurusu

*İlk olarak [NuGet. config başvurusu](../reference/nuget-config-file.md).*

`globalPackagesFolder`yalnızca için `project.json`geçerlidir. (Eklenen Note: PackageReference için de geçerlidir.)

### <a name="nuspec-file-reference"></a>nuspec dosya başvurusu

*[Nuspec başvurusunda](../reference/nuspec.md)başlangıçta.*

`<contentFiles>` Öğesi`<files>` yerine`project.json`kullanılır.

### <a name="package-manager-options-control"></a>Paket Yöneticisi seçenekler denetimi

*[Paket Yöneticisi Kullanıcı arabirimi başvurusunda](../consume-packages/install-use-packages-visual-studio.md)başlangıçta.*

Yönetim biçimi `project.json` kullanan projeler yalnızca **Önizlemeyi göster pencere** seçeneğini gösterir.

### <a name="visual-studio-templates"></a>Visual Studio şablonları

*İlk olarak [Visual Studio şablonlarındaki NuGet paketlerinde](../visual-studio-extensibility/visual-studio-templates.md).*

En iyi Yöntemler: Şablonlar bir `project.json` dosya içermez ve NuGet paketleri yüklendiğinde eklenecek başvuruları ya da içeriği içermez.