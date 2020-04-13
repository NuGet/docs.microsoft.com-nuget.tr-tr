---
title: NuGet paketlerini kullanmanın genel bakışı ve iş akışı
description: Projenin diğer belirli bölümlerine bağlantılar içeren nuget paketlerini bir projede tüketme sürecine genel bir bakış.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428886"
---
# <a name="package-consumption-workflow"></a>Paket tüketim iş akışı

Kuruluşunuzun oluşturabileceği nuget.org ve özel paket galerileri arasında, uygulamalarınızda ve hizmetlerinizde kullanmak üzere on binlerce son derece kullanışlı paket bulabilirsiniz. Ancak kaynak ne olursa olsun, bir paketi tüketmek aynı genel iş akışını izler.

![Paket kaynağına gitme, paket bulma, projeye yükleme, ardından kullanma deyimi ekleme ve paket API'sine çağrı ekleme akışı](media/Overview-01-GeneralFlow.png)

\*_Visual Studio `dotnet.exe` ve sadece. Komut `nuget install` proje dosyalarını veya `packages.config` dosyayı değiştirmez; girişler el ile yönetilmelidir._

Daha fazla bilgi için, [Paketleri Bulma ve Seçme](../consume-packages/finding-and-choosing-packages.md) ve Paket [yüklendiğinde ne olur'a bakın.](../concepts/package-installation-process.md)

NuGet, yüklenen her paketin kimlik ve sürüm numarasını hatırlar, proje dosyasına [(PackageReference](../consume-packages/package-references-in-project-files.md)kullanarak) veya [`packages.config`](../reference/packages-config.md)proje türüne ve NuGet sürümünüze bağlı olarak kaydeder. NuGet 4.0+ ile PackageReference tercih edilir, ancak bu [Paket Yöneticisi UI](install-use-packages-visual-studio.md)aracılığıyla Visual Studio'da yapılandırılabilir. Her durumda, projenizin bağımlılıklarının tam listesini görmek için istediğiniz zaman ilgili dosyaya bakabilirsiniz.

> [!Tip]
> Yazılımınızda kullanmak istediğiniz her paketin lisansını her zaman kontrol etmek akıllıca olur. nuget.org, her paketin açıklama sayfasının sağ tarafında bir **Lisans Bilgileri** bağlantısı bulabilirsiniz. Bir paket lisans koşullarını belirtmiyorsa, paket sayfasındaki **İlgili Kişi sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılardan size herhangi bir fikri mülkiyet lisansı vermez ve üçüncü taraflarca sağlanan bilgilerden sorumlu değildir.

Paketleri yüklerken, NuGet genellikle paketin önbelleğinden zaten kullanılabilir olup olmadığını denetler. Bu önbelleği, [genel paketleri ve önbellek klasörlerini yönetmede](../consume-packages/managing-the-global-packages-and-cache-folders.md)açıklandığı gibi komut satırından el ile temizleyebilirsiniz.

NuGet ayrıca paket tarafından desteklenen hedef çerçevelerin projenizle uyumlu olmasını sağlar. Paket uyumlu derlemeler içermiyorsa, NuGet bir hata görüntüler. Bkz. [Uyumsuz paket hatalarını çözme.](../concepts/dependency-resolution.md#resolving-incompatible-package-errors)

Bir kaynak deposuna proje kodu eklerken, genellikle NuGet paketlerini içermezsiniz. Daha sonra depoyu klonlayan veya Visual Studio Team Services gibi sistemlerde yapı aracıları da dahil olmak üzere projeyi başka bir şekilde satın alanlar, bir yapıyı çalıştırmadan önce gerekli paketleri geri yüklemelidir:

![Bir depoklonlayarak ve geri yükleme komutunu kullanarak NuGet paketlerini geri yükleme akışı](media/Overview-02-RestoreFlow.png)

[Paket Geri Yükleme,](../consume-packages/package-restore.md) proje dosyasındaki bilgileri veya `packages.config` tüm bağımlılıkları yeniden yüklemek için kullanır. [Bağımlılık Çözümü'nde](../concepts/dependency-resolution.md)açıklandığı gibi, ilgili süreçte farklılıklar olduğunu unutmayın. Ayrıca, yukarıdaki diyagram Da Paket Yöneticisi Konsolu için bir geri yükleme komutu göstermez, çünkü Konsol'daysanız, genellikle paketleri otomatik olarak geri yükleyen ve gösterildiği gibi çözüm düzeyi komutunu sağlayan Visual Studio bağlamında zaten bulunuyorsunuz.

Bazen, zaten projeye dahil edilmiş olan ve bağımlılıkları yeniden yükleyebilecek paketleri yeniden yüklemek gerekir. Bu `nuget reinstall` komutu veya NuGet Paket Yöneticisi Konsolu kullanarak yapmak kolaydır. Ayrıntılar için [Paketleri Yeniden Yükleme ve Güncelleştirme'ye](../consume-packages/reinstalling-and-updating-packages.md)bakın.

Son olarak, NuGet'in `Nuget.Config` davranışı dosyalar tarafından yönlendirilir. [NuGet Davranışını Yapılandırmada](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi, farklı düzeylerde belirli ayarları merkezileştirmek için birden çok dosya kullanılabilir.

## <a name="ways-to-install-a-nuget-package"></a>NuGet Paketi yüklemenin yolları

NuGet paketleri aşağıdaki tablodaki yöntemlerden herhangi biri kullanılarak indirilir ve yüklenir.

| Araç | Açıklama |
| --- | --- |
| [dotnet.exe CLI](install-use-packages-dotnet-cli.md) | (Tüm platformlar) .NET Core ve .NET Standart kitaplıkları ve .NET Framework'ü hedefleyen SDK tarzı projeler için CLI aracı (bkz. [SDK özniteliği).](/dotnet/core/tools/csproj#additions) package_name \<\> tarafından tanımlanan paketi alır ve proje dosyasına bir başvuru ekler. Ayrıca bağımlılıkları alır ve yükler. |
| Visual Studio | (Windows ve Mac) Belirli bir paket kaynağından paketlere ve bunların bağımlılıklarına göz atabileceğiniz, seçebileceğiniz ve yükleyebileceğiniz bir kullanıcı arama aracı sağlar. Yüklü paketlere başvurular proje dosyasına ekler.<ul><li>[Visual Studio'u kullanarak paketleri yükleyin ve yönetin](install-use-packages-visual-studio.md)</li><li>[Projenize bir NuGet paketi (Mac) dahil](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Paket Yöneticisi Konsolu (Visual Studio)](install-use-packages-powershell.md) | (Yalnızca Windows) Package_name \<\> tarafından tanımlanan paketi seçili bir kaynaktan çözümde belirli bir projeye alır ve yükler, ardından proje dosyasına bir başvuru ekler. Ayrıca bağımlılıkları alır ve yükler. |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | (Tüm platformlar) .NET Framework kitaplıkları ve .NET Standart kitaplıklarını hedefleyen SDK tarzı olmayan projeler için CLI aracı. package_name \<\> tarafından tanımlanan paketi alır ve içeriğini geçerli dizindeki bir klasöre genişletir; bir `packages.config` dosyada listelenen tüm paketleri de alabilir. Ayrıca bağımlılıkları alır ve yükler, ancak proje dosyalarında veya `packages.config`. |
