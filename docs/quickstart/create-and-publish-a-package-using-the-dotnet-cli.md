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
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Quickstart: Bir paket oluşturma ve yayımlama (dotnet CLI)

Bir .NET Sınıf Kitaplığı'ndan bir NuGet paketi oluşturmak ve `dotnet` komut satırı arabirimini (CLI) kullanarak nuget.org yayınlamak basit bir işlemdir.

## <a name="prerequisites"></a>Ön koşullar

1. CLI'yi içeren [.NET Core SDK'yı](https://www.microsoft.com/net/download/)yükleyin. `dotnet` Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

1. Zaten bir hesabınız yoksa [nuget.org ücretsiz bir hesaba kaydolun.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Yeni bir hesap oluşturmak bir onay e-postası gönderir. Bir paket yükleyemeden önce hesabı onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

Paketlemek istediğiniz kod için varolan bir .NET Sınıf Kitaplığı projesini kullanabilir veya aşağıdaki gibi basit bir kitap oluşturabilirsiniz:

1. 'li bir `AppLogger`klasör oluşturun.

1. Komut istemini açın ve `AppLogger` klasöre geçin.

1. Proje `dotnet new classlib`için geçerli klasörün adını kullanan türü yazın.

   Bu, yeni projeyi oluşturur.

## <a name="add-package-metadata-to-the-project-file"></a>Proje dosyasına paket meta verisi ekleme

Her NuGet paketinin paketin içeriğini ve bağımlılıklarını açıklayan bir bildirime ihtiyacı vardır. Son pakette, bildirim proje `.nuspec` dosyasına eklediğiniz NuGet meta veri özelliklerinden oluşturulan bir dosyadır.

1. Proje dosyanızı`.csproj`açın ( ) ve aşağıdaki `<PropertyGroup>` en az özellikleri varolan etiketin içine ekleyerek değerleri uygun şekilde değiştirin:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Pakete, nuget.org veya kullandığınız ana bilgisayarda benzersiz bir tanımlayıcı verin. Bu izlenecek yol için, daha sonraki yayımlama adımı paketi herkese açık hale getirebildiğinden (kimsenin gerçekten kullanması pek olası olmasa da) adına "Örnek" veya "Test" eklenmesini öneririz.

1. [NuGet meta veri özelliklerinde](/dotnet/core/tools/csproj#nuget-metadata-properties)açıklanan isteğe bağlı özellikleri ekleyin.

    > [!Note]
    > Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **PackageTags** özelliğine özel olarak dikkat edin.

## <a name="run-the-pack-command"></a>Sürü komutunu çalıştırın

Projeden bir NuGet `.nupkg` paketi (dosya) oluşturmak `dotnet pack` için, projeyi otomatik olarak oluşturan komutu çalıştırın:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

`.nupkg` Çıktı, dosyaya giden yolu gösterir:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Otomatik olarak yapı üzerinde paket oluşturmak

Çalıştırdığınızda `dotnet pack` `dotnet build`otomatik olarak çalıştırmak için proje dosyanıza `<PropertyGroup>`aşağıdaki satırı ekleyin:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Paketi yayımlama

Bir `.nupkg` dosyaya sahip olduktan sonra, nuget.org'dan edinilen bir API anahtarıyla birlikte komutu kullanarak dosyayı `dotnet nuget push` nuget.org yayımlarsınız.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı edinin

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>dotnet nuget push ile yayımla

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanmış paketi yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi oluşturduğunuz için tebrikler!

> [!div class="nextstepaction"]
> [Paket Oluşturma](../create-packages/creating-a-package-dotnet-cli.md)

NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.

- [Paket Yayınlama](../nuget-org/publish-a-package.md)
- [Ön Sürüm Paketleri](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [Sembol paketleri oluşturma](../create-packages/symbol-packages-snupkg.md)
- [İmzalama paketleri](../create-packages/Sign-a-package.md)
