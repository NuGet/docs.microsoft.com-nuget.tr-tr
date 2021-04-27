---
title: NuGet paket türü ayarla
description: Bir paketin amaçlanan kullanımını göstermek için paket türlerini açıklar.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067289"
---
# <a name="set-a-nuget-package-type"></a>NuGet paket türü ayarla

Paketler, amaçlanan kullanımını göstermek için bir veya daha fazla *paket türüyle* işaretlenebilir.

## <a name="known-package-types"></a>Bilinen paket türleri

- `Dependency` tür paketleri kitaplıklara ve uygulamalarına derleme veya çalışma zamanı varlıkları ekleyin ve herhangi bir proje türüne (uyumlu oldukları varsayılarak) yüklenebilir.

- `DotnetTool` tür paketleri, [DotNet CLI](/dotnet/articles/core/tools/index)tarafından yüklenebilen .net araçlardır.

- `Template` tür paketleri, bir uygulama, hizmet, araç veya sınıf kitaplığı gibi dosyalar ya da projeler oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.

Daha önceki NuGet sürümleriyle oluşturulan tüm paketler de dahil olmak üzere bir tür ile işaretlenmemiş paketler, varsayılan olarak `Dependency` türü.

> [!NOTE]
> NuGet 3,5 ' ye paket türleri için destek eklenmiştir.
> Özel bir paket türüne ihtiyacınız yoksa, paket türünün açıkça *ayarlanmamanız* en iyisidir.
> Tür belirtilmediğinde NuGet varsayılan olarak `Dependency` türe ayarlanır.

## <a name="custom-package-types"></a>Özel paket türleri

Kendi kullanımı [bilinen paket türlerine](#known-package-types)uygun değilse, paketinize bir veya daha fazla özel paket türüyle işaret edebilirsiniz.

Örneğin, `Contoso` uygulamanın müşterilerinin uzantıları yükleyebileceklerini düşünün. Uygulama, `ContosoExtension` paketleri gerekli kuralları izleyen uygun uzantılar olarak tanımlamak için uzantı yazarlarının özel paket türünü kullanmasını gerektirebilir.

> [!WARNING]
> Özel bir paket türüne sahip bir paket, Visual Studio veya nuget.exe tarafından yüklenemez. Daha fazla bilgi için bkz. [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) .

# <a name="using-dotnet-cli"></a>[DotNet CLı kullanma](#tab/dotnet)

Paket türleri proje dosyasında ( `.csproj` ) ayarlanabilir:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Birden çok amaçlanan kullanımları olan paketler, sınırlayıcı kullanılarak birden çok paket türüyle işaretlenebilir `;` :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Paket türleri `,` , paket türü ve dizesi arasında bir sınırlayıcı kullanılarak sürümlenebilir [`Version`](/dotnet/api/system.version) :

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[nuget.exekullanma ](#tab/nugetexe)

Paket türleri, `.nuspec` öğesinin altındaki bir düğüm içindeki dosyada ayarlanır `packageTypes\packageType` `<metadata>` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

Birden çok amaçlanan kullanımları olan paketler birden çok paket türüyle işaretlenebilir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

Paket türleri bir dize kullanılarak sürümlenebilir [`Version`](/dotnet/api/system.version) :

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

Bir paket türü dizesinin biçimi tam olarak bir paket KIMLIĞI gibidir. Diğer bir deyişle, bir paket türü, en `^\w+([_.-]\w+)*$` az bir karakter ve en fazla 100 karakter içeren normal ifadeyle eşleşen büyük/küçük harf duyarsız bir dizedir.

Sağlanmışsa, paket türü sürümü bir [`Version`](/dotnet/api/system.version) dizedir. Paket türü sürümü isteğe bağlıdır ve varsayılan olarak ayarlanır `0.0` .
