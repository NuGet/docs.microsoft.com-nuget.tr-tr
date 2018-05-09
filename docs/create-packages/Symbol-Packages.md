---
title: NuGet simgesi paketleri oluşturma
description: Diğer NuGet paketleri Visual Studio'da hata ayıklamayı desteklemek için yalnızca sembolleri içeren NuGet paketleri oluşturma
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cf8761ac4c994d864cd49a8fb31b3be626d4c0a6
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="creating-symbol-packages"></a>Sembol paketleri oluşturma

Nuget.org veya diğer kaynakları NuGet paketleri de oluşturmanın yanı sıra oluşturmayı destekler, simge paketleri ve SymbolSource depoya yayımlama ilişkili.

Paket tüketicileri ardından ekleyebilirsiniz `https://nuget.smbsrc.net` Visual Studio'da simgesi kaynakları için böylece Visual Studio hata ayıklayıcısında paket koda atlama. Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) işlem hakkında ayrıntılı bilgi için.

## <a name="creating-a-symbol-package"></a>Sembol paket oluşturma

Sembol paketi oluşturmak için bu kuralları izleyin:

- Birincil paketiyle (kodunuzu) ad `{identifier}.nupkg` ve tüm dosyalar hariç dahil `.pdb` dosyaları.
- Sembol paket adı `{identifier}.symbols.nupkg` ve derlemenizi DLL dahil `.pdb` dosyaları, XMLDOC dosyaları, kaynak dosyaları (bölümlerde bakın).

Her iki paketlerle oluşturabilirsiniz `-Symbols` herhangi birinden seçeneği bir `.nuspec` veya proje dosyası:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz. Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.

## <a name="symbol-package-structure"></a>Sembol paket yapısı

Sembol paketi birden çok hedef çerçeveyi kitaplık paketi yapan aynı şekilde hedefleyebilirsiniz böylece yapısını `lib` klasörü tam olarak aynı olmalıdır birincil paketi olarak dahil olmak üzere yalnızca `.pdb` yanında DLL dosyaları.

Örneğin, .NET 4.0 ve Silverlight 4 hedefleyen bir sembol paketi bu düzeni sahip olur:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Kaynak dosyalarını sonra adlı ayrı bir özel klasöre yerleştirdiğiniz `src`, kaynak deponuz göreli yapısını izlemelidir. Pdb mutlak yolları eşleşen DLL derlemek için kullanılan kaynak dosyaları içerir ve yayımlama işlemi sırasında bulunması gerekir çünkü budur. Taban yol (ortak yolu önek) çıkarılır. Örneğin, bu dosyaları dışında oluşturulmuş bir kitaplık göz önünde bulundurun:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

Apart gelen `lib` klasörü, bir sembol paketi gerekir bu düzeni içerir:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Nuspec dosyalarında başvurma

Sembol paketi kurallarından önceki bölümde açıklandığı gibi klasör yapısı veya içeriğini belirterek yerleşik `files` bildirim bölümü. Örneğin, önceki bölümde gösterilen paketi oluşturmak için aşağıdakileri kullanın `.nuspec` dosyası:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Sembol Paketi Yayımlama

> [!Important]
> Anında iletme paketlere kullanmalısınız nuget.org için [nuget.exe v4.1.0 veya yukarıdaki](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).

1. Kolaylık olması için NuGet ile ilk API anahtarınıza kaydedin (bkz [bir paketi yayımlamaya](../create-packages/publish-a-package.md)nuget.org ve symbolsource.org için geçerli, symbolsource.org doğrulamak için nuget.org ile denetleyecek olduğundan paket sahibi değil.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Birincil paketiniz için nuget.org yayımlandıktan sonra simge paketini aşağıdaki gibi otomatik olarak symbolsource.org nedeniyle hedefi olarak kullanacak anında `.symbols` dosya:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

   > [!Note]
   > Nuget.exe 4.5.0 veya üzeri, simgeler paketleri otomatik olarak symbolsource.org için gönderilen değil. Sonraki adımda açıklandığı gibi ayrı ayrı simgeleri paketleri göndermek gerekir.

3. Farklı simge depoya yayımlamak ya da adlandırma kuralı IU bir sembol paketi göndermek için kullanmak `-Source` seçeneği:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Ayrıca, hem birincil hem de anında ve aşağıdakileri kullanarak aynı anda hem depoları paketlere simge:

    ```cli
    nuget push MyPackage.nupkg
    ```

Bu durumda, NuGet yayımlayacak `MyPackage.symbols.nupkg`, için varsa, https://nuget.smbsrc.net/ (gönderme URL'sini symbolsource.org), sonra nuget.org için birincil paketi yayımlar.

## <a name="see-also"></a>Ayrıca Bkz.

[Yeni SymbolSource altyapısı taşıma](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)