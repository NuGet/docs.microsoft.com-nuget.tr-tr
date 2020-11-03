---
title: NuGet CLı doğrulama komutu
description: nuget.exe Verify komutu için başvuru
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238146"
---
# <a name="verify-command-nuget-cli"></a>Verify komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.6 +

Bir paketi doğrular.

İmzalanmış paketlerin doğrulanması, Mono altında henüz desteklenmiyor.

## <a name="usage"></a>Kullanım

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` Dosya bulunur.

## <a name="nuget-verify--all"></a>NuGet Verify-tümü

Tüm doğrulamaları, paketler üzerinde gerçekleştirilmesi gerektiğini belirtir.

## <a name="nuget-verify--signatures"></a>NuGet doğrulama-Imzalar

Paket imzası doğrulamasının gerçekleştirilmesi gerektiğini belirtir.

## <a name="options-for-verify--signatures"></a>"Verify-Imzalara" seçenekleri

- **`-CertificateFingerprint`**

  İmzalı paketlerin imzalı olması gereken sertifikaların bir veya daha fazla SHA-256 sertifikası parmak izlerini belirtir. Bir sertifika SHA-256 parmak izi, sertifikanın SHA-256 karmasıdır. Birden çok giriş noktalı virgülle ayrılmalıdır.

## <a name="options"></a>Seçenekler

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

## <a name="examples"></a>Örnekler

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```