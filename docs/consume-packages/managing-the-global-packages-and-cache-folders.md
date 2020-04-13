---
title: NuGet'deki küresel paketleri, önbellekleri, geçici klasörleri nasıl yönetebilirsiniz?
description: Paketleri yüklerken, geri yüklerken ve güncellerken kullanılan genel paket yükleme klasörünü, paket önbelleğini ve bilgisayarda bulunan geçici klasörleri nasıl yönetiriz?
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428970"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Genel paketleri, önbelleği ve geçici klasörleri yönetme

Bir paketi yüklediğinizde, güncellediğinizde veya geri yüklediğinizde, NuGet paketleri ve paket bilgilerini proje yapınızın dışındaki çeşitli klasörlerde yönetir:

| Adı | Açıklama ve Konum (kullanıcı başına)|
| --- | --- |
| küresel&#8209;paketleri | *Genel paketler* klasörü, NuGet'in indirilen herhangi bir paketi yüklendiği yerdir. Her paket, paket tanımlayıcısı ve sürüm numarasıyla eşleşen bir alt klasöre tamamen genişletilir. [PackageReference](package-references-in-project-files.md) biçimini kullanan projeler her zaman paketleri doğrudan bu klasörden kullanır. [packages.config,](../reference/packages-config.md)paketleri kullanırken *genel paketler* klasörüne yüklenir ve proje `packages` klasörüne kopyalanır.<br/><ul><li>Windows:`%userprofile%\.nuget\packages`</li><li>Mac/Linux:`~/.nuget/packages`</li><li>NUGET_PACKAGES ortam `globalPackagesFolder` değişkenini, `repositoryPath` veya yapılandırma [ayarlarını](../reference/nuget-config-file.md#config-section) (Sırasıyla PackageReference ve `RestorePackagesPath` `packages.config`MSBuild özelliğini kullanırken) veya MSBuild özelliğini (yalnızca MSBuild) kullanarak geçersiz kılın. Ortam değişkeni yapılandırma ayarından önce gelir.</li></ul> |
| http&#8209;önbellek | Visual Studio Package Manager (NuGet 3.x+) ve `dotnet` araç, indirilen paketlerin kopyalarını `.dat` bu önbellekte (dosya olarak kaydedilir) her paket kaynağı için alt klasörler halinde düzenler. Paketler genişletilmez ve önbelleğin son kullanma süresi 30 dakikadır.<br/><ul><li>Windows:`%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/v3-cache`</li><li>NUGET_HTTP_CACHE_PATH ortamı değişkenini kullanarak geçersiz kılın.</li></ul> |
| Temp | NuGet'in çeşitli işlemleri sırasında geçici dosyaları depoladığı klasör.<br/><li>Windows:`%temp%\NuGetScratch`</li><li>Mac/Linux:`/tmp/NuGetScratch`</li></ul> |
| eklentileri-önbellek **4.8+** | NuGet'in operasyon talepleri isteğinin sonuçlarını depoladığı klasör.<br/><ul><li>Windows:`%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/plugins-cache`</li><li>NUGET_PLUGINS_CACHE_PATH ortam değişkenini kullanarak geçersiz kılın.</li></ul> |

> [!Note]
> NuGet 3.5 ve önceki *paketler-önbellek* yerine *http-önbellek*kullanır `%localappdata%\NuGet\Cache`, hangi bulunur .

Önbellek ve *genel paketler* klasörlerini kullanarak NuGet genellikle bilgisayarda zaten var olan paketleri karşıdan yükler, yükleme, güncelleştirme ve geri yükleme işlemlerinin performansını artırır. PackageReference'ı kullanırken, *genel paketler* klasörü indirilen paketleri, yanlışlıkla kaynak denetimine eklenebilecekleri proje klasörlerinde tutmayı da önler ve NuGet'in bilgisayar depolama üzerindeki genel etkisini azaltır.

Bir paket almak istendiğinde, NuGet ilk olarak *genel paketler* klasörüne bakar. Paketin tam sürümü yoksa, NuGet http olmayan tüm paket kaynaklarını denetler. Paket hala bulunamazsa, `dotnet.exe` komutlarla `-NoCache` veya `nuget.exe` komutlarla belirtmediğiniz `--no-cache` sürece NuGet paketi http *önbelleğinde* arar. Paket önbellekte değilse veya önbellek kullanılmamışsa, NuGet paketi HTTP üzerinden alır.

Daha fazla bilgi için [bkz.](../concepts/package-installation-process.md)

## <a name="viewing-folder-locations"></a>Klasör konumlarını görüntüleme

[Nuget locals komutunu](../reference/cli-reference/cli-ref-locals.md)kullanarak konumları görüntüleyebilirsiniz:

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Tipik çıktı (Windows; "user1" geçerli kullanıcı adıdır:

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` NuGet 2.x'te kullanılır ve NuGet 3.5 ve daha önce siyle birlikte görünür.)

Ayrıca [noktanu nuget yerel komutunu](/dotnet/core/tools/dotnet-nuget-locals)kullanarak klasör konumlarını görüntüleyebilirsiniz:

```dotnetcli
dotnet nuget locals all --list
```

Tipik çıktı (Mac/Linux; "user1" geçerli kullanıcı adıdır:

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Tek bir klasörün konumunu görüntülemek `http-cache` `global-packages`için `temp`, `plugins-cache` , `all`, veya yerine .

## <a name="clearing-local-folders"></a>Yerel klasörleri temizleme

Paket yükleme sorunlarıyla karşılaşırsanız veya uzak bir galeriden paket yüklediğinizden `locals --clear` emin olmak istiyorsanız, klasörü `locals -clear` temizlemek veya `all` temizlemek için klasörü belirterek seçeneği (dotnet.exe) veya (nuget.exe) kullanın:

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

Visual Studio'da şu anda açık olan projeler tarafından kullanılan paketler *genel paketler* klasöründen temizlenmez.

Visual Studio 2017'den **itibaren, NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutunu > Araçlar'ı kullanın ve ardından Tüm **NuGet Önbelleğini(ler) temizle'yi**seçin. Önbelleği yönetmek şu anda Paket Yöneticisi Konsolu aracılığıyla kullanılamaz. Visual Studio 2015'te cli komutlarını kullanın.

![Önbellekleri temizlemek için NuGet seçeneği komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Hatalarda sorun giderme

Aşağıdaki hatalar kullanırken `nuget locals` oluşabilir `dotnet nuget locals`veya:

- *Hata: İşlem, <package> başka bir işlem tarafından kullanıldığından* veya yerel kaynakları temizlemeden dosyaya erişemiyor: *Bir veya daha fazla dosya silinemiyor*

    Klasördeki bir veya daha fazla dosya başka bir işlem tarafından kullanılıyor; örneğin, *genel paketler* klasöründeki paketleri ifade eden bir Visual Studio projesi açıktır. Bu işlemleri kapatın ve yeniden deneyin.

- *Hata: Yola <path> erişim reddedildi* veya *dizin boş değil*

    Önbellekteki dosyaları silme izniniz yok. Mümkünse klasör izinlerini değiştirin ve yeniden deneyin. Aksi takdirde, sistem yöneticinize başvurun.

- *Hata: Belirtilen yol, dosya adı veya her ikisi de çok uzun. Tam nitelikli dosya adı 260 karakterden az olmalı ve dizin adı 248 karakterden az olmalıdır.*

    Klasör adlarını kısaltın ve yeniden deneyin.
