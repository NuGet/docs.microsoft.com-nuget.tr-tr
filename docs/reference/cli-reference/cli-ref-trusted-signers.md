---
title: NuGet CLı güvenilir-imzalayanlar komutu
description: NuGet. exe güvenilir-signers komutuna yönelik başvuru
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610341"
---
# <a name="trusted-signers-command-nuget-cli"></a>Güvenilen imzalayanlar komutu (NuGet CLı)

**Uygulama hedefi:** paket tüketimi **Desteklenen sürümler &bullet;:** 4.9.1 +

Güvenilen İmzalayanları NuGet yapılandırmasına alır veya ayarlar. Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md). NuGet. config şemasının nasıl görüneceğine ilişkin ayrıntılar için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.

## <a name="usage"></a>Kullanım

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

`list|add|remove|sync` Hiçbiri belirtilmediyse, komut varsayılan olarak `list`olur.

## <a name="nuget-trusted-signers-list"></a>NuGet güvenilir-imzalayanlar listesi

Yapılandırmadaki tüm güvenilen İmzalayanları listeler. Bu seçenek, her İmzalayanın sahip olduğu tüm sertifikaları (parmak izi ve parmak izi algoritması) içerir. Bir sertifikanın önceki bir `[U]`varsa, bu sertifika girişinin `true`olarak `allowUntrustedRoot` ayarlandığı anlamına gelir.

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

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosya olur.

| Seçenek | Açıklama |
| --- | --- |
| Yazar | Paket (ler) in yazar imzasında güvenilir olması gerektiğini belirtir. |
| Depo | Paket (lar) için depo imzasının veya onay imzasının güvenilir olması gerektiğini belirtir. |
| AllowUntrustedRoot | Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir. |
| lere | Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste. Yalnızca `-Repository` seçeneği kullanılırken geçerlidir. |

Hem `-Author` hem de `-Repository` aynı anda sağlanması desteklenmez.

## <a name="options-for-add-based-on-a-service-index"></a>Hizmet dizinine dayalı ekleme seçenekleri

```cli
nuget trusted-signers add -Name <name> [options]
```

_Note_: Bu seçenek yalnızca güvenilen depolar ekler. 

| Seçenek | Açıklama |
| --- | --- |
| Serviceındex | Güvenilecek deponun v3 hizmeti dizinini belirtir. Bu depo, depo imzaları kaynağını desteklemelidir. Sağlanmazsa, komut aynı `-Name` bir paket kaynağına bakar ve hizmet dizinini buradan alırlar. |
| AllowUntrustedRoot | Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir. |
| lere | Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Sertifika bilgilerine göre ekleme seçenekleri

```cli
nuget trusted-signers add -Name <name> [options]
```

_Note_: verilen ada sahip bir güvenilir imzalayan zaten varsa, sertifika öğesi bu İmzalayanın birlikte eklenir. Aksi halde, belirtilen sertifika bilgileri 'nden bir sertifika öğesiyle güvenilir bir yazar oluşturulacaktır.

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | İmzalı paketlerin imzalı olması gereken bir sertifikanın sertifika parmak izlerini belirtir. Sertifika parmak izi, sertifikanın bir karmasıdır. Bu karmayı hesaplamak için kullanılan karma algoritma `FingerprintAlgorithm` seçeneğinde belirtilmelidir. |
| Parmak izi Talgorithd | Sertifika parmak izini hesaplamak için kullanılan karma algoritmasını belirtir. Varsayılan olarak `SHA256`olur. Desteklenen değerler `SHA256`, `SHA384` ve `SHA512` |
| AllowUntrustedRoot | Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir. |

## <a name="nuget-trusted-signers-remove--name-name"></a>NuGet güvenilir-imzalayanlar Remove-Name \<Name\>

Verilen adla eşleşen tüm güvenilen İmzalayanları kaldırır.

## <a name="nuget-trusted-signers-sync--name-name"></a>NuGet güvenilir-sonuçcılar eşitleme-adı \<adı\>

Güvenilen İmzalayanın mevcut sertifika listesini güncelleştirmek için şu anda güvenilir bir depoda kullanılan sertifikaların en son listesini ister.

_Note_: Bu hareket, geçerli sertifika listesini silecek ve bunları depodan güncel bir listeyle değiştirecek.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| Yardım | Komut için yardım bilgilerini görüntüler. |
| Ayrıntı Düzeyi | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

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
