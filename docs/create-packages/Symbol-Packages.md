---
title: NuGet sembol paketleri oluşturma
description: Visual Studio 'da diğer NuGet paketlerinde hata ayıklamayı desteklemek için yalnızca semboller içeren NuGet paketleri oluşturma.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f7503dd413a976997580aa03da26df0c462ff0e1
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564557"
---
# <a name="creating-symbol-packages-legacy"></a>Sembol paketleri oluşturma (eski)

> [!Important]
> Sembol paketleri için önerilen yeni biçim. snupkg 'dir. Bkz. [sembol paketleri oluşturma (. snupkg)](Symbol-Packages-snupkg.md). </br>
> . Symbols. nupkg hala desteklenir ancak yalnızca uyumluluk nedenleriyle desteklenir.

NuGet, nuget.org veya diğer kaynaklar için paket oluşturmaya ek olarak ilişkili sembol paketleri oluşturmayı ve bunları SymbolSource deposuna yayımlamayı da destekler.

Paket tüketicileri, Visual `https://nuget.smbsrc.net` Studio 'da, Visual Studio hata ayıklayıcısında paket koduna adımla izin veren sembol kaynaklarına eklenebilir. Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

## <a name="creating-a-symbol-package"></a>Sembol paketi oluşturma

Bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:

- Birincil paketi (kodunuzla birlikte) `{identifier}.nupkg` adlandırın ve dosyalar hariç `.pdb` tüm dosyalarınızı ekleyin.
- Sembol paketini `{identifier}.symbols.nupkg` adlandırın ve derleme dll 'sini, `.pdb` dosyalarınızı, xmlDoc dosyalarını, kaynak dosyalarınızı (izleyen bölümlere bakın) ekleyin.

`-Symbols` Bir`.nuspec` dosya ya da proje dosyasından, seçeneğiyle her iki paket de oluşturabilirsiniz:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Mac OS X mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığına not edin. `pack` Mac 'te Ayrıca, `.nuspec` dosyadaki Windows yol adlarını UNIX stili yollara dönüştürmeniz gerekir.

## <a name="symbol-package-structure"></a>Sembol paketi yapısı

Bir sembol paketi birden çok hedef çerçeveyi bir kitaplık paketiyle aynı şekilde hedefleyebilir, bu nedenle `lib` klasörün yapısı yalnızca dll ile birlikte dosyalar dahil olmak üzere `.pdb` birincil paket ile tam olarak aynı olmalıdır.

Örneğin, .NET 4,0 ve Silverlight 4 ' ü hedefleyen bir sembol paketinin bu düzeni olacaktır:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Kaynak dosyalar daha sonra adlı `src`ayrı bir özel klasöre yerleştirilir ve bu, kaynak deponuzun göreli yapısına uymalıdır. Bunun nedeni, pdb 'leri 'ın eşleşen DLL 'yi derlemek için kullanılan kaynak dosyalara mutlak yollar içermesi ve yayımlama işlemi sırasında bulunması gerekir. Temel yol (ortak yol öneki) eklenebilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplığı düşünün:

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

`lib` Klasörden ayrı olarak, bir sembol paketinin bu düzeni içermesi gerekir:

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

## <a name="referring-to-files-in-the-nuspec"></a>Nuspec içindeki dosyalara başvurma

Bir sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin `files` bölümünde içeriğini belirterek, kurallara göre derlenebilir. Örneğin, önceki bölümde gösterilen paketi oluşturmak için, `.nuspec` dosyasında aşağıdakileri kullanın:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Sembol paketi yayımlama

> [!Important]
> Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.9.1 veya üstünü](https://www.nuget.org/downloads)kullanmalısınız.

1. Daha kolay olması için, önce API anahtarınızı NuGet ile kaydedin (bkz. nuget.org ve symbolsource.org için uygulanacak [bir paket yayımlama](../nuget-org/publish-a-package.md)), bu, paket sahibi olduğunuzu doğrulamak üzere NuGet.org ile kontrol edecektir.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Birincil paketinizi NuGet.org 'e yayımladıktan sonra, sembol paketini aşağıdaki gibi gönderin. Bu, dosya adında adı nedeniyle `.symbols` otomatik olarak symbolsource.org ' i kullanacaktır.

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Farklı bir sembol deposuna yayımlamak veya adlandırma kuralını izleyen bir sembol paketini göndermek için `-Source` seçeneğini kullanın:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Ayrıca, aşağıdakileri kullanarak hem birincil hem de sembol paketlerini aynı anda her iki depoya da gönderebilirsiniz:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > NuGet. exe 4.5.0 veya üzeri ile, semboller paketleri otomatik olarak symbolsource.org 'e gönderilmez. Önceki adımlarda açıklandığı gibi semboller paketlerini ayrı olarak göndermeniz gerekir.
   
Bu durumda, NuGet birincil paketi NuGet.org `MyPackage.symbols.nupkg`' ye yayımladıktan sonra https://nuget.smbsrc.net/ , varsa NuGet (symbolsource.org için gönderim URL 'si) olarak yayımlanır.

## <a name="see-also"></a>Ayrıca Bkz.

[Yeni SymbolSource altyapısına geçme](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
