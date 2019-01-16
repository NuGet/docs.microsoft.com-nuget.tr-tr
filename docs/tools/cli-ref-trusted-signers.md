---
title: NuGet CLI güvenilen İmzalayanları komutu
description: Nuget.exe güvenilen İmzalayanları komut başvurusu
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324714"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="41c48-103">Güvenilen İmzalayanları komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="41c48-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="41c48-104">**İçin geçerlidir:** paketini tüketim &bullet; **desteklenen sürümler:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="41c48-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="41c48-105">Alır veya güvenilen İmzalayanları için NuGet yapılandırmayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="41c48-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="41c48-106">Ek kullanım için bkz: [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="41c48-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="41c48-107">Nuget.config şema bakın gibi nasıl göründüğüne ilişkin ayrıntılar için [NuGet yapılandırma dosyası başvurusu](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="41c48-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="41c48-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="41c48-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="41c48-109">Hiçbiri `list|add|remove|sync` belirtilirse, komut için varsayılan `list`.</span><span class="sxs-lookup"><span data-stu-id="41c48-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="41c48-110">nuget güvenilen İmzalayanları listesi</span><span class="sxs-lookup"><span data-stu-id="41c48-110">nuget trusted-signers list</span></span>

<span data-ttu-id="41c48-111">Tüm güvenilen imzalayanlardan yapılandırmasında listeler.</span><span class="sxs-lookup"><span data-stu-id="41c48-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="41c48-112">Bu seçenek, tüm sertifikaları dahil edilir (parmak izi ve parmak izi algoritması ile) her imzalayan sahiptir.</span><span class="sxs-lookup"><span data-stu-id="41c48-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="41c48-113">Bir önceki bir sertifika varsa `[U]`, sertifika girdisi olduğu anlamına gelir `allowUntrustedRoot` yap `true`.</span><span class="sxs-lookup"><span data-stu-id="41c48-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="41c48-114">Bu komut bir örnek çıktısı aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="41c48-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="41c48-115">nuget güvenilen İmzalayanları [Seçenekler] ekleyin</span><span class="sxs-lookup"><span data-stu-id="41c48-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="41c48-116">Belirtilen ada sahip bir güvenilen imzalayan yapılandırmaya ekler. Bu seçenek bir güvenilen yazar veya depo eklemek için farklı hareketlerini sahiptir.</span><span class="sxs-lookup"><span data-stu-id="41c48-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="41c48-117">Bir paketine dayalı ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="41c48-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="41c48-118">Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="41c48-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="41c48-119">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41c48-119">Option</span></span> | <span data-ttu-id="41c48-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41c48-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41c48-121">Yazar</span><span class="sxs-lookup"><span data-stu-id="41c48-121">Author</span></span> | <span data-ttu-id="41c48-122">Paket yazarı imzası güvenilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="41c48-123">Havuz</span><span class="sxs-lookup"><span data-stu-id="41c48-123">Repository</span></span> | <span data-ttu-id="41c48-124">Depo imza veya onay imzası paketleri, güvenilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="41c48-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="41c48-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="41c48-126">İçin güvenilen imzalayan sertifika zinciri güvenilmeyen bir kökü için izin verilmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="41c48-127">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="41c48-127">Owners</span></span> | <span data-ttu-id="41c48-128">Bir havuzun güven kısıtlamanız güvenilen sahiplerinin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="41c48-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="41c48-129">Kullanırken yalnızca geçerli `-Repository` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="41c48-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="41c48-130">Hem `-Author` ve `-Repository` aynı anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="41c48-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="41c48-131">Bir hizmet dizinini temel alarak ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="41c48-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="41c48-132">_Not_: Bu seçenek yalnızca güvenilen depoları ekler.</span><span class="sxs-lookup"><span data-stu-id="41c48-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="41c48-133">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41c48-133">Option</span></span> | <span data-ttu-id="41c48-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41c48-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41c48-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="41c48-135">ServiceIndex</span></span> | <span data-ttu-id="41c48-136">Güvenilir olmasını deponun V3 hizmet dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="41c48-137">Depo imzaları kaynağını desteklemek bu depoyu sahiptir.</span><span class="sxs-lookup"><span data-stu-id="41c48-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="41c48-138">Sağlanmazsa, komutu bir paket kaynağıyla aynı arar `-Name` ve buradan hizmet dizini alın.</span><span class="sxs-lookup"><span data-stu-id="41c48-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="41c48-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="41c48-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="41c48-140">İçin güvenilen imzalayan sertifika zinciri güvenilmeyen bir kökü için izin verilmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="41c48-141">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="41c48-141">Owners</span></span> | <span data-ttu-id="41c48-142">Bir havuzun güven kısıtlamanız güvenilen sahiplerinin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="41c48-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="41c48-143">Seçenekler için sertifika bilgilere göre Ekle</span><span class="sxs-lookup"><span data-stu-id="41c48-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="41c48-144">_Not_: Belirtilen ada sahip bir güvenilen imzalayan zaten varsa, sertifika öğesi için imzalayan eklenir.</span><span class="sxs-lookup"><span data-stu-id="41c48-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="41c48-145">Aksi takdirde bir sertifika öğesi ile güvenilir Yazar oluşturulacak alanından sertifika bilgileri verilir.</span><span class="sxs-lookup"><span data-stu-id="41c48-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="41c48-146">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41c48-146">Option</span></span> | <span data-ttu-id="41c48-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41c48-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41c48-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="41c48-148">CertificateFingerprint</span></span> | <span data-ttu-id="41c48-149">İmzalanmış bir sertifikanın parmak izi ile imzalanmalıdır sertifikayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="41c48-150">Sertifika parmak izi sertifika karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="41c48-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="41c48-151">Bu karma olmalıdır hesaplamak için kullanılan karma algoritmasını belirtir `FingerprintAlgorithm` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="41c48-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="41c48-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="41c48-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="41c48-153">Sertifika parmak izi hesaplamak için kullanılan karma algoritmasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="41c48-154">Varsayılan olarak `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="41c48-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="41c48-155">Desteklenen değerler: `SHA256`, `SHA384` ve `SHA512`</span><span class="sxs-lookup"><span data-stu-id="41c48-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="41c48-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="41c48-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="41c48-157">İçin güvenilen imzalayan sertifika zinciri güvenilmeyen bir kökü için izin verilmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="41c48-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="41c48-158">nuget güvenilen İmzalayanları Kaldır - ad <name></span><span class="sxs-lookup"><span data-stu-id="41c48-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="41c48-159">Verilen ada uyan herhangi bir güvenilir İmzalayanları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="41c48-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="41c48-160">nuget güvenilen İmzalayanları eşitleme - ad <name></span><span class="sxs-lookup"><span data-stu-id="41c48-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="41c48-161">Şu anda güvenilir bir depoda güncelleştirmek için kullanılan sertifikaları en son listesi ister mevcut sertifika listesine güvenilir imzalayan.</span><span class="sxs-lookup"><span data-stu-id="41c48-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="41c48-162">_Not_: Bu hareket geçerli sertifikaların listesini silmek ve depodan güncel bir listesi yerine.</span><span class="sxs-lookup"><span data-stu-id="41c48-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="41c48-163">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="41c48-163">Options</span></span>

| <span data-ttu-id="41c48-164">Seçenek</span><span class="sxs-lookup"><span data-stu-id="41c48-164">Option</span></span> | <span data-ttu-id="41c48-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41c48-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41c48-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="41c48-166">ConfigFile</span></span> | <span data-ttu-id="41c48-167">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="41c48-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="41c48-168">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="41c48-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="41c48-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="41c48-169">ForceEnglishOutput</span></span> | <span data-ttu-id="41c48-170">Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="41c48-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="41c48-171">Yardım</span><span class="sxs-lookup"><span data-stu-id="41c48-171">Help</span></span> | <span data-ttu-id="41c48-172">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="41c48-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="41c48-173">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="41c48-173">Verbosity</span></span> | <span data-ttu-id="41c48-174">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="41c48-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="41c48-175">Örnekler</span><span class="sxs-lookup"><span data-stu-id="41c48-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
