---
title: NuGet 2.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.1 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 sürüm notları

[NuGet 2.0 sürüm notları](../release-notes/nuget-2.0.md) | [NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md)

NuGet 2.1 4 Ekim 2012'de serbest bırakıldı.

## <a name="hierarchical-nugetconfig"></a>Hiyerarşik Nuget.Config

NuGet 2.1 aramakta klasör yapısını taramasını yinelemeli yapmamanız NuGet ayarlarını denetleme daha fazla esneklik sağlar `NuGet.Config` dosyaları ve tüm bulunan dosyaları kümesini yapılandırmasından oluşturma.  Örnek olarak, bir takım iç Paket Deposu diğer iç bağımlılıklar CI yapılar için sahip olduğu senaryo düşünün. Her bir proje için klasör yapısı aşağıdakine benzeyebilir:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Ayrıca, çözüm için paket geri yüklemesi etkinleştirilirse, aşağıdaki klasörü de bulunur:

    C:\myteam\solution1\.nuget

Ekibin iç Paket Deposu takım çalışır, her proje için makinede kullanıma değil sırasında tüm projeleri için kullanılabilir olması için Biz yeni bir Nuget.Config dosyası oluşturabilir ve bu c:\myteam klasöre yerleştirin. Hiçbir şekilde çok specificy proje her bir paket klasörü.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Şimdi aşağıda gösterildiği gibi c:\myteam altındaki herhangi bir klasörden 'nuget.exe kaynakları' komutunu çalıştırarak kaynak eklendi görebiliriz:

