---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496058"
---
<span data-ttu-id="068dc-101">nuget.org'daki profilinizden, yeni yayınladığınız profili görmek için **Paketleri Yönet'i** seçin.</span><span class="sxs-lookup"><span data-stu-id="068dc-101">From your profile on nuget.org, select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="068dc-102">Ayrıca bir onay e-postası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="068dc-102">You also receive a confirmation email.</span></span> <span data-ttu-id="068dc-103">Paketinizin dizine eklenmenin ve başkalarının bulabileceği arama sonuçlarında görünmesinin biraz zaman alacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="068dc-103">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="068dc-104">Bu süre zarfında paket sayfanız aşağıdaki iletiyi gösterir:</span><span class="sxs-lookup"><span data-stu-id="068dc-104">During that time your package page shows the message below:</span></span>

![Bu paket henüz dizine eklenmedi.](../media/QS_Create-03-NotIndexed.png)

<span data-ttu-id="068dc-107">Hepsi bu!</span><span class="sxs-lookup"><span data-stu-id="068dc-107">And that's it!</span></span> <span data-ttu-id="068dc-108">Diğer geliştiricilerin kendi projelerinde kullanabilecekleri nuget.org için ilk NuGet paketinizi yayınladınız.</span><span class="sxs-lookup"><span data-stu-id="068dc-108">You've just published your first NuGet package to nuget.org that other developers can use in their own projects.</span></span>

<span data-ttu-id="068dc-109">Bu gözden geçirme de gerçekten yararlı olmayan bir paket oluşturduysanız (boş bir sınıf kitaplığıyla oluşturulmuş bir paket gibi), paketi arama sonuçlarından gizlemek için *listeyi boşaltmanız* gerekir:</span><span class="sxs-lookup"><span data-stu-id="068dc-109">If in this walkthrough you created a package that isn't actually useful (such as a package created with an empty class library), you should *unlist* the package to hide it from search results:</span></span>

1. <span data-ttu-id="068dc-110">nuget.org kullanıcı adınızı (sayfanın sağ üst tarafında) seçin ve **ardından Paketleri Yönet'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="068dc-110">On nuget.org, select your user name (upper right of the page), then select **Manage Packages**.</span></span>

1. <span data-ttu-id="068dc-111">**Yayımlanmış** altında listeyi boşaltmak istediğiniz paketi bulun ve sağdaki çöp kutusu simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="068dc-111">Locate the package you want to unlist under **Published** and select the trash can icon on the right:</span></span>

    ![nuget.org'da bir paket listesi için gösterilen çöp kutusu simgesi](../media/qs_create-vs-03-trash-can.png)

1. <span data-ttu-id="068dc-113">Sonraki sayfada, **arama sonuçlarında Liste (paket adı)** etiketli kutuyu temizleyin ve **Kaydet'i**seçin:</span><span class="sxs-lookup"><span data-stu-id="068dc-113">On the subsequent page, clear the box labeled **List (package-name) in search results** and select **Save**:</span></span>

    ![nuget.org'da bir paket için Liste onay kutusunu temizleme](../media/qs_create-vs-04-unlist.png)