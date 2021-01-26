---
title: NuGet 2,2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,2 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780440"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="ec503-103">NuGet 2,2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ec503-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="ec503-104">[NuGet 2,1 sürüm notları](../release-notes/nuget-2.1.md)  |  [NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="ec503-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="ec503-105">NuGet 2,2, 12 Aralık 2012 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec503-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="ec503-106">Visual Studio hızlı başlatma</span><span class="sxs-lookup"><span data-stu-id="ec503-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="ec503-107">Visual Studio 2012 ' de eklenen yeni özelliklerden biri [Hızlı başlatma iletişim kutusu](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)idi.</span><span class="sxs-lookup"><span data-stu-id="ec503-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="ec503-108">NuGet 2,2, bu iletişim kutusunu genişleterek Paket Yöneticisi iletişim kutusunu hızlı başlatmaya girilen arama koşullarına göre başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="ec503-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="ec503-109">Örneğin, hızlı başlatma ' ya ' jQuery ' girildiğinde, ' jQuery ' ile eşleşen NuGet paketlerini aramak için sonuçlara bir seçenek de eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ec503-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio hızlı başlatma 'da NuGet](./media/quick-launch.png)

<span data-ttu-id="ec503-111">Bu seçeneğin belirlenmesi, ' jQuery ' terimi için standart NuGet Paket Yöneticisi arama deneyimini başlatacaktır.</span><span class="sxs-lookup"><span data-stu-id="ec503-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Önceden doldurulmuş NuGet Paket Yöneticisi Iletişim kutusu](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="ec503-113">Paket Içeriği için tüm klasörü belirt</span><span class="sxs-lookup"><span data-stu-id="ec503-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="ec503-114">NuGet 2,2, `<file>` `.nuspec` Bu klasörün tüm içeriğini dahil etmek için dosyanın öğesinde bir klasörün tamamını belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec503-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="ec503-115">Örneğin, aşağıdaki, paket bir projeye yüklendiğinde paketin komut dosyaları klasöründeki tüm betiklerin contents\scripts klasörüne eklenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="ec503-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="ec503-116">**Güncelleştirme 6/24/16: paket yüklenirken "içerik" klasöründeki boş klasörler yok sayılır.**</span><span class="sxs-lookup"><span data-stu-id="ec503-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="ec503-117">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="ec503-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="ec503-118">Paket Yöneticisi konsolu kullanılırken F # projeleri için paket yükleme başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="ec503-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="ec503-119">Paket Yöneticisi konsolunu kullanarak bir bir NuGet paketini F # projesine yüklemeye çalışırken bir InvalidOperationException atılır.</span><span class="sxs-lookup"><span data-stu-id="ec503-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="ec503-120">Sorunu çözmek için F # ekibiyle etkin bir şekilde çalışıyoruz, ancak bu arada geçici çözüm, NuGet paketlerini konsol yerine NuGet 'in Paket Yöneticisi iletişim kutusu aracılığıyla F # projelerine yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="ec503-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="ec503-121">[CodePlex üzerinde daha fazla bilgi bulabilirsiniz](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="ec503-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="ec503-122">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="ec503-122">Bug Fixes</span></span>
<span data-ttu-id="ec503-123">NuGet 2,2 birçok hata düzeltmesi içerir.</span><span class="sxs-lookup"><span data-stu-id="ec503-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="ec503-124">NuGet 2,2 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="ec503-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
