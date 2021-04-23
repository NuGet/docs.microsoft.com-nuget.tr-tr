---
title: NuGet paketini geri yükleme
description: NuGet 'in bir proje tarafından nasıl geri yükleneceği hakkında genel bakış, geri yüklemeyi devre dışı bırakma ve sürümleri kısıtlama de dahil olmak üzere.
author: JonDouglas
ms.author: jodou
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 6cdc826c85f233c7108a53ad244aa8c47df0be67
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901843"
---
# <a name="restore-packages-using-package-restore"></a>Paket geri yükleme kullanarak paketleri geri yükleme

Bir temizleyici geliştirme ortamını yükseltmek ve depo boyutunu azaltmak için, NuGet **paket geri yüklemesi** proje dosyasında veya proje dosyasında listelenen tüm bağımlılıklarını yükler `packages.config` . .NET Core 2.0 + `dotnet build` ve `dotnet run` komutları bir otomatik paket geri yükleme yapılır. Visual Studio bir proje oluşturduğunda paketleri otomatik olarak geri yükleyebilir ve Visual Studio, `nuget restore` ,, `dotnet restore` ve mono üzerinde xbuild aracılığıyla istediğiniz zaman paketleri geri yükleyebilirsiniz.

Paket geri yükleme, tüm proje bağımlılıklarının, kaynak denetiminde depolanması gerekmeden, kullanılabilir olduğundan emin olur. Kaynak denetimi deponuzu paket ikili dosyalarını hariç bırakacak şekilde yapılandırmak için bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Paket geri yüklemeye genel bakış

Paket geri yükleme, önce bir projenin doğrudan bağımlılıklarını gerektiği şekilde yükler ve ardından bu paketlerin tüm bağımlılıklarını bağımlılık grafiğinin tamamında yükler.

Bir paket zaten yüklü değilse, NuGet ilk olarak onu [önbellekten](../consume-packages/managing-the-global-packages-and-cache-folders.md)almaya çalışır. Paket önbellekte değilse, NuGet paketi   >    >  Visual Studio 'daki araçlar seçenekleri **NuGet Paket Yöneticisi**  >  **paket kaynakları** ' nda bulunan tüm etkin kaynaklardan indirmeyi dener. Geri yükleme sırasında, NuGet paket kaynaklarının sırasını yoksayar ve isteklere yanıt vermek için ilk kaynak olan paketi kullanır. NuGet 'in nasıl davrandığı hakkında daha fazla bilgi için bkz. [ortak NuGet yapılandırması](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet, tüm kaynaklar denetlenene kadar bir paketin geri yükleme başarısızlığını göstermez. Bu sırada, NuGet yalnızca listedeki son kaynak için bir hata bildiriyor. Hata, bu kaynakların her biri için ayrı ayrı gösterilmese de, paketin diğer kaynakların *hiçbirinde* mevcut olmadığını gösterir.

## <a name="restore-packages"></a>Paketleri geri yükleme

