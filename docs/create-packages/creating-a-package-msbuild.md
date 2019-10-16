---
title: MSBuild kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9512899a4086d17d2584f16833aba33efb321eae
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380700"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="83b0d-103">MSBuild kullanarak bir NuGet paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="83b0d-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="83b0d-104">Kodunuzdan bir NuGet paketi oluşturduğunuzda, bu işlevselliği herhangi bir sayıda diğer geliştirici tarafından paylaşılabilen ve kullanılabilecek bir bileşene paketleyerek.</span><span class="sxs-lookup"><span data-stu-id="83b0d-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="83b0d-105">Bu makalede, MSBuild kullanarak bir paketin nasıl oluşturulacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="83b0d-106">MSBuild, NuGet içeren her Visual Studio iş yüküne önceden yüklenmiş olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="83b0d-107">Ayrıca, [DotNet MSBuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild) Ile DotNet CLI aracılığıyla MSBuild 'i de kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="83b0d-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span></span>

<span data-ttu-id="83b0d-108">NuGet, .NET Core ve .NET Standard [SDK stili biçimini](../resources/check-project-format.md)kullanan projeler ve diğer SDK stilindeki projeler için, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak üzere kullanır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="83b0d-109">@No__t-0 kullanan SDK olmayan bir proje için, NuGet Ayrıca bir paket oluşturmak için proje dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="83b0d-110">SDK stili projelerde varsayılan olarak paket işlevselliği bulunur.</span><span class="sxs-lookup"><span data-stu-id="83b0d-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="83b0d-111">SDK olmayan biçim PackageReference projeleri için, proje bağımlılıklarına NuGet. Build. Tasks. Pack paketini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="83b0d-112">MSBuild paketi hedefleri hakkında ayrıntılı bilgi için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="83b0d-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="83b0d-113">@No__t-0 olan bir paket oluşturan komut, `dotnet pack` ' e denk işlev.</span><span class="sxs-lookup"><span data-stu-id="83b0d-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83b0d-114">Bu konu, [SDK stili](../resources/check-project-format.md) projelere, genellikle .NET Core ve .NET Standard projelerine ve PACKAGEREFERENCE kullanan SDK olmayan bir proje için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="83b0d-115">Özellikleri ayarla</span><span class="sxs-lookup"><span data-stu-id="83b0d-115">Set properties</span></span>

<span data-ttu-id="83b0d-116">Bir paket oluşturmak için aşağıdaki özellikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="83b0d-117">`PackageId`, paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="83b0d-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="83b0d-118">Belirtilmemişse, varsayılan değer `AssemblyName` ' dır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="83b0d-119">`Version`, *birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md)tanımlar.</span><span class="sxs-lookup"><span data-stu-id="83b0d-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="83b0d-120">Belirtilmemişse, varsayılan değer 1.0.0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="83b0d-121">Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="83b0d-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="83b0d-122">`Authors`, yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="83b0d-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="83b0d-123">Belirtilmemişse, varsayılan değer `AssemblyName` ' dır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="83b0d-124">`Company`, şirketinizin adı.</span><span class="sxs-lookup"><span data-stu-id="83b0d-124">`Company`, your company name.</span></span> <span data-ttu-id="83b0d-125">Belirtilmemişse, varsayılan değer `AssemblyName` ' dır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="83b0d-126">Visual Studio 'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini ' de projeye sağ tıklayıp **Özellikler**' i seçin ve **paket** sekmesini seçin).</span><span class="sxs-lookup"><span data-stu-id="83b0d-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="83b0d-127">Bu özellikleri doğrudan proje dosyaları ( *. csproj*) içinde de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-127">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="83b0d-128">Pakete nuget.org genelinde benzersiz bir tanımlayıcı verin veya kullandığınız herhangi bir paket kaynağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="83b0d-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="83b0d-129">Aşağıdaki örnekte, bu özelliklerle birlikte basit ve tamamlanmış bir proje dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-129">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="83b0d-130">Ayrıca, [MSBuild paketi hedefleri](../reference/msbuild-targets.md#pack-target)' nde açıklandığı gibi `Title`, `PackageDescription` ve `PackageTags` gibi isteğe bağlı özellikleri de ayarlayabilirsiniz, [bağımlılık varlıklarını](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta veri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties)kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="83b0d-131">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="83b0d-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="83b0d-132">Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. proje dosyaları ve [paket sürümü oluşturma](../concepts/package-versioning.md) [içindeki paket başvuruları](../consume-packages/package-references-in-project-files.md) .</span><span class="sxs-lookup"><span data-stu-id="83b0d-132">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="83b0d-133">Ayrıca, `<IncludeAssets>` ve `<ExcludeAssets>` özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan yüzeylerden yüzey olabilir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="83b0d-134">Daha fazla bilgi için, [bağımlılık varlıklarını denetleyen](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)seee.</span><span class="sxs-lookup"><span data-stu-id="83b0d-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="83b0d-135">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="83b0d-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="83b0d-136">NuGet. Build. Tasks. Pack paketini ekleme</span><span class="sxs-lookup"><span data-stu-id="83b0d-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="83b0d-137">SDK olmayan bir proje ve PackageReference ile MSBuild kullanıyorsanız, projenize NuGet. Build. Tasks. Pack paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="83b0d-137">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="83b0d-138">Proje dosyasını açın ve `<PropertyGroup>` öğesinden sonra aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="83b0d-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="83b0d-139">Bir geliştirici komut istemi açın ( **arama** kutusunda, **Geliştirici komut istemi**yazın).</span><span class="sxs-lookup"><span data-stu-id="83b0d-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="83b0d-140">Visual Studio için Geliştirici Komut İstemi, MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle **Başlangıç** menüsünden başlatmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-140">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="83b0d-141">Proje dosyasını içeren klasöre geçin ve NuGet. Build. Tasks. Pack paketini yüklemek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="83b0d-141">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="83b0d-142">MSBuild çıkışının, yapılandırmanın başarıyla tamamlandığını gösteriyor olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="83b0d-142">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="83b0d-143">MSBuild-t:Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="83b0d-143">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="83b0d-144">Projeden bir NuGet paketi (`.nupkg` dosyası) oluşturmak için `msbuild -t:pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="83b0d-144">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="83b0d-145">Visual Studio için geliştirici komut isteminde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="83b0d-145">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="83b0d-146">Çıktı, `.nupkg` dosyasının yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-146">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="83b0d-147">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="83b0d-147">Automatically generate package on build</span></span>

