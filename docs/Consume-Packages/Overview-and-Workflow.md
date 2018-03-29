---
title: Genel bakış ve NuGet paketleri kullanma iş akışı | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/22/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet paketlerini bir projede işleminin diğer belirli bölümlerine bağlantılar ile kullanma işlemi bir genel bakış.
keywords: NuGet paket tüketim, NuGet tüketim genel bakış, NuGet tüketim iş akışı, paket tüketimi iş akışı, paket tüketimi genel bakış
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e79b09fe8131f25c6bbed650e1927425dcc5d409
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="package-consumption-workflow"></a>Paket tüketimi iş akışı

Nuget.org ve kuruluşunuzun oluşturabilirsiniz özel paket galerileri arasında on binlerce uygulamaları ve Hizmetleri'kullanmak için çok yararlı paketleri bulabilirsiniz. Ancak kaynak bağımsız olarak bir paket tüketen aynı genel iş akışını izler.

![Akış bir paket kaynağına giden, bir paket bulma, projede yükledikten sonra kullanarak bir ekleme deyimi ve paket API çağrıları](media/Overview-01-GeneralFlow.png)

\* _Visual Studio ve dotnet.ex' yalnızca. Nuget yükleme komut proje dosyalarını veya packages.config değiştirmez; Giriş el ile yönetilmesi gerekir._

Daha fazla ayrıntı için bkz: [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md) ve [bir NuGet paketi yüklemek için farklı yollar](ways-to-install-a-package.md).

NuGet ya da kaydı yüklü her paket kimliği ve sürüm numarasını hatırlıyor [ `packages.config` ](../reference/packages-config.md) veya proje dosyası (kullanarak [PackageReference](../consume-packages/package-references-in-project-files.md)) proje türüne bağlı olarak ve NuGet sürümü. Bu Visual Studio yapılandırılabilir olsa da NuGet ile 4.0 +, PackageReference tercih edilen, [Paket Yöneticisi kullanıcı Arabirimi seçenekleri](../tools/package-manager-ui.md). Herhangi bir durumda, bağımlılıkları projeniz için tam listesini görmek için herhangi bir zamanda uygun dosyasında da bakabilirsiniz.

> [!Tip]
> Lisans yazılımınızla kullanmayı düşündüğünüz her paket için her zaman kontrol akıllıca olur. Nuget.org üzerinde bulduğunuz bir **lisans bilgilerini** her paketin açıklaması sayfasının sağ tarafında bağlantı. Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** bağlantı paketi sayfasında. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.

Paketler yüklenirken, NuGet genellikle paket zaten önbelleğinden kullanılabilir olup olmadığını denetler. Bu önbellek komut satırından açıklandığı gibi el ile temizleyebilirsiniz [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).

NuGet Ayrıca paket tarafından desteklenen bir hedef çerçeveyi projenizi ile uyumlu olduğundan emin olur. NuGet paket uyumlu derlemeleri içermiyorsa, bir hata görüntüler. Bkz: [uyumsuz paket hatalarını çözme](dependency-resolution.md#resolving-incompatible-package-errors).

Proje kodunu bir kaynak havuzuna eklerken NuGet paketleri genellikle eklemeyin. Kullanıcılar daha sonra depoyu kopyalayın veya aksi takdirde Visual Studio Team Services gibi sistemlerde derleme aracılarını dahil olmak üzere bu proje elde bir yapı çalıştırılmadan önce gerekli paketleri geri yüklemeniz gerekir:

![Bir depo kopyalama ve bir geri yükleme komutunu kullanarak NuGet paketleri geri akışı](media/Overview-02-RestoreFlow.png)

[Paket geri yükleme](../consume-packages/package-restore.md) proje dosyasındaki bilgileri kullanır veya `packages.config` tüm bağımlılıkları yeniden yüklemek için. Farklar olduğunu işleminde karmaşık açıklandığı gibi unutmayın [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md). Genellikle paketleri otomatik olarak geri yükler ve çözüm düzeyi komutu gösterildiği gibi sağlayan Visual Studio bağlamında zaten olduğunuz konsoluyla olduğundan Ayrıca, yukarıdaki diyagramda restore komutu için Paket Yöneticisi konsolu göstermez .

Bazen bağımlılıkları da yeniden yükleyebilir bir projede zaten dahil edilen paketler yeniden yüklemek gereklidir. Bu kullanarak yapmak kolaydır `nuget reinstall` komut veya NuGet Paket Yöneticisi konsolu. Ayrıntılar için bkz [Reinstalling ve güncelleştirme paketleri](../consume-packages/reinstalling-and-updating-packages.md).

Son olarak, NuGet davranışı tarafından yönlendirilen `Nuget.Config` dosyaları. Birden çok dosya farklı düzeylerde belirli ayarları merkezileştirmek için açıklandığı gibi kullanılabilir [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).

NuGet paketleri, üretken kodlama keyfini çıkarın!
