---
title: Yeni sembol paketi biçimi '. snupkg ' kullanarak NuGet sembol paketleri yayımlama | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet sembol paketleri oluşturma (snupkg).
keywords: NuGet sembol paketleri, NuGet paket hata ayıklaması, NuGet hata ayıklamayı destekleme, paket sembolleri, sembol paketi kuralları
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235730"
---
# <a name="creating-symbol-packages-snupkg"></a>Sembol paketleri (. snupkg) oluşturuluyor

İyi bir hata ayıklama deneyimi, derlenmiş ve kaynak kodu, yerel değişkenlerin adları, yığın izlemeleri ve daha fazlası arasındaki ilişki gibi kritik bilgiler sağlayan hata ayıklama sembollerinin varlığını kullanır. Sembol paketlerini (. snupkg), bu sembolleri dağıtmak ve NuGet paketlerinizin hata ayıklama deneyimini geliştirmek için kullanabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

Gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v 4.9.0 veya üzeri](https://www.nuget.org/downloads) ya da [DotNet CLI v 2.2.0 veya üzeri](https://www.microsoft.com/net/download/dotnet-core/2.2).

## <a name="creating-a-symbol-package"></a>Sembol paketi oluşturma

DotNet CLı veya MSBuild kullanıyorsanız, `IncludeSymbols` `SymbolPackageFormat` . nupkg dosyasına ek olarak. snupkg dosyası oluşturmak için ve özelliklerini ayarlamanız gerekir.

* Aşağıdaki özellikleri. csproj dosyanıza ekleyin:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Veya komut satırında aşağıdaki özellikleri belirtin:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  veya

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

NuGet.exe kullanıyorsanız,. nupkg dosyasına ek olarak. snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)Özellik iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg` . Bu özellik belirtilmezse, eski bir sembol paketi oluşturulur.

> [!Note]
> Eski biçim `.symbols.nupkg` hala destekleniyor ancak yalnızca yerel paketler gibi uyumluluk nedenleriyle (bkz. [eski sembol paketleri](Symbol-Packages.md)). NuGet. org 'ın sembol sunucusu yalnızca yeni sembol paketi biçimini kabul eder- `.snupkg` .

## <a name="publishing-a-symbol-package"></a>Sembol paketi yayımlama

1. Kolaylık olması için önce API anahtarınızı NuGet ile kaydedin (bkz. [bir paket yayımlama](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Birincil paketinizi nuget.org 'e yayımladıktan sonra, sembol paketini aşağıdaki gibi gönderin.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Ayrıca, aşağıdaki komutu kullanarak hem birincil hem de sembol paketlerini aynı anda gönderebilirsiniz. . Nupkg ve. snupkg dosyalarının her ikisi de geçerli klasörde bulunmalıdır.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet, her iki paketi de nuget.org 'e yayımlar. `MyPackage.nupkg` önce yayımlanacak ve ardından `MyPackage.snupkg` .

> [!Note]
> Sembol paketi yayınlanmamışsa, NuGet.org kaynağını olarak yapılandırdığınızdan emin olun `https://api.nuget.org/v3/index.json` . Sembol paketi yayımlaması yalnızca [NuGet v3 API 'si](../api/overview.md#versioning)tarafından desteklenir.

## <a name="nugetorg-symbol-server"></a>NuGet.org symbol sunucusu

NuGet.org kendi sembol sunucu deposunu destekler ve yalnızca yeni sembol paketi biçimini kabul eder- `.snupkg` . Paket tüketicileri Visual Studio 'daki sembol kaynaklarına ekleyerek nuget.org sembol sunucusunda yayınlanan sembolleri kullanarak `https://symbols.nuget.org/download/symbols` Visual Studio hata ayıklayıcısında paket koduna adımlamayı sağlar. Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org sembol paketi kısıtlamaları

NuGet.org, sembol paketleri için aşağıdaki kısıtlamalara sahiptir:

