---
title: Kendi NuGet akışlarınızı barındırılmasına genel bakış
description: Kendi NuGet paket akışlarınızı veya galerinizi yerel olarak veya uzaktan barındırmak için açılan bir genel bakış.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 737b13be70de9aaa7dec7904d4c2a4ec494ef7b3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317548"
---
# <a name="hosting-your-own-nuget-feeds"></a>Kendi NuGet akışlarınızı barındırma

Paketleri genel kullanıma hazır hale getirmek yerine, paketleri yalnızca kuruluşunuz veya çalışma grubunuz gibi sınırlı bir hedef kitleye serbest bırakmak isteyebilirsiniz. Ayrıca, bazı şirketler geliştiricilerin hangi üçüncü taraf kitaplıklarını kullandığını kısıtlamak ve böylece bu geliştiricilerin nuget.org yerine sınırlı bir paket kaynağından çizim yapmak isteyebilir.

NuGet, bu gibi tüm amaçlar için özel paket kaynaklarını aşağıdaki yollarla ayarlamayı destekler:

- Yerel akış: Paketler, bir hiyerarşik klasör yapısı (NuGet 3.3 +) oluşturmak için `nuget init` ve `nuget add` kullanarak ideal bir ağ dosya paylaşımında yer alır. Ayrıntılar için bkz. [Yerel akışlar](../hosting-packages/local-feeds.md).
- NuGet. Server: Paketler yerel bir HTTP sunucusu üzerinden kullanılabilir hale getirilir. Ayrıntılar için bkz. [NuGet. Server](../hosting-packages/nuget-server.md).
- NuGet Galerisi: Paketler, [NuGet Galeri projesi](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (GitHub.com) kullanılarak bir Internet sunucusunda barındırılır. NuGet Galerisi, nuget.org benzer şekilde, tarayıcı içinden paket aramaya ve keşfetmeye izin veren kapsamlı bir Web Kullanıcı arabirimi gibi Kullanıcı yönetimi ve özellikler sağlar.

Aşağıdakiler de dahil olmak üzere uzak özel akışları destekleyen diğer çeşitli NuGet barındırma ürünleri de mevcuttur:

- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), Team Foundation Server 2017 ve sonraki sürümlerde de kullanılabilir.
- [MyGet](http://myget.org)
- Inedo 'dan [temin edin](http://inedo.com/proget)
- [GitHub paket kayıt defteri](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- Inedo 'dan bir topluluk projesi olan [NuGet sunucusu](http://nugetserver.net/)
- Inedo 'ın NuGet sunucusuna benzer bir açık kaynaklı uygulama olan [NuGet sunucusu (açık kaynak)](http://nuget-server.net)
- Docker 'da Kestrel üzerinde çalışan NuGet v2 sunucusunun açık kaynaklı bir uygulama olan [Liget](https://github.com/ai-traders/liget)
- [Baget](https://github.com/loic-sharma/BaGet), NuGet v3 sunucusunun açık kaynaklı ASP.NET Core yerleşik bir uygulamasıdır
- [](https://github.com/emgarten/sleet)Açık kaynaklı bir NuGet v3 statik akış Oluşturucu olan uyma
- JFrog 'den [Artifactory](https://www.jfrog.com/artifactory/) .
- Sonatype 'dan [Nexus](http://www.sonatype.org/nexus/) .
- JetBrains 'den [TeamCity](https://www.jetbrains.com/teamcity/) .

Paketlerin nasıl barındırıldığından bağımsız olarak, ' deki `NuGet.Config`kullanılabilir kaynaklar listesine ekleyerek bunlara erişebilirsiniz. Bu, [paket kaynakları](../consume-packages/install-use-packages-visual-studio.md#package-sources)' nda veya kullanılarak [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)komut satırından açıklandığı şekilde Visual Studio 'da yapılabilir. Bir kaynağın yolu yerel bir klasör yol adı, ağ adı veya URL olabilir.
