---
title: Oluşturma ve yayımlama dotnet CLI kullanarak bir NuGet paketi
description: Oluşturma ve yayımlama dotnet .NET Core CLI kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 051fcc355fb78c0ab208125c2295b6316236fd46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426356"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="2b5fa-103">Hızlı Başlangıç: Bir paketi (dotnet CLI) oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="2b5fa-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="2b5fa-104">Bir .NET sınıf kitaplığı'ndan bir NuGet paketi oluşturmak ve nuget.org kullanarak yayımlamak için basit bir işlemdir `dotnet` komut satırı arabirimi (CLI).</span><span class="sxs-lookup"><span data-stu-id="2b5fa-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b5fa-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2b5fa-105">Prerequisites</span></span>

1. <span data-ttu-id="2b5fa-106">Yükleme [.NET Core SDK'sı](https://www.microsoft.com/net/download/), içeren `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="2b5fa-107">[Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="2b5fa-108">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2b5fa-109">Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2b5fa-110">Bir sınıf kitaplığı projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="2b5fa-110">Create a class library project</span></span>

<span data-ttu-id="2b5fa-111">Mevcut bir .NET sınıf kitaplığı projesi paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2b5fa-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2b5fa-112">Adlı bir klasör oluşturun `AppLogger` ve içine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="2b5fa-113">Kullanarak proje oluşturduğunuzda `dotnet new classlib`, proje için geçerli klasörün adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="2b5fa-114">Paket meta verileri proje dosyasına ekleyin</span><span class="sxs-lookup"><span data-stu-id="2b5fa-114">Add package metadata to the project file</span></span>

<span data-ttu-id="2b5fa-115">Her bir NuGet paketi paketin içeriği ve bağımlılıkları tanımlayan bir bildirim gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="2b5fa-116">Son bir pakette bildirimidir bir `.nuspec` proje dosyasına eklenecek NuGet meta verileri özelliklerinden oluşturulan dosya.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="2b5fa-117">Proje dosyanızı açın (`.csproj`) ve mevcut içinde en az aşağıdaki özellikleri ekleyin `<PropertyGroup>` değerleri uygun şekilde değiştirerek etiketi:</span><span class="sxs-lookup"><span data-stu-id="2b5fa-117">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="2b5fa-118">Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket verin.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2b5fa-119">Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="2b5fa-120">Üzerinde tanımlanan herhangi bir isteğe bağlı özellikler Ekle [NuGet meta veri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="2b5fa-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="2b5fa-121">Ortak tüketim için oluşturulan paketler için özel dikkat **PackageTags** özelliği olarak etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2b5fa-122">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2b5fa-122">Run the pack command</span></span>

<span data-ttu-id="2b5fa-123">Bir NuGet paketi oluşturmak için (bir `.nupkg` dosya) projeden çalıştırma `dotnet pack` komutu ayrıca projeyi otomatik olarak oluşturur:</span><span class="sxs-lookup"><span data-stu-id="2b5fa-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="2b5fa-124">Çıktı yolu gösterir `.nupkg` dosyası:</span><span class="sxs-lookup"><span data-stu-id="2b5fa-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="2b5fa-125">Derleme paketi otomatik olarak oluştur</span><span class="sxs-lookup"><span data-stu-id="2b5fa-125">Automatically generate package on build</span></span>

<span data-ttu-id="2b5fa-126">Otomatik olarak çalışacak şekilde `dotnet pack` çalıştırdığınızda `dotnet build`, proje dosyanızın aşağıdaki satırı ekleyin `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="2b5fa-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="2b5fa-127">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="2b5fa-127">Publish the package</span></span>

<span data-ttu-id="2b5fa-128">Sonra bir `.nupkg` dosyası yayımladığınızda, nuget.org kullanarak `dotnet nuget push` nuget.org adresinden alınan bir API anahtarı ile birlikte komutu.</span><span class="sxs-lookup"><span data-stu-id="2b5fa-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2b5fa-129">API anahtarınızı alma</span><span class="sxs-lookup"><span data-stu-id="2b5fa-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="2b5fa-130">DotNet nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="2b5fa-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="2b5fa-131">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="2b5fa-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="2b5fa-132">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="2b5fa-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="2b5fa-133">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="2b5fa-133">Related topics</span></span>

- [<span data-ttu-id="2b5fa-134">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b5fa-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="2b5fa-135">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="2b5fa-135">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="2b5fa-136">Yayın öncesi paketleri</span><span class="sxs-lookup"><span data-stu-id="2b5fa-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="2b5fa-137">Birden çok hedef çerçeve desteği</span><span class="sxs-lookup"><span data-stu-id="2b5fa-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2b5fa-138">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b5fa-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2b5fa-139">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b5fa-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2b5fa-140">Sembol paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b5fa-140">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="2b5fa-141">İmzalama paketleri</span><span class="sxs-lookup"><span data-stu-id="2b5fa-141">Signing packages</span></span>](../create-packages/Sign-a-package.md)
