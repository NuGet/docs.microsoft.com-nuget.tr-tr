---
title: NuGet bilinen sorunlar | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Kimlik doğrulama, paket yükleme ve araçlar da dahil olmak üzere NuGet ile ilgili bilinen sorunlar."
keywords: "Bilinen sorunlar, NuGet sorunları NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: bd85d9da61753d25c8918c7d55fab775820b017b
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="f713f-104">NuGet ile ilgili bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="f713f-104">Known Issues with NuGet</span></span>

<span data-ttu-id="f713f-105">Sürekli olarak bildirilen en yaygın ile ilgili bilinen sorunların NuGet bunlar.</span><span class="sxs-lookup"><span data-stu-id="f713f-105">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="f713f-106">NuGet yüklemeden veya paketlerini yönetme konusunda sorun yaşıyorsanız, lütfen bu bilinen sorunlar ve bunların çözümleri aracılığıyla göz atın.</span><span class="sxs-lookup"><span data-stu-id="f713f-106">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="f713f-107">NuGet 4.0 ile başlayarak, bilinen sorunlar ilgili sürüm notları, parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f713f-107">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="f713f-108">NuGet ile kimlik doğrulaması sorunlarını nuget.exe v3.4.3 ile VSTS içinde akışları</span><span class="sxs-lookup"><span data-stu-id="f713f-108">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="f713f-109">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="f713f-109">**Problem:**</span></span>

<span data-ttu-id="f713f-110">Şu kimlik bilgilerini depolamak için aşağıdaki komutu kullandığınızda, çift kişisel erişim belirteci şifreleme yukarı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="f713f-110">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="f713f-111">$PAT "Kişisel erişim belirtecinizi" = $Feed kaynakları ekleyin-"URL'si,".\nuget.exe Test adına =-kaynak $Feed - UserName $UserName-parola $PAT</span><span class="sxs-lookup"><span data-stu-id="f713f-111">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="f713f-112">**Geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="f713f-112">**Workaround:**</span></span>

<span data-ttu-id="f713f-113">Depolama parolaları düz metin kullanarak [- StorePasswordInClearText](../tools/cli-ref-sources.md) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f713f-113">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="f713f-114">3.4.1 NuGet 3.4 ile paketler yüklenirken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="f713f-114">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="f713f-115">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="f713f-115">**Problem:**</span></span>

<span data-ttu-id="f713f-116">NuGet 3.4 ve 3.4.1, NuGet eklenti kullanırken, herhangi bir kaynağa kullanılabilir olarak bildirilir ve yeni kaynakları yapılandırma penceresinde ekleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="f713f-116">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="f713f-117">Aşağıdaki görüntü sonucu benzer:</span><span class="sxs-lookup"><span data-stu-id="f713f-117">The result is similar to the image below:</span></span>

