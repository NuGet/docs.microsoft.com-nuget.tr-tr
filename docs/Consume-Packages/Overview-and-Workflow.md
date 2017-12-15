---
title: "Genel bakış ve NuGet paketleri kullanma iş akışı | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/06/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3c60f920-457d-4f43-9efe-210c514e5242
description: "NuGet paketlerini bir projede işleminin diğer belirli bölümlerine bağlantılar ile kullanma işlemi bir genel bakış."
keywords: "NuGet paket tüketim, NuGet tüketim genel bakış, NuGet tüketim iş akışı, paket tüketimi iş akışı, paket tüketimi genel bakış"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c48351cb6fed0ac94bd437d9443811f46c032bd0
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="package-consumption-workflow"></a>Paket tüketimi iş akışı

Nuget.org ve kuruluşunuzun oluşturabilirsiniz özel paket galerileri arasında on binlerce uygulamaları ve Hizmetleri'kullanmak için çok yararlı paketleri bulabilirsiniz. Ancak kaynak bağımsız olarak bir paket tüketen aynı genel iş akışı aşağıda gösterildiği gibi izler. Ayrıntılar için bkz [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md) ve [paket hızlı başlangıç kullanmak](../quickstart/use-a-package.md).

![Akış bir paket kaynağına giden, bir paket bulma, projede yükledikten sonra kullanarak bir ekleme deyimi ve paket API çağrıları](media/Overview-01-GeneralFlow.png)

\*_İle dışında `nuget install` komut satırından; bu durumda yapılandırmasını düzenlemek için gereken dosyaları el ile. Bkz: [komut başvurusu yüklemek](../tools/cli-ref-install.md)._

NuGet ya da kaydı yüklü her paket kimliği ve sürüm numarasını hatırlıyor `packages.config`, proje dosyası veya `project.json` proje türü ve NuGet sürümüne bağlı olarak, proje kök dosyasında. NuGet 4.0 +, ile [bağımlılıkları proje dosyasında depolamak](../consume-packages/package-references-in-project-files.md) (dışında Windows 10 RS1 hedefleme UWP projeleri) varsayılandır. Herhangi bir durumda, bağımlılıkları projeniz için tam listesini görmek için herhangi bir zamanda uygun dosyasında da bakabilirsiniz.

> [!Tip]
> Lisans yazılımınızla kullanmayı düşündüğünüz her paket için her zaman kontrol akıllıca olur. Nuget.org üzerinde bulabilirsiniz bir **lisans bilgilerini** her paketin açıklaması sayfasının sağ tarafında bağlantı. Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** bağlantı paketi sayfasında. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.

Paketler yüklenirken, NuGet genellikle paket zaten önbelleğinden kullanılabilir olup olmadığını denetler. Bu önbellek komut satırından açıklandığı gibi el ile temizleyebilirsiniz [NuGet önbelleği yönetme](../consume-packages/managing-the-nuget-cache.md).

NuGet Ayrıca paket tarafından desteklenen bir hedef çerçeveyi projenizi ile uyumlu olduğundan emin olur. NuGet paket uyumlu derlemeleri içermiyorsa, bir hata iletisi verecektir. Bkz: [uyumsuz paket hatalarını çözme](dependency-resolution.md#resolving-incompatible-package-errors).

Proje kodunu bir kaynak havuzuna eklerken NuGet paketleri genellikle eklemeyin. Kullanıcılar daha sonra Visual Studio Team Services gibi sistemlerde yapı aracıları içerir, depoyu kopyalama bir yapı çalıştırılmadan önce gerekli paketleri geri yüklemeniz gerekir:

![Bir depo kopyalama ve bir geri yükleme komutunu kullanarak NuGet paketleri geri akışı](media/Overview-02-RestoreFlow.png)

[Paket geri yükleme](../consume-packages/package-restore.md) proje dosyasındaki bilgileri kullanır `packages.config`, `project.json` tüm bağımlılıkları yeniden yüklemek için. Farklar olduğunu işleminde karmaşık açıklandığı gibi unutmayın [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).

Bazen bağımlılıkları da yeniden yükleyebilir bir projede zaten dahil edilen paketler yeniden yüklemek gereklidir. Bu kullanarak yapmak kolaydır `reinstall` NuGet komut satırı veya NuGet Paket Yöneticisi konsolu aracılığıyla komutu. Ayrıntılar için bkz [Reinstalling ve güncelleştirme paketleri](../consume-packages/reinstalling-and-updating-packages.md).

Son olarak, NuGet davranışı tarafından yönlendirilen `Nuget.Config` yapılandırma dosyaları. Birden çok dosya farklı düzeylerde belirli ayarları merkezileştirmek için açıklandığı gibi kullanılabilir [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).

NuGet paketleri, üretken kodlama keyfini çıkarın!
