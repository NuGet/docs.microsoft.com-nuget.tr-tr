---
title: NuGet istemci SDK'sı
description: Geliştirilmekte olan ve henüz belgelenmiş API'si, ancak örnekler Dave Glick'ın blogunda kullanılabilir.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 97ed3ec7d41d2847c0521af69373a1871eb585dd
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324688"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="7d5f4-103">NuGet istemci SDK'sı</span><span class="sxs-lookup"><span data-stu-id="7d5f4-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="7d5f4-104">İle karıştırılmamalıdır [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="7d5f4-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="7d5f4-105">*NuGet istemci SDK'sı* .NET kitaplıkları etrafında ortalanmış bir grup başvurduğu [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), ve [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="7d5f4-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="7d5f4-106">Bu paketler önceki değiştirin [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="7d5f4-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="7d5f4-107">Size en kısa sürede belgelemeye kararlı bir yüzey alanı olması çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7d5f4-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="7d5f4-108">Kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="7d5f4-108">Source code</span></span>

<span data-ttu-id="7d5f4-109">Kaynak kodu Github'da projede yayımlanan [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span><span class="sxs-lookup"><span data-stu-id="7d5f4-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="7d5f4-110">Üçüncü taraf belgeleri</span><span class="sxs-lookup"><span data-stu-id="7d5f4-110">Third-party documentation</span></span>

<span data-ttu-id="7d5f4-111">Örnekler ve belgeler için bazı API 2016 yayımlanan Dave Glick tarafından aşağıdaki blog dizisini bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d5f4-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="7d5f4-112">1. Bölüm NuGet v3 kitaplıkları keşfetme: Giriş ve kavramları</span><span class="sxs-lookup"><span data-stu-id="7d5f4-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="7d5f4-113">2. Bölüm NuGet v3 kitaplıkları keşfetme: Paketlerini arama</span><span class="sxs-lookup"><span data-stu-id="7d5f4-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="7d5f4-114">Bölüm 3 NuGet v3 kitaplıkları keşfetme: Paketleri yükleme</span><span class="sxs-lookup"><span data-stu-id="7d5f4-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="7d5f4-115">Bu blog gönderileri, kısa süre sonra yazılmış **3.4.3** istemci SDK paketleri kullanıma sunulan NuGet sürümü.</span><span class="sxs-lookup"><span data-stu-id="7d5f4-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="7d5f4-116">Paketlerin daha yeni sürümlerini blog gönderilerini bilgileri ile uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="7d5f4-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="7d5f4-117">Martin Björkström burada verilen NuGet paketlerini yüklemek için NuGet istemci SDK'sını kullanarak farklı bir yaklaşım tanıtan bir izleme blog gönderisi Dave Glick'ın blog serisine yaptınız:</span><span class="sxs-lookup"><span data-stu-id="7d5f4-117">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="7d5f4-118">NuGet v3 kitaplıkları hakkında yeniden değerlendirme</span><span class="sxs-lookup"><span data-stu-id="7d5f4-118">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
