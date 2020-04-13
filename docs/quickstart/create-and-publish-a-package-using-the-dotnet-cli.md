---
title: Dotnet CLI'yi kullanarak bir NuGet paketi oluşturun ve yayımlayın
description: .NET Core CLI, dotnet kullanarak bir NuGet paketi oluşturma ve yayımlama hakkında bir iz geçidi öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231311"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="54c75-103">Quickstart: Bir paket oluşturma ve yayımlama (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="54c75-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="54c75-104">Bir .NET Sınıf Kitaplığı'ndan bir NuGet paketi oluşturmak ve `dotnet` komut satırı arabirimini (CLI) kullanarak nuget.org yayınlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="54c75-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54c75-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="54c75-105">Prerequisites</span></span>

1. <span data-ttu-id="54c75-106">CLI'yi içeren [.NET Core SDK'yı](https://www.microsoft.com/net/download/)yükleyin. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="54c75-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="54c75-107">Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="54c75-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="54c75-108">Zaten bir hesabınız yoksa [nuget.org ücretsiz bir hesaba kaydolun.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)</span><span class="sxs-lookup"><span data-stu-id="54c75-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="54c75-109">Yeni bir hesap oluşturmak bir onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="54c75-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="54c75-110">Bir paket yükleyemeden önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54c75-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="54c75-111">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54c75-111">Create a class library project</span></span>

<span data-ttu-id="54c75-112">Paketlemek istediğiniz kod için varolan bir .NET Sınıf Kitaplığı projesini kullanabilir veya aşağıdaki gibi basit bir kitap oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="54c75-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="54c75-113">'li bir `AppLogger`klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54c75-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="54c75-114">Komut istemini açın ve `AppLogger` klasöre geçin.</span><span class="sxs-lookup"><span data-stu-id="54c75-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="54c75-115">Proje `dotnet new classlib`için geçerli klasörün adını kullanan türü yazın.</span><span class="sxs-lookup"><span data-stu-id="54c75-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="54c75-116">Bu, yeni projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54c75-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="54c75-117">Proje dosyasına paket meta verisi ekleme</span><span class="sxs-lookup"><span data-stu-id="54c75-117">Add package metadata to the project file</span></span>

<span data-ttu-id="54c75-118">Her NuGet paketinin paketin içeriğini ve bağımlılıklarını açıklayan bir bildirime ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="54c75-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="54c75-119">Son pakette, bildirim proje `.nuspec` dosyasına eklediğiniz NuGet meta veri özelliklerinden oluşturulan bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="54c75-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="54c75-120">Proje dosyanızı`.csproj`açın ( ) ve aşağıdaki `<PropertyGroup>` en az özellikleri varolan etiketin içine ekleyerek değerleri uygun şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="54c75-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="54c75-121">Pakete, nuget.org veya kullandığınız ana bilgisayarda benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="54c75-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="54c75-122">Bu izlenecek yol için, daha sonraki yayımlama adımı paketi herkese açık hale getirebildiğinden (kimsenin gerçekten kullanması pek olası olmasa da) adına "Örnek" veya "Test" eklenmesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="54c75-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="54c75-123">[NuGet meta veri özelliklerinde](/dotnet/core/tools/csproj#nuget-metadata-properties)açıklanan isteğe bağlı özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="54c75-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="54c75-124">Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **PackageTags** özelliğine özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="54c75-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="54c75-125">Sürü komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="54c75-125">Run the pack command</span></span>

<span data-ttu-id="54c75-126">Projeden bir NuGet `.nupkg` paketi (dosya) oluşturmak `dotnet pack` için, projeyi otomatik olarak oluşturan komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="54c75-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="54c75-127">`.nupkg` Çıktı, dosyaya giden yolu gösterir:</span><span class="sxs-lookup"><span data-stu-id="54c75-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="54c75-128">Otomatik olarak yapı üzerinde paket oluşturmak</span><span class="sxs-lookup"><span data-stu-id="54c75-128">Automatically generate package on build</span></span>

<span data-ttu-id="54c75-129">Çalıştırdığınızda `dotnet pack` `dotnet build`otomatik olarak çalıştırmak için proje dosyanıza `<PropertyGroup>`aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="54c75-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="54c75-130">Paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="54c75-130">Publish the package</span></span>

<span data-ttu-id="54c75-131">Bir `.nupkg` dosyaya sahip olduktan sonra, nuget.org'dan edinilen bir API anahtarıyla birlikte komutu kullanarak dosyayı `dotnet nuget push` nuget.org yayımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="54c75-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="54c75-132">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="54c75-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="54c75-133">dotnet nuget push ile yayımla</span><span class="sxs-lookup"><span data-stu-id="54c75-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="54c75-134">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="54c75-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="54c75-135">Yayımlanmış paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="54c75-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="54c75-136">İlgili video</span><span class="sxs-lookup"><span data-stu-id="54c75-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="54c75-137">[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.</span><span class="sxs-lookup"><span data-stu-id="54c75-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54c75-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54c75-138">Next steps</span></span>

<span data-ttu-id="54c75-139">İlk NuGet paketinizi oluşturduğunuz için tebrikler!</span><span class="sxs-lookup"><span data-stu-id="54c75-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="54c75-140">Paket Oluşturma</span><span class="sxs-lookup"><span data-stu-id="54c75-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="54c75-141">NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="54c75-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="54c75-142">Paket Yayınlama</span><span class="sxs-lookup"><span data-stu-id="54c75-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="54c75-143">Ön Sürüm Paketleri</span><span class="sxs-lookup"><span data-stu-id="54c75-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="54c75-144">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="54c75-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="54c75-145">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="54c75-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="54c75-146">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="54c75-146">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="54c75-147">Sembol paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="54c75-147">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="54c75-148">İmzalama paketleri</span><span class="sxs-lookup"><span data-stu-id="54c75-148">Signing packages</span></span>](../create-packages/Sign-a-package.md)
