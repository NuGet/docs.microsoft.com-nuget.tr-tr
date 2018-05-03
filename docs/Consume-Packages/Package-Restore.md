---
title: NuGet paket geri yüklemesi
description: Nasıl NuGet bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil bağlı olan paketler geri yükleyen bir genel bakış.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 6a8a2f1c5ced956f18b623f112756cdd2fab22f5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="package-restore"></a>Paket geri yüklemesi

Temizleyici bir geliştirme ortamı yükseltmek için ve havuz boyutu, NuGet azaltmak için **paket geri yükleme** ya da proje dosyası listelendiği gibi bir projenin tüm bağımlılıkları yükler veya `packages.config`. Visual Studio Proje yapılandırıldığında paketleri otomatik olarak geri yükleyebilirsiniz. `dotnet build` Ve `dotnet run` komutları (.NET Core 2.0 +) de otomatik bir geri yükleme işlemini gerçekleştirin. Ayrıca paketleri Visual Studio aracılığıyla herhangi bir zamanda geri yükleyebilirsiniz `nuget restore`, `dotnet restore`ve xbuild Mono üzerinde.

Paket geri yüklemesi kaynak denetiminde bu paketleri depolamadan bir projenin tüm bağımlılıkları kullanılabilir olduğundan emin olur. Bkz: [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) paket ikili dosyaları hariç tutulacak deponuza yapılandırma.

## <a name="package-restore-overview"></a>Paket geri yükleme genel bakış

Paketleri geri ilk gerektiği gibi bir proje doğrudan bağımlılıkları yükler ve sonra tüm bağımlılık grafiğinin boyunca bu paketlerin bağımlılıkları yükler.

Bir paket zaten yüklü değilse, NuGet ilk ondan almaya çalışır [önbellek](../consume-packages/managing-the-global-packages-and-cache-folders.md). Paket önbellekte değilse, NuGet daha sonra tüm etkin kaynaklardan paketini indirmek çalışır (bkz [NuGet yapılandırma davranışı](Configuring-NuGet-Behavior.md); kaynakları da görüntülenir **Araçlar > Seçenekler > NuGet Paket Yöneticisi > Paket kaynaklarını** Visual Studio listesinde). Geri yükleme sırasında hangi kaynağı gelen paket isteklerini yanıtlamak için ilk kullanarak NuGet paket kaynaklarını sırasını yoksayar.

> [!Note]
> NuGet tüm kaynakları doğrulayana kadar bir paket geri yükleme hatası göstermez. O anda NuGet yalnızca listedeki son kaynağı için bir hata bildirir. Paket mevcut değildi hata gösterir *herhangi* diğer kaynaklardan rağmen hataları gösterilmiyor görüntülerin her birini ayrı ayrı kaynakları için.

Paket geri yüklemesi, aşağıdaki yollarla tetiklenir:

- **DotNet CLI**: kullanmak [dotnet geri yükleme](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)). .NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak yapılır `dotnet build` ve `dotnet run`.

