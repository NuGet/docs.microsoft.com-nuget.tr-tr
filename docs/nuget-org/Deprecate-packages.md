---
title: Nuget.org 'de paketleri kullanımdan kaldırma
description: Paketleri kullanımdan kaldırma işlemi ve istemcilerin bu bilgileri nasıl gösterdiği hakkında ayrıntılı açıklama
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248899"
---
# <a name="deprecating-packages"></a><span data-ttu-id="bd0cc-103">Paketleri kullanımdan kaldırma</span><span class="sxs-lookup"><span data-stu-id="bd0cc-103">Deprecating packages</span></span>

<span data-ttu-id="bd0cc-104">Artık paket bulundurmuyorsa veya paketinizin tüketicilerini başka bir pakete geçiş yapmak istiyorsanız bir paketi kullanımdan kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="bd0cc-105">Paket kullanımdan kaldırma, paketinizin aşağıda açıklandığı gibi **listelenenden** farklıdır:</span><span class="sxs-lookup"><span data-stu-id="bd0cc-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="bd0cc-106">Bir paketin **listesinin kaldırılması** , arama sonuçlarında gizlendiğinden bulma işlemini engeller.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="bd0cc-107">**Bir paketin** kullanım dışı bırakılması, paketinizin mevcut tüketicilerinin projelerine yüklenip yüklenmediğini veya bu kullanıcılara kullanılmaları halinde bulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="bd0cc-108">Ayrıca, kullanım dışı bırakma nedenini ve sizin tarafınızdan belirtilen alternatif önerilen paketi (paket yayımcısı) öğrenmelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="bd0cc-109">Bir paketin kullanımdan kaldırılması paketin listesini kaldırma.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="bd0cc-110">Bir yayımcı olarak, hem listeyi kaldırmayı hem de paketleri kullanımdan kaldırmayı tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="bd0cc-111">Kullanımdan kaldırma iş akışı</span><span class="sxs-lookup"><span data-stu-id="bd0cc-111">Deprecation workflow</span></span>
1. <span data-ttu-id="bd0cc-112">Bir paketin kullanımdan kaldırılması için **paketleri Yönet** ' e gidin ve **kullanımdan**Kaldır ' ı seçin:</span><span class="sxs-lookup"><span data-stu-id="bd0cc-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Kullanımdan Kaldır ' a git paket seçeneği](media/deprecation-select-option.png)

2. <span data-ttu-id="bd0cc-114">Kullanımdan kalkmak istediğiniz sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="bd0cc-115">Tüm sürümü kullanımdan kaldırmayı istiyorsanız **tüm sürümleri Seç** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Kullanımdan kalkmak için paket sürümlerini seçin](media/deprecation-select-version.png)

3. <span data-ttu-id="bd0cc-117">Kullanımdan kaldırma için bir neden seçin.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="bd0cc-118">Paket artık korunmuyorsa, **eski** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="bd0cc-119">Belirli bir sürüm kritik bir hata kullanıyorsa, **kritik hataları olan** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="bd0cc-120">Başka bir nedenle **diğer**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="bd0cc-121">Her zaman farklı bir önerilen paket (ve sürüm) ve Sahibe özel bir ileti belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Nedenler diğer paket önerisi ve özel ileti seçin](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="bd0cc-123">Özel ileti yalnızca nuget.org 'de gösterilir ancak istemcilerden gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="bd0cc-124">Şu anda, `dotnet.exe` ve NuGet Paket Yöneticisi gibi istemciler özel iletiyi göstermez.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="bd0cc-125">Kullanım dışı bırakılan paketler için istemci deneyimi</span><span class="sxs-lookup"><span data-stu-id="bd0cc-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="bd0cc-126">Bir paket kullanımdan kaldırıldıktan sonra, tüketicileri aşağıdaki yollarla (kullanılan istemciye bağlı olarak) bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="bd0cc-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bd0cc-127">Visual Studio</span></span> 
<span data-ttu-id="bd0cc-128">*Visual Studio 2019 sürüm 16,3 ' den başlayarak kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="bd0cc-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="bd0cc-129">Visual Studio, `Installed` kullanım dışı bırakılan paketin kullanımıyla ilgili olarak uyarır. Bu, pakete ve kullanımdan kaldırılmasıyla ilgili bilgileri (kullanım dışı olma nedeni ve varsa bunun yerine kullanılacak alternatif paket) size yol açacaktır.</span><span class="sxs-lookup"><span data-stu-id="bd0cc-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab.It will lead you to the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Paket Yöneticisi 'nin Visual Studio yüklü sekmesindeki kullanım dışı paketler](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="bd0cc-131">DotNet. exe</span><span class="sxs-lookup"><span data-stu-id="bd0cc-131">dotnet.exe</span></span>
<span data-ttu-id="bd0cc-132">*.NET SDK 3,0 ile başlayarak kullanılabilir*</span><span class="sxs-lookup"><span data-stu-id="bd0cc-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="bd0cc-133">DotNet. exe ' yi kullanırsanız, kullanım dışı bırakılan paketlerin listesini `dotnet list package --deprecated` kullanımdan kaldırma bilgileriyle birlikte çalıştırmak için çözüm veya proje klasörü üzerinde komutunu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd0cc-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
