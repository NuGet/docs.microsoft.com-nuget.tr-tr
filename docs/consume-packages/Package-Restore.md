---
title: NuGet paketini geri yükleme
description: NuGet 'in bir proje tarafından nasıl geri yükleneceği hakkında genel bakış, geri yüklemeyi devre dışı bırakma ve sürümleri kısıtlama de dahil olmak üzere.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231220"
---
# <a name="restore-packages-using-package-restore"></a>Paket geri yükleme kullanarak paketleri geri yükleme

Bir temizleyici geliştirme ortamını yükseltmek ve depo boyutunu azaltmak için, NuGet **paket geri yüklemesi** proje dosyasında ya da `packages.config`listelenen tüm bağımlılıklarını yükler. .NET Core 2.0 + `dotnet build` ve `dotnet run` komutları otomatik paket geri yükleme yapılır. Visual Studio bir proje oluşturduğunda paketleri otomatik olarak geri yükleyebilir ve Visual Studio, `nuget restore`, `dotnet restore`ve mono üzerinde xbuild aracılığıyla istediğiniz zaman paketleri geri yükleyebilirsiniz.

Paket geri yükleme, tüm proje bağımlılıklarının, kaynak denetiminde depolanması gerekmeden, kullanılabilir olduğundan emin olur. Kaynak denetimi deponuzu paket ikili dosyalarını hariç bırakacak şekilde yapılandırmak için bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Paket geri yüklemeye genel bakış

Paket geri yükleme, önce bir projenin doğrudan bağımlılıklarını gerektiği şekilde yükler ve ardından bu paketlerin tüm bağımlılıklarını bağımlılık grafiğinin tamamında yükler.

Bir paket zaten yüklü değilse, NuGet ilk olarak onu [önbellekten](../consume-packages/managing-the-global-packages-and-cache-folders.md)almaya çalışır. Paket önbellekte değilse, NuGet paketi Visual Studio 'daki **araçlar** > **Seçenekler** > **NuGet Package Manager** > **paket kaynakları** ' nda bulunan tüm etkin kaynaklardan indirmeyi dener. Geri yükleme sırasında, NuGet paket kaynaklarının sırasını yoksayar ve isteklere yanıt vermek için ilk kaynak olan paketi kullanır. NuGet 'in nasıl davrandığı hakkında daha fazla bilgi için bkz. [ortak NuGet yapılandırması](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet, tüm kaynaklar denetlenene kadar bir paketin geri yükleme başarısızlığını göstermez. Bu sırada, NuGet yalnızca listedeki son kaynak için bir hata bildiriyor. Hata, bu kaynakların her biri için ayrı ayrı gösterilmese de, paketin diğer kaynakların *hiçbirinde* mevcut olmadığını gösterir.

## <a name="restore-packages"></a>Paketleri geri yükle

