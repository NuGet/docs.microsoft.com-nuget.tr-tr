---
title: nuget.org'da ambalajları küçümseme
description: Paketleri küçümseme işlemi ve istemcilerin bu bilgileri nasıl gösterdiği hakkında ayrıntılı açıklama
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096879"
---
# <a name="deprecating-packages"></a><span data-ttu-id="26ada-103">Amortisman paketleri</span><span class="sxs-lookup"><span data-stu-id="26ada-103">Deprecating packages</span></span>

<span data-ttu-id="26ada-104">Bir paketi artık muhafaza etmezseniz veya paketinizin tüketicilerini başka bir pakete geçmeye teşvik etmek istiyorsanız, paketi amortismana dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26ada-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="26ada-105">Paket amortismanı, aşağıda açıklandığı gibi paketinizin **listeyi bırakmadan** farklıdır:</span><span class="sxs-lookup"><span data-stu-id="26ada-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="26ada-106">Bir paketin **listelenmesi,** arama sonuçlarında gizli olduğundan bulunmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="26ada-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="26ada-107">Bir paketin **amortismana sokulmaması,** paketinmevcut tüketicilerinin paketi yüklü veya projelerinde kullanıp kullanmadıklarını öğrenmelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="26ada-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="26ada-108">Ayrıca, amortisman nedenini ve sizin (paket yayımcısı) tarafından belirtildiği gibi alternatif bir önerilen paket ilerler.</span><span class="sxs-lookup"><span data-stu-id="26ada-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="26ada-109">Bir paketi küçümsemek paketin listesini geri almaz.</span><span class="sxs-lookup"><span data-stu-id="26ada-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="26ada-110">Yayımcı olarak, paketleri hem listedışı bırakmayı hem de amortismanı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26ada-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="26ada-111">Amortisman iş akışı</span><span class="sxs-lookup"><span data-stu-id="26ada-111">Deprecation workflow</span></span>
1. <span data-ttu-id="26ada-112">Bir paketi amortismana katmayı yönetmek için **paketleri Yönet'e** gidin ve **Amortisman'ı**seçin:</span><span class="sxs-lookup"><span data-stu-id="26ada-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Paket seçeneğini amortismana gitme](media/deprecation-select-option.png)

2. <span data-ttu-id="26ada-114">Amortismana uymak istediğiniz sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="26ada-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="26ada-115">Tüm sürümü amortismana kayırmak istiyorsanız, **tüm sürümleri seç** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="26ada-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Amortismana uymak için paket sürümlerini seçin](media/deprecation-select-version.png)

3. <span data-ttu-id="26ada-117">Amortisman için bir neden seçin.</span><span class="sxs-lookup"><span data-stu-id="26ada-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="26ada-118">Paket artık korunmazsa, **Eski** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="26ada-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="26ada-119">Belirli sürümde kritik bir hata varsa, **kritik hataları seçeneği ni** seçin.</span><span class="sxs-lookup"><span data-stu-id="26ada-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="26ada-120">Başka bir nedenle **Diğer'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="26ada-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="26ada-121">Her zaman alternatif bir önerilen paket (ve sürüm) ve sahiplerine özel bir ileti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26ada-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Alternatif paket önerisi ve özel ileti nedenleri seçin](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="26ada-123">Özel ileti yalnızca nuget.org gösterilir, ancak istemcilerden gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="26ada-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="26ada-124">Şu anda, `dotnet.exe` nuget paket yöneticisi gibi istemciler özel iletiyi göstermez.</span><span class="sxs-lookup"><span data-stu-id="26ada-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="26ada-125">Amortismana uyan paketler için müşteri deneyimi</span><span class="sxs-lookup"><span data-stu-id="26ada-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="26ada-126">Bir paket amortismana uğradıktan sonra, tüketicilere bu konuda aşağıdaki yollarla bilgi verilir (kullanılan müşteriye bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="26ada-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="26ada-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="26ada-127">Visual Studio</span></span> 
<span data-ttu-id="26ada-128">*Visual Studio 2019 sürümü16.3'ten itibaren kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="26ada-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="26ada-129">Visual `Installed` Studio, sekmede amortismana lı bir paketin kullanımı konusunda uyarır. Paket ve amortisman bilgileri için bir uyarı gösterir (amortismana neden ve varsa kullanılacak alternatif paket dahil).</span><span class="sxs-lookup"><span data-stu-id="26ada-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Visual Studio'da amortismana küçümşen paketler paket yöneticisisekmesine yüklenmiş](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="26ada-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="26ada-131">dotnet.exe</span></span>
<span data-ttu-id="26ada-132">*.NET SDK 3.0 ile başlayan fiyatlarla*</span><span class="sxs-lookup"><span data-stu-id="26ada-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="26ada-133">dotnet.exe kullanıyorsanız, amortisman bilgileriyle `dotnet list package --deprecated` birlikte amortismana alınan paketlerin listesini almak için çözüm veya proje klasöründeki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="26ada-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
