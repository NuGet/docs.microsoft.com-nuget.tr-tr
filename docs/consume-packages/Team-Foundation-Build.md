---
title: Team Foundation Yapısı ile NuGet paket Geri Yükleme Kılavuzu
description: NuGet paket geri yükleme ile Team Foundation Yapısı (TFS ve Visual Studio Team Services) ile nasıl bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549891"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Paket geri yükleme Team Foundation Yapısı ile ayarlama

Bu makalede, paketleri bir parçası olarak geri yükleme konusunda ayrıntılı bir kılavuz sağlar. [Team Services derleme](/vsts/build-release/index) her ikisi için hem Git hem de Team Services sürüm denetimi.

Bu izlenecek yol Visual Studio Team Services kullanarak senaryosu için belirli olsa da, kavramları da diğer sürüm denetimi için geçerlidir ve sistemler oluşturabilir.

Uygulama hedefi:

- TFS herhangi bir sürümünü çalıştıran özel bir MSBuild projeleri
- Team Foundation Server 2012 veya önceki bir sürümü
- TFS 2013 veya sonraki bir sürüme özel Team Foundation Yapı işlem şablonlarını geçişi
- Derleme işlem şablonları ile Nuget geri yükleme işlevi kaldırıldı

Kendi derleme işlem şablonları ile Visual Studio Team Services veya Team Foundation Server 2013 kullanıyorsanız, yapı işleminin bir parçası olarak otomatik paket geri yükleme gerçekleşir.

## <a name="the-general-approach"></a>Genel yaklaşım

NuGet kullanarak bir avantajı, sürüm denetimi Sisteminiz ikili dosyaları iade önlemek için kullanabileceğiniz olmasıdır.

