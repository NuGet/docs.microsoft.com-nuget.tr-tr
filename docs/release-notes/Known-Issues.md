---
title: Bilinen Sorunlar
description: NuGet ile kimlik doğrulama, paket yükleme ve araçlar gibi bilinen sorunlar.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383664"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="5ae6b-103">NuGet ile ilgili bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="5ae6b-103">Known Issues with NuGet</span></span>

<span data-ttu-id="5ae6b-104">Bunlar, sürekli olarak bildirilen NuGet ile ilgili en yaygın sorunlardır.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="5ae6b-105">NuGet veya paketleri yönetirken sorun yaşıyorsanız lütfen bu bilinen sorunlara ve bunların çözünürlüklerine göz atın.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="5ae6b-106">NuGet 4,0 ' den başlayarak, bilinen sorunlar ilgili sürüm notlarının bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="5ae6b-107">NuGet. exe v 3.4.3 ile VSTS 'de NuGet akışlarıyla ilgili kimlik doğrulama sorunları</span><span class="sxs-lookup"><span data-stu-id="5ae6b-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="5ae6b-108">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="5ae6b-108">**Problem:**</span></span>

<span data-ttu-id="5ae6b-109">Kimlik bilgilerini depolamak için aşağıdaki komutu kullandığımızda, kişisel erişim belirtecini iki kez şifreliyoruz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="5ae6b-110">$PAT = "kişisel erişim belirteciniz" $Feed = "URL 'Niz" .\nuget.exe Sources add-name test-source $Feed-kullanıcıadı $UserName-Password $PAT</span><span class="sxs-lookup"><span data-stu-id="5ae6b-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="5ae6b-111">**Geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="5ae6b-111">**Workaround:**</span></span>

<span data-ttu-id="5ae6b-112">Parolaları [-storepasswordincleartext](../reference/cli-reference/cli-ref-sources.md) seçeneğini kullanarak şifresiz metin olarak depolayın.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-112">Store passwords in clear text using the [-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="5ae6b-113">NuGet 3,4 ile paket yükleme hatası, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="5ae6b-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="5ae6b-114">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="5ae6b-114">**Problem:**</span></span>

<span data-ttu-id="5ae6b-115">NuGet 3,4 ve 3.4.1 ' de, NuGet eklentisini kullanırken kullanılabilir olarak hiçbir kaynak bildirilmemiştir ve yapılandırma penceresinde yeni kaynaklar ekleyememiştir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="5ae6b-116">Sonuç aşağıdaki görüntüyle benzerdir:</span><span class="sxs-lookup"><span data-stu-id="5ae6b-116">The result is similar to the image below:</span></span>

