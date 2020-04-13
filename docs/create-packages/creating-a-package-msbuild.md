---
title: MSBuild'i kullanarak NuGet paketi oluşturma
description: Dosyaları ve sürüm gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma sürecine ilişkin ayrıntılı bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231324"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="103d1-103">MSBuild'i kullanarak NuGet paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="103d1-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="103d1-104">Kodunuzdan bir NuGet paketi oluşturduğunuzda, bu işlevselliği diğer geliştiricilerle paylaşılabilen ve diğer geliştiriciler tarafından kullanılabilecek bir bileşene paketlersiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="103d1-105">Bu makalede, MSBuild kullanarak bir paket oluşturmak için nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="103d1-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="103d1-106">MSBuild, NuGet içeren her Visual Studio iş yüküyle önceden yüklenmiş olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="103d1-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="103d1-107">Ayrıca [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild)ile dotnet CLI üzerinden MSBuild kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="103d1-108">[SDK stili biçimini](../resources/check-project-format.md)ve diğer SDK stili projeleri kullanan .NET Core ve .NET Standard projeleri için NuGet, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="103d1-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="103d1-109">Kullanan SDK tarzı olmayan bir `<PackageReference>`proje için, NuGet bir paket oluşturmak için proje dosyasını da kullanır.</span><span class="sxs-lookup"><span data-stu-id="103d1-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="103d1-110">SDK tarzı projeler varsayılan olarak paket işlevine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="103d1-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="103d1-111">SDK tarzı olmayan PackageReference projeleri için proje bağımlılıklarına NuGet.Build.Tasks.Pack paketini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="103d1-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="103d1-112">MSBuild paketi hedefleri hakkında ayrıntılı bilgi için [NuGet paketine bakın ve MSBuild hedefleri olarak geri yükleyin.](../reference/msbuild-targets.md)</span><span class="sxs-lookup"><span data-stu-id="103d1-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="103d1-113">Bir paket oluşturan komut, `msbuild -t:pack` `dotnet pack`işlevsellik eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="103d1-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="103d1-114">Bu konu, genellikle .NET Core ve .NET Standart projeleri olan [SDK tarzı](../resources/check-project-format.md) projeler ve PackageReference kullanan SDK tarzı olmayan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="103d1-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="103d1-115">Özellikleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="103d1-115">Set properties</span></span>

<span data-ttu-id="103d1-116">Bir paket oluşturmak için aşağıdaki özellikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="103d1-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="103d1-117">`PackageId`, paketi barındıran galeride benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="103d1-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="103d1-118">Belirtilmemişse, varsayılan `AssemblyName`değer .</span><span class="sxs-lookup"><span data-stu-id="103d1-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="103d1-119">`Version`, *Major.Minor.Patch[-Soneki]* formunda belirli bir sürüm numarası ve *-Soneki* ön [sürüm sürümlerini](prerelease-packages.md)tanımlar.</span><span class="sxs-lookup"><span data-stu-id="103d1-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="103d1-120">Belirtilmemişse, varsayılan değer 1.0.0'dır.</span><span class="sxs-lookup"><span data-stu-id="103d1-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="103d1-121">Ana bilgisayarda görünmesi gerektiği gibi paket başlığı (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="103d1-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="103d1-122">`Authors`, yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="103d1-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="103d1-123">Belirtilmemişse, varsayılan `AssemblyName`değer .</span><span class="sxs-lookup"><span data-stu-id="103d1-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="103d1-124">`Company`, şirket adınız.</span><span class="sxs-lookup"><span data-stu-id="103d1-124">`Company`, your company name.</span></span> <span data-ttu-id="103d1-125">Belirtilmemişse, varsayılan `AssemblyName`değer .</span><span class="sxs-lookup"><span data-stu-id="103d1-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="103d1-126">Ayrıca PackageReference kullanan SDK tarzı olmayan projeleri paketliliyorsanız, aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="103d1-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="103d1-127">`PackageOutputPath`, paketi ararken oluşturulan paketin çıktı klasörü.</span><span class="sxs-lookup"><span data-stu-id="103d1-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="103d1-128">Visual Studio'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini'nde projeyi sağ tıklatın, **Özellikler'i**seçin ve **Paket** sekmesini seçin).</span><span class="sxs-lookup"><span data-stu-id="103d1-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="103d1-129">Ayrıca bu özellikleri doğrudan proje dosyalarında *(.csproj)* ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="103d1-130">Pakete, nuget.org veya kullandığınız paket kaynağında benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="103d1-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="103d1-131">Aşağıdaki örnekte, bu özelliklere sahip basit, tam bir proje dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="103d1-131">The following example shows a simple, complete project file with these properties included.</span></span>

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

