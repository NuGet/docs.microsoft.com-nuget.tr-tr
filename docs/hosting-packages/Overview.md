---
title: Kendi NuGet akışlarını barındırma genel bakış
description: Yerel olarak veya uzaktan kendi NuGet paketi akışlarını veya galerileri barındırmak için açılır genel bakış.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 48ebddb26aa6c236609691e099a82db80075944e
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818431"
---
# <a name="hosting-your-own-nuget-feeds"></a>Kendi NuGet barındırma akışları

Paketleri genel olarak kullanılabilir hale getirme yerine, yalnızca bir sınırlı kitleye, kuruluşunuz ya da çalışma grubu gibi paketleri yayın isteyebilirsiniz. Ayrıca, bazı şirketler kendi geliştiriciler kullanın ve bu nedenle bir sınırlı paket kaynağı nuget.org yerine çizmek için bu geliştiriciler doğrudan hangi üçüncü taraf kitaplıklar sınırlamak isteyebilirsiniz.

Bu tür amacıyla, NuGet aşağıdaki yollarla özel paket kaynaklarını ayarlama destekler:

- Yerel akışı: paketler yalnızca yerleştirilir uygun ağ dosya paylaşımında ideal olarak kullanarak `nuget init` ve `nuget add` hiyerarşik bir klasör yapısı (NuGet 3.3 +) oluşturmak için. Ayrıntılar için bkz [yerel akışları](../hosting-packages/local-feeds.md).
- NuGet.Server: Paketleri yerel bir HTTP sunucu üzerinden kullanılabilir hale getirilir. Ayrıntılar için bkz [NuGet.Server](../hosting-packages/nuget-server.md).
- NuGet galerisinde: Bir sunucu kullanarak Internet üzerindeki paketler barındırılan [NuGet Galerisi projesi](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com'u). NuGet galerisinde, kullanıcı yönetimi ve kapsamlı bir web arama ve paketlerinden nuget.org için benzer tarayıcısından keşfetme veren UI gibi özellikler sağlar.

Ayrıca, aşağıdakiler de dahil olmak üzere uzaktan özel akışları destekleyen ürünleri barındırma birkaç NuGet vardır:

- [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), olduğu da Team Foundation Server 2017 kullanılabilir ve sonraki sürümleri.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) Inedo gelen
- [NuGet sunucu](http://nugetserver.net/), Inedo topluluk projeden
- [NuGet sunucu (kaynak açın)](http://nuget-server.net), Inedo'nın NuGet sunucuya benzer bir açık kaynak uygulaması
- [Artifactory](https://www.jfrog.com/artifactory/) JFrog gelen.
- [Nexus](http://www.sonatype.org/nexus/) Sonatype gelen.
- [TeamCity](https://www.jetbrains.com/teamcity/) JetBrains gelen.

Paketleri nasıl barındırılan bağımsız olarak, kullanılabilir kaynakları listesine ekleyerek erişmesine `NuGet.Config`. Bu Visual Studio'da açıklandığı gibi yapılabilir [paket kaynaklarını](../tools/package-manager-ui.md#package-sources), veya kullanarak komut satırından [ `nuget sources` ](../tools/cli-ref-sources.md). Bir kaynak yolu, bir yerel klasör yol, bir ağ adı veya bir URL olabilir.
