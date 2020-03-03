---
title: MSBuild kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231324"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="8031c-103">MSBuild kullanarak bir NuGet paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8031c-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="8031c-104">Kodunuzdan bir NuGet paketi oluşturduğunuzda, bu işlevselliği herhangi bir sayıda diğer geliştirici tarafından paylaşılabilen ve kullanılabilecek bir bileşene paketleyerek.</span><span class="sxs-lookup"><span data-stu-id="8031c-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="8031c-105">Bu makalede, MSBuild kullanarak bir paketin nasıl oluşturulacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="8031c-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="8031c-106">MSBuild, NuGet içeren her Visual Studio iş yüküne önceden yüklenmiş olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="8031c-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="8031c-107">Ayrıca DotNet [MSBuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild)Ile DotNet CLI aracılığıyla MSBuild 'i de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="8031c-108">NuGet, .NET Core ve .NET Standard [SDK stili biçimini](../resources/check-project-format.md)kullanan projeler ve diğer SDK stilindeki projeler için, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak üzere kullanır.</span><span class="sxs-lookup"><span data-stu-id="8031c-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="8031c-109">`<PackageReference>`kullanan SDK olmayan bir proje için, NuGet Ayrıca bir paket oluşturmak için proje dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="8031c-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="8031c-110">SDK stili projelerde varsayılan olarak paket işlevselliği bulunur.</span><span class="sxs-lookup"><span data-stu-id="8031c-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="8031c-111">SDK olmayan biçim PackageReference projeleri için, proje bağımlılıklarına NuGet. Build. Tasks. Pack paketini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8031c-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="8031c-112">MSBuild paketi hedefleri hakkında ayrıntılı bilgi için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="8031c-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="8031c-113">`msbuild -t:pack`bir paket oluşturan komut, `dotnet pack`işlevi eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="8031c-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8031c-114">Bu konu, [SDK stili](../resources/check-project-format.md) projelere, genellikle .NET Core ve .NET Standard projelerine ve PACKAGEREFERENCE kullanan SDK olmayan bir proje için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8031c-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="8031c-115">Özellikleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="8031c-115">Set properties</span></span>

