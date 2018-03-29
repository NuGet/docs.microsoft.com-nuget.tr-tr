---
title: NuGet CLI oturum komutu | Microsoft Docs
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe oturum komut başvurusu
keywords: nuget oturum başvuru, oturum komutu
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9c83e5abae0e70cdc62917861c1febfce4f792c7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="e78bb-104">oturum komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e78bb-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="e78bb-105">**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="e78bb-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="e78bb-106">İlk bağımsız değişkeni bir sertifika ile eşleşen tüm paketler imzalar.</span><span class="sxs-lookup"><span data-stu-id="e78bb-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="e78bb-107">Sertifikanın özel anahtarı olan bir dosya ya da bir konu adı veya bir parmak izi sağlayarak bir sertifika deposunda yüklü bir sertifika elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="e78bb-108">Paket imzalama, Mono altında veya Windows olmayan platformlarında henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e78bb-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="e78bb-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="e78bb-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="e78bb-110">Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e78bb-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="e78bb-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="e78bb-111">Options</span></span>

| <span data-ttu-id="e78bb-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="e78bb-112">Option</span></span> | <span data-ttu-id="e78bb-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e78bb-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e78bb-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="e78bb-114">CertificateFingerprint</span></span> | <span data-ttu-id="e78bb-115">SHA-1 parmak izi sertifika için bir yerel sertifika deposu aramak için kullanılan sertifikanın belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="e78bb-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="e78bb-116">CertificatePassword</span></span> | <span data-ttu-id="e78bb-117">Sertifika parolası gerekirse belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="e78bb-118">Parola korumalı bir sertifikadır, ancak hiçbir parola sağlanan komutu için bir parola çalışma zamanında sürece ister etkileşimli olmayan seçeneği geçirilir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="e78bb-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="e78bb-119">CertificatePath</span></span> | <span data-ttu-id="e78bb-120">Paketin imzalanması kullanılmak üzere sertifika dosya yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="e78bb-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="e78bb-121">CertificateStoreLocation</span></span> | <span data-ttu-id="e78bb-122">Sertifikayı aramak için X.509 Sertifika deposu kullanımı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="e78bb-123">Varsayılan olarak "Currentuser'a", geçerli bir kullanıcı tarafından kullanılan X.509 Sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="e78bb-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="e78bb-124">Bu seçenek, sertifikayı CertificateSubjectName - veya - CertificateFingerprint seçenekleri aracılığıyla belirtirken kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e78bb-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="e78bb-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="e78bb-125">CertificateStoreName</span></span> | <span data-ttu-id="e78bb-126">Sertifika bulmak için kullanılacak X.509 Sertifika deposu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="e78bb-127">Varsayılan olarak "Benim", kişisel sertifikalar için X.509 Sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="e78bb-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="e78bb-128">Bu seçenek, sertifikayı CertificateSubjectName - veya - CertificateFingerprint seçenekleri aracılığıyla belirtirken kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e78bb-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="e78bb-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="e78bb-129">CertificateSubjectName</span></span> | <span data-ttu-id="e78bb-130">Sertifika için bir yerel sertifika deposu aramak için kullanılan sertifikanın konu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="e78bb-131">Arama diğer konu değerlerinden bağımsız olarak o dizeyi içeren konu adına sahip tüm sertifikaların bulur sağlanan değer kullanarak büyük küçük harf duyarlı dize karşılaştırmasının olur.</span><span class="sxs-lookup"><span data-stu-id="e78bb-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="e78bb-132">Sertifika deposu - SertifikaDeposuAdı ve - CertificateStoreLocation seçenekleri ile belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="e78bb-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e78bb-133">ConfigFile</span></span> | <span data-ttu-id="e78bb-134">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="e78bb-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e78bb-135">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e78bb-135">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="e78bb-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e78bb-136">ForceEnglishOutput</span></span> | <span data-ttu-id="e78bb-137">Bir sabit, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="e78bb-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e78bb-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="e78bb-138">HashAlgorithm</span></span> | <span data-ttu-id="e78bb-139">Paketi imzalamak için kullanılan karma algoritması.</span><span class="sxs-lookup"><span data-stu-id="e78bb-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="e78bb-140">Varsayılan olarak SHA256.</span><span class="sxs-lookup"><span data-stu-id="e78bb-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="e78bb-141">Yardım</span><span class="sxs-lookup"><span data-stu-id="e78bb-141">Help</span></span> | <span data-ttu-id="e78bb-142">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e78bb-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="e78bb-143">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="e78bb-143">NonInteractive</span></span> | <span data-ttu-id="e78bb-144">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="e78bb-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e78bb-145">Çıktıdizini</span><span class="sxs-lookup"><span data-stu-id="e78bb-145">OutputDirectory</span></span> | <span data-ttu-id="e78bb-146">İmzalı paketinin kaydedileceği dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e78bb-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="e78bb-147">Varsayılan olarak özgün paket imzalı paketi tarafından üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="e78bb-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="e78bb-148">Üzerine yaz</span><span class="sxs-lookup"><span data-stu-id="e78bb-148">Overwrite</span></span> | <span data-ttu-id="e78bb-149">Geçerli imza üzerine göstermek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="e78bb-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="e78bb-150">Paket imza zaten varsa, varsayılan olarak komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e78bb-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="e78bb-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="e78bb-151">Timestamper</span></span> | <span data-ttu-id="e78bb-152">RFC 3161 zaman damgası sunucu URL'si.</span><span class="sxs-lookup"><span data-stu-id="e78bb-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="e78bb-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="e78bb-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="e78bb-154">RFC 3161 zaman damgası sunucusu tarafından kullanılan karma algoritması.</span><span class="sxs-lookup"><span data-stu-id="e78bb-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="e78bb-155">Varsayılan olarak SHA256.</span><span class="sxs-lookup"><span data-stu-id="e78bb-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="e78bb-156">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="e78bb-156">Verbosity</span></span> | <span data-ttu-id="e78bb-157">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="e78bb-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="e78bb-158">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e78bb-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```