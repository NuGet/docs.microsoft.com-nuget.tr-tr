---
title: Genel paketler, önbellek NuGet geçici klasörlerde nasıl yönetilir
description: Genel paket yükleme klasörü, paket önbellek ve yüklenirken kullanılan bir bilgisayar, geri yükleme ve güncelleştirme paketlerini mevcut geçici klasör yönetmek nasıl.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 354a8ec80e2ba20abe27746dec8c8aaae9b6c96c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Genel paketler, önbellek ve geçici klasörleri yönetme

Yüklediğinizde, güncelleştirme veya bir paket geri yükleme her NuGet paketleri ve proje yapınızı dışında birkaç klasörlerde paket bilgilerini yönetir:

| Ad | Açıklama ve konumu (her bir kullanıcı)|
| --- | --- |
| Genel&#8209;paketleri | *Paketleri genel* klasördür nerede NuGet herhangi indirilen paketi yükler. Her paket sürüm numarası ve paket tanımlayıcısı ile eşleşen bir alt klasör içine tümüyle genişletilemiyor. PackageReference kullanarak projeleri her zaman bu klasörden doğrudan kullanım paketleri biçimlendirin. Kullanırken `packages.config`, paketleri yüklenir *paketleri genel* projenin kopyaladığınız klasörü `packages` klasörü.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>NUGET_PACKAGES ortam değişkeni kullanarak geçersiz kılma `globalPackagesFolder` veya `repositoryPath` [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section) (PackageReference kullanırken ve `packages.config`sırasıyla), veya `RestorePackagesPath` MSBuild özelliği (MSBuild yalnızca). Ortam değişkeni üzerinden yapılandırma ayarı öncelik alır.</li></ul> |
| http&#8209;cache | Visual Studio Paket Yöneticisi (NuGet 3.x+) ve `dotnet` aracı bu önbellekteki indirilen paketleri deposu kopyalarını (olarak kaydedilen `.dat` dosyaları), her bir paket kaynağı için alt klasörler halinde düzenlenir. Paketleri genişletilmemiş ve 30 dakikalık zaman aşımı değeri bir önbelleğe sahiptir.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>NUGET_HTTP_CACHE_PATH ortam değişkeni kullanarak geçersiz kılar.</li></ul> |
| Temp | NuGet, çeşitli işlemleri sırasında geçici dosyaları depoladığı bir klasör.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |

> [!Note]
> NuGet 3.5 ve önceki kullanır *paketleri önbellek* yerine *http önbellek*, bulunan `%localappdata%\NuGet\Cache`.

Önbellek kullanarak ve *paketleri genel* klasörler, NuGet genellikle önler bilgisayarda zaten mevcut paketleri indirme, yükleme performansını iyileştirme, güncelleştirme ve geri yükleme işlemleri. PackageReference, kullanırken *paketleri genel* klasörü ayrıca burada bunlar yanlışlıkla eklenmesi için kaynak denetimi, proje klasör içinde indirilen tutma paketleri engeller ve NuGet genel bilgisayar etkisini azaltır depolama alanı.

Bir paket almak için sorulduğunda, NuGet ilk görünür *paketleri genel* klasör. Paket'ün tam sürümünü yoksa, NuGet tüm HTTP olmayan paket kaynaklarını denetler. Paket yine bulunamazsa, NuGet paketi arar *http önbellek* belirtmediğiniz sürece `--no-cache` ile `dotnet.exe` komutları veya `-NoCache` ile `nuget.exe` komutları. Paketi önbellekte değil veya önbelleği kullanılmaz, NuGet paketi HTTP üzerinden sonra alır.

Daha fazla bilgi için bkz: [bir paket yüklendiğinde ne olacağını](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Klasör konumlarını görüntüleme

Klasör konumlarını kullanarak görüntüleyebileceğiniz [dotnet nuget Yereller komutu](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Tipik çıkış (Mac/Linux; "user1" olan geçerli kullanıcı adı):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

Tek bir klasör konumunu görüntülemek için kullanın `http-cache`, `global-packages`, veya `temp` yerine `all`. 

Ayrıca konumlardaki görüntülemek [nuget Yereller komutu](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

Tipik çıkış (Windows; "user1" olan geçerli kullanıcı adı):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

(`package-cache` NuGet içinde kullanılan 2.x ve NuGet 3.5 ve daha önce görünür.)

## <a name="clearing-local-folders"></a>Yerel klasörleri temizleme

Paket yükleme sorunlarla veya aksi takdirde uzaktan galerisinden, kullanım paketleri yüklüyorsanız sağlamak istiyorsanız `locals --clear` seçeneği (dotnet.exe) veya `locals -clear` (nuget.exe) temizlemek için klasörü belirtme veya `all` için tüm klasörleri temizleyin:

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

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Visual Studio şu anda açık olan projeler tarafından kullanılan herhangi bir paket gelen temizlenmez *paketleri genel* klasör.

Visual Studio 2017 ' kullanmak **Araçlar > NuGet Paket Yöneticisi > paket yönetimi ayarları** menü komutunu ve ardından **Temizle tüm NuGet önbellekler**. Önbellek yönetme, Paket Yöneticisi konsolu aracılığıyla şu anda kullanılamıyor. Visual Studio 2015'te, bunun yerine CLI komutları kullanın.

![Önbellekleri temizlemek için NuGet seçeneği komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Sorun giderme

Kullanırken aşağıdaki hatalar oluşabilir `nuget locals` veya `dotnet nuget locals`:

- *Hata: İşlem dosyasına erişemiyor <package> başka bir işlem tarafından kullanıldığından* veya *yerel kaynakları temizleme başarısız oldu: bir veya daha fazla dosya silinemiyor*

    Bir veya daha fazla dosya klasöründe başka bir işlem tarafından kullanılıyor; Örneğin, bir Visual Studio projesi paketlerinde başvurduğu açık olduğu *paketleri genel* klasör. Bu işlemleri kapatın ve yeniden deneyin.

- *Hata: Erişim yolunu <path> reddedildi* veya *dizini boş değil*

    Önbellekteki dosyaları silmek için izniniz yok. Mümkünse, klasör izinlerini değiştirin ve yeniden deneyin. Aksi takdirde, sistem yöneticinize başvurun.

- *Hata: Belirtilen yolun, dosya adı veya her ikisini birden çok uzun. Tam dosya adı 260 karakterden az olmalıdır ve dizin adı 248 karakterden kısa olmalıdır.*

    Klasör adları kısaltın ve yeniden deneyin.
