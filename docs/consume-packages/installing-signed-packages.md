---
title: Paket güven sınırları yönetme
description: İmzalı NuGet yükleme işlemi açıklanmıştır paketler ve yapılandırma paket imzası güven ayarlar.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 8da57dc295ea78f2eb183226fc9b2f4a37e3f5db
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426628"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="3ea56-103">Paket güven sınırları yönetme</span><span class="sxs-lookup"><span data-stu-id="3ea56-103">Manage package trust boundaries</span></span>

<span data-ttu-id="3ea56-104">İmzalı paketlerin yüklenmesi için herhangi bir özel işlem gerektirmez; Ancak, içeriği imzalandıktan sonra değiştirilmişse yükleme hatasıyla engellendi [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="3ea56-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="3ea56-105">Güvenilmeyen Sertifikalar ile imzalanmış paketleri olarak kabul edilir olarak imzalanmamış ve uyarıları veya hataları gibi diğer herhangi bir işaretsiz paket olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3ea56-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="3ea56-106">Paket imzası gereksinimlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3ea56-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="3ea56-107">NuGet 4.9.0+ ve Visual Studio sürüm 15.9 ve daha sonra Windows gerektirir</span><span class="sxs-lookup"><span data-stu-id="3ea56-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="3ea56-108">NuGet istemcileri ayarlayarak paket imzaları nasıl doğrulamak yapılandırabilirsiniz `signatureValidationMode` için `require` içinde [nuget.config](../reference/nuget-config-file.md) kullanarak dosya [ `nuget config` ](../tools/cli-ref-config.md) komutu.</span><span class="sxs-lookup"><span data-stu-id="3ea56-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../tools/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="3ea56-109">Bu mod, tüm paketler herhangi biri, güvenilen sertifika tarafından imzalanmış doğrular `nuget.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="3ea56-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="3ea56-110">Bu dosya hangi yazarlar belirtmenizi sağlar ve/veya sertifikanın parmak izi üzerinde tabanlı depoları güvenilir.</span><span class="sxs-lookup"><span data-stu-id="3ea56-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="3ea56-111">Paket yazarı güven</span><span class="sxs-lookup"><span data-stu-id="3ea56-111">Trust package author</span></span>

<span data-ttu-id="3ea56-112">Yazar imza kullanıma bağlı paketleri güvenmeyi [ `trusted-signers` ](../tools/cli-ref-trusted-signers.md) ayarlamak için komutu `author` nuget.Config'de özelliği.</span><span class="sxs-lookup"><span data-stu-id="3ea56-112">To trust packages based on the author signature use the [`trusted-signers`](../tools/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="3ea56-113">Kullanım `nuget.exe` [komutu doğrulayın](../tools/cli-ref-verify.md) almak için `SHA256` sertifikanın parmak izi değeri.</span><span class="sxs-lookup"><span data-stu-id="3ea56-113">Use the `nuget.exe` [verify command](../tools/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="3ea56-114">Bir depodan tüm paketler güven</span><span class="sxs-lookup"><span data-stu-id="3ea56-114">Trust all packages from a repository</span></span>

<span data-ttu-id="3ea56-115">Depo imza kullanıma bağlı paketleri güvenmeyi `repository` öğesi:</span><span class="sxs-lookup"><span data-stu-id="3ea56-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="3ea56-116">Paket sahipleri güven</span><span class="sxs-lookup"><span data-stu-id="3ea56-116">Trust Package Owners</span></span>

<span data-ttu-id="3ea56-117">Gönderme sırasındaki paket sahipleri belirlemek için ek meta veri deposu imzaları içerir.</span><span class="sxs-lookup"><span data-stu-id="3ea56-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="3ea56-118">Sahipler listesini temel alan bir depodan paketler kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3ea56-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="3ea56-119">Bir paket birden fazla sahibe vardır ve bu sahipler herhangi bir güvenilir listesinde paket yüklemesi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="3ea56-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="3ea56-120">Güvenilmeyen kök sertifikalar</span><span class="sxs-lookup"><span data-stu-id="3ea56-120">Untrusted Root certificates</span></span>

<span data-ttu-id="3ea56-121">Bazı durumlarda yerel makinede güvenilir bir kök zincir şeklinde bağlanmayan sertifikaları kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ea56-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="3ea56-122">Kullanabileceğiniz `allowUntrustedRoot` bu davranışını özelleştirmek için özniteliği.</span><span class="sxs-lookup"><span data-stu-id="3ea56-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="3ea56-123">Eşitleme depo sertifikaları</span><span class="sxs-lookup"><span data-stu-id="3ea56-123">Sync repository certificates</span></span>

<span data-ttu-id="3ea56-124">Paket depolarınızın içinde kullandıkları sertifikaları duyurmaktan kendi [hizmet dizini](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="3ea56-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="3ea56-125">Bu sertifikalar depo sonunda güncelleştirilir sertifika dolduğunda örn.</span><span class="sxs-lookup"><span data-stu-id="3ea56-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="3ea56-126">Bu durum oluştuğunda, istemcileri belirli ilkeleri ile yapılandırma yeni eklenen sertifika eklemek için bir güncelleştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3ea56-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="3ea56-127">Kullanarak bir depoya ilişkili güvenilen imzalayanlardan kolayca yükseltebilirsiniz `nuget.exe` [güvenilen İmzalayanları sync komutunu](../tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span><span class="sxs-lookup"><span data-stu-id="3ea56-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="3ea56-128">Şema başvurusu</span><span class="sxs-lookup"><span data-stu-id="3ea56-128">Schema reference</span></span>

<span data-ttu-id="3ea56-129">İstemci ilkelerinin tam şeması başvurusunu bulunabilir [nuget.config başvurusu](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="3ea56-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="3ea56-130">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="3ea56-130">Related articles</span></span>

- [<span data-ttu-id="3ea56-131">NuGet paketlerini imzalama</span><span class="sxs-lookup"><span data-stu-id="3ea56-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="3ea56-132">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="3ea56-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
