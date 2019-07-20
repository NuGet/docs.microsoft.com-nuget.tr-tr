---
title: DotNet CLı kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 6774329138c2bf26908496860267e3570a94d39c
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68346159"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>DotNet CLı kullanarak bir NuGet paketi oluşturma

Paketinizin ne yaptığını veya hangi kodu içerdiğini bağımsız olarak, bu işlevselliği bir veya daha fazla geliştirici tarafından kullanılabilen bir bileşene `nuget.exe` paketlemek `dotnet.exe`için ya da CLI araçlarından birini kullanırsınız. Bu makalede, DotNet CLı kullanarak bir paketin nasıl oluşturulacağı açıklanır. `dotnet` CLI 'yı yüklemek için bkz. [NuGet istemci araçları 'nı yükler](../install-nuget-client-tools.md). Visual Studio 2017 ' den başlayarak, DotNet CLı .NET Core iş yüklerine dahildir.

NuGet, .NET Core ve .NET Standard [SDK stili biçimini](../resources/check-project-format.md)kullanan projeler ve diğer SDK stilindeki projeler için, proje dosyasındaki bilgileri doğrudan bir paket oluşturmak üzere kullanır. Adım adım öğreticiler için bkz. [DotNet CLI ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Visual Studio ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-visual-studio.md).

`msbuild -t:pack`işlevine eşdeğerdir `dotnet pack`. MSBuild ile derlemek için, kavramlar bu makalede açıklananla aynıdır, ancak komut satırı komutları biraz farklıdır. Benzer şekilde, SDK olmayan bir proje ve `<PackageReference>`için kullanabilirsiniz. `msbuild /t:pack` Bu senaryolarda, NuGet. Build. Tasks. Pack paketini bağımlılıklarına eklemeniz gerekir. Bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).

> [!IMPORTANT]
> Bu konu, genellikle .NET Core ve .NET Standard projeleri [SDK stilindeki](../resources/check-project-format.md) projeler için geçerlidir.

## <a name="set-properties"></a>Özellikleri ayarla

Bir paket oluşturmak için aşağıdaki özellikler gereklidir.

- `PackageId`, paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı. Belirtilmemişse, varsayılan değer `AssemblyName`.
- `Version`, *birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md)tanımlar. Belirtilmemişse, varsayılan değer 1.0.0 ' dir.
- Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)
- `Authors`, yazar ve sahip bilgileri. Belirtilmemişse, varsayılan değer `AssemblyName`.
- `Company`, şirketinizin adı. Belirtilmemişse, varsayılan değer `AssemblyName`.

Visual Studio 'da bu değerleri proje özelliklerinde ayarlayabilirsiniz (Çözüm Gezgini ' de projeye sağ tıklayıp **Özellikler**' i seçin ve **paket** sekmesini seçin). Bu özellikleri doğrudan proje dosyaları (`.csproj`) içinde de ayarlayabilirsiniz.

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> Pakete nuget.org genelinde benzersiz bir tanımlayıcı verin veya kullandığınız herhangi bir paket kaynağını kullanın.

