---
title: Eski sembol paketleri oluşturma (.symbols.nupkg)
description: Visual Studio'daki diğer NuGet paketlerinin hata ayıklamasını desteklemek için yalnızca semboller içeren NuGet paketleri nasıl oluşturulur?
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476275"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>Eski sembol paketleri oluşturma (.symbols.nupkg)

> [!Important]
> Sembol paketleri için önerilen yeni biçim .snupkg'dır. Bkz. [Sembol paketleri oluşturma (.snupkg)](Symbol-Packages-snupkg.md). </br>
> .symbols.nupkg hala ancak uyumluluk nedenleriyle desteklenir.

NuGet, nuget.org veya diğer kaynaklar için paket oluşturmanın yanı sıra, sembol sunucularında yayımlanabilen ilişkili sembol paketleri oluşturmayı da destekler. Eski sembol paketi biçimi, .symbols.nupkg, SymbolSource deposuna itilebilir.

Paket tüketicileri `https://nuget.smbsrc.net` daha sonra Visual Studio'daki sembol kaynaklarına ekleyebilir, bu da Visual Studio hata ayıklayıcısında paket koduna adım atmanızı sağlar. Bkz. Bu işlemle ilgili ayrıntılar için [Visual Studio hata ayıklamasında ki simge (.pdb) ve kaynak dosyaları belirtin.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)

## <a name="creating-a-legacy-symbol-package"></a>Eski sembol paketi oluşturma

Eski bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:

- Birincil paketi (kodunuzla) `{identifier}.nupkg` adlandırın ve `.pdb` dosyalar hariç tüm dosyalarınızı ekleyin.
- Eski simge paketini `{identifier}.symbols.nupkg` adlandırın ve `.pdb` montaj DLL, dosyaları, XMLDOC dosyaları, kaynak dosyaları (aşağıdaki bölümlere bakın) içerir.

Her iki paketi de `-Symbols` `.nuspec` bir dosyadan veya proje dosyasından seçenekle oluşturabilirsiniz:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Mac `pack` OS X'te Mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığını unutmayın. Mac'te, dosyadaki `.nuspec` Windows yol adlarını Unix stili yollara dönüştürmeniz gerekir.

## <a name="legacy-symbol-package-structure"></a>Eski sembol paket yapısı

Eski bir simge paketi, kitaplık paketinin yaptığı gibi birden çok hedef `lib` çerçevesini hedefleyebilir, bu nedenle klasörün `.pdb` yapısı yalnızca DLL'nin yanında bulunan dosyalar da dahil olmak üzere birincil paketle tam olarak aynı olmalıdır.

Örneğin, .NET 4.0 ve Silverlight 4'ü hedefleyen bir eski sembol paketi şu düzene sahip olur:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Kaynak dosyaları daha sonra, kaynak `src`deponuzun göreli yapısını izlemesi gereken ayrı bir özel klasöre yerleştirilir. Bunun nedeni, PDB'lerin eşleşen DLL'yi derlemek için kullanılan kaynak dosyalarıiçin mutlak yollar içermesi ve yayımlama işlemi sırasında bulunmaları gerektiğidir. Bir temel yol (ortak yol öneki) çıkarılabilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplık düşünün:

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

Klasörün `lib` dışında, eski bir simge paketinin bu düzeni içermesi gerekir:

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

## <a name="referring-to-files-in-the-nuspec"></a>Nuspec'teki dosyalara atıfta

Eski sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin `files` bölümünde içeriğini belirterek, sözleşmeler tarafından oluşturulabilir. Örneğin, önceki bölümde gösterilen paketi oluşturmak için `.nuspec` dosyada aşağıdakileri kullanın:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>Eski sembol paketini yayımlama

> [!Important]
> Paketleri nuget.org itmek için gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v4.9.1 veya üzeri](https://www.nuget.org/downloads)nikullanmalısınız.

1. Kolaylık sağlamak için öncelikle API anahtarınızı NuGet ile kaydedin (bkz. hem nuget.org hem de symbolsource.org için geçerli olacak [bir paket yayımla,](../nuget-org/publish-a-package.md)çünkü symbolsource.org paket sahibi olduğunuzu doğrulamak için nuget.org ile kontrol edecektir.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Birincil paketinizi nuget.org yayımladıktan sonra, dosya adındaki dosya adı nedeniyle `.symbols` symbolsource.org otomatik olarak hedef olarak kullanacak olan eski sembol paketini aşağıdaki gibi itin:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Farklı bir sembol deposunda yayımlamak veya adlandırma kuralına uymayan eski bir simge paketini `-Source` zorlamak için aşağıdaki seçeneği kullanın:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Ayrıca, hem birincil hem de sembol paketlerini aşağıdakileri kullanarak aynı anda her iki depoya da itebilirsiniz:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > nuget.exe 4.5.0 veya üzeri ile sembol paketleri otomatik olarak symbolsource.org itilir. Semboller paketlerini daha önceki adımlarda açıklandığı gibi ayrı ayrı itmeniz gerekir.
   
Bu durumda, NuGet `MyPackage.symbols.nupkg`birincil paketi nuget.org https://nuget.smbsrc.net/ yayımladıktan sonra (symbolsource.org için itme URL'si) için yayımlar.

## <a name="see-also"></a>Ayrıca bkz.

* [Sembol paketleri oluşturma (.snupkg)](Symbol-Packages-snupkg.md) - Sembol paketleri için önerilen yeni biçim
* [Yeni SymbolSource motoruna taşıma](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
