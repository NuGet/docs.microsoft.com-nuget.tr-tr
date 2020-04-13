---
title: Bilinen Sorunlar
description: Kimlik doğrulama, paket yükleme ve araçlar da dahil olmak üzere NuGet ile bilinen sorunlar.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8f2b33a7290301bd16db3b1979ae496eee602f55
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "75383664"
---
# <a name="known-issues-with-nuget"></a>NuGet ile Bilinen Sorunlar

Bunlar, NuGet ile bilinen ve sürekli olarak bildirilen en yaygın sorunlardır. NuGet'i yüklerken veya paketleri yönetmekte sorun yaşıyorsanız, lütfen bu bilinen sorunlara ve çözümlerine bir göz atın.

> [!Note]
> NuGet 4.0 ile başlayarak, bilinen sorunlar ilgili sürüm notlarının bir parçasıdır.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Nuget beslemeleri ile nuget.exe v3.4.3 ile VSTS kimlik doğrulama sorunları

**Sorun:**

Kimlik bilgilerini depolamak için aşağıdaki komutu kullandığımızda, Kişisel Erişim Belirteci'ni çift şifreleriz.

$PAT = "Kişisel erişim belirteç" $Feed = "Url"niz .\nuget.exe kaynakları ekle -İsim Testi -Kaynak $Feed -Kullanıcı Adı $UserName -Şifre $PAT

**Geçici çözüm:**

[-StorePasswordInClearText](../reference/cli-reference/cli-ref-sources.md) seçeneğini kullanarak parolaları açık metin olarak saklayın.

## <a name="error-installing-packages-with-nuget-34-341"></a>NuGet 3.4, 3.4.1 ile hata yükleme paketleri

**Sorun:**

NuGet 3.4 ve 3.4.1'de, NuGet eklentisini kullanırken, kullanılabilir kaynak bildirilmemiştir ve yapılandırma penceresine yeni kaynaklar ekleyemiyorsunuz. Sonuç aşağıdaki resme benzer:

![Hiçbir kaynak ile NuGet config](./media/knownIssue-34-NoSources.PNG)

