---
title: "NuGet paket geri yüklemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "Nasıl NuGet üzerinde bir proje, geri yükleme devre dışı bırakın ve sürümleri sınırlamak nasıl dahil bağlı olan paketler geri yükler açıklaması."
keywords: "NuGet paket geri yüklemesi, NuGet paket yükleme paketini, paketleri, bağımlılık sürümleri otomatik geri yükleme, devre dışı bırakma, geri yükleme, paket sürümlerinin sınırlama"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a>Paket geri yüklemesi

Temizleyici bir geliştirme ortamı yükseltmek için ve havuz boyutu, NuGet azaltmak için **paketi geri yüklemesi** proje oluşturulmadan önce tüm başvurulmuş paketleri yükler. Yaygın olarak kullanılan bu özellik tüm bağımlılıkları kaynak denetiminde depolanması için bu paketleri gerek kalmadan bir projede kullanılabilir olmasını sağlar (bkz [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) deponuz dışlamak için yapılandırma Paket ikili dosyaları).

Bu konuda:
- [Hızlı Kılavuz paket geri yükleme](#quick-guide-to-package-restore)
- [Paket geri yükleme genel bakış](#package-restore-overview)
- [Paket geri yüklemesi devre dışı bırakma ve etkinleştirme](#enabling-and-disabling-package-restore)
- [Geri yükleme ile kısıtlayan paketi sürümleri](#constraining-package-versions-with-restore)
- [Komut satırı geri yükleme](#command-line-restore), NuGet'in tüm sürümleri için
- [Visual Studio'da otomatik geri yükleme](#automatic-restore-in-visual-studio), NuGet 2.7 için ve daha sonra.
- [Visual Studio geri yükleme MSBuild tümleşik](#msbuild-integrated-restore), NuGet 2.6 ve önceki sürümler için.
- [Team Foundation Build ile paket geri yükleme](#package-restore-with-team-foundation-build)

Geri yükleme davranışını sürümü tarafından; değişir NuGet sürümünüzü denetlemek için çalıştırmanız yeterlidir `nuget.exe` komut satırı ve çıktısının ilk satırı bakın.

Yapı sunucuları paket geri yükleme hakkında daha fazla ayrıntı için bkz: [TFBuild ile paket geri yükleme](../consume-packages/team-foundation-build.md).

> [!Note]
> Paket için yapılandırılan projeleri de xbuild Mono üzerinde çalışmak geri yükleyin.

## <a name="quick-guide-to-package-restore"></a>Hızlı Kılavuz paket geri yükleme

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> "Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru" hatayı görmek veya "bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı" başlığı altında verilen yönergeleri izleyerek otomatik geri yükleme Aç [Etkinleştirme ve paket geri yüklemesi devre dışı bırakma](#enabling-and-disabling-package-restore).

## <a name="package-restore-overview"></a>Paket geri yükleme genel bakış

İlk olarak, paket referanslarını proje türü ve NuGet sürümü bağlı olarak aşağıdaki paket Yönetimi biçimlerden birinde saklanır. (NuGet 4 ve MSBuild 15.1 ile Visual Studio 2017 yüklendiğini unutmayın.)

| Yöntem | NuGet sürümü | Açıklama | 
| --- | --- | --- |
| `packages.config` | 2.x + | Derin tamamını bağımlılıkları listeler. Eklenen paketler `packages.config` da proje dosyasına eklenmelidir ve hedefleri ve özellik de eklenmelidir proje dosyası. Bu, tüm sürümleri NuGet, ancak için diğer seçenekleri ile karşılaştırıldığında daha yavaş performans taban çizgisi yöntemidir. (Bkz [packages.config şema](../schema/packages-config.md).) | 
| `project.json` | 3.x + | Yalnızca UWP projeleri ile varsayılan olarak kullanılır, ancak projeleri, gelen dönüştürülebilir `packages.config`. `project.json`yalnızca üst düzey bağımlılıkları listeler. Başvurular, hedefleri ve özellik eklenir dinamik olarak proje derleme sırasında karşılaştırıldığında daha iyi performans elde edilen `packages.config`. (Bkz [project.json şema](../schema/project-json.md).)|
| PackageReference | 4.x + | Proje dosyasında doğrudan bağımlılıkları listeler `<PackageReference>` düğümü, alongside `<Reference>` ve `<ProjectReference>`. Benzer şekilde çalışır `project.json`; bkz [paketini proje dosyalarını başvurularında](../Consume-Packages/Package-References-in-Project-Files.md). |

İkinci olarak, çeşitli yollarla başvuru listesinde kullanarak geri yüklemeyi başlat:

Komut satırından veya [Paket Yöneticisi Konsolu](../tools/Package-Manager-Console.md):

| Komut | İlgili senaryolar |
| --- | --- | 
| `nuget restore` | NuGet ve tüm başvuru türleri tüm sürümleri. Bkz: [komut satırı geri yükleme](#command-line-restore) aşağıda. | 
| `dotnet restore` | Aynı `nuget restore` .NET Core projeleri için. Bkz: [dotnet geri yükleme](/dotnet/articles/core/tools/dotnet-restore). |
| `msbuild /t:restore` | Nuget 4.x+ ve MSBuild 15.1 + ile [paketini proje dosyalarını başvurularında](../Consume-Packages/Package-References-in-Project-Files.md) yalnızca. `nuget restore`ve `dotnet restore` her ikisi de geçerli projeleri için bu komutu kullanın. Bkz: [NuGet paketi ve geri yükleme olarak MSBuild hedefleri-geri yükleme hedefi](../schema/msbuild-targets.md#restore-target).|

Visual Studio kendisini paketleri farklı zamanlarda da yükler:

| Tür | Geri yükleme durumda |
| --- | --- |
| Şablon geri yükleme | Yeni bir proje oluşturma sırasında bazı şablonlar dış paketlere bağımlı. |
| Geri yükleme derleme | Bir yapı ilk adım olarak. |
| Çözüm geri yükleme | Kullanıcı ne zaman bir çözüm sağ tıklatır ve seçer **NuGet paketleri geri**. |
| Proje değişiminde geri yükleme | *(NuGet yalnızca 4.x)*  Zaman bir .NET Core SDK tabanlı proje kullanılır, ne zaman dahil olmak üzere proje durum değişiklikleri. |

## <a name="enabling-and-disabling-package-restore"></a>Paket geri yüklemesi devre dışı bırakma ve etkinleştirme

Paket geri yüklemesi aracılığıyla etkin öncelikle **Araçlar > Seçenekler > NuGet Paket Yöneticisi** Visual Studio'da:

![Paket geri yükleme davranışları NuGet Paket Yöneticisi seçeneklerle denetleme](media/Restore-01-AutoRestoreOptions.png)

- **Nuget'in eksik paketleri indirmesine izin ver**: değiştirerek denetimleri paket geri yükleme tüm forms `packageRestore/enabled` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.

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
    

- **Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**: Otomatik geri yükleme NuGet 2.7 için ve daha sonra değiştirerek denetimleri `packageRestore/automatic` ayarı `%AppData%\NuGet\NuGet.Config` aşağıda gösterildiği gibi dosya.
            
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

Başvuru için bkz: [NuGet yapılandırma dosyası - packageRestore bölüm](../Schema/nuget-config-file.md#packagerestore-section).

Bazı durumlarda, bir geliştirici veya şirket, etkinleştirmek veya paket geri yüklemesi bir makinedeki tüm kullanıcılar için varsayılan olarak devre dışı bırakmak isteyebilirsiniz. Bu bulunan genel NuGet yapılandırma dosyasını yukarıdaki aynı ayarları ekleyerek yapılabilir `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`. Tek tek kullanıcılar sonra seçerek geri yükleme üzerinde proje düzeyi gerektiği şekilde etkinleştirebilirsiniz. Bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) NuGet birden çok yapılandırma dosyaları nasıl önceliklendirir ilgili tam ayrıntılar.

## <a name="constraining-package-versions-with-restore"></a>Geri yükleme ile kısıtlayan paketi sürümleri

NuGet paketleri herhangi bir yöntemini yüklediğinde belirtilen kısıtlamalar dokunmaz `packages.config`, `project.json`, ya da proje dosyası:

- `packages.config`: Bir sürüm aralığı belirtin `allowedVersion` bağımlılık özelliği. Bkz: [yeniden yüklemeyi ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Örneğin:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- `project.json`: Doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin. Örneğin:

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- Proje dosyalarını başvurularında paketini: doğrudan bağımlılık ait sürüm numarasına sahip bir sürüm aralığı belirtin. Örneğin:
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

Her durumda, açıklanan gösterimini kullanın [paket sürüm](../reference/package-versioning.md).

## <a name="command-line-restore"></a>Komut satırı geri yükleme

NuGet 2.7 için ve üstü, kullanım [geri](../tools/cli-ref-restore.md) bir çözümde tüm paketler geri yüklemek için komut (bunu kullanıp kullanmadığını `packages.config`, `project.json`, veya paket proje dosyalarını başvurularında). Belirtilen proje klasörü gibi `c:\proj\app`, her aşağıda ortak Çeşitlemeler paketler geri:

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

NuGet 4.0 + ve MSBuild 15.1 + için de kullanabilirsiniz `MSBuild /t:restore` açıklandığı gibi [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md).

## <a name="build-time-restore-in-visual-studio"></a>Visual Studio'da derleme zamanı geri yükleme

Visual Studio eksik paketleri bir yapı başındaki varsayılan olarak otomatik olarak yükler. Bu davranış temizleyerek değiştirilebilir **Araçlar > Seçenekler > NuGet Paket Yöneticisi > Genel > Visual Studio'da sırasında eksik paketleri oluşturmak için otomatik olarak denetle**.

Etkinleştirildiğinde, otomatik geri yükleme gibi çalışır:

1. Visual Studio derleme işlemi başladığında, NuGet paketlerini geri yüklemek için bildirir.
1. NuGet özyinelemeli olarak arar tüm `packages.config` çözüm dosyaları arar `project.json`, veya proje dosyasında bakar.
1. Çözümde zaten varsa, her paketleri denetimleri başvuru dosyaları, NuGet listelenen için ( `packages` klasörünü `project.lock.json`, veya `project.assets.json` proje kullanmanıza bağlı olarak `packages.config`, `project.json`, veya paket başvuruları Proje dosyaları).
1. Paket bulunamadı NuGet paketi, ilk önbellekten çalışır (bkz [NuGet önbelleği yönetme](../consume-packages/managing-the-nuget-cache.md). Paket önbellekte değilse, NuGet paketi etkin kaynaklardan içinde listelenen indirmeyi dener **Araçlar > Seçenekler > NuGet Paket Yöneticisi > paket kaynaklarını**, sırayla kaynakları görünür. Bu durumda, NuGet paketi tüm kaynakları iade kadar isteğe bağlı olarak hangi aynı anda yalnızca listedeki son kaynak için hata raporları bulmak için bir hata olduğunu göstermez. Hataları bu kaynakları için ayrı ayrı gösterilmeyen olsa bile tarafından uygulanır böyle bir hata Ayrıca paket herhangi diğer kaynakları ya da, mevcut değildi olduğunu anlamına gelir.
1. Yükleme başarılı olursa, NuGet paketini önbelleğe alır ve çözüme yükler (ya da içine yeniden `packages` klasörünü `project.lock.json`, veya `project.assets.json`); Aksi takdirde NuGet başarısız olur ve derleme başarısız oluyor.

Bu işlem sırasında paket geri yüklemesi iptal etme seçeneği ile ilerleme iletişim kutusu görürsünüz.

## <a name="package-restore-with-team-foundation-build"></a>Team Foundation derlemesi ile paket geri yükleme

Paket geri yüklemesi, Team Foundation Server (TFS) ve Visual Studio Team Services (yanı sıra gibi burada incelenmemiştir diğer yapı sistemleri) ile derleme sunucularda projeleri oluştururken, yaygın olarak kullanılır.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services

Yalnızca bir derleme tanımınız Team Services oluştururken, önce herhangi bir derleme görev tanımında NuGet paketleri geri görev içerir. Bu görev varsayılan derleme şablonları sayısı olarak dahil edilir.

![Visual Studio Team hizmeti yapı tanımında NuGet paket geri yükleme görevi](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a>Team Foundation Server

Yapı Team Foundation Server 2013 veya üzeri Team şablonu kullanmakta olduğunuz koşuluyla TFS 2013 ve üzeri, paketleri otomatik olarak varsayılan derleme sırasında geri yüklenir.

Derleme şablonları (örn. TFS önceki sürümlerinden geçirilen bir proje) önceki bir sürümünü kullanıyorsanız, aynı zamanda geçirmek gerekir olanlar TFS 2013 için şablonlar oluşturma. Bu temelde derleme şablonları özel bölümlerini yeniden uygun şablonu, kaynak denetimi için (TFVC'yi veya Git) kullanarak anlamına gelir.

TFS önceki sürümü için çağrılacak bir derleme adımı yalnızca içerebilir [komut satırı geri yükleme](#command-line-restore) daha önce açıklandığı gibi.

Daha sonra daha fazla ayrıntı görmek için [gözden geçirme, paket geri yükleme ile Team Foundation Build](../consume-packages/team-foundation-build.md).    
