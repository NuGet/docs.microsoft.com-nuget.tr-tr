---
title: Eski sembol paketleri oluşturuluyor (. Symbols. nupkg)
description: Visual Studio 'da diğer NuGet paketlerinde hata ayıklamayı desteklemek için yalnızca semboller içeren NuGet paketleri oluşturma.
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774541"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Eski sembol paketleri oluşturuluyor (. Symbols. nupkg)

> [!Important]
> Sembol paketleri için önerilen yeni biçim. snupkg 'dir. Bkz. [sembol paketleri oluşturma (. snupkg)](Symbol-Packages-snupkg.md). </br>
> . Symbols. nupkg hala desteklenir ancak yalnızca uyumluluk nedenleriyle desteklenir.

NuGet, nuget.org veya diğer kaynaklar için paket oluşturmaya ek olarak, sembol sunucularına yayımlanmakta olabilecek ilişkili sembol paketleri oluşturmayı da destekler. Eski sembol paketi biçimi. Symbols. nupkg, SymbolSource deposuna itilmiş olabilir.

Paket tüketicileri, Visual Studio `https://nuget.smbsrc.net` 'da, Visual Studio hata ayıklayıcısında paket koduna adımla izin veren sembol kaynaklarına eklenebilir. Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .

## <a name="creating-a-legacy-symbol-package"></a>Eski sembol paketi oluşturma

Eski bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:

- Birincil paketi (kodunuzla birlikte) adlandırın `{identifier}.nupkg` ve dosyalar hariç tüm dosyalarınızı ekleyin `.pdb` .
- Eski sembol paketini adlandırın `{identifier}.symbols.nupkg` ve derleme DLL 'sini, `.pdb` DOSYALARıNıZı, xmlDoc dosyalarını, kaynak dosyalarınızı (izleyen bölümlere bakın) ekleyin.

`-Symbols`Bir `.nuspec` dosya ya da proje dosyasından, seçeneğiyle her iki paket de oluşturabilirsiniz:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

`pack`Mac OS X mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığına not edin. Mac 'te Ayrıca, dosyadaki Windows yol adlarını `.nuspec` UNIX stili yollara dönüştürmeniz gerekir.

## <a name="legacy-symbol-package-structure"></a>Eski sembol paketi yapısı

Eski bir sembol paketi, bir kitaplık paketiyle aynı şekilde birden çok hedef çerçeveyi hedefleyebilir, bu nedenle `lib` klasörün yapısı yalnızca dll ile birlikte dosyalar dahil olmak üzere birincil paket ile tam olarak aynı olmalıdır `.pdb` .

Örneğin, .NET 4,0 ve Silverlight 4 ' ü hedefleyen eski bir sembol paketi bu düzene sahip olacaktır:

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

Kaynak dosyalar daha sonra adlı ayrı bir özel klasöre yerleştirilir `src` ve bu, kaynak deponuzun göreli yapısına uymalıdır. Bunun nedeni, pdb 'leri 'ın eşleşen DLL 'yi derlemek için kullanılan kaynak dosyalara mutlak yollar içermesi ve yayımlama işlemi sırasında bulunması gerekir. Temel yol (ortak yol öneki) eklenebilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplığı düşünün:

```
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
```

`lib`Klasörden ayrı olarak, eski bir sembol paketinin bu düzeni içermesi gerekir:

```
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
```

## <a name="referring-to-files-in-the-nuspec"></a>Nuspec içindeki dosyalara başvurma

Eski bir sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin bölümünde içeriğini belirterek, kurallara göre derlenebilir `files` . Örneğin, önceki bölümde gösterilen paketi oluşturmak için, dosyasında aşağıdakileri kullanın `.nuspec` :

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Eski bir sembol paketi yayımlanıyor

> [!Important]
> Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v 4.9.1 veya üzeri](https://www.nuget.org/downloads)bir sürümü kullanmanız gerekir.

1. Daha kolay olması için, önce API anahtarınızı NuGet ile kaydedin (bkz. nuget.org ve symbolsource.org için uygulanacak [bir paket yayımlama](../nuget-org/publish-a-package.md)), bu, paket sahibi olduğunuzu doğrulamak üzere NuGet.org ile kontrol edecektir.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Birincil paketinizi nuget.org ' e yayımladıktan sonra, eski sembol paketini aşağıdaki gibi gönderin. Bu, dosya adında adı nedeniyle otomatik olarak symbolsource.org ' i kullanacaktır `.symbols` .

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Farklı bir sembol deposuna yayımlamak veya adlandırma kuralını takip eden eski bir sembol paketini göndermek için `-Source` seçeneğini kullanın:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Ayrıca, aşağıdakileri kullanarak hem birincil hem de sembol paketlerini aynı anda her iki depoya da gönderebilirsiniz:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > nuget.exe 4.5.0 veya üzeri ile, semboller paketleri otomatik olarak symbolsource.org 'e gönderilmez. Önceki adımlarda açıklandığı gibi semboller paketlerini ayrı olarak göndermeniz gerekir.
   
Bu durumda, NuGet `MyPackage.symbols.nupkg` https://nuget.smbsrc.net/ birincil paketi NuGet.org ' ye yayımladıktan sonra, varsa NuGet (symbolsource.org için gönderim URL 'si) olarak yayımlanır.

## <a name="see-also"></a>Ayrıca bkz.

* [Sembol paketleri (. snupkg) oluşturuluyor](Symbol-Packages-snupkg.md) -sembol paketleri için önerilen yeni biçim
* [Yeni SymbolSource Engine 'e geçme](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
