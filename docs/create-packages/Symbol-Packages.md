---
title: NuGet sembol paketleri oluşturma
description: Visual Studio 'da diğer NuGet paketlerinde hata ayıklamayı desteklemek için yalnızca semboller içeren NuGet paketleri oluşturma.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 97a533171d698792d66a78550dacfe8eaf29a440
ms.sourcegitcommit: fc0f8c950829ee5c96e3f3f32184bc727714cfdb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74253908"
---
# <a name="creating-symbol-packages-legacy"></a>Sembol paketleri oluşturma (eski)

> [!Important]
> Sembol paketleri için önerilen yeni biçim. snupkg 'dir. Bkz. [sembol paketleri oluşturma (. snupkg)](Symbol-Packages-snupkg.md). </br>
> . Symbols. nupkg hala desteklenir ancak yalnızca uyumluluk nedenleriyle desteklenir.

NuGet, nuget.org veya diğer kaynaklar için paket oluşturmaya ek olarak ilişkili sembol paketleri oluşturmayı ve bunları SymbolSource deposuna yayımlamayı da destekler.

Böylece, paket tüketicileri Visual Studio 'daki sembol kaynaklarına `https://nuget.smbsrc.net` ekleyebilir ve bu, Visual Studio hata ayıklayıcısında paket koduna adımlamayı sağlar. Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

## <a name="creating-a-symbol-package"></a>Sembol paketi oluşturma

Bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:

- Birincil paketi (kodunuzla birlikte) adlandırın `{identifier}.nupkg` ve `.pdb` dosyaları hariç tüm dosyalarınızı ekleyin.
- Sembol paketini `{identifier}.symbols.nupkg` adlandırın ve derleme DLL, `.pdb` Files, XMLDOC Files, kaynak dosyaları (izleyen bölümlere bakın) dahil edin.

`-Symbols` seçeneğiyle her iki paketi de oluşturabilirsiniz: bir `.nuspec` dosyası ya da bir proje dosyası:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

`pack` Mac OS X için mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmayacağını unutmayın. Mac 'te Ayrıca, `.nuspec` dosyasındaki Windows yol adları adlarını UNIX stili yollara dönüştürmeniz gerekir.

## <a name="symbol-package-structure"></a>Sembol paketi yapısı

Bir sembol paketi birden çok hedef çerçeveyi bir kitaplık paketiyle aynı şekilde hedefleyebilir, bu nedenle `lib` klasörünün yapısı, yalnızca DLL ile birlikte `.pdb` dosyaları dahil olmak üzere birincil paket ile tam olarak aynı olmalıdır.

Örneğin, .NET 4,0 ve Silverlight 4 ' ü hedefleyen bir sembol paketinin bu düzeni olacaktır:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Kaynak dosyalar daha sonra, kaynak deponuzun göreli yapısını izlemesi gereken `src`adlı ayrı bir özel klasöre yerleştirilir. Bunun nedeni, pdb 'leri 'ın eşleşen DLL 'yi derlemek için kullanılan kaynak dosyalara mutlak yollar içermesi ve yayımlama işlemi sırasında bulunması gerekir. Temel yol (ortak yol öneki) eklenebilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplığı düşünün:

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

`lib` klasörden ayrı olarak, bir sembol paketinin bu düzeni içermesi gerekir:

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

Bir sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin `files` bölümündeki içeriğini belirterek, kurallara göre derlenebilir. Örneğin, önceki bölümde gösterilen paketi oluşturmak için `.nuspec` dosyasında aşağıdakileri kullanın:

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

2. Birincil paketinizi nuget.org 'e yayımladıktan sonra, sembol paketini aşağıdaki gibi gönderin. Bu, dosya adında `.symbols` nedeniyle otomatik olarak symbolsource.org hedefi olarak kullanacaktır:

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
   
Bu durumda, NuGet birincil paketi nuget.org ' ye yayımladıktan sonra, varsa NuGet, varsa https://nuget.smbsrc.net/ (symbolsource.org için gönderim URL 'SI) `MyPackage.symbols.nupkg`yayımlar.

## <a name="see-also"></a>Ayrıca bkz.

[Yeni SymbolSource Engine 'e geçme](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
