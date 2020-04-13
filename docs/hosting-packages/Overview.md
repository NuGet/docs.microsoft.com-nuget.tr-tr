---
title: Kendi NuGet Feed'lerinizi Barındırmaya Genel Bakış
description: Kendi NuGet paket akışlarınızı veya galerilerinizi yerel veya uzaktan barındırmak için açılır.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 81acf15ac69d78d39d2784e77c18ba38bfea126d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385548"
---
# <a name="hosting-your-own-nuget-feeds"></a>Kendi NuGet akışlarınızı barındırma

Paketleri herkese açık hale getirmek yerine, paketleri kuruluşunuz veya çalışma grubunz gibi yalnızca sınırlı bir kitleye serbest bırakmak isteyebilirsiniz. Buna ek olarak, bazı şirketler geliştiricilerin kullanabileceği üçüncü taraf kitaplıklarını kısıtlamak ve böylece bu geliştiricileri nuget.org yerine sınırlı bir paket kaynağından çizim yapmaya yönlendirmek isteyebilir.

Tüm bu amaçlar için, NuGet özel paket kaynaklarının kurulmasını aşağıdaki yollarla destekler:

- Yerel özet akışı: Paketler ideal olarak kullanarak `nuget init` ve `nuget add` hiyerarşik bir klasör yapısı (NuGet 3.3+) oluşturmak için uygun bir ağ dosyası paylaşımına yerleştirilir. Ayrıntılar için [Yerel Özet Akışları'na](../hosting-packages/local-feeds.md)bakın.
- NuGet.Server: Paketler yerel bir HTTP sunucusu aracılığıyla kullanılabilir hale getirilir. Ayrıntılar için [NuGet.Server'a](../hosting-packages/nuget-server.md)bakın.
- NuGet Galerisi: [Paketler, NuGet Galeri Projesi](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) kullanılarak bir Internet sunucusunda barındırılır. NuGet Gallery, nuget.org benzer şekilde tarayıcı nın içinden paketleri aramave keşfetmeye olanak tanıyan kapsamlı bir web kullanıcı arabirimi gibi kullanıcı yönetimi ve özellikler sağlar.

Azure [Yapıları](https://www.visualstudio.com/docs/package/nuget/publish) ve [GitHub paket kayıt defteri](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) gibi uzak özel akışları destekleyen birkaç nuget barındırma ürünü de vardır. Aşağıda bu tür ürünlerin bir listesi:

- [JFrog'dan artifactory.](https://www.jfrog.com/artifactory/)
- Team Foundation Server 2017 ve sonrası için de kullanılabilen [Azure Yapıları.](https://www.visualstudio.com/docs/package/nuget/publish)
- [BaGet](https://github.com/loic-sharma/BaGet), NuGet V3 sunucusunun ASP.NET Core üzerine kurulu açık kaynak uygulaması
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), tam yönetilen paket yönetimi SaaS
- [GitHub paket kayıt defteri](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), NuGet V2 sunucusunun docker'da kerkenez üzerinde çalışan açık kaynak uygulaması
- [MyGet](https://myget.org)
- [Sonatype'tan Nexus Deposu OSS.](https://www.sonatype.com/nexus-repository-oss)
- [NuGet Server (Açık Kaynak)](https://github.com/svenkle/nuget-server), Inedo'nun NuGet Server'ına benzer bir açık kaynak uygulaması
- [NuGet Server](http://nugetserver.net/), Inedo'dan bir topluluk projesi
- Inedo'dan [ProGet](https://inedo.com/proget)
- [Sleet](https://github.com/emgarten/sleet), açık kaynak kodlu NuGet V3 statik besleme jeneratörü
- JetBrains'ten [TeamCity.](https://www.jetbrains.com/teamcity/)

Paketler nasıl barındırılırsa barındırılır, bunları kullanılabilir kaynaklar listesine `NuGet.Config`ekleyerek bunlara erişebilirsiniz. Bu, [Paket Kaynakları'nda](../consume-packages/install-use-packages-visual-studio.md#package-sources)açıklandığı gibi Visual Studio'da [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)veya komut satırından Bir kaynağa giden yol yerel klasör yol adı, ağ adı veya URL olabilir.
