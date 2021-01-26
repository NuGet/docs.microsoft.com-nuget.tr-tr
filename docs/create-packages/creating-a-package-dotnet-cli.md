---
title: DotNet CLı kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 4771a30ee2ff73e68154d05f1c84efd90b584162
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774477"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="76dea-103">DotNet CLı kullanarak bir NuGet paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="76dea-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="76dea-104">Paketinizin ne yaptığını veya hangi kodu içerdiğini bağımsız olarak, `nuget.exe` Bu işlevselliği bir veya daha fazla `dotnet.exe` Geliştirici tarafından kullanılabilen bir bileşene paketlemek için ya da CLI araçlarından birini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="76dea-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="76dea-105">Bu makalede, DotNet CLı kullanarak bir paketin nasıl oluşturulacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="76dea-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="76dea-106">`dotnet`CLI 'yı yüklemek için bkz. [NuGet istemci araçları 'nı yükler](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="76dea-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="76dea-107">Visual Studio 2017 ' den başlayarak, DotNet CLı .NET Core iş yüklerine dahildir.</span><span class="sxs-lookup"><span data-stu-id="76dea-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="76dea-108">NuGet, .NET Core ve .NET Standard [SDK stili biçimini](../resources/check-project-format.md)kullanan projeler ve diğer SDK stilindeki projeler için, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak üzere kullanır.</span><span class="sxs-lookup"><span data-stu-id="76dea-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="76dea-109">Adım adım öğreticiler için bkz. [DotNet CLI ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) veya [Visual Studio Ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="76dea-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="76dea-110">`msbuild -t:pack` işlevine eşdeğerdir `dotnet pack` .</span><span class="sxs-lookup"><span data-stu-id="76dea-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="76dea-111">MSBuild ile derlemek için bkz. [MSBuild kullanarak NuGet paketi oluşturma](creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="76dea-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76dea-112">Bu konu, genellikle .NET Core ve .NET Standard projeleri [SDK stilindeki](../resources/check-project-format.md) projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="76dea-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="76dea-113">Özellikleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="76dea-113">Set properties</span></span>

<span data-ttu-id="76dea-114">Bir paket oluşturmak için aşağıdaki özellikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="76dea-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="76dea-115">`PackageId`, paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="76dea-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="76dea-116">Belirtilmemişse, varsayılan değer `AssemblyName` .</span><span class="sxs-lookup"><span data-stu-id="76dea-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="76dea-117">`Version`, *birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md)tanımlar.</span><span class="sxs-lookup"><span data-stu-id="76dea-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="76dea-118">Belirtilmemişse, varsayılan değer 1.0.0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="76dea-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="76dea-119">Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="76dea-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="76dea-120">`Authors`, yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="76dea-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="76dea-121">Belirtilmemişse, varsayılan değer `AssemblyName` .</span><span class="sxs-lookup"><span data-stu-id="76dea-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="76dea-122">`Company`, şirketinizin adı.</span><span class="sxs-lookup"><span data-stu-id="76dea-122">`Company`, your company name.</span></span> <span data-ttu-id="76dea-123">Belirtilmemişse, varsayılan değer `AssemblyName` .</span><span class="sxs-lookup"><span data-stu-id="76dea-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="76dea-124">Visual Studio 'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini ' de projeye sağ tıklayıp **Özellikler**' i seçin ve **paket** sekmesini seçin).</span><span class="sxs-lookup"><span data-stu-id="76dea-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="76dea-125">Bu özellikleri doğrudan proje dosyaları () içinde de ayarlayabilirsiniz `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="76dea-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="76dea-126">Pakete nuget.org genelinde benzersiz bir tanımlayıcı verin veya kullandığınız herhangi bir paket kaynağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="76dea-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="76dea-127">Aşağıdaki örnekte, bu özelliklerle birlikte basit ve tamamlanmış bir proje dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="76dea-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="76dea-128">(Komutunu kullanarak yeni bir varsayılan proje oluşturabilirsiniz `dotnet new classlib` .)</span><span class="sxs-lookup"><span data-stu-id="76dea-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="76dea-129">Ayrıca,, ve gibi isteğe bağlı özellikleri, `Title` `PackageDescription` `PackageTags` [MSBuild paketi hedefleri](../reference/msbuild-targets.md#pack-target)' nde açıklandığı gibi, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta verileri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties)de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76dea-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="76dea-130">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="76dea-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="76dea-131">Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. proje dosyaları ve [paket sürümü oluşturma](../concepts/package-versioning.md) [içindeki paket başvuruları](../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="76dea-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="76dea-132">Ayrıca, ve özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan gelen bir varlık için de mümkündür `<IncludeAssets>` `<ExcludeAssets>` .</span><span class="sxs-lookup"><span data-stu-id="76dea-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="76dea-133">Daha fazla bilgi için bkz. [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="76dea-133">For more information, see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="76dea-134">İsteğe bağlı açıklama alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="76dea-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="76dea-135">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="76dea-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="76dea-136">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="76dea-136">Run the pack command</span></span>

<span data-ttu-id="76dea-137">Projeden bir NuGet paketi (bir `.nupkg` dosya) oluşturmak için `dotnet pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="76dea-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="76dea-138">Çıktı, dosyanın yolunu gösterir `.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="76dea-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="76dea-139">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="76dea-139">Automatically generate package on build</span></span>

<span data-ttu-id="76dea-140">Çalıştırdığınızda otomatik olarak çalıştırmak için `dotnet pack` `dotnet build` , aşağıdaki satırı içindeki proje dosyanıza ekleyin `<PropertyGroup>` :</span><span class="sxs-lookup"><span data-stu-id="76dea-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="76dea-141">`dotnet pack`Bir çözümde çalıştırdığınızda bu, çözümdeki ( [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) özelliği olarak ayarlanır) Çözümdeki tüm projeleri paketler `true` .</span><span class="sxs-lookup"><span data-stu-id="76dea-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="76dea-142">Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.</span><span class="sxs-lookup"><span data-stu-id="76dea-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="76dea-143">Test paketi yüklemesi</span><span class="sxs-lookup"><span data-stu-id="76dea-143">Test package installation</span></span>

<span data-ttu-id="76dea-144">Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="76dea-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="76dea-145">Testler, gerekli dosyaların projenin doğru konumlarında bulunduğundan emin olmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="76dea-145">The tests make sure that the necessary files all end up in their correct places in the project.</span></span>

<span data-ttu-id="76dea-146">Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76dea-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76dea-147">Paketler sabittir.</span><span class="sxs-lookup"><span data-stu-id="76dea-147">Packages are immutable.</span></span> <span data-ttu-id="76dea-148">Bir sorunu düzeltseniz, yeniden test ettiğinizde, siz de [genel paketler](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) klasörünüzü kaldırana kadar paketin eski sürümünü kullanmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="76dea-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="76dea-149">Bu, özellikle her derlemede benzersiz bir ön sürüm etiketi kullanmayan paketleri test ederken ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="76dea-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76dea-150">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="76dea-150">Next Steps</span></span>

<span data-ttu-id="76dea-151">Bir dosya olan bir paket oluşturduktan sonra `.nupkg` , bir [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76dea-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="76dea-152">Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76dea-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="76dea-153">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="76dea-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="76dea-154">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="76dea-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="76dea-155">Paket simgesi ekleme</span><span class="sxs-lookup"><span data-stu-id="76dea-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="76dea-156">Kaynak ve yapılandırma dosyalarının dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="76dea-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="76dea-157">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="76dea-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="76dea-158">Yayın öncesi sürümler</span><span class="sxs-lookup"><span data-stu-id="76dea-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="76dea-159">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="76dea-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="76dea-160">COM birlikte çalışma Derlemeleriyle paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="76dea-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="76dea-161">Son olarak, bilmeniz için ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="76dea-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="76dea-162">Yerel paketler</span><span class="sxs-lookup"><span data-stu-id="76dea-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="76dea-163">Sembol paketleri</span><span class="sxs-lookup"><span data-stu-id="76dea-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
