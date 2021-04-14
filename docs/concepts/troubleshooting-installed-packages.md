---
title: Yüklü paketlerin sorunlarını giderme
description: Ayrı paketler için kullanılan paket kaynağını bulma
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387573"
---
# <a name="troubleshooting-installed-packages"></a>Yüklü paketlerin sorunlarını giderme

Bazen belirli bir paketin hangi kaynağa yüklendiğini doğrulamak isteyebilirsiniz. Burada, bazı şekillerde denetim yapabilirsiniz.

> [!Note]
> Bazı paket kaynakları, yukarı akış kaynakları olarak bilinen bir kavramı destekler. Örneğin, [yukarı akış kaynakları Azure Artifacts](/azure/devops/artifacts/concepts/upstream-sources). NuGet istemcileri bir paketin yukarı akış kaynağından geldiğini bilmez. Bu nedenle, paket kaynağının herhangi bir günlüğü, yukarı akış kaynağını değil, yapılandırılmış kaynağı listeler.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>`.nupkg.metadata` Genel paketler klasöründeki dosya

Bir paket *genel paketler* klasörüne ayıklandığında bir dosya `.nupkg.metadata` yazılır. NuGet 5.9.0 'den başlayarak, NuGet paket kaynağını ekler. NuGet sürümlerini Visual Studio veya .NET SDK sürümleriyle eşlemek için aşağıya bakın. Örnek:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> *Genel paketler* klasörünüzün, NuGet 5.9.0 içeren araçların daha yeni bir sürümüne yükseltmeden önce ayıklandığı paketler varsa, `.nupkg.metadata` Dosya sürüm 1 olur ve paket kaynağını içermez. Tüm paketlerin paket kaynağını içermesini sağlamak için [ *genel paketler* klasörünüzü temizleyebilirsiniz](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) .

> [!Tip]
> NuGet `.nupkg.metadata` dosyayı yalnızca *genel paketler* klasörüne yazar. Kullanan projeler bir `packages.config` dosya oluşturmayan çözüm paketleri klasörünü kullanır `.nupkg.metadata` .

## <a name="installed-package-log-message"></a>Paket günlük iletisi yüklendi

NuGet 5.9.0 'den başlayarak NuGet, geri yükleme iletisindeki paket kaynağını bir paketin yüklendiğini bildiren çıkış olarak verir. Örnek:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Bu ileti, normal/bilgilendirici Ayrıntı ayrıntısı sırasında çıktıdır. Visual Studio ve `dotnet` CLI varsayılan olarak en az ayrıntı düzeyi, bu nedenle bu ileti varsayılan olarak görünür olmayacaktır. `msbuild`Ve `nuget` CLI araçları varsayılan olarak normal ayrıntı düzeyi olarak görünür, bu nedenle bu ileti varsayılan olarak görünür olur.

## <a name="http-log-message"></a>HTTP günlüğü iletisi

Bir paket yerel olarak mevcut olmadığında, *genel paketler* klasöründe, bir geri dönüş klasöründe veya yerel bir dosya kaynağında, NUGET bunu http üzerinden yapılandırılmış herhangi bir paket kaynağından indirir. HTTP istekleri ve yanıtları normal ayrıntı düzeyinde günlüğe kaydedilir ve paket sürümüne göre yalnızca tek bir istek ve yanıt görmeniz gerekir. Örnek:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Dosyalar yakın zamanda indirildiyse NuGet 'in *http önbelleğinden* alınmış olabilir

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

URL biçimi farklı NuGet HTTP sunucu uygulamaları için farklı olabilir ve NuGet v2 ya da v3 HTTP protokolünü mi uygulamadığını belirtir.

`nuget.config`Tanımlanmış birden çok http kaynağı varsa her `index.json` bir paket dosyası için her bir kaynak için birden çok istek görürsünüz. Ancak `nupkg` paketin her sürümü için yalnızca tek bir indirme olacaktır.

## <a name="package-signature-log-message"></a>Paket imza günlüğü iletisi

İndirilen paket imzalanmışsa, NuGet imzayı doğrular ve ayrıntılı ayrıntı olarak şu iletiyi günlüğe kaydeder:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Bu ileti, paketin bir HTTP paket kaynağından indirilip indirilmediğini veya yerel bir paket kaynağından kopyalanıp kopyalanmadığını rapor eder. Paket, *genel paketler* klasöründe veya bir geri dönüş klasöründe zaten kullanılabiliyorsa çıkış olmaz.

> [!Important]
> [VERISIGN CA 'nın güveninin kaldırılması](https://github.com/dotnet/announcements/issues/180) nedeniyle belirli platformlarda, belirli bir NuGet ve .NET SDK sürümünde imzalı paket doğrulaması devre dışı bırakıldı. Bu nedenle, `PackageSignatureVerificationLog` geri yükleme çalıştırdığınız platforma ve hangi .NET veya NuGet sürümüne bağlı olarak, aynı paketlerde Günlükler olabilir veya bu Günlükler eksik olabilir.

## <a name="nuget-version-map"></a>NuGet sürüm Haritası

Aşağıdaki NuGet sürümlerinde, paket kaynağı günlük kaydıyla ilgili önemli değişiklikler vardır:

|NuGet sürümü|Visual Studio sürümü|.NET SDK sürümü|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|.NET 5 SDK 5.0.200|