![Kaynak içermeyen NuGet yapılandırması](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="5ae6b-118">`%AppData%\NuGet\` (Windows) veya `~/.nuget/` (Mac/Linux) klasörünüzdeki `NuGet.Config` dosyası yanlışlıkla boşaltılır.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="5ae6b-119">Bu hatayı onarmak için: Visual Studio 'Yu kapatın (varsa Windows üzerinde) `NuGet.Config` dosyasını silip işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="5ae6b-120">NuGet yeni bir `NuGet.Config` üretti ve devam edebilmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="5ae6b-121">NuGet 2,7 ile paket yükleme hatası</span><span class="sxs-lookup"><span data-stu-id="5ae6b-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="5ae6b-122">**Sorun:**</span><span class="sxs-lookup"><span data-stu-id="5ae6b-122">**Problem:**</span></span>

<span data-ttu-id="5ae6b-123">NuGet 2,7 veya üzeri sürümlerde, derleme başvurularını içeren herhangi bir paketi yüklemeye çalıştığınızda **"giriş dizesi doğru biçimde değildi."** hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5ae6b-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

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

<span data-ttu-id="5ae6b-124">Bunun nedeni, sisteminizde kaydı yapılan `VSLangProj.dll` COM bileşeninin tür kitaplığından oluşur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="5ae6b-125">Bu durum, örneğin Visual Studio 'nun iki sürümünün yan yana yüklenip daha sonra eski sürümü kaldırabilmeniz gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="5ae6b-126">Bunun yapılması, yukarıdaki COM kitaplığının yanlışlıkla kaydını silmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="5ae6b-127">**Çözüm:** :</span><span class="sxs-lookup"><span data-stu-id="5ae6b-127">**Solution:**:</span></span>

<span data-ttu-id="5ae6b-128">`VSLangProj.dll` için tür kitaplığını yeniden kaydetmek üzere yükseltilmiş bir komut **isteminden** bu komutu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5ae6b-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="5ae6b-129">Komut başarısız olursa, dosyanın bu konumda bulunup bulunmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="5ae6b-130">Bu hata hakkında daha fazla bilgi için bu [iş öğesine](https://nuget.codeplex.com/workitem/3609 "İş öğesi 3609")bakın.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="5ae6b-131">VS 2012 ' deki paket güncelleştirmesinden sonra derleme hatası</span><span class="sxs-lookup"><span data-stu-id="5ae6b-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="5ae6b-132">Sorun: VS 2012 RTM kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="5ae6b-133">NuGet paketleri güncelleştirilirken şu iletiyi alırsınız: "bir veya daha fazla paketin kaldırılması tamamlanamadı."</span><span class="sxs-lookup"><span data-stu-id="5ae6b-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="5ae6b-134">Visual Studio 'Yu yeniden başlatmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="5ae6b-135">VS yeniden başlatıldıktan sonra, tuhaf derleme hataları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="5ae6b-136">Nedeni, eski paketlerdeki belirli dosyaların bir arka plan MSBuild işlemi tarafından kilitlenip kilitlenmemesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="5ae6b-137">VS yeniden başlatmasından sonra bile, arka plan MSBuild işlemi hala eski paketlerdeki dosyaları kullanır ve bu da derleme hatalarının görüntülenmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="5ae6b-138">Bu çözüm, vs 2012 güncelleştirme 2 gibi VS 2012 güncelleştirme 'yi yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="5ae6b-139">Eski bir sürümden en son NuGet 'e yükseltmek imza doğrulama hatasına neden olur</span><span class="sxs-lookup"><span data-stu-id="5ae6b-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="5ae6b-140">VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken aşağıdaki hata iletisini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Visual Studio Uzantı Yükleyicisi](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="5ae6b-142">Günlükleri görüntülerken, bir `SignatureMismatchException`bahsetmeyi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="5ae6b-143">Bunun oluşmasını önlemek için, yükleyebileceğiniz bir [Visual Studio 2010 SP1 düzeltmesi](http://bit.ly/vsixcertfix) vardır.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="5ae6b-144">Alternatif olarak, geçici çözüm NuGet 'i (Visual Studio 'Yu yönetici olarak çalıştırırken) kaldırmak ve sonra VS uzantısı galerisinden yüklemek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span> <span data-ttu-id="5ae6b-145">Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-145">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="5ae6b-146">Bir yansıtıcı Visual Studio eklentisi de yüklendiğinde Paket Yöneticisi konsolu bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="5ae6b-147">Paket Yöneticisi konsolunu çalıştırırken, bir yansıtıcı VS eklentisi yüklüyse aşağıdaki özel durum iletisiyle karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="5ae6b-148">veya</span><span class="sxs-lookup"><span data-stu-id="5ae6b-148">or</span></span>

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

<span data-ttu-id="5ae6b-149">Bir çözüm çalıştırma konusunda eklentinin yazarı ile iletişim kurduk.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="5ae6b-150">Güncelleştirme: en son Yansıtıcıyı, 6,5, artık konsolda bu özel duruma neden olduğunu doğrulıyoruz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="5ae6b-151">Paket Yöneticisi konsolu açılamadı ObjectSecurity özel durumuyla başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="5ae6b-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="5ae6b-152">Paket Yöneticisi konsolunu açmaya çalışırken şu hatalarla karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5ae6b-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="5ae6b-153">Varsa, bunları onarmak için [StackOverflow sayfasında ele alınan](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) çözümü izleyin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="5ae6b-154">Çözüm InstallShield Limited Edition projesi içeriyorsa paket kitaplığı başvurusu Ekle iletişim kutusu bir özel durum oluşturur</span><span class="sxs-lookup"><span data-stu-id="5ae6b-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="5ae6b-155">Çözümünüz bir veya daha fazla InstallShield Limited Edition projesi içeriyorsa, **paket kitaplığı başvurusu Ekle** iletişim kutusu açıldığında bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="5ae6b-156">Şimdilik InstallShield projelerini kaldırmadıysanız veya onları kaldırarak geçici çözüm yoktur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="5ae6b-157">Kaldırma düğmesi gri değil mi?</span><span class="sxs-lookup"><span data-stu-id="5ae6b-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="5ae6b-158">NuGet, yükleme/kaldırma için yönetici ayrıcalıkları gerektirir</span><span class="sxs-lookup"><span data-stu-id="5ae6b-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="5ae6b-159">NuGet 'i Visual Studio Uzantı Yöneticisi aracılığıyla kaldırmaya çalışırsanız, Kaldır düğmesinin devre dışı olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="5ae6b-160">NuGet, yükleme ve kaldırma için yönetici erişimi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="5ae6b-161">Uzantıyı kaldırmak için Visual Studio 'Yu yönetici olarak yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="5ae6b-162">NuGet, kullanmak için yönetici erişimi gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="5ae6b-163">Paket Yöneticisi konsolu, Windows XP 'de açtığımda kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="5ae6b-164">Ne oldu?</span><span class="sxs-lookup"><span data-stu-id="5ae6b-164">What's wrong?</span></span>

<span data-ttu-id="5ae6b-165">NuGet, PowerShell 2,0 çalışma zamanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="5ae6b-166">Windows XP 'de varsayılan olarak PowerShell 2,0 yoktur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="5ae6b-167">PowerShell 2,0 çalışma zamanını <https://support.microsoft.com/kb/968929>adresinden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-167">You can download the Powershell 2.0 runtime from <https://support.microsoft.com/kb/968929>.</span></span> <span data-ttu-id="5ae6b-168">Yükledikten sonra, Visual Studio 'Yu yeniden başlatın ve Paket Yöneticisi konsolu 'Nu açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="5ae6b-169">Paket Yöneticisi konsolu açıksa, çıkışta Visual Studio 2010 SP1 Beta kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="5ae6b-170">Visual Studio 2010 SP1 Beta sürümünü yüklediyseniz, Paket Yöneticisi konsolu 'Nu açık bırakıp Visual Studio 'Yu kapattıktan sonra kilitlendiğini fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="5ae6b-171">Bu, Visual Studio 'nun bilinen bir sorunudur ve SP1 RTM sürümünde düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="5ae6b-172">Şimdilik, daha sonra kilitlenmeyi yoksayın veya SP1 Beta sürümünü kaldırmanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="5ae6b-173">' Metadata ' öğesi... Geçersiz alt öğe özel durumu oluşuyor</span><span class="sxs-lookup"><span data-stu-id="5ae6b-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="5ae6b-174">NuGet 'in yayın öncesi sürümü ile oluşturulmuş paketler yüklediyseniz, bu projeyle birlikte NuGet 'in RTM sürümünü çalıştırırken ' schemas.microsoft.com/packaging/2010/07/nuspec.xsd ' ad alanındaki ' Metadata ' öğesinin geçersiz bir alt öğesi olduğunu belirten bir hata iletisiyle karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="5ae6b-175">NuGet 'in RTM sürümünü kullanarak her paketi kaldırmanız ve yeniden yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="5ae6b-176">"Bu dosya zaten mevcut olduğunda bir dosya oluşturulamıyor" hatası nedeniyle sonuçlar yüklenmeye veya kaldırılmaya çalışılıyor.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="5ae6b-177">Bazı nedenlerle, Visual Studio uzantıları VSıX uzantısını kaldırdığınız bir tuhaf durumunda alabilir, ancak bazı dosyalar arkasında bırakılır.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="5ae6b-178">Bu soruna geçici bir çözüm bulmak için:</span><span class="sxs-lookup"><span data-stu-id="5ae6b-178">To work around this issue:</span></span>

1. <span data-ttu-id="5ae6b-179">Visual Studio 'dan çık</span><span class="sxs-lookup"><span data-stu-id="5ae6b-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="5ae6b-180">Aşağıdaki klasörü açın (makinenizde farklı bir sürücüde olabilir)</span><span class="sxs-lookup"><span data-stu-id="5ae6b-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="5ae6b-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span><span class="sxs-lookup"><span data-stu-id="5ae6b-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version></span></span>\

1. <span data-ttu-id="5ae6b-182">*. Deleteme* uzantılarına sahip tüm dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="5ae6b-183">Visual Studio 'Yu yeniden açın</span><span class="sxs-lookup"><span data-stu-id="5ae6b-183">Re-open Visual Studio</span></span>

<span data-ttu-id="5ae6b-184">Bu adımları tamamladıktan sonra devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="5ae6b-185">Nadir durumlarda, kod analizi açık olarak derlenirken derleme hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="5ae6b-186">Paket Yöneticisi konsolu ile Floentnhazırda bekleme 'i yüklerse ve sonra projenizi "kod analizi" açık olarak derlerseniz aşağıdaki hatayı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="5ae6b-187">Varsayılan olarak, Floentnhazırda beklet Nhazırda beklet 3.0.0.2001 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="5ae6b-188">Ancak, Design NuGet tarafından projenize Nhazırda bekleme 3.0.0.4000 yüklenir ve uygun bağlama yeniden yönlendirmeleri çalışacak şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="5ae6b-189">Kod Analizi açık değilse, projeniz yalnızca daha iyi derlenir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="5ae6b-190">Derleyicinin aksine, Kod Analizi Aracı, 3.0.0.2001 yerine 3.0.0.4000 kullanmak için bağlama yeniden yönlendirmelerini doğru şekilde takip etmez.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="5ae6b-191">Bu sorunu geçici olarak çözmek için Nhazırda beklet 3.0.0.2001 veya kod analizi aracına, aşağıdakilerden birini yaparak derleyici ile aynı şekilde davranmasını söyleyin:</span><span class="sxs-lookup"><span data-stu-id="5ae6b-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="5ae6b-192">*%ProgramFiles%\Microsoft Visual Studio 10.0 \ Team Tools\Static Analysis Tools\FxCop* adresine gidin</span><span class="sxs-lookup"><span data-stu-id="5ae6b-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="5ae6b-193">FxCopCmd. exe. config dosyasını açın ve `StrongName` `StrongNameIgnoringVersion``AssemblyReferenceResolveMode` değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="5ae6b-194">Değişikliği kaydedin ve projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="5ae6b-195">Write-Error komutu Install. ps1/Uninstall. ps1/init. ps1 içinde çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="5ae6b-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="5ae6b-196">Bu bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-196">This is a known issue.</span></span> <span data-ttu-id="5ae6b-197">Write-Error çağırmak yerine throw çağrılmasını deneyin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="5ae6b-198">Windows 2003 ' de kısıtlı erişimle NuGet yükleme, Visual Studio 'Yu kilitleyebilir</span><span class="sxs-lookup"><span data-stu-id="5ae6b-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="5ae6b-199">Visual Studio Uzantı Yöneticisi 'Ni kullanarak NuGet yüklemeye çalışırken ve yönetici olarak &#8220;çalıştırılmadığından, farklı&#8221; Çalıştır iletişim kutusu, bu programı kısıtlı erişimle &#8220;&#8221; Çalıştır varsayılan olarak işaretlenen onay kutusuyla birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Kısıtlanmış olarak çalıştır Iletişim kutusu](./media/RunAsRestricted.png)

<span data-ttu-id="5ae6b-201">İşaretli bu çökme Visual Studio ile Tamam ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="5ae6b-202">NuGet 'i yüklemeden önce bu seçeneğin işaretini kaldırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="5ae6b-203">Windows Phone araçları için NuGet kaldırılamıyor</span><span class="sxs-lookup"><span data-stu-id="5ae6b-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="5ae6b-204">Windows Phone araçları, Visual Studio Uzantı Yöneticisi için desteğe sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="5ae6b-205">NuGet 'i kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="5ae6b-206">NuGet paket kimlikleri 'nin büyük/küçük harf durumunu değiştirme paket geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5ae6b-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="5ae6b-207">[Bu GitHub sorununun](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)uzunluğu konusunda anlatıldığı gibi, NuGet paketlerinin büyük/küçük harf durumunu değiştirmek NuGet desteği tarafından yapılabilir, ancak *genel paketler* klasöründe mevcut, farklı ve uyumlu paketlere sahip kullanıcılar için paket geri yükleme sırasında karmaşıklıklar oluşmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="5ae6b-208">Paketinizin, derleme zamanı paketi geri yükleme için oluşabilecek kesme hakkındaki mevcut kullanıcılarıyla iletişim kurmak için kullanabileceğiniz bir yönteme sahipseniz yalnızca bir örnek olarak değişiklik yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="5ae6b-209">Raporlama konuları</span><span class="sxs-lookup"><span data-stu-id="5ae6b-209">Reporting issues</span></span>

<span data-ttu-id="5ae6b-210">NuGet sorunlarını raporlamak için [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="5ae6b-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
