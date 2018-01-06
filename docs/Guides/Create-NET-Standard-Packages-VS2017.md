---
title: "Visual Studio 2017 ile .NET standart 2.0 NuGet paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "NuGet kullanarak .NET standart 2.0 NuGet paketleri oluşturma bir uçtan uca Kılavuz 4.x ve Visual Studio 2017."
keywords: "bir paket, .NET standart paketleri, .NET Core oluşturun"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="e12cf-104">Visual Studio 2017 ile .NET standart 2.0 paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e12cf-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="e12cf-105">*NuGet 4.x+ ve MSBuild 15.3 Visual Studio 2017 güncelleştirme 3 koşuluyla + uygulanır. Visual Studio 2017 önceki sürümleri için bu yönergeler için standart 1.4 .NET 1. 6 değiştirerek geçerli \<TargetFramework\> özelliği. Ayrıca bkz. [.NET standart paketleri oluşturmak Visual Studio 2015 ile](../guides/create-net-standard-packages-vs2015.md) NuGet 3.x+ ile çalışmak için.*</span><span class="sxs-lookup"><span data-stu-id="e12cf-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="e12cf-106">[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması.</span><span class="sxs-lookup"><span data-stu-id="e12cf-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="e12cf-107">.NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e12cf-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="e12cf-108">Bunu tüm .NET çalışma zamanları arasında kullanılabilir PCLs üretmek için geliştiricilere olanak sağlar ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e12cf-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="e12cf-109">Bu kılavuz .NET standart kitaplığı 2.0 Visual Studio 2017 güncelleştirme 3'ü ve NuGet 4.0 ile hedefleyen bir nuget paketi oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="e12cf-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="e12cf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e12cf-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="e12cf-111">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="e12cf-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="e12cf-112">.Csproj dosyasındaki meta verilerini düzenleme</span><span class="sxs-lookup"><span data-stu-id="e12cf-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="e12cf-113">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="e12cf-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="e12cf-114">İlgili Konular</span><span class="sxs-lookup"><span data-stu-id="e12cf-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="e12cf-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e12cf-115">Pre-requisites</span></span>

<span data-ttu-id="e12cf-116">Visual Studio 2017 güncelleştirme 3 ile bu gözden geçirme gerektiren **.NET Core platformlar arası geliştirme** iş yükü.</span><span class="sxs-lookup"><span data-stu-id="e12cf-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="e12cf-117">Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/), ya da Professional ve Enterprise sürümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e12cf-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="e12cf-118">İş yükü şu şekilde görünür Visual Studio yükleyicisinde gerektirir:</span><span class="sxs-lookup"><span data-stu-id="e12cf-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Visual Studio yükleyicisi .NET core platformlar arası geliştirme iş yükü](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="e12cf-120">.NET standart sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="e12cf-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="e12cf-121">Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > .NET standart** düğümü, select **sınıf kitaplığı (Net standart)**, AppLogger için adı değiştirin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e12cf-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Yeni sınıf kitaplığı proje oluşturma](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="e12cf-123">Derleme yapılandırmasını değiştirme **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="e12cf-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="e12cf-124">Sağ `AppLogger` seçin Çözüm Gezgini'nde projeye **özellikleri**seçin **yapı** sekmesinde, onay kutusunu için **XML belge dosyası**ve ayarlayın yalnızca filename `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="e12cf-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="e12cf-125">Projeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e12cf-125">Then save the project.</span></span>

1. <span data-ttu-id="e12cf-126">Kodunuzu bileşenine (hangi açıkça yalnızca konsola ileti çıkarır) aşağıdaki gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e12cf-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="e12cf-127">(Sürüm yapılandırmasıyla) projeyi oluşturun ve DLL ve XML dosyaları içinde üretilir denetleyin `bin\Release\netstandard2.0` klasör.</span><span class="sxs-lookup"><span data-stu-id="e12cf-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="e12cf-128">.Csproj dosyasındaki meta verilerini düzenleme</span><span class="sxs-lookup"><span data-stu-id="e12cf-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="e12cf-129">Paket meta verileri doğrudan yer alan NuGet 4.0 ve .NET Core projelerle `.csproj` yerine dış dosyaları gibi dosya bir `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="e12cf-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="e12cf-130">Meta verilerin tam açıklamasını bulunan [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="e12cf-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="e12cf-131">Select Çözüm Gezgini'nde projeye sağ tıklayın **Düzenle AppLogger.csproj**ve ardından aşağıdaki gibi paket bilgileri içerecek şekilde ilk özellik grubu düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="e12cf-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="e12cf-132">Projeyi kaydedin sonra çözüme sağ tıklayın ve seçin **yapı çözümü** bu kez doğru meta verilerle bir paket için tüm dosyaları yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="e12cf-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="e12cf-133">Paket bileşeni</span><span class="sxs-lookup"><span data-stu-id="e12cf-133">Package the component</span></span>

<span data-ttu-id="e12cf-134">NuGet 4.0 destekleyen MSBuild sürümü 15.1 + (MSBuild 15.3 Visual Studio 2017 güncelleştirme 3'ü bir parçası olarak dahil) kullanarak bir paketi hedef proje içerdiğinde gerekli paket meta verileri önceki bölümde eklendiği gibi.</span><span class="sxs-lookup"><span data-stu-id="e12cf-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="e12cf-135">Bu şekilde MSBuild çağırmak için yalnızca paketi hedef aynı klasörde komut satırında belirtin `.csproj` dosyası:</span><span class="sxs-lookup"><span data-stu-id="e12cf-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="e12cf-136">Ek seçeneklerle için `msbuild /t:pack`gibi içerik dosyalarını, simgeler ve kaynak kodu, bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="e12cf-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="e12cf-137">Herhangi bir durumda, yukarıdaki komut oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg` içinde `bin\Release` klasörü varsayılan olarak, bu yapılandırma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e12cf-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="e12cf-138">Atlarsanız `/p` anahtarı, varsayılan yapılandırmayı olacaktır `Debug`.</span><span class="sxs-lookup"><span data-stu-id="e12cf-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="e12cf-139">Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriği görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="e12cf-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![NuGet paket AppLogger paket gösteren Gezgini](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e12cf-141">A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="e12cf-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e12cf-142">Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e12cf-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e12cf-143">Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e12cf-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="e12cf-144">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="e12cf-144">Related topics</span></span>

- <span data-ttu-id="e12cf-145">[Proje dosyalarını başvurularında paketini](../consume-packages/package-references-in-project-files.md) paketinizi proje dosyasında doğrudan açıklayan tüm ayrıntılarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="e12cf-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="e12cf-146">[NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md) kullanmak için tüm seçenekleri açıklar `msbuild /t:pack` paketi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e12cf-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="e12cf-147">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="e12cf-147">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e12cf-148">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e12cf-148">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