- **Paket Yöneticisi kullanıcı Arabirimi (Windows için Visual Studio)**: paketler geri yüklenir otomatik olarak bir şablondan bir proje oluşturma ve proje oluşturma (açıklanan seçeneği tabi [etkinleştirme ve paket devre dışı bırakmageriyükleme](#enabling-and-disabling-package-restore)). NuGet içinde 4.0 +, geri yükleme de otomatik olarak .NET Core SDK tabanlı bir projeye yapılan bir değişiklik olduğunda gerçekleşir.

    El ile geri yüklemek için Çözüm Gezgini'ndeki çözüme sağ tıklayın ve seçin **NuGet paketleri geri**. Bir veya daha fazla tek tek paket olması durumunda düzgün yüklenmemiş hala (yani Çözüm Gezgini bir hata simgesi gösterir), sonra kullanım etkilenen paketler kaldırıp için Paket Yöneticisi kullanıcı Arabirimi. Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md)

    "Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru" hatayı görmek veya "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı" başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme Aç [Etkinleştirme ve paket geri yüklemesi devre dışı bırakma](#enabling-and-disabling-package-restore). Ayrıca bkz. [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

- **NuGet CLI**: kullanmak [nuget restore](../tools/cli-ref-restore.md) proje dosyası veya içinde listelenen paketler geri yükler komutu `packages.config`. Çözüm dosyası da belirtebilirsiniz.

- **MSBuild**: kullanmak [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) , hangi geri yükler (yalnızca PackageReference) proje dosyasında listelenen paketler paketleri komutu. Yalnızca Visual Studio 2017 ile birlikte NuGet 4.x+ ve MSBuild 15.1 + kullanılabilir. `nuget restore` ve `dotnet restore` her ikisi de geçerli projeleri için bu komutu kullanın.

- **Visual Studio Team Services**: bir derleme tanımınız Team Services oluştururken dahil [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) veya [.NET Core geri](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) herhangi bir görev oluşturmadan önce tanımında görev. Bu görev varsayılan derleme şablonları sayısı olarak dahil edilir.

- **Team Foundation Server**: TFS 2013 ve üzeri sürümler otomatik olarak yükler paketler derleme sırasında koşuluyla yapı TFS 2013 veya üzeri Team şablonu kullanıyorsanız. TFS önceki sürümü için yukarıdaki komut satırı geri yükleme seçeneklerinden birini çağırmak için bir derleme adımı içerebilir. İsteğe bağlı olarak, TFS 2013 için derleme şablonu geçirebilirsiniz. Daha fazla bilgi için bkz: [paket geri yüklemesi izlenecek Team Foundation Build ile](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Paket geri yüklemesi devre dışı bırakma ve etkinleştirme

Paket geri yüklemesi aracılığıyla etkin öncelikle **Araçlar > Seçenekler > NuGet Paket Yöneticisi** Visual Studio'da:

![Paket geri yükleme davranışları NuGet Paket Yöneticisi seçeneklerle denetleme](media/Restore-01-AutoRestoreOptions.png)

- **Nuget'in eksik paketleri indirmesine izin ver**: değiştirerek denetimleri paket geri yükleme tüm forms `packageRestore/enabled` ayarı `NuGet.Config` aşağıda gösterildiği gibi dosya (`%AppData%\NuGet\NuGet.Config` , Windows'da `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta). Visual Studio'da bu ayarı sağlar **NuGet paketleri geri** çalışmak için çözümün bağlam menüsünde komutu.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  `packageRestore/enabled` Ayarını geçersiz kılındı genel olarak adlandırılan bir ortam değişkeni ayarlayarak **EnableNuGetPackageRestore** doğru veya yanlış Visual Studio başlatılıyor veya bir yapı başlatmadan önce bir değere sahip.

- **Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**: değiştirerek otomatik geri yükleme denetimleri `packageRestore/automatic` ayarı `NuGet.Config` aşağıda gösterildiği gibi dosya (`%AppData%\NuGet\NuGet.Config` , Windows'da `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta). Bu seçenek ayarlandığında, bir derleme Visual Studio'dan otomatik olarak çalıştırarak herhangi eksik paketleri geri yükler. Seçenek MSBuild kullanarak komut satırından çalıştırma derlemeleri etkilemez.

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

Başvuru için bkz: [NuGet yapılandırma dosyası - packageRestore bölüm](../reference/nuget-config-file.md#packagerestore-section).

Bazı durumlarda, bir geliştirici veya şirket etkinleştirmek veya bir bilgisayardaki tüm kullanıcılar için paket geri yüklemesi devre dışı bırakmak isteyebilirsiniz. Bunu yapmak için yukarıdaki aynı ayarları bulunan genel NuGet yapılandırma dosyasına ekleyin `%ProgramData%\NuGet\Config` (büyük olasılıkla altında belirli bir Windows `\{IDE}\{Version}\{SKU}\` klasörü Visual Studio için) veya `~/.local/share` (Mac/Linux). Tek tek kullanıcılar sonra seçerek geri yükleme üzerinde proje düzeyi gerektiği şekilde etkinleştirebilirsiniz. Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyaları nasıl önceliklendirir ilgili tam ayrıntılar.

> [!Important]
> Düzenlediyseniz `packageRestore` ayarlarını doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir böylece Visual Studio'yu yeniden başlatın.

## <a name="constraining-package-versions-with-restore"></a>Geri yükleme ile kısıtlayan paketi sürümleri

Herhangi bir yöntemini paketleri geri yükleniyor, NuGet belirtilen kısıtlamalar yapılırken `packages.config` veya proje dosyası:

- `packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği. Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Proje dosyası (PackageReference): doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin. Örneğin:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Geri yükleme paketini kaynaklardan zorlama

Varsayılan olarak, NuGet geri yükleme işlemlerini paketlerinden kullanmak *paketleri genel* ve *http önbellek* üzerinde açıklanan klasörleri [önbellek klasörvegenelpaketleriniyönetme](managing-the-global-packages-and-cache-folders.md).

Kullanmaktan kaçınmak için *paketleri genel* klasörü, aşağıdakilerden birini yapın:

- Klasörü kullanılarak temizleyin `nuget locals global-packages -clear` veya `dotnet nuget locals global-packages --clear`
- Geçici olarak konumunu değiştirmek *paketleri genel* aşağıdaki yöntemlerden birini kullanarak geri yükleme işlemi önce klasörü:
  - NUGET_PACKAGES ortam değişkeni başka bir klasöre ayarlayın.
  - Oluşturma bir `NuGet.Config` ayarlar dosyası `globalPackagesFolder` (PackageReference kullanıyorsanız) veya `repositoryPath` (kullanıyorsanız `packages.config`) farklı bir klasöre (bkz [yapılandırma ayarları](../reference/nuget-config-file.md#config-section)
  - MSBuild yalnızca: ile farklı bir klasör belirtmek `RestorePackagesPath` özelliği.

HTTP kaynakları için önbellek kullanımını önlemek için aşağıdakilerden birini yapın:

- Kullanım `-NoCache` seçeneğini `nuget restore` veya `--no-cache` seçeneğini `dotnet restore`. Bu seçenekler Visual Studio Paket Yöneticisi kullanıcı Arabirimi veya Konsolu aracılığıyla geri yükleme işlemlerini etkilemez.
- Önbelleği kullanılarak temizleyin `nuget locals http-cache -clear` veya `dotnet nuget locals http-cache --clear`.
- Geçici olarak başka bir klasöre NUGET_HTTP_CACHE_PATH ortam değişkeninin ayarlayın.

## <a name="troubleshooting"></a>Sorun giderme

Bkz: [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).