---
title: İmzalı bir NuGet paketini yükle
description: İmzalı NuGet yükleme işlemi açıklanmıştır paketler ve yapılandırma paket imzası güven ayarlar.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977852"
---
# <a name="install-a-signed-package"></a>İmzalı paket yükleme

İmzalı paketlerin yüklenmesi için herhangi bir özel işlem gerektirmez; Ancak, içeriği imzalandıktan sonra değiştirilmişse yükleme hatasıyla engellendi [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Güvenilmeyen Sertifikalar ile imzalanmış paketleri olarak kabul edilir olarak imzalanmamış ve uyarıları veya hataları gibi diğer herhangi bir işaretsiz paket olmadan yüklenir.

## <a name="configure-package-signature-requirements"></a>Paket imzası gereksinimlerini yapılandırma

> [!Note]
> NuGet 4.9.0+ ve Visual Studio sürüm 15.9 ve daha sonra Windows gerektirir

NuGet istemcileri ayarlayarak paket imzaları nasıl doğrulamak yapılandırabilirsiniz `signatureValidationMode` için `require` içinde [nuget.config](../reference/nuget-config-file) kullanarak dosya [ `nuget config` ](../tools/cli-ref-config) komutu.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Bu mod, tüm paketler herhangi biri, güvenilen sertifika tarafından imzalanmış doğrular `nuget.config` dosya. Bu dosya hangi yazarlar belirtmenizi sağlar ve/veya sertifikanın parmak izi üzerinde tabanlı depoları güvenilir.

### <a name="trust-package-author"></a>Paket yazarı güven

Yazar imza kullanıma bağlı paketleri güvenmeyi [ `trusted-signers` ](..tools/cli-ref-trusted-signers) ayarlamak için komutu `author` nuget.Config'de özelliği.

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
>Kullanım `nuget.exe` [komutu doğrulayın](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) almak için `SHA256` sertifikanın parmak izi değeri.


### <a name="trust-all-packages-from-a-repository"></a>Bir depodan tüm paketler güven

Depo imza kullanıma bağlı paketleri güvenmeyi `repository` öğesi:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Paket sahipleri güven

Gönderme sırasındaki paket sahipleri belirlemek için ek meta veri deposu imzaları içerir. Sahipler listesini temel alan bir depodan paketler kısıtlayabilirsiniz:

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

Bir paket birden fazla sahibe vardır ve bu sahipler herhangi bir güvenilir listesinde paket yüklemesi başarısız olur.

### <a name="untrusted-root-certificates"></a>Güvenilmeyen kök sertifikalar

Bazı durumlarda yerel makinede güvenilir bir kök zincir şeklinde bağlanmayan sertifikaları kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz. Kullanabileceğiniz `allowUntrustedRoot` bu davranışını özelleştirmek için özniteliği.

### <a name="sync-repository-certificates"></a>Eşitleme depo sertifikaları

Paket depolarınızın içinde kullandıkları sertifikaları duyurmaktan kendi [hizmet dizini](https://docs.microsoft.com/en-us/nuget/api/service-index). Bu sertifikalar depo sonunda güncelleştirilir sertifika dolduğunda örn. Bu durum oluştuğunda, istemcileri belirli ilkeleri ile yapılandırma yeni eklenen sertifika eklemek için bir güncelleştirme gerektirir. Kullanarak bir depoya ilişkili güvenilen imzalayanlardan kolayca yükseltebilirsiniz `nuget.exe` [güvenilen İmzalayanları sync komutunu](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).

### <a name="schema-reference"></a>Şema başvurusu

İstemci ilkelerinin tam şeması başvurusunu bulunabilir [nuget.config başvurusu](/nuget/reference/nuget-config-file#trustedsigners-section)

## <a name="related-articles"></a>İlgili makaleler

- [Bir NuGet paketini yüklemek için farklı yollar](ways-to-install-a-package.md)
- [NuGet paketlerini imzalama](../create-packages/Sign-a-Package.md)
- [İmzalı paket başvurusu](../reference/Signed-Packages-Reference.md)
