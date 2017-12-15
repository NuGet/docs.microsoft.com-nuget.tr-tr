---
title: "Visual Studio proje dosyalarına NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet PackageReference NuGet 4.0 + ve VS2017 tarafından desteklenen gibi proje dosyalarına ayrıntıları"
keywords: "NuGet Paket bağımlılıklarını, paket referanslarını proje dosyalarını, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarına paket referanslarını (PackageReference)

Paketini kullanarak başvurular `PackageReference` düğümü, ayrı bir gerek yerine NuGet bağımlılıkları doğrudan proje dosyalarını yönetmenize olanak `packages.config` veya `project.json` dosyası. Bu yöntem, NuGet diğer yönlerini etkilemez; Örneğin, ayarlarında `NuGet.Config` açıklandığı gibi dosyaları (paket kaynaklarını dahil) uygulanan hala [NuGet davranışını yapılandırma](Configuring-NuGet-Behavior.md).

> [!Important]
> Şu anda paket referanslarını Visual Studio 2017 içinde yalnızca, .NET Core projeleri, .NET standart projeleri ve Windows 10 derleme 15063 (oluşturucuları güncelleştirme) hedefleme UWP projeleri için desteklenir.

`PackageReference` Yaklaşım paket referanslarını hedef framework, yapılandırma, platform veya diğer gruplandırmaları başına seçmek için MSBuild koşulları kullanmanıza olanak verir. Bu da bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar. Davranış açısından ve [bağımlılık çözümlemesi](Dependency-Resolution.md), kullanarak aynı olan `project.json`.

MSBuild proje dosyalarına paket referanslarını tümleştirilmesi hakkında daha fazla bilgi için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md).

## <a name="adding-a-packagereference"></a>Bir PackageReference ekleme

Bir bağımlılık aşağıdaki sözdizimini kullanarak, proje dosyasında ekleyin:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Bağımlılık sürümünü denetleme

Bir paketin sürümü belirtmek için aynı kullanırken kuraldır `packages.config` veya `project.json`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir. > açıklandığı gibi en düşük sürüm tercihini ile 3.6.0 = [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="floating-versions"></a>Kayan sürümleri

[Sürümleri kayan](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıklar denetleme

Bir bağımlılık tamamen geliştirme bandı kullanıyor olabilir ve paketinizi tüketir projelerine kullanıma istemeyebilirsiniz. Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışı denetlemek için meta verileri.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Aşağıdaki meta veri etiketlerini bağımlılık varlıklar kontrol edin:

| Etiket | Açıklama | Varsayılan Değer |
| --- | --- | --- |
| IncludeAssets | Bu varlıklar kullanılır | tüm |
| ExcludeAssets | Bu varlıklar tüketilen değil | yok | 
| PrivateAssets | Bu varlıklar kullanılır, ancak üst projeye akış olmaz | Content dosyaları, çözümleyiciler; derleme |


Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değerlerle `all` ve `none` gerekir göründüğü tek başına:

| Değer | Açıklama |
| --- | ---
| Derleme | İçeriği `lib` klasörü |
| çalışma zamanı | İçeriği `runtime` klasörü |
| Content dosyaları | İçeriği `contentfiles` klasörü |
| derleme | Özellik ve içinde hedefler `build` klasörü |
| Çözümleyiciler | .NET çözümleyiciler |
| yerel | İçeriği `native` klasörü |
| yok | Yukarıdakilerin hiçbiri kullanılır. |
| tüm | Yukarıdakilerin tümü (dışında `none`) |

Aşağıdaki örnekte, paket içerik dosyalarını dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Çünkü unutmayın `build` ile dahil edilmeyen `PrivateAssets`, hedefleri ve özellik *olacak* üst projeye akış. Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi derlemeler bir projede kullanıldığını değerlendirin. Hedefleri ve özellik gelen AppLogger tüketebileceği `Contoso.Utility.UsefulStuff`AppLogger tüketen projelerini gibi.

## <a name="adding-a-packagereference-condition"></a>PackageReference koşul ekleme

Koşullar herhangi bir MSBuild değişkeni kullanabilirsiniz veya bir değişkeni hedefler ya da özellik dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz. Ancak, şu anda yalnızca `TargetFramework` değişkeni desteklenir.

Örneğin, hedefleme deyin `netstandard1.4` yanı `net452` ancak yalnızca için geçerli bir bağımlılığı olan `net452`. Bu durumda istemediğiniz bir `netstandard1.4` gereksiz bu bağımlılığı eklemek için paket tüketen projesi. Bunu önlemek için bir koşul üzerinde belirttiğiniz `PackageReference` gibi:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulmuş bir paketin Newtonsoft.json yalnızca için bağımlılık olarak dahil olduğunu göstermek bir `net452` hedef:

![Bir koşul VS2017 ile PackageReference üzerinde uygulamanın sonucu](media/PackageReference-Condition.png)

Koşullar da uygulanabilir adresindeki `ItemGroup` düzey ve tüm alt öğelerine uygulanır `PackageReference` öğeleri:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
