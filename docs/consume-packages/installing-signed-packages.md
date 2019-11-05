---
title: Paket güven sınırlarını yönetme
description: İmzalı NuGet paketleri yükleme ve paket imzası güven ayarlarını yapılandırma sürecini açıklar.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 89b5fcbd76b85b77489ab36caa215c3a2fedf032
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610968"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="5b201-103">Paket güven sınırlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="5b201-103">Manage package trust boundaries</span></span>

<span data-ttu-id="5b201-104">İmzalı paketler, belirli bir eylemin yüklenmesini gerektirmez; Ancak, içerik imzalanmasından bu yana değiştirilmişse, yükleme [NU3008](../reference/errors-and-warnings/NU3008.md)hatasıyla engellenir.</span><span class="sxs-lookup"><span data-stu-id="5b201-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="5b201-105">Güvenilmeyen sertifikalarla imzalanmış paketler, imzasız olarak değerlendirilir ve herhangi bir imzasız pakette olduğu gibi herhangi bir uyarı veya hata olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5b201-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="5b201-106">Paket imza gereksinimlerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="5b201-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="5b201-107">Windows üzerinde NuGet 4.9.0 + ve Visual Studio sürüm 15,9 ve üstünü gerektirir</span><span class="sxs-lookup"><span data-stu-id="5b201-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="5b201-108">NuGet istemcilerinin, [`nuget config`](../reference/cli-reference/cli-ref-config.md) komutunu kullanarak [NuGet. config](../reference/nuget-config-file.md) dosyasında `require` `signatureValidationMode` ayarlayarak paket imzalarını nasıl doğruladığını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b201-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="5b201-109">Bu mod, tüm paketlerin `nuget.config` dosyasında güvenilen sertifikalar tarafından imzalandığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="5b201-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="5b201-110">Bu dosya, sertifikanın parmak izine göre hangi yazarların ve/veya depoların güvenilir olduğunu belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b201-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="5b201-111">Güven paketi yazarı</span><span class="sxs-lookup"><span data-stu-id="5b201-111">Trust package author</span></span>

<span data-ttu-id="5b201-112">Yazar imzasına göre paketlere güvenmek için, NuGet. config dosyasındaki `author` özelliğini ayarlamak üzere [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b201-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="5b201-113">Sertifikanın parmak izini `SHA256` değerini almak için `nuget.exe` [Verify komutunu](../reference/cli-reference/cli-ref-verify.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b201-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="5b201-114">Bir depodan tüm paketlere güvenin</span><span class="sxs-lookup"><span data-stu-id="5b201-114">Trust all packages from a repository</span></span>

<span data-ttu-id="5b201-115">Depo imzasına göre paketlere güvenmek için `repository` öğesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="5b201-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="5b201-116">Güven paketi sahipleri</span><span class="sxs-lookup"><span data-stu-id="5b201-116">Trust Package Owners</span></span>

<span data-ttu-id="5b201-117">Depo imzaları, gönderim sırasında paketin sahiplerini belirlemede ek meta veriler içerir.</span><span class="sxs-lookup"><span data-stu-id="5b201-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="5b201-118">Bir sahip listesine göre paketleri bir depodan kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b201-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="5b201-119">Bir paket birden çok Sahibe sahipse ve bu sahiplerden herhangi biri güvenilen listede ise, paket yüklemesi başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="5b201-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="5b201-120">Güvenilmeyen kök sertifikalar</span><span class="sxs-lookup"><span data-stu-id="5b201-120">Untrusted Root certificates</span></span>

<span data-ttu-id="5b201-121">Bazı durumlarda, yerel makinedeki güvenilir bir köke zincirsiz olmayan sertifikaları kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b201-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="5b201-122">Bu davranışı özelleştirmek için `allowUntrustedRoot` özniteliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b201-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="5b201-123">Depo sertifikalarını Eşitle</span><span class="sxs-lookup"><span data-stu-id="5b201-123">Sync repository certificates</span></span>

<span data-ttu-id="5b201-124">Paket depoları, kendi [hizmet dizininde](../api/service-index.md)kullandıkları sertifikaları duyurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5b201-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="5b201-125">Sonuç olarak, sertifikanın süresi dolduktan sonra depo bu sertifikaları güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="5b201-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="5b201-126">Bu durumda, belirli ilkelere sahip istemciler, yeni eklenen sertifikayı dahil etmek için yapılandırmada bir güncelleştirme yapılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b201-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="5b201-127">Bir depoyla ilişkili güvenilen İmzalayanları, `nuget.exe` [güvenilir-imzalayanların Sync komutu] (..) kullanarak kolayca yükseltebilirsiniz. /Reference/cli-Reference/cli-ref-Trusted-signers.MD # NuGet-güvenilen-signers-Sync--ad-Name</span><span class="sxs-lookup"><span data-stu-id="5b201-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name</span></span>

### <a name="schema-reference"></a><span data-ttu-id="5b201-128">Şema başvurusu</span><span class="sxs-lookup"><span data-stu-id="5b201-128">Schema reference</span></span>

<span data-ttu-id="5b201-129">İstemci ilkelerine ilişkin tüm şema başvurusu [NuGet. config başvurusunda](../reference/nuget-config-file.md#trustedsigners-section) bulunabilir</span><span class="sxs-lookup"><span data-stu-id="5b201-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="5b201-130">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="5b201-130">Related articles</span></span>

- [<span data-ttu-id="5b201-131">NuGet paketleri imzalanıyor</span><span class="sxs-lookup"><span data-stu-id="5b201-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="5b201-132">İmzalı paket başvurusu</span><span class="sxs-lookup"><span data-stu-id="5b201-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
