---
title: Visual Studio'da NuGet paket geri yükleme sorunlarını giderme
description: Visual Studio ve bunları gidermek nasıl hatalar geri yükleme ortak NuGet açıklaması.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 8e817b8e95c53d27120bf56db52b45b69a5ff973
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816982"
---
# <a name="troubleshooting-package-restore-errors"></a>Paket geri yükleme hatalarını giderme

Bu makalede, paketleri ve bunları gidermek için adımları geri yüklerken ortak hataları ele alınmaktadır. Paketler geri yükleme ile ilgili tam Ayrıntılar için bkz: [paket geri yüklemesi](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Buradaki yönergeleri, işe yaramazsa [Lütfen bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) böylece senaryonuz daha dikkatlice inceleyin. "Yararlıdır bu sayfayı?" kullanmayın Bunu bize daha fazla bilgi için sizinle vermek değil çünkü bu sayfada görünebilir denetim.

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio kullanıcılar için hızlı çözümü

İlk paket geri yüklemesi Visual Studio kullanıyorsanız, aşağıdaki gibi etkinleştirin. Aksi durumda bölümlerde için devam edin.

1. Seçin **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutu.
1. Her iki seçenekleri altında **paketi geri yüklemesi**.
1. Seçin **Tamam**.
1. Projenizi yeniden oluşturun.

![NuGet paket geri yüklemesi aracı/seçeneklerinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

Bu ayarları da değiştirilebilir, `NuGet.config` bakın; dosyası [onayı](#consent) bölümü.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Bu proje bu bilgisayarda eksik olan NuGet paketlerine başvuru

Tam hata iletisi:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Bu hata oluşur. bir veya daha fazla NuGet Paketlerine yönelik başvuruları içeren bir projeyi derleme çalışıldı, ancak bu paketleri şu anda bilgisayarda veya projesinde yüklü değil.

- PackageReference yönetim biçimi kullanırken, paket içinde yüklenmedi hata anlamına gelir *paketleri genel* açıklandığı gibi açık açıklandığı gibi klasör [önbellek klasörvegenelpaketleriniyönetme](managing-the-global-packages-and-cache-folders.md).
- Kullanırken `packages.config`, paket içinde yüklenmedi hata anlamına gelir `packages` çözüm kök klasör.

Bu durum, yaygın olarak kaynak denetimi veya başka bir yükleme projenin kaynak kodu elde oluşur. Paketleri genellikle atlanmış kaynak denetimi veya yüklemeleri bunlar paket akışları nuget.org gibi geri yüklenebileceği olduğundan (bkz [paketler ve kaynak denetimi](Packages-and-Source-Control.md)). Bunları dahil olmak üzere Aksi durumda depo Şişir veya gereksiz yere büyük .zip dosyalarını oluşturun.

Hata, paket konumlara mutlak yollar proje dosyanızı içeren ve projeye taşırsanız de oluşabilir.

Paketler geri yüklemek için aşağıdaki yöntemlerden birini kullanın:

- Proje dosyası taşıdıysanız doğrudan paket referanslarını güncelleştirmek için dosyayı düzenleyin.
- Visual Studio'da paket geri yüklemesi seçerek etkinleştirin **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutu, her iki seçenek altında ayarı **paketi geri yüklemesi**ve seçme **Tamam**. Ardından çözümü yeniden oluşturun.
- .NET Core projelerde çalıştırmak `dotnet restore` veya `dotnet build` (otomatik olarak çalıştığı geri yükleme).
- Komut satırında çalıştırmak `nuget restore` (ile oluşturulmuş projelerde dışında `dotnet`, bu durumda kullanmak `dotnet restore`).
- PackageReference biçimi kullanarak projeleri ile komut satırında çalıştırmak `msbuild /t:restore`.

Başarılı bir geri yüklendikten sonra paketi mevcut olmalıdır *paketleri genel* klasör. PackageReference kullanarak projeleri için bir geri yükleme yeniden oluşturmanız gerekir `obj/project.assets.json` dosya; kullanarak projeleri için `packages.config`, paket projesinin görünmelidir `packages` klasör. Projeyi şimdi başarıyla oluşturmalısınız. Aksi durumda, [bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz sizinle izleyecek şekilde.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Varlıklar bulunamadı project.assets.json dosya

Tam hata iletisi:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Dosyası, tüm gerekli paketleri bilgisayarda yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimi kullanırken bir projenin bağımlılık grafiğinin sağlar. Bu dosya paket geri yüklemesi dinamik olarak oluşturulduğundan, kaynak denetimine genellikle eklenmez. Sonuç olarak, aşağıdaki gibi bir araçla proje oluşturma bu hata oluşur `msbuild` , otomatik olarak paketler geri yüklemez.

Bu durumda, çalıştırmak `msbuild /t:restore` arkasından `msbuild`, veya `dotnet build` (hangi geri yükler paketleri otomatik olarak). Paket geri yükleme yöntemlerinden herhangi birini de kullanabilirsiniz [önceki bölümde](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Bir veya daha fazla NuGet paketinin geri yüklenmesi gerekiyor ancak izin verilmediği için yapılamadı

Tam hata iletisi:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Bu hata, paket geri yükleme NuGet yapılandırmanızda devre dışı gösterir.

Visual Studio içindeki geçerli ayarları altında daha önce açıklandığı gibi değiştirebilirsiniz [Visual Studio kullanıcılar için hızlı çözüm](#quick-solution-for-visual-studio-users).

Bu ayarları doğrudan geçerli de düzenleyebilirsiniz `nuget.config` dosyası (genellikle `%AppData%\NuGet\NuGet.Config` Windows'da ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta). Emin olun `enabled` ve `automatic` altında anahtarları `packageRestore` True olarak ayarlayın:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Düzenlediyseniz `packageRestore` ayarlarını doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir böylece Visual Studio'yu yeniden başlatın.

## <a name="other-potential-conditions"></a>Diğer olası koşulları

- Derleme hataları eksik dosyalar nedeniyle bunları indirmek için NuGet restore kullanılacağını belirten bir ileti ile karşılaşabilirsiniz. Ancak, bir geri yükleme çalıştıran söyleyin, "tüm paketler zaten yüklendi ve geri yüklenecek bir şey yok." Bu durumda, silme `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken) ve geri yüklemeyi yeniden çalıştırın. Hata devam ederse kullanmak `nuget locals all -clear` veya `dotnet locals all --clear` temizlemek için komut satırından *paketleri genel* ve açıklandığı gibi klasör önbelleğe [önbellek klasörvegenelpaketleriniyönetme](managing-the-global-packages-and-cache-folders.md).

- Bir proje kaynak denetiminden alırken, proje klasörlerinizi salt okunur ayarlanması. Klasör izinlerini değiştirin ve paketleri geri yüklemeyi yeniden deneyin.

- NuGet'ın eski sürümünü kullanıyor olabilirsiniz. Denetleme [nuget.org/downloads](https://www.nuget.org/downloads) için en son sürümleri önerilir. Visual Studio 2015 için 3.6.0 öneririz.

Başka bir sorunla karşılaşırsanız [bir sorun Github'da dosya](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz daha fazla ayrıntı, böylece elde edebilirsiniz.