<span data-ttu-id="103d1-132">[MsBuild paketi hedeflerinde](../reference/msbuild-targets.md#pack-target)açıklandığı `Title`gibi `PackageDescription` `PackageTags`isteğe bağlı özellikleri de ayarlayabilirsiniz, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta veri özellikleri.](/dotnet/core/tools/csproj#nuget-metadata-properties)</span><span class="sxs-lookup"><span data-stu-id="103d1-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="103d1-133">Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **PackageTags** özelliğine özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="103d1-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="103d1-134">Bağımlılıkları bildirme ve sürüm numaralarını belirtme yle ilgili ayrıntılar için [proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md) ve Paket [sürümüne](../concepts/package-versioning.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="103d1-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="103d1-135">Varlıkları bağımlılıklardan doğrudan pakete ve `<IncludeAssets>` `<ExcludeAssets>` öznitelikleri kullanarak yüzeye çıkarmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="103d1-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="103d1-136">Daha fazla bilgi için [bkz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)</span><span class="sxs-lookup"><span data-stu-id="103d1-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="103d1-137">İsteğe bağlı açıklama alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="103d1-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="103d1-138">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="103d1-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="103d1-139">NuGet.Build.Tasks.Pack paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="103d1-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="103d1-140">MSBuild'i SDK tarzı olmayan bir proje ve PackageReference ile kullanıyorsanız, Projenize NuGet.Build.Tasks.Pack paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="103d1-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="103d1-141">Proje dosyasını açın ve `<PropertyGroup>` öğeden sonra aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="103d1-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="103d1-142">Geliştirici komut istemini açın **(Arama** kutusunda **Geliştirici komut istemi**yazın).</span><span class="sxs-lookup"><span data-stu-id="103d1-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="103d1-143">MSBuild için gerekli tüm yollarla yapılandırılacak gibi, genellikle Görsel Stüdyo için Geliştirici Komut Komut Ustem komutunu **Başlat** menüsünden başlatmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="103d1-144">Proje dosyasını içeren klasöre geçin ve NuGet.Build.Tasks.Pack paketini yüklemek için aşağıdaki komutu yazın.</span><span class="sxs-lookup"><span data-stu-id="103d1-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="103d1-145">MSBuild çıktısının yapının başarıyla tamamlandığını gösterdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="103d1-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="103d1-146">msbuild -t:pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="103d1-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="103d1-147">Projeden bir NuGet `.nupkg` paketi (dosya) oluşturmak `msbuild -t:pack` için, projeyi otomatik olarak oluşturan komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="103d1-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="103d1-148">Visual Studio için Geliştirici komut isteminde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="103d1-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="103d1-149">`.nupkg` Çıktı, dosyaya giden yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="103d1-149">The output shows the path to the `.nupkg` file.</span></span>

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

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="103d1-150">Otomatik olarak yapı üzerinde paket oluşturmak</span><span class="sxs-lookup"><span data-stu-id="103d1-150">Automatically generate package on build</span></span>

<span data-ttu-id="103d1-151">Projeyi oluştururken veya geri yüklediğinizde otomatik olarak çalıştırmak `msbuild -t:pack` için `<PropertyGroup>`aşağıdaki satırı proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="103d1-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="103d1-152">Bir çözüm `msbuild -t:pack` üzerinde çalıştırdığınızda, bu paketlenebilir çözümdeki tüm[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) projeleri paketler `true`(özellik ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="103d1-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="103d1-153">Paketi otomatik olarak oluşturduğunuzda, paketi hazırlama süresi projenizin oluşturma süresini artırır.</span><span class="sxs-lookup"><span data-stu-id="103d1-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="103d1-154">Test paketi kurulumu</span><span class="sxs-lookup"><span data-stu-id="103d1-154">Test package installation</span></span>

<span data-ttu-id="103d1-155">Paket yayımlamadan önce, genellikle bir projeye paket yükleme işlemini sınamak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="103d1-156">Testler, zorunlu dosyaların tümünden inin projedeki doğru yerlerinde sonunun olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="103d1-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="103d1-157">Yüklemeleri Visual Studio'da veya komut satırında normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="103d1-158">Paketler değişmez.</span><span class="sxs-lookup"><span data-stu-id="103d1-158">Packages are immutable.</span></span> <span data-ttu-id="103d1-159">Bir sorunu düzeltirseniz, paketin içeriğini değiştirin ve yeniden paketleyin, yeniden test ettiğinizde, genel paketler klasörünüzü [temize çıkarana](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) kadar paketin eski sürümünü kullanmaya devam eceksiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="103d1-160">Bu, özellikle her yapıda benzersiz bir yayın öncesi etiket kullanmayan paketleri sınarken alakalıdır.</span><span class="sxs-lookup"><span data-stu-id="103d1-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="103d1-161">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="103d1-161">Next Steps</span></span>

<span data-ttu-id="103d1-162">Bir dosya olan bir `.nupkg` paket oluşturduktan sonra, paketi [Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi istediğiniz galeride yayınlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="103d1-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="103d1-163">Ayrıca paketinizin yeteneklerini genişletmek veya aşağıdaki konularda açıklandığı gibi diğer senaryoları desteklemek de isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="103d1-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="103d1-164">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="103d1-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="103d1-165">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="103d1-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="103d1-166">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="103d1-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="103d1-167">Kaynak ve yapılandırma dosyalarının dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="103d1-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="103d1-168">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="103d1-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="103d1-169">Ön sürüm sürümleri</span><span class="sxs-lookup"><span data-stu-id="103d1-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="103d1-170">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="103d1-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="103d1-171">COM interop montajları ile paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="103d1-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="103d1-172">Son olarak, dikkat edilmesi gereken ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="103d1-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="103d1-173">Yerli Paketler</span><span class="sxs-lookup"><span data-stu-id="103d1-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="103d1-174">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="103d1-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
