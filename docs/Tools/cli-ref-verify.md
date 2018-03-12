---
title: "NuGet CLI doğrulayın komutu | Microsoft Docs"
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe başvurusunu komutu doğrulayın"
keywords: "nuget başvuru doğrulamak için komut doğrulayın"
ms.reviewer:
- karann
- rmpablos
ms.openlocfilehash: 2747491eb35d8685a44e86fcc1b572013982c754
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="f5f35-104">verify komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f5f35-104">verify command (NuGet CLI)</span></span>

<span data-ttu-id="f5f35-105">**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="f5f35-105">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f5f35-106">Bir paket doğrular.</span><span class="sxs-lookup"><span data-stu-id="f5f35-106">Verifies a package.</span></span>

## <a name="usage"></a><span data-ttu-id="f5f35-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="f5f35-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="f5f35-108">Burada `<package(s)>` bir veya daha fazla `.nupkg` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f5f35-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="f5f35-109">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="f5f35-109">Options</span></span>

| <span data-ttu-id="f5f35-110">Seçenek</span><span class="sxs-lookup"><span data-stu-id="f5f35-110">Option</span></span> | <span data-ttu-id="f5f35-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f5f35-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5f35-112">Tümü</span><span class="sxs-lookup"><span data-stu-id="f5f35-112">All</span></span> | <span data-ttu-id="f5f35-113">Tüm Doğrulamalar olası paketler üzerinde gerçekleştirilmelidir belirtir.</span><span class="sxs-lookup"><span data-stu-id="f5f35-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="f5f35-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f5f35-114">CertificateFingerprint</span></span> | <span data-ttu-id="f5f35-115">Bir veya daha fazla SHA-256 sertifika parmak izi imzalı hangi paketlerin imzalanmalıdır sertifikaların (s) belirtir.</span><span class="sxs-lookup"><span data-stu-id="f5f35-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="f5f35-116">SHA-256 sertifika parmak izi sertifika SHA-256 karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f5f35-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="f5f35-117">Birden çok girişi noktalı virgülle ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5f35-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="f5f35-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f5f35-118">ConfigFile</span></span> | <span data-ttu-id="f5f35-119">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="f5f35-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f5f35-120">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f5f35-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="f5f35-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f5f35-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f5f35-122">Bir sabit, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="f5f35-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f5f35-123">Yardım</span><span class="sxs-lookup"><span data-stu-id="f5f35-123">Help</span></span> | <span data-ttu-id="f5f35-124">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f5f35-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f5f35-125">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="f5f35-125">NonInteractive</span></span> | <span data-ttu-id="f5f35-126">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="f5f35-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f5f35-127">İmzalar</span><span class="sxs-lookup"><span data-stu-id="f5f35-127">Signatures</span></span> | <span data-ttu-id="f5f35-128">Paket imza doğrulaması gerçekleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f5f35-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="f5f35-129">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="f5f35-129">Verbosity</span></span> | <span data-ttu-id="f5f35-130">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="f5f35-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f5f35-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f5f35-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```