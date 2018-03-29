---
title: Oluşturma ve yayımlama dotnet CLI kullanarak bir NuGet paketi | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/24/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Oluşturma ve yayımlama dotnet .NET Core CLI kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi.
keywords: NuGet paketini oluşturma, NuGet paketi yayımlama, NuGet öğretici dotnet yayımlama NuGet paketi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 536e39ae64649ca1c11afa95c20872515e9e4c83
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="create-and-publish-a-package"></a>Oluşturma ve bir paket yayımlama

Bir .NET sınıf kitaplığı'ndan bir NuGet paketi oluşturmak ve nuget.org kullanarak yayımlamak için basit bir işlemdir `dotnet` komut satırı arabirimi (CLI).

## <a name="prerequisites"></a>Önkoşullar

1. Yükleme [.NET Core SDK](https://www.microsoft.com/net/download/), içeren `dotnet` CLI.

1. [Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı proje oluşturma

Varolan bir .NET sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:

1. Adlı bir klasör oluşturun `AppLogger` ve içine değiştirin.

1. Kullanarak projeyi oluşturmak `dotnet new classlib`, proje için geçerli klasörün adını kullanır.

## <a name="add-package-metadata-to-the-project-file"></a>Proje dosyasına paket meta verileri ekleme

Her NuGet paketi paketin içeriği ve bağımlılıkları tanımlayan bir bildirim gerekiyor. Son bir pakette bildirimidir bir `.nuspec` proje dosyasında dahil NuGet meta verileri özelliklerinden oluşturulan dosya.

1. Proje dosyasını açın (`.csproj`) ve çıkma içinde en az aşağıdaki özellikleri ekleyin `<PropertyGroup>` değerleri uygun şekilde değiştirerek etiketi:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket verin. Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.

1. Açıklandığı isteğe bağlı özelliklerin eklemek [NuGet meta veri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties).

    > [!Note]
    > Ortak tüketim için oluşturulan paketler için özel dikkat **PackageTags** özelliği gibi etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

Bir NuGet paketi oluşturmak için (bir `.nupkg` dosyası) projeden çalıştırma `dotnet pack` ayrıca projenin otomatik olarak oluşturur komutu:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Çıkış yolu gösterir `.nupkg` dosyası:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Yapı paketini otomatik olarak oluştur

Otomatik olarak çalışacak şekilde `dotnet pack` çalıştırdığınızda `dotnet build`, proje dosyasında aşağıdaki satırı ekleyin `<PropertyGroup>`:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Paket yayımlama

Bulduktan sonra bir `.nupkg` dosyası, yayımlama, nuget.org kullanmaya `dotnet nuget push` nuget.org alınan bir API anahtarı ile birlikte komutu.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı edinin

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>DotNet nuget itme ile yayımlama

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanan paket yönetme

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>İlgili konular

- [Bir paket oluşturun](../create-packages/creating-a-package.md)
- [Paket Yayımlama](../create-packages/publish-a-package.md)
- [Birden çok hedef çerçeveyi desteği](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [İmzalama paketleri](../create-packages/Sign-a-package.md)
