---
title: NuGet Packagereference'a biçimi (proje dosyalarında paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen proje dosyalarında NuGet PackageReference hakkında ayrıntılar
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 48930701f1bb5f13718505b85b293f38d37d19fb
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508354"
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarında paket başvuruları (PackageReference)

Paket başvuruları kullanılarak, `PackageReference` düğümü, NuGet bağımlılıklarını doğrudan proje dosyaları içinde yönetme (ayrı bir aksine `packages.config` dosya). PackageReference, kullanarak çağrılır, NuGet diğer yönleri etkilemez; Örneğin, ayarlarında `NuGet.Config` (paket kaynaklarını dahil) dosyaları yine de açıklandığı gibi uygulanan [NuGet davranışını yapılandırma](configuring-nuget-behavior.md).

PackageReference ile paket başvuruları her hedef çerçeve, yapılandırma, platform veya diğer grupları seçmek için MSBuild koşulları kullanabilirsiniz. Ayrıca bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar. (Daha fazla ayrıntı için [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md).)

Varsayılan olarak, .NET Core projeleri, .NET Standard projelerine ve Windows 10 derleme 15063 (Creators Update) hedefleyen UWP projeleri için ve sonraki sürümlerinde, C++ UWP projeleri hariç PackageReference kullanılır. .NET Framework'ün tamamını projeleri PackageReference destekler, ancak şu anda varsayılan `packages.config`. PackageReference kullanmak için bağımlılıklardan geçirme `packages.config` proje dosyanıza ardından packages.config kaldırın.

## <a name="adding-a-packagereference"></a>PackageReference ekleme

Bir bağımlılık aşağıdaki sözdizimini kullanarak proje dosyanıza ekleyin:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Bağımlılık sürümünü denetleme

Bir paketin sürümü belirtmek için kural aynı kullanıldığında `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir > üzerinde açıklandığı 3.6.0 tercih en düşük sürümü ile = [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Hiçbir packagereferences'ı içeren bir proje için PackageReference kullanma
Gelişmiş: sahip paket yüklü bir projede (proje dosyasında hiçbir PackageReferences) ve hiçbir packages.config dosyası yok, ancak stili Packagereference'a geri yüklenmesini istediğiniz projesinin, proje özelliği RestoreProjectStyle Packagereference'a ayarlayabileceğiniz içinde Proje dosyanız.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
(Mevcut csproj veya SDK stili projeleri) stili Packagereference'a olan projeleri başvuruyorsa yararlı olabilir. Bu projelerdeki "geçişli" projeniz tarafından başvurulabilmesi için başvuran paketleri olanak sağlar.

## <a name="floating-versions"></a>Kayan sürümleri

[Kayan sürümleri](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıkları denetleme

Bir bağımlılık yalnızca bir geliştirme bandı kullanabilecek ve, paketiniz tüketecektir projeler için kullanıma sunmak istemeyebilirsiniz. Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışını denetlemek için meta verileri.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Şu meta veri etiketleri bağımlılık varlıklar kontrol edin:

| Etiket | Açıklama | Varsayılan Değer |
| --- | --- | --- |
| IncludeAssets | Bu varlıklar tarafından kullanılabilir | tüm |
| ExcludeAssets | Bu varlıklar tüketilir değil | yok |
| PrivateAssets | Bu varlıklar tarafından kullanılabilir ancak üst projeye akış olmaz | contentfiles, çözümleyiciler; derleme |

Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değer ile `all` ve `none` gerekir göründüğü başlarına:

| Değer | Açıklama |
| --- | ---
| Derleme | İçeriğini `lib` klasörü ve denetimleri klasördeki derlemelere karşı olup projenizi derleyin |
| çalışma zamanı | İçeriğini `lib` ve `runtimes` klasörü ve denetimleri bu derlemeler için derleme olup kopyalanacak çıktı dizini |
| contentFiles | İçeriğini `contentfiles` klasörü |
| derleme | Özellikler ve hedeflediğini `build` klasörü |
| Çözümleyiciler | .NET çözümleyiciler |
| yerel | İçeriğini `native` klasörü |
| yok | Yukarıdakilerin hiçbiri kullanılır. |
| tüm | Yukarıdakilerin tümü (dışında `none`) |

Aşağıdaki örnekte, içerik dosyalarını paketinden dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.

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

Dikkat edin çünkü `build` ile bulunmaz `PrivateAssets`, hedeflerini ve özellik *olur* üst projeye akış. Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi oluşturan bir projesinde kullanıldığını düşünün. AppLogger hedeflerini ve özellik gelen kullanabileceği `Contoso.Utility.UsefulStuff`, AppLogger kullanan projeler gibi.

## <a name="adding-a-packagereference-condition"></a>PackageReference koşul ekleme

Koşullar herhangi bir MSBuild değişken kullanabilirsiniz veya bir değişkeni hedefler ya da Özellikler dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz. Ancak, şu anda, yalnızca `TargetFramework` değişkeni desteklenir.

Örneğin, hedefleyen düşünelim `netstandard1.4` yanı `net452` ancak yalnızca için geçerli olan bir bağımlılığa sahip `net452`. Bu durumda istemediğiniz bir `netstandard1.4` paketiniz, gereksiz bağımlılık eklemek için kullanan bir proje. Bunu önlemek için bir koşul belirttiğiniz `PackageReference` gibi:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulan bir paket Newtonsoft.Json yalnızca bağımlılık olarak dahil olduğunu gösterir bir `net452` hedef:

![Bir koşul ile VS2017 PackageReference üzerinde sonucu](media/PackageReference-Condition.png)

Koşul da uygulanabilir `ItemGroup` düzeyi ve tüm alt öğelere uygulanacak `PackageReference` öğeleri:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
