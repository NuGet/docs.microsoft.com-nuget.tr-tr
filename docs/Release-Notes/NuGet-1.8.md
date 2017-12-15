---
title: "NuGet 1.8 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e694ee1a-fe4c-4397-8d0a-7336be4dfebe
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.8 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 1.8 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 875cb752fed102c24da255a336d3f16729ca082c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="09c4e-104">NuGet 1.8 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="09c4e-104">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="09c4e-105">[NuGet 1.7 Sürüm Notları](../release-notes/nuget-1.7.md) | [NuGet 2.0 sürüm notları](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="09c4e-105">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="09c4e-106">NuGet 1.8 23 Mayıs 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="09c4e-106">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="09c4e-107">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="09c4e-107">Known Installation Issue</span></span>
<span data-ttu-id="09c4e-108">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c4e-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="09c4e-109">Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="09c4e-110">Bkz: [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) daha fazla bilgi için veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="09c4e-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="09c4e-111">Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="09c4e-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="09c4e-112">Windows XP ile NuGet 1.8 uyumsuz yayımlanan düzeltme</span><span class="sxs-lookup"><span data-stu-id="09c4e-112">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="09c4e-113">Kısa süre içinde NuGet 1.8 yayımlandıktan sonra bir şifreleme değişiklik 1.8 kullanıcılar Windows XP ihlal öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="09c4e-113">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="09c4e-114">Bu sorunu giderir bir düzeltme beri yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="09c4e-114">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="09c4e-115">NuGet Visual Studio uzantısı Galerisine güncelleştirerek bu düzeltme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="09c4e-115">By updating NuGet through the Visual Studio Extension Gallery, you will receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="09c4e-116">Özellikler</span><span class="sxs-lookup"><span data-stu-id="09c4e-116">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="09c4e-117">Yerelleştirilmiş kaynaklar için uydu paketleri</span><span class="sxs-lookup"><span data-stu-id="09c4e-117">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="09c4e-118">NuGet 1.8 artık yerelleştirilmiş kaynaklar, .NET Framework uydu derleme yeteneklerini benzer için ayrı paketler oluşturma olanağı destekler.</span><span class="sxs-lookup"><span data-stu-id="09c4e-118">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="09c4e-119">Bir uydu paketi, başka bir NuGet paketi birkaç kuralları eklenmesi ile aynı şekilde oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="09c4e-119">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="09c4e-120">Uydu paket kimliği ve dosya adı standart biriyle eşleşen bir sonek içermelidir [kültür .NET Framework tarafından kullanılan dizeleri](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span><span class="sxs-lookup"><span data-stu-id="09c4e-120">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="09c4e-121">İçinde `.nuspec` dosya, uydu paket tanımlamanız gerekir language öğesi Kimliğinde kullanılan aynı kültür dizesiyle</span><span class="sxs-lookup"><span data-stu-id="09c4e-121">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="09c4e-122">Uydu paket bağımlılık olarak tanımlamanız gerekir, `.nuspec` paket dil soneki eksi aynı Kimliğe sahip yalnızca kendi çekirdek paket dosyasına.</span><span class="sxs-lookup"><span data-stu-id="09c4e-122">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="09c4e-123">Çekirdek paket yüklemenin başarılı deposunda kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-123">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="09c4e-124">Yerelleştirilmiş kaynaklar ile bir paketi yüklemek için bir uygulama geliştiricisi açıkça depodan yerelleştirilmiş paket seçer.</span><span class="sxs-lookup"><span data-stu-id="09c4e-124">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="09c4e-125">Şu anda NuGet galerisinde özel işleme uydu paketlerden herhangi bir tür sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="09c4e-125">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![Yerelleştirilmiş pacakges ile Paket Yöneticisi iletişim kutusu](./media/dlg-w-loc-packs.png)

<span data-ttu-id="09c4e-127">Çekirdek paket için bir bağımlılık uydu paketini listeler için uydu ve çekirdek paketleri NuGet paketleri klasörüne çekilen ve yüklü.</span><span class="sxs-lookup"><span data-stu-id="09c4e-127">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![Yerelleştirilmiş paketleriyle paketler klasörü](./media/fldr-loc-packs.png)

<span data-ttu-id="09c4e-129">Ayrıca, uydu paketi yüklerken, çalışırken NuGet da kültür dize adlandırma kuralı tanır ve böylece .NET Framework tarafından çekilebilir sonra yerelleştirilmiş kaynak assembly çekirdek paket içinde doğru alt klasörü içine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="09c4e-129">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![Çekirdek paket klasörüne kopyalanan kaynak klasör ile](./media/fldr-copied-loc.png)

<span data-ttu-id="09c4e-131">Uydu paketlerle not etmek için var olan bir hata olduğundan NuGet yerelleştirilmiş kaynaklar kopyalamaz `bin` Web sitesi projeleri için klasör.</span><span class="sxs-lookup"><span data-stu-id="09c4e-131">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="09c4e-132">Bu sorunu NuGet sonraki sürümde düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-132">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="09c4e-133">Oluşturma ve uydu paketlerini kullanma gösteren tam bir örnek için bkz: [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span><span class="sxs-lookup"><span data-stu-id="09c4e-133">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="09c4e-134">Paket geri yükleme onayı</span><span class="sxs-lookup"><span data-stu-id="09c4e-134">Package Restore Consent</span></span>
<span data-ttu-id="09c4e-135">NuGet 1.8 içinde kullanıcı gizliliğini korumak için paket geri yüklemesi üzerinde önemli bir kısıtlama desteklemek için geçişteki düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-135">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="09c4e-136">Bu kısıtlama, projeler ve paket geri yükleme için açıkça onaylaması için paket geri yüklemesi kullanarak çözümler oluşturan geliştiriciler yapılandırılmış paket kaynaklardan paketlerini indirmek için çevrimiçi olma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-136">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="09c4e-137">Bu onay vermeniz 2 yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="09c4e-137">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="09c4e-138">İlk aşağıda gösterildiği gibi Paket Yöneticisi yapılandırma iletişim bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-138">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="09c4e-139">Bu yöntem, öncelikle Geliştirici makineler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="09c4e-139">This method is primarily intended for developer machines.</span></span>

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/pr-consent-configdlg.png)

<span data-ttu-id="09c4e-141">İkinci ortam değişkeni "EnableNuGetPackageRestore" "true" değerini ayarlamak için yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-141">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="09c4e-142">Bu yöntem CI veya yapı sunucuları gibi katılımsız makineler yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-142">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="09c4e-143">Şimdi, yukarıda belirtildiği gibi biz yalnızca bu özellik için geçişteki NuGet 1.8 yerleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="09c4e-143">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="09c4e-144">Pratikte, bu özelliği etkinleştirmek için mantığı tümünün ekledik olsa da, bunu şu anda bu sürümde zorlanmaz olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-144">Practically, this means that while we’ve added all of the logic to enable the feature, it is not currently enforced in this version.</span></span> <span data-ttu-id="09c4e-145">Etkin olacaktır, ancak, sonraki ortamınızı uygun şekilde yapılandırabilir ve biz başlattığınızda, bu nedenle etkilenmiş değil, farkında mümkün olan en kısa sürede yaptığınız istedik şekilde NuGet sürümü zorunlu izin kısıtlaması.</span><span class="sxs-lookup"><span data-stu-id="09c4e-145">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="09c4e-146">Daha fazla ayrıntı için lütfen bkz. [ekip Web günlüğü postası](http://blog.nuget.org/20120518/package-restore-and-consent.html) bu özelliği.</span><span class="sxs-lookup"><span data-stu-id="09c4e-146">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="09c4e-147">nuget.exe performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="09c4e-147">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="09c4e-148">İndirmek ve paralel olarak paketleri yüklemek için yükleme komut değiştirerek, NuGet 1.8 önemli ölçüde performans artışı nuget.exe – ve uzantı paket geri yüklemesi tarafından getirir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-148">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="09c4e-149">Yüksek düzey sınama 6 paket bir projeye yüklemeye yönelik performans NuGet 1.8 yaklaşık %35 tarafından artırır gösterir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-149">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="09c4e-150">25 paketlerin sayısını artırmak hakkında 60 oranında bir performans kazancı gösterir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-150">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="09c4e-151">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="09c4e-151">Bug Fixes</span></span>
<span data-ttu-id="09c4e-152">Paket geri yükleme izniniz ve Windows 8 Express tümleştirme özellikle ilgili olarak NuGet 1.8 Paket Yöneticisi konsolunda ve paket geri yükleme iş akışı, bir Vurgu ile çeşitli hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="09c4e-152">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="09c4e-153">İş tam listesi için öğeleri NuGet 1.8 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="09c4e-153">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
