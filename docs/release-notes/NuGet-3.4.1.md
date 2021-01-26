---
title: NuGet 3.4.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1e234becd2c92ae64fa0f1ac95b358e9a2fb3207
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776477"
---
# <a name="nuget-341-release-notes"></a><span data-ttu-id="53502-103">NuGet 3.4.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="53502-103">NuGet 3.4.1 Release Notes</span></span>

<span data-ttu-id="53502-104">[NuGet 3,4 sürüm notları](../release-notes/nuget-3.4.md)  |  [NuGet 3.4.2 sürüm notları](../release-notes/nuget-3.4.2.md)</span><span class="sxs-lookup"><span data-stu-id="53502-104">[NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md) | [NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md)</span></span>

<span data-ttu-id="53502-105">NuGet 3.4.1, 3,4 sürümünde tanımlanan birkaç sorunu gidermek için Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümü ile aynı anda 30 Mart 2016 ' den yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="53502-105">NuGet 3.4.1 was released March 30, 2016 at the same time as the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release to address several issues that were identified in the 3.4 release.</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="53502-106">Güncelleştirmeler ve geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="53502-106">Updates and Improvements</span></span>

* <span data-ttu-id="53502-107">Visual Studio kullanıcı arabiriminden, en az Visual Studio yüklemesi ile paketleri taramayı önleyen bir sorun düzeltildi</span><span class="sxs-lookup"><span data-stu-id="53502-107">Corrected an issue that prevented browsing packages from the Visual Studio UI with a minimum Visual Studio install</span></span>
* <span data-ttu-id="53502-108">Visual Studio bulma ile ilgili bir sorun düzeltildi `lucene.net.dll`</span><span class="sxs-lookup"><span data-stu-id="53502-108">Corrected an issue with Visual Studio locating `lucene.net.dll`</span></span>
* <span data-ttu-id="53502-109">Bir NuGet uzantısının yüklenmesi veya güncelleştirilmesi sonrasında tüm kaynaklar varsayılan depo kaynağı olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="53502-109">All sources should not be the default repository source after a NuGet extension install or update.</span></span>  <span data-ttu-id="53502-110">Bu özelliği yapılandırma ayarlarından kabul edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53502-110">You can opt-in to this feature from the configuration settings.</span></span>

<span data-ttu-id="53502-111">GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="53502-111">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>