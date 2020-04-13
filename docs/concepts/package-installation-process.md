---
title: Paket yüklendiğinde ne olur?
description: Paket yükleme işlemi hakkında detaylı bilgi
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77036909"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Bir NuGet paketi yüklendiğinde ne olur?

Basitçe, farklı NuGet araçları genellikle proje dosyasında bir paket `packages.config`için bir başvuru oluşturmak veya , sonra etkili paketi yükler bir paket geri yükleme gerçekleştirmek söyledi. Özel `nuget install`durum, paketi yalnızca bir `packages` klasöre genişleten ve diğer dosyaları değiştirmeyen dir.

Genel işlem aşağıdaki gibidir:

1. (Hariç `nuget.exe`tüm araçlar ) Paket tanımlayıcısını ve sürümünü proje dosyasına kaydedin veya `packages.config`.

   Yükleme aracı Visual Studio veya dotnet CLI ise, araç önce paketi yüklemeye çalışır. Uyumsuzsa, paket proje dosyasına veya `packages.config`.

2. Paketi edinin:
   - Paketin (tam identifer ve sürüm numarasına göre) [genel paketleri ve önbellek klasörlerini yönetmede](../consume-packages/managing-the-global-packages-and-cache-folders.md)açıklandığı gibi *genel paketler* klasörüne zaten yüklenmiş olup olmadığını kontrol edin.

   - Paket *genel paketler* klasöründe değilse, [yapılandırma dosyalarında](../consume-packages/Configuring-NuGet-Behavior.md)listelenen kaynaklardan almaya çalış. `-NoCache` Çevrimiçi kaynaklarda, `nuget.exe` komutlarla belirtilmedikçe veya `--no-cache` . `dotnet restore` (Visual Studio `dotnet add package` ve her zaman önbelleği kullanın.) Önbellekten bir paket kullanılırsa, çıktıda "CACHE" görüntülenir. Önbelleğin son kullanma süresi 30 dakikadır.

   - Paket HTTP önbelleğinde değilse, yapılandırmada listelenen kaynaklardan indirmeyi deneyin. Bir paket karşıdan yüklenirse, çıktıda "GET" ve "Ok" görünür. NuGet günlükleri normal verbosity http trafik.

   - Paket herhangi bir kaynaktan başarıyla elde edilemiyorsa, yükleme [nu1103](../reference/errors-and-warnings/NU1103.md)gibi bir hata ile bu noktada başarısız olur. Komutlardan gelen `nuget.exe` hataların yalnızca son kaynağın işaretedildiğini gösterdiğini, ancak paketin herhangi bir kaynaktan kullanılamadığı anlamına geldiğini unutmayın.

   Paketi alırken, NuGet yapılandırmasındaki kaynakların sırası geçerli olabilir:

   - NuGet, HTTP kaynaklarını kontrol etmeden önce kaynakları yerel klasörü ve ağ paylaşımlarını denetler.

3. Genel paketleri ve [önbellek klasörlerini yönetmede](../consume-packages/managing-the-global-packages-and-cache-folders.md)açıklandığı şekilde paketin ve diğer bilgilerin bir kopyasını *http önbellek* klasörüne kaydedin.

4. İndirilirse, paketi kullanıcı başına *genel paketler* klasörüne yükleyin. NuGet her paket tanımlayıcısı için bir alt klasör oluşturur, ardından paketin yüklenen her sürümü için alt klasörler oluşturur.

5. NuGet paket bağımlılıklarını gerektiği gibi yükler. Bu işlem, [Bağımlılık Çözümü'nde](../concepts/dependency-resolution.md)açıklandığı gibi, işlemdeki paket sürümlerini güncelleştirebilir.

6. Diğer proje dosya ve klasörlerini güncelleştirme:

    - PackageReference kullanan projelerde, 'de `obj/project.assets.json`depolanan paket bağımlılık grafiğini güncelleştirin. Paket içeriği herhangi bir proje klasörüne kopyalanmaz.
    - Güncelleştirme `app.config` ve `web.config` / veya paket [kaynak ve config dosya dönüşümleri kullanıyorsa.](../create-packages/source-and-config-file-transformations.md)

7. (Sadece Visual Studio) Varsa paketin okuma dosyasını Visual Studio penceresinde görüntüleyin.

NuGet paketleri ile üretken kodlamanın keyfini çıkarın!
