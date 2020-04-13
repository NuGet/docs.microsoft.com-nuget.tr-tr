---
title: Team Foundation Build ile NuGet Paketi Geri Yükleme'nin Walkthrough'u
description: Team Foundation Build (Hem TFS hem de Visual Studio Team Services) ile NuGet paketinin nasıl geri yüklenirolduğunun bir walkthrough'u.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610996"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Team Foundation Build ile paket geri yüklemesi ayarlama

Bu makalede, hem Git hem de Takım Hizmetleri Sürüm Denetimi [için, Her](/vsts/build-release/index) ikisi de Ekip Hizmetleri Yapısı'nın bir parçası olarak paketlerin nasıl geri yükleneneceklerine ilişkin ayrıntılı bir gözden geçirme sağlar.

Bu izbis Visual Studio Team Services'ı kullanma senaryosu için özel olsa da, kavramlar diğer sürüm denetimi ve yapı sistemleri için de geçerlidir.

Şunun için geçerlidir:

- TFS'nin herhangi bir sürümünde çalışan özel MSBuild projeleri
- Team Foundation Server 2012 veya önceki
- TFS 2013 veya sonraki bir süre sonra geçirilen Özel Takım Temel Oluşturma İşlemşablonları
- Nuget Geri Yükleme işlevi kaldırılmış olan İşlem Şablonları Oluşturma

Visual Studio Team Services veya Team Foundation Server 2013'ü yapı işlem şablonlarıyla kullanıyorsanız, otomatik paket geri yüklemesi yapı sürecinin bir parçası olarak gerçekleşir.

## <a name="the-general-approach"></a>Genel yaklaşım

NuGet kullanmanın bir avantajı, sürüm kontrol sisteminize ikili olarak giriş yapmaktan kaçınmak için bunu kullanabilirsiniz.

