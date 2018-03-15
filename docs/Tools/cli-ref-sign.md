---
title: NuGet CLI oturum komutu | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe oturum komut başvurusu"
keywords: "nuget oturum başvuru, oturum komutu"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: f600a0830472703f40ef62f1b1538c53671703a9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="sign-command-nuget-cli"></a>oturum komutu (NuGet CLI)

**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 4.6 +

İlk bağımsız değişkeni bir sertifika ile eşleşen tüm paketler imzalar. Sertifikanın özel anahtarı olan bir dosya ya da bir konu adı veya bir parmak izi sağlayarak bir sertifika deposunda yüklü bir sertifika elde edilebilir.

Paket imzalama, Mono altında veya Windows olmayan platformlarında henüz desteklenmiyor.

## <a name="usage"></a>Kullanım

```cli
nuget sign <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | SHA-1 parmak izi sertifika için bir yerel sertifika deposu aramak için kullanılan sertifikanın belirtir. |
| CertificatePassword | Sertifika parolası gerekirse belirtir. Parola korumalı bir sertifikadır, ancak hiçbir parola sağlanan komutu için bir parola çalışma zamanında sürece ister etkileşimli olmayan seçeneği geçirilir. |
| CertificatePath | Paketin imzalanması kullanılmak üzere sertifika dosya yolunu belirtir. |
| CertificateStoreLocation | Sertifikayı aramak için X.509 Sertifika deposu kullanımı adını belirtir. Varsayılan olarak "Currentuser'a", geçerli bir kullanıcı tarafından kullanılan X.509 Sertifika deposu. Bu seçenek, sertifikayı CertificateSubjectName - veya - CertificateFingerprint seçenekleri aracılığıyla belirtirken kullanılmalıdır. |
| CertificateStoreName | Sertifika bulmak için kullanılacak X.509 Sertifika deposu adını belirtir. Varsayılan olarak "Benim", kişisel sertifikalar için X.509 Sertifika deposu. Bu seçenek, sertifikayı CertificateSubjectName - veya - CertificateFingerprint seçenekleri aracılığıyla belirtirken kullanılmalıdır. |
| CertificateSubjectName | Sertifika için bir yerel sertifika deposu aramak için kullanılan sertifikanın konu adını belirtir.  Arama diğer konu değerlerinden bağımsız olarak o dizeyi içeren konu adına sahip tüm sertifikaların bulur sağlanan değer kullanarak büyük küçük harf duyarlı dize karşılaştırmasının olur.  Sertifika deposu - SertifikaDeposuAdı ve - CertificateStoreLocation seçenekleri ile belirtilebilir. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | Bir sabit, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| HashAlgorithm | Paketi imzalamak için kullanılan karma algoritması. Varsayılan olarak SHA256. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Çıktıdizini | İmzalı paketinin kaydedileceği dizini belirtir. Varsayılan olarak özgün paket imzalı paketi tarafından üzerine yazılır. |
| Üzerine yaz | Geçerli imza üzerine göstermek için anahtar. Paket imza zaten varsa, varsayılan olarak komut başarısız olur. |
| Timestamper | RFC 3161 zaman damgası sunucu URL'si. |
| TimestampHashAlgorithm | RFC 3161 zaman damgası sunucusu tarafından kullanılan karma algoritması. Varsayılan olarak SHA256. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```