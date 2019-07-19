---
title: NuGet CLı doğrulama komutu
description: NuGet. exe Verify komutu için başvuru
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328254"
---
# <a name="verify-command-nuget-cli"></a>Verify komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.6 +

Bir paketi doğrular.

İmzalanmış paketlerin doğrulanması henüz .NET Core 'da, mono kapsamında veya Windows dışı platformlarda desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosya bulunur.

## <a name="nuget-verify--all"></a>NuGet Verify-tümü

Tüm doğrulamaları, paketler üzerinde gerçekleştirilmesi gerektiğini belirtir.

## <a name="nuget-verify--signatures"></a>NuGet doğrulama-Imzalar

Paket imzası doğrulamasının gerçekleştirilmesi gerektiğini belirtir.

## <a name="options-for-verify--signatures"></a>"Verify-Imzalara" seçenekleri

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | İmzalı paketlerin imzalı olması gereken sertifikaların bir veya daha fazla SHA-256 sertifikası parmak izlerini belirtir. Bir sertifika SHA-256 parmak izi, sertifikanın SHA-256 karmasıdır. Birden çok giriş noktalı virgülle ayrılmalıdır. |

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```