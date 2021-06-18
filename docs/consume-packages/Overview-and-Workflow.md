---
title: NuGet paketlerini kullanarak genel bakış ve iş akışı
description: Bir projedeki NuGet paketlerini kullanma işlemine genel bakış ve işlemin diğer belirli bölümlerinin bağlantıları.
author: JonDouglas
ms.author: jodou
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: d1d6df3bcc36d8a78fcee97099b301c9ffc440d9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323641"
---
# <a name="package-consumption-workflow"></a>Paket tüketimi iş akışı

Kuruluşunuzun yapabilmesini sağlayan nuget.org ve özel paket galerileri arasında, uygulamalarınızda ve hizmetleriniz için kullanmak üzere on binlerce çok yararlı paket bulabilirsiniz. Ancak kaynağa bakılmaksızın, bir paket kullanılması aynı genel iş akışını izler.

![Bir paket kaynağına gidip bir paket bulma, bir projeye yükleme, daha sonra bir using ifadesini ve paket API 'sine çağrıları ekleme](media/Overview-01-GeneralFlow.png)

\*_Yalnızca Visual Studio ve `dotnet.exe` . `nuget install`Komut proje dosyalarını veya `packages.config` dosyayı değiştirmez; girişlerin el ile yönetilmesi gerekir._

Daha fazla ayrıntı için bkz. [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md) ve [bir paket yüklendiğinde ne olur?](../concepts/package-installation-process.md).

NuGet, yüklü her paketin kimliğini ve sürüm numarasını anımsar, proje dosyasında ( [Packagereference](../consume-packages/package-references-in-project-files.md)kullanılarak) veya [`packages.config`](../reference/packages-config.md) proje türüne ve NuGet sürümünüze bağlı olarak bu paket. NuGet 4.0 + ile, bu, Visual Studio 'da [Paket Yöneticisi Kullanıcı arabirimi](install-use-packages-visual-studio.md)aracılığıyla yapılandırılabilse de, packagereference tercih edilir. Herhangi bir durumda, projeniz için bağımlılıkların tam listesini görmek üzere dilediğiniz zaman uygun dosyaya bakabilirsiniz.

> [!Tip]
> Bu, yazılımınız üzerinde kullanmak istediğiniz her bir pakete ilişkin lisansı her zaman denetleyebilir. Nuget.org 'de, her bir paketin açıklama sayfasının sağ tarafında bir **Lisans bilgisi** bağlantısı bulabilirsiniz. Bir paket lisans koşulları belirtmezse, paket sayfasındaki **kişi sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılarından sizin için herhangi bir fikri mülkiyet hakkı vermez ve üçüncü taraflar tarafından sunulan bilgilerden sorumlu değildir.

Paketler yüklenirken, NuGet genellikle paketin önbelleğinde zaten kullanılabilir olup olmadığını denetler. Bu önbelleği, [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md)bölümünde açıklandığı gibi komut satırından el ile temizleyebilirsiniz.

NuGet Ayrıca, paket tarafından desteklenen hedef çerçevelerin projenizle uyumlu olduğundan da emin olur. Paket uyumlu derlemeler içermiyorsa, NuGet bir hata görüntüler. Bkz. [uyumsuz paket hatalarını çözümleme](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Bir kaynak depoya proje kodu eklerken, genellikle NuGet paketleri dahil değildir. Daha sonra depoyu klonlayan veya başka bir şekilde projeyi edinenler, Visual Studio Team Services gibi sistemlerdeki derleme aracıları dahil, bir derlemeyi çalıştırmadan önce gerekli paketleri geri yüklemesi gerekir:

![Bir depoyu kopyalayarak ve bir restore komutu kullanarak NuGet paketlerini geri yükleme akışı](media/Overview-02-RestoreFlow.png)

[Paket geri yükleme](../consume-packages/package-restore.md) , proje dosyasındaki bilgileri kullanır veya `packages.config` tüm bağımlılıkları yeniden yükler. [Bağımlılık çözümlemesi](../concepts/dependency-resolution.md)bölümünde açıklandığı gibi işlemde ilgili farklılıklar olduğunu unutmayın. Ayrıca, Yukarıdaki diyagramda Paket Yöneticisi konsolu için geri yükleme komutu gösterilmez çünkü konsolunuz zaten Visual Studio bağlamında, genellikle paketleri otomatik olarak geri yükler ve gösterildiği gibi çözüm düzeyi komut sağlar.

Bazen bir projede zaten bulunan paketleri yeniden yüklemek gerekir, bu da bağımlılıkları yeniden yükleyebilir. Bu, `nuget reinstall` komutu veya NuGet Paket Yöneticisi konsolunu kullanarak kolayca yapılır. Ayrıntılar için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md).

Son olarak, NuGet davranışı dosyalar tarafından çalıştırılır `NuGet.Config` . [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md)bölümünde açıklandığı gibi, farklı düzeylerde belirli ayarları merkezileştirmek için birden çok dosya kullanılabilir.

## <a name="ways-to-install-a-nuget-package"></a>NuGet paketi yüklemeye yönelik yollar

NuGet paketleri, aşağıdaki tablodaki yöntemlerden herhangi birini kullanarak indirilir ve yüklenir.

| Araç | Platformlar | Açıklama |
| --- | --- | --- |
| [dotnet CLI](install-use-packages-dotnet-cli.md) | Tümü | .NET Core ve .NET Standard kitaplıkları için CLı aracı ve .NET Framework hedefi olan SDK stili projeler için (bkz. [SDK özniteliği](/dotnet/core/tools/csproj#additions)). Tarafından tanımlanan paketi alır \<package_name\> ve proje dosyasına bir başvuru ekler. Ayrıca bağımlılıkları alır ve kurar. |
| Visual Studio | Windows ve Mac | , Paketleri ve bağımlılıklarını belirtilen bir paket kaynağından bir projeye göz atabilmeniz, seçebileceğiniz ve yükleyebileceğiniz bir kullanıcı arabirimi sağlar. Proje dosyasına yüklenen paketlere başvurular ekler.<ul><li>[Visual Studio kullanarak paketleri yükleyip yönetme](install-use-packages-visual-studio.md)</li><li>[Projenize NuGet paketi ekleme (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Paket Yöneticisi Konsolu (Visual Studio)](install-use-packages-powershell.md) | Yalnızca Windows | \<package_name\>Seçilen bir kaynaktan tarafından tanımlanan paketi çözümdeki belirli bir projeye alır ve ekler, ardından proje dosyasına bir başvuru ekler. Ayrıca bağımlılıkları alır ve kurar. |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | Tümü | .NET Standard kitaplıklarını hedefleyen .NET Framework kitaplıkları ve SDK olmayan projeler için CLı aracı. Tarafından tanımlanan paketi alır \<package_name\> ve içeriğini geçerli dizindeki bir klasöre genişletir; Ayrıca, bir dosyada listelenen tüm paketleri de alabilir `packages.config` . Ayrıca bağımlılıkları alır ve kurar, ancak proje dosyalarında veya hiçbir değişiklik yapmaz `packages.config` . |