(Windows) `NuGet.Config` `%AppData%\NuGet\` veya `~/.nuget/` (Mac/Linux) klasörünüzdeki dosya yanlışlıkla boşaltıldı. Bunu düzeltmek için: Visual Studio'yu kapatın (varsa Windows'da), dosyayı `NuGet.Config` silin ve işlemi yeniden deneyin. NuGet yeni `NuGet.Config` bir yeni oluşturdu ve devam edebilmeniz gerekir.

## <a name="error-installing-packages-with-nuget-27"></a>NuGet 2.7 ile hata yükleme paketleri

**Sorun:**

NuGet 2.7 veya üzeri, montaj başvuruları içeren herhangi bir paket yüklemeye çalıştığınızda, hata iletisi alabilirsiniz **"Giriş dize doğru bir biçimde değildi."**, aşağıdaki gibi:

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

Bunun nedeni, COM bileşeninin `VSLangProj.dll` sisteminizde kaydedilmemiş olması için tür kitaplığından kaynaklanır. Bu, örneğin, Visual Studio'nun yan yana yüklenmiş iki sürümü varsa ve daha sonra eski sürümü kaldırdığınızda gerçekleşebilir. Bunu yapmak, yanlışlıkla yukarıdaki COM kitaplığının kaydını açabilir.

**Çözüm:**:

Tür kitaplığını yeniden kaydetmek için bu komutu yükseltilmiş bir **komut isteminden** çalıştırın`VSLangProj.dll`

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Komut başarısız olursa, dosyanın o konumda bulunıp var olmadığını denetleyin.

Bu hata hakkında daha fazla bilgi için bu [çalışma öğesine](https://nuget.codeplex.com/workitem/3609 "İş öğesi 3609")bakın.

## <a name="build-failure-after-package-update-in-vs-2012"></a>VS 2012'de paket güncelleştirmesi sonrası hata oluşturma

Sorun: VS 2012 RTM kullanıyorsunuz. NuGet paketlerini güncellerken şu mesajı alırsınız: "Bir veya daha fazla paket kaldırılamadı." ve Visual Studio'yı yeniden başlatmanız istenir. VS yeniden başlattıktan sonra, garip yapı hataları olsun.

Bunun nedeni, eski paketlerdeki bazı dosyaların arka plandaki MSBuild işlemi tarafından kilitlenmiş olmasıdır. VS yeniden başlattıktan sonra bile, arka plan MSBuild işlemi hala eski paketlerdeki dosyaları kullanır ve yapı hatalarına neden olur.

Düzeltme VS 2012 Güncelleme, örneğin VS 2012 Güncelleme 2 yüklemektir.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Eski bir sürümden en son NuGet'e yükseltme imza doğrulama hatasına neden olur

VS 2010 SP1 çalıştırıyorsanız, eski bir sürümünüz yüklüyse NuGet'i yükseltmeye çalışırken aşağıdaki hata iletisine rastlaabilirsiniz.

![Visual Studio Uzantılı Yükleyici](./media/Visual-Studio-Extension-Installer.png)

Günlükleri görüntülerken, bir `SignatureMismatchException`.

Bunun oluşmasını önlemek için yükleyebileceğiniz bir [Visual Studio 2010 SP1 düzeltmesi](http://bit.ly/vsixcertfix) vardır.
Alternatif olarak, geçici çözüm sadece NuGet kaldırmak (Yönetici olarak Visual Studio çalıştırırken) ve sonra VS Uzantı Galerisi'nden yüklemektir. Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Package Manager Console, Reflektör Visual Studio Eklentisi de yüklendiğinde bir özel durum oluşturur.

Paket Yöneticisi konsolu çalıştırırken, Reflektör VS Eklentisi yüklüyse aşağıdaki özel durum iletisine rastlayabilirsiniz.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

or

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

Biz bir çözüm üzerinde çalışma umuduyla eklenti nin yazarı ile temasa geçtik.

<p class="info">Güncelleme: Reflektör, 6.5 en son sürümü, artık konsolda bu özel durum neden olduğunu doğruladı.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Açılış Package Manager Console ObjectSecurity özel durum ile başarısız olur

Paket Yöneticisi Konsolu'nu açmaya çalışırken aşağıdaki hataları görebilirsiniz:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

Bu durumda, bunları düzeltmek için [StackOverflow üzerinde tartışılan](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) çözümü izleyin.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Paket Kitaplığı Ekle Başvurusu iletişim kutusu, çözüm InstallShield Limited Edition Project içeriyorsa bir özel durum oluşturur

Çözümünüz bir veya daha fazla InstallShield Limited Edition projesi içeriyorsa, **Paket Kitaplığı Başvuru Ekle** iletişim kutusunun açıldığında bir özel durum sunacağını belirledik. InstallShield projelerini kaldırmak veya boşaltmak dışında henüz geçici bir çözüm bulunmamaktadır.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Düğmeyi Kaldır Solukmu? NuGet Yüklemek/Kaldırmak Için Yönetici Ayrıcalıkları Gerektirir

Visual Studio Extension Manager aracılığıyla NuGet'i kaldırmayı denerseniz, Kaldır düğmesinin devre dışı bırakıldığını fark edebilirsiniz. NuGet yüklemek ve kaldırmak için yönetici erişimi gerektirir. Uzantıyı kaldırmak için Visual Studio'yu yönetici olarak yeniden başlatın. NuGet kullanmak için yönetici erişimi gerektirmez.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Windows XP'de açtığımda Package Manager Console çöküyor. Ne oldu?

NuGet Powershell 2.0 çalışma süresi gerektirir. Windows XP, varsayılan olarak Powershell 2.0'a sahip değildir. Powershell 2.0 çalışma süresini .'den <https://support.microsoft.com/kb/968929>indirebilirsiniz. Yükledikten sonra Visual Studio'yı yeniden başlatın ve Package Manager Console'u açabilirsiniz.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Visual Studio 2010 SP1 Beta, Package Manager Konsolu açıksa çıkışta çöküyor.

Visual Studio 2010 SP1 Beta yüklü varsa, Paket Yöneticisi Konsolu açık ve visual studio kapatın bırakırsanız, çökecek fark edebilirsiniz. Bu Visual Studio bilinen bir konudur ve SP1 RTM sürümünde sabit olacaktır. Şimdilik, sadece çökmesi göz ardı veya eğer yapabilirseniz SP1 Beta kaldırın.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Öğe 'meta veri' ... geçersiz alt öğe özel durum oluşur

NuGet'in ön sürüm sürümüyle oluşturulmuş paketleri yüklediyseniz, nuget'in RTM sürümünü bu projeyle çalıştırırken "ad alanında 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' öğesi 'meta veri' geçersiz alt öğeye sahiptir" belirten bir hata iletisi ile karşılaşabilirsiniz. NuGet'in RTM sürümünü kullanarak her paketi kaldırmanız ve sonra yeniden yüklemeniz gerekir.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>Yüklemeye veya kaldırmaya çalışmak , "Bu dosya zaten varken dosya oluşturamaz" hatasıyla sonuçlanır.

Nedense, Visual Studio uzantıları VSIX uzantısını kaldırdığınız garip bir durumda olabilir, ancak bazı dosyalar geride kaldı. Bu soruna geçici bir çözüm olarak:

1. Çıkış Görsel Stüdyosu
1. Aşağıdaki klasörü açın (makinenizde farklı bir sürücüde olabilir)

    C:\Program Dosyaları (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft\<Corporation\NuGet Package Manager sürümü>\

1. *.deleteme* uzantıları ile tüm dosyaları silin.
1. Visual Studio'yı yeniden açın

Bu adımları takip ettikten sonra, devam edebilmeniz gerekir.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Nadir durumlarda, Kod Analizi ile derleme hataya neden olur.

Paket Yöneticisi konsolu ile FluentNHibernate yükler ve daha sonra "Kod Analizi" açık olan projenizi derlemek aşağıdaki hata alabilirsiniz.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Varsayılan olarak, FluentNHibernate NHibernate 3.0.0.2001 gerektirir. Ancak, tasarım nuGet projenizde NHibernate 3.0.0.4000 yükler ve çalışacak şekilde uygun bağlama yönlendirmeleri ekleyin. Kod çözümlemesi açık değilse, proje niz gayet iyi derlenir. Derleyicinin aksine, kod çözümleme aracı 3.0.0.2001 yerine 3.0.0.4000 kullanmak için bağlayıcı yönlendirmeleri düzgün bir şekilde izlemez. NHibernate 3.0.0.2001'i yükleyerek sorunu çözebilir veya kod çözümleme aracına aşağıdakileri yaparak derleyiciyle aynı şekilde çalışmasını söyleyebilirsiniz:

1. *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop* adresine gidin
1. Açık FxCopCmd.exe.config `AssemblyReferenceResolveMode` ve `StrongName` `StrongNameIgnoringVersion`değiştirmek .
1. Değişikliği kaydedin ve projenizi yeniden oluşturun.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Write-Error komutu install.ps1/uninstall.ps1/init.ps1 içinde çalışmıyor

Bu bilinen bir sorundur. Yazma-Hata'yı aramak yerine throw'u aramayı deneyin.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Windows 2003'te kısıtlı erişimle NuGet'i yüklemek Visual Studio'nun çökmesine neden olabilir

Visual Studio Extension Manager'ı kullanarak NuGet'i yüklemeye çalışırken ve yönetici olarak çalışmayan &#8220;Run&#8221; As iletişim kutusu, bu programı varsayılan olarak&#8221; denetleyerek çalıştır'&#8220;etiketli onay kutusuyla görüntülenir.

![Sınırlı İletişim Kutusu Olarak Çalıştır](./media/RunAsRestricted.png)

Bu kontrol ile Tamam'ı tıklatarak Visual Studio çöküyor. NuGet'i yüklemeden önce bu seçeneğin işaretlerini geri aldığından emin olun.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Windows Phone Araçları için NuGet'i kaldıramıyor

Windows Phone Tools'un Visual Studio Extension Manager desteği yoktur. NuGet'i kaldırmak için aşağıdaki komutu çalıştırın.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>NuGet paket iD'lerinin büyük harfdeğiştirme paketi geri yüklemesi tatili

[Bu GitHub sorunu](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)üzerinde uzun uzadıya tartışıldığı gibi, NuGet paketlerinin büyük harf değiştirme NuGet desteği ile yapılabilir, ancak mevcut kullanıcılar için paket geri yükleme sırasında komplikasyonlara neden olur, farklı-cased, küresel *paketler* klasöründe paketleri. Yalnızca paketinizin varolan kullanıcılarıyla oluşturma zamanı paketi geri yüklemesi nedeniyle oluşabilecek mola hakkında iletişim kurmanız için bir yol olduğunda bir servis talebi değişikliği isteğinde bulunmanızı öneririz.

## <a name="reporting-issues"></a>Raporlama sorunları

NuGet sorunlarını bildirmek [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues)için.
