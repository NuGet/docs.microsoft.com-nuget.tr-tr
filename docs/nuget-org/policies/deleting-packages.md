---
title: NuGet paketleri nuget.org adresinden silme
description: Nuget.org unlisting paketleri için ilkeleri; paketleri diğer ilkelerini ihlal olduğunda dışında kalıcı silme desteklenmiyor.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427511"
---
# <a name="deleting-packages"></a><span data-ttu-id="4e81c-103">Paketleri silme</span><span class="sxs-lookup"><span data-stu-id="4e81c-103">Deleting packages</span></span>

<span data-ttu-id="4e81c-104">nuget.org paketleri kalıcı olarak silinmesini desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4e81c-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="4e81c-105">Bunun yapılması özellikle paket geri yükleme içeren derleme iş akışlarıyla paket kullanılabilirliğini bağlı olarak her proje bölün.</span><span class="sxs-lookup"><span data-stu-id="4e81c-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="4e81c-106">nuget.org destekliyor mu *unlisting* bir paketi paket Yönetim sayfasında web sitesinde yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="4e81c-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="4e81c-107">Listelenmemiş paketleri nuget.org üzerinde veya Visual Studio kullanıcı arabiriminde görünmez ve arama sonuçlarında görünmez.</span><span class="sxs-lookup"><span data-stu-id="4e81c-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="4e81c-108">Listelenmemiş paketleri, ancak yine de indirilebilen ve paket geri yükleme destekleyen bir tam sürüm numarası kullanarak yüklü.</span><span class="sxs-lookup"><span data-stu-id="4e81c-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="4e81c-109">Ayrıca, listede bulunmayan paketler hala aşağıdaki belirli senaryolarda bulunan:</span><span class="sxs-lookup"><span data-stu-id="4e81c-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="4e81c-110">Kayan sürümleri kullanılarak geri yükleme paketini (örneğin, `1.0.0-*`), sürüm veya bağımlılık kısıtlamalarıyla eşleşen en son kullanılabilir paket listelenmemiş bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="4e81c-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="4e81c-111">Paket Kataloğu aracılığıyla çoğaltma (Kataloğu ayrıca listelenmemiş paketleri içerdiği için).</span><span class="sxs-lookup"><span data-stu-id="4e81c-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="4e81c-112">Özel Durumlar</span><span class="sxs-lookup"><span data-stu-id="4e81c-112">Exceptions</span></span>

<span data-ttu-id="4e81c-113">Telif hakkı ihlali ve potansiyel olarak zararlı içeriği gibi olağanüstü durumlarda, paketleri el ile NuGet ekibi tarafından silinebilir.</span><span class="sxs-lookup"><span data-stu-id="4e81c-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="4e81c-114">NuGet.org Paket Ayrıntıları sayfasındaki "Uygunsuz" düğmesini kullanarak bir paket bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e81c-114">You can report a package using the "Report abuse" button on the NuGet.org package details page.</span></span> <span data-ttu-id="4e81c-115">NuGet.org Paket Ayrıntıları sayfasındaki "desteğe başvurun" düğmesini kullanarak NuGet desteği ulaşmaya NuGet.org hesabınızda oturum açın paket sahibinden varsa.</span><span class="sxs-lookup"><span data-stu-id="4e81c-115">If you are the package owner, login to your NuGet.org account to reach NuGet support using the "Contact support" button on the NuGet.org package details page.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="4e81c-116">Yasaklanmış kullanımı</span><span class="sxs-lookup"><span data-stu-id="4e81c-116">Prohibited use</span></span>

<span data-ttu-id="4e81c-117">Aşağıdaki ölçütleri karşılayan paketleri genel NuGet galerisinde izin verilmez ve tartışma hemen kaldırılacak.</span><span class="sxs-lookup"><span data-stu-id="4e81c-117">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="4e81c-118">Sahipleri olacaktır, ancak paket, kaldırılmasını bildirim.</span><span class="sxs-lookup"><span data-stu-id="4e81c-118">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="4e81c-119">Kötü amaçlı yazılım, reklam yazılımlarından ve her türlü bir casus yazılım içerir.</span><span class="sxs-lookup"><span data-stu-id="4e81c-119">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="4e81c-120">Geliştirici iş istasyonu veya kuruluş zarar vermek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4e81c-120">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="4e81c-121">Telif Hakkı herhangi bir mülkiyet veya lisans ihlal ediyor.</span><span class="sxs-lookup"><span data-stu-id="4e81c-121">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="4e81c-122">Geçersiz içerik içerir.</span><span class="sxs-lookup"><span data-stu-id="4e81c-122">Contains illegal content.</span></span>
- <span data-ttu-id="4e81c-123">Kullanılmakta olan sıfır üretken içerik paketleri de dahil olmak üzere paket tanımlayıcılarla ilgili squat için.</span><span class="sxs-lookup"><span data-stu-id="4e81c-123">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="4e81c-124">Kod paketleri içermelidir veya sahipleri tanımlayıcısını oluşturmak için bir ürün olan birisi bırakma gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e81c-124">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="4e81c-125">Açıkça yapmak için tasarlanmış bir şey yapın galerisini çıkarmaya çalışın.</span><span class="sxs-lookup"><span data-stu-id="4e81c-125">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="4e81c-126">İhlal bu öğelerden herhangi birinin bir paketi bulursanız, tıklayın **uygunsuz** Paket Ayrıntıları sayfasına bağlantı ve bir rapor gönderin.</span><span class="sxs-lookup"><span data-stu-id="4e81c-126">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="4e81c-127">NuGet takım ve .NET Foundation herhangi bir zamanda bu ölçütlerini değiştirmek için sağ ayırdığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4e81c-127">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
