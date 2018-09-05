---
title: NuGet 2.0 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.0 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547581"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 sürüm notları

[1.8 NuGet sürüm notları](../release-notes/nuget-1.8.md) | [2.1 NuGet sürüm notları](../release-notes/nuget-2.1.md)

NuGet 2.0 19 Haziran 2012 tarihinde yayınlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.

Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi edinmek veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir

## <a name="package-restore-consent-is-now-active"></a>Paket geri yükleme onayı artık etkindir

Bu konuda açıklandığı gibi [paket geri yükleme onay sonrası](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, çevrimiçi ve paketleri indirmek paket geri yükleme etkinleştirmek için onay verilmesi artık gerekir. Paket Yöneticisi'ni yapılandırma iletişim kutusu veya EnableNuGetPackageRestore ortam değişkeni aracılığıyla onay sağladığınızdan emin olun.

## <a name="group-dependencies-by-target-frameworks"></a>Grup bağımlılıklarını hedef çerçeve tarafından

Sürüm 2.0 ile başlayarak, paket bağımlılıkları değişebilir projenin hedef çerçevesi profilini temel alan. Bu güncelleştirilmiş kullanılarak gerçekleştirilir `.nuspec` şema. `<dependencies>` Öğesi artık bir dizi içeren `<group>` öğeleri. Sıfır veya daha fazlasını içeren her grubu `<dependency>` öğeleri ve `targetFramework` özniteliği. Hedef Framework'ü hedef proje framework profili ile uyumlu ise, bir grup içindeki tüm bağımlılıkları birlikte yüklenir. Örneğin:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Bir grup içerebilir Not **sıfır** bağımlılıkları. Paket Silverlight 3.0 hedefleyen bir projeye veya üstünü, varsa, yukarıdaki örnekte, bağımlılık yüklenir. Paket, .NET 4.0 hedefleyen bir projeye veya üstünü ise, jQuery ve WebActivator, iki bağımlılıklar yüklenir.  Bu 2 çerçeveleri veya diğer herhangi bir çerçeveyi eski bir sürümünü hedefleyen bir projeye paketini yüklediyseniz, RouteMagic 1.1.0 yüklenir. Grupları arasında hiçbir devralma yoktur. Bir projenin hedef çatısının eşleşiyorsa `targetFramework` öznitelik grubunun, yalnızca o grup içindeki bağımlılıklar yüklenir.

Bir paketi Paket bağımlılıklarını iki biçimlerden birini belirtebilirsiniz: düz listesini eski biçimi `<dependency>` öğeleri veya gruplar. Varsa `<group>` biçimi kullanılır, paket 2.0 sürümünden öncekileri NuGet sürümlerine yüklenemez.

İki biçim karıştırılmasına izin olduğunu unutmayın. Örneğin, aşağıdaki kod parçacığını olduğu **geçersiz** ve NuGet tarafından reddedilir.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>İçerik dosyaları ve PowerShell betikleri tarafından hedef Framework'ü gruplandırma

Derleme başvuruları ek olarak, içerik dosyaları ve PowerShell betikleri de hedef Framework'ü gruplandırılabilir. Aynı klasör yapısında bulunan `lib` klasörü hedef Framework'ü belirtmek için artık uygulanabilir aynı şekilde `content` ve `tools` klasörleri. Örneğin:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Not**: çünkü `init.ps1` çözüm düzeyinde yürütülür ve olduğu bağımlı olmayan her bir proje, bunu doğrudan altında yerleştirilmelidir `tools` klasör. Çerçeveye özgü bir klasörde yerleştirdiyseniz göz ardı edilir.

Ayrıca, bir çerçeve klasörü olabilir NuGet 2.0 içinde yeni bir özellik olan *boş*, bu durumda, NuGet değil derleme başvurularını ekler, içerik dosyalarını eklemek veya belirli framework sürümü için PowerShell betikleri çalıştırın. Klasör yukarıdaki örnekte `content\net40` boştur.

## <a name="improved-tab-completion-performance"></a>Geliştirilmiş sekme tamamlama performans
NuGet Paket Yöneticisi konsolu için sekmesinde Tamamlama özelliği, performansı önemli ölçüde artırmak için güncelleştirildi. Öneri açılan görünene kadar SEKME tuşuna basıldığında saatten daha az gecikme olacaktır.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.0 paket geri yükleme onayı ve performans ile ilgili bir Vurgu ile birçok hata düzeltmeleri içerir.
Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
