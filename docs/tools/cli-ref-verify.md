---
title: NuGet CLI komutu doğrulayın
description: Nuget.exe başvurusunu komutu doğrulayın
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a>verify komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 4.6 +

Bir paket doğrular.

İmzalı paketlerin doğrulama, .NET Core, Mono altında ya da Windows olmayan platformlarında içinde henüz desteklenmiyor.

## <a name="usage"></a>Kullanım

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.

## <a name="nuget-verify--all"></a>nuget doğrulama - tüm

Tüm Doğrulamalar olası paketler üzerinde gerçekleştirilmelidir belirtir.

## <a name="nuget-verify--signatures"></a>nuget doğrulama - imzaları

Paket imza doğrulaması gerçekleştirilmesi gerektiğini belirtir.

## <a name="options-for-verify--signatures"></a>"Doğrulama - imzaları" seçenekleri

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | Bir veya daha fazla SHA-256 sertifika parmak izi imzalı hangi paketlerin imzalanmalıdır sertifikaların (s) belirtir. SHA-256 sertifika parmak izi sertifika SHA-256 karmasıdır. Birden çok girişi noktalı virgülle ayrılmış olması gerekir. |

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | Bir sabit, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```