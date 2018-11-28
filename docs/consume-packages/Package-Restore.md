---
title: NuGet paket geri yükleme
description: NuGet paketleri bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil olmak üzere bağımlı olduğu nasıl geri yükler, bir genel bakış.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9acb87a5f5731fb33c91a1ae9b106c6df492ddcd
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453539"
---
# <a name="package-restore"></a>Paket geri yükleme

Temiz bir geliştirme ortamı yükseltmek ve NuGet depo boyutunu küçültmek için **paketi geri yüklemeyi** ya da proje dosyası listelendiği gibi bir projenin tüm bağımlılıkları yükler veya `packages.config`. Visual Studio bir proje derlenirken paketleri otomatik olarak geri yükleyebilirsiniz. `dotnet build` Ve `dotnet run` komutları (.NET Core 2.0 +), ayrıca otomatik bir geri yükleme gerçekleştirin. Ayrıca paketleri, Visual Studio ile dilediğiniz zaman geri yükleyebilirsiniz `nuget restore`, `dotnet restore`ve xbuild Mono üzerinde.

Paket geri yükleme kaynak denetiminde bu paketleri depolamadan bir projenin tüm bağımlılıkları kullanılabilir olduğundan emin olur. Bkz: [paketleri ve kaynak denetimi](../consume-packages/packages-and-source-control.md) nasıl paketi ikili dosyaları hariç tutmak için deponuzu yapılandırın.

## <a name="package-restore-overview"></a>Paket geri yükleme genel bakış

Paketler geri yükleniyor ilk gerektiği gibi bir proje doğrudan bağımlılıkları yükler ve ardından bu paket tüm bağımlılık grafiği boyunca tüm bağımlılıkları yükler.

