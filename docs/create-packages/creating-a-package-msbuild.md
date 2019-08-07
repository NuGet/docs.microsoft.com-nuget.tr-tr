---
title: MSBuild kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8512b7b214db45fb2a4db742287270cb86054b7c
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68818082"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="05c1e-103">MSBuild kullanarak bir NuGet paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="05c1e-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="05c1e-104">Paketinizin ne olduğu veya hangi kodun içerdiği, bu işlevselliği herhangi bir sayıda başka geliştirici tarafından paylaşılabilecek ve kullanılabilecek bir bileşene göre paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-104">No matter what your package does or what code it contains, you need to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="05c1e-105">Bu makalede, MSBuild kullanarak bir paketin nasıl oluşturulacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="05c1e-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="05c1e-106">MSBuild 'i kullanmak için önce `dotnet` CLI 'yı, bkz. [NuGet istemci araçları 'nı yükler](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="05c1e-106">To use MSBuild, first install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="05c1e-107">Visual Studio 2017 ' den başlayarak, DotNet CLı .NET Core iş yüklerine dahildir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="05c1e-108">NuGet, .NET Core ve .NET Standard [SDK stili biçimini](../resources/check-project-format.md)kullanan projeler ve diğer SDK stilindeki projeler için, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak üzere kullanır.</span><span class="sxs-lookup"><span data-stu-id="05c1e-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="05c1e-109">Tarafından kullanılan `<PackageReference>`SDK olmayan bir proje için MSBuild (`msbuild /t:pack`) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-109">For a non-SDK-style project that uses `<PackageReference>`, you can also use MSBuild (`msbuild /t:pack`).</span></span>

<span data-ttu-id="05c1e-110">MSBuild ile derlemek için, proje bağımlılıklarına NuGet. Build. Tasks. Pack paketini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-110">To build with MSBuild, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="05c1e-111">MSBuild paketi hedefleri hakkında ayrıntılı bilgi için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="05c1e-111">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="05c1e-112">`msbuild -t:pack`işlevine eşdeğerdir `dotnet pack`.</span><span class="sxs-lookup"><span data-stu-id="05c1e-112">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="05c1e-113">Bunun yerine `dotnet` CLI kullanarak adım adım öğreticiler için bkz. [DotNet CLI ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="05c1e-113">For step-by-step tutorials using the `dotnet` CLI instead, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05c1e-114">Bu konu, genellikle .NET Core ve .NET Standard projeleri [SDK stilindeki](../resources/check-project-format.md) projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="05c1e-115">Özellikleri ayarla</span><span class="sxs-lookup"><span data-stu-id="05c1e-115">Set properties</span></span>

<span data-ttu-id="05c1e-116">Bir paket oluşturmak için aşağıdaki özellikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="05c1e-117">`PackageId`, paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="05c1e-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="05c1e-118">Belirtilmemişse, varsayılan değer `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="05c1e-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="05c1e-119">`Version`, *birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md)tanımlar.</span><span class="sxs-lookup"><span data-stu-id="05c1e-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="05c1e-120">Belirtilmemişse, varsayılan değer 1.0.0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="05c1e-121">Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="05c1e-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="05c1e-122">`Authors`, yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="05c1e-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="05c1e-123">Belirtilmemişse, varsayılan değer `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="05c1e-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="05c1e-124">`Company`, şirketinizin adı.</span><span class="sxs-lookup"><span data-stu-id="05c1e-124">`Company`, your company name.</span></span> <span data-ttu-id="05c1e-125">Belirtilmemişse, varsayılan değer `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="05c1e-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="05c1e-126">Visual Studio 'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini ' de projeye sağ tıklayıp **Özellikler**' i seçin ve **paket** sekmesini seçin).</span><span class="sxs-lookup"><span data-stu-id="05c1e-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="05c1e-127">Bu özellikleri doğrudan proje dosyaları (`.csproj`) içinde de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-127">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="05c1e-128">Pakete nuget.org genelinde benzersiz bir tanımlayıcı verin veya kullandığınız herhangi bir paket kaynağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="05c1e-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="05c1e-129">Aşağıdaki örnekte, bu özelliklerle birlikte basit ve tamamlanmış bir proje dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-129">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="05c1e-130">Ayrıca,, ve `Title` `PackageDescription` `PackageTags`gibi isteğe bağlı özellikleri, [MSBuild paketi hedefleri](../reference/msbuild-targets.md#pack-target)' nde açıklandığı gibi, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta verileri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties)de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="05c1e-131">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="05c1e-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="05c1e-132">Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. [paket sürümü oluşturma](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="05c1e-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="05c1e-133">Ayrıca, `<IncludeAssets>` ve `<ExcludeAssets>` özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan gelen bir varlık için de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="05c1e-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="05c1e-134">Daha fazla bilgi için, [bağımlılık varlıklarını denetleyen](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)seee.</span><span class="sxs-lookup"><span data-stu-id="05c1e-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="05c1e-135">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="05c1e-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="05c1e-136">NuGet. Build. Tasks. Pack paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="05c1e-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="05c1e-137">MSBuild 'i kullanmak için, projenize NuGet. Build. Tasks. Pack paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="05c1e-137">To use MSBuild, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="05c1e-138">Proje dosyasını açın ve `<PropertyGroup>` öğesinden sonra aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="05c1e-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="05c1e-139">Bir geliştirici komut istemi açın ( **arama** kutusunda, **Geliştirici komut istemi**yazın).</span><span class="sxs-lookup"><span data-stu-id="05c1e-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

3. <span data-ttu-id="05c1e-140">Proje dosyasını içeren klasöre geçin ve NuGet. Build. Tasks. Pack paketini yüklemek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="05c1e-140">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="05c1e-141">MSBuild çıkışının, derlenmesinin başarıyla tamamlandığını gösteriyor olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="05c1e-141">Make sure that the MSBuild output indicates that the built completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="05c1e-142">MSBuild-t:Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="05c1e-142">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="05c1e-143">Projeden bir NuGet paketi (bir `.nupkg` dosya) oluşturmak için `msbuild -t:pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="05c1e-143">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="05c1e-144">Geliştirici komut isteminde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="05c1e-144">In the Developer command prompt, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="05c1e-145">Çıktı, `.nupkg` dosyanın yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-145">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).


Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="05c1e-146">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="05c1e-146">Automatically generate package on build</span></span>

