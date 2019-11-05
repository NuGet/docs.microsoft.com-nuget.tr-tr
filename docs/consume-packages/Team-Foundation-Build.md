---
title: Team Foundation derlemesi ile NuGet paketi geri yükleme kılavuzu
description: NuGet paketinin Team Foundation Build (TFS ve Visual Studio Team Services) ile birlikte nasıl geri yükleneceğini gösteren bir yol.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610996"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Team Foundation derlemesi ile paket geri yüklemeyi ayarlama

Bu makalede, hem git hem de Team Services sürüm denetimi için [Team Services derlemesinin](/vsts/build-release/index) bir parçası olarak paketlerin nasıl geri yükleneceği hakkında ayrıntılı bir yol sunulmaktadır.

Bu izlenecek yol Visual Studio Team Services kullanma senaryosuna özgü olsa da, kavramlar diğer sürüm denetimi ve yapı sistemleri için de geçerlidir.

Uygulama hedefi:

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

Yapı işleminiz kodu oluşturmadan önce paketleri geri yüklediğinde, `.targets` dosyaları iade etmeniz gerekmez

> [!Note]
> Visual Studio 'da yüklemeye izin vermek için paketlerin yazılması gerekir. Aksi takdirde, diğer geliştiricilerin önce paketleri geri yüklemek zorunda kalmadan çözümü açabilmeleri için `.targets` dosyaları iade etmek isteyebilirsiniz.

Aşağıdaki demo projesi, `packages` klasörlerinin ve `.targets` dosyalarının iade alınması gerekmeyen şekilde derlemeyi nasıl ayarlayagösterdiğini gösterir. Ayrıca, bu örnek proje için Team Foundation Service otomatik bir derlemeyi ayarlamayı gösterir.

## <a name="repository-structure"></a>Depo yapısı

Tanıtım projemiz, Bing sorgulamak için komut satırı bağımsız değişkenini kullanan basit bir komut satırı aracıdır. .NET Framework 4 ' ü hedefler ve birçok [BCL paketini](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.net. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)ve [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) kullanır.

Deponun yapısı şöyle görünür:

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

`packages` klasörünü veya `.targets` dosyalarını iade etmediğimiz hakkında bilgi alabilirsiniz.

Ancak, derleme sırasında gerekli olduğu gibi `nuget.exe` iade ettik. Yaygın olarak kullanılan kuralları paylaşılan bir `tools` klasörü altında denetliyoruz.

Kaynak kodu `src` klasörünün altındadır. Tanıtımız yalnızca tek bir çözüm kullandığından, bu klasörün birden fazla çözüm içerdiğini kolayca hayal edebilirsiniz.

### <a name="ignore-files"></a>Dosyaları yoksayma

> [!Note]
> [NuGet istemcisinde](https://nuget.codeplex.com/workitem/4072) , istemcinin hala `packages` klasörünü sürüm denetimine eklemesine neden olan bilinen bir hata var. Kaynak denetimi tümleştirmesini devre dışı bırakmak geçici bir çözümdür. Bunu yapmak için çözümünüze paralel `.nuget` klasöründe bir `Nuget.Config ` dosyası gerekir. Bu klasör henüz yoksa, oluşturmanız gerekir. [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

**Paket** klasörlerinde iade etme amacını verdiğimiz Sürüm denetimiyle iletişim kurmak için hem git (`.gitignore`) hem de TF sürüm denetimi (`.tfignore`) için de Ignore dosyalarını ekledik. Bu dosyalar iade etmek istemediğiniz dosyaların desenlerini anlatmaktadır.

`.gitignore` dosya aşağıdaki gibi görünür:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` dosya [oldukça güçlüdür](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Örneğin, `packages` klasörünün içeriğini iade etmek, ancak `.targets` dosyaları iade etme hakkında önceki kılavuza gitmek istiyorsanız bunun yerine aşağıdaki kurala sahip olabilirsiniz:

    packages
    !packages/**/*.targets

Bu, tüm `packages` klasörlerini dışlayacak, ancak içerilen tüm `.targets` dosyalarını yeniden ekleyecek. Bu şekilde, [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio geliştiricilerinin ihtiyaçlarını karşılamak için özel olarak uyarlanmış `.gitignore` dosyaları için bir şablon bulabilirsiniz.

TF Version Control, [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosyası aracılığıyla çok benzer bir mekanizmayı destekler. Sözdizimi neredeyse aynıdır:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>Build. proj

Tanıtımızın için yapı sürecini oldukça basit tutuyoruz. Çözümleri oluşturmadan önce paketlerin geri yüklendiğinden emin olmak için tüm çözümleri oluşturan bir MSBuild projesi oluşturacağız.

Bu proje üç geleneksel hedefe `Clean`, `Build` ve `Rebuild` yanı sıra yeni bir hedef `RestorePackages`sahip olacaktır.

- `Build` ve `Rebuild` hedeflerin ikisi de `RestorePackages`bağımlıdır. Bu, hem `Build` hem de `Rebuild` çalıştırabildiğinden ve geri yüklenen paketlere güvendiğinizden emin olmanızı sağlar.
- `Clean`, `Build` ve `Rebuild` tüm çözüm dosyalarında karşılık gelen MSBuild hedefini çağırır.
- `RestorePackages` hedefi her çözüm dosyası için `nuget.exe` çağırır. Bu, [MSBuild 'in toplu işlem işlevselliği](/visualstudio/msbuild/msbuild-batching)kullanılarak gerçekleştirilir.

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

İlk olarak, git için işlem şablonuna göz atalım. Git tabanlı şablonda, derleme `Solution to build`özellik ile seçilir:

![Git için derleme Işlemi](media/PackageRestoreTeamBuildGit.png)

Bu özelliğin deponuzdaki bir konum olduğunu lütfen unutmayın. `build.proj` kökte olduğundan, `build.proj`yalnızca kullandık. Yapı dosyasını `tools`adlı bir klasöre yerleştirirseniz, değer `tools\build.proj`olur.

TF sürüm denetimi şablonunda proje, özellik `Projects`seçilir:

![TFVC için derleme Işlemi](media/PackageRestoreTeamBuildTFVC.png)

Git tabanlı şablonun aksine, TF sürüm denetimi, etiketleri destekler (üç nokta ile sağ taraftaki düğme). Bu nedenle, herhangi bir yazma hatasını önlemek için, projeyi seçmek üzere bunları kullanmanızı öneririz.