- Sembol paketlerinde yalnızca şu dosya uzantılarına izin veriliyor: `.pdb` ,,, `.nuspec` `.xml` `.psmdcp` , `.rels` , `.p7s`
- NuGet. org 'ın sembol sunucusunda yalnızca yönetilen [Taşınabilir pdb 'leri](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) desteklenir.
- Pdb 'leri ve ilişkili. nupkg dll 'Lerinin Visual Studio sürüm 15,9 veya üzeri bir derleyici ile oluşturulması gerekir (bkz. [pdb şifre karması](https://github.com/dotnet/roslyn/issues/24429))

NuGet.org 'e yayınlanan sembol paketleri, bu kısıtlamalar karşılanmazsa doğrulama başarısız olur. 

> [!NOTE]
> C++ projeleri gibi yerel projeler, taşınabilir pdb 'leri yerine Windows pdb 'leri oluşturur. Bunlar NuGet. org 'ın sembol sunucusu tarafından desteklenmez. Lütfen bunun yerine [eski sembol paketlerini](Symbol-Packages.md) kullanın.

### <a name="symbol-package-validation-and-indexing"></a>Sembol paketi doğrulama ve dizin oluşturma

[NuGet.org](https://www.nuget.org/) ' de yayınlanan sembol paketleri kötü amaçlı yazılım tarama dahil olmak üzere çeşitli doğrulamalar sağlar. Bir paket doğrulama denetiminden başarısız olursa, paket ayrıntıları sayfasında bir hata mesajı görüntülenir. Ayrıca, paketin sahipleri, tanımlanan sorunları nasıl gidereceğiniz hakkında yönergeler içeren bir e-posta alır.

Sembol paketi tüm doğrulamaları geçtiğinde, semboller NuGet. org 'ın sembol sunucuları tarafından dizine alınır ve tüketim için kullanılabilir olacaktır.

Paket doğrulama ve dizin oluşturma genellikle 15 dakika boyunca sürer. Paket yayımlaması beklenenden uzun sürerse, NuGet.org 'in herhangi bir kesinti yaşamadığını denetlemek için [Status.NuGet.org](https://status.nuget.org/) adresini ziyaret edin. Tüm sistemler çalışır durumda ve paket bir saat içinde başarıyla yayımlanmamışsa, lütfen nuget.org ' e oturum açın ve paket ayrıntıları sayfasında desteğe başvurun bağlantısını kullanarak bizimle iletişime geçin.

## <a name="symbol-package-structure"></a>Sembol paketi yapısı

Sembol paketi (. snupkg) aşağıdaki özelliklere sahiptir:

1) . Snupkg, karşılık gelen NuGet paketiyle (. nupkg) aynı kimliğe ve sürüme sahiptir.
2) . Snupkg, dll 'Ler veya EXE dosyaları için karşılık gelen. nupkg ile aynı klasör yapısına sahiptir; bu, bunlara karşılık gelen pdb 'leri, aynı klasör hiyerarşisine dahil edilir. PDB 'den farklı uzantılara sahip dosyalar ve klasörler, snupkg 'dan bırakılır.
3) Sembol paketinin. nuspec dosyası `SymbolsPackage` paket türüne sahiptir:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Bir yazar, nupkg ve snupkg 'leri oluşturmak için özel bir nuspec kullanılmasına karar verirse, snupkg, aynı klasör hiyerarşisine ve 2 ' de ayrıntılı dosyalar içermelidir.
5) Aşağıdaki alanlar, snupkg 'dan nuspec 'ten çıkarılacak: ```authors``` , ```owners``` ,, ```requireLicenseAcceptance``` ```license type``` , ```licenseUrl``` ve  ```icon``` .
6) ```<license>```Öğesini kullanmayın. A. snupkg, karşılık gelen. nupkg ile aynı lisans kapsamında ele alınmıştır.

## <a name="see-also"></a>Ayrıca bkz.

.NET derlemelerinin kaynak kodu hata ayıklamasını etkinleştirmek için kaynak bağlantısı kullanmayı düşünün. Daha fazla bilgi için lütfen [kaynak bağlantı kılavuzuna](/dotnet/standard/library-guidance/sourcelink)bakın.

Sembol paketleri hakkında daha fazla bilgi için lütfen [NuGet paketi hata ayıklama & sembol geliştirmeleri](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) tasarım belirtimine bakın.
