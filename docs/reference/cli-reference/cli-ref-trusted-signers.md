---
title: NuGet CLı güvenilir-imzalayanlar komutu
description: NuGet. exe güvenilir-signers komutuna yönelik başvuru
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328266"
---
# <a name="trusted-signers-command-nuget-cli"></a>Güvenilen imzalayanlar komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.9.1 +

Güvenilen İmzalayanları NuGet yapılandırmasına alır veya ayarlar. Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md). NuGet. config şemasının nasıl görüneceğine ilişkin ayrıntılar için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.

## <a name="usage"></a>Kullanım

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

hiçbiri `list|add|remove|sync` belirtilmemişse, komut varsayılan olarak `list`olur.

## <a name="nuget-trusted-signers-list"></a>NuGet güvenilir-imzalayanlar listesi

Yapılandırmadaki tüm güvenilen İmzalayanları listeler. Bu seçenek, her İmzalayanın sahip olduğu tüm sertifikaları (parmak izi ve parmak izi algoritması) içerir. Bir sertifika öncesinde `[U]`varsa, sertifika `allowUntrustedRoot` girişinin olarak `true`ayarlandığı anlamına gelir.

Bu komuttan bir örnek çıktı aşağıda verilmiştir:

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

## <a name="nuget-trusted-signers-add-options"></a>NuGet güvenilir-imzalayanlar Add [seçenekler]

Yapılandırmaya verilen adı taşıyan güvenilen bir imzalayan ekler. Bu seçeneğin, güvenilen bir yazar veya depo eklemek için farklı hareketleri vardır.

## <a name="options-for-add-based-on-a-package"></a>Pakete dayalı ekleme seçenekleri

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosya bulunur.

| Seçenek | Açıklama |
| --- | --- |
| Yazar | Paket (ler) in yazar imzasında güvenilir olması gerektiğini belirtir. |
| Havuz | Paket (lar) için depo imzasının veya onay imzasının güvenilir olması gerektiğini belirtir. |
| AllowUntrustedRoot | Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir. |
| lere | Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste. Yalnızca `-Repository` seçeneği kullanılırken geçerlidir. |

Aynı anda `-Repository` ve aynı zamanda sağlama desteklenmez. `-Author`

## <a name="options-for-add-based-on-a-service-index"></a>Hizmet dizinine dayalı ekleme seçenekleri

```cli
nuget trusted-signers add -Name <name> [options]
```

_Not_: Bu seçenek yalnızca güvenilen depolar ekler. 

| Seçenek | Açıklama |
| --- | --- |
| Serviceındex | Güvenilecek deponun v3 hizmeti dizinini belirtir. Bu depo, depo imzaları kaynağını desteklemelidir. Sağlanmazsa, komut aynı `-Name` olan bir paket kaynağını arar ve hizmet dizinini buradan alır. |
| AllowUntrustedRoot | Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir. |
| lere | Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Sertifika bilgilerine göre ekleme seçenekleri

```cli
nuget trusted-signers add -Name <name> [options]
```

_Not_: Verilen ada sahip bir güvenilir imzalayan zaten varsa, sertifika öğesi bu İmzalayanın birlikte eklenir. Aksi halde, belirtilen sertifika bilgileri 'nden bir sertifika öğesiyle güvenilir bir yazar oluşturulacaktır.

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | İmzalı paketlerin imzalı olması gereken bir sertifikanın sertifika parmak izlerini belirtir. Sertifika parmak izi, sertifikanın bir karmasıdır. Bu karmayı hesaplamak için kullanılan karma algoritma, `FingerprintAlgorithm` seçeneğinde belirtilmelidir. |
| Parmak izi Talgorithd | Sertifika parmak izini hesaplamak için kullanılan karma algoritmasını belirtir. Varsayılan olarak `SHA256`. Desteklenen değerler şunlardır `SHA256`ve `SHA384``SHA512` |
| AllowUntrustedRoot | Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir. |

## <a name="nuget-trusted-signers-remove--name-name"></a>NuGet güvenilir-imzalayanlar Remove-Name<name>

Verilen adla eşleşen tüm güvenilen İmzalayanları kaldırır.

## <a name="nuget-trusted-signers-sync--name-name"></a>NuGet güvenilir-imzalayanlar eşitleme-adı<name>

Güvenilen İmzalayanın mevcut sertifika listesini güncelleştirmek için şu anda güvenilir bir depoda kullanılan sertifikaların en son listesini ister.

_Not_: Bu hareket, geçerli sertifika listesini silecek ve bunları depodan güncel bir listeyle değiştirecek.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Help | Komut için yardım bilgilerini görüntüler. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

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
