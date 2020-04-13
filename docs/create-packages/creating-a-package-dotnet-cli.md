---
title: dotnet CLI'yi kullanarak NuGet paketi oluşturma
description: Dosyaları ve sürüm gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma sürecine ilişkin ayrıntılı bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230596"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="f7758-103">dotnet CLI'yi kullanarak NuGet paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7758-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="f7758-104">Paketiniz ne yaparsa yapsın veya hangi kodu içerse içersin, `dotnet.exe`bu işlevselliği diğer geliştiricilerle paylaşılabilen ve diğer geliştiriciler tarafından kullanılabilecek bir bileşene dönüştürmek için CLI araçlarından `nuget.exe` birini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="f7758-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="f7758-105">Bu makalede, dotnet CLI kullanarak bir paket oluşturmak için nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f7758-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="f7758-106">CLI'yi yüklemek için `dotnet` [NuGet istemci araçlarını yükleyin'](../install-nuget-client-tools.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="f7758-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="f7758-107">Visual Studio 2017'den itibaren dotnet CLI .NET Core iş yüklerine dahildir.</span><span class="sxs-lookup"><span data-stu-id="f7758-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="f7758-108">[SDK stili biçimini](../resources/check-project-format.md)ve diğer SDK stili projeleri kullanan .NET Core ve .NET Standard projeleri için NuGet, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f7758-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="f7758-109">Adım adım eğitimler için [dotnet CLI ile .NET Standart Paketleri Oluştur](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) veya [Visual Studio ile .NET Standart Paketleri Oluştur'a](../quickstart/create-and-publish-a-package-using-visual-studio.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="f7758-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="f7758-110">`msbuild -t:pack`'ye `dotnet pack`eşdeğer işlevselliktir.</span><span class="sxs-lookup"><span data-stu-id="f7758-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="f7758-111">MSBuild ile oluşturmak için [bkz.](creating-a-package-msbuild.md)</span><span class="sxs-lookup"><span data-stu-id="f7758-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7758-112">Bu konu, genellikle .NET Core ve .NET Standard projeleri olan [SDK tarzı](../resources/check-project-format.md) projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f7758-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="f7758-113">Özellikleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="f7758-113">Set properties</span></span>

<span data-ttu-id="f7758-114">Bir paket oluşturmak için aşağıdaki özellikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f7758-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="f7758-115">`PackageId`, paketi barındıran galeride benzersiz olması gereken paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f7758-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="f7758-116">Belirtilmemişse, varsayılan `AssemblyName`değer .</span><span class="sxs-lookup"><span data-stu-id="f7758-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="f7758-117">`Version`, *Major.Minor.Patch[-Soneki]* formunda belirli bir sürüm numarası ve *-Soneki* ön [sürüm sürümlerini](prerelease-packages.md)tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f7758-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="f7758-118">Belirtilmemişse, varsayılan değer 1.0.0'dır.</span><span class="sxs-lookup"><span data-stu-id="f7758-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="f7758-119">Ana bilgisayarda görünmesi gerektiği gibi paket başlığı (nuget.org gibi)</span><span class="sxs-lookup"><span data-stu-id="f7758-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="f7758-120">`Authors`, yazar ve sahip bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f7758-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="f7758-121">Belirtilmemişse, varsayılan `AssemblyName`değer .</span><span class="sxs-lookup"><span data-stu-id="f7758-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="f7758-122">`Company`, şirket adınız.</span><span class="sxs-lookup"><span data-stu-id="f7758-122">`Company`, your company name.</span></span> <span data-ttu-id="f7758-123">Belirtilmemişse, varsayılan `AssemblyName`değer .</span><span class="sxs-lookup"><span data-stu-id="f7758-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="f7758-124">Visual Studio'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini'nde projeyi sağ tıklatın, **Özellikler'i**seçin ve **Paket** sekmesini seçin).</span><span class="sxs-lookup"><span data-stu-id="f7758-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="f7758-125">Ayrıca bu özellikleri doğrudan proje dosyalarında`.csproj`ayarlayabilirsiniz ( ).</span><span class="sxs-lookup"><span data-stu-id="f7758-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="f7758-126">Pakete, nuget.org veya kullandığınız paket kaynağında benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="f7758-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="f7758-127">Aşağıdaki örnekte, bu özelliklere sahip basit, tam bir proje dosyası gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f7758-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="f7758-128">(Komutu `dotnet new classlib` kullanarak yeni bir varsayılan proje oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="f7758-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

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

<span data-ttu-id="f7758-129">[MsBuild paketi hedeflerinde](../reference/msbuild-targets.md#pack-target)açıklandığı `Title`gibi `PackageDescription` `PackageTags`isteğe bağlı özellikleri de ayarlayabilirsiniz, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta veri özellikleri.](/dotnet/core/tools/csproj#nuget-metadata-properties)</span><span class="sxs-lookup"><span data-stu-id="f7758-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="f7758-130">Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **PackageTags** özelliğine özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f7758-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="f7758-131">Bağımlılıkları bildirme ve sürüm numaralarını belirtme yle ilgili ayrıntılar için [proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md) ve Paket [sürümüne](../concepts/package-versioning.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="f7758-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="f7758-132">Varlıkları bağımlılıklardan doğrudan pakete ve `<IncludeAssets>` `<ExcludeAssets>` öznitelikleri kullanarak yüzeye çıkarmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f7758-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="f7758-133">Daha fazla bilgi için [bkz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)</span><span class="sxs-lookup"><span data-stu-id="f7758-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="f7758-134">İsteğe bağlı açıklama alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="f7758-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="f7758-135">Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f7758-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="f7758-136">Sürü komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f7758-136">Run the pack command</span></span>

<span data-ttu-id="f7758-137">Projeden bir NuGet `.nupkg` paketi (dosya) oluşturmak `dotnet pack` için, projeyi otomatik olarak oluşturan komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f7758-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="f7758-138">`.nupkg` Çıktı, dosyaya giden yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7758-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="f7758-139">Otomatik olarak yapı üzerinde paket oluşturmak</span><span class="sxs-lookup"><span data-stu-id="f7758-139">Automatically generate package on build</span></span>

<span data-ttu-id="f7758-140">Çalıştırdığınızda `dotnet pack` `dotnet build`otomatik olarak çalıştırmak için proje dosyanıza `<PropertyGroup>`aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f7758-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="f7758-141">Bir çözüm `dotnet pack` üzerinde çalıştırdığınızda, bu paketlenebilir çözümdeki tüm[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) projeleri paketler `true`(özellik ayarlanır).</span><span class="sxs-lookup"><span data-stu-id="f7758-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="f7758-142">Paketi otomatik olarak oluşturduğunuzda, paketi hazırlama süresi projenizin oluşturma süresini artırır.</span><span class="sxs-lookup"><span data-stu-id="f7758-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="f7758-143">Test paketi kurulumu</span><span class="sxs-lookup"><span data-stu-id="f7758-143">Test package installation</span></span>

<span data-ttu-id="f7758-144">Paket yayımlamadan önce, genellikle bir projeye paket yükleme işlemini sınamak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="f7758-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="f7758-145">Testler, zorunlu dosyaların tümünden inin projedeki doğru yerlerinde sonunun olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7758-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="f7758-146">Yüklemeleri Visual Studio'da veya komut satırında normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak el ile test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7758-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7758-147">Paketler değişmez.</span><span class="sxs-lookup"><span data-stu-id="f7758-147">Packages are immutable.</span></span> <span data-ttu-id="f7758-148">Bir sorunu düzeltirseniz, paketin içeriğini değiştirin ve yeniden paketleyin, yeniden test ettiğinizde, genel paketler klasörünüzü [temize çıkarana](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) kadar paketin eski sürümünü kullanmaya devam eceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f7758-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="f7758-149">Bu, özellikle her yapıda benzersiz bir yayın öncesi etiket kullanmayan paketleri sınarken alakalıdır.</span><span class="sxs-lookup"><span data-stu-id="f7758-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7758-150">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f7758-150">Next Steps</span></span>

<span data-ttu-id="f7758-151">Bir dosya olan bir `.nupkg` paket oluşturduktan sonra, paketi [Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi istediğiniz galeride yayınlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7758-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="f7758-152">Ayrıca paketinizin yeteneklerini genişletmek veya aşağıdaki konularda açıklandığı gibi diğer senaryoları desteklemek de isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f7758-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="f7758-153">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="f7758-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="f7758-154">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="f7758-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="f7758-155">Paket simgesi ekleme</span><span class="sxs-lookup"><span data-stu-id="f7758-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="f7758-156">Kaynak ve yapılandırma dosyalarının dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="f7758-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="f7758-157">Yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="f7758-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f7758-158">Ön sürüm sürümleri</span><span class="sxs-lookup"><span data-stu-id="f7758-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="f7758-159">Paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="f7758-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="f7758-160">COM interop montajları ile paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7758-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="f7758-161">Son olarak, dikkat edilmesi gereken ek paket türleri vardır:</span><span class="sxs-lookup"><span data-stu-id="f7758-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="f7758-162">Yerli Paketler</span><span class="sxs-lookup"><span data-stu-id="f7758-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="f7758-163">Sembol Paketleri</span><span class="sxs-lookup"><span data-stu-id="f7758-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
