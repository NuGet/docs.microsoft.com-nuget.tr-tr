---
title: NuGet paketlerini yükleme yolu
description: Geçerli proje dosyaları ve diskte ne de dahil olmak üzere, bir projeye NuGet paketlerini yükleme işlemi açıklanır.
author: karann-msft
ms.author: karann
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 3cb3d5f97e9fb7ce292ddc5a95b61c13f64a17e7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547672"
---
# <a name="different-ways-to-install-a-nuget-package"></a>Bir NuGet paketini yüklemek için farklı yollar

NuGet paketlerini indirilir ve aşağıdaki tabloda yöntemlerden birini kullanarak yüklü (bkz [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md) Bunlar zaten yüklü yoksa). Paket bir önbellekten alınabilir yerine indirilir.

| Yöntem | Açıklama |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (Tüm platformlar) Tarafından tanımlanan paket alır \<package_name\>içeriğini geçerli dizin bir klasörde genişletir ve proje dosyasına bir başvuru ekler. Ayrıca alır ve bağımlılıkları yükler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[DotNet paketi komut ekleme](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Paket Yöneticisi UI (Visual Studio) | (Windows ve Mac) Bir kullanıcı Arabirimi üzerinden göz atabilir, seçin ve belirtilen paket kaynağı bir projeden paketler ve bağımlılıkları yükleme sağlar. Yüklü paketleri başvuruları proje dosyasına ekler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi kullanıcı Arabirimi başvurusu (Windows)](../tools/package-manager-ui.md)</li><li>[Bir NuGet paketini projenize (Mac) dahil olmak üzere](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Paket Yöneticisi Konsolu (Visual Studio)<br/>`Install-Package <package_name>` | (Yalnızca Windows) Alır ve tarafından tanımlanan paket yükler \<package_name\> çözümde belirtilen projesine seçili kaynaktan ardından proje dosyasına bir başvuru ekler. Ayrıca alır ve bağımlılıkları yükler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi konsolu Kılavuzu](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (Tüm platformlar) Tarafından tanımlanan paket alır \<package_name\> ve içeriğini geçerli dizin bir klasörde genişletir; listelenen tüm paketleri de alabilirsiniz bir `packages.config` dosya. Ayrıca alır ve bağımlılıkları yükler, ancak proje dosyaları için hiçbir değişiklik yapar veya `packages.config`.<ul><li>[Yükleme komutu](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Bir paketi yüklendiğinde ne olur

Kısaca, farklı NuGet araçları genellikle bir pakete bir başvuru proje dosyasında oluşturma veya `packages.config`, ardından etkili bir şekilde paket yükleyen bir paket geri yükleme gerçekleştirin. Özel durum `nuget install`, hangi yalnızca genişletir pakete bir `packages` klasör ve diğer dosyaları değiştirmez.

Genel süreç aşağıdaki gibidir:

1. (Tüm araçlar dışında `nuget.exe`) sürümü ve paket tanımlayıcısı proje dosyasına kaydedin veya `packages.config`.

2. Paket Al:
   - İçinde paket (tam tanımlayıcı ve sürüm numarası tarafından) önceden yüklenip yüklenmediğini denetlemek *genel paketleri* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md).

   - Paketin içinde değilse *genel paketleri* klasörü, onu listelenen kaynaklarından listelenen alma denemesi [yapılandırma dosyalarını](Configuring-NuGet-Behavior.md). Çevrimiçi kaynaklar için ilk paketi önbellekten sürece alma denemesi `-NoCache` ile belirtilen `nuget.exe` komutları veya `--no-cache` ile belirtilen `dotnet restore`. (Visual Studio ve `dotnet add package` her zaman önbelleğe kullanın.) Bir paket önbellekten kullanılan "ÖNBELLEK" çıktısında görüntülenir. Önbellek sona erme süresini 30 dakika vardır.

   - Paket önbellekte değilse yapılandırmasında listelenen kaynaklardan indirme girişimi. Bir paket yüklediyseniz, "GET" ve "Tamam" çıkışında görüntülenir.

   - Paket başarıyla tüm kaynaklardan gelen alınamıyor, yükleme bir hata ile bu noktada gibi başarısız [NU1103](../reference/errors-and-warnings/NU1103.md). Not Bu hatalardan `nuget.exe` komutları göster yalnızca son kaynak işaretli, ancak gelir paket herhangi bir kaynaktan kullanılabilir durumda.

   Paket alırken, kaynakları NuGet yapılandırma sırasını uygulanabilir:

   - PackageReference biçimini kullanan projeler için NuGet HTTP kaynakları denetlemeden önce kaynakları yerel klasörü ve ağ paylaşımlara denetler.

   - Kullanarak projeleri için `packages.config` yönetim biçimi, NuGet sırayı yapılandırmasında kaynakları kullanır. Bu durumda kaynak sırası göz ardı geri yükleme işlemleri, bir özel durumdur ve NuGet paketi'nın hangi kaynak yanıt kullanır.

   - Genel olarak, herhangi belirli bir paket belirli bir tanımlayıcı ve sürüm numarası ile tam olarak hangi kaynak anlaşıldığında aynı olduğu için NuGet kaynakları denetleyen sırası özellikle anlamlı değildir.

3. (Dışındaki tüm araçları `nuget.exe`) bir paket ve diğer bilgileri kaydetmek *http önbellek* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](managing-the-global-packages-and-cache-folders.md).

4. İndirdiyseniz, paketi, kullanıcı başına yükleyin. *genel paketleri* klasör. NuGet, her paket tanımlayıcısı için bir alt klasör oluşturur ve ardından paketi yüklü her sürüm için alt klasörler oluşturur.

5. Diğer proje dosyaları ve klasörleri güncelleştirin:

    - Projeler için PackageReference, kullanarak depolanan paket bağımlılık grafiği güncelleştirmek `obj/project.assets.json`. Paket içeriğini kendilerini herhangi bir proje klasörüne kopyalanmaz.
    - Kullanarak projeleri için `packages.config`, projenin hedef çerçeve proje eşleşen genişletilmiş paketi parçaları kopyalama `packages` klasör. (Kullanırken `nuget install`, tüm genişletilmiş paketi kopyalanamadı çünkü `nuget.exe` hedef Framework'ü tanımlamak için proje dosyaları incelemez.)
    - Güncelleştirme `app.config` ve/veya `web.config` paketi kullanıyorsa [kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md).

6. Tüm alt düzey bağımlılıkları yüklemek zaten projede mevcut değilse. Bu işlem işleminde, paket sürümlerini açıklandığı güncelleştirebilir [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).

7. (Yalnızca visual Studio) Paketin Benioku dosyası varsa, Visual Studio penceresinde görüntüler.

## <a name="related-articles"></a>İlgili makaleler

- [Genel bakış ve paket tüketim iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [NuGet önbelleğini ve genel paketleri klasörleri yönetme](managing-the-global-packages-and-cache-folders.md)
- [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md)
