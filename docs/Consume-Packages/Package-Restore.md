---
title: "NuGet paket geri yüklemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Nasıl NuGet bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil bağlı olan paketler geri yükleyen bir genel bakış."
keywords: "NuGet paket geri yüklemesi, NuGet paket yükleme paketini, paketleri, bağımlılık sürümleri otomatik geri yükleme, devre dışı bırakma, geri yükleme, paket sürümlerinin sınırlama"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a>Paket geri yüklemesi

Temizleyici bir geliştirme ortamı yükseltmek için ve havuz boyutu, NuGet azaltmak için **paketi geri yüklemesi** proje oluşturulmadan önce tüm başvurulmuş paketleri yükler. Yaygın olarak kullanılan bu özellik&mdash;Visual Studio, .NET Core 2.0 + ve xbuild Mono üzerinde kullanılabilir&mdash;kaynak denetiminde depolanması için bu paketleri gerek kalmadan tüm bağımlılıkları projede kullanılabilir olmasını sağlar (bkz: [ Paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) paket ikili dosyaları hariç tutulacak deponuza yapılandırma). Herhangi bir zamanda paketleri de el ile geri yükleyebilirsiniz.

Yapı sunucuları paket geri yükleme hakkında daha fazla ayrıntı için bkz: [TFBuild ile paket geri yükleme](../consume-packages/team-foundation-build.md).

## <a name="package-restore-overview"></a>Paket geri yükleme genel bakış

Paketleri geri ilk proje doğrudan bağımlılıklarını, tüm bağımlılık grafiğinin boyunca bu paketlerin bağımlılıkları yükleme gerektiğinde yükler.

Bir paket zaten yüklü değilse, NuGet ilk ondan almaya çalışır [önbellek](../consume-packages/managing-the-nuget-cache.md). Paketi önbellekte değil NuGet sonra indirin (ve önbelleğe) paket tüm etkin kaynaklardan çalışır (bkz [NuGet yapılandırma davranışı](Configuring-NuGet-Behavior.md)); kaynakları da görüntülenir **Araçlar > Seçenekler > NuGet paketi Yöneticisi > paket kaynaklarını** Visual Studio listesinde). NuGet paket kaynaklarını sırasını isteklerini yanıtlamak için hangi kaynak olan gelen paket ilk kullanarak yok sayar.

> [!Note]
> NuGet tüm kaynakları doğrulayana kadar bir paket geri yükleme hatası göstermez. O anda NuGet yalnızca listedeki son kaynağı için hata bildirir. Paket mevcut değildi hata gösterir *herhangi* diğer kaynaklardan rağmen hataları gösterilmiyor görüntülerin her birini ayrı ayrı kaynakları için.

Paket geri yüklemesi, aşağıdaki yollarla tetiklenir:

- **DotNet CLI**: kullanmak [dotnet geri yükleme](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)). .NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak yapılır `dotnet build` ve `dotnet run`.

- **Paket Yöneticisi kullanıcı Arabirimi (Windows için Visual Studio)**: paketler geri yüklenir otomatik olarak bir şablondan bir proje oluşturma ve proje oluşturma (açıklanan seçeneği tabi [etkinleştirme ve paket devre dışı bırakmageriyükleme](#enabling-and-disabling-package-restore)). NuGet içinde 4.0 +, geri yükleme de otomatik olarak .NET Core SDK tabanlı bir projeye yapılan bir değişiklik olduğunda gerçekleşir.

    El ile geri yüklemek için Çözüm Gezgini'ndeki çözüme sağ tıklayın ve seçin **NuGet paketleri geri**. Bir veya daha fazla tek tek paket olması durumunda düzgün yüklenmemiş hala (yani Çözüm Gezgini bir hata simgesi gösterir), sonra kullanım etkilenen paketler kaldırıp için Paket Yöneticisi kullanıcı Arabirimi. Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md)

    "Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru" hatayı görmek veya "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı" başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme Aç [Etkinleştirme ve paket geri yüklemesi devre dışı bırakma](#enabling-and-disabling-package-restore).

- **NuGet CLI**: kullanmak [nuget restore](../tools/cli-ref-restore.md) proje dosyasında listelenen paketler geri yükler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)) veya bir [packages.config](../reference/packages-config.md) dosya. Çözüm dosyası da belirtebilirsiniz.

- **MSBuild**: kullanmak [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) , hangi geri yüklemeler paketler proje dosyasında listelenen paketler komutu (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)). Yalnızca Visual Studio 2017 ile birlikte NuGet 4.x+ ve MSBuild 15.1 + kullanılabilir. `nuget restore` ve `dotnet restore` her ikisi de geçerli projeleri için bu komutu kullanın.

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

Bazı durumlarda, bir geliştirici veya şirket etkinleştirmek veya bir bilgisayardaki tüm kullanıcılar için paket geri yüklemesi devre dışı bırakmak isteyebilirsiniz. Bu bulunan genel NuGet yapılandırma dosyasını yukarıdaki aynı ayarları ekleyerek yapılır `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Tek tek kullanıcılar sonra seçerek geri yükleme üzerinde proje düzeyi gerektiği şekilde etkinleştirebilirsiniz. Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyaları nasıl önceliklendirir ilgili tam ayrıntılar.

## <a name="constraining-package-versions-with-restore"></a>Geri yükleme ile kısıtlayan paketi sürümleri

Herhangi bir yöntemini paketleri geri yükleniyor, NuGet belirtilen kısıtlamalar yapılırken `packages.config` veya proje dosyası:

- `packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği. Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- PackageReference: doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin. Örneğin:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md).

## <a name="troubleshooting"></a>Sorun giderme

Bkz: [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).