---
title: NuGet 'de küresel paketleri, önbelleği, temp klasörlerini yönetme
description: Paket yükleme, geri yükleme ve güncelleştirme sırasında kullanılan genel paket yükleme klasörünü, paket önbelleğini ve bir bilgisayarda bulunan temp klasörlerini yönetme.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e5585267d4ce2563d77ff30ec5c31e196d98686a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774793"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Küresel paketleri, önbelleği ve temp klasörlerini yönetme

Bir paketi yüklediğinizde, güncelleştirdiğinizde veya geri yükledikten sonra, NuGet paketleri ve paket bilgilerini proje yapınız dışında çeşitli klasörlerde yönetir:

| Name | Açıklama ve konum (Kullanıcı başına)|
| --- | --- |
| Genel&#8209;paketleri | *Genel paketler* klasörü, NuGet 'in indirilen tüm paketleri yüklediği yerdir. Her paket, paket tanımlayıcısı ve sürüm numarasıyla eşleşen bir alt klasöre tamamen genişletilir. [Packagereference](package-references-in-project-files.md) biçimini kullanan projeler her zaman paketleri doğrudan bu klasörden kullanır. [packages.config](../reference/packages-config.md)kullanılırken, paketler *genel paketler* klasörüne yüklenir ve ardından projenin `packages` klasörüne kopyalanır.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>NUGET_PACKAGES ortam değişkenini, `globalPackagesFolder` veya `repositoryPath` [yapılandırma ayarlarını](../reference/nuget-config-file.md#config-section) (, packagereference ve `packages.config` sırasıyla) veya `RestorePackagesPath` MSBuild özelliğini (yalnızca MSBuild) kullanarak geçersiz kılın. Ortam değişkeni yapılandırma ayarından önceliklidir.</li></ul> |
| http&#8209;önbelleği | Visual Studio Paket Yöneticisi (NuGet 3. x +) ve araç, `dotnet` indirilen paketlerin kopyalarını `.dat` , her bir paket kaynağı için alt klasörlere düzenlenmiş bu önbellekte (dosya olarak kaydedilir) depolar. Paketler genişletilmez ve önbellekte 30 dakikalık bir sona erme saati bulunur.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>NUGET_HTTP_CACHE_PATH ortam değişkenini kullanarak geçersiz kılın.</li></ul> |
| temp | NuGet 'in farklı işlemleri sırasında geçici dosyaları depoladığı bir klasör.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| Eklentiler-önbellek **4.8 +** | NuGet 'in işlem talep isteğinden sonuçları depoladığı bir klasör.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>NUGET_PLUGINS_CACHE_PATH ortam değişkenini kullanarak geçersiz kılın.</li></ul> |

> [!Note]
> NuGet 3,5 ve önceki sürümleri, ' de bulunan *http önbelleği* yerine *paketler-önbellek* kullanır `%localappdata%\NuGet\Cache` .

NuGet, önbellek ve *küresel paketler* klasörlerini kullanarak, yükleme, güncelleştirme ve geri yükleme işlemlerinin performansını artırarak, genellikle bilgisayarda zaten mevcut olan paketleri indirmeyi önler. PackageReference kullanılırken, *genel paketler* klasörü, karşıdan yüklenen paketlerin proje klasörleri içinde tutulmasını önler. Bu dosyalar, yanlışlıkla kaynak denetimine eklenmiş olabilir ve NuGet 'in bilgisayar depolamada genel etkisini azaltır.

Bir paketi almak isteyip istemediğiniz sorulduğunda, NuGet ilk olarak *genel paketler* klasörüne bakar. Paketin tam sürümü orada yoksa NuGet, HTTP olmayan tüm paket kaynaklarını denetler. Paket hala bulunamazsa NuGet, komutlarla veya komutlarla belirtmediğiniz takdirde, paketi *http önbelleğinde* arar `--no-cache` `dotnet.exe` `-NoCache` `nuget.exe` . Paket önbellekte değilse veya önbellek kullanılmıyorsa, NuGet paketi HTTP üzerinden alır.

Daha fazla bilgi için bkz. [bir paket yüklendiğinde ne olur?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Klasör konumlarını görüntüleme

[NuGet Yereller komutunu](../reference/cli-reference/cli-ref-locals.md)kullanarak konumları görüntüleyebilirsiniz:

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Tipik çıkış (Windows; "kullanıcı1" geçerli kullanıcı adıdır):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

( `package-cache` NuGet 2. x içinde kullanılır ve nuget 3,5 ve önceki sürümlerde görüntülenir.)

Ayrıca, [DotNet NuGet Yereller komutunu](/dotnet/core/tools/dotnet-nuget-locals)kullanarak klasör konumlarını görüntüleyebilirsiniz:

```dotnetcli
dotnet nuget locals all --list
```

Tipik çıkış (Mac/Linux; "kullanıcı1" geçerli kullanıcı adıdır):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Tek bir klasörün konumunu görüntüleme,,, `http-cache` `global-packages` `temp` veya `plugins-cache` yerine kullanın `all` .

## <a name="clearing-local-folders"></a>Yerel klasörleri Temizleme

Paket yükleme sorunlarıyla karşılaşırsanız veya uzak bir galeriden paket yüklediğinizden emin olmak istiyorsanız, `locals --clear` (dotnet.exe) veya `locals -clear` (nuget.exe) seçeneğini kullanın, temizlenecek klasörü belirterek veya `all` tüm klasörleri temizleyin:

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

Visual Studio 'da Şu anda açık olan projeler tarafından kullanılan tüm paketler, *genel paketler* klasöründen silinmez.

Visual Studio 2017 ' den başlayarak, **araç > NuGet paket yöneticisi > Paket Yöneticisi ayarları** menü komutunu kullanın ve **Tüm NuGet önbelleklerini temizle**' yi seçin. Önbelleğin yönetilmesi, şu anda Paket Yöneticisi konsolu aracılığıyla kullanılamaz. Visual Studio 2015 ' de, bunun yerine CLı komutlarını kullanın.

![Önbellekleri temizlemek için NuGet seçenek komutu](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Hatalarda sorun giderme

Veya kullanırken aşağıdaki hatalar oluşabilir `nuget locals` `dotnet nuget locals` :

- *Hata: <package> başka bir işlem tarafından kullanıldığı* veya *yerel kaynakları temizleyemedi, işlem dosyaya erişemiyor: bir veya daha fazla dosya silinemiyor*

    Klasördeki bir veya daha fazla dosya başka bir işlem tarafından kullanılıyor; Örneğin, *genel paketler* klasöründeki paketlere başvuran bir Visual Studio projesi açıktır. Bu işlemi kapatın ve yeniden deneyin.

- *Hata: yola erişim <path> engellendi* veya *Dizin boş değil*

    Önbellekteki dosyaları silme izniniz yok. Mümkünse klasör izinlerini değiştirip yeniden deneyin. Aksi takdirde, sistem yöneticinize başvurun.

- *Hata: belirtilen yol, dosya adı veya her ikisi çok uzun. Tam dosya adı 260 karakterden az olmalıdır ve dizin adı 248 karakterden az olmalıdır.*

    Klasör adlarını kısaltın ve yeniden deneyin.
