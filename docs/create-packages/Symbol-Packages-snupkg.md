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
ms.openlocfilehash: 0109aea95ec255b3e0abcdff4cf51b4bfeafbb8c
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813487"
---
# <a name="creating-symbol-packages-snupkg"></a>Sembol paketleri (. snupkg) oluşturuluyor

Sembol paketleri, NuGet paketlerinizin hata ayıklama deneyimini iyileştirmenize olanak tanır.

## <a name="prerequisites"></a>Prerequisites

gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.9.0 veya üzeri](https://www.nuget.org/downloads) ya da [DotNet. exe v 2.2.0 veya üzeri](https://www.microsoft.com/net/download/dotnet-core/2.2).

## <a name="creating-a-symbol-package"></a>Sembol paketi oluşturma

DotNet. exe veya MSBuild kullanıyorsanız,. nupkg dosyasına ek olarak bir. snupkg dosyası oluşturmak için `IncludeSymbols` ve `SymbolPackageFormat` özelliklerini ayarlamanız gerekir.

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

NuGet. exe kullanıyorsanız,. nupkg dosyasına ek olarak bir. snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) özelliği iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`. Bu özellik belirtilmezse, eski bir sembol paketi oluşturulur.

> [!Note]
> Eski biçim `.symbols.nupkg` hala destekleniyor ancak yalnızca uyumluluk nedenleriyle desteklenir (bkz. [eski sembol paketleri](Symbol-Packages.md)). NuGet. org 'ın sembol sunucusu yalnızca `.snupkg`yeni sembol paketi biçimini kabul eder.

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

NuGet, her iki paketi de nuget.org 'e yayımlar. `MyPackage.nupkg` önce yayımlanacak, ardından `MyPackage.snupkg`.

> [!Note]
> Sembol paketi yayınlanmamışsa, NuGet.org kaynağını `https://api.nuget.org/v3/index.json`olarak yapılandırdığınızdan emin olun. Sembol paketi yayımlaması yalnızca [NuGet v3 API 'si](../api/overview.md#versioning)tarafından desteklenir.

## <a name="nugetorg-symbol-server"></a>NuGet.org symbol sunucusu

NuGet.org kendi sembolleri sunucu deposunu destekler ve yalnızca yeni sembol paketi biçimini kabul eder `.snupkg`. Paket tüketicileri, Visual Studio hata ayıklayıcısında paket koduna Adımlama sağlayan Visual Studio 'daki sembol kaynaklarına `https://symbols.nuget.org/download/symbols` ekleyerek nuget.org sembol sunucusunda yayınlanan sembolleri kullanabilir. Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org sembol paketi kısıtlamaları

NuGet.org, sembol paketleri için aşağıdaki kısıtlamalara sahiptir:

- Sembol paketlerinde yalnızca şu dosya uzantılarına izin veriliyor: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- NuGet. org 'ın sembol sunucusunda yalnızca yönetilen [Taşınabilir pdb 'leri](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) desteklenir.
- Pdb 'leri ve ilişkili. nupkg dll 'Lerinin Visual Studio sürüm 15,9 veya üzeri bir derleyici ile oluşturulması gerekir (bkz. [pdb şifre karması](https://github.com/dotnet/roslyn/issues/24429))

NuGet.org 'e yayınlanan sembol paketleri, bu kısıtlamalar karşılanmazsa doğrulama başarısız olur. 

### <a name="symbol-package-validation-and-indexing"></a>Sembol paketi doğrulama ve dizin oluşturma

[NuGet.org](https://www.nuget.org/) ' de yayınlanan sembol paketleri kötü amaçlı yazılım tarama dahil olmak üzere çeşitli doğrulamalar sağlar. Bir paket doğrulama denetiminden başarısız olursa, paket ayrıntıları sayfasında bir hata mesajı görüntülenir. Ayrıca, paketin sahipleri, tanımlanan sorunları nasıl gidereceğiniz hakkında yönergeler içeren bir e-posta alır.

Sembol paketi tüm doğrulamaları geçtiğinde, semboller NuGet. org 'ın sembol sunucuları tarafından dizine alınır. Dizin oluşturulduktan sonra sembol, NuGet.org sembol sunucularından tüketim için kullanılabilir olacaktır.

Paket doğrulama ve dizin oluşturma genellikle 15 dakika boyunca sürer. Paket yayımlaması beklenenden uzun sürüyorsa, NuGet.org 'in herhangi bir kesinti yaşamadığını denetlemek için [Status.NuGet.org](https://status.nuget.org/) adresini ziyaret edin. Tüm sistemler çalışır durumda ve paket bir saat içinde başarıyla yayımlanmamışsa, lütfen nuget.org ' e oturum açın ve paket ayrıntıları sayfasında desteğe başvurun bağlantısını kullanarak bizimle iletişime geçin.

## <a name="symbol-package-structure"></a>Sembol paketi yapısı

. Nupkg dosyası bugün olduğu gibi tamamen aynıdır, ancak. snupkg dosyası aşağıdaki özelliklere sahip olacaktır:

1) . Snupkg, karşılık gelen. nupkg ile aynı kimliğe ve sürüme sahip olacaktır.
2) . Snupkg, DLL 'Ler veya EXE dosyaları için, dll/EXEs yerine, karşılık gelen pdb 'leri aynı klasör hiyerarşisine dahil edilecek şekilde tam klasör yapısına sahip olur. PDB 'den farklı uzantılara sahip dosyalar ve klasörler, snupkg 'dan bırakılır.
3) . Snupkg içindeki. nuspec dosyası, aşağıda gösterildiği gibi yeni bir PackageType de belirtir. Bu, tek bir PackageType belirtilmelidir.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Bir yazar, nupkg ve snupkg 'leri oluşturmak için özel bir nuspec kullanılmasına karar verirse, snupkg, aynı klasör hiyerarşisine ve 2 ' de ayrıntılı dosyalar içermelidir.
5) Aşağıdaki alanlar, snupkg 'dan nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```ve ```icon```dışarıda bırakılır.
6) ```<license>``` öğesini kullanmayın. A. snupkg, karşılık gelen. nupkg ile aynı lisans kapsamında ele alınmıştır.

## <a name="see-also"></a>Ayrıca bkz.

.NET derlemelerinin kaynak kodu hata ayıklamasını etkinleştirmek için kaynak bağlantısı kullanmayı düşünün. Daha fazla bilgi için lütfen [kaynak bağlantı kılavuzuna](/dotnet/standard/library-guidance/sourcelink)bakın.

Sembol paketleri hakkında daha fazla bilgi için lütfen [NuGet paketi hata ayıklama & sembol geliştirmeleri](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) tasarım belirtimine bakın.
