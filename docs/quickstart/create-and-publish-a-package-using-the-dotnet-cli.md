---
title: DotNet CLı kullanarak bir NuGet paketi oluşturma ve yayımlama
description: .NET Core CLI, DotNet kullanarak bir NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231311"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="6e669-103">Hızlı başlangıç: paket oluşturma ve yayımlama (DotNet CLı)</span><span class="sxs-lookup"><span data-stu-id="6e669-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="6e669-104">.NET sınıf kitaplığından bir NuGet paketi oluşturmak ve `dotnet` komut satırı arabirimi (CLı) kullanarak nuget.org 'de yayımlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="6e669-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e669-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6e669-105">Prerequisites</span></span>

1. <span data-ttu-id="6e669-106">`dotnet` CLı 'yi içeren [.NET Core SDK](https://www.microsoft.com/net/download/)'yi yükler.</span><span class="sxs-lookup"><span data-stu-id="6e669-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="6e669-107">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="6e669-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="6e669-108">Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .</span><span class="sxs-lookup"><span data-stu-id="6e669-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="6e669-109">Yeni hesap oluşturma onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="6e669-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="6e669-110">Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e669-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="6e669-111">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e669-111">Create a class library project</span></span>

<span data-ttu-id="6e669-112">Paketlemek istediğiniz kod için mevcut bir .NET sınıf kitaplığı projesi kullanabilir veya basit bir tane aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e669-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="6e669-113">`AppLogger`adlı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6e669-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="6e669-114">Bir komut istemi açın ve `AppLogger` klasöre geçin.</span><span class="sxs-lookup"><span data-stu-id="6e669-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="6e669-115">Proje için geçerli klasörün adını kullanan `dotnet new classlib`yazın.</span><span class="sxs-lookup"><span data-stu-id="6e669-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="6e669-116">Bu, yeni projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e669-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="6e669-117">Proje dosyasına paket meta verileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="6e669-117">Add package metadata to the project file</span></span>

<span data-ttu-id="6e669-118">Her NuGet paketinin, paketin içeriğini ve bağımlılıklarını açıklayan bir bildirime ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="6e669-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="6e669-119">Son bir pakette bildirim, proje dosyasına dahil ettiğiniz NuGet meta verileri özelliklerinden oluşturulan bir `.nuspec` dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6e669-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="6e669-120">Proje dosyanızı (`.csproj`) açın ve mevcut `<PropertyGroup>` etiketinin içine aşağıdaki en az özellikleri ekleyerek değerleri uygun şekilde değiştirerek:</span><span class="sxs-lookup"><span data-stu-id="6e669-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="6e669-121">Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="6e669-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="6e669-122">Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).</span><span class="sxs-lookup"><span data-stu-id="6e669-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="6e669-123">[NuGet meta veri özelliklerinde](/dotnet/core/tools/csproj#nuget-metadata-properties)açıklanan isteğe bağlı özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e669-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="6e669-124">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6e669-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="6e669-125">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="6e669-125">Run the pack command</span></span>

<span data-ttu-id="6e669-126">Projeden bir NuGet paketi (`.nupkg` dosyası) oluşturmak için, Ayrıca projeyi otomatik olarak oluşturan `dotnet pack` komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6e669-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="6e669-127">Çıktı `.nupkg` dosyanın yolunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="6e669-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="6e669-128">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="6e669-128">Automatically generate package on build</span></span>

<span data-ttu-id="6e669-129">`dotnet build`çalıştırdığınızda `dotnet pack` otomatik olarak çalıştırmak için, aşağıdaki satırı `<PropertyGroup>`içindeki proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6e669-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="6e669-130">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="6e669-130">Publish the package</span></span>

<span data-ttu-id="6e669-131">Bir `.nupkg` dosyasına sahip olduktan sonra, nuget.org komutunu `dotnet nuget push` kullanarak, nuget.org ' den alınan bir API anahtarı ile birlikte bu dosyayı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6e669-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="6e669-132">API anahtarınızı alın</span><span class="sxs-lookup"><span data-stu-id="6e669-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="6e669-133">DotNet NuGet Push ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="6e669-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="6e669-134">Yayımlama hataları</span><span class="sxs-lookup"><span data-stu-id="6e669-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="6e669-135">Yayınlanan paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="6e669-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="6e669-136">İlgili video</span><span class="sxs-lookup"><span data-stu-id="6e669-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="6e669-137">[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.</span><span class="sxs-lookup"><span data-stu-id="6e669-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e669-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e669-138">Next steps</span></span>

<span data-ttu-id="6e669-139">İlk NuGet paketinizi oluştururken Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6e669-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6e669-140">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e669-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="6e669-141">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="6e669-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="6e669-142">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="6e669-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="6e669-143">Yayın öncesi paketler</span><span class="sxs-lookup"><span data-stu-id="6e669-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="6e669-144">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="6e669-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="6e669-145">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e669-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="6e669-146">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e669-146">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="6e669-147">Sembol paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e669-147">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="6e669-148">İmzalama paketleri</span><span class="sxs-lookup"><span data-stu-id="6e669-148">Signing packages</span></span>](../create-packages/Sign-a-package.md)
