---
title: NuGet sembol paketleri oluşturma
description: NuGet paketi Visual Studio'da hata ayıklamayı desteklemek için yalnızca sembolleri içeren NuGet paketleri oluşturma
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e917895d0fa6ed6dc4bc24b72afc7fa0770f2dd0
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843374"
---
# <a name="creating-symbol-packages"></a>Sembol paketleri oluşturma

Nuget.org veya diğer kaynaklar, NuGet paketlerini de oluşturmaya ek olarak, sembol paketleri ve SymbolSource depoya yayımlama oluşturmayı destekler ilişkili.

Paketi tüketicileri daha sonra ekleyebilirsiniz `https://nuget.smbsrc.net` kendi sembol kaynaklarına Visual Studio'da sağlayan Visual Studio hata ayıklayıcısı paket kod içine Adımlama. Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) işlem hakkında ayrıntılı bilgi için.

## <a name="creating-a-symbol-package"></a>Bir sembol paketi oluşturma

Bir sembol paketi oluşturmak için bu kuralları izleyin:

- (Sizin kodunuz ile) birincil paket adı `{identifier}.nupkg` ve hariç tüm dosyalarınızı eklemek `.pdb` dosyaları.
- Sembol paketi adı `{identifier}.symbols.nupkg` ve bütünleştirilmiş kodunuzda DLL `.pdb` dosyaları, XMLDOC dosyaları, kaynak dosyaları (bölümlerde bakın).

Her iki paketlerle oluşturabilirsiniz `-Symbols` seçeneği,'nden ya da bir `.nuspec` dosyası veya proje dosyası:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Unutmayın `pack` Mac OS X üzerinde Mono 4.4.2 gerektirir ve Linux sistemlerinde çalışmaz. Mac bilgisayarlarda, Windows yol adları olarak da dönüştürmelisiniz `.nuspec` UNIX stili yollara dosya.

## <a name="symbol-package-structure"></a>Sembol paket yapısı

Bir sembol paketi birden çok hedef çerçeve kitaplığı paketi yapan aynı şekilde hedefleyebilirsiniz. böylece yapısını `lib` klasör tam olarak aynı olmalıdır, birincil paketi olarak dahil olmak üzere yalnızca `.pdb` yanında DLL dosyaları.

Örneğin, .NET 4.0 ve Silverlight 4'ü hedefleyen bir sembol paketi bu düzen gerekir:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Kaynak dosyaları ardından adlı ayrı bir özel klasöre yerleştirilen `src`, kaynak deponuza göreli yapısını izlemelidir. Pdb eşleşen DLL derlemek için kullanılan kaynak dosyalarının mutlak yolları içerir ve yayımlama işlemi sırasında bulunması gerekir çünkü budur. Temel bir yol (genel yol ön eki) kullanıma kesilmiş. Örneğin, bu dosyalardaki yerleşik bir kitaplık göz önünde bulundurun:

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

Gelen apart `lib` klasöründe bir sembol paketi gerekir bu düzen içerir:

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

## <a name="referring-to-files-in-the-nuspec"></a>Nuspec dosyalara başvurma

Önceki bölümde açıklandığı gibi bir klasör yapısı kurallarından veya içeriğini belirterek bir sembol paketi oluşturulabilir `files` bildiriminin. Örneğin, önceki bölümde gösterilenle paketi oluşturmak için aşağıdakileri kullanın. `.nuspec` dosyası:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Bir sembol Paketi Yayımlama

> [!Important]
> Anında iletme paketlerine nuget.org'da kullanmalısınız [nuget.exe verze 4.1.0 veya üzeri](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).

1. Kolaylık olması için NuGet ile ilk API anahtarınızı kaydedin (bkz [paket yayımlama](../create-packages/publish-a-package.md)nuget.org hem symbolsource.org geçerli, symbolsource.org doğrulamak için nuget.org ile denetleyecek çünkü paket sahip olursunuz.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Nuget.org için birincil paketinizi yayımladıktan sonra sembol paketi aşağıdaki gibi otomatik olarak symbolsource.org nedeniyle hedefi olarak kullanacak anında iletme `.symbols` dosya:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Farklı bir sembol deposuna yayımlamak için veya yönelik adlandırma kuralını uygulamalıdır olmayan bir sembol paketi göndermeye `-Source` seçeneği:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Ayrıca, hem birincil hem de anında iletme ve paketleri hem de aşağıdaki kullanarak aynı anda simge:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Nuget.exe 4.5.0 veya yukarıdaki simgeleri paketleri otomatik olarak için symbolsource.org itilir değil. Sembol paketleri sonraki adımda açıklandığı gibi ayrı ayrı anında iletme gerekecektir.
   
Bu durumda, NuGet yayımlayacak `MyPackage.symbols.nupkg`için mevcut, https://nuget.smbsrc.net/ (anında iletme URL'si için symbolsource.org) sonra nuget.org için birincil paketi yayımlar.

## <a name="see-also"></a>Ayrıca Bkz.

[Yeni SymbolSource Altyapısı'na taşıma](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
