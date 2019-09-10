---
title: Kendi NuGet akışlarınızı barındırılmasına genel bakış
description: Kendi NuGet paket akışlarınızı veya galerinizi yerel olarak veya uzaktan barındırmak için açılan bir genel bakış.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 10651e2cc26f7df4115e4de5dac8c91c93af7374
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815295"
---
# <a name="hosting-your-own-nuget-feeds"></a>Kendi NuGet akışlarınızı barındırma

Paketleri genel kullanıma hazır hale getirmek yerine, paketleri yalnızca kuruluşunuz veya çalışma grubunuz gibi sınırlı bir hedef kitleye serbest bırakmak isteyebilirsiniz. Ayrıca, bazı şirketler geliştiricilerin hangi üçüncü taraf kitaplıklarını kullandığını kısıtlamak ve böylece bu geliştiricilerin nuget.org yerine sınırlı bir paket kaynağından çizim yapmak isteyebilir.

NuGet, bu gibi tüm amaçlar için özel paket kaynaklarını aşağıdaki yollarla ayarlamayı destekler:

- Yerel akış: Paketler, bir hiyerarşik klasör yapısı (NuGet 3.3 +) oluşturmak için `nuget init` ve `nuget add` kullanarak ideal bir ağ dosya paylaşımında yer alır. Ayrıntılar için bkz. [Yerel akışlar](../hosting-packages/local-feeds.md).
- NuGet. Server: Paketler yerel bir HTTP sunucusu üzerinden kullanılabilir hale getirilir. Ayrıntılar için bkz. [NuGet. Server](../hosting-packages/nuget-server.md).
- NuGet Galerisi: Paketler, [NuGet Galeri projesi](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com) kullanılarak bir Internet sunucusunda barındırılır. NuGet Galerisi, nuget.org benzer şekilde, tarayıcı içinden paket aramaya ve keşfetmeye izin veren kapsamlı bir Web Kullanıcı arabirimi gibi Kullanıcı yönetimi ve özellikler sağlar.

Ayrıca, uzak özel akışları destekleyen [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) ve [GitHub paket kayıt defteri](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry) gibi diğer çeşitli NuGet barındırma ürünleri de vardır. Bu tür ürünlerin listesi aşağıda verilmiştir:

- JFrog 'den [Artifactory](https://www.jfrog.com/artifactory/) .
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), Team Foundation Server 2017 ve sonraki sürümlerde de kullanılabilir.
- [Baget](https://github.com/loic-sharma/BaGet), NuGet v3 sunucusunun açık kaynaklı ASP.NET Core yerleşik bir uygulamasıdır
- Tam olarak yönetilen bir paket yönetimi SaaS olan [Cloudsmith](https://cloudsmith.io/l/nuget-feed/)
- [GitHub paket kayıt defteri](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- Docker 'da Kestrel üzerinde çalışan NuGet v2 sunucusunun açık kaynaklı bir uygulama olan [Liget](https://github.com/ai-traders/liget)
- [MyGet](http://myget.org)
- Sonatype 'dan [Nexus](http://www.sonatype.org/nexus/) .
- Inedo 'ın NuGet sunucusuna benzer bir açık kaynaklı uygulama olan [NuGet sunucusu (açık kaynak)](http://nuget-server.net)
- Inedo 'dan bir topluluk projesi olan [NuGet sunucusu](http://nugetserver.net/)
- Inedo 'dan [temin edin](http://inedo.com/proget)
- Açık kaynaklı bir NuGet v3 statik akış Oluşturucu olan [uyma](https://github.com/emgarten/sleet)
- JetBrains 'den [TeamCity](https://www.jetbrains.com/teamcity/) .

Paketlerin nasıl barındırıldığından bağımsız olarak, ' deki `NuGet.Config`kullanılabilir kaynaklar listesine ekleyerek bunlara erişebilirsiniz. Bu, [paket kaynakları](../consume-packages/install-use-packages-visual-studio.md#package-sources)' nda veya kullanılarak [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)komut satırından açıklandığı şekilde Visual Studio 'da yapılabilir. Bir kaynağın yolu yerel bir klasör yol adı, ağ adı veya URL olabilir.
