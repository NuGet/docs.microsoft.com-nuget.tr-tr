---
title: Bilinen Sorunlar
description: NuGet ile kimlik doğrulama, paket yükleme ve araçlar gibi bilinen sorunlar.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e6030670875192470fa47de84066281e45ac3eff
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777305"
---
# <a name="known-issues-with-nuget"></a>NuGet ile ilgili bilinen sorunlar

Bunlar, sürekli olarak bildirilen NuGet ile ilgili en yaygın sorunlardır. NuGet veya paketleri yönetirken sorun yaşıyorsanız lütfen bu bilinen sorunlara ve bunların çözünürlüklerine göz atın.

> [!Note]
> NuGet 4,0 ' den başlayarak, bilinen sorunlar ilgili sürüm notlarının bir parçasıdır.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>nuget.exe v 3.4.3 ile VSTS 'deki NuGet akışlarıyla kimlik doğrulama sorunları

**Sorun:**

Kimlik bilgilerini depolamak için aşağıdaki komutu kullandığımızda, kişisel erişim belirtecini iki kez şifreliyoruz.

$PAT = "kişisel erişim belirteciniz" $Feed = "URL 'Niz .\nuget.exe Sources ad Ekle test-kaynak $Feed-Kullanıcı adı $UserName-Parola $PAT

**Geçici çözüm:**

Parolaları [-storepasswordincleartext](../reference/cli-reference/cli-ref-sources.md) seçeneğini kullanarak şifresiz metin olarak depolayın.

## <a name="error-installing-packages-with-nuget-34-341"></a>NuGet 3,4 ile paket yükleme hatası, 3.4.1

**Sorun:**

NuGet 3,4 ve 3.4.1 ' de, NuGet eklentisini kullanırken kullanılabilir olarak hiçbir kaynak bildirilmemiştir ve yapılandırma penceresinde yeni kaynaklar ekleyememiştir. Sonuç aşağıdaki görüntüyle benzerdir:

![Kaynak içermeyen NuGet yapılandırması](./media/knownIssue-34-NoSources.PNG)