![Hiçbir kaynaklarıyla NuGet yapılandırma](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="f713f-119">`NuGet.Config` Dosyasını, `%AppData%\NuGet\` klasörü yanlışlıkla boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="f713f-119">The `NuGet.Config` file in your `%AppData%\NuGet\` folder has accidentally been emptied.</span></span> <span data-ttu-id="f713f-120">Bu sorunu gidermek için: Kapat Visual Studio 2015, silme `NuGet.Config` dosyasını `%AppData%\NuGet\` klasörü ve Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f713f-120">To fix this: Close Visual Studio 2015, delete the `NuGet.Config` file in the `%AppData%\NuGet\` folder and restart Visual Studio.</span></span>  <span data-ttu-id="f713f-121">Yeni bir `NuGet.Config` dosya oluşturulur ve devam etmek mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f713f-121">A new `NuGet.Config` file will be generated and you will be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="f713f-122">NuGet 2.7 ile paketler yüklenirken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="f713f-122">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="f713f-123">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="f713f-123">**Problem:**</span></span>

<span data-ttu-id="f713f-124">NuGet 2.7 veya üzerini derleme başvuruları içeren herhangi bir paket yüklemeye çalıştığınızda hata iletisini alabilirsiniz **"giriş dizesi değildi doğru bir biçimde."** gibi altında:</span><span class="sxs-lookup"><span data-stu-id="f713f-124">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="f713f-125">Bu tür kitaplığının kaynaklanır `VSLangProj.dll` sisteminizde kaydedilmeyen COM bileşeni.</span><span class="sxs-lookup"><span data-stu-id="f713f-125">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="f713f-126">Bu durum, örneğin, varsa iki Visual Studio sürümlerini yan yana ve yüklü sonra eski sürümü kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f713f-126">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="f713f-127">Bunun yapılması, yukarıdaki COM kitaplığı yanlışlıkla bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="f713f-127">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="f713f-128">**Çözüm:**:</span><span class="sxs-lookup"><span data-stu-id="f713f-128">**Solution:**:</span></span>

<span data-ttu-id="f713f-129">Bu komutu çalıştırmak bir **yükseltilmiş istemi** için tür kitaplığı yeniden kaydetmek için`VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="f713f-129">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="f713f-130">Komut başarısız olursa, dosyanın bu konumda olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f713f-130">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="f713f-131">Bu hata hakkında daha fazla bilgi için bkz [iş öğesi](https://nuget.codeplex.com/workitem/3609 "iş öğesi 3609").</span><span class="sxs-lookup"><span data-stu-id="f713f-131">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="f713f-132">Derleme hatasından sonra VS 2012'de paket güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="f713f-132">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="f713f-133">Sorun: VS 2012 RTM kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="f713f-133">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="f713f-134">NuGet paket güncelleştirilirken bu ileti Al: "bir veya daha fazla paket tamamlanamadı kaldırıldı."</span><span class="sxs-lookup"><span data-stu-id="f713f-134">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="f713f-135">ve Visual Studio yeniden başlatmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="f713f-135">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="f713f-136">VS yeniden başlattıktan sonra tuhaf derleme hataları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f713f-136">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="f713f-137">Eski paketler belirli dosyaları arka planda MSBuild işlem kilitlenen nedenidir.</span><span class="sxs-lookup"><span data-stu-id="f713f-137">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="f713f-138">Hatta VS yeniden başlattıktan sonra arka plan MSBuild işlem yapı hatalarına neden eski paketlerdeki dosyalar devam eder.</span><span class="sxs-lookup"><span data-stu-id="f713f-138">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="f713f-139">Düzeltme VS 2012 güncelleştirmesi, örneğin VS 2012 güncelleştirme 2 yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="f713f-139">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="f713f-140">En son NuGet eski bir sürümden yükseltme bir imza doğrulama hatasına neden oluyor</span><span class="sxs-lookup"><span data-stu-id="f713f-140">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="f713f-141">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken aşağıdaki hata iletisine çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713f-141">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio Uzantı Yükleyicisi](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="f713f-143">Günlükleri görüntülerken, Bahsetme görebileceğiniz bir `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="f713f-143">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="f713f-144">Bu, var olmaması için bir [Visual Studio 2010 SP1 Düzeltmesi](http://bit.ly/vsixcertfix) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713f-144">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="f713f-145">Alternatif olarak, yalnızca NuGet (yönetici olarak Visual Studio çalıştırılırken) kaldırıp VS uzantısı Galeriden yükleme geçici bir çözüm değildir.</span><span class="sxs-lookup"><span data-stu-id="f713f-145">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="f713f-146">Bkz: [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f713f-146">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="f713f-147">Reflector Visual Studio eklentisi ayrıca yüklendiğinde, Paket Yöneticisi konsolu bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f713f-147">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="f713f-148">Reflector VS yüklü eklenti varsa Paket Yöneticisi konsolu çalışırken, aşağıdaki özel durum iletisi çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="f713f-148">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="f713f-149">veya</span><span class="sxs-lookup"><span data-stu-id="f713f-149">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="f713f-150">Şu eklenti bir çözüm çalışma büyük yazarı temas.</span><span class="sxs-lookup"><span data-stu-id="f713f-150">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="f713f-151">Güncelleştirme: Reflector, 6.5, en son sürümünü konsolda artık bu özel durumun neden doğrulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f713f-151">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="f713f-152">Açılış Paket Yöneticisi konsolu ObjectSecurity özel durum ile başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="f713f-152">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="f713f-153">Paket Yöneticisi konsolu açmaya çalışırken bu hatalar görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f713f-153">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="f713f-154">Bu durumda, çözümü uygulayın [üzerinde StackOverflow ele alınan](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) bunları düzeltmek için.</span><span class="sxs-lookup"><span data-stu-id="f713f-154">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="f713f-155">Çözüm InstallShield Limited Edition proje içeriyorsa, paket Kitaplığı Başvurusu Ekle iletişim kutusu bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f713f-155">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="f713f-156">Çözümünüzü bir veya daha fazla InstallShield Limited Edition proje içeriyorsa, belirledik, **paketi Kitaplığı Başvurusu Ekle** iletişim kutusu açıldığında bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f713f-156">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="f713f-157">Şu anda henüz InstallShield projeleri kaldırma veya bunları kaldırma dışında geçici çözüm yoktur.</span><span class="sxs-lookup"><span data-stu-id="f713f-157">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="f713f-158">Düğmesi gri çıkışı kaldırabilir?</span><span class="sxs-lookup"><span data-stu-id="f713f-158">Uninstall Button Greyed out?</span></span> <span data-ttu-id="f713f-159">NuGet yükleme/kaldırma için yönetici ayrıcalıkları gerektirmez</span><span class="sxs-lookup"><span data-stu-id="f713f-159">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="f713f-160">NuGet aracılığıyla Visual Studio Uzantı Yöneticisi kaldırmayı denerseniz, Kaldır düğmesini devre dışı olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713f-160">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="f713f-161">NuGet yüklemek ve kaldırmak için yönetici erişimi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f713f-161">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="f713f-162">Visual Studio uzantısı kaldırmak için yönetici yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f713f-162">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="f713f-163">NuGet kullanmak için yönetici erişimi gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="f713f-163">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="f713f-164">Windows XP'de açtığınızda, Paket Yöneticisi konsolu çöker.</span><span class="sxs-lookup"><span data-stu-id="f713f-164">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="f713f-165">Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="f713f-165">What's wrong?</span></span>

<span data-ttu-id="f713f-166">NuGet Powershell 2.0 çalışma zamanını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f713f-166">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="f713f-167">Windows XP, varsayılan olarak, Powershell 2.0 sahip değil.</span><span class="sxs-lookup"><span data-stu-id="f713f-167">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="f713f-168">Powershell 2.0 çalışma zamanını şuradan indirebilirsiniz [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="f713f-168">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="f713f-169">Yükledikten sonra Visual Studio'yu yeniden başlatın ve Paket Yöneticisi konsolu yapabiliyor olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f713f-169">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="f713f-170">Paket Yöneticisi konsolu açıksa, visual Studio 2010 SP1 Beta Çıkışta çöküyor.</span><span class="sxs-lookup"><span data-stu-id="f713f-170">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="f713f-171">Visual Studio 2010 SP1 Beta yüklediyseniz, Paket Yöneticisi konsolunu açık bırakın ve Visual Studio'yu kapatın, onu kilitleniyor fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713f-171">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="f713f-172">Bu, Visual Studio'nun bilinen bir sorundur ve SP1 RTM sabit serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="f713f-172">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="f713f-173">Şimdilik, kilitlenme Yoksay veya yapabiliyorsanız SP1 Beta kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f713f-173">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="f713f-174">'Meta verileri'... öğesi geçersiz alt öğesi özel durumu olan oluşur</span><span class="sxs-lookup"><span data-stu-id="f713f-174">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="f713f-175">NuGet bir yayım öncesi sürümü ile oluşturulan paketler yüklediyseniz, "ad alanında 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' ' meta verileri' öğesi, geçersiz alt öğesi var" bildiren bir hata iletisi karşılaşabileceğiniz RTM çalışırken Bu proje ile olan NuGet sürümü.</span><span class="sxs-lookup"><span data-stu-id="f713f-175">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="f713f-176">Kaldırmanız ve NuGet'in RTM sürümünü kullanan her bir paketi yeniden yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f713f-176">You'll need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="f713f-177">Yükleme veya "Bu dosya zaten varken bir dosya oluşturamıyor." hatası sonuçlarında kaldırma girişimi</span><span class="sxs-lookup"><span data-stu-id="f713f-177">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="f713f-178">Herhangi bir nedenle burada VSIX uzantısı kaldırıldı, ancak bazı dosyalar geride tuhaf durumda Visual Studio uzantıları elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f713f-178">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="f713f-179">Bu soruna geçici bir çözüm bulmak için:</span><span class="sxs-lookup"><span data-stu-id="f713f-179">To work around this issue:</span></span>

1. <span data-ttu-id="f713f-180">Exit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f713f-180">Exit Visual Studio</span></span>
1. <span data-ttu-id="f713f-181">(Bu, makinenize farklı bir sürücüde olabilir) şu klasörü açın</span><span class="sxs-lookup"><span data-stu-id="f713f-181">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="f713f-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="f713f-182">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="f713f-183">İle tüm dosyaları silin *.deleteme* uzantıları.</span><span class="sxs-lookup"><span data-stu-id="f713f-183">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="f713f-184">Visual Studio'da yeniden açın</span><span class="sxs-lookup"><span data-stu-id="f713f-184">Re-open Visual Studio</span></span>

<span data-ttu-id="f713f-185">Bu adımları uyguladıktan sonra devam etmek mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f713f-185">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="f713f-186">Nadir durumlarda açık Kod Analizi ile derleme hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="f713f-186">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="f713f-187">Paket Yöneticisi konsolu ile FluentNHibernate yüklerse aşağıdaki hatayı alıyorsunuz ve açık "Kod Analizi" ile projenizi derleme.</span><span class="sxs-lookup"><span data-stu-id="f713f-187">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="f713f-188">Varsayılan olarak, FluentNHibernate NHibernate 3.0.0.2001 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f713f-188">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="f713f-189">Ancak, tasarım gereği NuGet NHibernate 3.0.0.4000 projenizde yükleyecek ve böylece çalışır uygun bağlama yeniden yönlendirmelerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f713f-189">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="f713f-190">Kod çözümleme açık değilse, proje düzgün derlenir.</span><span class="sxs-lookup"><span data-stu-id="f713f-190">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="f713f-191">Derleyici aksine kod analizi aracı düzgün 3.0.0.4000 yerine 3.0.0.2001 kullanmak için bağlama yeniden yönlendirmeleri izleyin değil.</span><span class="sxs-lookup"><span data-stu-id="f713f-191">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="f713f-192">Ya da yükleme NHibernate 3.0.0.2001 sorundan geçici çözüm ya da derleyici aynı aşağıdakileri yaparak davranmasına kod analizi aracı söyleyin:</span><span class="sxs-lookup"><span data-stu-id="f713f-192">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="f713f-193">Git *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analiz Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="f713f-193">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="f713f-194">FxCopCmd.exe.config açın ve değiştirme `AssemblyReferenceResolveMode` gelen `StrongName` için `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="f713f-194">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="f713f-195">Değişikliği kaydetmek ve projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="f713f-195">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="f713f-196">Yazma hatası komutu install.ps1/uninstall.ps1/init.ps1 içinde çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="f713f-196">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="f713f-197">Bu bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="f713f-197">This is a known issue.</span></span> <span data-ttu-id="f713f-198">Write-Error çağırmak yerine, throw çağırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="f713f-198">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="f713f-199">Windows 2003'te kısıtlı erişime sahip NuGet yükleme Visual Studio çökebilir</span><span class="sxs-lookup"><span data-stu-id="f713f-199">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="f713f-200">Visual Studio Uzantı Yöneticisi'ni kullanarak ve bir yönetici olarak çalışmıyor NuGet yüklemeye çalışırken &#8220; Farklı Çalıştır &#8221; iletişim kutusu etiketli onay kutusunu &#8220;görüntülenir; Kısıtlı erişim &#8221;bu programı çalıştır; Varsayılan olarak işaretli.</span><span class="sxs-lookup"><span data-stu-id="f713f-200">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Sınırlı iletişim kutusu olarak çalıştırma](./media/RunAsRestricted.png)

<span data-ttu-id="f713f-202">İşaretli değilse, ile Tamam'a tıkladığınızda Visual Studio kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="f713f-202">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="f713f-203">NuGet'ı yüklemeden önce bu seçeneğin işaretini kaldırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f713f-203">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="f713f-204">Windows Phone araçları NuGet kaldıramadı.</span><span class="sxs-lookup"><span data-stu-id="f713f-204">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="f713f-205">Windows Phone araçları Visual Studio uzantısı Yöneticisi için destek yok.</span><span class="sxs-lookup"><span data-stu-id="f713f-205">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="f713f-206">NuGet kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f713f-206">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="f713f-207">Paket geri yüklemesi keser NuGet paket kimliği, büyük/küçük harf değiştirme</span><span class="sxs-lookup"><span data-stu-id="f713f-207">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="f713f-208">Üzerinde en length anlatıldığı gibi [bu GitHub sorunu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), NuGet paketleri, büyük/küçük harf değiştirme yapılabilir NuGet destek ancak nedenler zorluklar farklı-ortası, var olan kullanıcılar paketler için paket geri yüklemesi sırasında kendi yerel paket önbelleği.</span><span class="sxs-lookup"><span data-stu-id="f713f-208">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their local package cache.</span></span> <span data-ttu-id="f713f-209">Varolan kullanıcılar, derleme zamanı paket geri yüklemesi oluşabilir sonu hakkında paketinin ile iletişim kurmak için bir yol olduğunda yalnızca büyük/küçük harf değiştirme isteyen öneririz.</span><span class="sxs-lookup"><span data-stu-id="f713f-209">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="f713f-210">Raporlama konuları</span><span class="sxs-lookup"><span data-stu-id="f713f-210">Reporting issues</span></span>

<span data-ttu-id="f713f-211">NuGet sorunları bildirmek için ziyaret [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="f713f-211">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
