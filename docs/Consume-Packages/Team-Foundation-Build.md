---
title: "İzlenecek yol NuGet paketinin geri yükleme ile Team Foundation derlemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3113cccd-35f7-4980-8a6e-fc06556b5064
description: "Nasıl NuGet paket geri yükleme işlemi ile Team Foundation Build (TFS ve Visual Studio Team Services) ile bir gözden geçirme."
keywords: "NuGet paket geri yüklemesi, NuGet ve TFS, NuGet ve VSTS, NuGet yapı sistemleri, team foundation derlemesi, özel MSBuild projelerine bulut yapı, sürekli tümleştirme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4be1bb83549958897a15d690439cac073c9683d1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Paket geri yüklemesi Team Foundation Build ile ayarlama

> Uygulandığı öğe:
>  - Herhangi bir TFS sürümü özel MSBuild projelerine
>  - Team Foundation Server 2012 veya önceki
>  - TFS 2013 veya sonraki bir sürüme özel Team Foundation Yapı işlem şablonları geçişi
>  - İşlem şablonları kaldırılan Nuget geri yükleme işlevselliği ile derleme
>
> Alt yapı işlem şablonları ile Visual Studio Team Services veya şirket içi Team Foundation Server 2013 kullanıyorsanız, otomatik paket geri yükleme yapılandırma işleminin bir parçası olarak gerçekleşir.