![Paket kaynaklardan üst nuget yapılandırma](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` dosyaları aşağıdaki sırayla aranır:

1. `.nuget\Nuget.Config`
2. Özyinelemeli kök proje klasöründen yol
3. Genel `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

İçinde uygulanan daha bağlantılardır *ters sırada*, yukarıdaki sırasını temel anlamına gelir, genel Nuget.Config ilk uygulanan, keşfedilen Nuget.Config dosyalar kökünden proje klasörüne gelir, ve ardından tarafından `.nuget\Nuget.Config`.  Bu kullanıyorsanız, özellikle önemlidir `<clear/>` öğeleri kümesi yapılandırma dosyasından kaldırılacak öğe.

## <a name="specify-packages-folder-location"></a>'Packages' klasörü konumu belirtin

Geçmişte, NuGet, çözüm kök klasörünün altında bulunan bir bilinen 'packages' klasöründen bir çözümün paketleri yönetilen.  NuGet paketleri yüklü olan birçok farklı çözümler sahip geliştirme ekipleri için bu dosya sisteminde pek çok farklı yerde yüklenen aynı paketin neden olabilir.

NuGet 2.1 paketleri klasörünün konumunu üzerinde daha ayrıntılı denetim sağlar `repositoryPath` öğesinde `NuGet.Config` dosya.  Hiyerarşik Nuget.Config destek önceki örneği oluşturma, C:\myteam\ paylaşımı aynı paketler klasörü altındaki tüm projeleri istediğimiz varsayalım.  Bunu başarmak için yalnızca aşağıdaki girdiyi `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Bu örnekte, paylaşılan `Nuget.Config` dosya C:\myteam derinliği bağımsız olarak oluşturulan her proje için paylaşılan paketler klasörünü belirtir. Var olan bir paket klasörü altında çözüm kök varsa, NuGet paketleri yeni konuma yerleştirir önce silmeniz gerektiğini unutmayın.

## <a name="support-for-portable-libraries"></a>Taşınabilir kitaplıklara desteği

[Taşınabilir kitaplıklara](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) önce farklı platformlarda Microsoft.NET Framework Windows Phone ve hatta Xbox Silverlight'a sürümlerinden yapmadan çalışabilirsiniz derlemeleri oluşturmanıza olanak sağlayan bir .NET 4 ile sunulan bir özelliktir 360 (şu anda NuGet Xbox taşınabilir kitaplığı hedef desteklemiyor rağmen).  Genişletme tarafından [paketini kuralları](../create-packages/supporting-multiple-target-frameworks.md) framework sürümleri ve profilleri için NuGet 2.1 artık taşınabilir kitaplıklara bileşik framework ve profil hedef sahip paketleri oluşturmanıza olanak sağlayarak destekler `lib` klasörler.

Örnek olarak, aşağıdaki taşınabilir sınıf kitaplığının kullanılabilir hedef platformlar göz önünde bulundurun.

![Taşınabilir Kitaplığı oluşturma iletişim kutusu](./media/releasenotes-21-plib.png)

Kitaplığı oluşturulduktan sonra ve komutu `nuget.exe pack MyPortableProject.csproj` çalıştırıldığında, yeni taşınabilir kitaplık paketi klasör yapısı oluşturulan NuGet paketinin içeriğini inceleyerek görülme.

![Taşınabilir kitaplık paketi düzeni](./media/releasenotes-21-plib-layout.png)

Gördüğünüz gibi taşınabilir kitaplığı klasörü adı kuralını düzeni 'taşınabilir-{framework 1} + {framework n}' Varolan framework tanımlayıcıları burada izleyin izleyen [framework adı ve sürümü kuralları](../reference/target-frameworks.md). Bir özel durum adı ve sürümü kuralları için Windows Phone için kullanılan framework tanımlayıcısı dizininde bulunur.  Bu ad, çerçeve adı 'wp' (wp7, wp71 veya wp8) kullanmanız gerekir. 'Silverlight-wp7' kullanarak, örneğin, bir hatayla sonuçlanır.

Bu klasör yapısından oluşturduğunuz paketi yüklerken, NuGet çerçevesi ve profil kurallarını klasör adı belirtildiği gibi birden çok hedefe şimdi uygulayabilirsiniz.  NuGet eşleştirme kurallarına "daha fazla belirli" hedefler "küçük" yayına öncelik kazanır ilkesidir.  Bu her ikisi de bir proje ile uyumlu olmaları durumunda belirli bir platform desteği adlar her zaman taşınabilir olanları tercih edilen olacağı anlamına gelir.  Ayrıca, birden çok taşınabilir hedefi bir projeyle uyumlu olup olmadıklarını NuGet desteklenen platformlar kümesi "paketi başvuran projeye yakın" olduğu bir tercih eder.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Hedefleme Windows 8 ve Windows Phone 8 projeleri

Taşınabilir kitaplık projeleri hedefleyen desteği ekleme ek olarak, NuGet 2.1 yeni framework adlar için Windows mağazası ve olacaktır Windows Phone projeleri için bazı yeni genel adlar yanı sıra Windows 8 Mağazası ve Windows Phone 8 projeleri sağlar ilgili platformları gelecekteki sürümleri arasında yönetmek daha kolay.

Windows 8 Mağazası uygulamaları için tanımlayıcıları aşağıdaki gibi görünür:

| NuGet 2.0 ve daha önceki | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45. NETCore45 | Windows, Windows8, win olduğu win8 |

<br/>
Windows Phone projeleri için tanımlayıcıları aşağıdaki gibi görünür:

| Phone OS | NuGet 2.0 ve daha önceki | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | WB, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (desteklenmez) | wp8, WindowsPhone8 |

<br/>
Tüm yukarıdaki değişiklikleri eski framework adları tam olarak NuGet 2.1 tarafından desteklenen devam eder.  Bunlar ilgili platformları gelecekteki sürümleri arasında daha tutarlı olarak ilerleyen, yeni adlarını kullanılmalıdır. Yeni adlarını olur *değil* olması 2.1 önce NuGet sürümlerinde desteklenir, ancak, bu nedenle uygun şekilde planlamak geçiş yapmak ne zaman.

## <a name="improved-search-in-package-manager-dialog"></a>Paket Yöneticisi iletişim kutusundaki Gelişmiş arama

Son birkaç yinelemeler üzerinden değişiklikleri hızı ve paket aramaları alaka büyük ölçüde geliştirilmiş NuGet galerisinde tanıtılmıştır.  Ancak, bu geliştirmeler nuget.org Web sitesine sınırlı.  NuGet 2.1 deneyimi geliştirilmiş arama NuGet Paket Yöneticisi iletişim kutusu üzerinden kullanılabilir hale getirir.  Örnek olarak, Windows Azure önbelleğe alma Önizleme paketini bulmak istediğinizi düşünelim.  Bu paket için makul arama sorgusu, "Azure önbelleği" olabilir.  Paket Yöneticisi iletişim önceki sürümlerinde, istenen paket bile sonuçları'nın ilk sayfasında listelenir değil.  Ancak, NuGet 2.1 istenen paket şimdi arama sonuçları en üstünde görünür.

![Paket Yöneticisi iletişim arama](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Paket güncelleştirme zorla

Bir not değiştirildiği bir paketin güncelleştirilmesi, NuGet 2.1 önce NuGet Atla yüksek sürüm numarası.  Bu uyuşmazlık – özellikle söz konusu olduğunda derleme veya CI senaryolar burada takım Paket sürümü ile her yapı numarası artırılacağını istemediğiniz belirli senaryolar için kullanıma sunuldu.  Bir güncelleştirme bakılmaksızın zorlamak için istenen davranışı oluştu.  NuGet 2.1 Bu 'yeniden' bayrağıyla giderir.  Örneğin, NuGet önceki sürümleri aşağıdaki daha yeni bir paket sürüme sahip bir paketi güncelleştirmeye çalışırken neden olur:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Paket olup olmamasına bakılmaksızın yeniden bayrağıyla güncelleştirileceği daha yeni bir sürümü.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Burada REINSTALL bayrağı faydalı kanıtlar başka bir senaryo framework yeniden hedefleme olmasıdır. Bir projeden (örneğin, .NET 4.5 için .NET 4), hedef Framework'ü değiştirirken güncelleştirme paketini-yeniden projede yüklü olan tüm NuGet paketleri için doğru derlemelerine başvurular güncelleştirebilirsiniz.

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio içinde paket kaynaklarını Düzenle

NuGet önceki sürümlerinde, silme ve paket kaynağı yeniden eklenmesi gereken Visual Studio Seçenekleri iletişim kutusu içinde bir paket kaynağından güncelleştiriliyor.  NuGet 2.1, bu iş akışı Yapılandırması kullanıcı arabirimi birinci sınıf bir işlevi olarak güncelleştirme destekleyerek artırır.

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

NuGet 2.1 birçok hata düzeltmeleri içerir. Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
