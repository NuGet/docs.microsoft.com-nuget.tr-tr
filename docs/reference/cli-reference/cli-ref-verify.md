---
title: NuGet CLı doğrulama komutu
description: NuGet. exe Verify komutu için başvuru
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328254"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="90988-103">Verify komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="90988-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="90988-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="90988-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="90988-105">Bir paketi doğrular.</span><span class="sxs-lookup"><span data-stu-id="90988-105">Verifies a package.</span></span>

<span data-ttu-id="90988-106">İmzalanmış paketlerin doğrulanması henüz .NET Core 'da, mono kapsamında veya Windows dışı platformlarda desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="90988-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="90988-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="90988-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="90988-108">Burada `<package(s)>` bir veya daha fazla `.nupkg` dosya bulunur.</span><span class="sxs-lookup"><span data-stu-id="90988-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="90988-109">NuGet Verify-tümü</span><span class="sxs-lookup"><span data-stu-id="90988-109">nuget verify -All</span></span>

<span data-ttu-id="90988-110">Tüm doğrulamaları, paketler üzerinde gerçekleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="90988-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="90988-111">NuGet doğrulama-Imzalar</span><span class="sxs-lookup"><span data-stu-id="90988-111">nuget verify -Signatures</span></span>

<span data-ttu-id="90988-112">Paket imzası doğrulamasının gerçekleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="90988-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="90988-113">"Verify-Imzalara" seçenekleri</span><span class="sxs-lookup"><span data-stu-id="90988-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="90988-114">Seçenek</span><span class="sxs-lookup"><span data-stu-id="90988-114">Option</span></span> | <span data-ttu-id="90988-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="90988-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="90988-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="90988-116">CertificateFingerprint</span></span> | <span data-ttu-id="90988-117">İmzalı paketlerin imzalı olması gereken sertifikaların bir veya daha fazla SHA-256 sertifikası parmak izlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="90988-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="90988-118">Bir sertifika SHA-256 parmak izi, sertifikanın SHA-256 karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="90988-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="90988-119">Birden çok giriş noktalı virgülle ayrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90988-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="90988-120">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="90988-120">Options</span></span>

| <span data-ttu-id="90988-121">Seçenek</span><span class="sxs-lookup"><span data-stu-id="90988-121">Option</span></span> | <span data-ttu-id="90988-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="90988-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="90988-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="90988-123">ConfigFile</span></span> | <span data-ttu-id="90988-124">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="90988-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="90988-125">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90988-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="90988-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="90988-126">ForceEnglishOutput</span></span> | <span data-ttu-id="90988-127">NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="90988-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="90988-128">Help</span><span class="sxs-lookup"><span data-stu-id="90988-128">Help</span></span> | <span data-ttu-id="90988-129">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="90988-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="90988-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="90988-130">Verbosity</span></span> | <span data-ttu-id="90988-131">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="90988-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="90988-132">Örnekler</span><span class="sxs-lookup"><span data-stu-id="90988-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```