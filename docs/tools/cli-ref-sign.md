---
title: NuGet CLI oturum komutu
description: Nuget.exe oturum komutu için başvuru
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546369"
---
# <a name="sign-command-nuget-cli"></a>oturum komutu (NuGet CLI)

**İçin geçerlidir:** paket oluşturma &bullet; **desteklenen sürümler:** 4.6 +

İlk bağımsız değişken bir sertifika ile eşleşen tüm paketleri imzalar. Sertifikanın özel anahtarı içeren bir dosyadaki veya bir konu adı veya parmak izi sağlayarak bir sertifika deposunda yüklü sertifika elde edilebilir.

Paket imzalama henüz .NET Core, Mono altında ya da Windows olmayan platformlarda desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget sign <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | SHA-1 parmak izi için sertifika yerel sertifika deposu aramak için kullanılan sertifikanın belirtir. |
| CertificatePassword | Gerekirse, sertifika parolasını belirtir. Parola korumalı bir sertifikası olan ancak hiçbir parola sağlandı, komutu bir çalışma zamanında sürece isteyecek etkileşimli olmayan seçeneği geçirilir. |
| CertificatePath | Paket oturum açarken kullanılacak sertifika dosyası yolunu belirtir. |
| CertificateStoreLocation | Sertifikayı aramak için X.509 Sertifika deposu kullan adını belirtir. Varsayılan olarak "CurrentUser", geçerli kullanıcı tarafından kullanılan X.509 Sertifika deposunun. Bu seçenek, CertificateSubjectName - veya - CertificateFingerprint seçeneği aracılığıyla sertifikası belirtilirken kullanılmalıdır. |
| SertifikaDeposuAdı | Sertifikayı aramak için kullanılacak olan X.509 Sertifika deposunun adını belirtir. Varsayılan olarak "My", X.509 Sertifika deposunun kişisel sertifikalar için. Bu seçenek, CertificateSubjectName - veya - CertificateFingerprint seçeneği aracılığıyla sertifikası belirtilirken kullanılmalıdır. |
| CertificateSubjectName | Sertifika için bir yerel sertifika deposu aramak için kullanılan sertifikanın konu adını belirtir.  Diğer konu değerlerinden bağımsız olarak o dizeyi içeren konu adına sahip tüm sertifikaların bulabilirsiniz sağlanan değerini kullanarak bir büyük küçük harf duyarlı dize karşılaştırması aramadır.  Sertifika deposu - SertifikaDeposuAdı ve - CertificateStoreLocation seçenekleri ile belirtilebilir. |
| ConfigFile | Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| HashAlgorithm | Paketi imzalamak için kullanılan karma algoritması. Varsayılan değer SHA256. |
| Yardım | Bilgi komut için yardımı görüntüler. |
| NonInteractive | Kullanıcı girişini veya onaylar ister bastırır. |
| OutputDirectory | İmzalı paketinin kaydedileceği dizini belirtir. Varsayılan olarak, özgün paket imzalı paket tarafından üzerine yazılır. |
| Üzerine yaz | Geçerli imza üzerine göstermek için anahtar. Paket bir imza zaten varsa, varsayılan olarak komut başarısız olur. |
| Timestamper | Bir RFC 3161 zaman damgası sunucu URL'si. |
| TimestampHashAlgorithm | RFC 3161 zaman damgası sunucusu tarafından kullanılan karma algoritması. Varsayılan değer SHA256. |
| Ayrıntı Düzeyi | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```