Bu kullanıyorsanız özellikle ilgi çekici bir [dağıtılmış sürüm denetimi](http://en.wikipedia.org/wiki/Distributed_revision_control) geliştiriciler, yerel olarak çalışmaya başlamadan önce tam geçmişini de dahil olmak üzere tüm depoyu kopyalamak gerektiği için git gibi sistem. İkili dosyalar genellikle delta sıkıştırma depolandığından ikili dosyaları denetleniyor önemli depoyu Şişirme neden olabilir.

NuGet desteklenmediği [paketler geri yükleniyor](../consume-packages/package-restore.md) uzun bir süre için derlemenin bir parçası olarak artık zaman. Önceki uygulaması için proje derlenirken NuGet paketleri geri çünkü derleme işlemini genişletme istediğiniz paketlerini tavuk ve Yumurta sorunu yaşıyor. Ancak, MSBuild, derleme yapı sırasında genişletme izin vermez; bir buna bu MSBuild içinde bir sorun, ancak bu devralınan bir sorun olduğunu buna. Genişletmek için gereken hangi yönüyle bağlı olarak, paket geri zaman kaydetmek için çok geç olabilir.

Bu sorunun hastalıktan yapı sürecinin ilk adımı olarak paketleri geri yüklendiğinden emin yapıyor:

```cli
nuget restore path\to\solution.sln
```

Yapı işleminizin, kod oluşturulmadan önce paketleri geri yükler, iade edilmesine gerekmeyen `.targets` dosyaları

> [!Note]
> Visual Studio'da yükleme izin vermek için paketler yeniden yazılması gerekir. Aksi takdirde, yine de iade isteyebileceğiniz `.targets` diğer geliştiriciler çözüm paketleri önce geri yüklemeye gerek kalmadan açabilirler dosyalar.

Aşağıdaki tanıtım proje derleme şekilde ayarlama işlemi gösterilmektedir, `packages` klasörleri ve `.targets` dosyaları iade olması gerekmez. Ayrıca bu örnek project için Team Foundation Service üzerinde otomatik bir yapı ayarlama işlemini de gösterir.

## <a name="repository-structure"></a>Depo yapısı

Tanıtım Projemizin sorgu Bing komut satırı bağımsız değişkeni kullanan bir basit bir komut satırı aracıdır. .NET Framework 4 hedefleyen ve birçok kullanan [BCL paketleri](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), ve [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

Depo yapısı şu şekilde görünür:

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

Şu iade, henüz gördüğünüz `packages` klasörünün veya `.targets` dosyaları.

Biz ancak iade olan `nuget.exe` yapı sırasında gerektiğinde. Aşağıdaki yaygın olarak kullanılan kuralları biz iade, paylaşılan altında `tools` klasör.

Kaynak kodu altındadır `src` klasör. Tanıtımımızı yalnızca tek bir çözüm kullansa da, bu klasör, birden fazla çözüm içeriyor kolayca hayal edebilirsiniz.

### <a name="ignore-files"></a>Dosyaları yoksayma

> [!Note]
> Şu anda bir [NuGet istemci bilinen hata](https://nuget.codeplex.com/workitem/4072) hala eklemek istemci neden `packages` sürüm denetimi klasörü. Kaynak denetimi tümleştirmesi devre dışı bırakmak için bir çözüm olabilir. Bunu yapmak için bir `Nuget.Config ` dosyası `.nuget` çözümünüze paralel klasör. Bu klasörü henüz yoksa, oluşturmanız gerekir. İçinde [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Sürüm denetimi için biz iade için hedefi yok iletişim kurmak için **paketleri** klasörleri ekledik hem git dosyaları yoksay (`.gitignore`) TF sürüm denetimi yanında (`.tfignore`). Bu dosyalar, dosyaların iade edilmesine istemediğiniz desenleri açıklar.

`.gitignore` Dosya şu şekilde görünür:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` Dosyasıdır [oldukça güçlü](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Örneğin, genellikle içeriği iade değil istediğiniz `packages` klasör ancak iade kılavuzun önceki ile gitmek istiyorsanız `.targets` dosyaları sahip olabilir, aşağıdaki kuralı yerine:

    packages
    !packages/**/*.targets

Bu, tüm dışladığı `packages` klasörleri ancak olacak yeniden dahil tüm kapsanan `.targets` dosyaları. Şekilde, bir şablon bulabilirsiniz `.gitignore` ihtiyaçlarını Visual Studio geliştiricileri için özel olarak uyarlanmıştır dosyaları [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

TF sürüm denetimi destekleyen çok benzer bir mekanizma aracılığıyla [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosya. Söz dizimi neredeyse aynıdır:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>Build.proj

Tanıtımımızı için derleme işlemi oldukça basittir saklarız. Paketleri çözüm oluşturmadan önce geri yüklendiğinden emin olmasını sağlarken tüm çözümler oluşturan bir MSBuild Projesi oluşturacağız.

Bu projeyi üç geleneksel hedefleri olur `Clean`, `Build` ve `Rebuild` yeni bir hedef yanı sıra `RestorePackages`.

- `Build` Ve `Rebuild` hem de bağımlı hedefleri `RestorePackages`. Bu, her ikisi de çalıştırabilirsiniz xenapp'i `Build` ve `Rebuild` ve paketleri geri yükleniyor.
- `Clean`, `Build` ve `Rebuild` tüm çözüm dosyalarını karşılık gelen MSBuild hedef çağırır.
- `RestorePackages` Hedefini çağırır `nuget.exe` her çözüm dosyası. Bu kullanılarak başarılır [MSBuild toplu işleme işlevleri](/visualstudio/msbuild/msbuild-batching).

Sonuç şu şekilde görünür:

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

## <a name="configuring-team-build"></a>Takım derlemesi yapılandırma

Takım derlemesi, çeşitli şablonlar sunar. Bu Tanıtım için Team Foundation Service kullanıyoruz. Şirket içi TFS yüklemeleri yine de çok benzer olacaktır.

Aşağıdaki adımlarda kullandığınız hangi sürüm denetimi sistemine bağlı olarak farklılık gösterir farklı ekip şablonları, Git ve TF sürüm denetimi vardır. Her iki durumda da, tüm yapmanız gereken seçmeye build.proj derlemek istediğiniz proje.

İlk olarak, işlem şablonu git için göz atalım. Git tabanlı şablonda yapı özelliği aracılığıyla seçili `Solution to build`:

![Derleme işlemi için git](media/PackageRestoreTeamBuildGit.png)

Lütfen bu özellik bir konumda bir deponuz olduğuna dikkat edin. Bu yana bizim `build.proj` olduğu kök dizininde yalnızca kullandığımız `build.proj`. Derleme dosyası adlı bir klasör yerleştirmek, `tools`, değer `tools\build.proj`.

TF sürüm denetimi şablonunda özelliği aracılığıyla proje seçilen `Projects`:

![TFVC için derleme işlemi](media/PackageRestoreTeamBuildTFVC.png)

Git tabanlı şablon aksine TF sürüm denetimi seçiciler (sağ taraftaki üç noktalı düğme) destekler. Bu nedenle herhangi bir yazım hatalarını önlemek için bunları projeyi seçmek için kullandığınız öneririz.
