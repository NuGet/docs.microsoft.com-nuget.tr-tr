---
title: Bir NuGet paketi oluşturma
description: Ayrıntılı bir kılavuz tasarlama ve dosyaları ve sürüm oluşturma gibi temel karar noktaları da dahil olmak üzere bir NuGet paketi oluşturma işlemidir.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 1bc67927ddc463dcc3a0abe80fe20e625e188e63
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981177"
---
# <a name="creating-nuget-packages"></a>NuGet paketleri oluşturma

Paketiniz yapar veya hangi kod içeren olursa olsun, kullandığınız `nuget.exe` paylaşıldığı ve kullanılan bir bileşen herhangi bir sayıda diğer geliştiriciler tarafından bu işlevselliği paketlemek için. Yüklenecek `nuget.exe`, bkz: [NuGet CLI yükleme](../install-nuget-client-tools.md#nugetexe-cli). Visual Studio otomatik olarak içermez Not `nuget.exe`.

Teknik terimlerle açıklamak gerekirse, bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğu `.nupkg` uzantısı ve içerikleri belirli kuralları eşleşmesi. Bu konuda ayrıntılı bu kuralları karşılayan paket oluşturma işlemi açıklanmaktadır. Odaklanmış bir kılavuz için başvurmak [hızlı başlangıç: bir paketi oluşturma ve yayımlama](../quickstart/create-and-publish-a-package.md).

Derlenmiş kodu (bütünleştirilmiş kodları), simge ve/veya bir paket olarak sunmak istediğiniz diğer dosyaları ile paketleme başlar (bkz [genel bakış ve iş akışı](overview-and-workflow.md)). Bu işlem, derleme veya derlenmiş bütünleştirilmiş kodların ve paketlerin eşitlenmiş şekilde tutmanızı sağlayacak bir proje dosyasında bilgilerden çizebilirsiniz ancak Aksi takdirde pakete Git dosyaları oluşturma bağımsızdır.

> [!Note]
> Bu konu, .NET Core projeleri Visual Studio 2017 ile NuGet 4.0 + dışında proje türleri için geçerlidir. Bu .NET Core projelerinde, NuGet bilgileri proje dosyasında doğrudan kullanır. Ayrıntılar için bkz [.NET standart paketleri oluşturma Visual Studio 2017 ile](../guides/create-net-standard-packages-vs2017.md) ve [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Hangi derlemelerin paketini karar verme

En genel amaçlı paketleri diğer geliştiriciler kendi projelerinde kullanabileceğiniz bir veya daha fazla derlemeleri içerir.

- Genel olarak, her derleme bağımsız olarak faydalı olması şartıyla, NuGet paket başına bir derleme en iyisidir. Örneğin, bir `Utilities.dll` , bağımlı `Parser.dll`, ve `Parser.dll` kendi yararlıdır ve ardından her biri için bir paket oluşturun. Bunun yapılması geliştiricilerin kullanmasına olanak verir `Parser.dll` bağımsız `Utilities.dll`.

- Ardından kitaplığınızı bağımsız olarak faydalı olmayan birden çok derlemelerinin oluşuyorsa, tek bir pakette birleştirip başlatılıyorsa sorun yoktur. Önceki örnekte, kullanarak `Parser.dll` yalnızca kullanılan kodu içeren `Utilities.dll`, tutmak iyi ise `Parser.dll` aynı pakette.

- Benzer şekilde, varsa `Utilities.dll` bağlıdır `Utilities.resources.dll`, burada yeniden ikinci hem de aynı paket yerleştirin, kendi, kullanışlı değildir.

Aslında bir özel durum kaynaklardır. Bir projeye bir paketi yüklendiğinde, NuGet paket DLL'leri derleme başvurularını otomatik olarak ekler. *hariç* adlandırılmış olanlar `.resources.dll` yerelleştirilmiş yardımcı derlemeler (bkz: olarakkabuledilirçünkü[ Yerelleştirilmiş paketler oluşturma](creating-localized-packages.md)). Bu nedenle, kullanmaktan kaçının `.resources.dll` Aksi takdirde, gerekli paket kodu içeren dosyalar için.

COM birlikte çalışma derlemelerini, ek izleme kitaplığınızı yönergeleri içeriyorsa [COM birlikte çalışma derlemelerini paketlerle yazma](#authoring-packages-with-com-interop-assemblies).

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rol ve .nuspec dosyası yapısı

Paket istediğiniz hangi dosyaların öğrendikten sonra sonraki adım bir paketi bildiriminde oluşturma bir `.nuspec` XML dosyası.

Bildirim:

1. Paket içeriğini açıklar ve kendisi paket içerisine dâhil.
1. Sürücü paketi oluşturmaya ve NuGet paketini projeye yükle konusunda bildirir. Örneğin, ana paket yüklendiğinde bu bağımlılıkların NuGet de yükleyebilir, bildirim diğer Paket bağımlılıklarını tanımlar.
1. Aşağıda açıklandığı gibi gerekli ve isteğe bağlı özellikler içerir. Burada, geçmeyen diğer özellikler dahil olmak üzere tam Ayrıntılar için bkz. [.nuspec başvuru](../reference/nuspec.md).

Gerekli özellikler:

- Paket tanımlayıcısı paketini barındıran galeri arasında benzersiz olması gerekir.
- Belirli bir sürüm numarasını biçiminde *ana.İkincil.yama [-soneki]* burada *-soneki* tanımlayan [yayın öncesi sürümleri](prerelease-packages.md)
- Her paket başlık (gibi nuget.org) konak üzerindeki görünür
- Yazar ve sahibi bilgileri.
- Paketinin uzun açıklaması.

Ortak isteğe bağlı özellikler:

- Sürüm notları
- Telif hakkı bilgileri
- Kısa bir açıklaması için [Visual Studio'da Paket Yöneticisi UI](../tools/package-manager-ui.md)
- Bir yerel ayar kimliği
- Giriş sayfası ve lisans URL'leri
- Simge URL'si
- Bağımlılıklar ve başvuru listeleri
- Galeri Arama Yardımcısı etiketleri

Verilmiştir (ancak kurgusal) tipik bir `.nuspec` dosyasıyla özelliklerini açıklayan bir yorum:

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

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
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

Bağımlılıkları bildirme ve sürüm numaraları belirtme hakkında daha fazla bilgi için bkz [Paket sürümü oluşturma](../reference/package-versioning.md). Ayrıca surface varlıklara doğrudan paketindeki bağımlılıklardan kullanarak mümkündür `include` ve `exclude` üzerinde öznitelikleri `dependency` öğesi. Bkz: [.nuspec başvuru - bağımlılıkları](../reference/nuspec.md#dependencies).

Bildirim oluşturulan paketteki dahil olduğundan, mevcut paketleri inceleyerek herhangi bir sayıda ek örnekler bulabilirsiniz. İyi bir kaynaktır *genel paketleri* bilgisayarınızdaki konumunu aşağıdaki komutu tarafından döndürülen klasörü:

```cli
nuget locals -list global-packages
```

Tüm Git *package\version* klasörü, kopyalama `.nupkg` dosyasını bir `.zip` dosya ve ardından, `.zip` inceleyin ve dosya `.nuspec` içindeki.

> [!Note]
> Oluştururken bir `.nuspec` bir Visual Studio projesinden bildirim paketi oluşturulduğunda, projeden bilgileriyle değiştirilir belirteçleri içerir. Bkz: [.nuspec bir Visual Studio projesi oluşturma](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>.Nuspec dosyası oluşturma

Tam bir bildirim oluşturmak genellikle başlar ile temel bir `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan dosya:

- [Kural tabanlı bir çalışma dizini](#from-a-convention-based-working-directory)
- [Bir derlemeyi DLL](#from-an-assembly-dll)
- [Visual Studio projesi](#from-a-visual-studio-project)    
- [Varsayılan değerlerle yeni dosya](#new-file-with-default-values)

Böylece son pakette istediğiniz tam içeriği açıklar, ardından dosyayı el ile düzenleyin.

> [!Important]
> Oluşturulan `.nuspec` dosyaları içeren paket ile oluşturmadan önce değiştirilmelidir yer tutucuları `nuget pack` komutu. Komutu, başarısız `.nuspec` herhangi bir yer tutucu içerir.

### <a name="from-a-convention-based-working-directory"></a>Bir kural tabanlı çalışma dizinine

Bir NuGet paketi yalnızca ile adlandırılmış bir ZIP dosyası olduğundan `.nupkg` uzantısı, genellikle kolay yöntemi, yerel dosya sisteminizde istediğiniz klasör yapısını oluşturmak oluşturup `.nuspec` dosyasını doğrudan, yapı. `nuget pack` Komut daha sonra otomatik olarak ekler tüm dosyaları bu klasör yapısındaki (ile başlayan tüm klasörler hariç `.`, aynı yapı içinde özel dosyaları tutmak izin verme).

Bu yaklaşımın avantajı (Bu konunun ilerleyen kısımlarında açıklandığı gibi) paket içerisine dâhil etmek istediğiniz dosyaları bildiriminde belirtmeniz gerekmez ' dir. Yalnızca yapı işleminizi pakete giden tam bir klasör yapısını oluşturmak olabilir ve gelecekteki bir kolayca Aksi takdirde bir projenin parçası olmayabilir diğer dosyaları dahil edebilirsiniz:

- Hedef projeye eklenen içerik ve kaynak kodu.
- PowerShell betikleri (NuGet içinde desteklenmeyen NuGet 2.x yükleme betikleri de dahil edebilirsiniz kullanılan paketler 3.x ve üzeri).
- Bir projede var olan yapılandırma ve kaynak kodu dosyalarına dönüştürmeler.

Klasör kuralları aşağıdaki gibidir:

| Klasör | Açıklama | Paket yükleme sonrasında eylem |
| --- | --- | --- |
| (kök) | Readme.txt konumu | Paket yüklenirken visual Studio Paket kök dizininde readme.txt dosyasını görüntüler. |
| lib/{tfm} | Derleme (`.dll`), belgeleri (`.xml`) ve simgesi (`.pdb`) dosyaları belirtilen hedef çerçeve adı (TFM) için | Derlemeler, derleme ve bunun yanı sıra çalışma zamanı için başvuru olarak eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır. Bkz: [birden çok hedef çerçeveyi destekleme](supporting-multiple-target-frameworks.md) framework hedef özgü alt klasörler oluşturmak için. |
| ref / {tfm} | Derleme (`.dll`) ve simgesi (`.pdb`) dosyaları belirtilen hedef çerçeve adı (TFM) için | Derlemeleri yalnızca derleme zamanı başvuruları eklenir; Bu nedenle hiçbir proje bin klasörüne kopyalanır. |
| Çalışma zamanları | Mimariye özel derleme (`.dll`), sembol (`.pdb`) ve yerel kaynak (`.pri`) dosyaları | Derlemeleri, yalnızca çalışma zamanı için başvuru olarak eklenir; diğer dosyalar, proje klasörlerine kopyalanır. Ayrıca karşılık gelen (TFM) uymanız gereken `AnyCPU` altında belirli derleme `/ref/{tfm}` karşılık gelen derleme zamanı derlemesi sağlamak için klasör. Bkz: [birden çok hedef çerçeveyi destekleme](supporting-multiple-target-frameworks.md). |
| içerik | Rastgele dosyalar | İçeriği, proje kök dizinine kopyalanır. Düşünün **içeriği** nihai olarak Paketle tüketen hedef uygulamanın kök klasör. Uygulamanın resim ekleme paket için */görüntüleri* klasörü, paketin içinde yerleştirin *içeriği/görüntülerinden* klasör. |
| derleme | MSBuild `.targets` ve `.props` dosyaları | Proje dosyasına otomatik olarak eklenen veya `project.lock.json` (NuGet 3.x+). |
| araçlar | PowerShell betikleri ve programları Paket Yöneticisi konsolunda erişilebilir | `tools` Klasör eklenir `PATH` yalnızca Paket Yöneticisi konsolu için ortam değişkenini (özellikle *değil* için `PATH` projeyi derlerken MSBuild için belirlenen). |

Herhangi bir sayıda hedef çerçeveleri için derlemeler herhangi bir sayıda klasör yapınız içerebileceğinden, bu yöntem, birden çok çerçeveyi destekleyen bir paket oluştururken gereklidir 

Herhangi bir durumda, istenen klasör yapısı yerinde olduktan sonra bu klasörde oluşturmak için aşağıdaki komutu çalıştırın `.nuspec` dosyası:

```cli
nuget spec
```

Yeniden oluşturulan `.nuspec` klasörü yapısı içinde dosyaların açık başvuru içeriyor. Paketi oluşturulduğunda NuGet tüm dosyaları otomatik olarak içerir. Ancak bildirimin diğer bölümlerinde yer tutucu değerlerini düzenlemek yine.

### <a name="from-an-assembly-dll"></a>Bir derleme DLL

Basit durumda da, bir derlemeden bir paket oluşturma oluşturabileceğiniz bir `.nuspec` aşağıdaki komutu kullanarak derleme içindeki meta veri dosyası:

```cli
nuget spec <assembly-name>.dll
```

Bu formu kullanarak bazı yer tutucuları bildiriminde derlemesinden belirli değerlerle değiştirir. Örneğin, `<id>` özelliği, derleme adı için ayarlanır ve `<version>` derleme sürüme ayarlayın. Diğer özellikleri bildiriminde ancak yoksa eşleşen değerler derlemedeki olmalı ve yine de bu nedenle yer tutucular içermelidir.

### <a name="from-a-visual-studio-project"></a>Visual Studio projesinden

Oluşturma bir `.nuspec` gelen bir `.csproj` veya `.vbproj` dosya, bu projeye yüklü diğer paketleri otomatik bağımlılıkları başvurulduğu için kullanışlıdır. Sadece proje dosyası ile aynı klasörde aşağıdaki komutu kullanın:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Ortaya çıkan `<project-name>.nuspec` dosyasını içeren *belirteçleri* , yerini paketleme zamanında projesinden zaten yüklenmiş olan diğer tüm paketler için başvuruları dahil olmak üzere değerlerle.

Bir belirteç tarafından ayrılmış `$` simgeler iki tarafındaki proje özelliği. Örneğin, `<id>` bu şekilde genellikle oluşturulan bildirim değeri şu şekilde görünür:

```xml
<id>$id$</id>
```

Bu belirteç ile değiştirilir `AssemblyName` zaman paketleme sırasında proje dosyasından değer. Proje değerlerinin tam eşlemesi için `.nuspec` belirteçlerini bkz [değiştirme belirteçleri başvuru](../reference/nuspec.md#replacement-tokens).

Belirteçleri hafifletmek, sürüm numarası gibi önemli değerleri güncelleştirmek gerek `.nuspec` projeyi güncelleştirin. (Her zaman belirteçleri değişmez değer değerlerle isterseniz değiştirebilirsiniz). 

Kullanılabilir olduğundan emin birkaç ek paketleme seçenekleri bir Visual Studio projesinde çalışırken açıklandığı Not [.nupkg dosyası oluşturmak için nuget paketi](#running-nuget-pack-to-generate-the-nupkg-file) daha sonra.

#### <a name="solution-level-packages"></a>Çözüm düzeyinde paketleri

*NuGet 2.x yalnızca. NuGet 3.0 + kullanılamaz.*

NuGet 2.x desteklenen araçlar veya ek komutlar için Paket Yöneticisi konsolu yükleyen bir çözüm düzeyinde paket kavramı (içeriğini `tools` klasör), başvurular, içerik, eklenemiyor veya yapı özelleştirmeleri için herhangi bir projeyi ancak Çözüm. Yok, doğrudan dosyalarında gibi paketlerin içeren `lib`, `content`, veya `build` klasörleri ve bağımlılıklarını hiçbiri sahip kendi ilgili dosyalarında `lib`, `content`, veya `build` klasörleri.

NuGet parçaları çözüm düzeyinde paketleri yüklü bir `packages.config` dosyası `.nuget` projenin yerine klasör `packages.config` dosya.

### <a name="new-file-with-default-values"></a>Varsayılan değerlerle yeni dosya

Aşağıdaki komut varsayılan bildirimi yer tutucularını, uygun dosya yapısı ile Başlat sağlayan oluşturur:

```cli
nuget spec [<package-name>]
```

Atlarsanız \<paket adı\>, sonuçta elde edilen dosya `Package.nuspec`. Gibi bir ad verin, `Contoso.Utility.UsefulStuff`, dosya `Contoso.Utility.UsefulStuff.nuspec`.

Ortaya çıkan `.nuspec` ister değerler için yer tutucular içerir `projectUrl`. En son oluşturmak amacıyla kullanmadan önce dosyayı düzenlemek mutlaka `.nupkg` dosya.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Benzersiz paket tanımlayıcısı seçme ve sürüm numarasını ayarlama

Paket tanımlayıcısı (`<id>` öğesi) ve sürüm numarasını (`<version>` öğesi) pakette yer alan tam kodu, benzersiz şekilde tanımlamak için iki en önemli bildirim değerler.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: tanımlayıcı nuget.org veya hangi galeri paketi barındıran arasında benzersiz olmalıdır. Bir tanımlayıcının karar vermeden önce uygun galeri adı zaten kullanımda olup olmadığını denetlemek için arama yapın. Çakışmaları önlemek için iyi bir desen şirket adınızı tanımlayıcısı ilk parçası olarak gibi kullanmaktır `Contoso.`.
- **Namespace benzeri adları**: .NET, kısa çizgi yerine nokta gösterimi kullanılarak ad alanları için benzer bir desen izleyin. Örneğin, `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`. Paket tanımlayıcısı kod içinde kullanılan ad alanları eşleştiğinde tüketiciler de yararlı.
- **Örnek paketleri**: bir paket nasıl başka bir paket ekleme kullanılacağını gösteren örnek kod üretir, `.Sample` soneki olarak da tanımlayıcı olarak `Contoso.Utility.UsefulStuff.Sample`. (Örnek paketinin Elbette diğer paketi bir bağımlılık yoktur.) Örnek paketi oluştururken, daha önce açıklanan kural tabanlı çalışma dizini yöntemini kullanın. İçinde `content` klasör adında bir klasör örnek kodda düzenleme `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, bu kesinlikle gerekli olmasa da kitaplığı eşleşecek şekilde paketin sürümü ayarlayın. Bir paketi tek bir derleme sınırladığınızda ibarettir daha önce açıklandığı gibi budur [pakete hangi derlemelerin karar](#deciding-which-assemblies-to-package). Genel olarak, kendi NuGet Paket sürümü ile derleme sürümlerini bağımlılıkları çözümlenirken anlaştığından emin unutmayın.
- Standart sürüm şeması kullanırken, NuGet sürüm oluşturma kuralları açıklandığı şekilde dikkate aldığınızdan emin olun [Paket sürümü oluşturma](../reference/package-versioning.md).

> Aşağıdaki bir dizi kısa blog gönderileri da sürüm anlamak yararlıdır:
>
> - [1. Bölüm: Alma DLL cehennemi üzerinde](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [2. Bölüm: Çekirdek algoritması](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3. Bölüm: bağlama yönlendirmeleri aracılığıyla birleştirme](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Ayar paket türü

NuGet ile 3.5 +, paketleri ile belirli bir işaretlenebilir *paket türü* kullanım amacı belirtmek için. NuGet, önceki sürümleriyle oluşturulan tüm paketleri de dahil olmak üzere, bir tür ile işaretlenmemiş paketleri varsayılan `Dependency` türü.

- `Dependency` türü paketler, kitaplıkları ve uygulamaları için derleme veya çalışma zamanı varlıklar eklemek ve (uyumlu olduklarından varsayılarak) herhangi bir proje türü yüklenebilir.

- `DotnetCliTool` tür paketlerin uzantıları [.NET CLI](/dotnet/articles/core/tools/index) ve komut satırından çağrılır. Bu paketler, yalnızca .NET Core projelerinde yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur. Bu proje başına uzantılar hakkında daha fazla ayrıntı kullanılabilir [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgeleri.

- Özel tür paketleri paket kimliği olarak aynı biçimi kurallara uyan bir rastgele tür tanımlayıcısı kullanın. Dışında herhangi türdeki `Dependency` ve `DotnetCliTool`, ancak Visual Studio'da NuGet Paket Yöneticisi tarafından tanınmıyor.

Paket türlerinin ayarlanır `.nuspec` dosya. Geriye dönük için en iyi uyumluluk *değil* açıkça ayarlanmış `Dependency` yazın ve bunun yerine NuGet varsayılarak türü yok, bu tür üzerinde yararlanmayı belirtilir.

- `.nuspec`: Paket türü içinde göstermek bir `packageTypes\packageType` düğümünde `<metadata>` öğesi:

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

## <a name="adding-a-readme-and-other-files"></a>Benioku ve diğer dosyaları ekleme

Pakete dahil edilecek dosyalar doğrudan belirtmek için kullanın `<files>` düğümünde `.nuspec` dosyası, hangi *izleyen* `<metadata>` etiketi:

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
> Çalışma dizini kural tabanlı yaklaşım kullanırken, readme.txt paket kök ve diğer içeriği yerleştirebilirsiniz `content` klasör. Hayır `<file>` bildiriminde öğeler gereklidir.

Adlı bir dosya dahil ettiğinizde `readme.txt` paket kök dizininde, Visual Studio, dosyanın içeriğini düz metin olarak hemen paket doğrudan yüklendikten sonra görüntüler. (Benioku dosyaları bağımlılıkların yüklü paketler için görüntülenmez). Örneğin, işte HtmlAgilityPack paketinin Benioku dosyasını nasıl görünür:

![Yükleme sonrasında bir NuGet paketi için bir benioku dosyası görüntüsü](media/Create_01-ShowReadme.png)

> [!Note]
> Boş bir eklerseniz `<files>` düğümünde `.nuspec` dosya, NuGet içermez herhangi bir içerik paketinde ne olduğunu dışında `lib` klasör.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>MSBuild özellikler ve hedefler bir pakete dahil etme

Bazı durumlarda, derleme sırasında bir özel araç veya işlemin çalıştırma gibi paketinizi kullanan projelerdeki özel yapı hedefleri veya özellikleri eklemek isteyebilirsiniz. Dosya biçiminde yerleştirerek bunu `<package_id>.targets` veya `<package_id>.props` (gibi `Contoso.Utility.UsefulStuff.targets`) içinde `\build` proje klasörü.

Kök dosyaları `\build` için tüm çerçeveleri hedef klasörü uygun değerlendirilir. Çerçeveye özgü dosyaları sağlamak için önce aşağıdaki gibi uygun bir alt kategorilerindekiler yerleştirin:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Ardından `.nuspec` dosya, bu dosyalara başvurmak mutlaka `<files>` düğüm:

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

Bir paket içinde MSBuild özellikler ve hedefler dahil edildi [NuGet 2.5 ile sunulan](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), bu nedenle eklemeniz önerilir `minClientVersion="2.5"` özniteliğini `metadata` öğesi için gereken en düşük NuGet istemci sürümü belirtmek için paketi kullanır.

NuGet paketi ile yüklendiğinde `\build` dosyaları, MSBuild ekler `<Import>` işaret proje dosyasındaki öğeleri `.targets` ve `.props` dosyaları. (`.props` ; proje dosyasının en üstüne eklenir `.targets` altına eklenir.) Ayrı bir koşullu MSBuild `<Import>` öğesi, her hedef çerçeve için eklenir.

MSBuild `.props` ve `.targets` arası framework'ü hedefleyen yerleştirilebilir için dosyaları `\buildCrossTargeting` klasör. Buna karşılık gelen NuGet paketi yüklemesi sırasında ekler `<Import>` öğeleri hedef Framework'ü ayarlı değil koşuluyla, proje dosyasına (MSBuild özelliğini `$(TargetFramework)` boş olmalıdır).

İle NuGet 3.x hedefleri projeye eklenmez ancak bunun yerine kullanılabilir hale getirilir `project.lock.json`.

## <a name="authoring-packages-with-com-interop-assemblies"></a>COM birlikte çalışma derlemelerini paketlerle yazma

COM birlikte çalışma derlemelerini içeren paketleri uygun bir içermelidir [hedefler dosyası](#including-msbuild-props-and-targets-in-a-package) böylece doğru `EmbedInteropTypes` PackageReference biçimini kullanan projeler için meta veriler eklenir. Varsayılan olarak, `EmbedInteropTypes` meta verileri olduğundan her zaman tüm derlemeler için false PackageReference kullanıldığında, bu meta veriler, açıkça hedefler dosyası ekler. Çakışmaları önlemek için hedef adı benzersiz olmalıdır; İdeal olarak, paket adınızla ve katıştırılmış, değiştirilmesini olan derleme birleşimini kullanın `{InteropAssemblyName}` aşağıdaki örnekte bu değere sahip. (Ayrıca bkz: [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Kullanırken dikkat `packages.config` yönetim biçimi paketlerinden derlemelerine başvurular ekleme oluyor NuGet ve Visual Studio için COM birlikte çalışma derlemeleri denetleyin ve ayarlamak `EmbedInteropTypes` proje dosyasındaki true. Bu durumda geçersiz kılınmış hedeflerdir.

Ayrıca, varsayılan olarak [derleme varlıklar akan geçişli](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Geçişli bağımlılık gelen bir projeden projeye başvuru olarak çekildiğinde burada iş farklı bir şekilde açıklandığı yazılan paketler. Paket kullanıcısı PrivateAssets varsayılan değer, derleme içermeyecek şekilde değiştirerek akmasına izin verebilirsiniz.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Nuget paketi .nupkg dosyası oluşturmak için

Bir derleme veya kural tabanlı çalışma dizinini kullanarak, bir paket çalıştırarak oluşturun `nuget pack` ile `.nuspec` değiştirerek, dosya `<project-name>` , belirli bir dosya adına sahip:

```cli
nuget pack <project-name>.nuspec
```

Visual Studio projesi kullanırken çalıştırmak `nuget pack` proje dosyanız ile otomatik olarak yükleyen projenin `.nuspec` dosya ve proje dosyasında değerleri kullanarak içindeki herhangi bir belirteç değiştirir:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Proje dosyasını kullanarak doğrudan proje kaynak belirteci değerler olduğundan belirteç değiştirme için gereklidir. Belirteç değiştirme kullanırsanız testler bulunmuyor `nuget pack` ile bir `.nuspec` dosya.

Tüm durumlarda `nuget pack` gibi bir noktayla başlayan klasörleri dışlar `.git` veya `.hg`.

NuGet, herhangi bir hata olup olmadığını gösteren `.nuspec` bildiriminde yer tutucu değerlerini değiştirmek unutarak gibi düzeltilmesi gereken bir dosya.

Bir kez `nuget pack` başarılı, sahip olduğunuz bir `.nupkg` açıklandığı gibi uygun bir Galeriye yayımlayabilirsiniz dosya [bir paket yayımlama](../create-packages/publish-a-package.md).

> [!Tip]
> Bir paket oluşturma açılır olduktan sonra incelemek için kullanışlı bir yol [paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracı. Bu, paket içeriğini ve bildirimi grafik bir görünümünü sağlar. Ayrıca sonuç yeniden adlandırabilirsiniz `.nupkg` dosyasını bir `.zip` dosya ve doğrudan içeriğini inceleyin.

### <a name="additional-options"></a>Ek Seçenekler

Çeşitli komut satırı anahtarları ile kullanabileceğiniz `nuget pack` dosyaları hariç tutmak, sürüm numarasını bildiriminde geçersiz kılma ve yanı sıra başka özellikler çıkış klasörüne değiştirin. Tam bir listesi için başvurmak [paketi komut başvurusu](../tools/cli-ref-pack.md).

Visual Studio projeleriyle ortak olan birkaç aşağıdaki seçenekler şunlardır:

- **Başvurulan projeler**: projenin diğer projelerden başvuruda bulunuyorsa, başvurulan projeler paketinin bir parçası olarak veya bağımlılıkları ekleyebilirsiniz `-IncludeReferencedProjects` seçeneği:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Bu ekleme işlemi özyinelemelidir dolayısıyla `MyProject.csproj` başvuruları projeleri B ve C ve bu projelerde başvuru D, E ve F, ardından B, C, D, E ve F dosyalarından pakete dahil edilir.

    Başvurulan proje içeriyorsa, bir `.nuspec` dosya, kendi sonra nuget başvurulan proje bunun yerine bir bağımlılık olarak ekler.  Paket ve bu projeyi ayrı ayrı yayımlama gerekir.

- **Derleme Yapılandırması**: varsayılan olarak, NuGet genellikle proje dosyasında ayarlanmış varsayılan derleme yapılandırmasını kullanır. *hata ayıklama*. Farklı bir derleme yapılandırma dosyaları gibi paketlenecek *yayın*, kullanın `-properties` yapılandırma seçeneğiyle:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Semboller**: hata ayıklayıcı paket kodunuzda adım adım tüketicilerin izin simgeleri eklemek için kullanın `-Symbols` seçeneği:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Test paketi yükleme

Bir paket yayımlamadan önce genellikle bir projeye bir paket yükleme işlemini test etmek istediğiniz. Testleri emin mutlaka tüm düştüğünden kendi doğru yerde proje dosyaları.

Yüklemelerini el ile normal kullanarak komut satırında veya Visual Studio'da test edebilirsiniz [paketini yükleme adımlarını](../consume-packages/ways-to-install-a-package.md).

Otomatik test için temel işlemi aşağıdaki gibidir:

1. Kopyalama `.nupkg` dosyasını bir yerel klasöre.
1. Paket kaynaklarınızı kullanarak klasör eklemek `nuget sources add -name <name> -source <path>` komut (bkz [nuget kaynakları](../tools/cli-ref-sources.md)). Yalnızca gereksinim duyduğunuz Not Bu yerel kaynak herhangi belirli bir bilgisayarda bir kez ayarlayın.
1. Bu kaynağı kullanarak paketi yükleyin `nuget install <packageID> -source <name>` burada `<name>` için belirtilen kaynak adıyla eşleşen `nuget sources`. Kaynağını belirterek, bu kaynak paketin yüklendiğini sağlar.
1. Dosyaları düzgün yüklendiğini kontrol etmek için dosya sisteminize inceleyin.

## <a name="next-steps"></a>Sonraki Adımlar

Olan bir paketi oluşturduktan sonra bir `.nupkg` dosyasını yayımlayabilirsiniz, tercih ettiğiniz Galerisine üzerinde açıklandığı [bir paket yayımlama](../create-packages/publish-a-package.md).

Paketiniz yeteneklerini genişletmek veya aksi halde aşağıdaki konularda açıklandığı gibi başka senaryoları destekleyecek isteyebilirsiniz:

- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Kaynak ve yapılandırma dosyalarını dönüşümleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Yayın öncesi sürümleri](../create-packages/prerelease-packages.md)

Son olarak, dikkat edilmesi gereken ek paket türü vardır:

- [Yerel Paketler](../create-packages/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages.md)