<span data-ttu-id="83b0d-148">@No__t otomatik olarak çalıştırmak için-0 proje oluşturduğunuzda veya geri yüklediğinizde, proje dosyanıza aşağıdaki satırı `<PropertyGroup>` içinde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="83b0d-148">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="83b0d-149">Bir çözümde `msbuild -t:pack` ' ı çalıştırdığınızda, bu, çözümdeki ([<IsPackable> özelliği) (-2](/dotnet/core/tools/csproj#nuget-metadata-properties) özelliği) `true` olarak ayarlanmış olan tüm projeleri paketler.</span><span class="sxs-lookup"><span data-stu-id="83b0d-149">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="83b0d-150">Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.</span><span class="sxs-lookup"><span data-stu-id="83b0d-150">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="83b0d-151">Test paketi yüklemesi</span><span class="sxs-lookup"><span data-stu-id="83b0d-151">Test package installation</span></span>

<span data-ttu-id="83b0d-152">Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-152">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="83b0d-153">Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="83b0d-153">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="83b0d-154">Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-154">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83b0d-155">Paketler sabittir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-155">Packages are immutable.</span></span> <span data-ttu-id="83b0d-156">Bir sorunu düzeltseniz, yeniden test ettiğinizde, siz de [genel paketler](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) klasörünüzü kaldırana kadar paketin eski sürümünü kullanmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-156">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="83b0d-157">Bu, özellikle her derlemede benzersiz bir ön sürüm etiketi kullanmayan paketleri test ederken ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="83b0d-157">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83b0d-158">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="83b0d-158">Next Steps</span></span>

<span data-ttu-id="83b0d-159">Bir `.nupkg` dosyası olan bir paket oluşturduktan sonra, [paketi yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83b0d-159">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="83b0d-160">Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="83b0d-160">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="83b0d-161">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="83b0d-161">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="83b0d-162">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="83b0d-162">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="83b0d-163">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="83b0d-163">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="83b0d-164">Kaynak ve yapılandırma dosyalarının dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="83b0d-164">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="83b0d-165">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="83b0d-165">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="83b0d-166">Yayın öncesi sürümler</span><span class="sxs-lookup"><span data-stu-id="83b0d-166">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="83b0d-167">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="83b0d-167">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="83b0d-168">COM birlikte çalışma Derlemeleriyle paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="83b0d-168">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="83b0d-169">Son olarak, bilmeniz için ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="83b0d-169">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="83b0d-170">Yerel Paketler</span><span class="sxs-lookup"><span data-stu-id="83b0d-170">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="83b0d-171">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="83b0d-171">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
