---
title: Proje biçimini tanımlama
description: Proje biçiminizin nasıl kimliklendirilebildiğini açıklar
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488488"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="614cf-103">Proje biçimini tanımlama</span><span class="sxs-lookup"><span data-stu-id="614cf-103">Identify the project format</span></span>

<span data-ttu-id="614cf-104">NuGet tüm .NET projeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="614cf-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="614cf-105">Ancak, proje biçimi (SDK stili veya SDK tarzı olmayan) NuGet paketlerini tüketmek ve oluşturmak için kullanmanız gereken araçlar ve yöntemlerden bazılarını belirler.</span><span class="sxs-lookup"><span data-stu-id="614cf-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="614cf-106">SDK tarzı projeler [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanır.</span><span class="sxs-lookup"><span data-stu-id="614cf-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="614cf-107">NuGet paketlerini tüketmek ve oluşturmak için kullandığınız yöntemler ve araçlar proje biçimine bağlı olduğundan proje türünü belirlemek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="614cf-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="614cf-108">SDK tarzı olmayan projelerde, yöntem ve araçlar da projenin biçime geçirilip `PackageReference` geçirilemediğine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="614cf-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="614cf-109">Projenizin SDK tarzı olup olmaması, projeyi oluşturmak için kullanılan yönteme bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="614cf-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="614cf-110">Aşağıdaki tablo, Visual Studio 2017 ve sonraki sürümleri kullanarak oluşturduğunuzda projeniz için varsayılan proje biçimini ve ilişkili CLI aracını gösterir.</span><span class="sxs-lookup"><span data-stu-id="614cf-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="614cf-111">Proje&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="614cf-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="614cf-112">Varsayılan proje biçimi</span><span class="sxs-lookup"><span data-stu-id="614cf-112">Default project format</span></span> | <span data-ttu-id="614cf-113">CLI aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="614cf-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="614cf-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="614cf-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="614cf-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="614cf-115">.NET Standard</span></span> | <span data-ttu-id="614cf-116">SDK stili</span><span class="sxs-lookup"><span data-stu-id="614cf-116">SDK-style</span></span> | [<span data-ttu-id="614cf-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="614cf-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="614cf-118">Visual Studio 2017 öncesinde oluşturulan projeler SDK tarzı değildir.</span><span class="sxs-lookup"><span data-stu-id="614cf-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="614cf-119">CLI'yi kullanın. `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="614cf-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="614cf-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="614cf-120">.NET Core</span></span> | <span data-ttu-id="614cf-121">SDK stili</span><span class="sxs-lookup"><span data-stu-id="614cf-121">SDK-style</span></span> | [<span data-ttu-id="614cf-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="614cf-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="614cf-123">Visual Studio 2017 öncesinde oluşturulan projeler SDK tarzı değildir.</span><span class="sxs-lookup"><span data-stu-id="614cf-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="614cf-124">CLI'yi kullanın. `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="614cf-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="614cf-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="614cf-125">.NET Framework</span></span> | <span data-ttu-id="614cf-126">SDK tarzı olmayan</span><span class="sxs-lookup"><span data-stu-id="614cf-126">Non-SDK-style</span></span> | [<span data-ttu-id="614cf-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="614cf-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="614cf-128">.DIĞER yöntemler kullanılarak oluşturulan NET Framework projeleri SDK tarzı projeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="614cf-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="614cf-129">Bunlar için [dotnet CLI'yi](../install-nuget-client-tools.md#dotnetexe-cli) kullanın.</span><span class="sxs-lookup"><span data-stu-id="614cf-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="614cf-130">[Geçirilen](../consume-packages/migrate-packages-config-to-package-reference.md) .NET projesi</span><span class="sxs-lookup"><span data-stu-id="614cf-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="614cf-131">SDK tarzı olmayan</span><span class="sxs-lookup"><span data-stu-id="614cf-131">Non-SDK-style</span></span>| <span data-ttu-id="614cf-132">Paket oluşturmak için, paketleri oluşturmak için [msbuild -t:pack'i](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) kullanın.</span><span class="sxs-lookup"><span data-stu-id="614cf-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="614cf-133">Paketleri oluşturmak `msbuild -t:pack` için, önerilir.</span><span class="sxs-lookup"><span data-stu-id="614cf-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="614cf-134">Aksi takdirde, [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)kullanın.</span><span class="sxs-lookup"><span data-stu-id="614cf-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="614cf-135">Geçirilen projeler SDK tarzı projeler değildir.</span><span class="sxs-lookup"><span data-stu-id="614cf-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="614cf-136">Proje biçimini denetleme</span><span class="sxs-lookup"><span data-stu-id="614cf-136">Check the project format</span></span>

<span data-ttu-id="614cf-137">Projenin SDK tarzı biçiminde olup olmadığından emin değilseniz, proje dosyasındaki `<Project>` öğedeki SDK özniteliğini arayın (C#, bu \*.csproj dosyasıdır).</span><span class="sxs-lookup"><span data-stu-id="614cf-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="614cf-138">Varsa, proje SDK tarzı bir projedir.</span><span class="sxs-lookup"><span data-stu-id="614cf-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="614cf-139">Visual Studio'da proje biçimini kontrol edin</span><span class="sxs-lookup"><span data-stu-id="614cf-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="614cf-140">Visual Studio'da çalışıyorsanız, aşağıdaki yöntemlerden birini kullanarak proje biçimini hızlı bir şekilde kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="614cf-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="614cf-141">Solution Explorer'da projeyi sağ tıklatın ve **myprojectname.csproj'u edin'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="614cf-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="614cf-142">Bu seçenek yalnızca Visual Studio 2017'den itibaren SDK stili özniteliği kullanan projeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="614cf-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="614cf-143">Aksi takdirde, diğer yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="614cf-143">Otherwise, use the other method.</span></span>

   ![Proje dosyasını düzenlemesi](media/edit-project-file.png)

   <span data-ttu-id="614cf-145">SDK tarzı bir proje, proje dosyasında [SDK özniteliğini](/dotnet/core/tools/csproj#additions) gösterir.</span><span class="sxs-lookup"><span data-stu-id="614cf-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="614cf-146">**Project** menüsünden **Project'i Boşalt'ı** seçin (veya projeyi sağ tıklatın ve **Project'i Boşalt'ı**seçin).</span><span class="sxs-lookup"><span data-stu-id="614cf-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="614cf-147">Bu proje, proje dosyasına SDK özniteliğini içermez.</span><span class="sxs-lookup"><span data-stu-id="614cf-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="614cf-148">Bu Bir SDK tarzı proje değildir.</span><span class="sxs-lookup"><span data-stu-id="614cf-148">It is not an SDK-style project.</span></span>

   ![Projeyi boşaltma](media/unload-project.png)

   <span data-ttu-id="614cf-150">Ardından, boşaltılan projeyi sağ tıklatın ve **myprojectname.csproj'u edit'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="614cf-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="614cf-151">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="614cf-151">See also</span></span>

- [<span data-ttu-id="614cf-152">dotnet CLI ile .NET Standart Paketleri Oluşturun</span><span class="sxs-lookup"><span data-stu-id="614cf-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="614cf-153">Visual Studio ile .NET Standart Paketleri Oluşturun</span><span class="sxs-lookup"><span data-stu-id="614cf-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="614cf-154">Bir .NET Framework paketi oluşturma ve yayımla (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="614cf-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="614cf-155">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="614cf-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
