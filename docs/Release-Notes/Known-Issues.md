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
ms.openlocfilehash: ac00e3f11c54290a31319e7f2946fd965a0a9288
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="known-issues-with-nuget"></a>NuGet ile ilgili bilinen sorunlar

Sürekli olarak bildirilen en yaygın ile ilgili bilinen sorunların NuGet bunlar. NuGet yüklemeden veya paketlerini yönetme konusunda sorun yaşıyorsanız, lütfen bu bilinen sorunlar ve bunların çözümleri aracılığıyla göz atın.

> [!Note]
> NuGet 4.0 ile başlayarak, bilinen sorunlar ilgili sürüm notları, parçasıdır.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>NuGet ile kimlik doğrulaması sorunlarını nuget.exe v3.4.3 ile VSTS içinde akışları

**Sorun:**

Şu kimlik bilgilerini depolamak için aşağıdaki komutu kullandığınızda, çift kişisel erişim belirteci şifreleme yukarı sonlandırın.

$PAT "Kişisel erişim belirtecinizi" = $Feed kaynakları ekleyin-"URL'si,".\nuget.exe Test adına =-kaynak $Feed - UserName $UserName-parola $PAT

**Geçici çözüm:**

Depolama parolaları düz metin kullanarak [- StorePasswordInClearText](../tools/cli-ref-sources.md) seçeneği.

## <a name="error-installing-packages-with-nuget-34-341"></a>3.4.1 NuGet 3.4 ile paketler yüklenirken hata oluştu

**Sorun:**

NuGet 3.4 ve 3.4.1, NuGet eklenti kullanırken, herhangi bir kaynağa kullanılabilir olarak bildirilir ve yeni kaynakları yapılandırma penceresinde ekleyemiyor. Aşağıdaki görüntü sonucu benzer:

