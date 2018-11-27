---
title: NuGet CLI güvenilen İmzalayanları komutu
description: Nuget.exe güvenilen İmzalayanları komut başvurusu
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ffd0cf5d50a2deed16e1722b32e43047bc81df2f
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303730"
---
# <a name="trusted-signers-command-nuget-cli"></a>Güvenilen İmzalayanları komut (NuGet CLI)

**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** 4.9 +

Alır veya güvenilen İmzalayanları için NuGet yapılandırmayı ayarlar. Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md). Nuget.config şema bakın gibi nasıl göründüğüne ilişkin ayrıntılar için [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).

## <a name="usage"></a>Kullanım

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Hiçbiri `list|add|remove|sync` belirtilirse, komut için varsayılan `list`.

## <a name="nuget-trusted-signers-list"></a>nuget güvenilen İmzalayanları listesi

Tüm güvenilen imzalayanlardan yapılandırmasında listeler. Bu seçenek, tüm sertifikaları dahil edilir (parmak izi ve parmak izi algoritması ile) her imzalayan sahiptir. Bir önceki bir sertifika varsa `[U]`, sertifika girdisi olduğu anlamına gelir `allowUntrustedRoot` yap `true`.

Bu komut bir örnek çıktısı aşağıdadır:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget güvenilen İmzalayanları [Seçenekler] ekleyin

Belirtilen ada sahip bir güvenilen imzalayan yapılandırmaya ekler. Bu seçenek bir güvenilen yazar veya depo eklemek için farklı hareketlerini sahiptir.

## <a name="options-for-add-based-on-a-package"></a>Bir paketine dayalı ekleme seçenekleri

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.

| Seçenek | Açıklama |
| --- | --- |
| Yazar | Paket yazarı imzası güvenilir olması gerektiğini belirtir. |
| Depo | Depo imza veya onay imzası paketleri, güvenilir olması gerektiğini belirtir. |
| AllowUntrustedRoot | İçin güvenilen imzalayan sertifika zinciri güvenilmeyen bir kökü için izin verilmediğini belirtir. |
| Sahipleri | Bir havuzun güven kısıtlamanız güvenilen sahiplerinin noktalı virgülle ayrılmış listesi. Kullanırken yalnızca geçerli `-Repository` seçeneği. |

Hem `-Author` ve `-Repository` aynı anda desteklenmiyor.

## <a name="options-for-add-based-on-a-service-index"></a>Bir hizmet dizinini temel alarak ekleme seçenekleri

```cli
nuget trusted-signers add -Name <name> [options]
```

_Not_: Bu seçenek yalnızca güvenilen depoları ekleyeceksiniz. 

| Seçenek | Açıklama |
| --- | --- |
| ServiceIndex | Güvenilir olmasını deponun V3 hizmet dizini belirtir. Depo imzaları kaynağını desteklemek bu depoyu sahiptir. Sağlanmazsa, komutu bir paket kaynağıyla aynı arar `-Name` ve buradan hizmet dizini alın. |
| AllowUntrustedRoot | İçin güvenilen imzalayan sertifika zinciri güvenilmeyen bir kökü için izin verilmediğini belirtir. |
| Sahipleri | Bir havuzun güven kısıtlamanız güvenilen sahiplerinin noktalı virgülle ayrılmış listesi. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Seçenekler için sertifika bilgilere göre Ekle

```cli
nuget trusted-signers add -Name <name> [options]
```

_Not_: verilen ada sahip bir güvenilen imzalayan zaten varsa, sertifika öğesi için imzalayan eklenir. Aksi takdirde bir sertifika öğesi ile güvenilir Yazar oluşturulacak alanından sertifika bilgileri verilir.

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | İmzalanmış bir sertifikanın parmak izi ile imzalanmalıdır sertifikayı belirtir. Sertifika parmak izi sertifika karmasıdır. Bu karma olmalıdır hesaplamak için kullanılan karma algoritmasını belirtir `FingerprintAlgorithm` seçeneği. |
| FingerprintAlgorithm | Sertifika parmak izi hesaplamak için kullanılan karma algoritmasını belirtir. Varsayılan olarak `SHA256`. Desteklenen değerler: `SHA256`, `SHA384` ve `SHA512` |
| AllowUntrustedRoot | İçin güvenilen imzalayan sertifika zinciri güvenilmeyen bir kökü için izin verilmediğini belirtir. |

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget güvenilen İmzalayanları Kaldır - ad <name>

Verilen ada uyan herhangi bir güvenilir İmzalayanları kaldırır.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget güvenilen İmzalayanları eşitleme - ad <name>

Şu anda güvenilir bir depoda güncelleştirmek için kullanılan sertifikaları en son listesi ister mevcut sertifika listesine güvenilir imzalayan.

_Not_: Bu hareket geçerli sertifikaların listesini silmek ve bunları depodan güncel bir listesi ile değiştirin.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```