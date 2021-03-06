---
title: MSBuild kullanarak bir NuGet paketi oluşturma
description: Dosya ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere, MSBuild kullanarak bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: JonDouglas
ms.author: jodou
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 18e0da335f65fde99d035388b95f35160757ee84
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901466"
---
# <a name="create-a-nuget-package-using-msbuild"></a>MSBuild kullanarak bir NuGet paketi oluşturma

Kodunuzdan bir NuGet paketi oluşturduğunuzda, bu işlevselliği herhangi bir sayıda diğer geliştirici tarafından paylaşılabilen ve kullanılabilecek bir bileşene paketleyerek. Bu makalede, MSBuild kullanarak bir paketin nasıl oluşturulacağı açıklanır. MSBuild, NuGet içeren her Visual Studio iş yüküne önceden yüklenmiş olarak gelir. Ayrıca DotNet [MSBuild](/dotnet/core/tools/dotnet-msbuild)Ile DotNet CLI aracılığıyla MSBuild 'i de kullanabilirsiniz.

NuGet, .NET Core ve .NET Standard [SDK stili biçimini](../resources/check-project-format.md)kullanan projeler ve diğer SDK stilindeki projeler için, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak üzere kullanır.  Tarafından kullanılan SDK olmayan bir proje için `<PackageReference>` , NuGet Ayrıca bir paket oluşturmak için proje dosyasını kullanır.

SDK stili projelerde varsayılan olarak paket işlevselliği bulunur. SDK olmayan biçim PackageReference projeleri için, proje bağımlılıklarına NuGet. Build. Tasks. Pack paketini eklemeniz gerekir. MSBuild paketi hedefleri hakkında ayrıntılı bilgi için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).

Bir paket oluşturan komut, `msbuild -t:pack` işlevine eşdeğerdir `dotnet pack` .

> [!IMPORTANT]
> Bu konu, [SDK stili](../resources/check-project-format.md) projelere, genellikle .NET Core ve .NET Standard projelerine ve PACKAGEREFERENCE kullanan SDK olmayan bir proje için geçerlidir.

## <a name="set-properties"></a>Özellikleri ayarlama

Bir paket oluşturmak için aşağıdaki özellikler gereklidir.

- `PackageId`, paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı. Belirtilmemişse, varsayılan değer `AssemblyName` .
- `Version`, *birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md)tanımlar. Belirtilmemişse, varsayılan değer 1.0.0 ' dir.
- Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)
- `Authors`, yazar ve sahip bilgileri. Belirtilmemişse, varsayılan değer `AssemblyName` .
- `Company`, şirketinizin adı. Belirtilmemişse, varsayılan değer `AssemblyName` .

Ayrıca, PackageReference kullanan SDK olmayan bir stil projesi paketlebiliyorsanız aşağıdakiler gereklidir:

- `PackageOutputPath`, paketi çağırırken oluşturulan paketin çıktı klasörü.

Visual Studio 'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini ' de projeye sağ tıklayıp **Özellikler**' i seçin ve **paket** sekmesini seçin). Bu özellikleri doğrudan proje dosyaları (*. csproj*) içinde de ayarlayabilirsiniz.

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> Pakete nuget.org genelinde benzersiz bir tanımlayıcı verin veya kullandığınız herhangi bir paket kaynağını kullanın.

Aşağıdaki örnekte, bu özelliklerle birlikte basit ve tamamlanmış bir proje dosyası gösterilmektedir.

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

Ayrıca,, ve gibi isteğe bağlı özellikleri, `Title` `PackageDescription` `PackageTags` [MSBuild paketi hedefleri](../reference/msbuild-targets.md#pack-target)' nde açıklandığı gibi, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta verileri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties)de ayarlayabilirsiniz.

> [!NOTE]
> Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.

Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. proje dosyaları ve [paket sürümü oluşturma](../concepts/package-versioning.md) [içindeki paket başvuruları](../consume-packages/package-references-in-project-files.md) . Ayrıca, ve özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan gelen bir varlık için de mümkündür `<IncludeAssets>` `<ExcludeAssets>` . Daha fazla bilgi için, [bağımlılık varlıklarını denetleyen](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)seee.

## <a name="add-an-optional-description-field"></a>İsteğe bağlı açıklama alanı ekleme

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlayın

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>NuGet. Build. Tasks. Pack paketini ekleme

SDK olmayan bir proje ve PackageReference ile MSBuild kullanıyorsanız, projenize NuGet. Build. Tasks. Pack paketini ekleyin.

1. Proje dosyasını açın ve öğesinden sonra aşağıdakini ekleyin `<PropertyGroup>` :

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. Bir geliştirici komut istemi açın ( **arama** kutusunda, **Geliştirici komut istemi** yazın).

   Visual Studio için Geliştirici Komut İstemi, MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle **Başlangıç** menüsünden başlatmak istersiniz.

3. Proje dosyasını içeren klasöre geçin ve NuGet. Build. Tasks. Pack paketini yüklemek için aşağıdaki komutu yazın.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   MSBuild çıkışının, yapılandırmanın başarıyla tamamlandığını gösteriyor olduğundan emin olun.

## <a name="run-the-msbuild--tpack-command"></a>MSBuild-t:Pack komutunu çalıştırın

Projeden bir NuGet paketi (bir `.nupkg` dosya) oluşturmak için `msbuild -t:pack` komutunu çalıştırın, bu da projeyi otomatik olarak oluşturur:

Visual Studio için geliştirici komut isteminde aşağıdaki komutu yazın:

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

Çıktı, dosyanın yolunu gösterir `.nupkg` .

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

### <a name="automatically-generate-package-on-build"></a>Derleme üzerinde otomatik olarak paket oluştur

Projeyi derlediğinizde veya geri yüklerken otomatik olarak çalıştırmak için `msbuild -t:pack` aşağıdaki satırı proje dosyanıza ekleyin `<PropertyGroup>` :

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

`msbuild -t:pack`Bir çözümde çalıştırdığınızda bu, çözümdeki ( [<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) özelliği olarak ayarlanır) Çözümdeki tüm projeleri paketler `true` .

> [!NOTE]
> Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.

### <a name="test-package-installation"></a>Test paketi yüklemesi

Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz. Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.

Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.

> [!IMPORTANT]
> Paketler sabittir. Bir sorunu düzeltseniz, yeniden test ettiğinizde, siz de [genel paketler](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) klasörünüzü kaldırana kadar paketin eski sürümünü kullanmaya devam edersiniz. Bu, özellikle her derlemede benzersiz bir ön sürüm etiketi kullanmayan paketleri test ederken ilgilidir.

## <a name="next-steps"></a>Sonraki Adımlar

Bir dosya olan bir paket oluşturduktan sonra `.nupkg` , bir [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.

Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:

- [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Kaynak ve yapılandırma dosyalarının dönüştürmeleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Yayın öncesi sürümler](../create-packages/prerelease-packages.md)
- [Paket türünü ayarlama](../create-packages/set-package-type.md)
- [COM birlikte çalışma Derlemeleriyle paket oluşturma](../create-packages/author-packages-with-COM-interop-assemblies.md)

Son olarak, bilmeniz için ek paket türleri vardır:

- [Yerel paketler](../guides/native-packages.md)
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md)