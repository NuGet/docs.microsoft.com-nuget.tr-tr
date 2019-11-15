---
title: Paket güven sınırlarını yönetme
description: İmzalı NuGet paketleri yükleme ve paket imzası güven ayarlarını yapılandırma sürecini açıklar.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096861"
---
# <a name="manage-package-trust-boundaries"></a>Paket güven sınırlarını yönetme

İmzalı paketler, belirli bir eylemin yüklenmesini gerektirmez; Ancak, içerik imzalanmasından bu yana değiştirilmişse, yükleme [NU3008](../reference/errors-and-warnings/NU3008.md)hatasıyla engellenir.

> [!Warning]
> Güvenilmeyen sertifikalarla imzalanmış paketler, imzasız olarak değerlendirilir ve herhangi bir imzasız pakette olduğu gibi herhangi bir uyarı veya hata olmadan yüklenir.

## <a name="configure-package-signature-requirements"></a>Paket imza gereksinimlerini Yapılandır

> [!Note]
> Windows üzerinde NuGet 4.9.0 + ve Visual Studio sürüm 15,9 ve üstünü gerektirir

NuGet istemcilerinin, [`nuget config`](../reference/cli-reference/cli-ref-config.md) komutunu kullanarak [NuGet. config](../reference/nuget-config-file.md) dosyasında `require` `signatureValidationMode` ayarlayarak paket imzalarını nasıl doğruladığını yapılandırabilirsiniz.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Bu mod, tüm paketlerin `nuget.config` dosyasında güvenilen sertifikalar tarafından imzalandığını doğrular. Bu dosya, sertifikanın parmak izine göre hangi yazarların ve/veya depoların güvenilir olduğunu belirtmenizi sağlar.

### <a name="trust-package-author"></a>Güven paketi yazarı

Yazar imzasına göre paketlere güvenmek için, NuGet. config dosyasındaki `author` özelliğini ayarlamak üzere [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) komutunu kullanın.

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
>Sertifikanın parmak izini `SHA256` değerini almak için `nuget.exe` [Verify komutunu](../reference/cli-reference/cli-ref-verify.md) kullanın.


### <a name="trust-all-packages-from-a-repository"></a>Bir depodan tüm paketlere güvenin

Depo imzasına göre paketlere güvenmek için `repository` öğesini kullanın:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Güven paketi sahipleri

Depo imzaları, gönderim sırasında paketin sahiplerini belirlemede ek meta veriler içerir. Bir sahip listesine göre paketleri bir depodan kısıtlayabilirsiniz:

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

Bir paket birden çok Sahibe sahipse ve bu sahiplerden herhangi biri güvenilen listede ise, paket yüklemesi başarılı olur.

### <a name="untrusted-root-certificates"></a>Güvenilmeyen kök sertifikalar

Bazı durumlarda, yerel makinedeki güvenilir bir köke zincirsiz olmayan sertifikaları kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz. Bu davranışı özelleştirmek için `allowUntrustedRoot` özniteliğini kullanabilirsiniz.

### <a name="sync-repository-certificates"></a>Depo sertifikalarını Eşitle

Paket depoları, kendi [hizmet dizininde](../api/service-index.md)kullandıkları sertifikaları duyurmalıdır. Sonuç olarak, sertifikanın süresi dolduktan sonra depo bu sertifikaları güncelleştirir. Bu durumda, belirli ilkelere sahip istemciler, yeni eklenen sertifikayı dahil etmek için yapılandırmada bir güncelleştirme yapılmasını gerektirir. `nuget.exe` [güvenilir-imzalayanların sync komutunu](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)kullanarak bir depoyla ilişkili güvenilen İmzalayanları kolayca yükseltebilirsiniz.

### <a name="schema-reference"></a>Şema başvurusu

İstemci ilkelerine ilişkin tüm şema başvurusu [NuGet. config başvurusunda](../reference/nuget-config-file.md#trustedsigners-section) bulunabilir

## <a name="related-articles"></a>İlgili makaleler

- [NuGet paketleri imzalanıyor](../create-packages/Sign-a-Package.md)
- [İmzalı paket başvurusu](../reference/Signed-Packages-Reference.md)
