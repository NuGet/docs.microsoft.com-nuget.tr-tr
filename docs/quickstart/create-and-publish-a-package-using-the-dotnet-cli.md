---
title: DotNet CLı kullanarak bir NuGet paketi oluşturma ve yayımlama
description: .NET Core CLI, DotNet kullanarak bir NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 30a77b427fe0a33b41262c5784045e5a6b10852f
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419989"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="ecdb6-103">Hızlı Başlangıç: Paket oluşturma ve yayımlama (DotNet CLı)</span><span class="sxs-lookup"><span data-stu-id="ecdb6-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="ecdb6-104">.NET sınıf kitaplığından bir NuGet paketi oluşturmak ve `dotnet` komut satırı arabirimini (CLI) kullanarak NuGet.org 'de yayımlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecdb6-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ecdb6-105">Prerequisites</span></span>

1. <span data-ttu-id="ecdb6-106">`dotnet` CLI içeren [.NET Core SDK](https://www.microsoft.com/net/download/)' yi yükler.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="ecdb6-107">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="ecdb6-108">Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .</span><span class="sxs-lookup"><span data-stu-id="ecdb6-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="ecdb6-109">Yeni hesap oluşturma onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ecdb6-110">Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="ecdb6-111">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecdb6-111">Create a class library project</span></span>

<span data-ttu-id="ecdb6-112">Paketlemek istediğiniz kod için mevcut bir .NET sınıf kitaplığı projesi kullanabilir veya basit bir tane aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ecdb6-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="ecdb6-113">Adlı `AppLogger` bir klasör oluşturun ve içine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="ecdb6-114">Proje için geçerli klasörün `dotnet new classlib`adını kullanan öğesini kullanarak projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="ecdb6-115">Proje dosyasına paket meta verileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="ecdb6-115">Add package metadata to the project file</span></span>

<span data-ttu-id="ecdb6-116">Her NuGet paketinin, paketin içeriğini ve bağımlılıklarını açıklayan bir bildirime ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="ecdb6-117">Son bir pakette bildirim, proje dosyasına dahil ettiğiniz `.nuspec` NuGet meta verileri özelliklerinden oluşturulan bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="ecdb6-118">Proje dosyanızı (`.csproj`) açın ve mevcut `<PropertyGroup>` etiketin içine aşağıdaki en az özellikleri ekleyerek değerleri uygun şekilde değiştirerek:</span><span class="sxs-lookup"><span data-stu-id="ecdb6-118">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="ecdb6-119">Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="ecdb6-120">Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).</span><span class="sxs-lookup"><span data-stu-id="ecdb6-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="ecdb6-121">[NuGet meta veri özelliklerinde](/dotnet/core/tools/csproj#nuget-metadata-properties)açıklanan isteğe bağlı özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="ecdb6-122">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ecdb6-123">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ecdb6-123">Run the pack command</span></span>

<span data-ttu-id="ecdb6-124">Projeden bir NuGet paketi (bir `.nupkg` dosya) oluşturmak için `dotnet pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ecdb6-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="ecdb6-125">Çıktı, `.nupkg` dosyanın yolunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="ecdb6-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="ecdb6-126">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="ecdb6-126">Automatically generate package on build</span></span>

<span data-ttu-id="ecdb6-127">`<PropertyGroup>`Çalıştırdığınızda `dotnet pack` otomatikolarakçalıştırmakiçin,aşağıdakisatırıiçindeki`dotnet build`proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ecdb6-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="ecdb6-128">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="ecdb6-128">Publish the package</span></span>

<span data-ttu-id="ecdb6-129">Bir `.nupkg` dosyaya sahip olduktan sonra, NuGet.org. NuGet.org ' den alınan bir `dotnet nuget push` API anahtarı ile birlikte komutunu kullanarak bu dosyayı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="ecdb6-130">API anahtarınızı alın</span><span class="sxs-lookup"><span data-stu-id="ecdb6-130">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="ecdb6-131">DotNet NuGet Push ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="ecdb6-131">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="ecdb6-132">Yayımlama hataları</span><span class="sxs-lookup"><span data-stu-id="ecdb6-132">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="ecdb6-133">Yayınlanan paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="ecdb6-133">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="ecdb6-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ecdb6-134">Next steps</span></span>

<span data-ttu-id="ecdb6-135">İlk NuGet paketinizi oluştururken Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ecdb6-135">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ecdb6-136">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecdb6-136">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="ecdb6-137">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="ecdb6-137">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="ecdb6-138">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="ecdb6-138">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="ecdb6-139">Yayın öncesi paketler</span><span class="sxs-lookup"><span data-stu-id="ecdb6-139">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="ecdb6-140">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="ecdb6-140">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="ecdb6-141">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecdb6-141">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ecdb6-142">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecdb6-142">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ecdb6-143">Sembol paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecdb6-143">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="ecdb6-144">İmzalama paketleri</span><span class="sxs-lookup"><span data-stu-id="ecdb6-144">Signing packages</span></span>](../create-packages/Sign-a-package.md)