Paket geri yükleme, tüm paket bağımlılıklarını proje dosyanızdaki (*. csproj*) veya *Packages. config* dosyanızdaki paket başvurularıyla eşleşen doğru duruma yüklemeye çalışır. (Visual Studio 'da, başvurular **Bağımlılıklar \ NuGet** veya **başvurular** düğümü altında Çözüm Gezgini görüntülenir.)

1. Proje dosyanızdaki paket başvuruları doğruysa paketleri geri yüklemek için tercih ettiğiniz aracı kullanın.

   - [Visual Studio](#restore-using-visual-studio) ([otomatik geri yükleme](#restore-packages-automatically-using-visual-studio) veya [el ile geri yükleme](#restore-packages-manually-using-visual-studio))
   - [dotnet CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Paket proje dosyanıza (*. csproj*) veya *paketleriniz. config* dosyanız yanlış ise (paket geri yüklemesinin ardından istenen durumla eşleşmez), bunun yerine paketleri yüklemeniz ya da güncelleştirmeniz gerekir.

   PackageReference kullanan projeler için, başarılı bir geri yüklemeden sonra, paket *genel paketler* klasöründe bulunmalı ve `obj/project.assets.json` dosyası yeniden oluşturulur. `packages.config`kullanan projeler için, paketin projenin `packages` klasöründe görünmesi gerekir. Projenin şimdi başarıyla oluşturulması gerekir. 

2. Paket geri yükleme çalıştırıldıktan sonra eksik paketlerle veya paketle ilgili hatalardan (Visual Studio 'da Çözüm Gezgini hata simgeleri) hala karşılaşıyorsanız, [paket geri yükleme hatalarını giderme](package-restore-troubleshooting.md) veya alternatif olarak, [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)konularında açıklanan yönergeleri izlemeniz gerekebilir.

   Visual Studio 'da Paket Yöneticisi konsolu paketleri yeniden yüklemek için çeşitli esnek seçenekler sağlar. Bkz. [paket-güncelleştirme kullanma](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Visual Studio 'Yu kullanarak geri yükleme

Windows üzerinde Visual Studio 'da şunlardan birini yapın:

- Paketleri otomatik olarak geri yükleyin veya

- Paketleri el ile geri yükleme

### <a name="restore-packages-automatically-using-visual-studio"></a>Visual Studio kullanarak paketleri otomatik olarak geri yükleme

Bir şablondan proje oluşturduğunuzda veya bir proje oluşturduğunuzda paket geri yükleme otomatik olarak gerçekleşir [ve paket geri yükleme 'Yi etkinleştirme ve devre dışı bırakma](#enable-and-disable-package-restore-in-visual-studio)seçeneklerine tabidir. NuGet 4.0 + ' da, bir SDK stili projede (genellikle bir .NET Core veya .NET Standard Projesi) değişiklikler yaptığınızda geri yükleme de otomatik olarak gerçekleşir.

1. Otomatik paket geri yüklemeyi etkinleştirmek için **araçlar** > **Seçenekler** > **NuGet Paket Yöneticisi**' ni ve ardından **paket geri yükleme**altında **Visual Studio 'da derleme sırasında eksik paketleri otomatik olarak denetle** ' yi seçerek etkinleştirin.

   SDK olmayan stil projeleri için, ilk olarak otomatik geri yükleme seçeneğini etkinleştirmek üzere **NuGet 'in eksik paketleri Indirmesine Izin ver** ' i seçmeniz gerekir.

1. Projeyi derleyin.

   Bir veya daha fazla paket hala düzgün yüklenmemişse **Çözüm Gezgini** bir hata simgesi gösterir. Sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin ve etkilenen paketleri kaldırmak ve yeniden yüklemek Için **Paket Yöneticisi** ' ni kullanın. Daha fazla bilgi için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)

   "Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvuruyor," ya da "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor, ancak izin verilmediğinden," [otomatik geri yüklemeyi etkinleştir](#enable-and-disable-package-restore-in-visual-studio)"hatasını görürseniz. Daha eski projeler için Ayrıca bkz. [otomatik paket geri yüklemeye geçiş](#migrate-to-automatic-package-restore-visual-studio). Ayrıca bkz. [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Visual Studio kullanarak paketleri el ile geri yükleme

1. **NuGet paket yöneticisi** > **Araçlar** > **Seçenekler** ' i seçerek paket geri yüklemeyi etkinleştirin. **Paket geri yükleme** seçenekleri altında **NuGet 'in eksik paketleri indirmesine izin ver**' i seçin.

1. **Çözüm Gezgini**, çözüme sağ tıklayın ve **NuGet paketlerini geri yükle**' yi seçin.

   Bir veya daha fazla paket hala düzgün yüklenmemişse **Çözüm Gezgini** bir hata simgesi gösterir. Sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin ve ardından **Paket Yöneticisi** ' ni kullanarak etkilenen paketleri kaldırın ve yeniden yükleyin. Daha fazla bilgi için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)

   "Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvuruyor," ya da "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor, ancak izin verilmediğinden," [otomatik geri yüklemeyi etkinleştir](#enable-and-disable-package-restore-in-visual-studio)"hatasını görürseniz. Daha eski projeler için Ayrıca bkz. [otomatik paket geri yüklemeye geçiş](#migrate-to-automatic-package-restore-visual-studio). Ayrıca bkz. [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Visual Studio 'da paket geri yüklemeyi etkinleştirme ve devre dışı bırakma

Visual Studio 'da paket geri yüklemeyi öncelikle **araçlar** > **Seçenekler** aracılığıyla ( **NuGet Paket Yöneticisi** > kontrol edersiniz:

![NuGet Paket Yöneticisi seçenekleri aracılığıyla paket geri yüklemeyi denetleme](media/Restore-01-AutoRestoreOptions.png)

- **NuGet 'in eksik paketleri Indirmesine Izin ver** , `NuGet.Config` dosyasının [packageresubi bölümündeki](../reference/nuget-config-file.md#packagerestore-section) `packageRestore/enabled` ayarını değiştirerek, Windows üzerinde `%AppData%\NuGet\` ya da Mac/Linux üzerinde `~/.nuget/NuGet/`, tüm paket geri yükleme biçimlerini denetler. Bu ayar ayrıca çözümün Visual Studio 'daki bağlam menüsünde **NuGet paketlerini geri yükle** komutunu da sunar.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > `packageRestore/enabled` ayarını küresel olarak geçersiz kılmak için, Visual Studio 'Yu başlatmadan veya bir derlemeyi başlatmadan önce **Enablenugetpackageresant** ortam değişkenini true veya false değeriyle ayarlayın.

- **Visual Studio 'da derleme sırasında eksik paketleri otomatik olarak denetle** `NuGet.Config` dosyasının [packageresubi bölümündeki](../reference/nuget-config-file.md#packagerestore-section) `packageRestore/automatic` ayarını değiştirerek otomatik geri yüklemeyi denetler. Bu seçenek true olarak ayarlandığında, Visual Studio 'dan bir derlemeyi çalıştırmak eksik paketleri otomatik olarak geri yükler. Bu ayar MSBuild komut satırından çalıştırılan derlemeleri etkilemez.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

Bir bilgisayardaki tüm kullanıcılar için paket geri yüklemeyi etkinleştirmek veya devre dışı bırakmak için, bir geliştirici veya şirket, yapılandırma ayarlarını genel `nuget.config` dosyasına ekleyebilir. Genel `nuget.config`, bazı durumlarda belirli bir `\{IDE}\{Version}\{SKU}\` Visual Studio klasörü veya `~/.local/share`adresinden Mac/Linux altında bulunan Windows 'da `%ProgramData%\NuGet\Config`. Bireysel kullanıcılar daha sonra bir proje düzeyinde gerektiğinde geri yüklemeyi seçmeli olarak etkinleştirebilir. NuGet 'in birden çok yapılandırma dosyasını nasıl önceliklendiren hakkında daha fazla ayrıntı için bkz. [ortak NuGet yapılandırması](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> `packageRestore` ayarları doğrudan `nuget.config`' de düzenlerseniz, Visual Studio 'Yu yeniden başlatarak **Seçenekler** iletişim kutusunda geçerli değerler gösterilir.

### <a name="choose-default-package-management-format"></a>Varsayılan paket yönetimi biçimini seçin

![NuGet Paket Yöneticisi seçeneklerinde varsayılan paket yönetimi biçimini denetle](media/Restore-02-PackageFormatOptions.png)

NuGet, bir projenin paketleri kullanabileceği iki biçimi vardır: [`PackageReference`](package-references-in-project-files.md) ve [`packages.config`](../reference/packages-config.md). Varsayılan biçim **Paket Yönetimi** başlığı altında açılan kutudan seçilebilir. Bir projeye ilk paket yüklendiğinde bir seçenek de kullanılabilir.

> [!Note]
> Bir proje her iki paket yönetimi biçimini de desteklemiyorsa, kullanılan paket yönetim biçimi proje ile uyumlu olan ve bu nedenle, seçeneklerde varsayılan olarak ayarlanan bir seçenek olmayabilir. Ayrıca, Seçenekler penceresinde seçilmiş olsa bile, NuGet ilk paket yüklemesinde seçim yapılmayacaktır.
>
> Paket Yöneticisi konsolu bir projedeki ilk paketi yüklemek için kullanılıyorsa, Seçenekler penceresinde seçilmiş olsa bile, NuGet biçim seçimini istemez.

## <a name="restore-using-the-dotnet-cli"></a>DotNet CLı kullanarak geri yükleme

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Proje dosyasına eksik bir paket başvurusu eklemek için, `restore` komutunu da çalıştıran [DotNet Add paketini](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)kullanın.

## <a name="restore-using-the-nugetexe-cli"></a>NuGet. exe CLı kullanarak geri yükleme

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> `restore`komutu bir proje dosyasını veya *Packages. config*öğesini değiştirmez. Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *Packages. config dosyasını* değiştirip `install` ya da `restore`çalıştırın.

## <a name="restore-using-msbuild"></a>MSBuild kullanarak geri yükleme

Proje dosyasında listelenen paketleri PackageReference ile geri yüklemek için [MSBuild-t:restore](../reference/msbuild-targets.md#restore-target) komutunu kullanın. Bu komut, Visual Studio 2017 ve üzeri sürümlerde bulunan NuGet 4. x + ve MSBuild 15.1 + ' da kullanılabilir. Hem `nuget restore` hem de `dotnet restore` ilgili projeler için bu komutu kullanın.

1. Bir geliştirici komut istemi açın ( **arama** kutusunda, **Geliştirici komut istemi**yazın).

   Visual Studio için Geliştirici Komut İstemi, MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle **Başlangıç** menüsünden başlatmak istersiniz.

2. Proje dosyasını içeren klasöre geçin ve aşağıdaki komutu yazın.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Projeyi yeniden derlemek için aşağıdaki komutu yazın.

   ```cmd
   msbuild
   ```

   MSBuild çıkışının, yapılandırmanın başarıyla tamamlandığını gösteriyor olduğundan emin olun.

## <a name="restore-using-azure-pipelines"></a>Azure Pipelines kullanarak geri yükleme

Azure Pipelines ' de bir derleme tanımı oluşturduğunuzda, herhangi bir yapı görevinin önüne, tanım içine NuGet [geri yükleme](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) veya .NET Core [geri yükleme](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) görevini ekleyin. Bazı yapı şablonlarında geri yükleme görevi varsayılan olarak yer alır.

## <a name="restore-using-azure-devops-server"></a>Azure DevOps Server kullanarak geri yükleme

TFS 2013 veya sonraki bir ekip derleme şablonu kullanıyorsanız, derleme sırasında Azure DevOps Server ve TFS 2013 ve üzeri paketleri otomatik olarak geri yükler. Önceki TFS sürümleri için bir komut satırı geri yükleme seçeneği çalıştırmak için bir derleme adımı ekleyebilir veya isteğe bağlı olarak yapı şablonunu daha sonraki bir sürüme geçirebilirsiniz. Daha fazla bilgi için bkz. [Team Foundation Build ile paket geri yüklemeyi ayarlama](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Paket sürümlerini geri yükleme ile sınırlama

NuGet, paketleri herhangi bir yöntemle geri yüklediğinde, `packages.config` veya proje dosyasında belirttiğiniz tüm kısıtlamalara sahiptir:

- `packages.config`, bağımlılığın `allowedVersion` özelliğinde bir sürüm aralığı belirtebilirsiniz. Daha fazla bilgi için bkz. [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) . Örnek:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Bir proje dosyasında, bir bağımlılığın doğrudan aralığını belirtmek için PackageReference kullanabilirsiniz. Örnek:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, [paket sürümü oluşturma](../concepts/package-versioning.md)bölümünde açıklanan gösterimi kullanın.

## <a name="force-restore-from-package-sources"></a>Paket kaynaklarından geri yüklemeyi zorla

NuGet geri yükleme işlemleri, varsayılan olarak genel paketler ve [önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md)bölümünde açıklanan *genel paketler* ve *http önbellek* klasörlerinden paketleri kullanır.

*Küresel paketler* klasörünü kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- `nuget locals global-packages -clear` veya `dotnet nuget locals global-packages --clear`kullanarak klasörü temizleyin.
- Aşağıdaki yöntemlerden birini kullanarak, geri yükleme işleminden önce *genel paketler* klasörünün konumunu geçici olarak değiştirin:
  - NUGET_PACKAGES ortam değişkenini farklı bir klasöre ayarlayın.
  - `globalPackagesFolder` (PackageReference kullanılıyorsa) veya `repositoryPath` (`packages.config`kullanılıyorsa) farklı bir klasöre ayarlayan `NuGet.Config` bir dosya oluşturun. Daha fazla bilgi için bkz. [yapılandırma ayarları](../reference/nuget-config-file.md#config-section).
  - Yalnızca MSBuild: `RestorePackagesPath` özelliği ile farklı bir klasör belirtin.

HTTP kaynakları için önbelleği kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- `nuget restore``-NoCache` seçeneğini veya `dotnet restore`ile `--no-cache` seçeneğini kullanın. Bu seçenekler, Visual Studio Paket Yöneticisi veya konsolu aracılığıyla geri yükleme işlemlerini etkilemez.
- `nuget locals http-cache -clear` veya `dotnet nuget locals http-cache --clear`kullanarak önbelleği temizleyin.
- NUGET_HTTP_CACHE_PATH ortam değişkenini geçici olarak farklı bir klasöre ayarlayın.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Otomatik paket geri yüklemeye geçiş (Visual Studio)

NuGet 2,6 ve önceki sürümlerde, MSBuild ile tümleşik bir paket geri yükleme daha önce destekleniyordu ancak artık doğru değildir. (Visual Studio 'da bir çözüme sağ tıklayıp **NuGet paketini geri yüklemeyi etkinleştir**' i seçerek, bu genellikle etkinleştirilmiştir. Projeniz kullanım dışı olan MSBuild ile tümleşik paket geri yüklemeyi kullanıyorsa, lütfen otomatik paket geri yüklemeye geçirin.

MSBuild ile tümleşik paket geri yükleme kullanan projeler genellikle üç dosya içeren bir *. NuGet* klasörü Içerir: *NuGet. config*, *NuGet. exe*ve *NuGet. targets*. *NuGet. targets* dosyasının varlığı, NuGet 'in MSBuild-unınted yaklaşımını kullanmaya devam edip etmediğini belirler, bu nedenle geçiş sırasında bu dosyanın kaldırılması gerekir.

Otomatik paket geri yüklemeye geçiş yapmak için:

1. Visual Studio’yu kapatın.
2. *. NuGet/NuGet. exe* ve *. NuGet/NuGet. targets*öğesini silin.
3. Her proje dosyası için `<RestorePackages>` öğesini kaldırın ve *NuGet. targets*başvurusunu kaldırın.

Otomatik paket geri yüklemeyi test etmek için:

1. Çözüm klasöründen *paketler* klasörünü kaldırın.
2. Visual Studio 'da çözümü açın ve bir derleme başlatın.

   Otomatik paket geri yükleme, her bağımlılık paketini, kaynak denetimine eklenmeden önce indirip yüklemelidir.

## <a name="troubleshooting"></a>Sorun giderme

Bkz. [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).
