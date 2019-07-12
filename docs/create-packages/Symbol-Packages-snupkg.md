---
title: Yeni Sembol paket biçimi '.snupkg' kullanarak NuGet sembol paketleri yayımlama | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet sembol paketleri (snupkg) oluşturma
keywords: NuGet sembol paketleri, hata ayıklama, hata ayıklama, paket sembolleri sembol paketi kuralları NuGet destekleyen NuGet paketi
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 9f9cdd188cf2ec678bc9047604e618f1af9124ae
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842459"
---
# <a name="creating-symbol-packages-snupkg"></a>Sembol paketleri (.snupkg) oluşturma

Sembol paketleri NuGet paketlerinizi hata ayıklama deneyimini geliştirmeye olanak sağlar.

## <a name="prerequisites"></a>Önkoşullar

[nuget.exe v4.9.0 veya yukarıdaki](https://www.nuget.org/downloads) veya [dotnet.exe v2.2.0 veya yukarıdaki](https://www.microsoft.com/net/download/dotnet-core/2.2), hangi uygulamak gerekli [NuGet protokolleri](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Bir sembol paketi oluşturma

Dotnet.exe, NuGet.exe veya MSBuild'ı kullanarak bir snupkg sembol paketi oluşturabilirsiniz. NuGet.exe kullanıyorsanız .nupkg dosyasının yanı sıra bir .snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Dotnet.exe veya MSBuild'ı kullanıyorsanız .nupkg dosyasının yanı sıra bir .snupkg dosyası oluşturmak için aşağıdaki adımları kullanın:

1. Aşağıdaki özellikler için .csproj dosyasını ekleyin:

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. Projenizle paketi `dotnet pack MyPackage.csproj` veya `msbuild -t:pack MyPackage.csproj`.

[ `SymbolPackageFormat` ](/dotnet/core/tools/csproj#symbolpackageformat) Özelliği iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`. Varsa [ `SymbolPackageFormat` ](/dotnet/core/tools/csproj#symbolpackageformat) özelliği belirtilmezse, eski sembol paketi oluşturulacak.

> [!Note]
> Eski biçim `.symbols.nupkg` ancak yalnızca uyumluluk açısından hala desteklenmektedir (bkz [eski sembol paketleri](Symbol-Packages.md)). Sembol sunucusuna NuGet.org yalnızca yeni sembol paket biçimi - kabul `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Bir sembol Paketi Yayımlama

1. Kolaylık olması için NuGet ile ilk API anahtarınızı kaydedin (bkz [paket yayımlama](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Nuget.org için birincil paketinizi yayımladıktan sonra aşağıdaki gibi sembol paketi gönderin.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Ayrıca hem birincil hem de anında iletme ve sembol kullanarak aynı anda paketleri aşağıdaki komutu. .Nupkg hem .snupkg dosyaları geçerli klasörde mevcut olması gerekir.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet nuget.org için her iki paketi yayımlar. `MyPackage.nupkg` ilk yayımlama, ardından `MyPackage.snupkg`.

> [!Note]
> NuGet.org kaynağı olarak yapılandırdığınız sembol paketi yayımlanmış değil, denetleyin `https://api.nuget.org/v3/index.json`. Sembol Paketi Yayımlama tarafından desteklenen yalnızca [NuGet V3 API](../api/overview.md#versioning).

## <a name="nugetorg-symbol-server"></a>NuGet.org sembol sunucusu

NuGet.org kendi sembolleri sunucu deposu destekler ve yalnızca yeni sembol paket biçimi - kabul `.snupkg`. Paketi tüketicileri, sembol sunucusuna nuget.org ekleyerek yayımlanan simgeleri kullanabilirsiniz `https://symbols.nuget.org/download/symbols` kendi sembol kaynaklarına Visual Studio'da sağlayan Visual Studio hata ayıklayıcısı paket kod içine Adımlama. Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) işlem hakkında ayrıntılı bilgi için.

### <a name="nugetorg-symbol-package-constraints"></a>Nuget.org sembol paketi kısıtlamaları

Sembol paketleri nuget.org üzerinde desteklenen aşağıdaki kısıtlamaları vardır.

- Yalnızca aşağıdaki dosya uzantılarını sembol pakete eklenecek izin verilir. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Yalnızca yönetilen [taşınabilir pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) nuget sembol sunucusunda şu anda desteklenmiyor.
- Ekli PDB'ler ve ilişkili nupkg DLL'lerini Visual Studio sürüm 15.9 ya da üzeri derleyici ile oluşturulması gereken (bkz [pdb şifreleme karması](https://github.com/dotnet/roslyn/issues/24429))

Sembol Paketi Yayımlama üzerinde herhangi bir dosya türünün içinde .snupkg eklediyseniz nuget.org başarısız olur.

### <a name="symbol-package-validation-and-indexing"></a>Sembol paketi doğrulama ve dizin oluşturma

Sembol paketleri yayımlanan [NuGet.org](https://www.nuget.org/) virüs denetimleri gibi çeşitli doğrulamaları geçeriz.

Paket tüm doğrulama denetimlerini geçtiğinde, dizin ve NuGet.org sembol sunucularından tüketim için kullanılabilir semboller için biraz sürebilir. Paket doğrulama denetimi başarısız olursa .nupkg için Paket Ayrıntıları sayfasına ilgili hatayı görüntülemek için güncelleştirir ve ayrıca bunu bildiren bir e-posta alırsınız.

Paket doğrulaması ve dizin oluşturma genellikle 15 dakika alır. Paket yayımlama beklenenden daha uzun sürerse ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org herhangi bir kesinti yaşıyor olmadığını denetlemek için. Tüm sistemler çalışır durumda ve paket başarıyla bir saat içinde yayımlanmadı Lütfen nuget.org için oturum açın ve Paket Ayrıntıları sayfasına başvurun destek bağlantısı kullanarak bize ulaşın.

## <a name="symbol-package-structure"></a>Sembol paket yapısı

.Nupkg dosyanın tam olarak aynı bugün olduğu halde .snupkg dosya aşağıdaki özelliklere sahip gibi olacaktır:

1) .snupkg karşılık gelen .nupkg aynı kimliği ve sürüm gerekir.
2) .snupkg tam klasör yapısını yerine dll/exe, aynı klasör hiyerarşisindeki karşılık gelen kendi pdb eklenecek ayrım ile DLL veya EXE dosyaları için nupkg olur. PDB dışında uzantıları ile dosya ve klasörleri snupkg dışında bırakılır.
3) .snupkg .nuspec dosyasında da yeni bir PackageType aşağıdaki gibi belirtin. Bu, belirtilen yalnızca bir PackageType gerekir. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) Bir yazar kendi nupkg ve snupkg oluşturmak için özel bir nuspec kullanmaya karar verirse, snupkg 2'de ayrıntılı dosya ve klasör hiyerarşisi aynı olmalıdır).
5) ```authors``` ve ```owners``` alan snupkg'ın nuspec ' çıkarılır.

## <a name="see-also"></a>Ayrıca Bkz.

[NuGet-Package - hata ayıklama - ve - sembolleri - iyileştirmeler](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
