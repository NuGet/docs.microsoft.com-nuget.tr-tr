---
title: "NuGet istemci Araçları'nı yükleme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "İstemci araçlarında, komut satırı arabirimi (CLI) ve Paket Yöneticisi Visual Studio için Yükleme Kılavuzu."
keywords: "nuget.exe CLI, NuGet istemcisi araçları, NuGet Paket Yöneticisi, NuGet Paket Yöneticisi konsolu, NuGet Visual Studio, NuGet beta kanal"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="1f99f-104">NuGet istemci araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="1f99f-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="1f99f-105">**Bir paketi yüklemek istiyorsunuz? Bkz: [hızlı başlangıç - kullanım bir paketi](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="1f99f-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="1f99f-106">Yapı, yayımlama ve NuGet paketleri kullanmasına yardımcı olmak için kullanılabilen iki birincil araçlar vardır:</span><span class="sxs-lookup"><span data-stu-id="1f99f-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="1f99f-107">[ **NuGet CLI** ](#nuget-cli) komut satırı yardımcı programıdır Windows için tüm NuGet yetenekleri sağlayan; Mac OSX ve Linux Mono kullanarak veya .NET Core CLI aracılığıyla da çalıştırılabilir (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="1f99f-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="1f99f-108">[ **Visual Studio'da NuGet Paket Yöneticisi** ](#nuget-package-manager-in-visual-studio) (yalnızca Windows) yönetme ve paketleri doğrudan Visual içinde belirli NuGet komutlarını üzerinden kullanabileceğiniz bir PowerShell konsolunda içeren bir GUI araçtır Studio.</span><span class="sxs-lookup"><span data-stu-id="1f99f-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="1f99f-109">Paket Yöneticisi kullanıcı Arabirimi ve konsol Visual Studio ile (Windows) 2012 ve üzeri dahil ve önceki sürümleri için el ile yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="1f99f-110">Mac için Visual Studio ile doğrudan NuGet özellikleri yerleşiktir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="1f99f-111">Bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough) kılavuz.</span><span class="sxs-lookup"><span data-stu-id="1f99f-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="1f99f-112">Visual Studio Code günümüzde hiçbir yerleşik NuGet destek yok.</span><span class="sxs-lookup"><span data-stu-id="1f99f-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="1f99f-113">NuGet CLI kullanın veya [dotnet CLI](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="1f99f-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="1f99f-114">NuGet CLI ve Paket Yöneticisi aşağıdaki işlemleri destekler:</span><span class="sxs-lookup"><span data-stu-id="1f99f-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="1f99f-115">Arama paketleri</span><span class="sxs-lookup"><span data-stu-id="1f99f-115">Search packages</span></span>
- <span data-ttu-id="1f99f-116">Paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="1f99f-116">Install packages</span></span>
- <span data-ttu-id="1f99f-117">Güncelleştirme paketleri</span><span class="sxs-lookup"><span data-stu-id="1f99f-117">Update packages</span></span>
- <span data-ttu-id="1f99f-118">Paketlerini kaldırma</span><span class="sxs-lookup"><span data-stu-id="1f99f-118">Uninstall packages</span></span>
- <span data-ttu-id="1f99f-119">Geri yükleme paketleri (yalnızca Paket Yöneticisi'nde kullanıcı Arabirimi)</span><span class="sxs-lookup"><span data-stu-id="1f99f-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="1f99f-120">NuGet kaynaklarını yönet</span><span class="sxs-lookup"><span data-stu-id="1f99f-120">Manage NuGet sources</span></span>

<span data-ttu-id="1f99f-121">Aşağıdaki özellikleri yalnızca NuGet CLI içinde desteklenir:</span><span class="sxs-lookup"><span data-stu-id="1f99f-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="1f99f-122">(Nuget.org veya özel akış) paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="1f99f-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="1f99f-123">Paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f99f-123">Create packages</span></span> 
- <span data-ttu-id="1f99f-124">Paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="1f99f-124">Publish packages</span></span>
- <span data-ttu-id="1f99f-125">Nuget.Config yönetme</span><span class="sxs-lookup"><span data-stu-id="1f99f-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="1f99f-126">NuGet önbelleği yönetme</span><span class="sxs-lookup"><span data-stu-id="1f99f-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="1f99f-127">Bir paket çoğaltma</span><span class="sxs-lookup"><span data-stu-id="1f99f-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="1f99f-128">Başka bir iyi araçtır [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), görsel olarak araştırmak, oluşturmak ve NuGet paketleri düzenlemek için açık kaynaklı, tek başına bir araç.</span><span class="sxs-lookup"><span data-stu-id="1f99f-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="1f99f-129">Örneğin, paket her zaman yeniden oluşturmak zorunda kalmadan bir paket yapısı Deneysel değişiklik yapmak için çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="1f99f-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="1f99f-130">Platformlar arası [.NET Core CLI](/dotnet/articles/core/tools/index#installation) .NET Core uygulamaları geliştirmek için kullanılan araç zinciri, silebilir, yerel öğeler, gönderme, paketi ve geri yükleme gibi birkaç NuGet komutlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="1f99f-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="1f99f-131">NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="1f99f-131">NuGet CLI</span></span>

<span data-ttu-id="1f99f-132">NuGet komut satırı arabirimi NuGet olanaklarına erişim sağlar ve Windows, Mac OSX ve aşağıdaki bölümlerde açıklandığı gibi Linux üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="1f99f-133">Windows</span><span class="sxs-lookup"><span data-stu-id="1f99f-133">Windows</span></span>

<span data-ttu-id="1f99f-134">**Doğrudan indirme:**</span><span class="sxs-lookup"><span data-stu-id="1f99f-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="1f99f-135">NuGet ile 1.4 +, kullandığınız `nuget update -self` varolan nuget.exe en son sürüme güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="1f99f-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="1f99f-136">**Diğer yöntemleri:**</span><span class="sxs-lookup"><span data-stu-id="1f99f-136">**Other methods:**</span></span>

- <span data-ttu-id="1f99f-137">**Chocolatey**: yükleme [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey paketini kullanarak [Chocolatey](http://chocolatey.org) istemci.</span><span class="sxs-lookup"><span data-stu-id="1f99f-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="1f99f-138">**Visual Studio**: yükleme [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) Visual Studio'da Paket Yöneticisi Konsolu'ndan paket.</span><span class="sxs-lookup"><span data-stu-id="1f99f-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="1f99f-139">**NuGet 2.x kullanıcılar için**: NuGet 3.2 sürümünde sunulan değişiklikler nedeniyle [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) noktaları en son kararlı sürekli tümleştirme sistemleri olası önlemek için NuGet 2.x sürüm kesiliyor.</span><span class="sxs-lookup"><span data-stu-id="1f99f-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="1f99f-140">Mac OSX ve Linux</span><span class="sxs-lookup"><span data-stu-id="1f99f-140">Mac OSX and Linux</span></span>

<span data-ttu-id="1f99f-141">Mac OSX ve Linux üzerinde NuGet CLI çalıştırmak için iki yol vardır:</span><span class="sxs-lookup"><span data-stu-id="1f99f-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="1f99f-142">Yükleme [.NET Core SDK](https://www.microsoft.com/net/download/core), çekirdek NuGet özellikler içerir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="1f99f-143">Yüklemeleri de listelenir [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="1f99f-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="1f99f-144">Daha eksiksiz özelliklerine ihtiyacınız varsa, ardından aşağıdaki ikinci seçeneği kullanmak için kullanmak `nuget.exe` Mono ile.</span><span class="sxs-lookup"><span data-stu-id="1f99f-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="1f99f-145">Yükleme [Mono](http://www.mono-project.com/docs/getting-started/install/) ve sonra da `nuget.exe` (sürüm 3.2 ve üstü) Windows'dan komut satırı yürütülebilir dosyası [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="1f99f-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="1f99f-146">NuGet üzerinde Mono aşağıdaki sınırlamalara tabi çalışıyor:</span><span class="sxs-lookup"><span data-stu-id="1f99f-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="1f99f-147">Komutları çalışmaya test edilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1f99f-147">Commands tested to work:</span></span>
        - <span data-ttu-id="1f99f-148">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1f99f-148">config</span></span>
        - <span data-ttu-id="1f99f-149">Sil</span><span class="sxs-lookup"><span data-stu-id="1f99f-149">delete</span></span>
        - <span data-ttu-id="1f99f-150">Yardım</span><span class="sxs-lookup"><span data-stu-id="1f99f-150">help</span></span>
        - <span data-ttu-id="1f99f-151">Yükleme</span><span class="sxs-lookup"><span data-stu-id="1f99f-151">install</span></span>
        - <span data-ttu-id="1f99f-152">liste</span><span class="sxs-lookup"><span data-stu-id="1f99f-152">list</span></span>
        - <span data-ttu-id="1f99f-153">Anında iletme</span><span class="sxs-lookup"><span data-stu-id="1f99f-153">push</span></span>
        - <span data-ttu-id="1f99f-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="1f99f-154">setApiKey</span></span>
        - <span data-ttu-id="1f99f-155">Kaynakları</span><span class="sxs-lookup"><span data-stu-id="1f99f-155">sources</span></span>
        - <span data-ttu-id="1f99f-156">belirtimi</span><span class="sxs-lookup"><span data-stu-id="1f99f-156">spec</span></span>

    - <span data-ttu-id="1f99f-157">Kısmen çalışan komutlar:</span><span class="sxs-lookup"><span data-stu-id="1f99f-157">Partially-working commands:</span></span>
        - <span data-ttu-id="1f99f-158">paketi: ile çalışır `.nuspec` dosyaları proje dosyalarını birlikte değil.</span><span class="sxs-lookup"><span data-stu-id="1f99f-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="1f99f-159">geri yükleme: ile çalışır `packages.config` ve `project.json` dosyaları bilgisayardı çözüm (`.sln`) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="1f99f-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="1f99f-160">İşe yaramazsa komutlar:</span><span class="sxs-lookup"><span data-stu-id="1f99f-160">Commands that do not work:</span></span>
        - <span data-ttu-id="1f99f-161">Güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1f99f-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="1f99f-162">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="1f99f-162">Related topics</span></span>

- [<span data-ttu-id="1f99f-163">NuGet CLI başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f99f-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="1f99f-164">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f99f-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="1f99f-165">Bir paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="1f99f-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="1f99f-166">Visual Studio'da NuGet Paket Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="1f99f-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="1f99f-167">NuGet Paket Yöneticisi Visual Studio 2012 ve sonraki Windows her sürümü dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="1f99f-168">Paket Yöneticisi kullanıcı Arabirimi içerir ([başvuru](../tools/package-manager-ui.md)) ve Paket Yöneticisi konsolu üzerinden erişebilirsiniz belirli paketlerle gelen araçlar ([başvuru](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="1f99f-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="1f99f-169">Visual Studio 2017 yükleyici .NET kullanan herhangi bir iş yükü ile NuGet Paket Yöneticisi'ni içerir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="1f99f-170">Ayrı olarak yüklemeniz ya da Paket Yöneticisi'nin yüklü olduğunu doğrulamak için Visual Studio 2017 yükleyiciyi çalıştırın ve altında seçeneğini **bileşenleri tek tek > kod Araçlar > NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="1f99f-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="1f99f-171">Konsol gerektirir [PowerShell 2.0](http://support.microsoft.com/kb/968929), zaten olacak Windows 7 veya üstü ve Windows Server 2008 R2 üzerinde yüklü ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="1f99f-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="1f99f-172">Paket Yöneticisi konsolu komutlar, yalnızca Visual Studio içinde Windows üzerinde de çalışır.</span><span class="sxs-lookup"><span data-stu-id="1f99f-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="1f99f-173">Mac ve Visual Studio Code için Visual Studio ile de dahil olmak üzere bu ortam dışında NuGet CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f99f-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="1f99f-174">Paket Yöneticisi'ni yükleme ve önceki sürümler için Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="1f99f-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="1f99f-175">*Bu adımları zaten Paket Yöneticisi içeren Visual Studio 2012 için gerekli ve daha sonra değildir.*</span><span class="sxs-lookup"><span data-stu-id="1f99f-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="1f99f-176">Visual Studio 2010 ve daha önce'ı **Araçlar > uzantısı ve güncelleştirmeleri**.</span><span class="sxs-lookup"><span data-stu-id="1f99f-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="1f99f-177">Gidin **çevrimiçi**, NuGet Paket Yöneticisi için Visual Studio için"" araması yapın ve tıklayın **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="1f99f-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="1f99f-178">Yükleyici iletişim kutusunda tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="1f99f-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="1f99f-179">Yükleme tamamlandığında, Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1f99f-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="1f99f-180">Kullanılacak yapamıyorsanız **Uzantılar ve güncelleştirmeler** iletişim (örneğin, bir proxy tarafından kendi engellenen) Visual Studio, Visual Studio 2013 ve doğrudan 2015 için uzantıları yükleyebilirsiniz [https://dist.nuget.org/ index.HTML](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="1f99f-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="1f99f-181">Paket Yöneticisi güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="1f99f-181">Updating the Package Manager</span></span>

<span data-ttu-id="1f99f-182">Visual Studio 2015 güncelleştirme 2 ve daha sonra Paket Yöneticisi otomatik olarak en son kararlı sürümüne güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1f99f-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="1f99f-183">Seçin ve önceki sürümleri, Visual Studio 2015 güncelleştirme 1 için **Araçlar > Uzantılar ve güncelleştirmeler** komut ve tıklayın **güncelleştirmeleri** Paket Yöneticisi'nin yeni bir sürümü kullanılabilir olup olmadığını görmek için sekmesini.</span><span class="sxs-lookup"><span data-stu-id="1f99f-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="1f99f-184">NuGet önizlemeleri</span><span class="sxs-lookup"><span data-stu-id="1f99f-184">NuGet previews</span></span>

<span data-ttu-id="1f99f-185">Yaklaşan NuGet özellikleri Önizleme istiyorsanız, yükleme [Visual Studio 2017 Önizleme](https://www.visualstudio.com/vs/preview/), Visual Studio, kararlı sürümleriyle-yana çalışır.</span><span class="sxs-lookup"><span data-stu-id="1f99f-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="1f99f-186">Önceki NuGet Beta kanal Not (`https://dotnet.myget.org/F/nuget-beta/vsix/`) Visual Studio 2015 artık kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1f99f-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="1f99f-187">NuGet herhangi bir sürümünden sorunları rapor veya fikirleri paylaşmak için bir sorun açmak için [NuGet GitHub deposunu](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="1f99f-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="1f99f-188">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="1f99f-188">Related topics</span></span>

- [<span data-ttu-id="1f99f-189">Paket Yöneticisi kullanıcı Arabirimi başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f99f-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="1f99f-190">Paket Yöneticisi konsolu başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f99f-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="1f99f-191">Paket Yöneticisi konsolu PowerShell başvurusu</span><span class="sxs-lookup"><span data-stu-id="1f99f-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)