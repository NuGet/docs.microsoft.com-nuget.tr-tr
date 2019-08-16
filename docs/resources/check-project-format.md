---
title: Proje biçimini tanımla
description: Proje biçiminizi nasıl kullanacağınızı açıklar
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488488"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="3b59a-103">Proje biçimini tanımla</span><span class="sxs-lookup"><span data-stu-id="3b59a-103">Identify the project format</span></span>

<span data-ttu-id="3b59a-104">NuGet tüm .NET projeleriyle birlikte çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b59a-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="3b59a-105">Ancak, proje biçimi (SDK stili veya SDK olmayan stili), NuGet paketlerini tüketmek ve oluşturmak için kullanmanız gereken bazı araç ve yöntemleri belirler.</span><span class="sxs-lookup"><span data-stu-id="3b59a-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="3b59a-106">SDK stili projeler [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanır.</span><span class="sxs-lookup"><span data-stu-id="3b59a-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="3b59a-107">NuGet paketlerini tüketmek ve oluşturmak için kullandığınız yöntemler ve araçlar proje biçimine bağlı olduğundan, proje türünü tanımlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="3b59a-108">SDK olmayan stil projeleri için, Yöntemler ve araçlar projenin `PackageReference` biçime geçirilme biçimine de bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3b59a-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="3b59a-109">Projenizin SDK stili olup olmadığı veya proje oluşturmak için kullanılan yönteme bağlı olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="3b59a-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="3b59a-110">Aşağıdaki tabloda, Visual Studio 2017 ve sonraki sürümlerini kullanarak oluşturduğunuzda projeniz için varsayılan proje biçimi ve ilişkili CLı aracı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="3b59a-111">Proje&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="3b59a-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="3b59a-112">Varsayılan proje biçimi</span><span class="sxs-lookup"><span data-stu-id="3b59a-112">Default project format</span></span> | <span data-ttu-id="3b59a-113">CLı aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="3b59a-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="3b59a-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="3b59a-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="3b59a-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="3b59a-115">.NET Standard</span></span> | <span data-ttu-id="3b59a-116">SDK stili</span><span class="sxs-lookup"><span data-stu-id="3b59a-116">SDK-style</span></span> | [<span data-ttu-id="3b59a-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="3b59a-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="3b59a-118">Visual Studio 2017 ' den önce oluşturulan projeler SDK olmayan stillerdir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="3b59a-119">CLI `nuget.exe` kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b59a-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="3b59a-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3b59a-120">.NET Core</span></span> | <span data-ttu-id="3b59a-121">SDK stili</span><span class="sxs-lookup"><span data-stu-id="3b59a-121">SDK-style</span></span> | [<span data-ttu-id="3b59a-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="3b59a-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="3b59a-123">Visual Studio 2017 ' den önce oluşturulan projeler SDK olmayan stillerdir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="3b59a-124">CLI `nuget.exe` kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b59a-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="3b59a-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3b59a-125">.NET Framework</span></span> | <span data-ttu-id="3b59a-126">SDK olmayan stil</span><span class="sxs-lookup"><span data-stu-id="3b59a-126">Non-SDK-style</span></span> | [<span data-ttu-id="3b59a-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="3b59a-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="3b59a-128">Diğer yöntemler kullanılarak oluşturulan .NET Framework projeleri SDK stilinde projeler olabilir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="3b59a-129">Bunlar için bunun yerine [DotNet CLI](../install-nuget-client-tools.md#dotnetexe-cli) kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b59a-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="3b59a-130">[Geçirilen](../consume-packages/migrate-packages-config-to-package-reference.md) .NET projesi</span><span class="sxs-lookup"><span data-stu-id="3b59a-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="3b59a-131">SDK olmayan stil</span><span class="sxs-lookup"><span data-stu-id="3b59a-131">Non-SDK-style</span></span>| <span data-ttu-id="3b59a-132">Paket oluşturmak için, paketler oluşturmak üzere [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b59a-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="3b59a-133">Paket `msbuild -t:pack` oluşturmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="3b59a-134">Aksi takdirde, [DotNet CLI](../install-nuget-client-tools.md#dotnetexe-cli)kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b59a-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="3b59a-135">Geçirilen projeler SDK stilinde projeler değildir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="3b59a-136">Proje biçimini denetle</span><span class="sxs-lookup"><span data-stu-id="3b59a-136">Check the project format</span></span>

<span data-ttu-id="3b59a-137">Projenin SDK stili biçim olup olmadığı konusunda emin değilseniz, proje dosyasındaki `<Project>` öğesinde SDK özniteliğini arayın (için C#, bu, \*. csproj dosyasıdır).</span><span class="sxs-lookup"><span data-stu-id="3b59a-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="3b59a-138">Varsa, proje bir SDK stili projem olur.</span><span class="sxs-lookup"><span data-stu-id="3b59a-138">If it is present, the project is an SDK-style project.</span></span>

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

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="3b59a-139">Visual Studio 'da proje biçimini denetleme</span><span class="sxs-lookup"><span data-stu-id="3b59a-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="3b59a-140">Visual Studio 'da çalışıyorsanız, aşağıdaki yöntemlerden birini kullanarak proje biçimini hızlıca kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3b59a-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="3b59a-141">Çözüm Gezgini projeye sağ tıklayın ve **MyProjectName. csproj Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3b59a-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="3b59a-142">Bu seçenek yalnızca SDK stili özniteliği kullanan projeler için Visual Studio 2017 ' den itibaren kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="3b59a-143">Aksi takdirde, diğer yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b59a-143">Otherwise, use the other method.</span></span>

   ![Proje dosyasını düzenleme](media/edit-project-file.png)

   <span data-ttu-id="3b59a-145">SDK stili bir proje, proje dosyasında [SDK özniteliğini](/dotnet/core/tools/csproj#additions) gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="3b59a-146">**Proje** menüsünden **Projeyi Kaldır** ' ı seçin (veya projeye sağ tıklayıp **Projeyi Kaldır**' ı seçin).</span><span class="sxs-lookup"><span data-stu-id="3b59a-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="3b59a-147">Bu proje, proje dosyasında SDK özniteliğini içermez.</span><span class="sxs-lookup"><span data-stu-id="3b59a-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="3b59a-148">Bu bir SDK stili proje değildir.</span><span class="sxs-lookup"><span data-stu-id="3b59a-148">It is not an SDK-style project.</span></span>

   ![Projeyi Kaldır](media/unload-project.png)

   <span data-ttu-id="3b59a-150">Ardından, yüklenmeyen projeye sağ tıklayın ve **MyProjectName. csproj öğesini Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3b59a-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="3b59a-151">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3b59a-151">See also</span></span>

- [<span data-ttu-id="3b59a-152">DotNet CLı ile .NET Standard paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b59a-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="3b59a-153">Visual Studio ile .NET Standard paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="3b59a-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="3b59a-154">.NET Framework paketi oluşturma ve yayımlama (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3b59a-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="3b59a-155">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="3b59a-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
