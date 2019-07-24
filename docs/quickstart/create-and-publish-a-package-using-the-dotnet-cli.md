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
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Hızlı Başlangıç: Paket oluşturma ve yayımlama (DotNet CLı)

.NET sınıf kitaplığından bir NuGet paketi oluşturmak ve `dotnet` komut satırı arabirimini (CLI) kullanarak NuGet.org 'de yayımlamak basit bir işlemdir.

## <a name="prerequisites"></a>Önkoşullar

1. `dotnet` CLI içeren [.NET Core SDK](https://www.microsoft.com/net/download/)' yi yükler. Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

1. Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) . Yeni hesap oluşturma onay e-postası gönderir. Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

Paketlemek istediğiniz kod için mevcut bir .NET sınıf kitaplığı projesi kullanabilir veya basit bir tane aşağıdaki gibi oluşturabilirsiniz:

1. Adlı `AppLogger` bir klasör oluşturun ve içine değiştirin.

1. Proje için geçerli klasörün `dotnet new classlib`adını kullanan öğesini kullanarak projeyi oluşturun.

## <a name="add-package-metadata-to-the-project-file"></a>Proje dosyasına paket meta verileri ekleyin

Her NuGet paketinin, paketin içeriğini ve bağımlılıklarını açıklayan bir bildirime ihtiyacı vardır. Son bir pakette bildirim, proje dosyasına dahil ettiğiniz `.nuspec` NuGet meta verileri özelliklerinden oluşturulan bir dosyadır.

1. Proje dosyanızı (`.csproj`) açın ve mevcut `<PropertyGroup>` etiketin içine aşağıdaki en az özellikleri ekleyerek değerleri uygun şekilde değiştirerek:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı verin. Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).

1. [NuGet meta veri özelliklerinde](/dotnet/core/tools/csproj#nuget-metadata-properties)açıklanan isteğe bağlı özellikleri ekleyin.

    > [!Note]
    > Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.

## <a name="run-the-pack-command"></a>Pack komutunu çalıştırın

Projeden bir NuGet paketi (bir `.nupkg` dosya) oluşturmak için `dotnet pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Çıktı, `.nupkg` dosyanın yolunu gösterir:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Derleme üzerinde otomatik olarak paket oluştur

`<PropertyGroup>`Çalıştırdığınızda `dotnet pack` otomatikolarakçalıştırmakiçin,aşağıdakisatırıiçindeki`dotnet build`proje dosyanıza ekleyin:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Paketi Yayımla

Bir `.nupkg` dosyaya sahip olduktan sonra, NuGet.org. NuGet.org ' den alınan bir `dotnet nuget push` API anahtarı ile birlikte komutunu kullanarak bu dosyayı yayımlayın.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı alın

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>DotNet NuGet Push ile yayımlama

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Yayımlama hataları

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayınlanan paketi yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi oluştururken Tebrikler!

> [!div class="nextstepaction"]
> [Paket oluşturma](../create-packages/creating-a-package-dotnet-cli.md)

NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.

- [Paket Yayımlama](../nuget-org/publish-a-package.md)
- [Yayın öncesi paketler](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [Sembol paketleri oluşturma](../create-packages/symbol-packages-snupkg.md)
- [İmzalama paketleri](../create-packages/Sign-a-package.md)