![Hiçbir kaynaklarıyla NuGet yapılandırma](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config` Dosyasını, `%AppData%\NuGet\` (Windows) veya `~/.nuget/` (Mac/Linux) klasör yanlışlıkla boşaltılır. Bu sorunu gidermek için: (Windows'da, eğer varsa) Visual Studio'yu kapatın, silme `NuGet.Config` dosya ve işlemi yeniden deneyin. NuGet oluşturulan yeni bir `NuGet.Config` ve devam etmek mümkün olması gerekir.

## <a name="error-installing-packages-with-nuget-27"></a>NuGet 2.7 ile paketler yüklenirken hata oluştu

**Sorun:**

NuGet 2.7 veya üzerini derleme başvuruları içeren herhangi bir paket yüklemeye çalıştığınızda hata iletisini alabilirsiniz **"giriş dizesi değildi doğru bir biçimde."** gibi altında:

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

Bu tür kitaplığının kaynaklanır `VSLangProj.dll` sisteminizde kaydedilmeyen COM bileşeni. Bu durum, örneğin, varsa iki Visual Studio sürümlerini yan yana ve yüklü sonra eski sürümü kaldırın. Bunun yapılması, yukarıdaki COM kitaplığı yanlışlıkla bir kaydı.

**Çözüm:**:

Bu komutu çalıştırmak bir **yükseltilmiş istemi** için tür kitaplığı yeniden kaydetmek için `VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Komut başarısız olursa, dosyanın bu konumda olup olmadığını denetleyin.

Bu hata hakkında daha fazla bilgi için bkz [iş öğesi](https://nuget.codeplex.com/workitem/3609 "iş öğesi 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Derleme hatasından sonra VS 2012'de paket güncelleştirmesi

Sorun: VS 2012 RTM kullanıyor. NuGet paket güncelleştirilirken bu ileti Al: "bir veya daha fazla paket tamamlanamadı kaldırıldı." ve Visual Studio yeniden başlatmanız istenir. VS yeniden başlattıktan sonra tuhaf derleme hataları alırsınız.

Eski paketler belirli dosyaları arka planda MSBuild işlem kilitlenen nedenidir. Hatta VS yeniden başlattıktan sonra arka plan MSBuild işlem yapı hatalarına neden eski paketlerdeki dosyalar devam eder.

Düzeltme VS 2012 güncelleştirmesi, örneğin VS 2012 güncelleştirme 2 yüklemektir.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>En son NuGet eski bir sürümden yükseltme bir imza doğrulama hatasına neden oluyor

VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken aşağıdaki hata iletisine çalıştırabilirsiniz.

![Visual Studio Uzantı Yükleyicisi](./media/Visual-Studio-Extension-Installer.png)

Günlükleri görüntülerken, Bahsetme görebileceğiniz bir `SignatureMismatchException`.

Bu, var olmaması için bir [Visual Studio 2010 SP1 Düzeltmesi](http://bit.ly/vsixcertfix) yükleyebilirsiniz.
Alternatif olarak, yalnızca NuGet (yönetici olarak Visual Studio çalıştırılırken) kaldırıp VS uzantısı Galeriden yükleme geçici bir çözüm değildir.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Reflector Visual Studio eklentisi ayrıca yüklendiğinde, Paket Yöneticisi konsolu bir özel durum oluşturur.

Reflector VS yüklü eklenti varsa Paket Yöneticisi konsolu çalışırken, aşağıdaki özel durum iletisi çalışabilir.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

veya

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

Şu eklenti bir çözüm çalışma büyük yazarı temas.

<p class="info">Güncelleştirme: Reflector, 6.5, en son sürümünü konsolda artık bu özel durumun neden doğrulanmıştır.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Açılış Paket Yöneticisi konsolu ObjectSecurity özel durum ile başarısız oluyor

Paket Yöneticisi konsolu açmaya çalışırken bu hatalar görebilirsiniz:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Bu durumda, çözümü uygulayın [üzerinde StackOverflow ele alınan](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) bunları düzeltmek için.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Çözüm InstallShield Limited Edition proje içeriyorsa, paket Kitaplığı Başvurusu Ekle iletişim kutusu bir özel durum oluşturur.

Çözümünüzü bir veya daha fazla InstallShield Limited Edition proje içeriyorsa, belirledik, **paketi Kitaplığı Başvurusu Ekle** iletişim kutusu açıldığında bir özel durum oluşturur. Şu anda henüz InstallShield projeleri kaldırma veya bunları kaldırma dışında geçici çözüm yoktur.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Düğmesi gri çıkışı kaldırabilir? NuGet yükleme/kaldırma için yönetici ayrıcalıkları gerektirmez

NuGet aracılığıyla Visual Studio Uzantı Yöneticisi kaldırmayı denerseniz, Kaldır düğmesini devre dışı olduğunu fark edebilirsiniz. NuGet yüklemek ve kaldırmak için yönetici erişimi gerektirir. Visual Studio uzantısı kaldırmak için yönetici yeniden başlatın. NuGet kullanmak için yönetici erişimi gerektirmez.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Windows XP'de açtığınızda, Paket Yöneticisi konsolu çöker. Ne oldu?

NuGet Powershell 2.0 çalışma zamanını gerektirir. Windows XP, varsayılan olarak, Powershell 2.0 sahip değil. Powershell 2.0 çalışma zamanını şuradan indirebilirsiniz [ http://support.microsoft.com/kb/968929 ](http://support.microsoft.com/kb/968929). Yükledikten sonra Visual Studio'yu yeniden başlatın ve Paket Yöneticisi konsolu yapabiliyor olmanız gerekir.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Paket Yöneticisi konsolu açıksa, visual Studio 2010 SP1 Beta Çıkışta çöküyor.

Visual Studio 2010 SP1 Beta yüklediyseniz, Paket Yöneticisi konsolunu açık bırakın ve Visual Studio'yu kapatın, onu kilitleniyor fark edebilirsiniz. Bu, Visual Studio'nun bilinen bir sorundur ve SP1 RTM sabit serbest bırakın. Şimdilik, kilitlenme Yoksay veya yapabiliyorsanız SP1 Beta kaldırın.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>'Meta verileri'... öğesi geçersiz alt öğesi özel durumu olan oluşur

NuGet bir yayım öncesi sürümü ile oluşturulan paketler yüklediyseniz, "ad alanında 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' ' meta verileri' öğesi, geçersiz alt öğesi var" bildiren bir hata iletisi karşılaşabileceğiniz RTM çalışırken Bu proje ile olan NuGet sürümü. Kaldırmanız ve NuGet'in RTM sürümünü kullanan her bir paketi yeniden yüklemeniz gerekir.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Yükleme veya "Bu dosya zaten varken bir dosya oluşturamıyor." hatası sonuçlarında kaldırma girişimi

Herhangi bir nedenle burada VSIX uzantısı kaldırıldı, ancak bazı dosyalar geride tuhaf durumda Visual Studio uzantıları elde edebilirsiniz. Bu soruna geçici bir çözüm bulmak için:

1. Exit Visual Studio
1. (Bu, makinenize farklı bir sürücüde olabilir) şu klasörü açın

    C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. İle tüm dosyaları silin *.deleteme* uzantıları.
1. Visual Studio'da yeniden açın

Bu adımları uyguladıktan sonra devam etmek mümkün olması gerekir.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Nadir durumlarda açık Kod Analizi ile derleme hataya neden olur.

Paket Yöneticisi konsolu ile FluentNHibernate yüklerse aşağıdaki hatayı alıyorsunuz ve açık "Kod Analizi" ile projenizi derleme.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Varsayılan olarak, FluentNHibernate NHibernate 3.0.0.2001 gerektirir. Ancak, tasarım gereği NuGet NHibernate 3.0.0.4000 projenizde yükleyecek ve böylece çalışır uygun bağlama yeniden yönlendirmelerini ekleyin. Kod çözümleme açık değilse, proje düzgün derlenir. Derleyici aksine kod analizi aracı düzgün 3.0.0.4000 yerine 3.0.0.2001 kullanmak için bağlama yeniden yönlendirmeleri izleyin değil. Ya da yükleme NHibernate 3.0.0.2001 sorundan geçici çözüm ya da derleyici aynı aşağıdakileri yaparak davranmasına kod analizi aracı söyleyin:

1. Git *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static analiz Tools\FxCop*
1. FxCopCmd.exe.config açın ve değiştirme `AssemblyReferenceResolveMode` gelen `StrongName` için `StrongNameIgnoringVersion`.
1. Değişikliği kaydetmek ve projenizi yeniden derleyin.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Yazma hatası komutu install.ps1/uninstall.ps1/init.ps1 içinde çalışmıyor

Bu bilinen bir sorundur. Write-Error çağırmak yerine, throw çağırmayı deneyin.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Windows 2003'te kısıtlı erişime sahip NuGet yükleme Visual Studio çökebilir

Visual Studio Uzantı Yöneticisi'ni kullanarak ve bir yönetici olarak çalışmıyor NuGet yüklemeye çalışırken &#8220;Çalıştır&#8221; iletişim etiketli onay kutusu ile görüntülenen &#8220;kısıtlı erişime sahip bu programı çalıştır&#8221; tarafından iade Varsayılan.

![Sınırlı iletişim kutusu olarak çalıştırma](./media/RunAsRestricted.png)

İşaretli değilse, ile Tamam'a tıkladığınızda Visual Studio kilitleniyor. NuGet'ı yüklemeden önce bu seçeneğin işaretini kaldırdığınızdan emin olun.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Windows Phone araçları NuGet kaldıramadı.

Windows Phone araçları Visual Studio uzantısı Yöneticisi için destek yok. NuGet kaldırmak için aşağıdaki komutu çalıştırın.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>Paket geri yüklemesi keser NuGet paket kimliği, büyük/küçük harf değiştirme

Üzerinde en length anlatıldığı gibi [bu GitHub sorunu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), NuGet paketleri, büyük/küçük harf değiştirme yapılabilir NuGet destek ancak nedenler zorluklar farklı-ortası, var olan kullanıcılar paketler için paket geri yüklemesi sırasında kendi yerel paket önbelleği. Varolan kullanıcılar, derleme zamanı paket geri yüklemesi oluşabilir sonu hakkında paketinin ile iletişim kurmak için bir yol olduğunda yalnızca büyük/küçük harf değiştirme isteyen öneririz.

## <a name="reporting-issues"></a>Raporlama konuları

NuGet sorunları bildirmek için ziyaret [ https://github.com/nuget/home/issues ](https://github.com/nuget/home/issues).
