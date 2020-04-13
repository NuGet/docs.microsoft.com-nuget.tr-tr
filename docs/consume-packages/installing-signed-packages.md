---
title: Paket güven sınırlarını yönetme
description: İmzalı NuGet paketlerini yükleme ve paket imzası güven ayarlarını yapılandırma işlemini açıklar.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428984"
---
# <a name="manage-package-trust-boundaries"></a>Paket güven sınırlarını yönetme

İmzalı paketlerin yüklenmesi için belirli bir eylem gerekmez; ancak, içerik imzalandığından beri değiştirildiyse, yükleme [nu3008](../reference/errors-and-warnings/NU3008.md)hatasıyla engellenir.

> [!Warning]
> Güvenilmeyen sertifikalarla imzalanmış paketler imzasız olarak kabul edilir ve diğer imzalanmamış paket gibi herhangi bir uyarı veya hata olmadan yüklenir.

## <a name="configure-package-signature-requirements"></a>Paket imza gereksinimlerini yapılandırma

> [!Note]
> NuGet 4.9.0+ ve Visual Studio sürüm 15.9 ve daha sonra Windows gerektirir

NuGet istemcilerinin paket imzalarını nasıl doğruladığını `signatureValidationMode` `require` [`nuget config`](../reference/cli-reference/cli-ref-config.md) [nuget.config](../reference/nuget-config-file.md) dosyasında komutu kullanarak ayarlayarak yapılandırabilirsiniz.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Bu mod, tüm paketlerin dosyada güvenilen sertifikalardan `nuget.config` herhangi biri tarafından imzalandığıdoğrulanır. Bu dosya, sertifikanın parmak izine bağlı olarak hangi yazarlara ve/veya depolara güvenilmenizi sağlar.

### <a name="trust-package-author"></a>Paket yazarına güven

Yazar imzasına dayalı paketlere [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) güvenmek için `author` nuget.config özelliği ayarlamak için komutu kullanın.

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>Sertifikanın `nuget.exe` parmak izinin `SHA256` değerini almak için [doğrulama komutunu](../reference/cli-reference/cli-ref-verify.md) kullanın.


### <a name="trust-all-packages-from-a-repository"></a>Depodaki tüm paketlere güvenin

Depo imzasına dayalı paketlere güvenmek için `repository` aşağıdaki öğeyi kullanın:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Paket Sahiplerine Güven

Depo imzaları, paket sahiplerini teslim sırasında belirlemek için ek meta veriler içerir. Paketleri, sahipler listesine göre bir depodan kısıtlayabilirsiniz:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

Bir paketin birden çok sahibi varsa ve bu sahiplerden herhangi biri güvenilir listedeyse, paket yükleme başarılı olur.

### <a name="untrusted-root-certificates"></a>Güvenilmeyen Root sertifikaları

Bazı durumlarda, yerel makinede güvenilir bir köke zincirleme olmayan sertifikalar kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz. Bu davranışı `allowUntrustedRoot` özelleştirmek için özniteliği kullanabilirsiniz.

### <a name="sync-repository-certificates"></a>Resit asyon sertifikaları

Paket depoları, kullandıkları sertifikaları [hizmet dizini](../api/service-index.md)içinde duyurmalıdır. Sonunda depo, örneğin sertifikanın süresi dolduğunda bu sertifikaları güncelleştirecektir. Bu durumda, belirli ilkelere sahip istemciler, yeni eklenen sertifikayı eklemek için yapılandırmada bir güncelleştirme gerektirir. `nuget.exe` [Güvenilen imzalayanlar eşitleme komutunu](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)kullanarak depoyla ilişkili güvenilir imzalayanları kolayca yükseltebilirsiniz.

### <a name="schema-reference"></a>Şema referansı

İstemci ilkeleri için tam şema [referans nuget.config referans](../reference/nuget-config-file.md#trustedsigners-section) bulunabilir

## <a name="related-articles"></a>İlgili makaleler:

- [NuGet Paketlerini İmzalama](../create-packages/Sign-a-Package.md)
- [İmzalı Paketler Referans](../reference/Signed-Packages-Reference.md)