Bu bölümde paketleri parçası olarak geri yükleme konusunda ayrıntılı bilgi sağlayacaktır [Team Foundation Build](http://msdn.microsoft.com/library/ms181710(v=VS.90).aspx) her ikisi için [git](http://en.wikipedia.org/wiki/Git_(software)) yanı [TF sürüm denetimi](http://msdn.microsoft.com/library/ms181237(v=vs.120).aspx).

Bu kılavuzu kullanarak bu senaryo için belirli olmasına rağmen [Team Foundation Service](http://tfs.visualstudio.com/), kavramları ayrıca diğer sürüm denetimi için uygulama ve sistemler oluşturabilir.

## <a name="the-general-approach"></a>Genel yaklaşım

NuGet kullanarak bir avantajı, onu ikili dosyalarının sürüm denetim sisteminiz için iade önlemek için kullanabileceğiniz olmasıdır.

Bu kullanıyorsanız özellikle ilginç bir [dağıtılmış sürüm denetim](http://en.wikipedia.org/wiki/Distributed_revision_control) geliştiriciler, yerel olarak çalışmaya başlamadan önce tam geçmişi dahil olmak üzere tüm depoyu kopyalayın gerektiğinden git gibi sistem. İkili dosyalar genellikle delta sıkıştırma kaydedildikçe ikili dosyalarda denetimi önemli deposu oluşan şişirmeyi neden olabilir.

NuGet desteklenen [paketleri geri](../consume-packages/package-restore.md) derleme için uzun bir parçası olarak şimdi saat. Önceki uygulaması proje oluşturulurken NuGet paketleri geri çünkü derleme işlemini genişletme istediğiniz paketler için tavuk ve Yumurta sorunu yaşıyor. Ancak, MSBuild yapı oluşturma sırasında genişletme izin vermez; bir karşıdır bu MSBuild bir sorunu ancak bu devralınan bir sorun olduğunu savunabilir. Genişletmek için gereken hangi en boy bağlı olarak, paketi geri yüklemesi zamanına göre kaydetmek için çok geç olabilir.

Bu sorunun kurut paketler derleme işlemindeki ilk adım olarak geri emin yapılmasıdır. NuGet 2.7 + bu basitleştirilmiş bir komut satırı kolaylaştırır:

```
nuget restore path\to\solution.sln
```

Derleme sürecinde kod oluşturmadan önce paketleri yüklediğinde, iade gerekmez `.targets` dosyaları

> [!Note]
> Paketleri yükleme Visual Studio'da izin vermek için yazılmış olmalıdır. Aksi takdirde, hala iade isteyebilirsiniz `.targets` diğer geliştiriciler çözüm paketlerini ilk geri yüklemek zorunda kalmadan açabilirler böylece dosyaları.

Aşağıdaki gösterim proje derleme şekilde ayarlamak gösterilmektedir, `packages` klasörleri ve `.targets` dosyaları iade edildi olması gerekmez. Ayrıca, bu örnek proje için Team Foundation Service üzerinde otomatik bir yapı ayarlamak nasıl gösterir.

## <a name="repository-structure"></a>Depo yapısı

Tanıtım Projemizin sorgu Bing komut satırı bağımsız değişkeni kullanan bir basit komut satırı aracıdır. .NET Framework 4 hedefler ve birçok kullanan [BCL paketleri](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), ve [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

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

Biz iade edildi, henüz gördüğünüz `packages` ya da herhangi bir klasör `.targets` dosyaları.

Biz ancak iade edildi olan `nuget.exe` derleme sırasında gerektiğinde. Aşağıdaki yaygın olarak kullanılan biz iade, paylaşılan altında kuralları `tools` klasör.

Kaynak kodu altındadır `src` klasör. Kendi Tanıtımı yalnızca tek bir çözüm kullansa da, bu klasör, birden fazla çözüm içeriyor kolayca düşünebilirsiniz.

### <a name="ignore-files"></a>Dosyaları yoksay

> [!Note]
> Var. şu anda bir [NuGet istemci bilinen hata](https://nuget.codeplex.com/workitem/4072) hala eklemek istemci neden `packages` sürüm denetimi klasörüne. Kaynak denetimi tümleştirmesi devre dışı bırakmak için bir çözüm olabilir. Bunu yapmak için gerekir bir `Nuget.Config ` dosyasını `.nuget` çözümünüze paralel klasör. Bu klasör henüz mevcut değilse, bunu oluşturmanız gerekir. İçinde [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```


Sürüm denetimi biz giriş yapma yok iletişim kurmak için **paketleri** klasörleri ayrıca eklediğimiz yoksaymak için her iki git dosyaları (`.gitignore`) TF sürüm denetimi yanı sıra (`.tfignore`). Bu dosyaları iade istemediğiniz dosyaların desenleri açıklar.

`.gitignore` Dosya şu şekilde görünür:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

`.gitignore` Dosyası [oldukça güçlü](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Örneğin, genellikle içeriğini iade değil istiyorsanız `packages` klasör ancak denetleme önceki yönlendirme ile gitmek istiyorsanız `.targets` sahip olabilir, aşağıdaki dosyaları kural bunun yerine:

    packages
    !packages/**/*.targets

Bu tüm dışlayacak `packages` klasörleri ancak olacak yeniden dahil tüm kapsanan `.targets` dosyaları. İçin bir şablon isteyenlerin bulabilirsiniz `.gitignore` Visual Studio geliştiriciler ihtiyaçlarını için özellikle tasarlanmış dosyaları [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

TF sürüm denetimi destekleyen çok benzer bir mekanizma aracılığıyla [.tfignore](http://msdn.microsoft.com/library/ms245454.aspx) dosya. Neredeyse aynı söz dizimi:

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a>Build.proj

Kendi tanıtımı için biz oluşturma işlemi oldukça basit tutun. Çözümler oluşturulmadan önce paketleri geri yüklendiğini emin olmasını sağlarken tüm çözümler oluşturan MSBuild Projesi oluşturacağız.

Bu proje üç geleneksel hedefleri olacaktır `Clean`, `Build` ve `Rebuild` yeni bir hedef yanı sıra `RestorePackages`.

- `Build` Ve `Rebuild` her ikisi de bağlıdır hedefleri `RestorePackages`. Bu, her ikisi de çalıştırabilirsiniz emin olur `Build` ve `Rebuild` ve paketleri geri yükleniyor.
- `Clean`, `Build` ve `Rebuild` tüm çözüm dosyalarını karşılık gelen MSBuild hedef çağırma.
- `RestorePackages` Hedef çağırır `nuget.exe` her çözüm dosyası. Bu kullanarak gerçekleştirilir [toplu işleme MSBuild işlevselliği](http://msdn.microsoft.com/library/ms171473.aspx).

Sonucu şu şekilde görünür:

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

## <a name="configuring-team-build"></a>Takım yapı yapılandırma

Ekip derlemesi çeşitli şablonlar sunar. Bu Tanıtım için biz Team Foundation Service kullanıyorsunuz. TFS şirket içi yüklemeleri yine de çok benzer.

Aşağıdaki adımlarda kullandığınız hangi sürüm denetimi sistemi bağlı olarak farklılık gösterir Git ve TF sürüm denetimi ekip farklı şablonlar vardır. Her iki durumda da, tek ihtiyacınız seçerek build.proj oluşturmak istediğiniz projesi olarak.

İlk olarak, git için işlem şablonu bakalım. Temel git şablonda yapı özelliği aracılığıyla seçilir `Solution to build`:

![Derleme işlemi için git](media/PackageRestoreTeamBuildGit.png)

Bu özellik deponuzun bir konum olduğunu unutmayın. Bu yana bizim `build.proj` olduğu kök dizininde yalnızca kullandık `build.proj`. Adlı bir klasör altında derleme dosyasını yerleştirin, `tools`, değer olacaktır `tools\build.proj`.

TF sürüm denetimi Şablonu proje özelliği aracılığıyla seçilen `Projects`:

![TFVC'yi için derleme işlemi](media/PackageRestoreTeamBuildTFVC.png)

Temel git şablonu TF aksine, sürüm denetimi seçiciler (sağ taraftaki üç noktalı düğmeyi) destekler. Bu nedenle yazım hatalarını önlemek için bunları projeyi seçmek için kullandığınız öneririz.