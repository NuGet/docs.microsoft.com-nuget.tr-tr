---
title: NuGet 5,4 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,4 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: c7fb9c1e587b6603abe63581c662571abfd4506b
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384117"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="f07e2-103">NuGet 5,4 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="f07e2-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="f07e2-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="f07e2-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f07e2-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="f07e2-105">NuGet version</span></span> | <span data-ttu-id="f07e2-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f07e2-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f07e2-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f07e2-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f07e2-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="f07e2-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f07e2-109">Visual Studio 2019 sürüm 16,4</span><span class="sxs-lookup"><span data-stu-id="f07e2-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f07e2-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f07e2-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="f07e2-111"><sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi</span><span class="sxs-lookup"><span data-stu-id="f07e2-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="f07e2-112">Özet: 5,4 sürümündeki yenilikler</span><span class="sxs-lookup"><span data-stu-id="f07e2-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="f07e2-113">Daha hızlı çözüm yükleme süresi-ilk çözüm yükü sırasında NuGet kodu çalıştıran ek yük, JıT maliyetini azaltmak için kısmi Ngen aracılığıyla azaltılmıştır [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="f07e2-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="f07e2-114">Yeni yardımcı işlev-paket kimliklerinin ve sürümlerinin bir listesi verildiğinde, olası en üst düzey paketleri alın.</span><span class="sxs-lookup"><span data-stu-id="f07e2-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="f07e2-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="f07e2-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="f07e2-116">[GitHub eylemleri](https://github.com/features/actions)üzerinde NuGet. exe ' yi yükleme ve yapılandırma için yeni [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) eylem.</span><span class="sxs-lookup"><span data-stu-id="f07e2-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="f07e2-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="f07e2-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f07e2-118">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="f07e2-118">Issues fixed in this release</span></span>

<span data-ttu-id="f07e2-119">**Hata**</span><span class="sxs-lookup"><span data-stu-id="f07e2-119">**Bugs**</span></span>

* <span data-ttu-id="f07e2-120">Eklenti: Linux/Mac 'te günlüğe kaydetme süresi doğruluğu kapalı [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="f07e2-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="f07e2-121">Bir eklentiyi elden atmak bazen tüm işlemi oluşturabilir ve başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="f07e2-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="f07e2-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="f07e2-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="f07e2-123">PMUI- [#8679](https://github.com/NuGet/Home/issues/8679) izin verilen ve engellenen sürümler listesinde sürüm yinelemelerini görüntülemeyi durdur</span><span class="sxs-lookup"><span data-stu-id="f07e2-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="f07e2-124">Kilit dosyası düzgün oluşturulmamış-çerçeve sıralaması geri yüklemeyi lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645) ile etkilememelidir</span><span class="sxs-lookup"><span data-stu-id="f07e2-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="f07e2-125">SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639) <RuntimeIdentifiers> ayarlanan projelerde LockFile doğrulaması başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="f07e2-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="f07e2-126">İmzalama doğrulaması artık aynı OID altında 2 değere sahip olan zaman damgalarıyla imzaları doğru şekilde reddedecek [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="f07e2-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="f07e2-127">Lisans listesini güncelleştirme- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="f07e2-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="f07e2-128">**DCR**</span><span class="sxs-lookup"><span data-stu-id="f07e2-128">**DCRs**</span></span>

* <span data-ttu-id="f07e2-129">IFeedbackDiagnosticFileProvider- [#8535](https://github.com/NuGet/Home/issues/8535) tanılama dosyalarını ekleme</span><span class="sxs-lookup"><span data-stu-id="f07e2-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="f07e2-130">**[Bu yayında düzeltilen tüm sorunların listesi-5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="f07e2-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
