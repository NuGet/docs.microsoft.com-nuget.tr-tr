---
title: Visual Studio'da NuGet paket geri yükleme sorunlarını giderme
description: Visual Studio ve bunları nasıl giderebileceğinizden hatalar ortak NuGet açıklamasını geri yükleyin.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 11acb90b45af73137faac1ec6bc403b109e6e808
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549606"
---
# <a name="troubleshooting-package-restore-errors"></a>Paket geri yükleme hatalarını giderme

Bu makalede, paketleri ve bunların çözülmesine yönelik adımları geri yüklerken ortak hataları ele alınmaktadır. Paketleri geri yükleme ile ilgili tüm ayrıntılar için bkz. [paket geri yükleme](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Buradaki yönergeleri sizin için işe yaramazsa [Lütfen Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) böylece biz kendi senaryonuza daha dikkatli bir şekilde inceleyebilir. "Is bu sayfa faydalı?" kullanmayın Bize daha fazla bilgi için sizinle olanağı vermez çünkü bu sayfada görünebilir denetimi.

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio kullanıcılar için daha hızlı çözüm

İlk paket geri yükleme Visual Studio kullanıyorsanız, şu şekilde etkinleştirin. Aksi takdirde, izleyen bölümlerde devam edin.

1. Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu.
1. Her iki seçenekleri altında **paketi geri yüklemeyi**.
1. Seçin **Tamam**.
1. Projenizi yeniden derleyin.

![NuGet paket geri yükleme araç/seçenekler içinde etkinleştir](../consume-packages/media/restore-01-autorestoreoptions.png)

Bu ayarlar da içinde değiştirilebilir, `NuGet.config` bakın; dosyası [onay](#consent) bölümü.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Bu proje, bu bilgisayarda eksik olan NuGet paket başvuruları

Tam hata iletisi:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Bir veya daha fazla NuGet paket başvuruları içeren proje oluşturma girişimi, ancak bu paketleri şu anda bilgisayarınızda veya proje yüklenmez bu hata oluşur.

- PackageReference yönetim biçimi kullanılırken, paketin içinde yüklü değil hatası anlamına gelir *genel paketleri* sitesinde açıklandığı üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörleriniyönetme](managing-the-global-packages-and-cache-folders.md).
- Kullanırken `packages.config`, paket içinde yüklü değil hatası anlamına gelir `packages` çözüm kök klasör.

Bu durum genellikle kaynak denetimi veya başka bir yükleme projenin kaynak kodunu edinmek oluşur. Paketleri genellikle atlanmış kaynak denetimi veya yüklemeleri paket akışları nuget.org gibi gelen döndürülebilir olduğundan (bkz [paketleri ve kaynak denetimi](Packages-and-Source-Control.md)). Bunları da dahil olmak üzere Aksi halde depoyu Şişirme veya gereksiz derecede büyük .zip dosyalarını oluşturun.

Hata, proje dosyanızı içeren paket konumlara mutlak yollar ve proje taşıyorsanız de oluşabilir.

Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:

- Proje dosyası taşıdıysanız, doğrudan paket başvuruları güncelleştirileceği dosyayı düzenleyin.
- Visual Studio'da paket geri yükleme seçerek etkinleştirin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu, her iki çalışma seçeneklerde ayarlama **paketi geri yüklemeyi**, seçerek **Tamam**. Daha sonra çözümü yeniden oluşturun.
- .NET Core projeleri için çalıştırma `dotnet restore` veya `dotnet build` (otomatik olarak çalıştığı geri yükleme).
- Komut satırında çalıştırın `nuget restore` (ile oluşturulan projeleri hariç `dotnet`, bu durumda kullanın `dotnet restore`).
- PackageReference biçimini kullanarak projeleri ile komut satırında çalıştırın `msbuild /t:restore`.

Paket başarılı bir geri yüklemeden sonra mevcut olmalıdır *genel paketleri* klasör. PackageReference'ı kullanarak projeleri için bir geri yükleme yeniden oluşturmanız gerekir `obj/project.assets.json` dosya; kullanarak projeleri için `packages.config`, paket projesinin görünmelidir `packages` klasör. Şimdi, projeyi başarıyla oluşturmalısınız. Aksi halde [Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz size izleyecek şekilde.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Varlıklar dosya project.assets.json bulunamadı

Tam hata iletisi:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

`project.assets.json` Dosyası, bilgisayarda gerekli tüm paketleri yüklü olduğundan emin olmak için kullanılan PackageReference yönetim biçimi kullanılırken bir projenin bağımlılık grafiği tutar. Bu dosya paket geri yükleme ile dinamik olarak oluşturulmuş olduğu için kaynak denetimine genellikle eklenmez. Sonuç olarak, bir aracı ile proje gibi oluştururken bu hata oluşur `msbuild` , otomatik olarak paketleri geri yüklemez.

Bu durumda, çalıştırma `msbuild /t:restore` ardından `msbuild`, veya `dotnet build` (hangi yükler paketleri otomatik olarak). İçinde paket geri yükleme yöntemlerinden herhangi birini de kullanabilirsiniz [önceki bölümde](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Bir veya daha fazla NuGet paketlerini geri yüklenmesi gerekir, ancak izin verilmedi olduğundan kaldırılamadı

Tam hata iletisi:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Bu hata, bu paket geri yükleme, NuGet yapılandırmasında devre dışı gösterir.

Visual Studio'da geçerli ayarlar altında daha önce açıklandığı gibi değiştirebilirsiniz [hızlı çözüm için Visual Studio kullanıcılarına](#quick-solution-for-visual-studio-users).

Bu ayarları doğrudan geçerli da düzenleyebilirsiniz `nuget.config` dosyası (genellikle `%AppData%\NuGet\NuGet.Config` Windows üzerinde ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux üzerinde). Emin `enabled` ve `automatic` altında anahtarları `packageRestore` True olarak ayarlayın:

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
> Düzenlediyseniz `packageRestore` ayarları doğrudan `nuget.config`, Seçenekler iletişim kutusu geçerli değerleri gösterir, böylece Visual Studio'yu yeniden başlatın.

## <a name="other-potential-conditions"></a>Diğer olası koşulları

- Derleme hataları eksik dosyalar nedeniyle bunları indirmek için NuGet geri yükleme kullanmak bildiren bir ileti ile karşılaşabilirsiniz. Ancak, bir geri yükleme devam varsayalım, "tüm paketler zaten yüklü ve geri yüklemek için bir şey yok." Bu durumda, silme `packages` klasörü (kullanırken `packages.config`) veya `obj/project.assets.json` dosya (PackageReference kullanırken) ve geri yüklemeyi yeniden çalıştırın. Hatanın hala devam ederse `nuget locals all -clear` veya `dotnet locals all --clear` temizlemek için komut satırından *genel paketleri* ve klasörler üzerinde açıklandığı gibi önbelleğe [genel paketleri ve önbellek klasörleriniyönetme](managing-the-global-packages-and-cache-folders.md).

- Bir projeyi kaynak denetiminden edinirken, proje klasörleri salt okunur ayarlanması. Klasör izinleri ve paketleri yeniden geri yüklemeyi deneyin.

- NuGet'ın eski bir sürümünü kullanıyor olabilir. Denetleme [nuget.org/downloads](https://www.nuget.org/downloads) için en son sürümleri önerilir. Visual Studio 2015 için 3.6.0 öneririz.

Diğer sorunlarla karşılaşırsanız [Github'da sorun kaydedebilir](https://github.com/NuGet/docs.microsoft.com-nuget/issues) biz daha fazla ayrıntı, böylece elde edebilirsiniz.