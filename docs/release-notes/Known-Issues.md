---
title: Bilinen Sorunlar
description: Kimlik doğrulaması, paket yükleme ve araçlar da dahil olmak üzere NuGet ile ilgili bilinen sorunlar.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548480"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="496a8-103">NuGet ile ilgili bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="496a8-103">Known Issues with NuGet</span></span>

<span data-ttu-id="496a8-104">Sürekli olarak bildirilen en sık karşılaşılan bilinen sorunlar NuGet ile şunlardır.</span><span class="sxs-lookup"><span data-stu-id="496a8-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="496a8-105">NuGet yükleme veya paketlerini yönetme konusunda sorun yaşıyorsanız, lütfen bu bilinen sorunlar ve çözümleri aracılığıyla göz atın.</span><span class="sxs-lookup"><span data-stu-id="496a8-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="496a8-106">NuGet 4.0 ile başlayarak, bilinen sorunlar, ilgili sürüm notlarını parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="496a8-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="496a8-107">NuGet ile kimlik doğrulama sorunları ile nuget.exe v3.4.3 VSTS'de akışları</span><span class="sxs-lookup"><span data-stu-id="496a8-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="496a8-108">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="496a8-108">**Problem:**</span></span>

<span data-ttu-id="496a8-109">Şu kimlik bilgilerini depolamak için aşağıdaki komutu kullandığınızda, çift kişisel erişim belirteci şifreleme yukarı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="496a8-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="496a8-110">$PAT "Kişisel erişim belirtecinizi" = $Feed kaynakları Ekle-"url".\nuget.exe adı Test =-kaynak $Feed - UserName $UserName-parola $PAT</span><span class="sxs-lookup"><span data-stu-id="496a8-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="496a8-111">**Geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="496a8-111">**Workaround:**</span></span>

<span data-ttu-id="496a8-112">Kullanarak düz metin parolalar Store [- StorePasswordInClearText](../tools/cli-ref-sources.md) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="496a8-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="496a8-113">NuGet 3.4, 3.4.1 paketleri yüklenirken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="496a8-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="496a8-114">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="496a8-114">**Problem:**</span></span>

<span data-ttu-id="496a8-115">NuGet 3.4 ve 3.4.1, kaynağı yok NuGet eklentisini kullanırken, kullanılabilir olarak raporlanır ve yeni kaynakları yapılandırma penceresinde eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="496a8-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="496a8-116">Sonuç aşağıdaki görüntüye benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="496a8-116">The result is similar to the image below:</span></span>

