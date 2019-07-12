---
title: Proje biçimi tanımlayın
description: Kimlik için projenizi biçimini açıklar
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843520"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="93991-103">Proje biçimi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="93991-103">Identify the project format</span></span>

<span data-ttu-id="93991-104">NuGet tüm .NET projeleriyle çalışır.</span><span class="sxs-lookup"><span data-stu-id="93991-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="93991-105">Ancak, proje biçimi (SDK stilinde veya SDK stilinde olmayan) bazı araçlar ve kullanmak ve NuGet paketleri oluşturmak için kullanmanız gereken yöntemleri belirler.</span><span class="sxs-lookup"><span data-stu-id="93991-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="93991-106">SDK stili projeleri kullanmak [SDK özniteliği](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="93991-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="93991-107">Kullanma ve NuGet paketleri oluşturmak için kullandığınız araçları ve yöntemleri üzerinde proje biçimi bağımlı olduğundan, proje türünü tanımlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="93991-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="93991-108">SDK stili projeleri için Araçlar ve yöntemler de bağımlı olup olmadığını proje için geçirilmiş olan üzerinde `PackageReference` biçimi.</span><span class="sxs-lookup"><span data-stu-id="93991-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="93991-109">Projenize SDK stilinde olup, projeyi oluşturmak için kullandığınız yönteme bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="93991-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="93991-110">Visual Studio 2017 ve sonraki sürümler kullanarak oluşturduğunuzda varsayılan proje biçimi ve ilişkili CLI aracı projeniz için aşağıdaki tabloda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="93991-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="93991-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="93991-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="93991-112">Varsayılan proje biçimi</span><span class="sxs-lookup"><span data-stu-id="93991-112">Default project format</span></span> | <span data-ttu-id="93991-113">CLI aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="93991-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="93991-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="93991-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="93991-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="93991-115">.NET Standard</span></span> | <span data-ttu-id="93991-116">SDK stili</span><span class="sxs-lookup"><span data-stu-id="93991-116">SDK-style</span></span> | [<span data-ttu-id="93991-117">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="93991-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="93991-118">Visual Studio 2017'den önce oluşturulan projeleri olmayan-SDK-style ' dir.</span><span class="sxs-lookup"><span data-stu-id="93991-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="93991-119">Kullanım `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="93991-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="93991-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="93991-120">.NET Core</span></span> | <span data-ttu-id="93991-121">SDK stili</span><span class="sxs-lookup"><span data-stu-id="93991-121">SDK-style</span></span> | [<span data-ttu-id="93991-122">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="93991-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="93991-123">Visual Studio 2017'den önce oluşturulan projeleri olmayan-SDK-style ' dir.</span><span class="sxs-lookup"><span data-stu-id="93991-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="93991-124">Kullanım `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="93991-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="93991-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="93991-125">.NET Framework</span></span> | <span data-ttu-id="93991-126">SDK stili</span><span class="sxs-lookup"><span data-stu-id="93991-126">Non-SDK-style</span></span> | [<span data-ttu-id="93991-127">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="93991-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="93991-128">Diğer yöntemleri kullanarak oluşturulan .NET framework projeleri SDK stili projeleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="93991-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="93991-129">Bu, [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) yerine.</span><span class="sxs-lookup"><span data-stu-id="93991-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="93991-130">[Geçirilen](../reference/migrate-packages-config-to-package-reference.md) .NET projesi</span><span class="sxs-lookup"><span data-stu-id="93991-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="93991-131">SDK stili</span><span class="sxs-lookup"><span data-stu-id="93991-131">Non-SDK-style</span></span>| <span data-ttu-id="93991-132">Paket oluşturmak üzere kullanmak [msbuild - t: paketi](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) paketleri oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="93991-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="93991-133">Paket oluşturmayı `msbuild -t:pack` önerilir.</span><span class="sxs-lookup"><span data-stu-id="93991-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="93991-134">Aksi takdirde kullanın [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="93991-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="93991-135">Geçirilen proje SDK stili projeleri değildir.</span><span class="sxs-lookup"><span data-stu-id="93991-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="93991-136">Proje biçimini denetleyin</span><span class="sxs-lookup"><span data-stu-id="93991-136">Check the project format</span></span>

<span data-ttu-id="93991-137">Proje SDK stilinde biçim olup olmadığından emin değilseniz SDK'sı özniteliğinde arayın `<Project>` öğesi proje dosyasında (için C#, bu \*.csproj dosyasıdır).</span><span class="sxs-lookup"><span data-stu-id="93991-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="93991-138">Varsa, projeye bir SDK stilinde bir projedir.</span><span class="sxs-lookup"><span data-stu-id="93991-138">If it is present, the project is an SDK-style project.</span></span>

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

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="93991-139">Visual Studio'da proje biçimini denetleyin</span><span class="sxs-lookup"><span data-stu-id="93991-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="93991-140">Visual Studio'da çalışıyorsanız, aşağıdaki yöntemlerden birini kullanarak proje biçimi hızlı bir şekilde denetleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="93991-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="93991-141">Çözüm Gezgini'nde projeye sağ tıklayıp **myprojectname.csproj Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="93991-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="93991-142">Bu seçenek, yalnızca SDK stilinde öznitelik kullanan projeler için Visual Studio 2017'de başlayarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="93991-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="93991-143">Aksi takdirde, diğer bir yöntem kullanın.</span><span class="sxs-lookup"><span data-stu-id="93991-143">Otherwise, use the other method.</span></span>

   ![Proje dosyası Düzenle](media/edit-project-file.png)

   <span data-ttu-id="93991-145">SDK stili projeyi gösteren [SDK özniteliği](/dotnet/core/tools/csproj#additions) proje dosyasındaki.</span><span class="sxs-lookup"><span data-stu-id="93991-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="93991-146">Gelen **proje** menüsünde seçin **projeyi** (veya projeye sağ tıklayıp seçin **projeyi**).</span><span class="sxs-lookup"><span data-stu-id="93991-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="93991-147">Bu proje, proje dosyasında SDK özniteliği içermeyecek.</span><span class="sxs-lookup"><span data-stu-id="93991-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="93991-148">SDK stili projesi değil.</span><span class="sxs-lookup"><span data-stu-id="93991-148">It is not an SDK-style project.</span></span>

   ![Projeyi](media/unload-project.png)

   <span data-ttu-id="93991-150">Ardından bellekten projeye sağ tıklayın ve seçin **myprojectname.csproj Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="93991-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="93991-151">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="93991-151">See also</span></span>

- [<span data-ttu-id="93991-152">Dotnet CLI ile .NET standart paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="93991-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="93991-153">Visual Studio ile .NET standart paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="93991-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="93991-154">.NET Framework paketi (Visual Studio) oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="93991-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="93991-155">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="93991-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
