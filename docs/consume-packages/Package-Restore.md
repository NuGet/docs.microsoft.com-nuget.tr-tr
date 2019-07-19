---
title: NuGet paketini geri yükleme
description: NuGet 'in bir proje tarafından nasıl geri yükleneceği hakkında genel bakış, geri yüklemeyi devre dışı bırakma ve sürümleri kısıtlama de dahil olmak üzere.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 0df2b0ebcf438fba99291558f1cf929dcb32618b
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316981"
---
# <a name="package-restore-options"></a>Paket geri yükleme seçenekleri

Bir temizleyici geliştirme ortamını yükseltmek ve depo boyutunu azaltmak için, NuGet **paket geri yüklemesi** proje dosyasında veya `packages.config`proje dosyasında listelenen tüm bağımlılıklarını yükler. .NET Core 2.0 + `dotnet build` ve `dotnet run` komutları bir otomatik paket geri yükleme yapılır. Visual Studio bir proje oluşturduğunda paketleri otomatik olarak geri yükleyebilir ve Visual Studio, `nuget restore`, `dotnet restore`, ve mono üzerinde xbuild aracılığıyla istediğiniz zaman paketleri geri yükleyebilirsiniz.

Paket geri yükleme, tüm proje bağımlılıklarının, kaynak denetiminde depolanması gerekmeden, kullanılabilir olduğundan emin olur. Kaynak denetimi deponuzu paket ikili dosyalarını hariç bırakacak şekilde yapılandırmak için bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Paket geri yüklemeye genel bakış

Paket geri yükleme, önce bir projenin doğrudan bağımlılıklarını gerektiği şekilde yükler ve ardından bu paketlerin tüm bağımlılıklarını bağımlılık grafiğinin tamamında yükler.