![NuGet yapılandırmasını kaynağı yok](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="496a8-118">`NuGet.Config` Dosyası, `%AppData%\NuGet\` (Windows) veya `~/.nuget/` (Mac/Linux) klasör yanlışlıkla boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="496a8-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="496a8-119">Bu sorunu gidermek için: (Windows, eğer varsa üzerinde) Visual Studio'yu kapatın, silme `NuGet.Config` dosya ve işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="496a8-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="496a8-120">NuGet yeni oluşturulan `NuGet.Config` ve devam etmek mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="496a8-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="496a8-121">2.7 ile NuGet paketleri yüklenirken hata oluştu</span><span class="sxs-lookup"><span data-stu-id="496a8-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="496a8-122">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="496a8-122">**Problem:**</span></span>

<span data-ttu-id="496a8-123">NuGet 2.7 ya da üzeri, derleme başvuruları içeren herhangi bir paket yüklemeye çalıştığınızda, hata iletisi alabilirsiniz **"giriş dizesi değil doğru bir biçimde."** gibi aşağıda:</span><span class="sxs-lookup"><span data-stu-id="496a8-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="496a8-124">Bu tür kitaplığının kaynaklanır `VSLangProj.dll` sisteminizde kaydedilmeyen bir COM bileşeni.</span><span class="sxs-lookup"><span data-stu-id="496a8-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="496a8-125">Bu durum ortaya çıkabilir, örneğin, varsa iki Visual Studio sürümleri ve yan yana yüklü ardından eski sürümü kaldırın.</span><span class="sxs-lookup"><span data-stu-id="496a8-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="496a8-126">Bunun yapılması, yukarıdaki COM kitaplığı yanlışlıkla bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="496a8-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="496a8-127">**Çözüm:**:</span><span class="sxs-lookup"><span data-stu-id="496a8-127">**Solution:**:</span></span>

<span data-ttu-id="496a8-128">Bu komutu çalıştırın bir **yükseltilmiş istem** için tür kitaplığı yeniden kaydetmek için `VSLangProj.dll`</span><span class="sxs-lookup"><span data-stu-id="496a8-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="496a8-129">Komut başarısız olursa, dosyanın bu konumda olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="496a8-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="496a8-130">Bu hata hakkında daha fazla bilgi için bkz. Bu [iş öğesi](https://nuget.codeplex.com/workitem/3609 "iş öğesi 3609").</span><span class="sxs-lookup"><span data-stu-id="496a8-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="496a8-131">VS 2012'de paket güncelleştirmesinden sonra derleme hatası</span><span class="sxs-lookup"><span data-stu-id="496a8-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="496a8-132">Sorun: VS 2012 RTM kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="496a8-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="496a8-133">NuGet paketleri güncelleştirildikten sonra bu iletiyi alırsınız: "bir veya daha fazla paket tamamlanamadı kaldırıldı."</span><span class="sxs-lookup"><span data-stu-id="496a8-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="496a8-134">ve Visual Studio'yu yeniden başlatmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="496a8-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="496a8-135">VS yeniden başlattıktan sonra tuhaf derleme hataları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="496a8-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="496a8-136">Belirli paketlerdeki dosyalar eski bir arka plan MSBuild işlem tarafından kilitlidir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="496a8-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="496a8-137">VS yeniden başlatmanızın ardından dahi, arka plan MSBuild işlem yine de derleme hatalarına neden eski paketleri, dosyaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="496a8-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="496a8-138">VS 2012 güncelleştirmesi, örneğin VS 2012 Update 2 düzeltme yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="496a8-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="496a8-139">En son NuGet için eski bir sürümden yükseltme bir imza doğrulama hatasına neden olur</span><span class="sxs-lookup"><span data-stu-id="496a8-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="496a8-140">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken aşağıdaki hata iletisine çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="496a8-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio Uzantı Yükleyicisi](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="496a8-142">Günlükleri görüntülerken, bir Bahsetme görebileceğiniz bir `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="496a8-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="496a8-143">Bu, var olmaması için bir [Visual Studio 2010 SP1 Düzeltmesi](http://bit.ly/vsixcertfix) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="496a8-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="496a8-144">Alternatif olarak, yalnızca (yönetici olarak Visual Studio çalıştırılırken) NuGet kaldırın ve VS uzantısı Galeriden yüklemeyi çözüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="496a8-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="496a8-145">Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="496a8-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="496a8-146">Paket Yöneticisi konsolu, Reflector Visual Studio eklentisini de yüklendiğinde, özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="496a8-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="496a8-147">Reflector VS yüklü eklenti varsa Paket Yöneticisi konsolu çalışırken, aşağıdaki durum iletisine çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="496a8-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="496a8-148">veya</span><span class="sxs-lookup"><span data-stu-id="496a8-148">or</span></span>

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

<span data-ttu-id="496a8-149">Biz, eklentinin bir çözüm çalışmanın yiyeceklere yazarı görüştüğünüz.</span><span class="sxs-lookup"><span data-stu-id="496a8-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="496a8-150">Güncelleştirme: Reflector, 6.5, en son sürümünü konsolda artık bu özel durumun neden doğrulanmıştır.</span><span class="sxs-lookup"><span data-stu-id="496a8-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="496a8-151">Açılış Paket Yöneticisi konsolu ObjectSecurity özel durumuyla başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="496a8-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="496a8-152">Paket Yöneticisi konsolu çalışırken bu hataları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="496a8-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="496a8-153">Bu durumda, çözümü uygulayın [StackOverflow ele alınan](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) bunları düzeltmek için.</span><span class="sxs-lookup"><span data-stu-id="496a8-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="496a8-154">Çözüm InstallShield Limited Edition projesi içeriyorsa, paket Kitaplığı Başvurusu Ekle iletişim kutusu bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="496a8-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="496a8-155">Çözümünüz bir veya daha fazla InstallShield Limited Edition projesi içeriyorsa, belirledik, **paketi Kitaplığı Başvurusu Ekle** iletişim kutusu açıldığında bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="496a8-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="496a8-156">Şu anda henüz InstallShield projeleri kaldırma veya bunları kaldırma dışında geçici çözüm yoktur.</span><span class="sxs-lookup"><span data-stu-id="496a8-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="496a8-157">Kaldır düğmesi gri?</span><span class="sxs-lookup"><span data-stu-id="496a8-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="496a8-158">NuGet yükleme/kaldırma için yönetici ayrıcalıkları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="496a8-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="496a8-159">NuGet aracılığıyla Visual Studio Uzantı Yöneticisi kaldırmayı denerseniz, Kaldır düğmesini devre dışı olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="496a8-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="496a8-160">NuGet, yüklemek ve kaldırmak için yönetici erişimi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="496a8-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="496a8-161">Visual Studio, uzantıyı kaldırmak için yönetici olarak yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="496a8-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="496a8-162">NuGet kullanmak için yönetici erişimi gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="496a8-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="496a8-163">Windows XP'de açtığınızda, Paket Yöneticisi konsolu çöker.</span><span class="sxs-lookup"><span data-stu-id="496a8-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="496a8-164">Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="496a8-164">What's wrong?</span></span>

<span data-ttu-id="496a8-165">NuGet Powershell 2.0 çalışma zamanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="496a8-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="496a8-166">Windows XP Powershell 2.0 varsayılan olarak, sahip değil.</span><span class="sxs-lookup"><span data-stu-id="496a8-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="496a8-167">Powershell 2.0 çalışma zamanını şuradan indirebilirsiniz [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="496a8-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="496a8-168">Yükledikten sonra Visual Studio'yu yeniden başlatın ve Paket Yöneticisi konsolu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="496a8-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="496a8-169">Paket Yöneticisi konsolu açık değilse visual Studio 2010 SP1 Beta Çıkışta kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="496a8-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="496a8-170">Visual Studio 2010 SP1 Beta yüklediyseniz, Paket Yöneticisi konsolunu açık bırakın ve Visual Studio'yu kapatın, onu kilitlenir fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="496a8-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="496a8-171">Bu, Visual Studio'nun bilinen bir sorundur ve SP1 RTM'de düzeltilecektir bırakın.</span><span class="sxs-lookup"><span data-stu-id="496a8-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="496a8-172">Şimdilik yalnızca kilitlenme Yoksay veya mümkünse SP1 Beta kaldırın.</span><span class="sxs-lookup"><span data-stu-id="496a8-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="496a8-173">' % S'öğesi 'metadata'... sahip geçersiz bir alt öğesi özel durum oluşur</span><span class="sxs-lookup"><span data-stu-id="496a8-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="496a8-174">NuGet yayın öncesi bir sürümü ile oluşturulan paketler yüklü değilse, "'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' ad alanındaki ' metadata' öğesi geçersiz alt öğesine sahip" belirten bir hata iletisi karşılaşabileceğiniz RTM çalışırken Bu proje ile NuGet sürümü.</span><span class="sxs-lookup"><span data-stu-id="496a8-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="496a8-175">Kaldırmanız ve ardından her paketini NuGet RTM sürümünü kullanarak yeniden yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="496a8-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="496a8-176">Yükleme veya "Bu dosya zaten varken bir dosya oluşturulamıyor." hatasına kaldırma girişimi</span><span class="sxs-lookup"><span data-stu-id="496a8-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="496a8-177">Bazı nedenlerden dolayı burada VSIX uzantısı kaldırdınız, ancak bazı dosyalar bırakılmış tuhaf durumda Visual Studio uzantıları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="496a8-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="496a8-178">Bu soruna geçici bir çözüm bulmak için:</span><span class="sxs-lookup"><span data-stu-id="496a8-178">To work around this issue:</span></span>

1. <span data-ttu-id="496a8-179">Visual Studio çıkış</span><span class="sxs-lookup"><span data-stu-id="496a8-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="496a8-180">(Bu, makinenize farklı bir sürücüde olabilir) şu klasörü açın</span><span class="sxs-lookup"><span data-stu-id="496a8-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="496a8-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span><span class="sxs-lookup"><span data-stu-id="496a8-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="496a8-182">Tüm dosyaları Sil *.deleteme* uzantıları.</span><span class="sxs-lookup"><span data-stu-id="496a8-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="496a8-183">Visual Studio'da yeniden açın</span><span class="sxs-lookup"><span data-stu-id="496a8-183">Re-open Visual Studio</span></span>

<span data-ttu-id="496a8-184">Bu adımları uyguladıktan sonra devam etmek mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="496a8-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="496a8-185">Nadiren de olsa, Kod Analizi açık ile derleme hatasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="496a8-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="496a8-186">Paket Yöneticisi konsolu ile FluentNHibernate yüklerse, aşağıdaki hatayı alıyorsunuz ve ardından "Kod analizini" açık projenizi derleyin.</span><span class="sxs-lookup"><span data-stu-id="496a8-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="496a8-187">Varsayılan olarak, NHibernate 3.0.0.2001 FluentNHibernate gerektirir.</span><span class="sxs-lookup"><span data-stu-id="496a8-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="496a8-188">Ancak, tasarımı gereği NuGet NHibernate 3.0.0.4000 projenizde yükleyecek ve çalışır böylece uygun bağlama yeniden yönlendirmeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="496a8-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="496a8-189">Kod Analizi açık değilse, proje düzgün derlenir.</span><span class="sxs-lookup"><span data-stu-id="496a8-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="496a8-190">Derleyicinin aksine, kod analizi aracı düzgün 3.0.0.4000 3.0.0.2001 yerine kullanılacak bağlama yeniden yönlendirmeleri izleyin değil.</span><span class="sxs-lookup"><span data-stu-id="496a8-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="496a8-191">Ya da yükleme NHibernate 3.0.0.2001 tarafından sorun gidermek veya derleyici aynı aşağıdakileri yaparak davranmaya kod analizi aracı bildirin:</span><span class="sxs-lookup"><span data-stu-id="496a8-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="496a8-192">Git *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analiz Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="496a8-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="496a8-193">FxCopCmd.exe.config açın ve `AssemblyReferenceResolveMode` gelen `StrongName` için `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="496a8-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="496a8-194">Değişikliği kaydetmek ve projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="496a8-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="496a8-195">Yazma hatası komutu install.ps1/uninstall.ps1/init.ps1 içinde çalışmaz</span><span class="sxs-lookup"><span data-stu-id="496a8-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="496a8-196">Bu bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="496a8-196">This is a known issue.</span></span> <span data-ttu-id="496a8-197">Write-Error çağırmak yerine, throw çağırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="496a8-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="496a8-198">Windows 2003'te kısıtlı erişimle NuGet yükleme Visual Studio çökebilir</span><span class="sxs-lookup"><span data-stu-id="496a8-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="496a8-199">Visual Studio Uzantı Yöneticisi'ni kullanarak ve bir yönetici olarak çalışmıyor NuGet yüklemeye çalışırken &#8220;Çalıştır&#8221; iletişim etiketli onay kutusu ile görüntülenir &#8220;kısıtlı erişime sahip bu programı çalıştır&#8221; tarafından denetlenen Varsayılan.</span><span class="sxs-lookup"><span data-stu-id="496a8-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Sınırlı iletişim kutusu olarak çalıştırma](./media/RunAsRestricted.png)

<span data-ttu-id="496a8-201">Tamam, iade ile tıklayarak Visual Studio kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="496a8-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="496a8-202">NuGet yüklemeden önce bu seçeneğin işaretini emin olun.</span><span class="sxs-lookup"><span data-stu-id="496a8-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="496a8-203">Windows Phone araçları için NuGet kaldırılamıyor</span><span class="sxs-lookup"><span data-stu-id="496a8-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="496a8-204">Windows Phone araçları desteği için Visual Studio Uzantı Yöneticisi yok.</span><span class="sxs-lookup"><span data-stu-id="496a8-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="496a8-205">NuGet kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="496a8-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="496a8-206">Paket geri yükleme keser NuGet paket kimlikleri büyük/küçük harf değiştirme</span><span class="sxs-lookup"><span data-stu-id="496a8-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="496a8-207">Üzerinde en length açıklandığı gibi [bu GitHub sorunu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), NuGet paketlerinin büyük/küçük harf değiştirme yapılabilir NuGet desteği ancak nedenleri zorluklar farklı harfleri, var olan kullanıcılar paketleri için paket geri yükleme sırasında kendi *genel paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="496a8-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="496a8-208">Mevcut kullanıcıları kendi derleme zamanı paket geri yükleme için oluşabilecek sonu hakkında paketinizin ile iletişim kurmak için bir yol varsa, yalnızca büyük/küçük bir değişiklik isteyen öneririz.</span><span class="sxs-lookup"><span data-stu-id="496a8-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="496a8-209">Raporlama konuları</span><span class="sxs-lookup"><span data-stu-id="496a8-209">Reporting issues</span></span>

<span data-ttu-id="496a8-210">NuGet sorunları bildirmek için ziyaret [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="496a8-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
