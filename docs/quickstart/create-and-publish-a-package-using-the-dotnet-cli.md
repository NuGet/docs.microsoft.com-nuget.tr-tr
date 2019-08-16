---
title: DotNet CLı kullanarak bir NuGet paketi oluşturma ve yayımlama
description: .NET Core CLI, DotNet kullanarak bir NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c0e6de2c3b9978538d504f4af6e744ece43b4a4d
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488942"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="ebd86-103">Hızlı Başlangıç: Paket oluşturma ve yayımlama (DotNet CLı)</span><span class="sxs-lookup"><span data-stu-id="ebd86-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="ebd86-104">.NET sınıf kitaplığından bir NuGet paketi oluşturmak ve `dotnet` komut satırı arabirimini (CLI) kullanarak NuGet.org 'de yayımlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ebd86-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebd86-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ebd86-105">Prerequisites</span></span>

1. <span data-ttu-id="ebd86-106">`dotnet` CLI içeren [.NET Core SDK](https://www.microsoft.com/net/download/)' yi yükler.</span><span class="sxs-lookup"><span data-stu-id="ebd86-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="ebd86-107">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ebd86-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="ebd86-108">Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .</span><span class="sxs-lookup"><span data-stu-id="ebd86-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="ebd86-109">Yeni hesap oluşturma onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="ebd86-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ebd86-110">Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebd86-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="ebd86-111">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebd86-111">Create a class library project</span></span>

<span data-ttu-id="ebd86-112">Paketlemek istediğiniz kod için mevcut bir .NET sınıf kitaplığı projesi kullanabilir veya basit bir tane aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ebd86-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="ebd86-113">Adlı `AppLogger`bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ebd86-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="ebd86-114">Bir komut istemi açın ve `AppLogger` klasöre geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="ebd86-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="ebd86-115">Proje `dotnet new classlib`için geçerli klasörün adını kullanan türü.</span><span class="sxs-lookup"><span data-stu-id="ebd86-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="ebd86-116">Bu, yeni projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ebd86-116">This creates the new project.</span></span>

1. <span data-ttu-id="ebd86-117">Uygulamanın `dotnet run` düzgün şekilde oluşturulduğunu test etmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ebd86-117">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="ebd86-118">Proje dosyasına paket meta verileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="ebd86-118">Add package metadata to the project file</span></span>

<span data-ttu-id="ebd86-119">Her NuGet paketinin, paketin içeriğini ve bağımlılıklarını açıklayan bir bildirime ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="ebd86-119">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="ebd86-120">Son bir pakette bildirim, proje dosyasına dahil ettiğiniz `.nuspec` NuGet meta verileri özelliklerinden oluşturulan bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="ebd86-120">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="ebd86-121">Proje dosyanızı (`.csproj`) açın ve mevcut `<PropertyGroup>` etiketin içine aşağıdaki en az özellikleri ekleyerek değerleri uygun şekilde değiştirerek:</span><span class="sxs-lookup"><span data-stu-id="ebd86-121">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="ebd86-122">Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="ebd86-122">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="ebd86-123">Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).</span><span class="sxs-lookup"><span data-stu-id="ebd86-123">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="ebd86-124">[NuGet meta veri özelliklerinde](/dotnet/core/tools/csproj#nuget-metadata-properties)açıklanan isteğe bağlı özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ebd86-124">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="ebd86-125">Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ebd86-125">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ebd86-126">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ebd86-126">Run the pack command</span></span>

<span data-ttu-id="ebd86-127">Projeden bir NuGet paketi (bir `.nupkg` dosya) oluşturmak için `dotnet pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ebd86-127">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="ebd86-128">Çıktı, `.nupkg` dosyanın yolunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="ebd86-128">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="ebd86-129">Derleme üzerinde otomatik olarak paket oluştur</span><span class="sxs-lookup"><span data-stu-id="ebd86-129">Automatically generate package on build</span></span>

<span data-ttu-id="ebd86-130">`<PropertyGroup>`Çalıştırdığınızda `dotnet pack` otomatikolarakçalıştırmakiçin,aşağıdakisatırıiçindeki`dotnet build`proje dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ebd86-130">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="ebd86-131">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="ebd86-131">Publish the package</span></span>

<span data-ttu-id="ebd86-132">Bir `.nupkg` dosyaya sahip olduktan sonra, NuGet.org. NuGet.org ' den alınan bir `dotnet nuget push` API anahtarı ile birlikte komutunu kullanarak bu dosyayı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ebd86-132">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="ebd86-133">API anahtarınızı alın</span><span class="sxs-lookup"><span data-stu-id="ebd86-133">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="ebd86-134">DotNet NuGet Push ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="ebd86-134">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="ebd86-135">Yayımlama hataları</span><span class="sxs-lookup"><span data-stu-id="ebd86-135">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="ebd86-136">Yayınlanan paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="ebd86-136">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="ebd86-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ebd86-137">Next steps</span></span>

<span data-ttu-id="ebd86-138">İlk NuGet paketinizi oluştururken Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ebd86-138">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ebd86-139">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebd86-139">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="ebd86-140">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="ebd86-140">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="ebd86-141">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="ebd86-141">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="ebd86-142">Yayın öncesi paketler</span><span class="sxs-lookup"><span data-stu-id="ebd86-142">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="ebd86-143">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="ebd86-143">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="ebd86-144">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebd86-144">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="ebd86-145">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebd86-145">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ebd86-146">Sembol paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ebd86-146">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="ebd86-147">İmzalama paketleri</span><span class="sxs-lookup"><span data-stu-id="ebd86-147">Signing packages</span></span>](../create-packages/Sign-a-package.md)
