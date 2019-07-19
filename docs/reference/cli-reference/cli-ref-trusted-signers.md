---
title: NuGet CLı güvenilir-imzalayanlar komutu
description: NuGet. exe güvenilir-signers komutuna yönelik başvuru
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 197f2eaeed1a4a11f0f3ed426534807a0136271e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328266"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="7736f-103">Güvenilen imzalayanlar komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="7736f-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="7736f-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="7736f-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="7736f-105">Güvenilen İmzalayanları NuGet yapılandırmasına alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7736f-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="7736f-106">Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7736f-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="7736f-107">NuGet. config şemasının nasıl görüneceğine ilişkin ayrıntılar için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="7736f-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7736f-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="7736f-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="7736f-109">hiçbiri `list|add|remove|sync` belirtilmemişse, komut varsayılan olarak `list`olur.</span><span class="sxs-lookup"><span data-stu-id="7736f-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="7736f-110">NuGet güvenilir-imzalayanlar listesi</span><span class="sxs-lookup"><span data-stu-id="7736f-110">nuget trusted-signers list</span></span>

<span data-ttu-id="7736f-111">Yapılandırmadaki tüm güvenilen İmzalayanları listeler.</span><span class="sxs-lookup"><span data-stu-id="7736f-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="7736f-112">Bu seçenek, her İmzalayanın sahip olduğu tüm sertifikaları (parmak izi ve parmak izi algoritması) içerir.</span><span class="sxs-lookup"><span data-stu-id="7736f-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="7736f-113">Bir sertifika öncesinde `[U]`varsa, sertifika `allowUntrustedRoot` girişinin olarak `true`ayarlandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7736f-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="7736f-114">Bu komuttan bir örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7736f-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="7736f-115">NuGet güvenilir-imzalayanlar Add [seçenekler]</span><span class="sxs-lookup"><span data-stu-id="7736f-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="7736f-116">Yapılandırmaya verilen adı taşıyan güvenilen bir imzalayan ekler. Bu seçeneğin, güvenilen bir yazar veya depo eklemek için farklı hareketleri vardır.</span><span class="sxs-lookup"><span data-stu-id="7736f-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="7736f-117">Pakete dayalı ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7736f-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="7736f-118">Burada `<package(s)>` bir veya daha fazla `.nupkg` dosya bulunur.</span><span class="sxs-lookup"><span data-stu-id="7736f-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="7736f-119">Seçenek</span><span class="sxs-lookup"><span data-stu-id="7736f-119">Option</span></span> | <span data-ttu-id="7736f-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7736f-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7736f-121">Yazar</span><span class="sxs-lookup"><span data-stu-id="7736f-121">Author</span></span> | <span data-ttu-id="7736f-122">Paket (ler) in yazar imzasında güvenilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="7736f-123">Havuz</span><span class="sxs-lookup"><span data-stu-id="7736f-123">Repository</span></span> | <span data-ttu-id="7736f-124">Paket (lar) için depo imzasının veya onay imzasının güvenilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="7736f-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="7736f-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="7736f-126">Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="7736f-127">lere</span><span class="sxs-lookup"><span data-stu-id="7736f-127">Owners</span></span> | <span data-ttu-id="7736f-128">Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste.</span><span class="sxs-lookup"><span data-stu-id="7736f-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="7736f-129">Yalnızca `-Repository` seçeneği kullanılırken geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7736f-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="7736f-130">Aynı anda `-Repository` ve aynı zamanda sağlama desteklenmez. `-Author`</span><span class="sxs-lookup"><span data-stu-id="7736f-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="7736f-131">Hizmet dizinine dayalı ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7736f-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="7736f-132">_Not_: Bu seçenek yalnızca güvenilen depolar ekler.</span><span class="sxs-lookup"><span data-stu-id="7736f-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="7736f-133">Seçenek</span><span class="sxs-lookup"><span data-stu-id="7736f-133">Option</span></span> | <span data-ttu-id="7736f-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7736f-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7736f-135">Serviceındex</span><span class="sxs-lookup"><span data-stu-id="7736f-135">ServiceIndex</span></span> | <span data-ttu-id="7736f-136">Güvenilecek deponun v3 hizmeti dizinini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="7736f-137">Bu depo, depo imzaları kaynağını desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="7736f-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="7736f-138">Sağlanmazsa, komut aynı `-Name` olan bir paket kaynağını arar ve hizmet dizinini buradan alır.</span><span class="sxs-lookup"><span data-stu-id="7736f-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="7736f-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="7736f-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="7736f-140">Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="7736f-141">lere</span><span class="sxs-lookup"><span data-stu-id="7736f-141">Owners</span></span> | <span data-ttu-id="7736f-142">Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste.</span><span class="sxs-lookup"><span data-stu-id="7736f-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="7736f-143">Sertifika bilgilerine göre ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7736f-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="7736f-144">_Not_: Verilen ada sahip bir güvenilir imzalayan zaten varsa, sertifika öğesi bu İmzalayanın birlikte eklenir.</span><span class="sxs-lookup"><span data-stu-id="7736f-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="7736f-145">Aksi halde, belirtilen sertifika bilgileri 'nden bir sertifika öğesiyle güvenilir bir yazar oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="7736f-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="7736f-146">Seçenek</span><span class="sxs-lookup"><span data-stu-id="7736f-146">Option</span></span> | <span data-ttu-id="7736f-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7736f-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7736f-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="7736f-148">CertificateFingerprint</span></span> | <span data-ttu-id="7736f-149">İmzalı paketlerin imzalı olması gereken bir sertifikanın sertifika parmak izlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="7736f-150">Sertifika parmak izi, sertifikanın bir karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="7736f-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="7736f-151">Bu karmayı hesaplamak için kullanılan karma algoritma, `FingerprintAlgorithm` seçeneğinde belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7736f-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="7736f-152">Parmak izi Talgorithd</span><span class="sxs-lookup"><span data-stu-id="7736f-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="7736f-153">Sertifika parmak izini hesaplamak için kullanılan karma algoritmasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="7736f-154">Varsayılan olarak `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="7736f-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="7736f-155">Desteklenen değerler şunlardır `SHA256`ve `SHA384``SHA512`</span><span class="sxs-lookup"><span data-stu-id="7736f-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="7736f-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="7736f-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="7736f-157">Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7736f-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="7736f-158">NuGet güvenilir-imzalayanlar Remove-Name<name></span><span class="sxs-lookup"><span data-stu-id="7736f-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="7736f-159">Verilen adla eşleşen tüm güvenilen İmzalayanları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7736f-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="7736f-160">NuGet güvenilir-imzalayanlar eşitleme-adı<name></span><span class="sxs-lookup"><span data-stu-id="7736f-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="7736f-161">Güvenilen İmzalayanın mevcut sertifika listesini güncelleştirmek için şu anda güvenilir bir depoda kullanılan sertifikaların en son listesini ister.</span><span class="sxs-lookup"><span data-stu-id="7736f-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="7736f-162">_Not_: Bu hareket, geçerli sertifika listesini silecek ve bunları depodan güncel bir listeyle değiştirecek.</span><span class="sxs-lookup"><span data-stu-id="7736f-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="7736f-163">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="7736f-163">Options</span></span>

| <span data-ttu-id="7736f-164">Seçenek</span><span class="sxs-lookup"><span data-stu-id="7736f-164">Option</span></span> | <span data-ttu-id="7736f-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7736f-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7736f-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7736f-166">ConfigFile</span></span> | <span data-ttu-id="7736f-167">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="7736f-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7736f-168">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7736f-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7736f-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7736f-169">ForceEnglishOutput</span></span> | <span data-ttu-id="7736f-170">NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="7736f-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7736f-171">Help</span><span class="sxs-lookup"><span data-stu-id="7736f-171">Help</span></span> | <span data-ttu-id="7736f-172">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7736f-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="7736f-173">Verbosity</span><span class="sxs-lookup"><span data-stu-id="7736f-173">Verbosity</span></span> | <span data-ttu-id="7736f-174">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="7736f-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="7736f-175">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7736f-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
