---
title: NuGet CLI doğrulayın komutu | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe başvurusunu komutu doğrulayın
keywords: nuget başvuru doğrulamak için komut doğrulayın
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4423e491e0ab5dc1e13982440db42bc9b0e85c38
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="verify-command-nuget-cli"></a>verify komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 4.6 +

Bir paket doğrular.

## <a name="usage"></a>Kullanım

```cli
nuget verify <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| Tümü | Tüm Doğrulamalar olası paketler üzerinde gerçekleştirilmelidir belirtir. |
| CertificateFingerprint | Bir veya daha fazla SHA-256 sertifika parmak izi imzalı hangi paketlerin imzalanmalıdır sertifikaların (s) belirtir. SHA-256 sertifika parmak izi sertifika SHA-256 karmasıdır. Birden çok girişi noktalı virgülle ayrılmış olması gerekir. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | Bir sabit, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| İmzalar | Paket imza doğrulaması gerçekleştirilmesi gerektiğini belirtir. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```