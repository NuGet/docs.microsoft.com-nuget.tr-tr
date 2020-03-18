---
title: NuGet paketlerini kullanarak genel bakış ve iş akışı
description: Bir projedeki NuGet paketlerini kullanma işlemine genel bakış ve işlemin diğer belirli bölümlerinin bağlantıları.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: ddd1d163e18ed4ce1e7cbf41ed152acc40c1c423
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428886"
---
# <a name="package-consumption-workflow"></a>Paket tüketimi iş akışı

Kuruluşunuzun yapabilmesini sağlayan nuget.org ve özel paket galerileri arasında, uygulamalarınızda ve hizmetleriniz için kullanmak üzere on binlerce çok yararlı paket bulabilirsiniz. Ancak kaynağa bakılmaksızın, bir paket kullanılması aynı genel iş akışını izler.

![Bir paket kaynağına gidip bir paket bulma, bir projeye yükleme, daha sonra bir using ifadesini ve paket API 'sine çağrıları ekleme](media/Overview-01-GeneralFlow.png)

_yalnızca Visual Studio ve `dotnet.exe` \*. `nuget install` komutu proje dosyalarını veya `packages.config` dosyasını değiştirmez; girişlerin el ile yönetilmesi gerekir._

Daha fazla ayrıntı için bkz. [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md) ve [bir paket yüklendiğinde ne olur?](../concepts/package-installation-process.md).

NuGet, yüklü her paketin kimliğini ve sürüm numarasını anımsar, proje türüne ve NuGet sürümünüze bağlı olarak proje dosyasında ( [Packagereference](../consume-packages/package-references-in-project-files.md)kullanarak) veya [`packages.config`](../reference/packages-config.md). NuGet 4.0 + ile, bu, Visual Studio 'da [Paket Yöneticisi Kullanıcı arabirimi](install-use-packages-visual-studio.md)aracılığıyla yapılandırılabilse de, packagereference tercih edilir. Herhangi bir durumda, projeniz için bağımlılıkların tam listesini görmek üzere dilediğiniz zaman uygun dosyaya bakabilirsiniz.

> [!Tip]
> Bu, yazılımınız üzerinde kullanmak istediğiniz her bir pakete ilişkin lisansı her zaman denetleyebilir. Nuget.org 'de, her bir paketin açıklama sayfasının sağ tarafında bir **Lisans bilgisi** bağlantısı bulabilirsiniz. Bir paket lisans koşulları belirtmezse, paket sayfasındaki **kişi sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılarından sizin için herhangi bir fikri mülkiyet hakkı vermez ve üçüncü taraflar tarafından sunulan bilgilerden sorumlu değildir.

Paketler yüklenirken, NuGet genellikle paketin önbelleğinde zaten kullanılabilir olup olmadığını denetler. Bu önbelleği, [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md)bölümünde açıklandığı gibi komut satırından el ile temizleyebilirsiniz.

NuGet Ayrıca, paket tarafından desteklenen hedef çerçevelerin projenizle uyumlu olduğundan da emin olur. Paket uyumlu derlemeler içermiyorsa, NuGet bir hata görüntüler. Bkz. [uyumsuz paket hatalarını çözümleme](../concepts/dependency-resolution.md#resolving-incompatible-package-errors).

Bir kaynak depoya proje kodu eklerken, genellikle NuGet paketleri dahil değildir. Daha sonra depoyu klonlayan veya başka bir şekilde projeyi edinenler, Visual Studio Team Services gibi sistemlerdeki derleme aracıları dahil, bir derlemeyi çalıştırmadan önce gerekli paketleri geri yüklemesi gerekir:

![Bir depoyu kopyalayarak ve bir restore komutu kullanarak NuGet paketlerini geri yükleme akışı](media/Overview-02-RestoreFlow.png)

[Paket geri yükleme](../consume-packages/package-restore.md) , tüm bağımlılıkları yeniden yüklemek için proje dosyasındaki bilgileri kullanır veya `packages.config`. [Bağımlılık çözümlemesi](../concepts/dependency-resolution.md)bölümünde açıklandığı gibi işlemde ilgili farklılıklar olduğunu unutmayın. Ayrıca, Yukarıdaki diyagramda Paket Yöneticisi konsolu için geri yükleme komutu gösterilmez çünkü konsolunuz zaten Visual Studio bağlamında, genellikle paketleri otomatik olarak geri yükler ve çözüm düzeyi komutunu şu şekilde sağlar mekte.

Bazen bir projede zaten bulunan paketleri yeniden yüklemek gerekir, bu da bağımlılıkları yeniden yükleyebilir. Bu, `nuget reinstall` komutu veya NuGet Paket Yöneticisi konsolu kullanılarak kolayca yapılır. Ayrıntılar için bkz. [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md).

Son olarak, NuGet davranışı `Nuget.Config` dosya tarafından çalıştırılır. [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md)bölümünde açıklandığı gibi, farklı düzeylerde belirli ayarları merkezileştirmek için birden çok dosya kullanılabilir.

## <a name="ways-to-install-a-nuget-package"></a>NuGet paketi yüklemeye yönelik yollar

NuGet paketleri, aşağıdaki tablodaki yöntemlerden herhangi birini kullanarak indirilir ve yüklenir.

| Araç | Açıklama |
| --- | --- |
| [DotNet. exe CLı](install-use-packages-dotnet-cli.md) | (Tüm platformlar) .NET Core ve .NET Standard kitaplıkları için CLı aracı ve .NET Framework hedefi olan SDK stili projeler için (bkz. [SDK özniteliği](/dotnet/core/tools/csproj#additions)). \<package_name\> tarafından tanımlanan paketi alır ve proje dosyasına bir başvuru ekler. Ayrıca bağımlılıkları alır ve kurar. |
| {1&gt;Visual Studio&lt;1} | (Windows ve Mac) , Paketleri ve bağımlılıklarını belirtilen bir paket kaynağından bir projeye göz atabilmeniz, seçebileceğiniz ve yükleyebileceğiniz bir kullanıcı arabirimi sağlar. Proje dosyasına yüklenen paketlere başvurular ekler.<ul><li>[Visual Studio kullanarak paketleri yükleyip yönetme](install-use-packages-visual-studio.md)</li><li>[Projenize NuGet paketi ekleme (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| [Paket Yöneticisi Konsolu (Visual Studio)](install-use-packages-powershell.md) | (Yalnızca Windows) \<package_name\> tarafından tanımlanan paketi seçili bir kaynaktan çözümdeki belirli bir projeye alır ve ekler, sonra proje dosyasına bir başvuru ekler. Ayrıca bağımlılıkları alır ve kurar. |
| [nuget.exe CLI](install-use-packages-nuget-cli.md) | (Tüm platformlar) .NET Standard kitaplıklarını hedefleyen .NET Framework kitaplıkları ve SDK olmayan projeler için CLı aracı. \<package_name\> tarafından tanımlanan paketi alır ve içeriğini geçerli dizindeki bir klasöre genişletir; , bir `packages.config` dosyasında listelenen tüm paketleri de alabilir. Ayrıca bağımlılıkları alır ve kurar, ancak proje dosyalarında veya `packages.config`hiçbir değişiklik yapmaz. |
