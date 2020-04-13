---
title: NuGet sembol paketleri yeni sembol paketi formatı '.snupkg' kullanarak nasıl yayımlanır? Microsoft Dokümanlar
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet sembol paketleri (snupkg) nasıl oluşturulur?
keywords: NuGet sembol paketleri, NuGet paketi hata ayıklama, NuGet hata ayıklama destekleyen, paket sembolleri, sembol paketi kuralları
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380424"
---
# <a name="creating-symbol-packages-snupkg"></a>Sembol paketleri oluşturma (.snupkg)

İyi bir hata ayıklama deneyimi, derlenen ve kaynak kod arasındaki ilişki, yerel değişkenlerin adları, yığın izleri ve daha fazlası gibi kritik bilgileri sağladığından hata ayıklama sembollerinin varlığına dayanır. Bu sembolleri dağıtmak ve NuGet paketlerinizin hata ayıklama deneyimini geliştirmek için sembol paketlerini (.snupkg) kullanabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

[nuget.exe v4.9.0 veya üzeri](https://www.nuget.org/downloads) veya [dotnet CLI v2.2.0 veya üzeri,](https://www.microsoft.com/net/download/dotnet-core/2.2)gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulamak .

## <a name="creating-a-symbol-package"></a>Sembol paketi oluşturma

Dotnet CLI veya MSBuild kullanıyorsanız, .nupkg dosyasına ek olarak bir .snupkg dosyası oluşturmak için özellikleri `IncludeSymbols` ve `SymbolPackageFormat` özelliklerini ayarlamanız gerekir.

* .csproj dosyanıza aşağıdaki özellikleri ekleyin:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Veya komut satırında bu özellikleri belirtin:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  or

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

NuGet.exe kullanıyorsanız, .nupkg dosyasına ek olarak bir .snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Özellik [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) iki değerden birine `symbols.nupkg` sahip olabilir: `snupkg`(varsayılan) veya . Bu özellik belirtilmemişse, eski bir simge paketi oluşturulur.

> [!Note]
> Eski biçim `.symbols.nupkg` hala ancak uyumluluk nedenleriyle desteklenir (bkz. [Eski Simge Paketleri).](Symbol-Packages.md) NuGet.org sembol sunucusu sadece yeni sembol paketi `.snupkg`biçimini kabul eder - .

## <a name="publishing-a-symbol-package"></a>Sembol paketi yayımlama

1. Kolaylık sağlamak için önce API anahtarınızı NuGet ile kaydedin (bkz. [bir paket yayımla).](../nuget-org/publish-a-package.md)

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Birincil paketinizi nuget.org yayımladıktan sonra, sembol paketini aşağıdaki gibi itin.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Ayrıca, aşağıdaki komutu kullanarak hem birincil hem de sembol paketlerini aynı anda itebilirsiniz. Hem .nupkg hem de .snupkg dosyalarının geçerli klasörde bulunması gerekir.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet her iki paketi de nuget.org yayınlayacaktır. `MyPackage.nupkg` önce yayınlanacak, ardından `MyPackage.snupkg`.

> [!Note]
> Sembol paketi yayımlanmıyorsa, NuGet.org kaynağı 'olarak `https://api.nuget.org/v3/index.json`yapılandırdığınızdan denetlemeyin. Sembol paket yayımlama yalnızca [NuGet V3 API](../api/overview.md#versioning)tarafından desteklenir.

## <a name="nugetorg-symbol-server"></a>NuGet.org sembol sunucusu

NuGet.org kendi sembolleri sunucu deposu destekler ve sadece yeni sembol `.snupkg`paketi biçimini kabul eder - . Paket tüketicileri, Visual Studio'daki sembol `https://symbols.nuget.org/download/symbols` kaynaklarına ekleyerek sembol sunucuyu nuget.org için yayınlanan sembolleri kullanabilirler, bu da Visual Studio hata ayıklayıcısında paket koduna adım atmanızı sağlar. Bkz. Bu işlemle ilgili ayrıntılar için [Visual Studio hata ayıklamasında ki simge (.pdb) ve kaynak dosyaları belirtin.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org sembolü paket kısıtlamaları

NuGet.org sembol paketleri için aşağıdaki kısıtlamalara sahiptir:

- Yalnızca aşağıdaki dosya uzantılarına sembol paketlerinde `.nuspec` `.xml`izin `.psmdcp` `.rels`verilir: `.pdb`, , , ,`.p7s`
- NuGet.org'un sembol sunucusunda yalnızca yönetilen [Taşınabilir PDF'ler](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) desteklenir.
- PDB'ler ve bunların ilişkili .nupkg DL'leri Visual Studio sürüm 15.9 veya üzeri derleyici ile oluşturulmalıdır (bkz. [PDB kripto karma)](https://github.com/dotnet/roslyn/issues/24429)

bu kısıtlamalar karşılanmazsa, NuGet.org için yayınlanan sembol paketleri doğrulamada başarısız olur. 

### <a name="symbol-package-validation-and-indexing"></a>Sembol paketi doğrulama ve dizin oluşturma

[NuGet.org](https://www.nuget.org/) için yayınlanan sembol paketleri, kötü amaçlı yazılım taraması da dahil olmak üzere çeşitli doğrulamalara tabi dir. Bir paket doğrulama denetiminde başarısız olursa, paket ayrıntıları sayfası bir hata iletisi görüntüler. Buna ek olarak, paketin sahipleri tanımlanan sorunları nasıl düzelteceklerine ilişkin talimatları içeren bir e-posta alır.

Sembol paketi tüm doğrulamaları geçtiğinde, semboller NuGet.org'un sembol sunucuları tarafından dizine eklenir ve tüketime sunulacaktır.

Paket doğrulama ve dizin oluşturma genellikle 15 dakikanın altında sürer. Paket yayımlama beklenenden uzun sürüyorsa, NuGet.org herhangi bir kesinti yaşanıp yaşanmayacağını kontrol etmek için [status.nuget.org](https://status.nuget.org/) ziyaret edin. Tüm sistemler çalışır durumdaysa ve paket bir saat içinde başarıyla yayınlanmamışsa, lütfen nuget.org giriş yapın ve paket detayları sayfasındaki İletişim Destek bağlantısını kullanarak bizimle iletişime geçin.

## <a name="symbol-package-structure"></a>Sembol paket yapısı

Sembol paketi (.snupkg) aşağıdaki özelliklere sahiptir:

1) .snupkg, karşılık gelen NuGet paketi (.nupkg) ile aynı id ve sürüme sahiptir.
2) .snupkg, DLs/EXE yerine, ilgili PDB'lerinin aynı klasör hiyerarşisine dahil olacağı ayrımına sahip herhangi bir DLL veya EXE dosyası için karşılık gelen .nupkg ile aynı klasör yapısına sahiptir. PDB dışındaki uzantılı dosya ve klasörler snupkg dışında bırakılır.
3) Sembol paketinin .nuspec dosyasında `SymbolsPackage` paket türü vardır:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Bir yazar nupkg ve snupkg oluşturmak için özel bir nuspec kullanmaya karar verirse, snupkg aynı klasör hiyerarşisi ve dosyaları 2 ayrıntılı olmalıdır).
5) Aşağıdaki alanlar snupkg'ın nuspec dışında tutulur: ```authors``` ```owners```, ```requireLicenseAcceptance``` ```license type```, ```licenseUrl```, ```icon```, ve .
6) Öğeyi kullanmayın. ```<license>``` Bir .snupkg ilgili .nupkg ile aynı lisans altında dır.

## <a name="see-also"></a>Ayrıca bkz.

.NET derlemelerinin kaynak kodunun hata ayıklanmasını etkinleştirmek için Kaynak Bağlantısını kullanmayı düşünün. Daha fazla bilgi için lütfen [Kaynak Bağlantı kılavuzuna](/dotnet/standard/library-guidance/sourcelink)bakın.

Sembol paketleri hakkında daha fazla bilgi için lütfen [NuGet Paketi Hata Ayıklama & Semboller Geliştirmeleri](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) tasarım özelliklerine bakın.
