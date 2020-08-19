---
title: NuGet CLı imza komutu
description: nuget.exe Sign komutu başvurusu
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622778"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="01a8d-103">Sign komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="01a8d-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="01a8d-104">**Uygulama hedefi:** paket oluşturma &bullet; **Desteklenen sürümler:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="01a8d-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="01a8d-105">İlk bağımsız değişkenle eşleşen tüm paketleri bir sertifikayla imzalar.</span><span class="sxs-lookup"><span data-stu-id="01a8d-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="01a8d-106">Özel anahtara sahip sertifika, bir dosya veya bir parmak izi sağlayarak bir sertifika deposunda yüklü olan bir sertifikadan elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="01a8d-107">Paket imzalama henüz .NET Core 'da, mono veya Windows dışı platformlarda desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="01a8d-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="01a8d-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="01a8d-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="01a8d-109">Burada `<package(s)>` bir veya daha fazla `.nupkg` Dosya bulunur.</span><span class="sxs-lookup"><span data-stu-id="01a8d-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="01a8d-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="01a8d-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="01a8d-111">Sertifika için bir yerel sertifika deposunda arama yapmak üzere kullanılan sertifikanın SHA-1 parmak izini belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="01a8d-112">Gerekirse sertifika parolasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="01a8d-113">Bir sertifika parola korumalıysa ancak parola sağlanmazsa, seçenek geçirilmediği takdirde komut çalışma zamanında bir parola ister `-NonInteractive` .</span><span class="sxs-lookup"><span data-stu-id="01a8d-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="01a8d-114">Paketi imzalarken kullanılacak sertifikanın dosya yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="01a8d-115">Sertifikayı aramak için kullanılan X. 509.440 sertifika deposunun adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="01a8d-116">Geçerli Kullanıcı tarafından kullanılan X. 509.440 sertifika deposu varsayılan olarak "CurrentUser" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="01a8d-117">Bu seçenek, sertifika veya seçenekler aracılığıyla belirtildiğinde kullanılmalıdır `-CertificateSubjectName` `-CertificateFingerprint` .</span><span class="sxs-lookup"><span data-stu-id="01a8d-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="01a8d-118">Sertifikayı aramak için kullanılacak X. 509.440 sertifika deposunun adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="01a8d-119">Kişisel sertifikalara ait X. 509.440 sertifika depolama alanı varsayılan olarak "My" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="01a8d-120">Bu seçenek, sertifika veya seçenekler aracılığıyla belirtildiğinde kullanılmalıdır `-CertificateSubjectName` `-CertificateFingerprint` .</span><span class="sxs-lookup"><span data-stu-id="01a8d-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="01a8d-121">Sertifika için bir yerel sertifika deposunda arama yapmak üzere kullanılan sertifikanın konu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="01a8d-122">Arama, diğer konu değerlerinden bağımsız olarak bu dizeyi içeren konu adına sahip tüm sertifikaları bulacak, sağlanan değeri kullanarak büyük/küçük harfe duyarsız bir dize karşılaştırmasından oluşur.</span><span class="sxs-lookup"><span data-stu-id="01a8d-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="01a8d-123">Sertifika deposu `-CertificateStoreName` ve seçenekleri ile belirtilebilir `-CertificateStoreLocation` .</span><span class="sxs-lookup"><span data-stu-id="01a8d-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="01a8d-124">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="01a8d-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="01a8d-125">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="01a8d-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="01a8d-126">nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="01a8d-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="01a8d-127">Paketi imzalamak için kullanılacak karma algoritması.</span><span class="sxs-lookup"><span data-stu-id="01a8d-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="01a8d-128">Varsayılan olarak SHA256.</span><span class="sxs-lookup"><span data-stu-id="01a8d-128">Defaults to SHA256.</span></span> <span data-ttu-id="01a8d-129">Olası değerler şunlardır SHA256, SHA384 ve SHA512 olur.</span><span class="sxs-lookup"><span data-stu-id="01a8d-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="01a8d-130">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="01a8d-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="01a8d-131">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="01a8d-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="01a8d-132">İmzalanan paketin kaydedileceği dizini belirtir.</span><span class="sxs-lookup"><span data-stu-id="01a8d-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="01a8d-133">Varsayılan olarak, özgün paketin imzalanmış paket tarafından üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="01a8d-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="01a8d-134">Geçerli imzanın üzerine yazılıp yazılmayacağını belirten geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="01a8d-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="01a8d-135">Varsayılan olarak, pakette zaten imza varsa komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="01a8d-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="01a8d-136">RFC 3161 zaman damgası sunucusunun URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="01a8d-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="01a8d-137">RFC 3161 zaman damgası sunucusu tarafından kullanılacak karma algoritması.</span><span class="sxs-lookup"><span data-stu-id="01a8d-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="01a8d-138">Varsayılan olarak SHA256.</span><span class="sxs-lookup"><span data-stu-id="01a8d-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="01a8d-139">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="01a8d-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="01a8d-140">Örnekler</span><span class="sxs-lookup"><span data-stu-id="01a8d-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
