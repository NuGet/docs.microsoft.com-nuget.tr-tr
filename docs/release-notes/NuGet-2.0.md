---
title: NuGet 2,0 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,0 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776986"
---
# <a name="nuget-20-release-notes"></a>NuGet 2,0 sürüm notları

[NuGet 1,8 sürüm notları](../release-notes/nuget-1.8.md)  |  [NuGet 2,1 sürüm notları](../release-notes/nuget-2.1.md)

NuGet 2,0, 19 Haziran 2012 tarihinde yayınlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.

Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.  <https://support.microsoft.com/kb/2581019>Daha fazla bilgi için bkz. veya [doğrudan vs düzeltmesine git](http://bit.ly/vsixcertfix).

Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.

## <a name="package-restore-consent-is-now-active"></a>Paket geri yükleme onayı artık etkin

[Paket geri yükleme onayı](http://blog.nuget.org/20120518/package-restore-and-consent.html)' nda bu gönderi bölümünde açıklandığı gibi, NuGet 2,0 artık paket geri yükleme 'nin çevrimiçi hale geçmesine ve paketleri indirmesine olanak tanımak için izin verilmesini gerektirir. Lütfen Paket Yöneticisi yapılandırma iletişim kutusu veya Enablenugetpackageresant ortam değişkeni aracılığıyla izin sağladığınızdan emin olun.

## <a name="group-dependencies-by-target-frameworks"></a>Hedef çerçevelere göre bağımlılıkları Gruplandır

Sürüm 2,0 ' den başlayarak, paket bağımlılıkları hedef projenin çerçeve profiline göre farklılık gösterebilir. Bu, güncelleştirilmiş bir şema kullanılarak gerçekleştirilir `.nuspec` . `<dependencies>`Öğesi artık bir dizi `<group>` öğe içerebilir. Her grup sıfır veya daha fazla `<dependency>` öğe ve bir `targetFramework` özniteliği içerir. Hedef çerçeve hedef proje çerçevesi profiliyle uyumluysa, bir grup içindeki tüm bağımlılıklar birlikte yüklenir. Örneğin:

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

Bir grubun **sıfır** bağımlılıklar içerebileceğini unutmayın. Yukarıdaki örnekte, paket Silverlight 3,0 veya sonraki bir sürümü hedefleyen bir projeye yüklenirse, hiçbir bağımlılık yüklenmez. Paket, .NET 4,0 veya sonraki bir sürümü hedefleyen bir projeye yüklendiyse, iki bağımlılık, jQuery ve WebActivator yüklenir.  Paket, bu 2 çerçevenin erken bir sürümünü veya başka bir çerçeveyi hedefleyen bir projeye yüklenirse, bir Kab1.1.0 yüklenir. Gruplar arasında devralma yoktur. Projenin hedef çerçevesi `targetFramework` bir grubun özniteliğiyle eşleşiyorsa, yalnızca o grup içindeki bağımlılıklar yüklenir.

Bir paket iki biçimden birinde paket bağımlılıklarını belirtebilir: düz bir öğe listesinin eski biçimi `<dependency>` veya grupları. `<group>`Biçim kullanılıyorsa, paket 2,0 öncesi NuGet sürümüne yüklenemez.

İki biçimin karıştırılmasına izin verilmeyeceğini unutmayın. Örneğin, aşağıdaki kod parçacığı **geçersiz** olur ve NuGet tarafından reddedilir.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Hedef çerçeveye göre içerik dosyalarını ve PowerShell betiklerini gruplandırma

Derleme başvurularına ek olarak, içerik dosyaları ve PowerShell betikleri hedef çerçeveye göre de gruplandırılabilir. `lib`Hedef Framework belirtme klasöründe bulunan aynı klasör yapısı artık ve klasörlerine aynı şekilde uygulanabilir `content` `tools` . Örneğin:

```
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
```

**Not**: `init.ps1` Çözüm düzeyinde yürütüldüğü ve tek bir projeye bağımlı olmadığı için, bu, doğrudan klasörün altına yerleştirilmelidir `tools` . Çerçeveye özgü bir klasör içine yerleştirilirse, yok sayılır.

Ayrıca, NuGet 2,0 ' deki yeni bir özellik çerçeve klasörünün *boş* olması, bu durumda NuGet derleme başvuruları eklememe, içerik dosyaları eklemesi veya belirli Framework sürümü için PowerShell betikleri çalıştırmayacak. Yukarıdaki örnekte, klasör `content\net40` boştur.

## <a name="improved-tab-completion-performance"></a>Gelişmiş sekme tamamlama performansı
NuGet Paket Yöneticisi konsolundaki sekme tamamlama özelliği performansı önemli ölçüde artırmak için güncelleştirildi. Öneri açılan menüsü görünene kadar SEKME tuşuna basıldığında, bu süreden çok daha az gecikme olur.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2,0, paket geri yükleme onayı ve performansı üzerine bir vurgu içeren çok sayıda hata düzeltmesi içerir.
NuGet 2,0 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.
