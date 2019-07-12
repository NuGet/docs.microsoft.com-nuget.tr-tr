---
title: NuGet paket geri yükleme
description: Genel Bakış nasıl NuGet geri yükleme paketleri bir proje üzerinde geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil olmak üzere bağlıdır.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: e85d8cc3fd9492118bd8f34cfd05f20a9724c281
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842347"
---
# <a name="package-restore-options"></a>Paket geri yükleme seçenekleri

Temiz bir geliştirme ortamı yükseltmek ve NuGet depo boyutunu küçültmek için **paketi geri yüklemeyi** tümünü ya da proje dosyasında listelenen bir proje bağımlılıklarınızı yükler veya `packages.config`. .NET Core 2.0 + `dotnet build` ve `dotnet run` komutları bir otomatik paket geri yükleme yapın. Visual Studio geri yükleyebilir, paketleri otomatik olarak bir proje oluşturur ve bu paketleri, Visual Studio ile dilediğiniz zaman geri yükleyebilirsiniz `nuget restore`, `dotnet restore`ve xbuild Mono üzerinde.

Paket geri yükleme kaynak denetiminde bunları depolamak zorunda kalmadan bir projenin tüm bağımlılıkları kullanılabilir olduğundan emin olur. Paketi ikili dosyaları hariç tutmak için kaynak denetimi deponuza yapılandırmak için bkz [paketleri ve kaynak denetimi](../consume-packages/packages-and-source-control.md). 

## <a name="package-restore-overview"></a>Paket geri yükleme genel bakış

Paket geri yükleme ilk gerektiği gibi bir proje doğrudan bağımlılıkları yükler ve ardından bu paket tüm bağımlılık grafiği boyunca tüm bağımlılıkları yükler.

Bir paket zaten yüklü değilse, NuGet ilk ondan almaya çalışır [önbellek](../consume-packages/managing-the-global-packages-and-cache-folders.md). NuGet paketi önbellekte değilse, paket listesinde etkinleştirilmiş tüm kaynaklardan gelen indirmeye çalışmadan **Araçları** > **seçenekleri** > **NuGet Paket Yöneticisi**   >  **Paket kaynakları** Visual Studio'da. Geri yükleme sırasında NuGet paket kaynaklarını sırasını yoksayar ve hangi kaynak gelen paketin ilk isteklerine yanıt vermek için kullanır. NuGet nasıl davranacağı hakkında daha fazla bilgi için bkz. [ortak NuGet yapılandırmaları](Configuring-NuGet-Behavior.md). 

> [!Note]
> NuGet tüm kaynakları doğrulayana kadar bir paket geri yükleme hatası göstermiyor. O anda NuGet yalnızca listedeki son kaynağı için bir hata bildirir. Hata paketi üzerinde bulunmamıştır gösterir *herhangi* diğer kaynaklardan olsa bile hata olmayan gösterilen görüntülerin her birini tek tek kaynakları için.

## <a name="restore-packages"></a>Paketleri geri yükle

Paketi geri yüklemeyi aşağıdaki yollardan biriyle tetikleyebilirsiniz:

