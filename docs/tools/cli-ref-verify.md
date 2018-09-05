---
title: NuGet CLI komutu doğrulayın
description: Nuget.exe başvurusunu doğrulama komutu
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545219"
---
# <a name="verify-command-nuget-cli"></a>verify komutu (NuGet CLI)

**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** 4.6 +

Bir paket doğrular.

İmzalı paketlerin doğrulama, .NET Core, Mono altında veya Windows dışı platformlarda, henüz desteklenmiyor.

## <a name="usage"></a>Kullanım

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.

## <a name="nuget-verify--all"></a>nuget doğrulama - tümü

Olası tüm doğrulamaları üzerinde paket gerçekleştirilmesi gerektiğini belirtir.

## <a name="nuget-verify--signatures"></a>nuget doğrulama - imzaları

Paket imzası doğrulaması gerçekleştirilmesi gerektiğini belirtir.

## <a name="options-for-verify--signatures"></a>"Doğrula - imzaları" seçenekleri

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | Bir veya daha fazla SHA-256'yı sertifika parmak izleri imzalı paketler imzalanmalıdır sertifikaların (s) belirtir. SHA-256'yı sertifika parmak izi sertifika SHA-256'yı karmasıdır. Birden çok girişler noktalı virgülle ayrılmış olması gerekir. |

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```