<span data-ttu-id="8031c-116">Bir paket oluşturmak için aşağıdaki özellikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8031c-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="8031c-117">paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısını `PackageId`.</span><span class="sxs-lookup"><span data-stu-id="8031c-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="8031c-118">Belirtilmemişse, varsayılan değer `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="8031c-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="8031c-119">`Version`, *birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md)tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8031c-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="8031c-120">Belirtilmemişse, varsayılan değer 1.0.0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8031c-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="8031c-121">Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="8031c-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="8031c-122">`Authors`, yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8031c-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="8031c-123">Belirtilmemişse, varsayılan değer `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="8031c-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="8031c-124">`Company`, şirketinizin adı.</span><span class="sxs-lookup"><span data-stu-id="8031c-124">`Company`, your company name.</span></span> <span data-ttu-id="8031c-125">Belirtilmemişse, varsayılan değer `AssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="8031c-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="8031c-126">Ayrıca, PackageReference kullanan SDK olmayan bir stil projesi paketlebiliyorsanız aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="8031c-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="8031c-127">paketi çağırırken oluşturulan paketin çıkış klasörü `PackageOutputPath`.</span><span class="sxs-lookup"><span data-stu-id="8031c-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="8031c-128">Visual Studio 'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini ' de projeye sağ tıklayıp **Özellikler**' i seçin ve **paket** sekmesini seçin).</span><span class="sxs-lookup"><span data-stu-id="8031c-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="8031c-129">Bu özellikleri doğrudan proje dosyaları (*. csproj*) içinde de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="8031c-130">Pakete nuget.org genelinde benzersiz bir tanımlayıcı verin veya kullandığınız herhangi bir paket kaynağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8031c-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="8031c-131">Aşağıdaki örnekte, bu özelliklerle birlikte basit ve tamamlanmış bir proje dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8031c-131">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="8031c-132">`Title`, `PackageDescription`ve `PackageTags`gibi isteğe bağlı özellikleri, [MSBuild paketi hedefleri](../reference/msbuild-targets.md#pack-target)' nde açıklandığı gibi, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta verileri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties)de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="8031c-133">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8031c-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="8031c-134">Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. proje dosyaları ve [paket sürümü oluşturma](../concepts/package-versioning.md) [içindeki paket başvuruları](../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="8031c-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="8031c-135">Ayrıca, `<IncludeAssets>` ve `<ExcludeAssets>` özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan yüzeylerden yüzey mümkündür.</span><span class="sxs-lookup"><span data-stu-id="8031c-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="8031c-136">Daha fazla bilgi için, [bağımlılık varlıklarını denetleyen](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)seee.</span><span class="sxs-lookup"><span data-stu-id="8031c-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="8031c-137">İsteğe bağlı açıklama alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="8031c-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="8031c-138">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8031c-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="8031c-139">NuGet. Build. Tasks. Pack paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="8031c-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="8031c-140">SDK olmayan bir proje ve PackageReference ile MSBuild kullanıyorsanız, projenize NuGet. Build. Tasks. Pack paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8031c-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="8031c-141">Proje dosyasını açın ve `<PropertyGroup>` öğeden sonra aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8031c-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="8031c-142">Bir geliştirici komut istemi açın ( **arama** kutusunda, **Geliştirici komut istemi**yazın).</span><span class="sxs-lookup"><span data-stu-id="8031c-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="8031c-143">Visual Studio için Geliştirici Komut İstemi, MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle **Başlangıç** menüsünden başlatmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="8031c-144">Proje dosyasını içeren klasöre geçin ve NuGet. Build. Tasks. Pack paketini yüklemek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="8031c-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="8031c-145">MSBuild çıkışının, yapılandırmanın başarıyla tamamlandığını gösteriyor olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8031c-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="8031c-146">MSBuild-t:Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8031c-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="8031c-147">Projeden bir NuGet paketi (`.nupkg` dosyası) oluşturmak için, Ayrıca projeyi otomatik olarak oluşturan `msbuild -t:pack` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8031c-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="8031c-148">Visual Studio için geliştirici komut isteminde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="8031c-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="8031c-149">Çıktı, `.nupkg` dosyasının yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8031c-149">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="8031c-150">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="8031c-150">Automatically generate package on build</span></span>

<span data-ttu-id="8031c-151">Projeyi oluştururken veya geri yüklerken `msbuild -t:pack` otomatik olarak çalıştırmak için, aşağıdaki satırı `<PropertyGroup>`içindeki proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8031c-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="8031c-152">Bir çözümde `msbuild -t:pack` çalıştırdığınızda bu, çözümdeki ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) özelliği olarak ayarlanmış olan) tüm projeler için paketler `true`olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8031c-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="8031c-153">Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.</span><span class="sxs-lookup"><span data-stu-id="8031c-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="8031c-154">Test paketi yüklemesi</span><span class="sxs-lookup"><span data-stu-id="8031c-154">Test package installation</span></span>

<span data-ttu-id="8031c-155">Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="8031c-156">Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="8031c-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="8031c-157">Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8031c-158">Paketler sabittir.</span><span class="sxs-lookup"><span data-stu-id="8031c-158">Packages are immutable.</span></span> <span data-ttu-id="8031c-159">Bir sorunu düzeltseniz, yeniden test ettiğinizde, siz de [genel paketler](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) klasörünüzü kaldırana kadar paketin eski sürümünü kullanmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="8031c-160">Bu, özellikle her derlemede benzersiz bir ön sürüm etiketi kullanmayan paketleri test ederken ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="8031c-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8031c-161">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8031c-161">Next Steps</span></span>

<span data-ttu-id="8031c-162">Bir `.nupkg` dosyası olan bir paket oluşturduktan sonra, [paketi yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8031c-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="8031c-163">Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8031c-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="8031c-164">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="8031c-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="8031c-165">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="8031c-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="8031c-166">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="8031c-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="8031c-167">Kaynak ve yapılandırma dosyalarının dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="8031c-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="8031c-168">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="8031c-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="8031c-169">Yayın öncesi sürümler</span><span class="sxs-lookup"><span data-stu-id="8031c-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="8031c-170">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="8031c-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="8031c-171">COM birlikte çalışma Derlemeleriyle paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="8031c-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="8031c-172">Son olarak, bilmeniz için ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="8031c-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="8031c-173">Yerel Paketler</span><span class="sxs-lookup"><span data-stu-id="8031c-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="8031c-174">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="8031c-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