Ayrıca,, ve `Title` `PackageDescription` `PackageTags`gibi isteğe bağlı özellikleri, [MSBuild paketi hedefleri](../reference/msbuild-targets.md#pack-target)' nde açıklandığı gibi, [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)ve [NuGet meta verileri özelliklerini](/dotnet/core/tools/csproj#nuget-metadata-properties)de ayarlayabilirsiniz.

> [!NOTE]
> Genel tüketim için derlenmiş paketler için, paket **etiketleri** özelliğine özel bir dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamalarına yardımcı olur.

Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. [paket sürümü oluşturma](../reference/package-versioning.md). Ayrıca, `<IncludeAssets>` ve `<ExcludeAssets>` özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan gelen bir varlık için de mümkündür. Daha fazla bilgi için, [bağımlılık varlıklarını denetleyen](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)seee.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarla

Paket tanımlayıcısı ve sürüm numarası, pakette bulunan tam kodu benzersiz bir şekilde tanımladıklarından, projedeki en önemli iki değer vardır.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: Tanımlayıcının nuget.org genelinde benzersiz olması veya paketi barındırdığı bir galeri olması gerekir. Bir tanımlayıcıya karar vermeden önce, adın zaten kullanımda olup olmadığını denetlemek için ilgili galeride arama yapın. Çakışmaları önlemek için iyi bir model, tanımlayıcı `Contoso.`ilk parçası olarak şirketinizin adını kullanmaktır.
- **Ad alanı benzeri adlar**: Kısa çizgi yerine nokta gösterimini kullanarak .NET 'teki ad alanlarına benzer bir model izleyin. Örneğin, `Contoso.Utility.UsefulStuff` `Contoso-Utility-UsefulStuff` veya yerinekullanın.`Contoso_Utility_UsefulStuff` Tüketiciler ayrıca, paket tanımlayıcısı kodda kullanılan ad alanları ile eşleştiğinde yararlı olduğunu bulur.
- **Örnek paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir örnek kod paketi oluşturursanız, ' de `.Sample` `Contoso.Utility.UsefulStuff.Sample`olduğu gibi, tanımlayıcıda bir sonek olarak iliştirme. (Örnek paketin, diğer pakete bağımlılığı vardır.) Örnek bir paket oluştururken, içindeki `contentFiles` `<IncludeAssets>`değerini kullanın. Klasöründe, örnek kodu içinde `\Samples\Contoso.Utility.UsefulStuff.Sample`olarak adlandırılan `\Samples\<identifier>` bir klasörde düzenleyin. `content`

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, paketin sürümünü proje (veya bütünleştirilmiş kod) ile eşleşecek şekilde ayarlayın, ancak bu kesinlikle gerekli değildir. Bu, bir paketi tek bir derlemeyle sınırlandırdığınızda basit bir işlemdir. Genel olarak, NuGet 'in derleme sürümlerini değil, bağımlılıkları çözümlerken Paket sürümleriyle uğraşır olduğunu unutmayın.
- Standart olmayan bir sürüm düzeni kullanırken, [paket sürümü oluşturma](../reference/package-versioning.md)bölümünde açıklandığı gibi NuGet sürüm oluşturma kurallarını dikkate aldığınızdan emin olun. NuGet genellikle [semver 2 uyumludur](../reference/package-versioning.md#semantic-versioning-200).

> Bağımlılık çözümleme hakkında daha fazla bilgi için bkz. [PackageReference Ile bağımlılık çözünürlüğü](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Sürüm oluşturmayı daha iyi anlamak için de yararlı olabilecek eski bilgiler için, bu blog gönderilerine bakın.
>
> - [Bölüm 1: DLL Hell 'i alma](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Bölüm 2: Çekirdek algoritması](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Bölüm 3: Bağlama yeniden yönlendirmeleri aracılığıyla birleşme](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

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

Bir çözümde çalıştırdığınızda `dotnet pack` , bu, çözümde bulunan ve packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) özellik olarak `true`ayarlanır) tüm projeleri paketler.

> [!NOTE]
> Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.

### <a name="test-package-installation"></a>Test paketi yüklemesi

Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz. Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.

Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.

> [!IMPORTANT]
> Paketler sabittir. Bir sorunu düzeltseniz, yeniden test ettiğinizde, siz de [genel paketler](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) klasörünüzü kaldırana kadar paketin eski sürümünü kullanmaya devam edersiniz. Bu, özellikle her derlemede benzersiz bir ön sürüm etiketi kullanmayan paketleri test ederken ilgilidir.

## <a name="next-steps"></a>Sonraki Adımlar

Bir `.nupkg` dosya olan bir paket oluşturduktan sonra, bir [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.

Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:

- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Kaynak ve yapılandırma dosyalarının dönüştürmeleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Yayın öncesi sürümler](../create-packages/prerelease-packages.md)
- [Paket türünü ayarlama](../create-packages/set-package-type.md)
- [COM birlikte çalışma Derlemeleriyle paket oluşturma](../create-packages/author-packages-with-COM-interop-assemblies.md)

Son olarak, bilmeniz için ek paket türleri vardır:

- [Yerel Paketler](../create-packages/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages.md)
