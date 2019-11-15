---
title: Nuget.org 'de paketleri kullanımdan kaldırma
description: Paketleri kullanımdan kaldırma işlemi ve istemcilerin bu bilgileri nasıl gösterdiği hakkında ayrıntılı açıklama
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096879"
---
# <a name="deprecating-packages"></a><span data-ttu-id="239d6-103">Paketleri kullanımdan kaldırma</span><span class="sxs-lookup"><span data-stu-id="239d6-103">Deprecating packages</span></span>

<span data-ttu-id="239d6-104">Artık paket bulundurmuyorsa veya paketinizin tüketicilerini başka bir pakete geçiş yapmak istiyorsanız bir paketi kullanımdan kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="239d6-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="239d6-105">Paket kullanımdan kaldırma, paketinizin aşağıda açıklandığı gibi **listelenenden** farklıdır:</span><span class="sxs-lookup"><span data-stu-id="239d6-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="239d6-106">Bir paketin **listesinin kaldırılması** , arama sonuçlarında gizlendiğinden bulma işlemini engeller.</span><span class="sxs-lookup"><span data-stu-id="239d6-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="239d6-107">**Bir paketin** kullanım dışı bırakılması, paketinizin mevcut tüketicilerinin projelerine yüklenip yüklenmediğini veya bu kullanıcılara kullanılmaları halinde bulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="239d6-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="239d6-108">Ayrıca, kullanım dışı bırakma nedenini ve sizin tarafınızdan belirtilen alternatif önerilen paketi (paket yayımcısı) öğrenmelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="239d6-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="239d6-109">Bir paketin kullanımdan kaldırılması paketin listesini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="239d6-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="239d6-110">Bir yayımcı olarak, hem listeyi kaldırmayı hem de paketleri kullanımdan kaldırmayı tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="239d6-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="239d6-111">Kullanımdan kaldırma iş akışı</span><span class="sxs-lookup"><span data-stu-id="239d6-111">Deprecation workflow</span></span>
1. <span data-ttu-id="239d6-112">Bir paketin kullanımdan kaldırılması için **paketleri Yönet** ' e gidin ve **kullanımdan**Kaldır ' ı seçin:</span><span class="sxs-lookup"><span data-stu-id="239d6-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Kullanımdan Kaldır ' a git paket seçeneği](media/deprecation-select-option.png)

2. <span data-ttu-id="239d6-114">Kullanımdan kalkmak istediğiniz sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="239d6-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="239d6-115">Tüm sürümü kullanımdan kaldırmayı istiyorsanız **tüm sürümleri Seç** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="239d6-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Kullanımdan kalkmak için paket sürümlerini seçin](media/deprecation-select-version.png)

3. <span data-ttu-id="239d6-117">Kullanımdan kaldırma için bir neden seçin.</span><span class="sxs-lookup"><span data-stu-id="239d6-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="239d6-118">Paket artık korunmuyorsa, **eski** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="239d6-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="239d6-119">Belirli bir sürüm kritik bir hata kullanıyorsa, **kritik hataları olan** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="239d6-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="239d6-120">Başka bir nedenle **diğer**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="239d6-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="239d6-121">Her zaman farklı bir önerilen paket (ve sürüm) ve Sahibe özel bir ileti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="239d6-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Nedenler diğer paket önerisi ve özel ileti seçin](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="239d6-123">Özel ileti yalnızca nuget.org 'de gösterilir ancak istemcilerden gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="239d6-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="239d6-124">Şu anda, `dotnet.exe` ve NuGet Paket Yöneticisi gibi istemciler özel iletiyi göstermez.</span><span class="sxs-lookup"><span data-stu-id="239d6-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="239d6-125">Kullanım dışı bırakılan paketler için istemci deneyimi</span><span class="sxs-lookup"><span data-stu-id="239d6-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="239d6-126">Bir paket kullanımdan kaldırıldıktan sonra, tüketicileri aşağıdaki yollarla (kullanılan istemciye bağlı olarak) bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="239d6-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="239d6-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="239d6-127">Visual Studio</span></span> 
<span data-ttu-id="239d6-128">*Visual Studio 2019 sürüm 16,3 ' den başlayarak kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="239d6-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="239d6-129">Visual Studio, `Installed` sekmesindeki kullanım dışı bırakılan paketin kullanımı hakkında uyarır. Paket ve kullanımdan kaldırma bilgileri (kullanım dışı olma nedeni ve varsa bunun yerine kullanılacak alternatif paket) için bir uyarı gösterir.</span><span class="sxs-lookup"><span data-stu-id="239d6-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Paket Yöneticisi 'nin Visual Studio yüklü sekmesindeki kullanım dışı paketler](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="239d6-131">DotNet. exe</span><span class="sxs-lookup"><span data-stu-id="239d6-131">dotnet.exe</span></span>
<span data-ttu-id="239d6-132">*.NET SDK 3,0 ile başlayarak kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="239d6-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="239d6-133">DotNet. exe ' yi kullanırsanız, kullanım dışı bırakılan paketlerin listesini kullanımdan kaldırma bilgileriyle birlikte almak için çözüm veya proje klasörü üzerinde `dotnet list package --deprecated` komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="239d6-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
