---
title: NuGet Istemci SDK 'Sı
description: API gelişiyor ve henüz belgelenmemiştir, ancak örnek, bave Glick 'in blogundan bulunabilir.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231246"
---
# <a name="nuget-client-sdk"></a>NuGet Istemci SDK 'Sı

*NuGet istemci SDK 'sı* bir NuGet paketleri grubunu ifade eder:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -http ve dosya tabanlı NuGet akışlarıyla etkileşim kurmak için kullanılır
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet paketleriyle etkileşim kurmak için kullanılır. `NuGet.Protocol` bu pakete bağlıdır

Bu paketlerin kaynak kodunu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub deposunda bulabilirsiniz.

> [!Note]
> NuGet sunucu protokolü hakkındaki belgeler için lütfen [NuGet sunucu API](~/api/overview.md)'sine bakın.

## <a name="getting-started"></a>Başlarken

### <a name="install-the-package"></a>Paketi yükler

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Örnekler

Bu örnekleri GitHub 'da [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) projesinde bulabilirsiniz.

### <a name="list-package-versions"></a>Paket sürümlerini Listele

[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md#enumerate-package-versions)'Sini kullanarak Newtonsoft. json ' nin tüm sürümlerini bulun:

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Paket indir

[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md)'Sini kullanarak Newtonsoft. JSON v 12.0.1 ' ni indirin:

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Paket meta verilerini al

[NuGet V3 paketi meta veri API 'sini](../api/registration-base-url-resource.md)kullanarak "Newtonsoft. JSON" paketine ait meta verileri alın:

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Paketleri ara

[NuGet v3 arama API](../api/search-query-service-resource.md)'sini kullanarak "JSON" paketleri arayın:

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>Üçüncü taraf belgeleri

Aşağıdaki blog serisindeki bazı API 'ler için örnekler ve belgeler için Glick, yayımlanan 2016:

- [NuGet v3 kitaplıklarını keşfetme, 1. Bölüm: giriş ve kavramlar](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [NuGet v3 kitaplıklarını keşfetme, Bölüm 2: paketleri arama](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [NuGet v3 kitaplıklarını keşfetme, 3. Bölüm: paketleri yükleme](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Bu blog gönderileri, NuGet istemci SDK paketlerinin **3.4.3** sürümü yayımlandıktan kısa bir süre sonra yazıldı.
> Paketlerin daha yeni sürümleri, blog gönderilerinin bilgileriyle uyumsuz olabilir.

Marve Glick 'in blog serisine, NuGet paketlerini yüklemek için NuGet Istemci SDK 'sını kullanma konusunda farklı bir yaklaşım tanıtan bir izleme blog gönderisi Björkström.

- [NuGet v3 kitaplıklarını yeniden ziyaret etme](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
