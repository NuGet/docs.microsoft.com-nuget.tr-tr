---
title: MSBuild'i kullanarak NuGet paketi oluşturma
description: Dosyaları ve sürüm gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma sürecine ilişkin ayrıntılı bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231324"
---
# <a name="create-a-nuget-package-using-msbuild"></a>MSBuild'i kullanarak NuGet paketi oluşturma

Kodunuzdan bir NuGet paketi oluşturduğunuzda, bu işlevselliği diğer geliştiricilerle paylaşılabilen ve diğer geliştiriciler tarafından kullanılabilecek bir bileşene paketlersiniz. Bu makalede, MSBuild kullanarak bir paket oluşturmak için nasıl açıklanmaktadır. MSBuild, NuGet içeren her Visual Studio iş yüküyle önceden yüklenmiş olarak gelir. Ayrıca [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild)ile dotnet CLI üzerinden MSBuild kullanabilirsiniz.

[SDK stili biçimini](../resources/check-project-format.md)ve diğer SDK stili projeleri kullanan .NET Core ve .NET Standard projeleri için NuGet, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak için kullanır.  Kullanan SDK tarzı olmayan bir `<PackageReference>`proje için, NuGet bir paket oluşturmak için proje dosyasını da kullanır.

SDK tarzı projeler varsayılan olarak paket işlevine sahiptir. SDK tarzı olmayan PackageReference projeleri için proje bağımlılıklarına NuGet.Build.Tasks.Pack paketini eklemeniz gerekir. MSBuild paketi hedefleri hakkında ayrıntılı bilgi için [NuGet paketine bakın ve MSBuild hedefleri olarak geri yükleyin.](../reference/msbuild-targets.md)

Bir paket oluşturan komut, `msbuild -t:pack` `dotnet pack`işlevsellik eşdeğerdir.

> [!IMPORTANT]
> Bu konu, genellikle .NET Core ve .NET Standart projeleri olan [SDK tarzı](../resources/check-project-format.md) projeler ve PackageReference kullanan SDK tarzı olmayan projeler için geçerlidir.

## <a name="set-properties"></a>Özellikleri ayarlama

Bir paket oluşturmak için aşağıdaki özellikler gereklidir.

- `PackageId`, paketi barındıran galeride benzersiz olması gereken paket tanımlayıcısı. Belirtilmemişse, varsayılan `AssemblyName`değer .
- `Version`, *Major.Minor.Patch[-Soneki]* formunda belirli bir sürüm numarası ve *-Soneki* ön [sürüm sürümlerini](prerelease-packages.md)tanımlar. Belirtilmemişse, varsayılan değer 1.0.0'dır.
- Ana bilgisayarda görünmesi gerektiği gibi paket başlığı (nuget.org gibi)
- `Authors`, yazar ve sahip bilgileri. Belirtilmemişse, varsayılan `AssemblyName`değer .
- `Company`, şirket adınız. Belirtilmemişse, varsayılan `AssemblyName`değer .

Ayrıca PackageReference kullanan SDK tarzı olmayan projeleri paketliliyorsanız, aşağıdakiler gereklidir:

- `PackageOutputPath`, paketi ararken oluşturulan paketin çıktı klasörü.

Visual Studio'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini'nde projeyi sağ tıklatın, **Özellikler'i**seçin ve **Paket** sekmesini seçin). Ayrıca bu özellikleri doğrudan proje dosyalarında *(.csproj)* ayarlayabilirsiniz.

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Pakete, nuget.org veya kullandığınız paket kaynağında benzersiz bir tanımlayıcı verin.

Aşağıdaki örnekte, bu özelliklere sahip basit, tam bir proje dosyası gösterilmektedir.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
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

## <a name="add-the-nugetbuildtaskspack-package"></a>NuGet.Build.Tasks.Pack paketini ekleyin

MSBuild'i SDK tarzı olmayan bir proje ve PackageReference ile kullanıyorsanız, Projenize NuGet.Build.Tasks.Pack paketini ekleyin.

1. Proje dosyasını açın ve `<PropertyGroup>` öğeden sonra aşağıdakileri ekleyin:

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Geliştirici komut istemini açın **(Arama** kutusunda **Geliştirici komut istemi**yazın).

   MSBuild için gerekli tüm yollarla yapılandırılacak gibi, genellikle Görsel Stüdyo için Geliştirici Komut Komut Ustem komutunu **Başlat** menüsünden başlatmak istersiniz.

3. Proje dosyasını içeren klasöre geçin ve NuGet.Build.Tasks.Pack paketini yüklemek için aşağıdaki komutu yazın.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   MSBuild çıktısının yapının başarıyla tamamlandığını gösterdiğinden emin olun.

## <a name="run-the-msbuild--tpack-command"></a>msbuild -t:pack komutunu çalıştırın

Projeden bir NuGet `.nupkg` paketi (dosya) oluşturmak `msbuild -t:pack` için, projeyi otomatik olarak oluşturan komutu çalıştırın:

Visual Studio için Geliştirici komut isteminde aşağıdaki komutu yazın:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

`.nupkg` Çıktı, dosyaya giden yolu gösterir.

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a>Otomatik olarak yapı üzerinde paket oluşturmak

Projeyi oluştururken veya geri yüklediğinizde otomatik olarak çalıştırmak `msbuild -t:pack` için `<PropertyGroup>`aşağıdaki satırı proje dosyanıza ekleyin:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

Bir çözüm `msbuild -t:pack` üzerinde çalıştırdığınızda, bu paketlenebilir çözümdeki tüm[<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) projeleri paketler `true`(özellik ayarlanır).

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

- [NuGet paketi ve MSBuild hedefleri olarak geri yükleme](../reference/msbuild-targets.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Kaynak ve yapılandırma dosyalarının dönüşümleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Ön sürüm sürümleri](../create-packages/prerelease-packages.md)
- [Paket türünü ayarlama](../create-packages/set-package-type.md)
- [COM interop montajları ile paketler oluşturma](../create-packages/author-packages-with-COM-interop-assemblies.md)

Son olarak, dikkat edilmesi gereken ek paket türleri vardır:

- [Yerli Paketler](../guides/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages-snupkg.md)
