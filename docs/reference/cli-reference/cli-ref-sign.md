---
title: NuGet CLı imza komutu
description: NuGet. exe Sign komutu için başvuru
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328281"
---
# <a name="sign-command-nuget-cli"></a>Sign komutu (NuGet CLı)

**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 4.6 +

İlk bağımsız değişkenle eşleşen tüm paketleri bir sertifikayla imzalar. Özel anahtara sahip sertifika, bir dosya veya bir parmak izi sağlayarak bir sertifika deposunda yüklü olan bir sertifikadan elde edilebilir.

Paket imzalama henüz .NET Core 'da, mono veya Windows dışı platformlarda desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget sign <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` dosya bulunur.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| CertificateFingerprint | Sertifika için bir yerel sertifika deposunda arama yapmak üzere kullanılan sertifikanın SHA-1 parmak izini belirtir. |
| certificatePassword | Gerekirse sertifika parolasını belirtir. Bir sertifika parola korumalıysa ancak parola sağlanmazsa,-etkileşimsiz seçenek geçirilmediği takdirde komut çalışma zamanında parola ister. |
| CertificatePath | Paketi imzalarken kullanılacak sertifikanın dosya yolunu belirtir. |
| CertificateStoreLocation | Sertifikayı aramak için kullanılan X. 509.440 sertifika deposunun adını belirtir. Geçerli Kullanıcı tarafından kullanılan X. 509.440 sertifika deposu varsayılan olarak "CurrentUser" olarak belirlenmiştir. Bu seçenek, sertifika-CertificateSubjectName veya-Certificateparmak izi seçenekleri kullanılarak belirtildiğinde kullanılmalıdır. |
| CertificateStoreName | Sertifikayı aramak için kullanılacak X. 509.440 sertifika deposunun adını belirtir. Kişisel sertifikalara ait X. 509.440 sertifika depolama alanı varsayılan olarak "My" olarak belirlenmiştir. Bu seçenek, sertifika-CertificateSubjectName veya-Certificateparmak izi seçenekleri kullanılarak belirtildiğinde kullanılmalıdır. |
| CertificateSubjectName | Sertifika için bir yerel sertifika deposunda arama yapmak üzere kullanılan sertifikanın konu adını belirtir.  Arama, diğer konu değerlerinden bağımsız olarak bu dizeyi içeren konu adına sahip tüm sertifikaları bulacak, sağlanan değeri kullanarak büyük/küçük harfe duyarsız bir dize karşılaştırmasından oluşur.  Sertifika deposu-CertificateStoreName ve-CertificateStoreLocation seçenekleri ile belirtilebilir. |
| ConfigFile | Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.|
| ForceEnglishOutput | NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar. |
| HashAlgorithm | Paketi imzalamak için kullanılacak karma algoritması. Varsayılan olarak SHA256. |
| Help | Komut için yardım bilgilerini görüntüler. |
| NonInteractive | Kullanıcı girişi veya onayları için istemleri bastırır. |
| OutputDirectory | İmzalanan paketin kaydedileceği dizini belirtir. Varsayılan olarak, özgün paketin imzalanmış paket tarafından üzerine yazılır. |
| Üzerine yaz | Geçerli imzanın üzerine yazılıp yazılmayacağını belirten geçiş yapın. Varsayılan olarak, pakette zaten imza varsa komut başarısız olur. |
| Timestamper | RFC 3161 zaman damgası sunucusunun URL 'SI. |
| TimestampHashAlgorithm | RFC 3161 zaman damgası sunucusu tarafından kullanılacak karma algoritması. Varsayılan olarak SHA256. |
| Verbosity | Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |

## <a name="examples"></a>Örnekler

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```