- **Visual Studio**: Windows üzerinde Visual Studio'da, aşağıdaki yöntemlerden birini kullanın.

    - Paketleri otomatik olarak geri yükleyin. Paket geri yükleme otomatik olarak gerçekleşir bir şablondan bir proje oluşturduğunuzda veya seçeneklerinde tabi bir projeyi derleme [etkinleştirme ve devre dışı paket geri yükleme](#enable-and-disable-package-restore-visual-studio). Nuget'te 4.0 +, geri yükleme de otomatik olarak (genellikle bir .NET Core veya .NET Standard projesi) SDK stilinde projeye değişiklikler yaptığınızda gerçekleşir.

    - Paketleri el ile geri yükleyin. El ile geri yüklemek için çözüme sağ **Çözüm Gezgini** seçip **NuGet paketlerini geri yükle**. Bir veya daha fazla tek paketler hala düzgün yüklü değilse **Çözüm Gezgini** bir hata simgesi gösterir. Sağ tıklayıp **NuGet paketlerini Yönet**ve **Paket Yöneticisi** kaldırıp yeniden etkilenen paketler. Daha fazla bilgi için [yeniden yükleme ve güncelleştirme paketleri](../consume-packages/reinstalling-and-updating-packages.md)

    Hata görürseniz "Bu proje, bu bilgisayarda eksik olan NuGet paket başvuruları" veya "bir veya daha fazla NuGet paketlerini geri yüklenmelidir ancak izin verilmedi olduğundan oluşturulamadı" [otomatik geri yükleme etkinleştirme](#enable-and-disable-package-restore-visual-studio). Ayrıca bkz [otomatik paket geri yükleme geçiş](#migrate-to-automatic-package-restore-visual-studio) ve [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

- **DotNet CLI**: Komut satırında, projenizi içeren klasöre geçin ve ardından [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) paketlerini geri yüklemek için komut listelenen ile proje dosyasında [PackageReference](../consume-packages/package-references-in-project-files.md). .NET Core 2.0 ve daha sonra geri yükleme otomatik olarak oluşur `dotnet build` ve `dotnet run` komutları.  

- **nuget.exe CLI**: Komut satırında, projenizi içeren klasöre geçin ve ardından [nuget geri yükleme](../tools/cli-ref-restore.md) paketlerini geri yüklemek için komutu, bir proje veya çözüm dosyası veya içinde listelenen `packages.config`. 

- **MSBuild**: Kullanım [msbuild - t: geri](../reference/msbuild-targets.md#restore-target) PackageReference proje dosyasıyla paketlerini geri yüklemek için komut listelenmektedir. Bu komut, yalnızca Visual Studio 2017 ve üzeri sürümleri dahildir NuGet 4.x+ ve 15.1 +, MSBuild içinde kullanılabilir. Her ikisi de `nuget restore` ve `dotnet restore` geçerli projeleri için bu komutu kullanın.

- **Azure işlem hatları**: Azure işlem hatlarında bir yapı tanımı oluşturduğunuzda, NuGet dahil [geri](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) veya .NET Core [geri](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) herhangi bir derleme görevleri önce tanımındaki görev. Bazı derleme şablonları, varsayılan olarak geri yükleme görev içerir.

- **Azure DevOps sunucusu**: Otomatik olarak TFS 2013 veya üzeri ekip şablonu kullanıyorsanız, paketleri oluşturma sırasında azure DevOps Server ve TFS 2013 ve üzeri sürümler geri. Önceki TFS sürümleri için bir komut satırı restore seçeneği çalıştırmayı bir derleme adımı dahil edebilir veya isteğe bağlı olarak derleme şablonu sonraki bir sürüme geçirin. Daha fazla bilgi için [Team Foundation Yapısı ile paket geri yükleme ayarlayın](../consume-packages/team-foundation-build.md).

## <a name="enable-and-disable-package-restore-visual-studio"></a>Enable ve disable paket geri yükleme (Visual Studio)

Visual Studio'da paket geri yükleme öncelikle ile denetim **Araçları** > **seçenekleri** > **NuGet Paket Yöneticisi**:

![Denetim paketi geri yüklemeyi NuGet Paket Yöneticisi seçenekleri](media/Restore-01-AutoRestoreOptions.png)

- **Eksik paketleri indirmek NuGet izin** değiştirerek paket geri yükleme, tüm form denetimleri `packageRestore/enabled` ayarı [packageRestore bölümü](../reference/nuget-config-file.md#packagerestore-section) , `NuGet.Config` dosyası konumundaki `%AppData%\NuGet\` Windows, şirket veya `~/.nuget/NuGet/` Mac/Linux üzerinde. Bu ayar, ayrıca etkinleştirir **NuGet paketlerini geri yükle** Visual Studio'da çözüme ilişkin bağlam menüsünde komutu.

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
  > Genel olarak geçersiz kılmak için `packageRestore/enabled` ayarı ortam değişkenini ayarlamak **EnableNuGetPackageRestore** True ya da Visual Studio başlatma veya bir yapı başlatmadan önce False değerine sahip.

- **Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle** değiştirerek otomatik geri yükleme denetimleri `packageRestore/automatic` ayarı [packageRestore bölümü](../reference/nuget-config-file.md#packagerestore-section) , `NuGet.Config` dosya. Bu seçeneği True olarak ayarlandığında, bir derleme Visual Studio'dan otomatik olarak çalıştırarak tüm eksik paketleri geri yükler. Bu ayar, yapı MSBuild komut satırından çalıştırmak etkilemez.

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

Etkinleştirmek veya devre dışı bir bilgisayardaki tüm kullanıcılar için paket geri yükleme, bir geliştirici ya da şirket yapılandırma ayarlarını genel ekleyebilirsiniz `nuget.config` dosya. Genel `nuget.config` Windows içinde `%ProgramData%\NuGet\Config`, bazen belirli bir altında `\{IDE}\{Version}\{SKU}\` Visual Studio klasörünü veya Mac/Linux `~/.local/share`. Bireysel kullanıcılar ardından seçerek geri yükleme bir proje düzeyinde gerektiği şekilde etkinleştirebilirsiniz. NuGet'ın birden çok yapılandırma dosyalarına nasıl önceliklendirdiğini hakkında ayrıntılı bilgi için bkz: [ortak NuGet yapılandırmaları](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

> [!Important]
> Düzenlediyseniz `packageRestore` ayarları doğrudan `nuget.config`, Visual Studio'yu yeniden başlatmanız böylece **seçenekleri** iletişim kutusu geçerli değerleri gösterir.

## <a name="constrain-package-versions-with-restore"></a>Paket sürümlerini geri yükleme ile sınırlama

NuGet paketleri herhangi bir yöntem geri yüklerse, belirttiğiniz kısıtlamalardan geliştirir. `packages.config` ya da proje dosyası:

- İçinde `packages.config`, bir sürüm aralığı içinde belirttiğiniz `allowedVersion` bağımlılık özelliği. Bkz: [sınırla yükseltme sürümlerinin](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) daha fazla bilgi için. Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Bir proje dosyasında PackageReference doğrudan bir bağımlılık 's aralığını belirtmek için kullanabilirsiniz. Örneğin:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, açıklanan gösterimi kullanan [Paket sürümü oluşturma](../reference/package-versioning.md).

## <a name="force-restore-from-package-sources"></a>Paket kaynaklarını zorla geri yükleme

Varsayılan olarak NuGet geri yükleme işlemleri paketlerden kullanın *genel paketleri* ve *http önbellek* anlatılan klasörleri [genel paketleri yönetin ve önbellek klasörleri](managing-the-global-packages-and-cache-folders.md).

Kullanmaktan kaçınmak için *genel paketleri* klasörü, aşağıdakilerden birini yapın:

- Klasörü kullanılarak Temizle `nuget locals global-packages -clear` veya `dotnet nuget locals global-packages --clear`.
- Geçici olarak konumunu değiştirmek *genel paketleri* aşağıdaki yöntemlerden birini kullanarak geri yükleme işlemi önce klasörü:
  - Farklı bir klasöre NUGET_PACKAGES ortam değişkenini ayarlayın.
  - Oluşturma bir `NuGet.Config` ayarlar dosyası `globalPackagesFolder` (PackageReference kullanıyorsanız) veya `repositoryPath` (kullanıyorsanız `packages.config`) farklı bir klasöre. Daha fazla bilgi için [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section).
  - Yalnızca MSBuild: İle farklı bir klasör belirtmek `RestorePackagesPath` özelliği.

Önbellek için HTTP kaynakları kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- Kullanım `-NoCache` seçeneğini `nuget restore`, veya `--no-cache` seçeneğini `dotnet restore`. Bu seçenekler, Visual Studio Paket Yöneticisi aracılığıyla geri yükleme işlemlerini etkilemediğinden veya konsol kullanmayın.
- Önbellek kullanarak Temizle `nuget locals http-cache -clear` veya `dotnet nuget locals http-cache --clear`.
- Geçici olarak farklı bir klasöre NUGET_HTTP_CACHE_PATH ortam değişkenini ayarlar.

## <a name="migrate-to-automatic-package-restore-visual-studio"></a>Otomatik paket geri yükleme (Visual Studio) geçirme

NuGet 2.6 ve önceki sürümlerinde, bir MSBuild tümleşik paket geri yükleme daha önce desteklenen ancak, artık geçerli değildir. (Visual Studio çözümünde sağ tıklatıp seçerek genellikle etkinleştirildi **NuGet paketi geri yüklemeyi etkinleştir**). Projeniz kullanım dışı MSBuild tümleşik paket geri yükleme kullanıyorsa, lütfen otomatik paket geri yükleme için geçirin.

MSBuild ile tümleşik paket geri yükleme genellikle kullanan projeleri içeren bir *.nuget* üç dosyayı içeren klasörü: *NuGet.config*, *nuget.exe*, ve *NuGet.targets*. Varlığı bir *NuGet.targets* dosya NuGet MSBuild untegrated yaklaşım bu dosya geçiş sırasında kaldırılacak şekilde kullanmaya devam edip etmeyeceğini belirler.

Otomatik paket geri yükleme için geçirmek için:

1. Visual Studio’yu kapatın.
2. Silme *.nuget/nuget.exe* ve *.nuget/NuGet.targets*.
3. Her proje dosyası için kaldırma `<RestorePackages>` öğesi ve tüm başvuru kaldırma *NuGet.targets*.

Otomatik paket geri yüklemeyi test etmek için:

1. Kaldırma *paketleri* çözüm klasöründen.
2. Visual Studio içinde çözümü açın ve bir derleme başlatın.

   Otomatik paket geri yükleme, indirin ve kaynak denetimine eklemeden her bağımlılık paketini yükleyin.

## <a name="troubleshooting"></a>Sorun giderme

Bkz: [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).
