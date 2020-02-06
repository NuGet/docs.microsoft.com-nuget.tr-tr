---
title: Paket yüklendiğinde ne olur?
description: Paket yükleme işlemi hakkında ayrıntılı bilgi
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036909"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Bir NuGet paketi yüklendiğinde ne olur?

Tek fark, farklı NuGet araçlarının genellikle proje dosyasındaki veya `packages.config`bir pakete başvuru oluşturup sonra paketi etkin bir şekilde yüklediği bir paket geri yükleme işlemi gerçekleştirmesini sağlar. Özel durum, paketi yalnızca bir `packages` klasörüne genişleten ve başka herhangi bir dosyayı değiştirmediğinden `nuget install`.

Genel işlem aşağıdaki gibidir:

1. (`nuget.exe`hariç tüm araçlar) Paket tanımlayıcısını ve sürümü proje dosyasına veya `packages.config`kaydedin.

   Yükleme Aracı Visual Studio veya DotNet CLı ise, araç ilk olarak paketi yüklemeye çalışır. Uyumsuz ise, paket proje dosyasına eklenmez veya `packages.config`.

2. Paketi edinin:
   - [Genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi paketin (tam olarak tanımlayıcı ve sürüm numarası ile) *genel paketler* klasöründe zaten yüklü olup olmadığını denetleyin.

   - Paket *genel paketler* klasöründe değilse, bunu [yapılandırma dosyalarında](../consume-packages/Configuring-NuGet-Behavior.md)listelenen kaynaklardan almayı deneyin. Çevrimiçi kaynaklar için, `-NoCache` `nuget.exe` komutlarıyla belirtilmedikçe veya `dotnet restore`ile `--no-cache` belirtilmedikçe, paketi HTTP önbelleğinden almayı deneyin. (Visual Studio ve `dotnet add package` her zaman önbelleği kullanır.) Bir paket önbellekten kullanılıyorsa, çıktıda "CACHE" görünür. Önbellekte 30 dakikalık bir sona erme saati vardır.

   - Paket HTTP önbelleğinde değilse, yapılandırmayı yapılandırmada listelenen kaynaklardan indirmeyi deneyin. Bir paket indirildiyse, çıktıda "Al" ve "Tamam" görüntülenir. NuGet, HTTP trafiğini normal ayrıntı temelinde günlüğe kaydeder.

   - Paket hiçbir kaynaktan başarıyla alınamazsa, yükleme bu noktada [NU1103](../reference/errors-and-warnings/NU1103.md)gibi bir hata ile başarısız olur. `nuget.exe` komutlarından gelen hataların yalnızca son kaynağı kontrol edin, ancak paketin herhangi bir kaynaktan kullanılamayacağını gösterir.

   Paket alınırken, NuGet yapılandırmasındaki kaynakların sırası uygulanabilir:

   - NuGet, HTTP kaynaklarını denetlemeden önce yerel klasör ve ağ paylaşımlarının kaynaklarını denetler.

3. [Genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi, paketin ve diğer bilgilerin bir kopyasını *http-Cache* klasörüne kaydedin.

4. İndirildiyse, paketi Kullanıcı başına *genel paketler* klasörüne yükler. NuGet her paket tanımlayıcısı için bir alt klasör oluşturur, sonra paketin yüklü her sürümü için alt klasörler oluşturur.

5. NuGet, paket bağımlılıklarını gerektiği şekilde yüklüyor. Bu işlem, [bağımlılık çözümlemesi](../concepts/dependency-resolution.md)bölümünde açıklandığı gibi işlemdeki paket sürümlerini güncelleştirebilir.

6. Diğer proje dosyalarını ve klasörlerini güncelleştir:

    - PackageReference kullanan projeler için `obj/project.assets.json`' de depolanan paket bağımlılığı grafiğini güncelleştirin. Paket içerikleri herhangi bir proje klasörüne kopyalanmaz.
    - Paket [kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md)kullanıyorsa `app.config` ve/veya `web.config` güncelleştirin.

7. (Yalnızca Visual Studio) Bir Visual Studio penceresinde, varsa paketin Benioku dosyasını görüntüleyin.

NuGet paketleriyle üretken kodlarınızın keyfini çıkarın!
