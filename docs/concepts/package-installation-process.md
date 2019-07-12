---
title: Bir paketi yüklendiğinde ne olur?
description: Paket yükleme işlemiyle ilgili ayrıntılı bilgileri
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 5676239bedb7f8fbe9f74725864afd297405d5c1
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842328"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Bir NuGet paketi yüklendiğinde ne olur?

Kısaca, farklı NuGet araçları genellikle bir pakete bir başvuru proje dosyasında oluşturma veya `packages.config`, ardından etkili bir şekilde paket yükleyen bir paket geri yükleme gerçekleştirin. Özel durum `nuget install`, hangi yalnızca genişletir pakete bir `packages` klasör ve diğer dosyaları değiştirmez.

Genel süreç aşağıdaki gibidir:

1. (Tüm araçlar dışında `nuget.exe`) sürümü ve paket tanımlayıcısı proje dosyasına kaydedin veya `packages.config`.

   Aracı Yükleme aracı Visual Studio ya da ' % s'dotnet CLI ise, ilk paketi yüklemek çalışır. Paket uyumlu değilse, proje dosyasına eklenmez veya `packages.config`.

2. Paket Al:
   - İçinde paket (tam tanımlayıcı ve sürüm numarası tarafından) önceden yüklenip yüklenmediğini denetlemek *genel paketleri* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Paketin içinde değilse *genel paketleri* klasörü, onu listelenen kaynaklarından listelenen alma denemesi [yapılandırma dosyalarını](../consume-packages/Configuring-NuGet-Behavior.md). Çevrimiçi kaynaklar için ilk paketi HTTP önbellekten sürece alma denemesi `-NoCache` ile belirtilen `nuget.exe` komutları veya `--no-cache` ile belirtilen `dotnet restore`. (Visual Studio ve `dotnet add package` her zaman önbelleğe kullanın.) Bir paket önbellekten kullanılan "ÖNBELLEK" çıktısında görüntülenir. Önbellek sona erme süresini 30 dakika vardır.

   - Paket HTTP önbellekte değilse yapılandırmasında listelenen kaynaklardan indirme girişimi. Bir paket yüklediyseniz, "GET" ve "Tamam" çıkışında görüntülenir. NuGet http trafiğini normal ayrıntı kaydeder.

   - Paket başarıyla tüm kaynaklardan gelen alınamıyor, yükleme bir hata ile bu noktada gibi başarısız [NU1103](../reference/errors-and-warnings/NU1103.md). Not Bu hatalardan `nuget.exe` komutları göster yalnızca son kaynak işaretli, ancak gelir paket herhangi bir kaynaktan kullanılabilir durumda.

   Paket alırken, kaynakları NuGet yapılandırma sırasını uygulanabilir:

   - NuGet HTTP kaynakları denetlemeden önce kaynakları yerel klasörü ve ağ paylaşımlara denetler.

3. Paket ve diğer bilgiler bir kopyasını kaydedin *http önbellek* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. İndirdiyseniz, paketi, kullanıcı başına yükleyin. *genel paketleri* klasör. NuGet, her paket tanımlayıcısı için bir alt klasör oluşturur ve ardından paketi yüklü her sürüm için alt klasörler oluşturur.

5. NuGet Paket bağımlılıklarını gerekli olarak yükler. Bu işlem işleminde, paket sürümlerini açıklandığı güncelleştirebilir [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).

6. Diğer proje dosyaları ve klasörleri güncelleştirin:

    - Projeler için PackageReference, kullanarak depolanan paket bağımlılık grafiği güncelleştirmek `obj/project.assets.json`. Paket içeriğini kendilerini herhangi bir proje klasörüne kopyalanmaz.
    - Güncelleştirme `app.config` ve/veya `web.config` paketi kullanıyorsa [kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md).

7. (Yalnızca visual Studio) Paketin Benioku dosyası varsa, Visual Studio penceresinde görüntüler.

NuGet paketleri ile üretken, kodlamanın keyfini çıkarın!