<span data-ttu-id="05c1e-147">Projeyi derlediğinizde veya `msbuild -t:pack` geri yüklerken otomatik olarak çalıştırmak için aşağıdaki satırı proje `<PropertyGroup>`dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="05c1e-147">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="05c1e-148">Bir çözümde çalıştırdığınızda `msbuild -t:pack` , bu, çözümde bulunan ve packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) özellik olarak `true`ayarlanır) tüm projeleri paketler.</span><span class="sxs-lookup"><span data-stu-id="05c1e-148">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="05c1e-149">Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.</span><span class="sxs-lookup"><span data-stu-id="05c1e-149">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="05c1e-150">Test paketi yüklemesi</span><span class="sxs-lookup"><span data-stu-id="05c1e-150">Test package installation</span></span>

<span data-ttu-id="05c1e-151">Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-151">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="05c1e-152">Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="05c1e-152">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="05c1e-153">Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-153">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05c1e-154">Paketler sabittir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-154">Packages are immutable.</span></span> <span data-ttu-id="05c1e-155">Bir sorunu düzeltseniz, yeniden test ettiğinizde, siz de [genel paketler](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) klasörünüzü kaldırana kadar paketin eski sürümünü kullanmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-155">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="05c1e-156">Bu, özellikle her derlemede benzersiz bir ön sürüm etiketi kullanmayan paketleri test ederken ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="05c1e-156">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05c1e-157">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="05c1e-157">Next Steps</span></span>

<span data-ttu-id="05c1e-158">Bir `.nupkg` dosya olan bir paket oluşturduktan sonra, bir [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05c1e-158">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="05c1e-159">Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05c1e-159">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="05c1e-160">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="05c1e-160">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="05c1e-161">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="05c1e-161">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="05c1e-162">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="05c1e-162">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="05c1e-163">Kaynak ve yapılandırma dosyalarının dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="05c1e-163">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="05c1e-164">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="05c1e-164">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="05c1e-165">Yayın öncesi sürümler</span><span class="sxs-lookup"><span data-stu-id="05c1e-165">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="05c1e-166">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="05c1e-166">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="05c1e-167">COM birlikte çalışma Derlemeleriyle paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="05c1e-167">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="05c1e-168">Son olarak, bilmeniz için ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="05c1e-168">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="05c1e-169">Yerel Paketler</span><span class="sxs-lookup"><span data-stu-id="05c1e-169">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="05c1e-170">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="05c1e-170">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
