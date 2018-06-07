---
title: NuGet PackageReference biçimi (proje dosyalarına paket referanslarını)
description: NuGet PackageReference NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen gibi proje dosyalarına ayrıntıları
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817677"
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

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Hiçbir PackageReferences sahip bir proje için PackageReference kullanma
Gelişmiş: (PackageReferences proje dosyasında) ve hiçbir packages.config dosyasına projede yüklü hiç paket var ancak PackageReference stil olarak geri yüklenmesini istediğiniz projesinin proje özelliği RestoreProjectStyle PackageReference için ayarlayabileceğiniz içinde Proje dosyanızı.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
(Mevcut csproj veya SDK stili projeleri) stilde PackageReference olan projeler başvuru durumlarda yararlı olabilir. Bu, bu proje için "geçişli" projeniz tarafından başvuruda başvurmak paketleri olanak tanır.

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
| Derleme | İçeriği `lib` klasörü ve denetimleri klasördeki derlemeleri karşı olup projenizi derleme |
| çalışma zamanı | İçeriği `lib` ve `runtimes` klasörü ve denetimleri bu derlemeler için yapı olup kopyalanacak çıktı dizini |
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
