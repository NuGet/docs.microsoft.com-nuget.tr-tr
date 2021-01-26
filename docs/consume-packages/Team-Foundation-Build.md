---
title: Team Foundation derlemesi ile NuGet paketi geri yükleme kılavuzu
description: NuGet paketinin Team Foundation Build (TFS ve Visual Studio Team Services) ile birlikte nasıl geri yükleneceğini gösteren bir yol.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 8b993106d439dc137fbe040b51fda373539de81a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774989"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Team Foundation derlemesi ile paket geri yüklemeyi ayarlama

Bu makalede, hem git hem de Team Services sürüm denetimi için [Team Services derlemesinin](/vsts/build-release/index) bir parçası olarak paketlerin nasıl geri yükleneceği hakkında ayrıntılı bir yol sunulmaktadır.

Bu izlenecek yol Visual Studio Team Services kullanma senaryosuna özgü olsa da, kavramlar diğer sürüm denetimi ve yapı sistemleri için de geçerlidir.

Şunun için geçerlidir:

- TFS 'nin herhangi bir sürümünde çalışan özel MSBuild projeleri
- Team Foundation Server 2012 veya öncesi
- TFS 2013 veya sonraki bir sürüme geçirilen özel Team Foundation derleme Işlemi şablonları
- NuGet geri yükleme işlevselliği kaldırılmış şekilde Işlem şablonları oluşturun

Yapı işlemi şablonlarıyla Visual Studio Team Services veya Team Foundation Server 2013 kullanıyorsanız, derleme işleminin bir parçası olarak otomatik paket geri yüklemesi gerçekleşir.

## <a name="the-general-approach"></a>Genel yaklaşım

NuGet kullanmanın bir avantajı, bunu, sürüm denetim sisteminize ikili dosyaları iade etmekten kaçınmak için kullanabilirsiniz.