Bir paket zaten yüklü değilse, NuGet ilk olarak onu [önbellekten](../consume-packages/managing-the-global-packages-and-cache-folders.md)almaya çalışır. Paket önbellekte değilse, NuGet paketi listedeki tüm etkin kaynaklardan indirmeye çalışır, Visual 'teki **araç** > **seçenekleri** > **NuGet Paket Yöneticisi** > **paket kaynakları** Stu. Geri yükleme sırasında, NuGet paket kaynaklarının sırasını yoksayar ve isteklere yanıt vermek için ilk kaynak olan paketi kullanır. NuGet 'in nasıl davrandığı hakkında daha fazla bilgi için bkz. [ortak NuGet yapılandırması](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet, tüm kaynaklar denetlenene kadar bir paketin geri yükleme başarısızlığını göstermez. Bu sırada, NuGet yalnızca listedeki son kaynak için bir hata bildiriyor. Hata, bu kaynakların her biri için ayrı ayrı gösterilmese de, paketin diğer kaynakların *hiçbirinde* mevcut olmadığını gösterir.

## <a name="restore-packages"></a>Paketleri geri yükle

Aşağıdaki yollarla paket geri yüklemeyi tetikleyebilirsiniz:

- **Visual Studio**: Windows üzerinde Visual Studio 'da aşağıdaki yöntemlerden birini kullanın.

    - Paketleri otomatik olarak geri yükleyin. Bir şablondan proje oluşturduğunuzda veya bir proje oluşturduğunuzda paket geri yükleme otomatik olarak gerçekleşir [ve paket geri yükleme 'Yi etkinleştirme ve devre dışı bırakma](#enable-and-disable-package-restore-visual-studio)seçeneklerine tabidir. NuGet 4.0 + ' da, bir SDK stili projede (genellikle bir .NET Core veya .NET Standard Projesi) değişiklikler yaptığınızda geri yükleme de otomatik olarak gerçekleşir.

    - Paketleri el ile geri yükleyin. El ile geri yüklemek için **Çözüm Gezgini** çözüme sağ tıklayın ve **NuGet paketlerini geri yükle**' yi seçin. Bir veya daha fazla paket hala düzgün yüklenmemişse **Çözüm Gezgini** bir hata simgesi gösterir. Sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin ve etkilenen paketleri kaldırmak ve yeniden yüklemek Için **Paket Yöneticisi** ' ni kullanın. Daha fazla bilgi için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)

    "Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvuruyor," ya da "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor, ancak izin verilmediğinden," [otomatik geri yüklemeyi etkinleştir](#enable-and-disable-package-restore-visual-studio)"hatasını görürseniz. Ayrıca bkz. [otomatik paket geri yükleme](#migrate-to-automatic-package-restore-visual-studio) ve [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

- **DotNet CLI**: Komut satırında, projenizi içeren klasöre geçin ve ardından [DotNet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanarak proje dosyasında listelenen paketleri [packagereference](../consume-packages/package-references-in-project-files.md)ile geri yükleyin. .NET Core 2,0 ve üzeri ile geri yükleme, `dotnet build` ve `dotnet run` komutlarıyla otomatik olarak gerçekleşir.  

- **NuGet. exe CLI**: Komut satırında, projenizi içeren klasöre geçin ve ardından bir proje veya çözüm dosyasında veya `packages.config`' de listelenen paketleri geri yüklemek için [NuGet restore](../reference/cli-reference/cli-ref-restore.md) komutunu kullanın. 

- **MSBuild**: Proje dosyasında listelenen paketleri PackageReference ile geri yüklemek için [MSBuild-t:restore](../reference/msbuild-targets.md#restore-target) komutunu kullanın. Bu komut, Visual Studio 2017 ve üzeri sürümlerde bulunan NuGet 4. x + ve MSBuild 15.1 + ' da kullanılabilir. Her ikisi de `nuget restore` ilgili projeler için bu komutu kullanın.`dotnet restore`

- **Azure Pipelines**: Azure Pipelines ' de bir derleme tanımı oluşturduğunuzda, herhangi bir yapı görevinin önüne, tanım içine NuGet [geri yükleme](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) veya .NET Core [geri yükleme](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) görevini ekleyin. Bazı yapı şablonlarında geri yükleme görevi varsayılan olarak yer alır.

- **Azure DevOps Server**: TFS 2013 veya sonraki bir ekip derleme şablonu kullanıyorsanız, derleme sırasında Azure DevOps Server ve TFS 2013 ve üzeri paketleri otomatik olarak geri yükler. Önceki TFS sürümleri için bir komut satırı geri yükleme seçeneği çalıştırmak için bir derleme adımı ekleyebilir veya isteğe bağlı olarak yapı şablonunu daha sonraki bir sürüme geçirebilirsiniz. Daha fazla bilgi için bkz. [Team Foundation Build ile paket geri yüklemeyi ayarlama](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore-visual-studio"></a>Paket geri yüklemeyi etkinleştirme ve devre dışı bırakma (Visual Studio)

Visual Studio 'da paket geri yüklemeyi birincil olarak **Araçlar** > **Seçenekler** > **NuGet Paket Yöneticisi**aracılığıyla denetlersiniz:

![NuGet Paket Yöneticisi seçenekleri aracılığıyla paket geri yüklemeyi denetleme](media/Restore-01-AutoRestoreOptions.png)

- **NuGet 'in eksik paketleri indirmesine izin ver** `packageRestore/enabled` ayarı, `NuGet.Config` dosyanın Windows veya `~/.nuget/NuGet/` Mac/Linux üzerinde bulunan `%AppData%\NuGet\` [packageresgerme bölümündeki](../reference/nuget-config-file.md#packagerestore-section) ayarı değiştirerek tüm paket geri yükleme biçimlerini denetler. Bu ayar ayrıca çözümün Visual Studio 'daki bağlam menüsünde **NuGet paketlerini geri yükle** komutunu da sunar.

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
  > `packageRestore/enabled` Ayarı Global olarak geçersiz kılmak için, Visual Studio 'yu başlatmadan veya bir derlemeyi başlatmadan önce **enablenugetpackageresant** ortam değişkenini true veya false değerine ayarlayın.

- **Visual Studio 'da derleme sırasında eksik paketleri otomatik olarak denetle** , `packageRestore/automatic` `NuGet.Config` dosyanın [packageresgerme bölümündeki](../reference/nuget-config-file.md#packagerestore-section) ayarı değiştirerek otomatik geri yüklemeyi denetler. Bu seçenek true olarak ayarlandığında, Visual Studio 'dan bir derlemeyi çalıştırmak eksik paketleri otomatik olarak geri yükler. Bu ayar MSBuild komut satırından çalıştırılan derlemeleri etkilemez.

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

Bir bilgisayardaki tüm kullanıcılar için paket geri yüklemeyi etkinleştirmek veya devre dışı bırakmak için, bir geliştirici veya şirket, yapılandırma ayarlarını genel `nuget.config` dosyasına ekleyebilir. Genel `nuget.config` olarak `\{IDE}\{Version}\{SKU}\` Windows 'ta, bazı durumlarda belirli bir Visual Studio `~/.local/share`klasörü veya Mac/Linux 'ta. `%ProgramData%\NuGet\Config` Bireysel kullanıcılar daha sonra bir proje düzeyinde gerektiğinde geri yüklemeyi seçmeli olarak etkinleştirebilir. NuGet 'in birden çok yapılandırma dosyasını nasıl önceliklendiren hakkında daha fazla ayrıntı için bkz. [ortak NuGet yapılandırması](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> `packageRestore` Ayarları doğrudan ' de `nuget.config`düzenlerseniz, Visual Studio 'yu yeniden başlatarak **Seçenekler** iletişim kutusunda geçerli değerler gösterilir.

## <a name="constrain-package-versions-with-restore"></a>Paket sürümlerini geri yükleme ile sınırlama

NuGet, paketleri herhangi bir yöntemle geri yüklediğinde, `packages.config` veya proje dosyasında belirttiğiniz kısıtlamalara sahiptir:

- İçinde `packages.config`, bağımlılık `allowedVersion` özelliğinde bir sürüm aralığı belirtebilirsiniz. Daha fazla bilgi için bkz. [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) . Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Bir proje dosyasında, bir bağımlılığın doğrudan aralığını belirtmek için PackageReference kullanabilirsiniz. Örneğin:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, [paket sürümü oluşturma](../reference/package-versioning.md)bölümünde açıklanan gösterimi kullanın.

## <a name="force-restore-from-package-sources"></a>Paket kaynaklarından geri yüklemeyi zorla

NuGet geri yükleme işlemleri, varsayılan olarak genel paketler ve [önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md)bölümünde açıklanan *genel paketler* ve *http önbellek* klasörlerinden paketleri kullanır.

*Küresel paketler* klasörünü kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- `nuget locals global-packages -clear` Veya`dotnet nuget locals global-packages --clear`kullanarak klasörü temizleyin.
- Aşağıdaki yöntemlerden birini kullanarak, geri yükleme işleminden önce *genel paketler* klasörünün konumunu geçici olarak değiştirin:
  - NUGET_PACKAGES ortam değişkenini farklı bir klasöre ayarlayın.
  - Farklı bir `NuGet.Config` klasöre (packagereference kullanılıyorsa `packages.config`) veya `repositoryPath` (kullanılıyorsa) ayarlayan `globalPackagesFolder` bir dosya oluşturun. Daha fazla bilgi için bkz. [yapılandırma ayarları](../reference/nuget-config-file.md#config-section).
  - Yalnızca MSBuild: `RestorePackagesPath` Özelliği ile farklı bir klasör belirtin.

HTTP kaynakları için önbelleği kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- `-NoCache` Seçeneğini`nuget restore`veya ile`--no-cache`seçeneğini kullanın .`dotnet restore` Bu seçenekler, Visual Studio Paket Yöneticisi veya konsolu aracılığıyla geri yükleme işlemlerini etkilemez.
- `nuget locals http-cache -clear` Veya`dotnet nuget locals http-cache --clear`kullanarak önbelleği temizleyin.
- NUGET_HTTP_CACHE_PATH ortam değişkenini geçici olarak farklı bir klasöre ayarlayın.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Otomatik paket geri yüklemeye geçiş (Visual Studio)

NuGet 2,6 ve önceki sürümlerde, MSBuild ile tümleşik bir paket geri yükleme daha önce destekleniyordu ancak artık doğru değildir. (Visual Studio 'da bir çözüme sağ tıklayıp **NuGet paketini geri yüklemeyi etkinleştir**' i seçerek, bu genellikle etkinleştirilmiştir. Projeniz kullanım dışı olan MSBuild ile tümleşik paket geri yüklemeyi kullanıyorsa, lütfen otomatik paket geri yüklemeye geçirin.

MSBuild ile tümleşik paket geri yükleme kullanan projeler genellikle üç dosya içeren bir *. NuGet* klasörü içerir: *NuGet. config*, *NuGet. exe*ve *NuGet. targets*. *NuGet. targets* dosyasının varlığı, NuGet 'in MSBuild-unınted yaklaşımını kullanmaya devam edip etmediğini belirler, bu nedenle geçiş sırasında bu dosyanın kaldırılması gerekir.

Otomatik paket geri yüklemeye geçiş yapmak için:

1. Visual Studio’yu kapatın.
2. *. NuGet/NuGet. exe* ve *. NuGet/NuGet. targets*öğesini silin.
3. Her proje dosyası için, `<RestorePackages>` öğesini kaldırın ve *NuGet. targets*başvurusunu kaldırın.

Otomatik paket geri yüklemeyi test etmek için:

1. Çözüm klasöründen *paketler* klasörünü kaldırın.
2. Visual Studio 'da çözümü açın ve bir derleme başlatın.

   Otomatik paket geri yükleme, her bağımlılık paketini, kaynak denetimine eklenmeden önce indirip yüklemelidir.

## <a name="troubleshooting"></a>Sorun giderme

Bkz. [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).
