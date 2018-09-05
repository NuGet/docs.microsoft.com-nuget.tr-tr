---
title: Genel paketleri, önbellek NuGet geçici klasörlere yönetmek nasıl
description: Genel paket yükleme klasörü, paket önbelleğini ve yüklenirken kullanılan bir bilgisayar, geri yükleme ve güncelleştirme paketlerini mevcut geçici klasör yönetmek nasıl.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548019"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Genel paketleri, önbellek ve geçici klasör yönetme

Yüklemek, güncelleştirmek ya da bir paket geri yükleme olduğunda, NuGet paketleri ve Proje yapısı dışında birçok klasörlerdeki paket bilgilerini yönetir:

| Ad | Açıklama ve konumu (kullanıcı başına)|
| --- | --- |
| Genel&#8209;paketleri | *Genel paketleri* klasördür burada NuGet herhangi indirilen paketi yükler. Her paket tam sürüm numarası ve paket tanımlayıcısı ile eşleşen bir alt klasör içine genişletilir. PackageReference'ı kullanarak projeleri, her zaman kullan paketlerini doğrudan bu klasörden biçimlendirin. Kullanırken `packages.config`, için yüklü paketleri *genel paketleri* klasörü, ardından projenin kopyalanır `packages` klasör.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Geçersiz kılma NUGET_PACKAGES ortam değişkenini kullanarak `globalPackagesFolder` veya `repositoryPath` [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section) (PackageReference kullanırken ve `packages.config`sırasıyla), veya `RestorePackagesPath` MSBuild özellik (yalnızca MSBuild). Ortam değişkenini üzerinden yapılandırma ayarı önceliklidir.</li></ul> |
| http&#8209;cache | Visual Studio Paket Yöneticisi'ni (NuGet 3.x+) ve `dotnet` aracı bu önbellek içinde indirilen paketler deposu kopyalarını (olarak kaydedilen `.dat` dosyaları), her paket kaynağı için alt klasörler halinde düzenlenmiş. Paketleri genişletilmemiş ve sona erme süresini 30 dakika bir önbelleğe sahiptir.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>NUGET_HTTP_CACHE_PATH ortam değişkenini kullanarak geçersiz kılar.</li></ul> |
| Temp | NuGet, çeşitli işlemleri sırasında geçici dosyaları depoladığı bir klasör.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| Eklentileri önbellek **4.8 +** | NuGet işlem talepleri isteği sonuçlardan depoladığı bir klasör.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>NUGET_PLUGINS_CACHE_PATH ortam değişkenini kullanarak geçersiz kılar.</li></ul> |

> [!Note]
> NuGet 3.5 ve önceki kullanımlar *paketleri önbellek* yerine *http önbellek*, bulunan `%localappdata%\NuGet\Cache`.

Önbellek kullanarak ve *genel paketleri* klasörleri NuGet genellikle önler bilgisayarda zaten mevcut olan paketleri indirme, yükleme performansını iyileştirme, güncelleştirme ve geri yükleme işlemleri. PackageReference, kullanırken *genel paketleri* klasör ayrıca tutma indirilen paketler nerede bunlar yanlışlıkla eklenmesi için kaynak denetimi, proje klasörleri içindeki önler ve bilgisayar NuGet'ın genel etkisini azaltır depolama alanı.

Bir paket almaya isteyip istemediğiniz sorulduğunda NuGet ilk baktığı *genel paketleri* klasör. Paket'ün tam sürümünü yoksa, NuGet HTTP olmayan paket kaynaklarının tümüne denetler. Paket hala bulunamıyorsa, NuGet paketi arar *http önbellek* belirtmediğiniz sürece `--no-cache` ile `dotnet.exe` komutları veya `-NoCache` ile `nuget.exe` komutları. Paket önbellekte değil ya da önbelleği kullanılmaz, NuGet paketi ardından HTTP üzerinden alır.

Daha fazla bilgi için [paketi yüklendiğinde ne](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Klasör konumlarını görüntüleme

Konumları kullanarak görüntüleyebileceğiniz [nuget Yereller komutu](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Tipik çıkış (Windows; "user1" olan geçerli kullanıcı adı):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` Nuget'te kullanılan 2.x ve NuGet 3.5 ve önceki sürümleri görüntülenir.)

Klasör konumlarını kullanarak da görüntüleyebilirsiniz [dotnet nuget Yereller komutu](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Tipik çıkış (Mac/Linux; "user1" olan geçerli kullanıcı adı):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Tek bir klasör konumunu görüntülemek için kullanın `http-cache`, `global-packages`, `temp`, veya `plugins-cache` yerine `all`.

## <a name="clearing-local-folders"></a>Yerel klasörler temizleme

Paket yükleme sorunlarla veya aksi halde uzak galerisinden, kullanım paketleri güvenilirliğinden emin olmak isterseniz `locals --clear` seçeneği (dotnet.exe) veya `locals -clear` (nuget.exe) temizlemek için bir klasör belirterek veya `all` için tüm klasörleri temizleyin:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Visual Studio'da açık olan projeler tarafından kullanılan tüm paketler gelen temizlenmez *genel paketleri* klasör.

Visual Studio 2017'de kullanmak **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutunu ve ardından **Temizle tüm NuGet önbellekler**. Önbellek Yönetimi, Paket Yöneticisi konsolu aracılığıyla şu anda kullanılamıyor. Visual Studio 2015'te, bunun yerine CLI komutlarını kullanın.

![Önbellek Temizleme için NuGet seçeneği komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Sorun giderme hataları

Kullanırken aşağıdaki hatalar oluşabilir `nuget locals` veya `dotnet nuget locals`:

- *Hata: İşlem dosyaya erişemiyor <package> başka bir işlem tarafından kullanıldığından* veya *yerel kaynakları temizleme başarısız oldu: bir veya daha fazla dosya silinemedi*

    Bir veya daha fazla dosya klasörüne başka bir işlem tarafından kullanılıyor; Örneğin, Visual Studio projesi paketlerine başvuran açık olan *genel paketleri* klasör. Bu işlemleri kapatın ve yeniden deneyin.

- *Hata: Erişim yolu <path> reddedildi* veya *dizini boş değil*

    Önbellekteki dosyaları silmek için izniniz yok. Mümkünse, klasör izinlerini değiştirin ve yeniden deneyin. Aksi takdirde, sistem yöneticinize başvurun.

- *Hata: Belirtilen yol, dosya adı veya her ikisi çok uzun olabilir. Tam dosya adı 260 karakterden az olmalıdır ve dizin adı 248 karakterden kısa olmalıdır.*

    Klasör adları kısaltın ve yeniden deneyin.