Geliştiriciler yerel olarak çalışmaya başlamadan önce, tam geçmişi de dahil olmak üzere tüm depo klonlamak gerekir, çünkü git gibi [dağıtılmış](https://en.wikipedia.org/wiki/Distributed_revision_control) bir sürüm kontrol sistemi kullanıyorsanız bu özellikle ilginç. İkili dosyaların genellikle delta sıkıştırma olmadan depolanır gibi ikili olarak kontrol önemli depo şişkinlik neden olabilir.

NuGet, uzun zamandır yapının bir parçası olarak [paketleri geri almayı](../consume-packages/package-restore.md) desteklemiştir. NuGet projeyi oluştururken paketleri geri yüklediği için, önceki uygulamada yapı işlemini uzatmak isteyen paketler için tavuk ve yumurta sorunu vardı. Ancak, MSBuild yapı sırasında yapı genişletilmesine izin vermez; bir MSBuild bu bir sorun olduğunu iddia edebilir ama bu doğal bir sorun olduğunu iddia ediyorum. Hangi yönü genişletmeniz gerektiğine bağlı olarak, paketiniz geri yüklenene kadar kaydolmak için çok geç olabilir.

Bu sorunun çözümü, paketlerin yapı işleminin ilk adımı olarak geri yüklenmesidir:

```cli
nuget restore path\to\solution.sln
```

Yapı işleminiz kodu oluşturmadan önce paketleri geri yüklediğinde, `.targets` iade dosyalarına gerek yoktur

> [!Note]
> Paketler Visual Studio'da yüklemeye izin verecek şekilde yazılmalıdır. Aksi takdirde, diğer geliştiricilerin `.targets` önce paketleri geri yüklemek zorunda kalmadan çözümü açabilmeleri için dosyaları iade etmek isteyebilirsiniz.

Aşağıdaki demo projesi, `packages` klasörlerin ve `.targets` dosyaların iade edilmesine gerek olmayacak şekilde yapının nasıl ayarlanış edilebildiğini gösterir. Ayrıca, bu örnek proje için Team Foundation Service üzerinde otomatik bir yapının nasıl kurulabildiğini de gösterir.

## <a name="repository-structure"></a>Depo yapısı

Demo projemiz, Bing'i sorgulamak için komut satırı bağımsız değişkenini kullanan basit bir komut satırı aracıdır. Bu .NET Framework 4 hedefleri ve [BCL paketleri](https://www.nuget.org/profiles/dotnetframework/) [(Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)ve [Microsoft.Bcl.Build)](https://www.nuget.org/packages/Microsoft.Bcl.Build)birçok kullanır.

Deponun yapısı aşağıdaki gibi görünür:

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

Klasöre veya herhangi bir `packages` `.targets` dosyaya giriş yapmadığımızı görebilirsiniz.

Ancak, inşa sırasında ihtiyaç duyulan `nuget.exe` şekilde check-in yaptık. Yaygın olarak kullanılan kuralları takiben, paylaşılan `tools` bir klasöraltında kontrol ettik.

Kaynak kodu klasörün `src` altındadır. Demomuz yalnızca tek bir çözüm kullansa da, bu klasörün birden fazla çözüm içerdiğini kolayca hayal edebilirsiniz.

### <a name="ignore-files"></a>Dosyaları yoksayma

> [!Note]
> Şu anda [NuGet istemcisinde istemcinin](https://nuget.codeplex.com/workitem/4072) klasörü `packages` sürüm denetimine eklemesine neden olan bilinen bir hata vardır. Geçici çözüm, kaynak denetim tümleştirmesini devre dışı betmektir. Bunu yapmak için, `Nuget.Config ` `.nuget` klasörde çözümünüze paralel bir dosya gerekir. Bu klasör henüz yoksa, klasörü oluşturmanız gerekir. In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

**Paket** klasörlerini iade etme niyetimiz olmadığını sürüm denetimine iletmek için, hem git (`.gitignore`) hem de TF sürüm`.tfignore`denetimi ( ) için yoksay dosyaları ekledik. Bu dosyalar, iade etmek istemediğiniz dosyaların modellerini açıklar.

Dosya `.gitignore` aşağıdaki gibi görünür:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

Dosya `.gitignore` [oldukça güçlü.](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) Örneğin, genellikle `packages` klasörün içeriğini iade etmek istemiyorsanız ancak `.targets` dosyaları iade etme kılavuzunu önceki kılavuzla gitmek istiyorsanız, bunun yerine aşağıdaki kurala sahip olabilirsiniz:

    packages
    !packages/**/*.targets

Bu, tüm `packages` klasörleri hariç tutar, `.targets` ancak içerdiği tüm dosyaları yeniden içerir. Bu arada, [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio `.gitignore` geliştiricilerin ihtiyaçlarına özel olarak uyarlanmış dosyalar için bir şablon bulabilirsiniz.

TF sürüm denetimi [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosyası üzerinden çok benzer bir mekanizmayı destekler. Sözdizimi hemen hemen aynıdır:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

Demomuz için, yapı işlemini oldukça basit tutuyoruz. Çözümleri oluşturmadan önce paketlerin geri yüklenirken tüm çözümleri oluşturan bir MSBuild projesi oluşturacağız.

Bu proje üç konvansiyonel `Clean`hedefleri `Build` `Rebuild` olacak, hem de `RestorePackages`yeni bir hedef .

- Hem hedefler hem de bağlıdır. `RestorePackages` `Build` `Rebuild` Bu, hem çalıştırabileceğinizi `Build` `Rebuild` hem de geri yüklenen paketlere güvenmenizi sağlar.
- `Clean`ve `Build` `Rebuild` tüm çözüm dosyalarında karşılık gelen MSBuild hedefini çağırın.
- Hedef `RestorePackages` her `nuget.exe` çözüm dosyası için çağırır. Bu, [MSBuild'in toplu işişlevini](/visualstudio/msbuild/msbuild-batching)kullanarak gerçekleştirilir.

Sonuç aşağıdaki gibi görünür:

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

## <a name="configuring-team-build"></a>Takım Oluşturmayı Yapılandırma

Team Build çeşitli işlem şablonları sunar. Bu gösteri için, Takım Hazırlık Servisi'ni kullanıyoruz. TFS'nin şirket içi kurulumları çok benzer olacaktır.

Git ve TF Sürüm Denetimi farklı Takım Oluşturma şablonlarına sahiptir, bu nedenle aşağıdaki adımlar kullandığınız sürüm kontrol sistemine bağlı olarak değişir. Her iki durumda da, tek ihtiyacınız oluşturmak istediğiniz proje olarak build.proj seçmektir.

İlk olarak, git için işlem şablonuna bakalım. Git tabanlı şablonda yapı özelliği `Solution to build`üzerinden seçilir:

![Git için Yapı Süreci](media/PackageRestoreTeamBuildGit.png)

Bu tesisin deponuzdaki bir yer olduğunu lütfen unutmayın. Bizim `build.proj` kök olduğu için, biz `build.proj`sadece kullanılır . Yapı dosyasını adlı `tools`bir klasörün altına yerlesanız, değer . `tools\build.proj`

TF sürüm kontrol şablonunda proje özellik `Projects`üzerinden seçilir:

![TFVC için Yapı Süreci](media/PackageRestoreTeamBuildTFVC.png)

Git tabanlı şablonun aksine TF sürüm denetimi toplayıcıları destekler (sağ taraftaki düğme üç noktayla birlikte). Bu nedenle yazım hatalarından kaçınmak için projeyi seçmek için bunları kullanmanızı öneririz.
