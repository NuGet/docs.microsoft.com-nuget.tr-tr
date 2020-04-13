---
title: NuGet Paketi Geri Yükleme
description: NuGet'in paketleri nasıl geri yükledığına ilişkin genel bir bakış, sürümleri niçin devre dışı bırakıp sınırlandırılacak da dahil olmak üzere bir projeye bağlıdır.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428746"
---
# <a name="restore-packages-using-package-restore"></a>Paket Geri Yükleme'yi kullanarak paketleri geri yükleme

Daha temiz bir geliştirme ortamını tanıtmak ve depo boyutunu azaltmak için NuGet **Paket Geri Yükleme,** proje dosyasında veya `packages.config`. .NET Core `dotnet build` 2.0+ `dotnet run` ve komutları otomatik paket geri yüklemeyapar. Visual Studio, bir proje oluştururken paketleri otomatik olarak geri yükleyebilir ve Visual `nuget restore` `dotnet restore`Studio, , ve Mono üzerinde xbuild aracılığıyla istediğiniz zaman paketleri geri yükleyebilirsiniz.

Paket Geri Yükleme, kaynak denetiminde depolamak zorunda kalmadan, projenin tüm bağımlılıklarının kullanılabilir olmasını sağlar. Paket ikililerini hariç tutmak için kaynak denetim deponuzu yapılandırmak için [Paketler'e ve kaynak denetimine](../consume-packages/packages-and-source-control.md)bakın. 

## <a name="package-restore-overview"></a>Paket Geri Yükleme genel bakış

Paket Geri Yükleme önce bir projenin doğrudan bağımlılıklarını gerektiği gibi yükler, sonra da tüm bağımlılık grafiği boyunca bu paketlerin bağımlılıklarını yükler.

Bir paket zaten yüklenmiyorsa, NuGet önce [önbellekten](../consume-packages/managing-the-global-packages-and-cache-folders.md)paketi almaya çalışır. Paket önbellekte değilse, NuGet paketi Visual Studio'daki **Tools** > **Options** > **NuGet Package Manager** > **Paket Kaynakları'ndaki** listedeki tüm etkin kaynaklardan indirmeye çalışır. Geri yükleme sırasında NuGet paket kaynaklarının sırasını yok sayar ve istekleri yanıtlamak için ilk kaynaktan gelen paketi kullanır. NuGet'in nasıl bir şekilde nasıl bir şekilde besleri hakkında daha fazla bilgi için [Ortak NuGet yapılandırmalarına](Configuring-NuGet-Behavior.md)bakın. 

> [!Note]
> NuGet, tüm kaynaklar kontrol edilene kadar paketin geri yüklenememesini göstermez. O zaman, NuGet listedeki yalnızca son kaynak için bir hata bildirir. Hata, bu kaynakların her biri için ayrı ayrı gösterilmese de, paketin diğer kaynaklardan *hiçbirinde* bulunmadığı anlamına gelir.

## <a name="restore-packages"></a>Paketleri geri yükleme

Paket Geri Yükleme, tüm paket bağımlılıklarını proje dosyanızdaki paket başvurularıyla *(.csproj)* veya *packages.config* dosyanızla eşleşen doğru duruma yüklemeye çalışır. (Visual Studio'da, başvurular **Bağımlılıklar \ NuGet** veya **Başvuru düğümü** altında Çözüm Gezgini'nde görünür.)

1. Proje dosyanızdaki paket başvuruları doğruysa, paketleri geri yüklemek için tercih ettiğiniz aracı kullanın.

   - [Visual Studio](#restore-using-visual-studio) ([otomatik geri yükleme](#restore-packages-automatically-using-visual-studio) veya manuel geri [yükleme](#restore-packages-manually-using-visual-studio))
   - [dotnet CLI](#restore-using-the-dotnet-cli)
   - [nuget.exe CLI](#restore-using-the-nugetexe-cli)
   - [MSBuild](#restore-using-msbuild)
   - [Azure Pipelines](#restore-using-azure-pipelines)
   - [Azure DevOps Server](#restore-using-azure-devops-server)

   Proje dosyanızdaki paket başvuruları (*.csproj*) veya *packages.config* dosyanız yanlışsa (Paket Geri Yükleme'den sonra istediğiniz durumla eşleşmiyorsa), bunun yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir.

   PackageReference kullanan projeleriçin, başarılı bir geri yüklemeden sonra paket *genel* `obj/project.assets.json` paketler klasöründe bulunmalıdır ve dosya yeniden oluşturulmalıdır. Kullanan `packages.config`projeler için paket, projenin `packages` klasöründe görünmelidir. Proje artık başarıyla inşa edilmelidir. 

2. Paket Geri Yükleme'yi çalıştırdıktan sonra, hala eksik paketler veya paketle ilgili hatalarla (Visual Studio'daki Solution Explorer'daki hata simgeleri gibi) yaşıyorsanız, [Sorun Giderme Paketi Geri Yükleme hatalarında](package-restore-troubleshooting.md) açıklanan yönergeleri izlemeniz veya alternatif olarak [paketleri yeniden yüklemeniz ve güncelleştirmeniz](../consume-packages/reinstalling-and-updating-packages.md)gerekebilir.

   Visual Studio'da Package Manager Console paketleri yeniden yüklemek için birkaç esnek seçenek sunar. Bkz. [Paket Güncelleme'yi kullanma.](reinstalling-and-updating-packages.md#using-update-package)

## <a name="restore-using-visual-studio"></a>Visual Studio kullanarak geri yükleme

Windows'daki Visual Studio'da:

- Paketleri otomatik olarak geri yükleme veya

- Paketleri el ile geri yükleme

### <a name="restore-packages-automatically-using-visual-studio"></a>Visual Studio'u kullanarak paketleri otomatik olarak geri yükleme

Paket Geri Yükleme, bir şablondan bir proje oluşturduğunuzda veya bir proje oluşturduğunuzda, [Etkinleştir ve paketi geri yüklemeyi devre dışı etme](#enable-and-disable-package-restore-in-visual-studio)seçeneklerine tabi olarak otomatik olarak gerçekleşir. NuGet 4.0+'da, SDK tarzı bir projede (genellikle .NET Core veya .NET Standard project) değişiklik yaptığınızda geri yükleme de otomatik olarak gerçekleşir.

1. **Araç** > **Seçenekleri** > **NuGet Paket Yöneticisi'ni**seçerek ve ardından Visual **Studio'da** Paket Geri **Yükleme**altında oluşturma sırasında eksik paketler için otomatik olarak kontrol seçeneğini seçerek otomatik paket geri yüklemesini etkinleştirin.

   SDK tarzı olmayan projelerde, otomatik geri yükleme seçeneğini etkinleştirmek için öncelikle **NuGet'in eksik paketleri indirmesine izin** verme seçeneğini seçmeniz gerekir.

1. Projeyi derleyin.

   Bir veya daha fazla tek tek paket hala düzgün yüklenmiyorsa, **Çözüm Gezgini** bir hata simgesi gösterir. NuGet **Paketlerini Yönet'e**sağ tıklayın ve seçin ve etkilenen paketleri kaldırmak ve yeniden yüklemek için **Paket Yöneticisi'ni** kullanın. Daha fazla bilgi için [paketleri yeniden yükle ve güncelleştir'e](../consume-packages/reinstalling-and-updating-packages.md) bakın

   "Bu proje, bu bilgisayarda eksik olan NuGet paketine(ler) başvurur" veya "Bir veya daha fazla NuGet paketinin geri yüklenmemesi gerekir, ancak onay verilmediği için olamaz" hatasını görürseniz, [otomatik geri yüklemeyi etkinleştirin.](#enable-and-disable-package-restore-in-visual-studio) Eski projeler için, [otomatik paket geri yüklemesine geçir'e](#migrate-to-automatic-package-restore-visual-studio)de bakın. Ayrıca [bkz.](Package-restore-troubleshooting.md)

### <a name="restore-packages-manually-using-visual-studio"></a>Visual Studio'u kullanarak paketleri el ile geri yükleme

1. **Araç** > **Seçenekleri** > **NuGet Paket Yöneticisi'ni**seçerek paket geri yüklemeyi etkinleştirin. **Paket Geri Yükleme** seçenekleri altında, eksik paketleri indirmek için **NuGet'e İzin**Ver'i'yi seçin.

1. **Solution**Explorer'da, çözüme sağ tıklayın ve **NuGet Paketlerini Geri Yükle'yi**seçin.

   Bir veya daha fazla tek tek paket hala düzgün yüklenmiyorsa, **Çözüm Gezgini** bir hata simgesi gösterir. NuGet **Paketlerini Yönet'e**sağ tıklayın ve seçin ve etkilenen paketleri kaldırmak ve yeniden yüklemek için **Paket Yöneticisi'ni** kullanın. Daha fazla bilgi için [paketleri yeniden yükle ve güncelleştir'e](../consume-packages/reinstalling-and-updating-packages.md) bakın

   "Bu proje, bu bilgisayarda eksik olan NuGet paketine(ler) başvurur" veya "Bir veya daha fazla NuGet paketinin geri yüklenmemesi gerekir, ancak onay verilmediği için olamaz" hatasını görürseniz, [otomatik geri yüklemeyi etkinleştirin.](#enable-and-disable-package-restore-in-visual-studio) Eski projeler için, [otomatik paket geri yüklemesine geçir'e](#migrate-to-automatic-package-restore-visual-studio)de bakın. Ayrıca [bkz.](Package-restore-troubleshooting.md)

### <a name="enable-and-disable-package-restore-in-visual-studio"></a>Visual Studio'da paket geri yüklemesini etkinleştirme ve devre dışı

Visual Studio'da, **Öncelikle Araç** > **Seçenekleri** > **NuGet Paket Yöneticisi**aracılığıyla Paket Geri Yükleme kontrol:

![NuGet Paket Yöneticisi seçenekleri ile Kontrol Paketi Geri Yükleme](media/Restore-01-AutoRestoreOptions.png)

- **NuGet'in eksik paketleri indirmesine izin verin,** `packageRestore/enabled` `NuGet.Config` dosyanın geri yükleme `%AppData%\NuGet\` [bölümündeki,](../reference/nuget-config-file.md#packagerestore-section) Windows'da `~/.nuget/NuGet/` veya Mac/Linux'ta ayarını değiştirerek tüm paket geri yükleme biçimlerini kontrol edin. Bu ayar aynı zamanda Visual Studio'daki çözümün bağlam menüsünde **NuGet Paketlerini Geri Yükleme** komutunu da etkinleştiri.

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
  > `packageRestore/enabled` Ayarı genel olarak geçersiz kılmak için, Visual Studio'yu başlatmadan veya bir yapı başlatmadan önce ortam değişkeni **EnableNuGetPackageRestore'i** True veya False değeriyle ayarlayın.

- **Visual Studio'da yapı sırasında eksik paketleri otomatik** olarak `packageRestore/automatic` kontrol edin, dosyanın [paketGeri Yükleme bölümündeki](../reference/nuget-config-file.md#packagerestore-section) ayarı değiştirerek otomatik geri yükleme yi kontrol edin. `NuGet.Config` Bu seçenek True olarak ayarlandığında, Visual Studio'dan bir yapı yı çalıştırmak eksik paketleri otomatik olarak geri yükler. Bu ayar, MSBuild komut satırından çalıştırılatan yapıları etkilemez.

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

Bir geliştirici veya şirket, bir bilgisayardaki tüm kullanıcılar için Paket Geri Yükleme'yi `nuget.config` etkinleştirmek veya devre dışı katmak için yapılandırma ayarlarını genel dosyaya ekleyebilir. Genel `nuget.config` `%ProgramData%\NuGet\Config`windows, bazen belirli `\{IDE}\{Version}\{SKU}\` bir Visual Studio klasörü altında, `~/.local/share`ya da Mac / Linux at . Tek tek kullanıcılar daha sonra proje düzeyinde gerektiğinde geri yüklemeyi seçik olarak etkinleştirebilir. NuGet'in birden çok config dosyaya nasıl öncelik verebildiği hakkında daha fazla bilgi için [Ortak NuGet yapılandırmalarına](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)bakın.

> [!Important]
> `packageRestore` Ayarları doğrudan Görsel Studio'da `nuget.config`ayarlarsanız, **Seçenekler** iletişim kutusunun geçerli değerleri göstermesi için Visual Studio'yu yeniden başlatın.

### <a name="choose-default-package-management-format"></a>Varsayılan paket yönetim biçimini seçin

![NuGet Package Manager seçeneklerine rağmen varsayılan paket yönetim biçimini denetleme](media/Restore-02-PackageFormatOptions.png)

NuGet,bir projenin paketleri kullanabileceği iki biçimi [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)vardır: ve . Varsayılan **biçim, Paket Yönetimi** başlığı altındaki açılır yerden seçilebilir. Projede ilk paket yüklendiğinde istenecek bir seçenek de kullanılabilir.

> [!Note]
> Bir proje her iki paket yönetim biçimini de desteklemiyorsa, kullanılan paket yönetim biçimi projeyle uyumlu olan biçim olur ve bu nedenle seçeneklerdeki varsayılan küme olmayabilir. Ayrıca, seçenekler penceresinde seçenek seçilse bile NuGet ilk paket yüklemesinde seçim istenmez.
>
> Paket Yöneticisi Konsolu bir projede ilk paketi yüklemek için kullanılırsa, seçenek seçenekler penceresinde seçilse bile NuGet biçim seçimi için istenmez.

## <a name="restore-using-the-dotnet-cli"></a>dotnet CLI kullanarak geri yükleme

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> Proje dosyasına eksik bir paket başvurusu eklemek için, komutu da `restore` çalıştıran [dotnet ekle paketini](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)kullanın.

## <a name="restore-using-the-nugetexe-cli"></a>nuget.exe CLI kullanarak geri yükleme

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> Komut, `restore`proje dosyasını veya *packages.config'i*değiştirmez. Bağımlılık eklemek için Visual Studio'daki Paket Yöneticisi UI veya Console üzerinden paket ekleyin veya *packages.config'i* değiştirin ve sonra ya da `install` `restore`çalıştırın.

## <a name="restore-using-msbuild"></a>MSBuild kullanarak geri yükleme

PackageReference ile proje dosyasında listelenen paketleri geri yüklemek için [msbuild -t:geri yükleme](../reference/msbuild-targets.md#restore-target) komutunu kullanın. Bu komut yalnızca Visual Studio 2017 ve daha yüksek sürümlerle birlikte bulunan NuGet 4.x+ ve MSBuild 15.1+'da kullanılabilir. Her `nuget restore` `dotnet restore` ikisini de kullanın ve bu komutu geçerli projeler için kullanın.

1. Geliştirici komut istemini açın **(Arama** kutusunda **Geliştirici komut istemi**yazın).

   MSBuild için gerekli tüm yollarla yapılandırılacak gibi, genellikle Görsel Stüdyo için Geliştirici Komut Komut Ustem komutunu **Başlat** menüsünden başlatmak istersiniz.

2. Proje dosyasını içeren klasöre geçin ve aşağıdaki komutu yazın.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. Projeyi yeniden oluşturmak için aşağıdaki komutu yazın.

   ```cmd
   msbuild
   ```

   MSBuild çıktısının yapının başarıyla tamamlandığını gösterdiğinden emin olun.

## <a name="restore-using-azure-pipelines"></a>Azure Ardışık Düzenlerini Kullanarak Geri Yükleme

Azure Ardışık Düzenler'de bir yapı tanımı oluşturduğunuzda, herhangi bir yapı görevinden önce nuget [geri yükleme](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) sini veya .NET Core [geri yükleme](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) görevini tanıma ekleyin. Bazı yapı şablonları varsayılan olarak geri yükleme görevini içerir.

## <a name="restore-using-azure-devops-server"></a>Azure DevOps Server'ı kullanarak geri yükleme

Azure DevOps Server ve TFS 2013 ve daha sonra bir TFS 2013 veya daha sonra Team Build şablonu kullanıyorsanız, yapı sırasında paketleri otomatik olarak geri yükleyin. Önceki TFS sürümleri için, komut satırı geri yükleme seçeneğini çalıştırmak için bir yapı adımı ekleyebilir veya isteğe bağlı olarak yapı şablonunu daha sonraki bir sürüme geçirebilirsiniz. Daha fazla bilgi için [bkz.](../consume-packages/team-foundation-build.md)

## <a name="constrain-package-versions-with-restore"></a>Paket sürümlerini geri yüklemeyle sınırlandırın

NuGet paketleri herhangi bir yöntemle geri yüklediğinde, belirttiğiniz kısıtlamaları `packages.config` veya proje dosyasını onurlandırar:

- , `packages.config`bağımlılık özelliğinde `allowedVersion` bir sürüm aralığı belirtebilirsiniz. Daha fazla bilgi için [Kısıtlama yükseltme sürümlerine](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) bakın. Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Proje dosyasında, bir bağımlılık aralığını doğrudan belirtmek için PackageReference'ı kullanabilirsiniz. Örneğin:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, [Paket sürümünde](../concepts/package-versioning.md)açıklanan gösterimi kullanın.

## <a name="force-restore-from-package-sources"></a>Paket kaynaklarından güç geri yüklemesi

Varsayılan olarak, NuGet geri yükleme *işlemleri, genel paketleri* ve [önbellek klasörlerini yönet'te](managing-the-global-packages-and-cache-folders.md)açıklanan genel paketlerden ve *http-cache* klasörlerinden gelen paketleri kullanır.

*Genel paketler* klasörünü kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- Klasörü kullanarak `nuget locals global-packages -clear` `dotnet nuget locals global-packages --clear`temizleyin veya .
- Aşağıdaki yöntemlerden birini kullanarak, geri yükleme işleminden önce *genel paketler* klasörünün konumunu geçici olarak değiştirin:
  - NUGET_PACKAGES ortamı değişkenini farklı bir klasöre ayarlayın.
  - (PackageReference `NuGet.Config` kullanıyorsanız) veya `globalPackagesFolder` `repositoryPath` (kullanıyorsanız) `packages.config`farklı bir klasöre ayarlayan bir dosya oluşturun. Daha fazla bilgi için [yapılandırma ayarlarına](../reference/nuget-config-file.md#config-section)bakın.
  - Yalnızca MSBuild: Özelliği yle `RestorePackagesPath` birlikte farklı bir klasör belirtin.

HTTP kaynakları için önbelleği kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- `-NoCache` Seçeneği , `nuget restore`'' ile veya ' ile `--no-cache` `dotnet restore`seçeneğini kullanın. Bu seçenekler Visual Studio Package Manager veya konsol aracılığıyla geri yükleme işlemlerini etkilemez.
- Önbelleği kullanarak `nuget locals http-cache -clear` `dotnet nuget locals http-cache --clear`temizleyin veya.
- Geçici olarak NUGET_HTTP_CACHE_PATH ortamı değişkenini farklı bir klasöre ayarlayın.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Otomatik paket geri yüklemesine geçiş (Visual Studio)

NuGet 2.6 ve daha önceki ler için, MSBuild ile entegre edilmiş paket geri yüklemesi daha önce desteklenmiştir, ancak bu artık doğru değildir. (Genellikle Visual Studio'da bir çözüme sağ tıklayarak ve **NuGet Paket Geri Yüklemesini Etkinleştir'i**seçerek etkinleştirildi). Projeniz, amortismana kalanmis MSBuild tümleşik paket geri yüklemesini kullanıyorsa, lütfen otomatik paket geri yüklemesine geçirin.

MSBuild-Integrated paketi geri yükleme kullanan projeler genellikle üç dosyaiçeren bir *.nuget* klasörü içerir: *NuGet.config,* *nuget.exe*ve *NuGet.targets.* *NuGet.targets* dosyasının varlığı, NuGet'in MSBuild'e uygun olmayan yaklaşımı kullanmaya devam edip etmeyeceğini belirler, bu nedenle bu dosya geçiş sırasında kaldırılmalıdır.

Otomatik paket geri yüklemesine geçiş yapmak için:

1. Visual Studio’yu kapatın.
2. *Sil .nuget/nuget.exe* ve *.nuget/NuGet.targets*.
3. Her proje dosyası için `<RestorePackages>` öğeyi kaldırın ve *NuGet.targets'a*yapılan tüm başvuruları kaldırın.

Otomatik paket geri yüklemesini test etmek için:

1. *Paketler* klasörünü çözümden kaldırın.
2. Visual Studio'da çözümü açın ve bir yapı başlatın.

   Otomatik paket geri yükleme, her bağımlılık paketini kaynak denetimine eklemeden karşıdan yüklemeli ve yüklemelidir.

## <a name="troubleshooting"></a>Sorun giderme

[Bkz. Sorun Giderme paketi geri yükleme.](package-restore-troubleshooting.md)