Paket geri yükleme, tüm paket bağımlılıklarını proje dosyanızdaki (*. csproj*) veya *packages.config* dosyanızdaki paket başvurularıyla eşleşen doğru duruma yüklemeye çalışır. (Visual Studio 'da, başvurular **Bağımlılıklar \ NuGet** veya **başvurular** düğümü altında Çözüm Gezgini görüntülenir.)

1. Proje dosyanızdaki paket başvuruları doğruysa paketleri geri yüklemek için tercih ettiğiniz aracı kullanın.

   - [Visual Studio](#restore-using-visual-studio) ([otomatik geri yükleme](#restore-packages-automatically-using-visual-studio) veya [el ile geri yükleme](#restore-packages-manually-using-visual-studio))
   - [dotnet CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Paket proje dosyanıza (*. csproj*) başvuruyorsa veya *packages.config* dosyanız hatalıysa (paket geri yüklemesinin ardından istenen durumla eşleşmez), bunun yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir.

   PackageReference kullanan projeler için başarılı bir geri yüklemeden sonra, paket *genel paketler* klasöründe bulunmalı ve `obj/project.assets.json` dosya yeniden oluşturulur. Kullanan projeler için `packages.config` , paketin projenin klasöründe görünmesi gerekir `packages` . Projenin şimdi başarıyla oluşturulması gerekir. 

2. Paket geri yükleme çalıştırıldıktan sonra eksik paketlerle veya paketle ilgili hatalardan (Visual Studio 'da Çözüm Gezgini hata simgeleri) hala karşılaşıyorsanız, [paket geri yükleme hatalarını giderme](package-restore-troubleshooting.md) veya alternatif olarak, [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)konularında açıklanan yönergeleri izlemeniz gerekebilir.

   Visual Studio 'da Paket Yöneticisi konsolu paketleri yeniden yüklemek için çeşitli esnek seçenekler sağlar. Bkz. [paket-güncelleştirme kullanma](reinstalling-and-updating-packages.md#using-update-package).

## <a name="restore-using-visual-studio"></a>Visual Studio 'Yu kullanarak geri yükleme

Windows üzerinde Visual Studio 'da şunlardan birini yapın:

- Paketleri otomatik olarak geri yükleyin veya

- Paketleri el ile geri yükleme

### <a name="restore-packages-automatically-using-visual-studio"></a>Visual Studio kullanarak paketleri otomatik olarak geri yükleme

Bir şablondan proje oluşturduğunuzda veya bir proje oluşturduğunuzda paket geri yükleme otomatik olarak gerçekleşir [ve paket geri yükleme 'Yi etkinleştirme ve devre dışı bırakma](#enable-and-disable-package-restore-in-visual-studio)seçeneklerine tabidir. NuGet 4.0 + ' da, bir SDK stili projede (genellikle bir .NET Core veya .NET Standard Projesi) değişiklikler yaptığınızda geri yükleme de otomatik olarak gerçekleşir.

1. **Araçlar**  >  **Seçenekler**  >  **NuGet Paket Yöneticisi**' ni seçerek otomatik paket geri yüklemeyi etkinleştirin ve sonra Visual Studio 'da **paket geri yükleme** altında **eksik paketleri otomatik olarak denetle** ' yi seçin.

   SDK olmayan stil projeleri için, ilk olarak otomatik geri yükleme seçeneğini etkinleştirmek üzere **NuGet 'in eksik paketleri Indirmesine Izin ver** ' i seçmeniz gerekir.

1. Projeyi derleyin.

   Bir veya daha fazla paket hala düzgün yüklenmemişse **Çözüm Gezgini** bir hata simgesi gösterir. Sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin ve etkilenen paketleri kaldırmak ve yeniden yüklemek Için **Paket Yöneticisi** ' ni kullanın. Daha fazla bilgi için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)

   "Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvuruyor," ya da "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor, ancak izin verilmediğinden," [otomatik geri yüklemeyi etkinleştir](#enable-and-disable-package-restore-in-visual-studio)"hatasını görürseniz. Daha eski projeler için Ayrıca bkz. [otomatik paket geri yüklemeye geçiş](#migrate-to-automatic-package-restore-visual-studio). Ayrıca bkz. [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

### <a name="restore-packages-manually-using-visual-studio"></a>Visual Studio kullanarak paketleri el ile geri yükleme

1. **Araçlar**  >  **Seçenekler**  >  **NuGet Paket Yöneticisi**' ni seçerek paket geri yüklemeyi etkinleştirin. **Paket geri yükleme** seçenekleri altında **NuGet 'in eksik paketleri indirmesine izin ver**' i seçin.

1. **Çözüm Gezgini**, çözüme sağ tıklayın ve **NuGet paketlerini geri yükle**' yi seçin.

   Bir veya daha fazla paket hala düzgün yüklenmemişse **Çözüm Gezgini** bir hata simgesi gösterir. Sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin ve ardından **Paket Yöneticisi** ' ni kullanarak etkilenen paketleri kaldırın ve yeniden yükleyin. Daha fazla bilgi için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)

   "Bu proje, bu bilgisayarda eksik olan NuGet paketlerine başvuruyor," ya da "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor, ancak izin verilmediğinden," [otomatik geri yüklemeyi etkinleştir](#enable-and-disable-package-restore-in-visual-studio)"hatasını görürseniz. Daha eski projeler için Ayrıca bkz. [otomatik paket geri yüklemeye geçiş](#migrate-to-automatic-package-restore-visual-studio). Ayrıca bkz. [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Visual Studio 'da paket geri yüklemeyi etkinleştirme ve devre dışı bırakma

Visual Studio 'da paket geri yüklemeyi birincil olarak **Araçlar**  >  **Seçenekler**  >  **NuGet Paket Yöneticisi** aracılığıyla denetlersiniz:

![NuGet Paket Yöneticisi seçenekleri aracılığıyla paket geri yüklemeyi denetleme](media/Restore-01-AutoRestoreOptions.png)

- **NuGet 'in eksik paketleri Indirmesine Izin ver** `packageRestore/enabled` ayarı, dosyanın Windows veya Mac/Linux üzerinde bulunan [packageresgerme bölümündeki](../reference/nuget-config-file.md#packagerestore-section) ayarı değiştirerek tüm paket geri yükleme biçimlerini denetler `NuGet.Config` `%AppData%\NuGet\` `~/.nuget/NuGet/` . Bu ayar ayrıca çözümün Visual Studio 'daki bağlam menüsünde **NuGet paketlerini geri yükle** komutunu da sunar.

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
  > Ayarı Global olarak geçersiz kılmak için `packageRestore/enabled` , Visual Studio 'yu başlatmadan veya bir derlemeyi başlatmadan önce **Enablenugetpackageresant** ortam değişkenini true veya false değerine ayarlayın.

- **Visual Studio 'da derleme sırasında eksik paketleri otomatik olarak denetle** `packageRestore/automatic` , dosyanın [packageresgerme bölümündeki](../reference/nuget-config-file.md#packagerestore-section) ayarı değiştirerek otomatik geri yüklemeyi denetler `NuGet.Config` . Bu seçenek true olarak ayarlandığında, Visual Studio 'dan bir derlemeyi çalıştırmak eksik paketleri otomatik olarak geri yükler. Bu ayar MSBuild komut satırından çalıştırılan derlemeleri etkilemez.

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

Bir bilgisayardaki tüm kullanıcılar için paket geri yüklemeyi etkinleştirmek veya devre dışı bırakmak için, bir geliştirici veya şirket, yapılandırma ayarlarını genel dosyasına ekleyebilir `nuget.config` . Genel olarak `nuget.config` Windows 'ta, `%ProgramData%\NuGet\Config` bazı durumlarda belirli bir `\{IDE}\{Version}\{SKU}\` Visual Studio klasörü veya Mac/Linux 'ta `~/.local/share` . Bireysel kullanıcılar daha sonra bir proje düzeyinde gerektiğinde geri yüklemeyi seçmeli olarak etkinleştirebilir. NuGet 'in birden çok yapılandırma dosyasını nasıl önceliklendiren hakkında daha fazla ayrıntı için bkz. [ortak NuGet yapılandırması](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> `packageRestore`Ayarları doğrudan ' de düzenlerseniz, `nuget.config` Visual Studio 'yu yeniden başlatarak **Seçenekler** iletişim kutusunda geçerli değerler gösterilir.

### <a name="choose-default-package-management-format"></a>Varsayılan paket yönetimi biçimini seçin

![NuGet Paket Yöneticisi seçeneklerinde varsayılan paket yönetimi biçimini denetle](media/Restore-02-PackageFormatOptions.png)

NuGet, bir projenin paketleri kullanabileceği iki biçimi vardır: [`PackageReference`](package-references-in-project-files.md) ve [`packages.config`](../reference/packages-config.md) . Varsayılan biçim **Paket Yönetimi** başlığı altında açılan kutudan seçilebilir. Bir projeye ilk paket yüklendiğinde bir seçenek de kullanılabilir.

> [!Note]
> Bir proje her iki paket yönetimi biçimini de desteklemiyorsa, kullanılan paket yönetim biçimi proje ile uyumlu olan ve bu nedenle, seçeneklerde varsayılan olarak ayarlanan bir seçenek olmayabilir. Ayrıca, Seçenekler penceresinde seçilmiş olsa bile, NuGet ilk paket yüklemesinde seçim yapılmayacaktır.
>
> Paket Yöneticisi konsolu bir projedeki ilk paketi yüklemek için kullanılıyorsa, Seçenekler penceresinde seçilmiş olsa bile, NuGet biçim seçimini istemez.

## <a name="restore-using-the-dotnet-cli"></a>DotNet CLı kullanarak geri yükleme

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Proje dosyasına eksik bir paket başvurusu eklemek için, aynı zamanda komutunu çalıştıran [DotNet Add paketini](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)kullanın `restore` .

## <a name="restore-using-the-nugetexe-cli"></a>nuget.exe CLı kullanarak geri yükleme

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> `restore`Komut bir proje dosyasını veya *packages.config* değiştirmez. Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *packages.config* değiştirin ve sonra ya da çalıştırın `install` `restore` .

## <a name="restore-using-msbuild"></a>MSBuild kullanarak geri yükleme

Proje dosyasında listelenen paketleri geri yüklemek için [MSBuild-t:restore](../reference/msbuild-targets.md#restore-target) komutunu kullanın (bkz. [packagereference](package-references-in-project-files.md)) ve MSBuild 16.5 +, projeler ile başlama `packages.config` .

 Bu komut, Visual Studio 2017 ve üzeri sürümlerde bulunan NuGet 4. x + ve MSBuild 15.1 + ' da kullanılabilir.
MSBuild 16.5 + ile başlayarak bu komut, `packages.config` ile birlikte çalıştırıldığında tabanlı projeleri de geri yükleyebilir `-p:RestorePackagesConfig=true` .

1. Bir geliştirici komut istemi açın ( **arama** kutusunda, **Geliştirici komut istemi** yazın).

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
   
> [!Note]
> MSBuild 'in `-restore` çalışacağı bir anahtarı vardır `Restore` , projeyi yeniden yükler ve ardından derler. Bkz. [bir MSBuild komutuyla geri yükleme ve oluşturma](../reference/msbuild-targets.md#restoring-and-building-with-one-msbuild-command).

```cmd
# Will restore the project, then build, since build is the default target.
msbuild -restore
```

## <a name="restore-using-azure-pipelines"></a>Azure Pipelines kullanarak geri yükleme

Azure Pipelines ' de bir derleme tanımı oluşturduğunuzda, herhangi bir yapı görevinin önüne, tanım içine NuGet [geri yükleme](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) veya .NET Core [geri yükleme](/azure/devops/pipelines/tasks/build/dotnet-core-cli) görevini ekleyin. Bazı yapı şablonlarında geri yükleme görevi varsayılan olarak yer alır.

## <a name="restore-using-azure-devops-server"></a>Azure DevOps Server kullanarak geri yükleme

TFS 2013 veya sonraki bir ekip derleme şablonu kullanıyorsanız, derleme sırasında Azure DevOps Server ve TFS 2013 ve üzeri paketleri otomatik olarak geri yükler. Önceki TFS sürümleri için bir komut satırı geri yükleme seçeneği çalıştırmak için bir derleme adımı ekleyebilir veya isteğe bağlı olarak yapı şablonunu daha sonraki bir sürüme geçirebilirsiniz. Daha fazla bilgi için bkz. [Team Foundation Build ile paket geri yüklemeyi ayarlama](../consume-packages/team-foundation-build.md).

## <a name="constrain-package-versions-with-restore"></a>Paket sürümlerini geri yükleme ile sınırlama

NuGet, paketleri herhangi bir yöntemle geri yüklediğinde, `packages.config` veya proje dosyasında belirttiğiniz kısıtlamalara sahiptir:

- İçinde `packages.config` , bağımlılık özelliğinde bir sürüm aralığı belirtebilirsiniz `allowedVersion` . Daha fazla bilgi için bkz. [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) . Örnek:

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

- Veya kullanarak klasörü temizleyin `nuget locals global-packages -clear` `dotnet nuget locals global-packages --clear` .
- Aşağıdaki yöntemlerden birini kullanarak, geri yükleme işleminden önce *genel paketler* klasörünün konumunu geçici olarak değiştirin:
  - NUGET_PACKAGES ortam değişkenini farklı bir klasöre ayarlayın.
  - `NuGet.Config` `globalPackagesFolder` `repositoryPath` Farklı bir klasöre (packagereference kullanılıyorsa) veya (kullanılıyorsa) ayarlayan bir dosya oluşturun `packages.config` . Daha fazla bilgi için bkz. [yapılandırma ayarları](../reference/nuget-config-file.md#config-section).
  - Yalnızca MSBuild: özelliği ile farklı bir klasör belirtin `RestorePackagesPath` .

HTTP kaynakları için önbelleği kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- Seçeneğini veya ile seçeneğini kullanın `-NoCache` `nuget restore` `--no-cache` `dotnet restore` . Bu seçenekler, Visual Studio Paket Yöneticisi veya konsolu aracılığıyla geri yükleme işlemlerini etkilemez.
- Veya kullanarak önbelleği temizleyin `nuget locals http-cache -clear` `dotnet nuget locals http-cache --clear` .
- NUGET_HTTP_CACHE_PATH ortam değişkenini geçici olarak farklı bir klasöre ayarlayın.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Otomatik paket geri yüklemeye geçiş (Visual Studio)

NuGet 2,6 ve önceki sürümlerde, MSBuild ile tümleşik bir paket geri yükleme daha önce destekleniyordu ancak artık doğru değildir. (Visual Studio 'da bir çözüme sağ tıklayıp **NuGet paketini geri yüklemeyi etkinleştir**' i seçerek, bu genellikle etkinleştirilmiştir. Projeniz kullanım dışı olan MSBuild ile tümleşik paket geri yüklemeyi kullanıyorsa, lütfen otomatik paket geri yüklemeye geçirin.

MSBuild-Integrated paketi geri yükleme kullanan projeler genellikle üç dosya içeren bir *. NuGet* klasörü içerir: *NuGet.config*, *nuget.exe* ve *NuGet. targets*. *NuGet. targets* dosyasının varlığı, NuGet 'in MSBuild ile tümleşik yaklaşımı kullanmaya devam edip etmediğini belirler. bu nedenle, geçiş sırasında bu dosyanın kaldırılması gerekir.

Otomatik paket geri yüklemeye geçiş yapmak için:

1. Visual Studio’yu kapatın.
2. *. NuGet/nuget.exe* ve *. NuGet/NuGet. targets* öğesini silin.
3. Her proje dosyası için, öğesini kaldırın `<RestorePackages>` ve *NuGet. targets* başvurusunu kaldırın.

Otomatik paket geri yüklemeyi test etmek için:

1. Çözüm klasöründen *paketler* klasörünü kaldırın.
2. Visual Studio 'da çözümü açın ve bir derleme başlatın.

   Otomatik paket geri yükleme, her bağımlılık paketini, kaynak denetimine eklenmeden önce indirip yüklemelidir.

## <a name="troubleshooting"></a>Sorun giderme

Bkz. [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).
