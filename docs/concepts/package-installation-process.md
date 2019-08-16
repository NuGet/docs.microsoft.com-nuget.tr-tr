---
title: Paket yüklendiğinde ne olur?
description: Paket yükleme işlemi hakkında ayrıntılı bilgi
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 69ef02e3c935287759b4012aadcfb1cb9811367c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488441"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Bir NuGet paketi yüklendiğinde ne olur?

Basitçe, farklı NuGet araçlarının genellikle proje dosyasındaki `packages.config`bir pakete başvuru oluşturup daha sonra paketi etkin bir şekilde yüklediği bir paket geri yüklemesi gerçekleştireceğini söylemiştik. Özel durum, `nuget install`paketini yalnızca bir `packages` klasöre genişleten ve başka herhangi bir dosyayı değiştirmediğinden olur.

Genel işlem aşağıdaki gibidir:

1. (Tüm araçlar hariç `nuget.exe`), paket tanımlayıcısını ve sürümü proje dosyasına veya `packages.config`sürümüne kaydeder.

   Yükleme Aracı Visual Studio veya DotNet CLı ise, araç ilk olarak paketi yüklemeye çalışır. Uyumsuz ise, paket proje dosyasına veya `packages.config`öğesine eklenmez.

2. Paketi edinin:
   - [Genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi paketin (tam olarak tanımlayıcı ve sürüm numarası ile) *genel paketler* klasöründe zaten yüklü olup olmadığını denetleyin.

   - Paket *genel paketler* klasöründe değilse, bunu [yapılandırma dosyalarında](../consume-packages/Configuring-NuGet-Behavior.md)listelenen kaynaklardan almayı deneyin. `-NoCache` Çevrimiçi kaynaklar için, `nuget.exe` komutlarla veya `--no-cache` ile `dotnet restore`belirtimediği takdirde, paketi http önbelleğinden almayı deneyin. (Visual Studio ve `dotnet add package` her zaman önbelleği kullanır.) Bir paket önbellekten kullanılıyorsa, çıktıda "CACHE" görünür. Önbellekte 30 dakikalık bir sona erme saati vardır.

   - Paket HTTP önbelleğinde değilse, yapılandırmayı yapılandırmada listelenen kaynaklardan indirmeyi deneyin. Bir paket indirildiyse, çıktıda "Al" ve "Tamam" görüntülenir. NuGet, HTTP trafiğini normal ayrıntı temelinde günlüğe kaydeder.

   - Paket hiçbir kaynaktan başarıyla alınamazsa, yükleme bu noktada [NU1103](../reference/errors-and-warnings/NU1103.md)gibi bir hata ile başarısız olur. Komutlardan gelen `nuget.exe` hataların yalnızca son kaynağı kontrol edin, ancak paketin herhangi bir kaynaktan kullanılamayacağını gösterir.

   Paket alınırken, NuGet yapılandırmasındaki kaynakların sırası uygulanabilir:

   - NuGet, HTTP kaynaklarını denetlemeden önce yerel klasör ve ağ paylaşımlarının kaynaklarını denetler.

3. [Genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi, paketin ve diğer bilgilerin bir kopyasını *http-Cache* klasörüne kaydedin.

4. İndirildiyse, paketi Kullanıcı başına *genel paketler* klasörüne yükler. NuGet her paket tanımlayıcısı için bir alt klasör oluşturur, sonra paketin yüklü her sürümü için alt klasörler oluşturur.

5. NuGet, paket bağımlılıklarını gerektiği şekilde yüklüyor. Bu işlem, [bağımlılık çözümlemesi](../concepts/dependency-resolution.md)bölümünde açıklandığı gibi işlemdeki paket sürümlerini güncelleştirebilir.

6. Diğer proje dosyalarını ve klasörlerini güncelleştir:

    - PackageReference kullanan projeler için, içinde `obj/project.assets.json`depolanan paket bağımlılığı grafiğini güncelleştirin. Paket içerikleri herhangi bir proje klasörüne kopyalanmaz.
    - Güncelleştirme `app.config` ve/veya `web.config` paket [kaynak ve yapılandırma dosyası dönüştürmeleri](../create-packages/source-and-config-file-transformations.md)kullanıyorsa.

7. (Yalnızca Visual Studio) Bir Visual Studio penceresinde, varsa paketin Benioku dosyasını görüntüleyin.

NuGet paketleriyle üretken kodlarınızın keyfini çıkarın!
