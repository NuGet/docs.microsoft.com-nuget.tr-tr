---
title: Paket güven sınırlarını yönetme
description: İmzalı NuGet paketleri yükleme ve paket imzası güven ayarlarını yapılandırma sürecini açıklar.
author: JonDouglas
ms.author: jodou
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 596ce330e434253e6fb200aa59ae4e14d47779ed
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774803"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="edc9d-103">Paket güven sınırlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="edc9d-103">Manage package trust boundaries</span></span>

<span data-ttu-id="edc9d-104">İmzalı paketler, belirli bir eylemin yüklenmesini gerektirmez; Ancak, içerik imzalanmasından bu yana değiştirilmişse, yükleme [NU3008](../reference/errors-and-warnings/NU3008.md)hatasıyla engellenir.</span><span class="sxs-lookup"><span data-stu-id="edc9d-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="edc9d-105">Güvenilmeyen sertifikalarla imzalanmış paketler, imzasız olarak değerlendirilir ve herhangi bir imzasız pakette olduğu gibi herhangi bir uyarı veya hata olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="edc9d-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="edc9d-106">Paket imza gereksinimlerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="edc9d-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="edc9d-107">Windows üzerinde NuGet 4.9.0 + ve Visual Studio sürüm 15,9 ve üstünü gerektirir</span><span class="sxs-lookup"><span data-stu-id="edc9d-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="edc9d-108">NuGet istemcilerinin, `signatureValidationMode` `require` komutunu kullanarak [nuget.config](../reference/nuget-config-file.md) dosyasında öğesini ayarlayarak paket imzalarını nasıl doğruladığını yapılandırabilirsiniz [`nuget config`](../reference/cli-reference/cli-ref-config.md) .</span><span class="sxs-lookup"><span data-stu-id="edc9d-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="edc9d-109">Bu mod, tüm paketlerin dosyada güvenilen sertifikalar tarafından imzalandığını doğrular `nuget.config` .</span><span class="sxs-lookup"><span data-stu-id="edc9d-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="edc9d-110">Bu dosya, sertifikanın parmak izine göre hangi yazarların ve/veya depoların güvenilir olduğunu belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="edc9d-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="edc9d-111">Güven paketi yazarı</span><span class="sxs-lookup"><span data-stu-id="edc9d-111">Trust package author</span></span>

<span data-ttu-id="edc9d-112">Yazar imzasına göre paketlere güvenmek için [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) komutunu kullanarak `author` nuget.config özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="edc9d-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="edc9d-113">`nuget.exe`Sertifikanın parmak izi değerini almak için [Verify komutunu](../reference/cli-reference/cli-ref-verify.md) kullanın `SHA256` .</span><span class="sxs-lookup"><span data-stu-id="edc9d-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="edc9d-114">Bir depodan tüm paketlere güvenin</span><span class="sxs-lookup"><span data-stu-id="edc9d-114">Trust all packages from a repository</span></span>

<span data-ttu-id="edc9d-115">Depo imzasına göre paketlere güvenmek için `repository` öğesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="edc9d-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="edc9d-116">Güven paketi sahipleri</span><span class="sxs-lookup"><span data-stu-id="edc9d-116">Trust Package Owners</span></span>

<span data-ttu-id="edc9d-117">Depo imzaları, gönderim sırasında paketin sahiplerini belirlemede ek meta veriler içerir.</span><span class="sxs-lookup"><span data-stu-id="edc9d-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="edc9d-118">Bir sahip listesine göre paketleri bir depodan kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="edc9d-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="edc9d-119">Bir paket birden çok Sahibe sahipse ve bu sahiplerden herhangi biri güvenilen listede ise, paket yüklemesi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="edc9d-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="edc9d-120">Güvenilmeyen kök sertifikalar</span><span class="sxs-lookup"><span data-stu-id="edc9d-120">Untrusted Root certificates</span></span>

<span data-ttu-id="edc9d-121">Bazı durumlarda, yerel makinedeki güvenilir bir köke zincirsiz olmayan sertifikaları kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edc9d-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="edc9d-122">`allowUntrustedRoot`Bu davranışı özelleştirmek için özniteliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edc9d-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="edc9d-123">Depo sertifikalarını Eşitle</span><span class="sxs-lookup"><span data-stu-id="edc9d-123">Sync repository certificates</span></span>

<span data-ttu-id="edc9d-124">Paket depoları, kendi [hizmet dizininde](../api/service-index.md)kullandıkları sertifikaları duyurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="edc9d-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="edc9d-125">Sonuç olarak, sertifikanın süresi dolduktan sonra depo bu sertifikaları güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="edc9d-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="edc9d-126">Bu durumda, belirli ilkelere sahip istemciler, yeni eklenen sertifikayı dahil etmek için yapılandırmada bir güncelleştirme yapılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="edc9d-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="edc9d-127">`nuget.exe` [Güvenilen imzalayanlar eşitleme komutunu](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)kullanarak bir depoyla ilişkili güvenilen İmzalayanları kolayca yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edc9d-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="edc9d-128">Şema başvurusu</span><span class="sxs-lookup"><span data-stu-id="edc9d-128">Schema reference</span></span>

<span data-ttu-id="edc9d-129">İstemci ilkelerine ilişkin tüm şema başvurusu [nuget.config başvurusunda](../reference/nuget-config-file.md#trustedsigners-section) bulunabilir</span><span class="sxs-lookup"><span data-stu-id="edc9d-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="edc9d-130">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="edc9d-130">Related articles</span></span>

- [<span data-ttu-id="edc9d-131">NuGet paketleri imzalanıyor</span><span class="sxs-lookup"><span data-stu-id="edc9d-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="edc9d-132">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="edc9d-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
