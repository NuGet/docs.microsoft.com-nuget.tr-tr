---
title: Kendi NuGet akışlarınızı barındırma genel bakış
description: Yerel olarak veya uzaktan kendi NuGet paket akışları veya galeriler barındırmak için açılır genel bakış.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f05c3a7a51bdc0760097422004cfc4339bf9ee2c
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426603"
---
# <a name="hosting-your-own-nuget-feeds"></a>Barındırma kendi NuGet akışları

Paketleri herkese yapmak yerine, paketleri yalnızca sınırlı bir hedef kitle için kuruluşunuz veya çalışma grubu gibi serbest bırakmak isteyebilirsiniz. Ayrıca, bazı şirketler, hangi üçüncü taraf kitaplıkların geliştiricileri kullanın ve bu nedenle bir sınırlı paket kaynağı nuget.org yerine çizmek için bu geliştiriciler doğrudan sınırlamak isteyebilirsiniz.

Tüm bu amaçlarla NuGet aşağıdaki yollarla özel paket kaynaklarını ayarlamayı destekler:

- Yerel akış: Paketler, ideal olarak kullanarak bir uygun bir ağ dosya paylaşımında, yalnızca yerleştirilir `nuget init` ve `nuget add` hiyerarşik klasör yapısı (NuGet 3.3 +) oluşturmak için. Ayrıntılar için bkz [yerel akışları](../hosting-packages/local-feeds.md).
- NuGet.Server: Paketler, yerel bir HTTP sunucusu sunulur. Ayrıntılar için bkz [NuGet.Server](../hosting-packages/nuget-server.md).
- NuGet Galerisi: Paketler, bir sunucu kullanarak Internet üzerinde barındırıldığı [NuGet Galerisi proje](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com). NuGet Galerisi, kullanıcı yönetimi ve kapsamlı bir web araması yapın ve paketleri nuget.org için benzer ve tarayıcıdaki keşfetmeye sağlayan kullanıcı Arabirimi gibi özellikleri sağlar.

Aşağıdakiler dahil olmak üzere uzaktan özel akışlarını destekleyen ürünleri barındırma birkaç NuGet vardır:

- [Azure yapılarını](https://www.visualstudio.com/docs/package/nuget/publish), olduğu da kullanılabilir Team Foundation Server 2017 ve üzeri.
- [MyGet](http://myget.org)
- [ProGet](http://inedo.com/proget) Inedo gelen
- [GitHub paketini kayıt defteri](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [NuGet sunucusu](http://nugetserver.net/), Inedo topluluk projeden
- [NuGet sunucusu (açık kaynak)](http://nuget-server.net), Inedo'nın NuGet sunucusu için benzer bir açık kaynak uygulama
- [LiGet](https://github.com/ai-traders/liget), açık kaynak uygulaması kestrel docker'da çalışan NuGet V2 sunucusu
- [BaGet](https://github.com/loic-sharma/BaGet), ASP.NET Core üzerine yapılandırılan NuGet V3 sunucusu açık kaynak uygulaması
- [Sleet](https://github.com/emgarten/sleet), bir açık kaynak NuGet V3 statik Oluşturucu akışı
- [Artifactory](https://www.jfrog.com/artifactory/) JFrog öğesinden.
- [Nexus](http://www.sonatype.org/nexus/) Sonatype öğesinden.
- [TeamCity](https://www.jetbrains.com/teamcity/) JetBrains öğesinden.

Paketleri nasıl barındırılan bağımsız olarak, kullanılabilir kaynakları listesine ekleyerek erişim `NuGet.Config`. Bu Visual Studio içinde açıklanan şekilde yapılabilir [paket kaynaklarını](../tools/package-manager-ui.md#package-sources), veya komut satırı kullanarak [ `nuget sources` ](../tools/cli-ref-sources.md). Bir kaynak yolu bir yerel klasör yol adı, bir ağ adı veya bir URL olabilir.
