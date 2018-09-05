---
title: Oluşturma ve yayımlama dotnet CLI kullanarak bir NuGet paketi
description: Oluşturma ve yayımlama dotnet .NET Core CLI kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi.
author: karann-msft
ms.author: karann
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: 02aa7bb9d27352bbecfc718ef5bd6ee33501018d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548435"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Hızlı Başlangıç: Oluşturma ve yayımlama paket (dotnet CLI)

Bir .NET sınıf kitaplığı'ndan bir NuGet paketi oluşturmak ve nuget.org kullanarak yayımlamak için basit bir işlemdir `dotnet` komut satırı arabirimi (CLI).

## <a name="prerequisites"></a>Önkoşullar

1. Yükleme [.NET Core SDK'sı](https://www.microsoft.com/net/download/), içeren `dotnet` CLI.

1. [Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Bir sınıf kitaplığı projesi oluşturun

Mevcut bir .NET sınıf kitaplığı projesi paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:

1. Adlı bir klasör oluşturun `AppLogger` ve içine değiştirin.

1. Kullanarak proje oluşturduğunuzda `dotnet new classlib`, proje için geçerli klasörün adını kullanır.

## <a name="add-package-metadata-to-the-project-file"></a>Paket meta verileri proje dosyasına ekleyin

Her bir NuGet paketi paketin içeriği ve bağımlılıkları tanımlayan bir bildirim gerekiyor. Son bir pakette bildirimidir bir `.nuspec` proje dosyasına eklenecek NuGet meta verileri özelliklerinden oluşturulan dosya.

1. Proje dosyanızı açın (`.csproj`) ve mevcut içinde en az aşağıdaki özellikleri ekleyin `<PropertyGroup>` değerleri uygun şekilde değiştirerek etiketi:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket verin. Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.

1. Üzerinde tanımlanan herhangi bir isteğe bağlı özellikler Ekle [NuGet meta veri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Ortak tüketim için oluşturulan paketler için özel dikkat **PackageTags** özelliği olarak etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

Bir NuGet paketi oluşturmak için (bir `.nupkg` dosya) projeden çalıştırma `dotnet pack` komutu ayrıca projeyi otomatik olarak oluşturur:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Çıktı yolu gösterir `.nupkg` dosyası:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Derleme paketi otomatik olarak oluştur

Otomatik olarak çalışacak şekilde `dotnet pack` çalıştırdığınızda `dotnet build`, proje dosyanızın aşağıdaki satırı ekleyin `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Paket yayımlama

Sonra bir `.nupkg` dosyası yayımladığınızda, nuget.org kullanarak `dotnet nuget push` nuget.org adresinden alınan bir API anahtarı ile birlikte komutu.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı alma

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>DotNet nuget itme ile yayımlama

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanan paket yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>İlgili konular

- [Paket oluşturma](../create-packages/creating-a-package.md)
- [Paket Yayımlama](../create-packages/publish-a-package.md)
- [Yayın öncesi paketleri](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeve desteği](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [İmzalama paketleri](../create-packages/Sign-a-package.md)
