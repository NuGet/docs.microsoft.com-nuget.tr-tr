---
title: NuGet CLı güvenilir-imzalayanlar komutu
description: nuget.exe Trusted-signers komutu için başvuru
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9dd3fe3786c824c4a0a1cb252aa50cfc4458a483
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859427"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="f9dfb-103">Güvenilen imzalayanlar komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="f9dfb-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="f9dfb-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="f9dfb-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="f9dfb-105">Güvenilen İmzalayanları NuGet yapılandırmasına alır veya ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="f9dfb-106">Ek kullanım için bkz. [ortak NuGet yapılandırması](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="f9dfb-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="f9dfb-107">nuget.config şemasının nasıl görüneceğine ilişkin ayrıntılar için [NuGet yapılandırma dosyası başvurusuna](../nuget-config-file.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f9dfb-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="f9dfb-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="f9dfb-109">hiçbiri `list|add|remove|sync` belirtilmemişse, komut varsayılan olarak olur `list` .</span><span class="sxs-lookup"><span data-stu-id="f9dfb-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="f9dfb-110">NuGet güvenilir-imzalayanlar listesi</span><span class="sxs-lookup"><span data-stu-id="f9dfb-110">nuget trusted-signers list</span></span>

<span data-ttu-id="f9dfb-111">Yapılandırmadaki tüm güvenilen İmzalayanları listeler.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="f9dfb-112">Bu seçenek, her İmzalayanın sahip olduğu tüm sertifikaları (parmak izi ve parmak izi algoritması) içerir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="f9dfb-113">Bir sertifika öncesinde varsa `[U]` , sertifika girişinin `allowUntrustedRoot` olarak ayarlandığı anlamına gelir `true` .</span><span class="sxs-lookup"><span data-stu-id="f9dfb-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="f9dfb-114">Bu komuttan bir örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f9dfb-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="f9dfb-115">NuGet güvenilir-imzalayanlar Add [seçenekler]</span><span class="sxs-lookup"><span data-stu-id="f9dfb-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="f9dfb-116">Yapılandırmaya verilen adı taşıyan güvenilen bir imzalayan ekler. Bu seçeneğin, güvenilen bir yazar veya depo eklemek için farklı hareketleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="f9dfb-117">Pakete dayalı ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f9dfb-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="f9dfb-118">Burada `<package(s)>` bir veya daha fazla `.nupkg` Dosya bulunur.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="f9dfb-119">Paket (ler) in yazar imzasında güvenilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="f9dfb-120">Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="f9dfb-121">Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="f9dfb-122">Yalnızca seçeneği kullanılırken geçerlidir `-Repository` .</span><span class="sxs-lookup"><span data-stu-id="f9dfb-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="f9dfb-123">Paket (lar) için depo imzasının veya onay imzasının güvenilir olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="f9dfb-124">`-Author` `-Repository` Aynı anda ve aynı zamanda sağlama desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="f9dfb-125">Hizmet dizinine dayalı ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f9dfb-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f9dfb-126">_Note_: Bu seçenek yalnızca güvenilen depolar ekler.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="f9dfb-127">Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="f9dfb-128">Bir deponun güvenini daha fazla kısıtlamak için güvenilen sahipler için noktalı virgülle ayrılmış liste.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="f9dfb-129">Güvenilecek deponun v3 hizmeti dizinini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="f9dfb-130">Bu depo, depo imzaları kaynağını desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="f9dfb-131">Sağlanmazsa, komut aynı olan bir paket kaynağını arar `-Name` ve hizmet dizinini buradan alır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="f9dfb-132">Sertifika bilgilerine göre ekleme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="f9dfb-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="f9dfb-133">_Note_: verilen ada sahip bir güvenilir imzalayan zaten varsa, sertifika öğesi bu İmzalayanın birlikte eklenir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="f9dfb-134">Aksi halde, belirtilen sertifika bilgileri 'nden bir sertifika öğesiyle güvenilir bir yazar oluşturulacaktır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="f9dfb-135">Güvenilen İmzalayanın sertifikasının güvenilmeyen bir köke zincirine izin verilip verilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="f9dfb-136">İmzalı paketlerin imzalı olması gereken bir sertifikanın sertifika parmak izlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="f9dfb-137">Sertifika parmak izi, sertifikanın bir karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="f9dfb-138">Bu karmayı hesaplamak için kullanılan karma algoritma, `FingerprintAlgorithm` seçeneğinde belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="f9dfb-139">Sertifika parmak izini hesaplamak için kullanılan karma algoritmasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="f9dfb-140">Varsayılan olarak olur `SHA256` .</span><span class="sxs-lookup"><span data-stu-id="f9dfb-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="f9dfb-141">Desteklenen değerler `SHA256` ve ' `SHA384` dir `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="f9dfb-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="f9dfb-142">NuGet güvenilir-imzalayanlar Remove-Name \<name\></span><span class="sxs-lookup"><span data-stu-id="f9dfb-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="f9dfb-143">Verilen adla eşleşen tüm güvenilen İmzalayanları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="f9dfb-144">NuGet güvenilir-imzalayanlar eşitleme-adı \<name\></span><span class="sxs-lookup"><span data-stu-id="f9dfb-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="f9dfb-145">Güvenilen İmzalayanın mevcut sertifika listesini güncelleştirmek için şu anda güvenilir bir depoda kullanılan sertifikaların en son listesini ister.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="f9dfb-146">_Note_: Bu hareket, geçerli sertifika listesini silecek ve bunları depodan güncel bir listeyle değiştirecek.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="f9dfb-147">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="f9dfb-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="f9dfb-148">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f9dfb-149">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="f9dfb-150">nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="f9dfb-151">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="f9dfb-152">Güvenilen İmzalayanın adı.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="f9dfb-153">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="f9dfb-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="f9dfb-154">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="f9dfb-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="f9dfb-155">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f9dfb-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
