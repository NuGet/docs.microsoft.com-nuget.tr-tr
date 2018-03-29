---
title: Bir NuGet paketi oluşturma | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Tasarlama ve dosyaları ve sürüm oluşturma gibi temel karar noktaları da dahil olmak üzere bir NuGet paketi oluşturma işlemi için ayrıntılı bir kılavuz.
keywords: NuGet paket oluşturma, bir paket, nuspec bildirimi, NuGet paketi kuralları, NuGet Paket sürümü oluşturma
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7bb7e16a317aff908effe0b6c603ea53c9e8a563
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-nuget-packages"></a>NuGet paketleri oluşturma

Konular paketinizi yaptığı veya ne kod içerir, kullandığınız `nuget.exe` işlevselliğini paylaşılan ve kullanılan bir bileşen herhangi bir sayıda diğer geliştiriciler tarafından halinde paketlemek için. Yüklemek için `nuget.exe`, bkz: [NuGet CLI yükleme](../install-nuget-client-tools.md#nugetexe-cli). Visual Studio otomatik olarak içermemesi Not `nuget.exe`.

Teknik olarak konuşarak bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olan `.nupkg` uzantısı ve içerikleri belirli kuralları eşleşmesi. Bu konu, bu kuralları karşılayan paket oluşturma ayrıntılı işlemi açıklanır. Odaklanmış bir anlatım için başvurmak [hızlı başlangıç: oluşturma ve bir paket yayımlama](../quickstart/create-and-publish-a-package.md).

Paketleme derlenmiş kod (derlemeler), simgeler ve/veya paket olarak teslim etmek istediğiniz diğer dosyaları şununla başlar (bkz [genel bakış ve iş akışı](overview-and-workflow.md)). Bu işlem derleme veya aksi halde pakete Git dosyalar oluşturma bağımsız, derlenmiş derlemeler ve paketleri eşitlenmiş tutmak için bir proje dosyası'ndan kullanabilirsiniz ancak çizin.

> [!Note]
> Bu konu, Visual Studio 2017 ve NuGet 4.0 + kullanarak .NET Core projeleri dışında proje türleri için geçerlidir. .NET Core projelerdeki NuGet bilgileri proje dosyasında doğrudan kullanır. Ayrıntılar için bkz [oluşturma .NET standart paketlerle Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) ve [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Paketlemek için hangi derlemelerin karar verme

En genel amaçlı paketler diğer geliştiricilerin kendi projelerinde kullanabileceğiniz bir veya daha fazla derlemeleri içerir.

- Genel olarak, her derleme bağımsız olarak yararlıdır koşuluyla NuGet paketi, her bir derleme sağlamak en iyisidir. Örneğin, bir `Utilities.dll` , bağımlı `Parser.dll`, ve `Parser.dll` , kendi yararlıdır sonra her biri için bir paket oluşturun. Böylece geliştiriciler verir `Parser.dll` bağımsız `Utilities.dll`.

- Ardından, kitaplık bağımsız olarak yararlı olmayan birden çok derlemelerinin oluşuyorsa, bir pakete birleştirmek sorun yoktur. Önceki örnekte, kullanarak `Parser.dll` yalnızca kullanılan kodu içeren `Utilities.dll`, tutmak uygundur sonra `Parser.dll` aynı pakette.

- Benzer şekilde, varsa `Utilities.dll` bağlıdır `Utilities.resources.dll`, burada yeniden ikinci her ikisinde de aynı paket put, kendi, kullanışlı değildir.

Kaynak aslında, özel bir durum yok. Bir paket bir projeye yüklendiğinde, NuGet paket DLL'leri derleme başvuruları otomatik olarak ekler. *hariç* adlandırıldığı o `.resources.dll` yerleştirilmiş yardımcı derlemeler (bkz: olarakkabulçünkü[ Yerelleştirilmiş paketleri oluşturma](creating-localized-packages.md)). Bu nedenle, kullanmaktan kaçının `.resources.dll` , aksi takdirde temel paket kodu içeren dosyaları için.

Kitaplığınızı yönergeleri COM birlikte çalışma derlemeleri, ek izleme içeriyorsa [COM birlikte çalışma derlemeleri paketlerle yazma](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rol ve .nuspec dosyası yapısı

İstediğiniz paketlemek için hangi dosyaların öğrendikten sonra sonraki adım bir paket bildirimi oluşturma bir `.nuspec` XML dosyası.

Bildirim:

1. Paketin içeriği açıklar ve kendisi paketine dahil değildir.
1. Her iki paket oluşturmayı sürücüleri ve paket bir projeye yüklemeye nasıl NuGet bildirir. Örneğin, ana paketi yüklendiğinde NuGet bu bağımlılıkları da yükleyebilirsiniz, bildirim diğer Paket bağımlılıklarını tanımlar.
1. Aşağıda açıklandığı gibi gerekli ve isteğe bağlı özellikler içerir. Burada, geçmeyen diğer özellikleri de dahil olmak üzere, tam Ayrıntılar için bkz: [.nuspec başvuru](../reference/nuspec.md).

Gerekli özellikleri:

- Paket tanımlayıcısı paketini barındıran galeri arasında benzersiz olması gerekir.
- Belirli bir sürüm numarasını biçiminde *Major.Minor.Patch [-soneki]* nerede *-soneki* tanımlayan [yayın öncesi sürümleri](prerelease-packages.md)
- Gerektiği gibi (gibi nuget.org) ana bilgisayardaki paket başlığı görüntülenir
- Yazar ve sahibi bilgileri.
- Paket, uzun bir açıklama.

Ortak isteğe bağlı özellikleri:

- Sürüm notları
- Telif hakkı bilgileri
- Kısa bir açıklaması [Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi](../tools/package-manager-ui.md)
- Yerel ayar kimliği
- Giriş sayfası ve lisans URL'leri
- Bir simge URL'si
- Bağımlılıklar ve başvurular listesi
- Galeri aramalarda yardımcı etiketleri

Tipik bir (ancak kurgusal) aşağıdadır `.nuspec` özelliklerini açıklayan yorumlarla dosyası:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>Contoso.Utility.UsefulStuff</id>

    <!-- The package version number that is used when resolving dependencies -->
    <version>1.8.3-beta</version>

    <!-- Authors contain text that appears directly on the gallery -->
    <authors>Dejana Tesic, Rajeev Dey</authors>

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
    <description>Core utility functions for web applications</description>

    <!-- Copyright information -->
    <copyright>Copyright ©2016 Contoso Corporation</copyright>

    <!-- Tags appear in the gallery and can be used for tag searches -->
    <tags>web utility http json url parsing</tags>

    <!-- Dependencies are automatically installed when the package is installed -->
    <dependencies>
        <dependency id="Newtonsoft.Json" version="9.0" />
    </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Bağımlılıklar bildirme ve sürüm numaralarını belirtme hakkında daha fazla bilgi için bkz: [paket sürüm](../reference/package-versioning.md). Ayrıca yüzey varlıklarına bağımlılıkları doğrudan paketindeki gelen kullanarak mümkündür `include` ve `exclude` üzerinde öznitelikleri `dependency` öğesi. Bkz: [.nuspec başvuru - bağımlılıkları](../reference/nuspec.md#dependencies).

Bildirim oluşturulan paketinde yer aldığından herhangi bir sayıda ek örnekler mevcut paketleri inceleyerek bulabilirsiniz. İyi bir kaynaktır *paketleri genel* klasör konumunu aşağıdaki komutu tarafından döndürülen bilgisayarınızda:

```cli
nuget locals -list global-packages
```

Tüm gidin *package\version* klasörü, kopya `.nupkg` dosyasını bir `.zip` dosya sonra açmak `.zip` dosya ve inceleyin `.nuspec` içindeki.

> [!Note]
> Oluştururken bir `.nuspec` bir Visual Studio projesinden paketi yapılandırıldığında projeden bilgilerle değiştirilir belirteçleri bildirimi içerir. Bkz: [.nuspec bir Visual Studio projesi oluşturma](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>.Nuspec dosyası oluşturma

Tam bildirim genellikle oluşturma başlar ile temel bir `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan dosyası:

- [Bir kurala dayalı çalışma dizini](#from-a-convention-based-working-directory)
- [DLL derleme](#from-an-assembly-dll)
- [A Visual Studio project](#from-a-visual-studio-project)    
- [Varsayılan değerlerle yeni dosya](#new-file-with-default-values)

Böylece son paketinde istediğiniz tam içeriğini açıklayan, sonra dosyayı el ile düzenleyin.

> [!Important]
> Oluşturulan `.nuspec` dosyalarını paket ile oluşturmadan önce değiştirilmelidir yer tutucuları içeren `nuget pack` komutu. Komutu, başarısız `.nuspec` herhangi yer tutucular içerir.

### <a name="from-a-convention-based-working-directory"></a>Bir kurala dayalı çalışma dizininden

Bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğundan `.nupkg` uzantısı, kendi genellikle en kolay dosya sisteminde istediğiniz klasör yapısını oluşturun ardından oluşturma `.nuspec` yapıyı doğrudan dosyasından. `nuget pack` Komut sonra otomatik olarak ekler tüm dosyaları bu klasör yapısındaki (ile başlayan tüm klasörleri hariç `.`, aynı yapısında özel dosyaları tutmak izin vererek).

Bu yaklaşımın avantajı, hangi dosyaların paketin içinde (Bu konunun ilerleyen bölümlerinde açıklandığı gibi) dahil etmek istediğiniz bildiriminde belirtmeniz gerekmez ' dir. Pakete gider tam klasör yapısı oluşturmak, oluşturma işlemi yalnızca olabilir ve bir projenin parçası Aksi durumda olmayabilir diğer dosyaları kolayca ekleyebilirsiniz:

- Hedef projeye eklenen içerik ve kaynak kodu.
- PowerShell komut dosyaları (NuGet içinde desteklenmeyen 2.x yükleme betikleri de dahil edebilirsiniz NuGet kullanılan paketler 3.x ve üzeri).
- Projede mevcut yapılandırma ve kaynak kodu dosyaları için dönüştürmeleri.

Klasör kuralları aşağıdaki gibidir:

| Klasör | Açıklama | Paketi Yükle üzerine gerçekleştirilecek eylemi |
| --- | --- | --- |
| (kök) | Readme.txt konumu | Paketi yüklendiğinde, visual Studio Paketi kök dizininde readme.txt dosyasına görüntüler. |
| lib/{tfm} | Derleme (`.dll`), belgeleri (`.xml`) ve simge (`.pdb`) dosyaları belirtilen hedef Framework bilinen ad (TFM) için | Derlemeleri başvuru olarak eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır. Bkz: [birden çok hedef çerçeveyi destekleyen](supporting-multiple-target-frameworks.md) framework hedef özgü alt klasörleri oluşturmak için. |
| Çalışma zamanları | Mimariye özel derleme (`.dll`), simge (`.pdb`) ve yerel kaynak (`.pri`) dosyaları | Derlemeleri başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır. Bkz: [birden çok hedef çerçeveyi destekleyen](supporting-multiple-target-frameworks.md). |
| içerik | İsteğe bağlı dosyalar | İçeriği proje kök dizinine kopyalanır. Düşünün **içerik** sonuçta paket tüketir hedef uygulama kökü olarak klasör. Paketi uygulamanın bir görüntüsünü Ekle olmasını */görüntüleri* klasörü, paketin içinde yerleştirin *içeriği/görüntüleri* klasör. |
| derleme | MSBuild `.targets` ve `.props` dosyaları | Otomatik olarak proje dosyasına eklenen veya `project.lock.json` (NuGet 3.x+). |
| araçlar | PowerShell komut dosyaları ve programları Paket Yöneticisi Konsolu'ndan erişilebilir | `tools` Klasörü eklenen `PATH` yalnızca Paket Yöneticisi konsolu için ortam değişkeni (özellikle *değil* için `PATH` projesi oluştururken MSBuild için belirlenen). |

Klasör yapısı herhangi bir sayıda hedef çerçeve için derlemeleri herhangi bir sayıda içerdiğinden bu yöntem, birden çok çerçeveyi destekleyen paket oluştururken gereklidir 

İstenen klasör yapısı yerinde olduktan sonra oluşturmak için bu klasörde herhangi bir durumda, aşağıdaki komutu çalıştırın `.nuspec` dosyası:

```cli
nuget spec
```

Yeniden oluşturulan `.nuspec` dosyaları klasörü yapısı içinde hiçbir açık başvurular içeriyor. Paketi oluştururken NuGet tüm dosyaları otomatik olarak ekler. Hala bildiriminin diğer bölümlerinde yer tutucu değerlerini ancak düzenlemeniz gerekir.

### <a name="from-an-assembly-dll"></a>Bir derlemeyi DLL

Bir derlemeye ait bir paket oluşturma en basit durumda, oluşturduğunuz bir `.nuspec` aşağıdaki komutu kullanarak derleme meta dosyası:

```cli
nuget spec <assembly-name>.dll
```

Bu formu kullanarak derlemesinden belirli değerleri içeren birkaç yer tutucuları bildiriminde yerini alır. Örneğin, `<id>` özelliği, derleme adı için ayarlanır ve `<version>` derleme sürümünü ayarlayın. Diğer özellikler bildiriminde ancak yoksa eşleşen değerleri bütünleştirilmiş ve hala böylece yer tutucuları içerir.

### <a name="from-a-visual-studio-project"></a>Bir Visual Studio Proje

Oluşturma bir `.nuspec` gelen bir `.csproj` veya `.vbproj` bu projeye yüklü diğer paketleri otomatik olarak bağımlılıklar olarak başvurulduğundan dosya uygun. Yalnızca proje dosyası ile aynı klasörde aşağıdaki komutu kullanın:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Elde edilen `<project-name>.nuspec` dosyasını içeren *belirteçleri* , yerini paketleme zaman önceden yüklenmiş olan diğer Paketlerine yönelik başvuruları dahil olmak üzere projeden değerlere sahip.

Bir belirteç virgülle ayrılan `$` proje özelliği her iki tarafında simgeler. Örneğin, `<id>` bu şekilde genellikle oluşturulan bildiriminde değer şu şekilde görünür:

```xml
<id>$id$</id>
```

Bu belirteç ile değiştirilir `AssemblyName` zaman sevk adresindeki Proje dosyasından değeri. Proje değerlerin tam eşlemesi için `.nuspec` belirteçleri bkz [değiştirme belirteçleri başvuru](../reference/nuspec.md#replacement-tokens).

Belirteçleri hafifletmek, sürüm numarası gibi önemli değerleri güncelleştirmek gerek `.nuspec` proje güncelleştirin. (Her zaman belirteçleri değişmez değerler ile isterseniz değiştirebileceğiniz). 

Kullanılabilir olduğundan emin birkaç ek paketleme seçenekleri bir Visual Studio projesinden çalışırken açıklandığı gibi Not [.nupkg dosyasını oluşturmak için nuget paketi çalıştıran](#running-nuget-pack-to-generate-the-nupkg-file) daha sonra.

#### <a name="solution-level-packages"></a>Çözüm düzeyi paketleri

*NuGet yalnızca 2.x. NuGet 3.0 + kullanılamaz.*

NuGet 2.x desteklenen araçları veya ek komutlar için Paket Yöneticisi konsolu yükleyen bir çözüm düzeyi paket kavramı (içeriğini `tools` klasör), başvurular, içerik, eklemeyin veya hiçbir projede özelleştirmeleri yapı ancak çözümü. Kendi doğrudan hiçbir dosyaları gibi paketlerin içeren `lib`, `content`, veya `build` klasörlerin ve bağımlılıklarını hiçbiri sahip kendi ilgili dosyalarında `lib`, `content`, veya `build` klasörler.

NuGet parçaları çözüm düzeyi paketlerinde yüklü bir `packages.config` dosyasını `.nuget` projenin yerine klasör `packages.config` dosya.

### <a name="new-file-with-default-values"></a>Varsayılan değerlerle yeni dosya

Aşağıdaki komut bir varsayılan bildirimi yer tutucularını, uygun dosya yapısıyla başlayın sağlayan oluşturur:

```cli
nuget spec [<package-name>]
```

Atlarsanız \<paket adı\>, sonuçta elde edilen dosya `Package.nuspec`. Bir ad gibi sağlarsanız, `Contoso.Utility.UsefulStuff`, dosya `Contoso.Utility.UsefulStuff.nuspec`.

Elde edilen `.nuspec` değerleri ister için yer tutucuları içeren `projectUrl`. En son oluşturmak amacıyla kullanmadan önce dosyayı düzenlemek mutlaka `.nupkg` dosya.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Benzersiz paket tanımlayıcısı seçme ve sürüm numarasını ayarlama

Paket tanımlayıcısı (`<id>` öğesi) ve uygulamanın sürüm numarasını (`<version>` öğesi) benzersiz şekilde pakette yer alan tam kodu belirttikleri iki en önemli bildiriminde değerlerdir.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: tanımlayıcısı nuget.org veya ne olursa olsun galeri paketi barındıran arasında benzersiz olması gerekir. Üzerinde bir tanımlayıcı karar vermeden önce ad zaten kullanımda olup olmadığını denetlemek için uygulanabilir galeri arayın. Çakışmaları önlemek için iyi bir desen şirket adınızı tanımlayıcı ilk parçası olarak gibi kullanmaktır `Contoso.`.
- **Namespace benzeri adları**: .NET, kısa çizgi yerine noktalı gösterim kullanılarak ad alanları için benzer bir yol izler. Örneğin, `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`. Paket tanımlayıcısı kod içinde kullanılan ad alanları eşleştiğinde tüketicileri de yararlı.
- **Örnek paketler**: başka bir paket kullanmak için iliştirmek nasıl gösteren örnek kod paketi oluşturmak, `.Sample` giriş olarak tanımlayıcısına soneki olarak `Contoso.Utility.UsefulStuff.Sample`. (Örnek paketi Elbette başka bir paketi bir bağımlılık gerekir.) Bir örnek paket oluştururken, daha önce açıklanan kurala dayalı çalışma dizini yöntemini kullanın. İçinde `content` klasör adında bir klasör örnek kodda düzenleme `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, bu kesinlikle gerekli olmasa da kitaplığı eşleşecek şekilde paketin sürümü ayarlayın. Bir paketi tek bir derleme sınırladığınızda atmaktan daha önce açıklandığı gibi budur [hangi derlemelerin pakete karar](#deciding-which-assemblies-to-package). Genel olarak, bağımlılıkları, derleme sürümlerini çözülürken kendisini NuGet paketi sürümleri ile ilgilenir unutmayın.
- Standart sürüm düzeni kullanırken açıklandığı şekilde NuGet sürüm kuralları dikkate aldığınızdan emin olun [paket sürüm](../reference/package-versioning.md).

> Kısa blog gönderileri aşağıdaki bir dizi ayrıca sürüm anlaşılması yararlı olur:
>
> - [1. Kısım: Alma DLL cehennemi üzerinde](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [2. Kısım: Çekirdek algoritması](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3. Kısım: bağlama yeniden yönlendirmeleri aracılığıyla Birleştirici](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Ayar paket türü

NuGet ile 3.5 +, paketleri ile belirli bir işaretlenebilir *paket türü* kullanım amacı belirtmek için. NuGet, önceki sürümleriyle oluşturulan tüm paketleri de dahil olmak üzere bir türü ile işaretli olmayan paketler için varsayılan değer `Dependency` türü.

- `Dependency` türü paketleri kitaplıkları ve uygulamalar için derleme veya çalışma zamanı varlıklar ekleyin ve (uyumlu olduğu varsayılarak) herhangi bir proje türü yüklenebilir.

- `DotnetCliTool` türü paketlerdir uzantıları [.NET CLI](/dotnet/articles/core/tools/index) ve komut satırından çağrılır. Gibi paketlerin, yalnızca .NET çekirdeği projelerinde yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur. Bu proje başına uzantıları hakkında daha fazla ayrıntı kullanılabilir [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgeleri.

- Özel tür paketleri paket kimlikleri ile aynı biçimi kurallara uyan bir rastgele türü tanımlayıcı kullanın. Herhangi türdeki dışında `Dependency` ve `DotnetCliTool`, ancak, Visual Studio'da NuGet Paket Yöneticisi tarafından tanınmıyor.

Paket türleri ayarlanır `.nuspec` dosya. Geriye dönük için en iyi uyumluluk *değil* açıkça ayarlanmış `Dependency` yazın ve bunun yerine bu türü tür varsayılarak NuGet üzerinde yararlanmayı belirtilir.

- `.nuspec`: İçinde paket türünü gösteren bir `packageTypes\packageType` düğümü altında `<metadata>` öğe:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>Bir Benioku ve diğer dosyaları ekleme

Doğrudan pakete eklenecek dosyaları belirtmek için kullanın `<files>` düğümünde `.nuspec` dosyası, hangi *izleyen* `<metadata>` etiketi:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Add a readme -->
    <file src="readme.txt" target="" />

    <!-- Add files from an arbitrary folder that's not necessarily in the project -->
    <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Çalışma dizini kurala dayalı yaklaşım kullanırken, readme.txt paket kök ve diğer içerik yerleştirebilirsiniz `content` klasör. Hayır `<file>` öğeleridir bildiriminde gerekli.

Adlı bir dosya eklediğinizde `readme.txt` paket kök, Visual Studio bu dosyanın içeriğini düz metin olarak hemen paketi doğrudan yüklendikten sonra görüntüler. (Benioku dosyaları bağımlılıklar olarak yüklenen paketler için görüntülenmez). Örneğin, işte nasıl HtmlAgilityPack paketi için Benioku görüntülenir:

![Yükleme sonrasında bir NuGet paketi için Benioku dosyasını görüntüleme](media/Create_01-ShowReadme.png)

> [!Note]
> Boş bir eklerseniz `<files>` düğümünde `.nuspec` dosyası NuGet içermez herhangi bir içerik paketinde ne olduğunu dışında `lib` klasör.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>MSBuild özellik ve hedefleri bir pakete dahil etme

Bazı durumlarda, özel araç veya işlem sırasında derleme çalıştırma gibi paketinizi tüketen projelerine özel derleme hedefler ya da özellikleri eklemek isteyebilirsiniz. Dosya biçiminde girerek bunu `<package_id>.targets` veya `<package_id>.props` (gibi `Contoso.Utility.UsefulStuff.targets`) içinde `\build` projenin klasör.

Kök dosyalarında `\build` tüm çerçeveler hedef için klasör uygun değerlendirilir. Çerçeveye özel dosyaları sağlamak için önce aşağıdaki gibi uygun alt içinde bulunanlar koyun:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Ardından `.nuspec` dosya, bu dosyaları başvurmak mutlaka `<files>` düğümü:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
    <!-- Include everything in \build -->
    <file src="build\**" target="build" />

    <!-- Other files -->
    <!-- ... -->
    </files>
</package>
```

MSBuild özellik ve hedefleri bir pakete dahil edildi [NuGet 2.5 ile sunulan](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), bu nedenle eklemeniz önerilir `minClientVersion="2.5"` özniteliğini `metadata` için gereken en düşük NuGet İstemcisi sürüm belirtmek için öğesi Paket kullanabilir.

NuGet paketi ile yüklendiğinde `\build` dosyaları MSBuild ekler `<Import>` işaret proje dosyasındaki öğeleri `.targets` ve `.props` dosyaları. (`.props` proje dosyası; en üstte eklenir `.targets` altındaki eklenir.) Ayrı bir koşullu MSBuild `<Import>` öğesi, her hedef çerçeve için eklenir.

MSBuild `.props` ve `.targets` arası framework hedefleme yerleştirilebilir dosyalarının `\buildCrossTargeting` klasör. Karşılık gelen NuGet paketi yüklemesi sırasında ekler `<Import>` hedef Framework'ü ayarlanmamış koşuluyla, proje dosyası öğelerine (MSBuild özelliği `$(TargetFramework)` boş olması gerekir).

NuGet ile 3.x hedefleri projeye eklenmez ancak bunun yerine kullanılabilir hale getirilir `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>COM birlikte çalışma derlemeleri paketlerle yazma

COM birlikte çalışma derlemeleri içeren paketleri uygun bir içermelidir [hedefler dosyası](#including-msbuild-props-and-targets-in-a-package) böylece doğru `EmbedInteropTypes` meta veri PackageReference biçimini kullanarak projelerine eklenir. Varsayılan olarak, `EmbedInteropTypes` meta verileri olduğundan her zaman tüm derlemeler için false PackageReference kullanıldığında, hedefler dosyası bu meta verileri açıkça ekler. Çakışmaları önlemek için hedef adı benzersiz olmalıdır; İdeal olarak, paket adı ve katıştırılmış, değiştirerek olan derleme oluşan bir bileşim kullanmanız `{InteropAssemblyName}` aşağıdaki örnekte bu değere sahip. (Ayrıca bkz. [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek için.)

```xml
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Kullanırken dikkat edin `packages.config` yönetim biçimi'nın paketlerinden derlemeler başvuruları ekleme neden olan NuGet ve Visual Studio COM birlikte çalışma derlemeleri için denetleyin ve ayarlamak `EmbedInteropTypes` proje dosyasında true. Bu durumda hedefleri kılınmadı ' dir.

Ayrıca, varsayılan olarak [yapı varlıklar akan geçişli](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Projeyi project başvurusundan geçişli bağımlılık olarak çekildiğinde burada iş farklı bir şekilde açıklandığı gibi yazılan paketler. Paket tüketici yapı içermeyecek şekilde PrivateAssets varsayılan değerini değiştirerek akmasına izin verebilirsiniz.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>.Nupkg dosyasını oluşturmak için nuget paketi çalıştırma

Bir derlemeyi ya da kurala dayalı çalışma dizini kullanarak, bir paket çalıştırarak oluşturduğunuzda `nuget pack` ile `.nuspec` dosya, değiştirme `<manifest-name>` , belirli dosya adı:

```cli
nuget pack <project-name>.nuspec
```

Visual Studio projesi kullanırken çalıştırmak `nuget pack` , proje dosyası ile otomatik olarak yükleyen projenin `.nuspec` dosya ve proje dosyasında değerleri kullanarak içinde herhangi bir belirtece değiştirir:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Proje dosyası kullanarak doğrudan proje simge değerlerini kaynağı olduğundan belirteci yapabilmek için gereklidir. Belirteç değiştirme olmayacak kullanırsanız `nuget pack` ile bir `.nuspec` dosyası.

Tüm durumlarda `nuget pack` gibi bir noktayla başlayan klasörleri dışlar `.git` veya `.hg`.

NuGet gösteren herhangi bir hata olup olmadığını `.nuspec` bildiriminde yer tutucu değerlerini değiştirmek işlerle gibi düzeltilmesi gereken dosya.

Bir kez `nuget pack` başarılı, sahip olduğunuz bir `.nupkg` açıklandığı gibi uygun bir Galeriye yayımlayabilirsiniz dosya [yayımlama bir paketi](../create-packages/publish-a-package.md).

> [!Tip]
> İçinde açmak için oluşturma tamamlandıktan sonra bir paket incelemek için kullanışlı bir yol [paket Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracı. Bu paket içeriğini ve onun bildirimi grafik bir görünümünü sağlar. Elde edilen adlandırabilirsiniz `.nupkg` dosyasını bir `.zip` dosya ve içeriğini doğrudan inceleyin.

### <a name="additional-options"></a>Ek Seçenekler

Çeşitli komut satırı anahtarları ile kullanabileceğiniz `nuget pack` dosyaları hariç tutmak, bildiriminde sürüm numarası geçersiz kılmak ve diğer özellikler arasında çıkış klasörü değiştirin. Tam bir listesi için bkz [pack komut başvurusu](../tools/cli-ref-pack.md).

Aşağıdaki seçenekler, birkaç Visual Studio projeleri ile ortak şunlardır:

- **Projeleri başvurulan**: Proje diğer projeler başvuruyorsa, başvurulan projeleri paketinin bir parçası olarak ya da bağımlılık, kullanarak ekleyebileceğiniz `-IncludeReferencedProjects` seçeneği:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Bu ekleme işlemi yinelemelidir dolayısıyla `MyProject.csproj` başvuruları projeleri B ve C ve bu projeler başvuru D, E ve F, ardından B, C D E ve F dosyalarından pakete dahil edilir.

    Başvuruda bulunulan bir proje içeriyorsa, bir `.nuspec` sonra kendi, NuGet dosyasının başvurulan proje bunun yerine bir bağımlılık olarak ekler.  Paket ve proje ayrıca yayımlamanız gerekir.

- **Derleme Yapılandırması**: varsayılan olarak, varsayılan derleme yapılandırması proje dosyasında genellikle ayarlanmış NuGet kullanır *hata ayıklama*. Farklı bir yapı yapılandırma dosyaları gibi paketlemek için *sürüm*, kullanın `-properties` yapılandırma seçeneğiyle:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Simgeler**: hata ayıklayıcı paket kodunuzda adım adım tüketicilerin izin simgeleri eklemek için kullanın `-Symbols` seçeneği:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Test paketi yükleme

Bir paket yayımlamadan önce genellikle bir paket bir projeye yükleme işlemi test etmek istediğiniz. Testleri olduğundan emin olun mutlaka tüm şunun kendi doğru yerde projedeki dosyaları.

Visual Studio'da veya normal kullanarak komut satırında el ile yüklemeleri komutunu sınayabilirsiniz [yükleme adımlarını paketini](../consume-packages/ways-to-install-a-package.md).

Otomatik test için temel işlem aşağıdaki gibidir:

1. Kopya `.nupkg` dosyasını bir yerel klasöre.
1. Paket kaynaklarınızın kullanarak klasörü Ekle `nuget sources add -name <name> -source <path>` komutu (bkz [nuget kaynakları](../tools/cli-ref-sources.md)). Yalnızca bu yerel kaynağı kez verilen herhangi bir bilgisayarda ayarlamanız unutmayın.
1. Bu kaynak kullanarak paketi yükleyin `nuget install <packageID> -source <name>` nerede `<name>` verilen kaynak adıyla eşleşen `nuget sources`. Kaynağını belirterek, bu kaynak paketinin yüklü olduğu sağlar.
1. Dosyaların doğru yüklü olduğunu denetlemek için dosya sistemini inceleyin.

## <a name="next-steps"></a>Sonraki Adımlar

Olan bir paketi oluşturduktan sonra bir `.nupkg` dosyası yayımlayarak, tercih ettiğiniz Galerisine açıklandığı gibi [yayımlama bir paketi](../create-packages/publish-a-package.md).

Paketinizi yeteneklerini veya aksi halde aşağıdaki konularda açıklandığı gibi başka senaryoları destekleyecek isteyebilirsiniz:

- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Kaynak ve yapılandırma dosyaları dönüşümleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Yayın öncesi sürümleri](../create-packages/prerelease-packages.md)

Son olarak, dikkat edilmesi gereken ek paket türleri vardır:

- [Yerel Paketler](../create-packages/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages.md)
