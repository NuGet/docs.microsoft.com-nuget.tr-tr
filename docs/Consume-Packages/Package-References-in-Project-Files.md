---
title: NuGet PackageReference biçimi (proje dosyalarına paket referanslarını) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet PackageReference NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi proje dosyalarına ayrıntıları
keywords: NuGet Paket bağımlılıklarını, paket referanslarını proje dosyalarını, PackageReference, packages.config VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarına paket referanslarını (PackageReference)

Paketini kullanarak başvurular `PackageReference` düğümü, NuGet bağımlılıkları doğrudan proje dosyalarını Yönet (ayrı bir aksine `packages.config` dosyası). Denir, PackageReference, kullanarak NuGet diğer yönlerini etkilemez; Örneğin, ayarlarında `NuGet.Config` açıklandığı gibi dosyaları (paket kaynaklarını dahil) uygulanan hala [NuGet davranışını yapılandırma](configuring-nuget-behavior.md).

PackageReference ile hedef framework, yapılandırma, platform veya diğer gruplandırmaları başına paket referanslarını seçmek için MSBuild koşulları kullanabilirsiniz. Bu da bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar. (Daha fazla ayrıntı için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)

Varsayılan olarak, PackageReference .NET Core projeleri, .NET standart projeler ve Windows 10 derleme 15063 (oluşturucuları güncelleştirme) hedefleme UWP projeleri için ve daha sonra C++ UWP projeleri hariç olmak üzere kullanılır. .NET framework tam projeleri PackageReference destekler, ancak şu anda varsayılan olarak `packages.config`. PackageReference kullanmak için bağımlılıklardan geçirmek `packages.config` proje dosyanıza ardından packages.config kaldırın.

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

Bir paketin sürümü belirtmek için aynı kullanırken kuraldır `packages.config`:

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
| çalışma zamanı | İçeriği `runtimes` klasörü |
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