`NuGet.Config` `%AppData%\NuGet\` (Windows) veya `~/.nuget/` (Mac/Linux) klasörünüzdeki dosya yanlışlıkla boşaltılır. Bu hatayı onarmak için: Visual Studio 'Yu kapatın (varsa Windows üzerinde), dosyayı silin `NuGet.Config` ve işlemi yeniden deneyin. NuGet yeni bir oluşturmuş `NuGet.Config` ve devam edebilmelisiniz.

## <a name="error-installing-packages-with-nuget-27"></a>NuGet 2,7 ile paket yükleme hatası

**Sorun:**

NuGet 2,7 veya üzeri sürümlerde, derleme başvurularını içeren herhangi bir paketi yüklemeye çalıştığınızda **"giriş dizesi doğru biçimde değildi."** hata iletisini alabilirsiniz:

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

Bunun nedeni, `VSLangProj.dll` sisteminizde kaydı yapılan com bileşeninin tür kitaplığından oluşur. Bu durum, örneğin Visual Studio 'nun iki sürümünün yan yana yüklenip daha sonra eski sürümü kaldırabilmeniz gibi olabilir. Bunun yapılması, yukarıdaki COM kitaplığının yanlışlıkla kaydını silmiş olabilir.

**Çözüm:**:

Tür kitaplığını yeniden kaydetmek için bu komutu yükseltilmiş bir komut **isteminden** çalıştırın `VSLangProj.dll`

```
regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"
```

Komut başarısız olursa, dosyanın bu konumda bulunup bulunmadığını denetleyin.

Bu hata hakkında daha fazla bilgi için bu [iş öğesine](https://nuget.codeplex.com/workitem/3609 "İş öğesi 3609")bakın.

## <a name="build-failure-after-package-update-in-vs-2012"></a>VS 2012 ' deki paket güncelleştirmesinden sonra derleme hatası

Sorun: VS 2012 RTM kullanıyorsunuz. NuGet paketleri güncelleştirilirken şu iletiyi alırsınız: "bir veya daha fazla paketin kaldırılması tamamlanamadı." Visual Studio 'Yu yeniden başlatmanız istenir. VS yeniden başlatıldıktan sonra, tuhaf derleme hataları alırsınız.

Nedeni, eski paketlerdeki belirli dosyaların bir arka plan MSBuild işlemi tarafından kilitlenip kilitlenmemesine neden olur. VS yeniden başlatmasından sonra bile, arka plan MSBuild işlemi hala eski paketlerdeki dosyaları kullanır ve bu da derleme hatalarının görüntülenmesine neden olur.

Bu çözüm, vs 2012 güncelleştirme 2 gibi VS 2012 güncelleştirme 'yi yüklemektir.

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>Eski bir sürümden en son NuGet 'e yükseltmek imza doğrulama hatasına neden olur

VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken aşağıdaki hata iletisini kullanabilirsiniz.

![Visual Studio Uzantı Yükleyicisi](./media/Visual-Studio-Extension-Installer.png)

Günlükleri görüntülerken, bir öğesinin bahsettiğini görebilirsiniz `SignatureMismatchException` .

Bunun oluşmasını önlemek için, yükleyebileceğiniz bir [Visual Studio 2010 SP1 düzeltmesi](http://bit.ly/vsixcertfix) vardır.
Alternatif olarak, geçici çözüm NuGet 'i (Visual Studio 'Yu yönetici olarak çalıştırırken) kaldırmak ve sonra VS uzantısı galerisinden yüklemek olacaktır. Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>Yansıtıcısı Visual Studio Add-In de yüklendiğinde Paket Yöneticisi konsolu bir özel durum oluşturur.

Paket Yöneticisi konsolunu çalıştırırken, bir yansıtıcı VS eklentisi yüklüyse aşağıdaki özel durum iletisiyle karşılaşabilirsiniz.

```
The following error occurred while loading the extended type data file:
Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
Error in type "System.Security.AccessControl.ObjectSecurity":
Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
value of type "System.String" to type "System.Type".
System.Management.Automation.ActionPreferenceStopException:
Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
is set to Stop: Unable to find type
```

veya

```
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
```

Bir çözüm çalıştırma konusunda eklentinin yazarı ile iletişim kurduk.

<p class="info">Güncelleştirme: en son Yansıtıcıyı, 6,5, artık konsolda bu özel duruma neden olduğunu doğrulıyoruz.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Paket Yöneticisi konsolu açılamadı ObjectSecurity özel durumuyla başarısız oluyor

Paket Yöneticisi konsolunu açmaya çalışırken şu hatalarla karşılaşabilirsiniz:

```
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
```

Varsa, bunları onarmak için [StackOverflow sayfasında ele alınan](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) çözümü izleyin.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>Çözüm InstallShield Limited Edition projesi içeriyorsa paket kitaplığı başvurusu Ekle iletişim kutusu bir özel durum oluşturur

Çözümünüz bir veya daha fazla InstallShield Limited Edition projesi içeriyorsa, **paket kitaplığı başvurusu Ekle** iletişim kutusu açıldığında bir özel durum oluşturur. Şimdilik InstallShield projelerini kaldırmadıysanız veya onları kaldırarak geçici çözüm yoktur.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Kaldırma düğmesi gri değil mi? NuGet, yükleme/kaldırma için yönetici ayrıcalıkları gerektirir

NuGet 'i Visual Studio Uzantı Yöneticisi aracılığıyla kaldırmaya çalışırsanız, Kaldır düğmesinin devre dışı olduğunu fark edebilirsiniz. NuGet, yükleme ve kaldırma için yönetici erişimi gerektirir. Uzantıyı kaldırmak için Visual Studio 'Yu yönetici olarak yeniden başlatın. NuGet, kullanmak için yönetici erişimi gerektirmez.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Paket Yöneticisi konsolu, Windows XP 'de açtığımda kilitleniyor. Ne oldu?

NuGet, PowerShell 2,0 çalışma zamanı gerektirir. Windows XP 'de varsayılan olarak PowerShell 2,0 yoktur. PowerShell 2,0 çalışma zamanını konumundan indirebilirsiniz <https://support.microsoft.com/kb/968929> . Yükledikten sonra, Visual Studio 'Yu yeniden başlatın ve Paket Yöneticisi konsolu 'Nu açmanız gerekir.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Paket Yöneticisi konsolu açıksa, çıkışta Visual Studio 2010 SP1 Beta kilitleniyor.

Visual Studio 2010 SP1 Beta sürümünü yüklediyseniz, Paket Yöneticisi konsolu 'Nu açık bırakıp Visual Studio 'Yu kapattıktan sonra kilitlendiğini fark edebilirsiniz. Bu, Visual Studio 'nun bilinen bir sorunudur ve SP1 RTM sürümünde düzeltilecektir. Şimdilik, daha sonra kilitlenmeyi yoksayın veya SP1 Beta sürümünü kaldırmanız yeterlidir.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>' Metadata ' öğesi... Geçersiz alt öğe özel durumu oluşuyor

NuGet 'in yayın öncesi sürümü ile oluşturulmuş paketler yüklediyseniz, bu projeyle birlikte NuGet 'in RTM sürümünü çalıştırırken ' schemas.microsoft.com/packaging/2010/07/nuspec.xsd ' ad alanındaki ' Metadata ' öğesinin geçersiz bir alt öğesi olduğunu belirten bir hata iletisiyle karşılaşabilirsiniz. NuGet 'in RTM sürümünü kullanarak her paketi kaldırmanız ve yeniden yüklemeniz gerekir.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a>"Bu dosya zaten mevcut olduğunda bir dosya oluşturulamıyor" hatası nedeniyle sonuçlar yüklenmeye veya kaldırılmaya çalışılıyor.

Bazı nedenlerle, Visual Studio uzantıları VSıX uzantısını kaldırdığınız bir tuhaf durumunda alabilir, ancak bazı dosyalar arkasında bırakılır. Bu soruna geçici bir çözüm olarak:

1. Visual Studio 'dan çık
1. Aşağıdaki klasörü açın (makinenizde farklı bir sürücüde olabilir)

    C:\Program Files (x86) \Microsoft Visual Studio 10.0 \ Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\

1. *. Deleteme* uzantılarına sahip tüm dosyaları silin.
1. Visual Studio 'Yu yeniden açın

Bu adımları tamamladıktan sonra devam edebilirsiniz.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>Nadir durumlarda, kod analizi açık olarak derlenirken derleme hataya neden olur.

Paket Yöneticisi konsolu ile Floentnhazırda bekleme 'i yüklerse ve sonra projenizi "kod analizi" açık olarak derlerseniz aşağıdaki hatayı alabilirsiniz.

```
Error 3 CA0058 : The referenced assembly
'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
could not be found. This assembly is required for analysis and was referenced by:
C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
MyProject.UnitTests
```

Varsayılan olarak, Floentnhazırda beklet Nhazırda beklet 3.0.0.2001 gerektirir. Ancak, Design NuGet tarafından projenize Nhazırda bekleme 3.0.0.4000 yüklenir ve uygun bağlama yeniden yönlendirmeleri çalışacak şekilde ekleyin. Kod Analizi açık değilse, projeniz yalnızca daha iyi derlenir. Derleyicinin aksine, Kod Analizi Aracı, 3.0.0.2001 yerine 3.0.0.4000 kullanmak için bağlama yeniden yönlendirmelerini doğru şekilde takip etmez. Bu sorunu geçici olarak çözmek için Nhazırda beklet 3.0.0.2001 veya kod analizi aracına, aşağıdakilerden birini yaparak derleyici ile aynı şekilde davranmasını söyleyin:

1. *%ProgramFiles%\Microsoft Visual Studio 10.0 \ Team Tools\Static Analysis Tools\FxCop* adresine gidin
1. FxCopCmd.exe.config açın ve ' `AssemblyReferenceResolveMode` den ' `StrongName` ye geçin `StrongNameIgnoringVersion` .
1. Değişikliği kaydedin ve projenizi yeniden derleyin.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Write-Error komut install.ps1/uninstall.ps1/init.ps1 içinde çalışmıyor

Bu bilinen bir sorundur. Write-Error çağırmak yerine throw çağrılmasını deneyin.

```
throw "My error message"
```

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>Windows 2003 ' de kısıtlı erişimle NuGet yükleme, Visual Studio 'Yu kilitleyebilir

Visual Studio Uzantı Yöneticisi 'Ni kullanarak NuGet 'i yüklemeye çalışırken ve yönetici olarak çalıştırılmayan &#8220;farklı çalıştır&#8221; iletişim kutusu, &#8220;bu programı kısıtlı erişimle Çalıştır&#8221; varsayılan olarak işaretli olan onay kutusuyla birlikte görüntülenir.

![Kısıtlanmış olarak çalıştır Iletişim kutusu](./media/RunAsRestricted.png)

İşaretli bu çökme Visual Studio ile Tamam ' a tıklayın. NuGet 'i yüklemeden önce bu seçeneğin işaretini kaldırdığınızdan emin olun.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Windows Phone araçları için NuGet kaldırılamıyor

Windows Phone araçları, Visual Studio Uzantı Yöneticisi için desteğe sahip değildir. NuGet 'i kaldırmak için aşağıdaki komutu çalıştırın.

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>NuGet paket kimlikleri 'nin büyük/küçük harf durumunu değiştirme paket geri yükleme

[Bu GitHub sorununun](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932)uzunluğu konusunda anlatıldığı gibi, NuGet paketlerinin büyük/küçük harf durumunu değiştirmek NuGet desteği tarafından yapılabilir, ancak *genel paketler* klasöründe mevcut, farklı ve uyumlu paketlere sahip kullanıcılar için paket geri yükleme sırasında karmaşıklıklar oluşmasına neden olur. Paketinizin, derleme zamanı paketi geri yükleme için oluşabilecek kesme hakkındaki mevcut kullanıcılarıyla iletişim kurmak için kullanabileceğiniz bir yönteme sahipseniz yalnızca bir örnek olarak değişiklik yapmanızı öneririz.

## <a name="reporting-issues"></a>Raporlama sorunları

NuGet sorunlarını raporlamak için, adresini ziyaret edin [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues) .
