---
title: NuGet CLı doğrulama komutu
description: nuget.exe Verify komutu için başvuru
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238146"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="6fd58-103">Verify komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="6fd58-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="6fd58-104">**Uygulama hedefi:** paket tüketimi &bullet; **Desteklenen sürümler:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="6fd58-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="6fd58-105">Bir paketi doğrular.</span><span class="sxs-lookup"><span data-stu-id="6fd58-105">Verifies a package.</span></span>

<span data-ttu-id="6fd58-106">İmzalanmış paketlerin doğrulanması, Mono altında henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="6fd58-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="6fd58-107">Kullanım</span><span class="sxs-lookup"><span data-stu-id="6fd58-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="6fd58-108">Burada `<package(s)>` bir veya daha fazla `.nupkg` Dosya bulunur.</span><span class="sxs-lookup"><span data-stu-id="6fd58-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="6fd58-109">NuGet Verify-tümü</span><span class="sxs-lookup"><span data-stu-id="6fd58-109">nuget verify -All</span></span>

<span data-ttu-id="6fd58-110">Tüm doğrulamaları, paketler üzerinde gerçekleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6fd58-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="6fd58-111">NuGet doğrulama-Imzalar</span><span class="sxs-lookup"><span data-stu-id="6fd58-111">nuget verify -Signatures</span></span>

<span data-ttu-id="6fd58-112">Paket imzası doğrulamasının gerçekleştirilmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6fd58-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="6fd58-113">"Verify-Imzalara" seçenekleri</span><span class="sxs-lookup"><span data-stu-id="6fd58-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="6fd58-114">İmzalı paketlerin imzalı olması gereken sertifikaların bir veya daha fazla SHA-256 sertifikası parmak izlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6fd58-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="6fd58-115">Bir sertifika SHA-256 parmak izi, sertifikanın SHA-256 karmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6fd58-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="6fd58-116">Birden çok giriş noktalı virgülle ayrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6fd58-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="6fd58-117">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="6fd58-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="6fd58-118">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="6fd58-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6fd58-119">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6fd58-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="6fd58-120">nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="6fd58-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="6fd58-121">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6fd58-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="6fd58-122">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="6fd58-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="6fd58-123">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="6fd58-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="6fd58-124">Örnekler</span><span class="sxs-lookup"><span data-stu-id="6fd58-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```