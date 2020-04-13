---
title: dotnet CLI'yi kullanarak NuGet paketi oluşturma
description: Dosyaları ve sürüm gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma sürecine ilişkin ayrıntılı bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230596"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>dotnet CLI'yi kullanarak NuGet paketi oluşturma

Paketiniz ne yaparsa yapsın veya hangi kodu içerse içersin, `dotnet.exe`bu işlevselliği diğer geliştiricilerle paylaşılabilen ve diğer geliştiriciler tarafından kullanılabilecek bir bileşene dönüştürmek için CLI araçlarından `nuget.exe` birini kullanırsınız. Bu makalede, dotnet CLI kullanarak bir paket oluşturmak için nasıl açıklanmaktadır. CLI'yi yüklemek için `dotnet` [NuGet istemci araçlarını yükleyin'](../install-nuget-client-tools.md)e bakın. Visual Studio 2017'den itibaren dotnet CLI .NET Core iş yüklerine dahildir.

[SDK stili biçimini](../resources/check-project-format.md)ve diğer SDK stili projeleri kullanan .NET Core ve .NET Standard projeleri için NuGet, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak için kullanır. Adım adım eğitimler için [dotnet CLI ile .NET Standart Paketleri Oluştur](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) veya [Visual Studio ile .NET Standart Paketleri Oluştur'a](../quickstart/create-and-publish-a-package-using-visual-studio.md)bakın.

`msbuild -t:pack`'ye `dotnet pack`eşdeğer işlevselliktir. MSBuild ile oluşturmak için [bkz.](creating-a-package-msbuild.md)

> [!IMPORTANT]
> Bu konu, genellikle .NET Core ve .NET Standard projeleri olan [SDK tarzı](../resources/check-project-format.md) projeler için geçerlidir.

## <a name="set-properties"></a>Özellikleri ayarlama

Bir paket oluşturmak için aşağıdaki özellikler gereklidir.

- `PackageId`, paketi barındıran galeride benzersiz olması gereken paket tanımlayıcısı. Belirtilmemişse, varsayılan `AssemblyName`değer .
- `Version`, *Major.Minor.Patch[-Soneki]* formunda belirli bir sürüm numarası ve *-Soneki* ön [sürüm sürümlerini](prerelease-packages.md)tanımlar. Belirtilmemişse, varsayılan değer 1.0.0'dır.
- Ana bilgisayarda görünmesi gerektiği gibi paket başlığı (nuget.org gibi)
- `Authors`, yazar ve sahip bilgileri. Belirtilmemişse, varsayılan `AssemblyName`değer .
- `Company`, şirket adınız. Belirtilmemişse, varsayılan `AssemblyName`değer .

Visual Studio'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini'nde projeyi sağ tıklatın, **Özellikler'i**seçin ve **Paket** sekmesini seçin). Ayrıca bu özellikleri doğrudan proje dosyalarında`.csproj`ayarlayabilirsiniz ( ).

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Pakete, nuget.org veya kullandığınız paket kaynağında benzersiz bir tanımlayıcı verin.

Aşağıdaki örnekte, bu özelliklere sahip basit, tam bir proje dosyası gösterilmektedir. (Komutu `dotnet new classlib` kullanarak yeni bir varsayılan proje oluşturabilirsiniz.)

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

[MsBuild paketi hedeflerinde](../reference/msbuild-targets.md#pack-target)açıklandığı `Title`gibi `PackageDescription` `PackageTags`isteğe bağlı özellikleri de ayarlayabilirsiniz, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta veri özellikleri.](/dotnet/core/tools/csproj#nuget-metadata-properties)

> [!NOTE]
> Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **PackageTags** özelliğine özel olarak dikkat edin.

Bağımlılıkları bildirme ve sürüm numaralarını belirtme yle ilgili ayrıntılar için [proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md) ve Paket [sürümüne](../concepts/package-versioning.md)bakın. Varlıkları bağımlılıklardan doğrudan pakete ve `<IncludeAssets>` `<ExcludeAssets>` öznitelikleri kullanarak yüzeye çıkarmak da mümkündür. Daha fazla bilgi için [bkz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)

## <a name="add-an-optional-description-field"></a>İsteğe bağlı açıklama alanı ekleme

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>Sürü komutunu çalıştırın

Projeden bir NuGet `.nupkg` paketi (dosya) oluşturmak `dotnet pack` için, projeyi otomatik olarak oluşturan komutu çalıştırın:

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

`.nupkg` Çıktı, dosyaya giden yolu gösterir.

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

Bir çözüm `dotnet pack` üzerinde çalıştırdığınızda, bu paketlenebilir çözümdeki tüm[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) projeleri paketler `true`(özellik ayarlanır).

> [!NOTE]
> Paketi otomatik olarak oluşturduğunuzda, paketi hazırlama süresi projenizin oluşturma süresini artırır.

### <a name="test-package-installation"></a>Test paketi kurulumu

Paket yayımlamadan önce, genellikle bir projeye paket yükleme işlemini sınamak istersiniz. Testler, zorunlu dosyaların tümünden inin projedeki doğru yerlerinde sonunun olmasını sağlar.

Yüklemeleri Visual Studio'da veya komut satırında normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak el ile test edebilirsiniz.

> [!IMPORTANT]
> Paketler değişmez. Bir sorunu düzeltirseniz, paketin içeriğini değiştirin ve yeniden paketleyin, yeniden test ettiğinizde, genel paketler klasörünüzü [temize çıkarana](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) kadar paketin eski sürümünü kullanmaya devam eceksiniz. Bu, özellikle her yapıda benzersiz bir yayın öncesi etiket kullanmayan paketleri sınarken alakalıdır.

## <a name="next-steps"></a>Sonraki Adımlar

Bir dosya olan bir `.nupkg` paket oluşturduktan sonra, paketi [Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi istediğiniz galeride yayınlayabilirsiniz.

Ayrıca paketinizin yeteneklerini genişletmek veya aşağıdaki konularda açıklandığı gibi diğer senaryoları desteklemek de isteyebilirsiniz:

- [Paket sürüm](../concepts/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Paket simgesi ekleme](../reference/nuspec.md#icon)
- [Kaynak ve yapılandırma dosyalarının dönüşümleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Ön sürüm sürümleri](../create-packages/prerelease-packages.md)
- [Paket türünü ayarlama](../create-packages/set-package-type.md)
- [COM interop montajları ile paketler oluşturma](../create-packages/author-packages-with-COM-interop-assemblies.md)

Son olarak, dikkat edilmesi gereken ek paket türleri vardır:

- [Yerli Paketler](../guides/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages-snupkg.md)