Bu özellikle, git gibi [Dağıtılmış bir sürüm denetimi](https://en.wikipedia.org/wiki/Distributed_revision_control) sistemi kullanıyorsanız, geliştiricilerin yerel olarak çalışmaya başlayabilmeleri için tam geçmiş dahil olmak üzere tüm depoyu kopyalaması gerektiğinden çok ilginç olur. İkili dosyalar genellikle değişim sıkıştırması olmadan depolandığından, ikili dosyaların iade edilirken önemli depo blobunun oluşmasına neden olabilir.

NuGet, yapılandırmanın bir parçası olarak uzun süredir [geri yüklemeyi](../consume-packages/package-restore.md) destekliyordu. Önceki uygulamada, derleme işlemini genişletmek isteyen paketlere yönelik bir tavuk-yumurg sorunu vardı, çünkü projeyi oluştururken NuGet geri yüklendi paketleri. Ancak, MSBuild derleme sırasında derlemeyi genişletmeye izin vermez; Bunlardan biri MSBuild 'deki bir sorun olduğunu, ancak bunun devralınmış bir sorun olduğunu anlıyorum. Genişletmeniz gereken en boy düzeyine bağlı olarak, paketinizin geri yüklendiği zamana göre kaydolmak için çok geç olabilir.

Bu sorunu çözmek, paketlerin derleme işlemindeki ilk adım olarak geri yüklendiğinden emin olmanızı sağlar:

```cli
nuget restore path\to\solution.sln
```

Yapı işleminiz kodu oluşturmadan önce paketleri geri yüklediğinde, dosyaları iade etmeniz gerekmez `.targets`

> [!Note]
> Visual Studio 'da yüklemeye izin vermek için paketlerin yazılması gerekir. Aksi takdirde, `.targets` diğer geliştiricilerin önce paketleri geri yüklemek zorunda kalmadan çözümü açabilmeleri için dosyaları iade etmek isteyebilirsiniz.

Aşağıdaki demo projesi, bir derlemeyi `packages` klasörlerin ve dosyaların iade etme gereksinimi olacak şekilde ayarlamayı gösterir `.targets` . Ayrıca, bu örnek proje için Team Foundation Service otomatik bir derlemeyi ayarlamayı gösterir.

## <a name="repository-structure"></a>Depo yapısı

Tanıtım projemiz, Bing sorgulamak için komut satırı bağımsız değişkenini kullanan basit bir komut satırı aracıdır. .NET Framework 4 ' ü hedefler ve birçok [BCL paketini](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.net. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)ve [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) kullanır.

Deponun yapısı şöyle görünür:

```
<Project>
    │   .gitignore
    │   .tfignore
    │   build.proj
    │
    ├───src
    │   │   BingSearcher.sln
    │   │
    │   └───BingSearcher
    │       │   App.config
    │       │   BingSearcher.csproj
    │       │   packages.config
    │       │   Program.cs
    │       │
    │       └───Properties
    │               AssemblyInfo.cs
    │
    └───tools
        └───NuGet
                nuget.exe
```

`packages`Klasörü veya herhangi bir dosyayı iade etmediğimiz hakkında bilgi alabilirsiniz `.targets` .

Ancak, `nuget.exe` derleme sırasında gerekli olduğu gibi iade ettik. Yaygın olarak kullanılan kuralları paylaşılan bir klasör altında denetliyoruz `tools` .

Kaynak kodu `src` klasörün altındadır. Tanıtımız yalnızca tek bir çözüm kullandığından, bu klasörün birden fazla çözüm içerdiğini kolayca hayal edebilirsiniz.

### <a name="ignore-files"></a>Dosyaları yoksayma

> [!Note]
> [NuGet istemcisinde](https://nuget.codeplex.com/workitem/4072) , istemcinin hala sürüm denetimine klasör eklemesine neden olan bilinen bir hata var `packages` . Kaynak denetimi tümleştirmesini devre dışı bırakmak geçici bir çözümdür. Bunu yapmak için `Nuget.Config `  `.nuget` çözümünüze paralel olan klasörde bir dosyaya ihtiyacınız vardır. Bu klasör henüz yoksa, oluşturmanız gerekir. İçinde [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) , aşağıdaki içeriği ekleyin:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

**Paket** klasörlerinde iade etme amacını verdiğimiz Sürüm denetimiyle iletişim kurmak için, hem git () hem de `.gitignore` tf sürüm denetimi () için de Ignore dosyaları ekledik `.tfignore` . Bu dosyalar iade etmek istemediğiniz dosyaların desenlerini anlatmaktadır.

`.gitignore`Dosya aşağıdaki gibi görünür:

```
syntax: glob
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

`.gitignore`Dosya [oldukça güçlüdür](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Örneğin, genellikle klasörün içeriğini iade etmek, `packages` ancak dosyaları iade etme hakkında daha önceki kılavuza gitmek istiyorsanız `.targets` bunun yerine aşağıdaki kurala sahip olabilirsiniz:

```
packages
!packages/**/*.targets
```

Bu, tüm klasörleri hariç tutar, `packages` ancak içerilen tüm dosyaları yeniden içerecektir `.targets` . Bu şekilde, `.gitignore` [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio geliştiricilerinin ihtiyaçlarını karşılamak için özel olarak uyarlanmış dosyalar için bir şablon bulabilirsiniz.

TF Version Control, [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosyası aracılığıyla çok benzer bir mekanizmayı destekler. Sözdizimi neredeyse aynıdır:

```
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

## <a name="buildproj"></a>Build. proj

Tanıtımızın için yapı sürecini oldukça basit tutuyoruz. Çözümleri oluşturmadan önce paketlerin geri yüklendiğinden emin olmak için tüm çözümleri oluşturan bir MSBuild projesi oluşturacağız.

Bu proje, üç geleneksel hedefe `Clean` `Build` ve `Rebuild` Ayrıca yeni bir hedefe sahip olacaktır `RestorePackages` .

- `Build`Ve `Rebuild` hedefleri her ikisi de bağımlıdır `RestorePackages` . Bu, hem çalıştırıp hem de `Build` `Rebuild` Geri yüklenmekte olan paketleri temel almanızı sağlar.
- `Clean``Build`ve `Rebuild` tüm çözüm dosyalarında karşılık gelen MSBuild hedefini çağırır.
- `RestorePackages`Hedef `nuget.exe` her çözüm dosyası için çağırır. Bu, [MSBuild 'in toplu işlem işlevselliği](/visualstudio/msbuild/msbuild-batching)kullanılarak gerçekleştirilir.

Sonuç şöyle görünür:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Takım derlemesini yapılandırma

Ekip derlemesi çeşitli işlem şablonları sunmaktadır. Bu gösterim için Team Foundation Service kullanırız. TFS 'nin şirket içi yüklemeleri çok benzer olacaktır.

Git ve TF sürüm denetimi farklı takım derleme şablonlarına sahiptir, bu nedenle, kullanmakta olduğunuz sürüm denetim sistemine bağlı olarak aşağıdaki adımlar değişiklik gösterecektir. Her iki durumda da tüm ihtiyacınız olan Build. proj ' i derlemek istediğiniz proje olarak seçmektir.

İlk olarak, git için işlem şablonuna göz atalım. Git tabanlı şablonda, yapı özelliği aracılığıyla seçilir `Solution to build` :

![Git için derleme Işlemi](media/PackageRestoreTeamBuildGit.png)

Bu özelliğin deponuzdaki bir konum olduğunu lütfen unutmayın. Bizim `build.proj` kökte olduğundan, yalnızca kullandık `build.proj` . Yapı dosyasını adlı bir klasöre yerleştirirseniz `tools` değer şöyle olur `tools\build.proj` .

TF sürüm denetimi şablonunda, proje özelliği aracılığıyla seçilir `Projects` :

![TFVC için derleme Işlemi](media/PackageRestoreTeamBuildTFVC.png)

Git tabanlı şablonun aksine, TF sürüm denetimi, etiketleri destekler (üç nokta ile sağ taraftaki düğme). Bu nedenle, herhangi bir yazma hatasını önlemek için, projeyi seçmek üzere bunları kullanmanızı öneririz.
