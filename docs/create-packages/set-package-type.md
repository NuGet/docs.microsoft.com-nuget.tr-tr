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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="89c52-103">NuGet paket türü ayarla</span><span class="sxs-lookup"><span data-stu-id="89c52-103">Set a NuGet package type</span></span>

<span data-ttu-id="89c52-104">Paketler, amaçlanan kullanımını göstermek için bir veya daha fazla *paket türüyle* işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="89c52-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="89c52-105">Bilinen paket türleri</span><span class="sxs-lookup"><span data-stu-id="89c52-105">Known package types</span></span>

- <span data-ttu-id="89c52-106">`Dependency` tür paketleri kitaplıklara ve uygulamalarına derleme veya çalışma zamanı varlıkları ekleyin ve herhangi bir proje türüne (uyumlu oldukları varsayılarak) yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="89c52-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="89c52-107">`DotnetTool` tür paketleri, [DotNet CLI](/dotnet/articles/core/tools/index)tarafından yüklenebilen .net araçlardır.</span><span class="sxs-lookup"><span data-stu-id="89c52-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="89c52-108">`Template` tür paketleri, bir uygulama, hizmet, araç veya sınıf kitaplığı gibi dosyalar ya da projeler oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.</span><span class="sxs-lookup"><span data-stu-id="89c52-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="89c52-109">Daha önceki NuGet sürümleriyle oluşturulan tüm paketler de dahil olmak üzere bir tür ile işaretlenmemiş paketler, varsayılan olarak `Dependency` türü.</span><span class="sxs-lookup"><span data-stu-id="89c52-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="89c52-110">NuGet 3,5 ' ye paket türleri için destek eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="89c52-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="89c52-111">Özel bir paket türüne ihtiyacınız yoksa, paket türünün açıkça *ayarlanmamanız* en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="89c52-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="89c52-112">Tür belirtilmediğinde NuGet varsayılan olarak `Dependency` türe ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="89c52-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="89c52-113">Özel paket türleri</span><span class="sxs-lookup"><span data-stu-id="89c52-113">Custom package types</span></span>

<span data-ttu-id="89c52-114">Kendi kullanımı [bilinen paket türlerine](#known-package-types)uygun değilse, paketinize bir veya daha fazla özel paket türüyle işaret edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89c52-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="89c52-115">Örneğin, `Contoso` uygulamanın müşterilerinin uzantıları yükleyebileceklerini düşünün.</span><span class="sxs-lookup"><span data-stu-id="89c52-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="89c52-116">Uygulama, `ContosoExtension` paketleri gerekli kuralları izleyen uygun uzantılar olarak tanımlamak için uzantı yazarlarının özel paket türünü kullanmasını gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="89c52-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="89c52-117">Özel bir paket türüne sahip bir paket, Visual Studio veya nuget.exe tarafından yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="89c52-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="89c52-118">Daha fazla bilgi için bkz. [NuGet/Home # 10468](https://github.com/NuGet/Home/issues/10468) .</span><span class="sxs-lookup"><span data-stu-id="89c52-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="89c52-119">DotNet CLı kullanma</span><span class="sxs-lookup"><span data-stu-id="89c52-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="89c52-120">Paket türleri proje dosyasında ( `.csproj` ) ayarlanabilir:</span><span class="sxs-lookup"><span data-stu-id="89c52-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="89c52-121">Birden çok amaçlanan kullanımları olan paketler, sınırlayıcı kullanılarak birden çok paket türüyle işaretlenebilir `;` :</span><span class="sxs-lookup"><span data-stu-id="89c52-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="89c52-122">Paket türleri `,` , paket türü ve dizesi arasında bir sınırlayıcı kullanılarak sürümlenebilir [`Version`](/dotnet/api/system.version) :</span><span class="sxs-lookup"><span data-stu-id="89c52-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="89c52-123">nuget.exekullanma </span><span class="sxs-lookup"><span data-stu-id="89c52-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="89c52-124">Paket türleri, `.nuspec` öğesinin altındaki bir düğüm içindeki dosyada ayarlanır `packageTypes\packageType` `<metadata>` :</span><span class="sxs-lookup"><span data-stu-id="89c52-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

<span data-ttu-id="89c52-125">Birden çok amaçlanan kullanımları olan paketler birden çok paket türüyle işaretlenebilir:</span><span class="sxs-lookup"><span data-stu-id="89c52-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

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

<span data-ttu-id="89c52-126">Paket türleri bir dize kullanılarak sürümlenebilir [`Version`](/dotnet/api/system.version) :</span><span class="sxs-lookup"><span data-stu-id="89c52-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

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

<span data-ttu-id="89c52-127">Bir paket türü dizesinin biçimi tam olarak bir paket KIMLIĞI gibidir.</span><span class="sxs-lookup"><span data-stu-id="89c52-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="89c52-128">Diğer bir deyişle, bir paket türü, en `^\w+([_.-]\w+)*$` az bir karakter ve en fazla 100 karakter içeren normal ifadeyle eşleşen büyük/küçük harf duyarsız bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="89c52-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="89c52-129">Sağlanmışsa, paket türü sürümü bir [`Version`](/dotnet/api/system.version) dizedir.</span><span class="sxs-lookup"><span data-stu-id="89c52-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="89c52-130">Paket türü sürümü isteğe bağlıdır ve varsayılan olarak ayarlanır `0.0` .</span><span class="sxs-lookup"><span data-stu-id="89c52-130">The package type version is optional and defaults to `0.0`.</span></span>
