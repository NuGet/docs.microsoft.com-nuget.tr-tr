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
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="2f793-103">Paket güven sınırlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="2f793-103">Manage package trust boundaries</span></span>

<span data-ttu-id="2f793-104">İmzalı paketlerin yüklenmesi için belirli bir eylem gerekmez; ancak, içerik imzalandığından beri değiştirildiyse, yükleme [nu3008](../reference/errors-and-warnings/NU3008.md)hatasıyla engellenir.</span><span class="sxs-lookup"><span data-stu-id="2f793-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="2f793-105">Güvenilmeyen sertifikalarla imzalanmış paketler imzasız olarak kabul edilir ve diğer imzalanmamış paket gibi herhangi bir uyarı veya hata olmadan yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2f793-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="2f793-106">Paket imza gereksinimlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2f793-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="2f793-107">NuGet 4.9.0+ ve Visual Studio sürüm 15.9 ve daha sonra Windows gerektirir</span><span class="sxs-lookup"><span data-stu-id="2f793-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="2f793-108">NuGet istemcilerinin paket imzalarını nasıl doğruladığını `signatureValidationMode` `require` [`nuget config`](../reference/cli-reference/cli-ref-config.md) [nuget.config](../reference/nuget-config-file.md) dosyasında komutu kullanarak ayarlayarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f793-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="2f793-109">Bu mod, tüm paketlerin dosyada güvenilen sertifikalardan `nuget.config` herhangi biri tarafından imzalandığıdoğrulanır.</span><span class="sxs-lookup"><span data-stu-id="2f793-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="2f793-110">Bu dosya, sertifikanın parmak izine bağlı olarak hangi yazarlara ve/veya depolara güvenilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f793-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="2f793-111">Paket yazarına güven</span><span class="sxs-lookup"><span data-stu-id="2f793-111">Trust package author</span></span>

<span data-ttu-id="2f793-112">Yazar imzasına dayalı paketlere [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) güvenmek için `author` nuget.config özelliği ayarlamak için komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f793-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="2f793-113">Sertifikanın `nuget.exe` parmak izinin `SHA256` değerini almak için [doğrulama komutunu](../reference/cli-reference/cli-ref-verify.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f793-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="2f793-114">Depodaki tüm paketlere güvenin</span><span class="sxs-lookup"><span data-stu-id="2f793-114">Trust all packages from a repository</span></span>

<span data-ttu-id="2f793-115">Depo imzasına dayalı paketlere güvenmek için `repository` aşağıdaki öğeyi kullanın:</span><span class="sxs-lookup"><span data-stu-id="2f793-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="2f793-116">Paket Sahiplerine Güven</span><span class="sxs-lookup"><span data-stu-id="2f793-116">Trust Package Owners</span></span>

<span data-ttu-id="2f793-117">Depo imzaları, paket sahiplerini teslim sırasında belirlemek için ek meta veriler içerir.</span><span class="sxs-lookup"><span data-stu-id="2f793-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="2f793-118">Paketleri, sahipler listesine göre bir depodan kısıtlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2f793-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="2f793-119">Bir paketin birden çok sahibi varsa ve bu sahiplerden herhangi biri güvenilir listedeyse, paket yükleme başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="2f793-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="2f793-120">Güvenilmeyen Root sertifikaları</span><span class="sxs-lookup"><span data-stu-id="2f793-120">Untrusted Root certificates</span></span>

<span data-ttu-id="2f793-121">Bazı durumlarda, yerel makinede güvenilir bir köke zincirleme olmayan sertifikalar kullanarak doğrulamayı etkinleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f793-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="2f793-122">Bu davranışı `allowUntrustedRoot` özelleştirmek için özniteliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f793-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="2f793-123">Resit asyon sertifikaları</span><span class="sxs-lookup"><span data-stu-id="2f793-123">Sync repository certificates</span></span>

<span data-ttu-id="2f793-124">Paket depoları, kullandıkları sertifikaları [hizmet dizini](../api/service-index.md)içinde duyurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2f793-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="2f793-125">Sonunda depo, örneğin sertifikanın süresi dolduğunda bu sertifikaları güncelleştirecektir.</span><span class="sxs-lookup"><span data-stu-id="2f793-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="2f793-126">Bu durumda, belirli ilkelere sahip istemciler, yeni eklenen sertifikayı eklemek için yapılandırmada bir güncelleştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2f793-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="2f793-127">`nuget.exe` [Güvenilen imzalayanlar eşitleme komutunu](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)kullanarak depoyla ilişkili güvenilir imzalayanları kolayca yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f793-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="2f793-128">Şema referansı</span><span class="sxs-lookup"><span data-stu-id="2f793-128">Schema reference</span></span>

<span data-ttu-id="2f793-129">İstemci ilkeleri için tam şema [referans nuget.config referans](../reference/nuget-config-file.md#trustedsigners-section) bulunabilir</span><span class="sxs-lookup"><span data-stu-id="2f793-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="2f793-130">İlgili makaleler:</span><span class="sxs-lookup"><span data-stu-id="2f793-130">Related articles</span></span>

- [<span data-ttu-id="2f793-131">NuGet Paketlerini İmzalama</span><span class="sxs-lookup"><span data-stu-id="2f793-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="2f793-132">İmzalı Paketler Referans</span><span class="sxs-lookup"><span data-stu-id="2f793-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