Bir paket zaten yüklü değilse, NuGet ilk ondan almaya çalışır [önbellek](../consume-packages/managing-the-global-packages-and-cache-folders.md). Paket önbellekte değilse, NuGet ardından etkinleştirilmiş tüm kaynaklardan gelen paketi indirmek çalışır (bkz [yapılandırma NuGet davranışını](Configuring-NuGet-Behavior.md); kaynakları da görünür **Araçlar > Seçenekler > NuGet Paket Yöneticisi > Paket kaynaklarını** Visual Studio'daki listesi). Geri yükleme sırasında NuGet isteklerine yanıt vermek için hangi kaynak gelen paketin ilk kullanarak paket kaynaklarını sırası yok sayar.

> [!Note]
> NuGet tüm kaynakları doğrulayana kadar bir paket geri yükleme başarısız olduğunu göstermez. O anda NuGet yalnızca listedeki son kaynağı için bir hata bildirir. Hata paketi üzerinde bulunmamıştır gösterir *herhangi* diğer kaynaklardan olsa bile hata gösterilmez görüntülerin her birini tek tek kaynakları için.

Paket geri yükleme, aşağıdaki yollarla tetiklenir:

- **DotNet CLI**: kullanın [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutu, proje dosyasında listelenen paketleri geri yükler (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)). .NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak gerçekleştirilir `dotnet build` ve `dotnet run`.

- **Paket Yöneticisi UI (Windows için Visual Studio)**: paketler geri yüklenir otomatik olarak bir şablondan bir proje oluştururken ve bir proje derlenirken (açıklanan seçeneği tabi [etkinleştirme ve devre dışı paketgeriyükleme](#enabling-and-disabling-package-restore)). Nuget'te 4.0 +, geri yükleme da otomatik olarak ne zaman .NET Core SDK tabanlı bir proje için değişiklikler yapılır.

    El ile geri yüklemek için Çözüm Gezgini'nde çözüme sağ tıklayıp **NuGet paketlerini geri yükle**. Bir veya daha fazla tek paketler varsa hala düzgün yüklenmemiş (yani, Çözüm Gezgini'nde bir hata simgesi gösterir) ve ardından Paket Yöneticisi UI kaldırıp yeniden etkilenen paketleri kullanın. Bkz: [Reinstalling ve paketler güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md)

    Hatayı görürsünüz "Bu proje, bu bilgisayarda eksik olan NuGet paket başvuruları" veya "bir veya daha fazla NuGet paketlerini geri yüklenmesi gereken ancak izin verilmedi olduğundan kaldırılamadı." başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme'yi açın [Etkinleştirme ve devre dışı paket geri yükleme](#enabling-and-disabling-package-restore). Ayrıca bkz: [paket geri yükleme sorunlarını giderme](Package-restore-troubleshooting.md).

- **NuGet CLI**: kullanın [nuget geri yükleme](../tools/cli-ref-restore.md) komutu, proje dosyası veya listelenen paketleri geri yükler `packages.config`. Bir çözüm dosyası da belirtebilirsiniz.

- **MSBuild**: kullanın [msbuild - t: geri](../reference/msbuild-targets.md#restore-target) , hangi geri yükleme paketleri (yalnızca PackageReference) proje dosyasında listelenen paketlerin komutu. Yalnızca Visual Studio 2017 ile içerdiği NuGet 4.x+ ve MSBuild 15.1 + kullanılabilir. `nuget restore` ve `dotnet restore` hem de geçerli projeleri için bu komutu kullanın.

- **Visual Studio Team Services**: Team Services üzerinde bir derleme tanımı oluşturma işlemlerinde [NuGet geri yükleme](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) veya [.NET Core geri](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) önce herhangi bir derleme görev tanımındaki görev. Bu görev varsayılan yapı şablonlarını bir dizi olarak dahil edilir.

- **Team Foundation Server**: TFS 2013 ve üzeri sürümler otomatik olarak yükler paketleri oluşturma sırasında derleme veya sonraki sürümler TFS 2013 için takım şablon kullanmakta olduğunuz koşuluyla. Önceki TFS sürümü için yukarıdaki komut satırı restore seçeneklerden birini çağırmak için bir derleme adımı içerebilir. İsteğe bağlı olarak, TFS 2013 yapı şablonu geçirebilirsiniz. Daha fazla bilgi için [Team Foundation Yapısı ile paket Geri Yükleme Kılavuzu](../consume-packages/team-foundation-build.md).

## <a name="enabling-and-disabling-package-restore"></a>Paket geri yükleme devre dışı bırakma ve etkinleştirme

Paket geri yükleme yoluyla etkin öncelikle **Araçlar > Seçenekler > NuGet Paket Yöneticisi** Visual Studio'daki:

![Paket geri yükleme davranışlarını NuGet Paket Yöneticisi seçenekleri aracılığıyla denetleme](media/Restore-01-AutoRestoreOptions.png)

- **Eksik paketleri indirmek NuGet izin**: değiştirerek paket geri yükleme, tüm form denetimleri `packageRestore/enabled` ayarı `NuGet.Config` aşağıda gösterildiği gibi dosya (`%AppData%\NuGet\NuGet.Config` , Windows üzerinde `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde). Visual Studio'da bu ayarı sağlar **NuGet paketlerini geri yükle** çalışmak için çözümün bağlam menüsünde komutu.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```

> [!Note]
>  `packageRestore/enabled` Ayarı geçersiz kılınabilir genel olarak adlandırılan bir ortam değişkenini ayarlayarak **EnableNuGetPackageRestore** TRUE ya da Visual Studio başlatma veya bir yapı başlatmadan önce FALSE değerine sahip.

- **Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**: değiştirerek otomatik geri yükleme denetimleri `packageRestore/automatic` ayarı `NuGet.Config` aşağıda gösterildiği gibi dosya (`%AppData%\NuGet\NuGet.Config` , Windows üzerinde `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde). Bu seçenek ayarlandığında, bir derleme Visual Studio'dan otomatik olarak çalıştırarak tüm eksik paketleri geri yükler. MSBuild kullanarak komut satırından çalıştırmak yapılar seçeneğini etkilemez.

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

Başvuru için bkz: [NuGet yapılandırma dosyası - packageRestore bölümü](../reference/nuget-config-file.md#packagerestore-section).

Bazı durumlarda, bir geliştirici ya da şirket, etkinleştirme veya devre dışı bir bilgisayardaki tüm kullanıcılar için paket geri yükleme isteyebilirsiniz. Bunu yapmak için yukarıdaki aynı ayarları bulunan genel NuGet yapılandırma dosyasını ekleme `%ProgramData%\NuGet\Config` (Windows, potansiyel olarak belirli bir altında `\{IDE}\{Version}\{SKU}\` Visual Studio için klasör) veya `~/.local/share` (Mac/Linux). Bireysel kullanıcılar ardından seçerek geri yükleme bir proje düzeyinde gerektiği şekilde etkinleştirebilirsiniz. Bkz: [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyalarına nasıl önceliklendirdiğini hakkında tam Ayrıntılar için.

> [!Important]
> Düzenlediyseniz `packageRestore` ayarları doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir, böylece Visual Studio'yu yeniden başlatın.

## <a name="constraining-package-versions-with-restore"></a>Geri yükleme ile kısıtlayan paket sürümleri

Herhangi bir yöntem paketleri geri yüklerken, NuGet belirtilen kısıtlamalardan oms'deki `packages.config` ya da proje dosyası:

- `packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği. Bkz: [Reinstalling ve paketlerin güncelleştirilmesi](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- Proje dosyası (PackageReference): doğrudan bağımlılık'ın sürüm numarasına sahip bir sürüm aralığı belirtin. Örneğin:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

Her durumda, açıklanan gösterimi kullanan [Paket sürümü oluşturma](../reference/package-versioning.md).

## <a name="forcing-restore-from-package-sources"></a>Paket kaynaklarını zorlayıcı yedekten geri yükleyin

Varsayılan olarak NuGet geri yükleme işlemleri paketlerden kullanın *genel paketleri* ve *http önbellek* açıklanan klasörleri [genel paketleri ve önbellek klasörleriniyönetme](managing-the-global-packages-and-cache-folders.md).

Kullanmaktan kaçınmak için *genel paketleri* klasörü, aşağıdakilerden birini yapın:

- Klasörü kullanılarak Temizle `nuget locals global-packages -clear` veya `dotnet nuget locals global-packages --clear`
- Geçici olarak konumunu değiştirmek *genel paketleri* aşağıdaki yöntemlerden birini kullanarak geri yükleme işlemi önce klasörü:
  - Farklı bir klasöre NUGET_PACKAGES ortam değişkenini ayarlayın.
  - Oluşturma bir `NuGet.Config` ayarlar dosyası `globalPackagesFolder` (PackageReference kullanıyorsanız) veya `repositoryPath` (kullanıyorsanız `packages.config`) farklı bir klasöre (bkz [yapılandırma ayarları](../reference/nuget-config-file.md#config-section)
  - Yalnızca MSBuild: ile farklı bir klasör belirtmek `RestorePackagesPath` özelliği.

Önbellek için HTTP kaynakları kullanmaktan kaçınmak için aşağıdakilerden birini yapın:

- Kullanım `-NoCache` seçeneğini `nuget restore` veya `--no-cache` seçeneğini `dotnet restore`. Bu seçenekler, Visual Studio Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden geri yükleme işlemleri etkilemez.
- Önbellek kullanarak Temizle `nuget locals http-cache -clear` veya `dotnet nuget locals http-cache --clear`.
- Geçici olarak farklı bir klasöre ilişkin NUGET_HTTP_CACHE_PATH ortam değişkeni ayarlayın.

## <a name="troubleshooting"></a>Sorun giderme

Bkz: [paket geri yükleme sorunlarını giderme](package-restore-troubleshooting.md).
