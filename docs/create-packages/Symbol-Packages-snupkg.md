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
ms.openlocfilehash: 5bd3d02a9f397b393cc56af815c40f9d718d4023
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303631"
---
# <a name="creating-symbol-packages-snupkg"></a>Sembol paketleri (.snupkg) oluşturma

## <a name="prerequisites"></a>Önkoşullar

[nuget.exe v4.9.0 veya yukarıdaki](https://www.nuget.org/downloads) veya [dotnet.exe v2.2.0 veya yukarıdaki](https://www.microsoft.com/net/download/dotnet-core/2.2), hangi uygulamak gerekli [NuGet protokolleri](../api/nuget-protocols.md).

## <a name="creating-a-symbol-package"></a>Bir sembol paketi oluşturma

Bir .nuspec dosyası veya .csproj dosyasını bir snupkg sembol paketi oluşturulabilir. NuGet.exe ve dotnet.exe her ikisi de desteklenir. Zaman seçenekleri ```-Symbols -SymbolPackageFormat snupkg``` .snupkg dosya Environment.specialfolder.ProgramFiles .nupkg dosyasına oluşturulacak nuget.exe paketi komutu kullanılır.

Örnek komutlar .snupkg dosyaları oluşturmak için
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild /t:pack MyPackage.csproj /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
```

`.snupkgs` Varsayılan olarak oluşturulan değil. Geçmesi gereken `SymbolPackageFormat` özelliği ile birlikte `-Symbols` nuget.exe durumunda `--include-symbols` dotnet.exe, durumunda veya `/p:IncludeSymbols` msbuild durumunda.

SymbolPackageFormat özelliği iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`. SymbolPackageFormat belirtilmezse, varsayılan `symbols.nupkg` ve eski sembol paketi oluşturulacak.

> [!Note]
> Eski biçim `.symbols.nupkg` ancak yalnızca uyumluluk açısından hala desteklenmektedir (bkz [eski sembol paketleri](Symbol-Packages.md)). Sembol sunucusuna NuGet.org yalnızca yeni sembol paket biçimi - kabul `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Bir sembol Paketi Yayımlama

1. Kolaylık olması için NuGet ile ilk API anahtarınızı kaydedin (bkz [paket yayımlama](../create-packages/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Nuget.org için birincil paketinizi yayımladıktan sonra aşağıdaki gibi sembol paketi gönderin.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Ayrıca hem birincil hem de anında iletme ve sembol kullanarak aynı anda paketleri aşağıdaki komutu. Her ikisi de .nupkg ve .snupkg dosyaları geçerli klasörde mevcut olması gerekir.

    ```cli
    nuget push MyPackage.nupkg
    ```

Bu durumda, NuGet nuget.org için yayımlayacak `MyPackage.nupkg` ilk ardından `MyPackage.snupkg`.

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
