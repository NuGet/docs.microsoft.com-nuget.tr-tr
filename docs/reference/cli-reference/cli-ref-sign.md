---
title: NuGet CLı imza komutu
description: nuget.exe Sign komutu başvurusu
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622778"
---
# <a name="sign-command-nuget-cli"></a>Sign komutu (NuGet CLı)

**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 4.6 +

İlk bağımsız değişkenle eşleşen tüm paketleri bir sertifikayla imzalar. Özel anahtara sahip sertifika, bir dosya veya bir parmak izi sağlayarak bir sertifika deposunda yüklü olan bir sertifikadan elde edilebilir.

> [!Note]
> Paket imzalama henüz .NET Core 'da, mono veya Windows dışı platformlarda desteklenmez.

## <a name="usage"></a>Kullanım

```cli
nuget sign <package(s)> [options]
```

Burada `<package(s)>` bir veya daha fazla `.nupkg` Dosya bulunur.

## <a name="options"></a>Seçenekler

- **`-CertificateFingerprint`**

  Sertifika için bir yerel sertifika deposunda arama yapmak üzere kullanılan sertifikanın SHA-1 parmak izini belirtir.

- **`-CertificatePassword`**

  Gerekirse sertifika parolasını belirtir. Bir sertifika parola korumalıysa ancak parola sağlanmazsa, seçenek geçirilmediği takdirde komut çalışma zamanında bir parola ister `-NonInteractive` .

- **`-CertificatePath`**

  Paketi imzalarken kullanılacak sertifikanın dosya yolunu belirtir.

- **`-CertificateStoreLocation`**

  Sertifikayı aramak için kullanılan X. 509.440 sertifika deposunun adını belirtir. Geçerli Kullanıcı tarafından kullanılan X. 509.440 sertifika deposu varsayılan olarak "CurrentUser" olarak belirlenmiştir. Bu seçenek, sertifika veya seçenekler aracılığıyla belirtildiğinde kullanılmalıdır `-CertificateSubjectName` `-CertificateFingerprint` .

- **`-CertificateStoreName`**

  Sertifikayı aramak için kullanılacak X. 509.440 sertifika deposunun adını belirtir. Kişisel sertifikalara ait X. 509.440 sertifika depolama alanı varsayılan olarak "My" olarak belirlenmiştir. Bu seçenek, sertifika veya seçenekler aracılığıyla belirtildiğinde kullanılmalıdır `-CertificateSubjectName` `-CertificateFingerprint` .

- **`-CertificateSubjectName`**

  Sertifika için bir yerel sertifika deposunda arama yapmak üzere kullanılan sertifikanın konu adını belirtir.  Arama, diğer konu değerlerinden bağımsız olarak bu dizeyi içeren konu adına sahip tüm sertifikaları bulacak, sağlanan değeri kullanarak büyük/küçük harfe duyarsız bir dize karşılaştırmasından oluşur.  Sertifika deposu `-CertificateStoreName` ve seçenekleri ile belirtilebilir `-CertificateStoreLocation` .

- **`-ConfigFile`**

  Uygulanacak NuGet yapılandırma dosyası. Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.

- **`-ForceEnglishOutput`**

  nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.

- **`-HashAlgorithm`**

  Paketi imzalamak için kullanılacak karma algoritması. Varsayılan olarak SHA256. Olası değerler şunlardır SHA256, SHA384 ve SHA512 olur.

- **`-?|-help`**

  Komut için yardım bilgilerini görüntüler.

- **`-NonInteractive`**

  Kullanıcı girişi veya onayları için istemleri bastırır.

- **`-OutputDirectory`**

  İmzalanan paketin kaydedileceği dizini belirtir. Varsayılan olarak, özgün paketin imzalanmış paket tarafından üzerine yazılır.

- **`-Overwrite`**

  Geçerli imzanın üzerine yazılıp yazılmayacağını belirten geçiş yapın. Varsayılan olarak, pakette zaten imza varsa komut başarısız olur.

- **`-Timestamper`**

  RFC 3161 zaman damgası sunucusunun URL 'SI.

- **`-TimestampHashAlgorithm`**

  RFC 3161 zaman damgası sunucusu tarafından kullanılacak karma algoritması. Varsayılan olarak SHA256.

- **`-Verbosity [normal|quiet|detailed]`**

  Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .

## <a name="examples"></a>Örnekler

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
