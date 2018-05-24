---
title: NuGet CLI komutu doğrulayın
description: Nuget.exe başvurusunu komutu doğrulayın
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/23/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="58d4f-103">verify komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="58d4f-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="58d4f-104">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="58d4f-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="58d4f-105">Bir paket doğrular.</span><span class="sxs-lookup"><span data-stu-id="58d4f-105">Verifies a package.</span></span>

<span data-ttu-id="58d4f-106">İmzalı paketlerin doğrulama, .NET Core, Mono altında ya da Windows olmayan platformlarında içinde henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="58d4f-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="58d4f-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="58d4f-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="58d4f-108">Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="58d4f-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="58d4f-109">nuget doğrulama - tüm</span><span class="sxs-lookup"><span data-stu-id="58d4f-109">nuget verify -All</span></span>

<span data-ttu-id="58d4f-110">Tüm Doğrulamalar olası paketler üzerinde gerçekleştirilmelidir belirtir.</span><span class="sxs-lookup"><span data-stu-id="58d4f-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="58d4f-111">nuget doğrulama - imzaları</span><span class="sxs-lookup"><span data-stu-id="58d4f-111">nuget verify -Signatures</span></span>

<span data-ttu-id="58d4f-112">Paket imza doğrulaması gerçekleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="58d4f-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="58d4f-113">"Doğrulama - imzaları" seçenekleri</span><span class="sxs-lookup"><span data-stu-id="58d4f-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="58d4f-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="58d4f-114">Option</span></span> | <span data-ttu-id="58d4f-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="58d4f-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58d4f-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="58d4f-116">CertificateFingerprint</span></span> | <span data-ttu-id="58d4f-117">Bir veya daha fazla SHA-256 sertifika parmak izi imzalı hangi paketlerin imzalanmalıdır sertifikaların (s) belirtir.</span><span class="sxs-lookup"><span data-stu-id="58d4f-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="58d4f-118">SHA-256 sertifika parmak izi sertifika SHA-256 karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="58d4f-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="58d4f-119">Birden çok girişi noktalı virgülle ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58d4f-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="58d4f-120">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="58d4f-120">Options</span></span>

| <span data-ttu-id="58d4f-121">Seçenek</span><span class="sxs-lookup"><span data-stu-id="58d4f-121">Option</span></span> | <span data-ttu-id="58d4f-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="58d4f-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="58d4f-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="58d4f-123">ConfigFile</span></span> | <span data-ttu-id="58d4f-124">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="58d4f-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="58d4f-125">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58d4f-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="58d4f-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="58d4f-126">ForceEnglishOutput</span></span> | <span data-ttu-id="58d4f-127">Bir sabit, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="58d4f-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="58d4f-128">Yardım</span><span class="sxs-lookup"><span data-stu-id="58d4f-128">Help</span></span> | <span data-ttu-id="58d4f-129">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="58d4f-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="58d4f-130">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="58d4f-130">Verbosity</span></span> | <span data-ttu-id="58d4f-131">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="58d4f-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="58d4f-132">Örnekler</span><span class="sxs-lookup"><span data-stu-id="58d4f-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```