---
title: NuGet 2.0 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 2.0 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 sürüm notları

[NuGet 1.8 sürüm notları](../release-notes/nuget-1.8.md) | [NuGet 2.1 sürüm notları](../release-notes/nuget-2.1.md)

NuGet 2.0 19 Haziran 2012'de serbest bırakıldı.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.

Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir

## <a name="package-restore-consent-is-now-active"></a>Paket geri yükleme izni şimdi etkindir

Bu konuda açıklandığı gibi [sonrası paket geri yükleme izni üzerinde](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0, çevrimiçi ve paketleri indirmek paket geri yüklemesi etkinleştirmek için izin verilmesini şimdi gerektirecektir. Paket Yöneticisi yapılandırma iletişim kutusu veya EnableNuGetPackageRestore ortam değişkeni aracılığıyla izin verilen emin olun.

## <a name="group-dependencies-by-target-frameworks"></a>Bir hedef çerçeveyi Grup bağımlılıkları

2.0 sürümünden başlayarak, paket bağımlılıkları değişebilir hedef projeyi framework profilini temel alan. Bu güncelleştirilmiş kullanılarak gerçekleştirilir `.nuspec` şema. `<dependencies>` Öğesi artık bir dizi içeren `<group>` öğeleri. Sıfır veya daha fazla içeren her grubu `<dependency>` öğeleri ve bir `targetFramework` özniteliği. Hedef Framework'ü hedef proje framework profili ile uyumlu ise, bir grup içindeki tüm bağımlılıkları birlikte yüklenir. Örneğin:

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

Bir grup içerebilir Not **sıfır** bağımlılıkları. Paket bir projeye Silverlight 3.0 hedefler veya üstünü, ise yukarıdaki örnekte, bağımlılık yüklenir. Paket, yüklü olan .NET 4.0 hedefleyen projesine veya sonrası ise, iki bağımlılıkları, jQuery ve WebActivator, yüklenecek.  Paketin 2 Bu çerçeveleri ya da diğer framework eski bir sürümü hedefleyen bir projeye yüklüyse, RouteMagic 1.1.0 yüklenir. Grupları arasında hiçbir devralma yoktur. Bir projenin hedef çerçevesi eşleşirse `targetFramework` öznitelik grubunun, yalnızca o grup dahilindeki bağımlılıklar yüklenir.

Bir paketi Paket bağımlılıklarını iki biçim birini belirtebilirsiniz: düz listesini eski biçimi `<dependency>` öğeleri ya da gruplar. Varsa `<group>` biçimi kullanıldığında, NuGet 2.0'den önceki sürümleri içine paket yüklenemiyor.

İki biçim karıştırma verilmez unutmayın. Örneğin, aşağıdaki kod parçacığında **geçersiz** ve NuGet tarafından reddedilir.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>İçerik dosyaları ve PowerShell komut dosyaları hedef çerçevesi tarafından gruplandırma

Derleme başvurularını ek olarak, içerik dosyaları ve PowerShell komut dosyalarını da hedef çerçevesi tarafından gruplandırılabilir. Aynı klasör yapısını bulunan `lib` hedef Framework'ü belirtmek için klasör şimdi uygulanabilir aynı şekilde `content` ve `tools` klasörler. Örneğin:

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

**Not**: çünkü `init.ps1` çözüm düzeyinde yürütülür ve olduğu her bir proje üzerinde bağlı değil, bunu doğrudan altında yerleştirilmelidir `tools` klasör. İçinde çerçeveye özel bir klasöre girdiyseniz yoksayılacak.

Ayrıca, yeni bir NuGet 2.0 framework klasör olabilir özelliktir *boş*, bu durumda NuGet değil derleme başvurularını ekler, içerik dosyalarını eklemek veya belirli framework sürümü için PowerShell betikleri çalıştırmak. Klasör yukarıdaki örnekte `content\net40` boş.

## <a name="improved-tab-completion-performance"></a>Gelişmiş sekmesi tamamlama performansı
NuGet Paket Yöneticisi konsolunda sekme tamamlama özelliği, performansı önemli ölçüde artırmak için güncelleştirilmiştir. Öneri açılır listesinde görünene kadar SEKME tuşuna basılana zamandan daha az gecikme olacaktır.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.0 paket geri yükleme izni ve performans ile ilgili bir Vurgu ile birçok hata düzeltmeleri içerir.
Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
