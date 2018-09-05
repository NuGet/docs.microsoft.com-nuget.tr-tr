---
title: NuGet 2.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikler ve dcr dahil olmak üzere 2.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548603"
---
# <a name="nuget-21-release-notes"></a>NuGet 2.1 sürüm notları

[NuGet 2.0 sürüm notları](../release-notes/nuget-2.0.md) | [NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md)

NuGet 2.1 4 Ekim 2012 tarihinde yayınlanmıştır.

## <a name="hierarchical-nugetconfig"></a>Hiyerarşik Nuget.Config

NuGet 2.1 özyinelemeli olarak aramak klasör yapısını walking yoluyla NuGet ayarları denetleme daha fazla esneklik sağlar `NuGet.Config` dosyaları ve ardından yapılandırma kümesinden tüm bulunan dosyalar oluşturma.  Örneğin, takım CI derlemeleri diğer iç bağımlılıklar için bir iç Paket Deposu olduğu senaryoyu düşünün. Her bir proje için klasör yapısı aşağıdaki gibi görünebilir:

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

Ayrıca, çözüm için paket geri yükleme etkinleştirilirse, aşağıdaki klasörü de vardır:

    C:\myteam\solution1\.nuget

Takımın iç paket deposu, her proje için kullanılabilir makinede yaparken değil, takımın çalıştığı tüm projeleri için kullanılabilir olması için size yeni bir Nuget.Config dosyası oluşturabilir ve c:\myteam klasörüne yerleştirin. Bir yolu yoktur çok specificy her proje bir paket klasörü.

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

Artık kaynak aşağıda gösterildiği gibi c:\myteam altındaki herhangi bir klasörde 'nuget.exe kaynakları' komutunu çalıştırarak eklendiğini görebiliriz:

![Paket kaynaklarından üst nuget yapılandırma](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` dosyaları aşağıdaki sırayla aranır:

1. `.nuget\Nuget.Config`
2. Yinelemeli proje klasöründen kök yol
3. Genel `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)

Uygulanan daha yapılandırmalarıdır *ters sırada*, yukarıdaki sıralamaya bağlı anlamına gelir, genel Nuget.Config ilk uygulanan, bulunan Nuget.Config dosyalar kökünden proje klasörüne gelir, ardından tarafından `.nuget\Nuget.Config`.  Bu kullanıyorsanız özellikle önemlidir `<clear/>` öğenin bir dizi öğesini yapılandırma dosyasından kaldırın.

## <a name="specify-packages-folder-location"></a>'Paketleri' klasör konumunu belirtin

Geçmişte, NuGet bilinen 'paketleri' klasöründen çözüm kök klasörü altında bulunan bir çözümün paketleri yönettiği.  NuGet paketlerini, yüklü olan birçok farklı çözümü olan geliştirme ekipleri için bu dosya sisteminde pek çok farklı yerde yüklenen paketteki sonuçlanabilir.

NuGet 2.1 paketleri klasörünün konumu üzerinde daha ayrıntılı denetim sağlar `repositoryPath` öğesinde `NuGet.Config` dosya.  Hiyerarşik Nuget.Config destek önceki örneği üzerinde oluşturma, tüm projeleri aynı paketleri klasörü C:\myteam\ paylaşmak istediğimiz varsayılır.  Bunu yapmak için aşağıdaki girişe eklemeniz yeterlidir `c:\myteam\Nuget.Config`.

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Bu örnekte, paylaşılan `Nuget.Config` dosya C:\myteam derinliği bağımsız olarak oluşturulan her proje için bir paylaşılan paketleri klasörünü belirtir. Var olan bir paket klasörü altında çözüm kökünüzde varsa, NuGet paketlerini yeni konuma yerleştirir önce VM'yi silmektir gerektiğini unutmayın.

## <a name="support-for-portable-libraries"></a>Taşınabilir kitaplıklar için destek

[Taşınabilir kitaplıklar](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ilk .NET 4,.NET Framework Windows Phone ve Xbox bile Silverlight'a sürümlerinden farklı Microsoft platformda değişiklik olmadan çalışan derlemeler oluşturmanıza olanak sağlayan ile sunulan bir özelliktir 360 (şu anda NuGet Xbox taşınabilir kitaplık hedefi desteklemiyor rağmen).  Genişleterek [paketini kuralları](../create-packages/supporting-multiple-target-frameworks.md) framework sürümleri ve profilleri, NuGet 2.1 artık taşınabilir kitaplıklar bileşik çerçevesi ve hedef profil olan paketleri oluşturmanızı sağlayarak destekler `lib` klasörleri.

Örneğin, aşağıdaki taşınabilir sınıf kitaplığının kullanılabilir hedef platformlar göz önünde bulundurun.

![Taşınabilir kitaplık oluşturma iletişim kutusu](./media/releasenotes-21-plib.png)

Kitaplığı oluşturulduktan sonra ve komut `nuget.exe pack MyPortableProject.csproj` çalıştırılır, yeni taşınabilir kitaplık paketi klasör yapısı oluşturulan NuGet paketinin içeriği incelenerek herkes tarafından görülebilir.

![Taşınabilir kitaplık paketi düzeni](./media/releasenotes-21-plib-layout.png)

Gördüğünüz gibi taşınabilir kitaplık klasörü adı kuralını 'taşınabilir-{framework 1} + {framework n}' deseni burada mevcut framework tanımlayıcıları izleyin izleyen [framework adı ve sürümü kuralları](../reference/target-frameworks.md). Bir özel durum adı ve sürümü kuralları için Windows Phone için kullanılan çerçeve tanımlayıcısı dizininde bulunur.  Bu ad, çerçeve adı 'wp' (wp7, wp71 veya wp8) kullanmanız gerekir. 'Silverlight-wp7' kullanarak, örneğin, bir hatayla sonuçlanır.

Bu klasör yapısından oluşturulan paketi yüklerken, NuGet klasör adı belirtildiği gibi birden çok hedefe artık kendi çerçevesi ve profili kuralları uygulayabilirsiniz.  NuGet'ın eşleştirme kuralları "ayrıntılı" hedef "daha az özel" olanları öncelik kazanır ilkesidir.  Bu hem de bir proje ile uyumlu olmaları durumunda belirli bir platformu hedefleyen adlar her zaman taşınabilir olanları tercih edilen anlamına gelir.  Ayrıca, birden çok taşınabilir hedefi bir proje ile uyumlu ise NuGet desteklenen platformlar kümesi "Bu paketi projeye en yakın" olduğu bir tercih eder.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Hedefleme Windows 8 ve Windows Phone 8 projeleri

Taşınabilir kitaplık projelerine hedeflemek için destek eklemenin yanı sıra, NuGet 2.1 yeni framework bilinen adlar için hem Windows 8 Store hem de Windows Phone 8 projeleri yanı sıra, Windows Store ve olacak Windows Phone projeleri için bazı yeni genel adlar sağlar gelecekteki sürümleri ilgili platformlar arasında yönetmek daha kolay.

Windows 8 Store uygulamaları için tanımlayıcıları aşağıdaki gibi görünür:

| NuGet 2.0 ve daha önceki | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45. NETCore45 | Windows, Windows8, win, win8 |

<br/>
Windows Phone projeleri için tanımlayıcıları aşağıdaki gibi görünür:

| Phone işletim sistemi | NuGet 2.0 ve daha önceki | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3 wp | WP, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7.5 (Mango) | silverlight4 wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (desteklenmiyor) | wp8, WindowsPhone8 |

<br/>
Tüm yukarıdaki değişiklikleri eski framework adları NuGet 2.1 tarafından tam olarak desteklenmeye devam edecektir.  Bunlar gelecek sürümleri ilgili platformlar arasında daha kararlı olacaktır gibi ilerletme, yeni adları kullanılmalıdır. Yeni adlar olur *değil* olması 2.1 önce NuGet sürümlerinde desteklenir, ancak, bu nedenle buna göre planlayın geçiş yapmak ne zaman.

## <a name="improved-search-in-package-manager-dialog"></a>Paket Yöneticisi iletişim kutusunda geliştirilmiş arama

Son birkaç yineleme büyük ölçüde geliştirilmiş hız ve paket aramalarınızı ilgi NuGet galerisinde değişiklikleri tanıtılmıştır.  Ancak, bu geliştirmeler nuget.org Web sitesine sınırlıydı.  NuGet 2.1 geliştirilmiş arama deneyimi NuGet Paket Yöneticisi iletişim kutusu kullanılabilir hale getirir.  Örneğin, Windows Azure önbelleğe almayı Önizleme paketi bulmak istediğinizi düşünelim.  Bu paket için makul bir arama sorgusu, "Azure Cache" olabilir.  Paket Yöneticisi iletişim kutusu önceki sürümlerinde, istenen paket bile sonuçları'nın ilk sayfasında listelenir değil.  Ancak, NuGet 2.1 içinde istenen paket artık arama sonuçları en üstünde gösterilir.

![Paket Yöneticisi iletişim arama](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Paket güncelleştirme zorla

NuGet 2.1 önce NuGet olmadığından değiştirildiği bir paketin güncelleştirilmesi atlarsınız yüksek sürüm numarası.  Bu, özellikle nerede takım Paket sürümü ile her yapı numarası artırmak için istemediğiniz derleme veya CI senaryoları durumunda belirli senaryoları uyuşmazlıkları kullanıma sunuldu.  Bir güncelleştirme bakılmaksızın zorlamak için istenen davranışı oluştu.  NuGet 2.1 'yeniden' bayrağına sahip'yöneliktir.  Örneğin, önceki NuGet sürümleri aşağıdaki daha yeni bir paket sürümü sahip bir paketi güncelleştirmeye çalışırken neden olur:

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

Yeniden bayrağıyla paket olup olmamasına bakılmaksızın güncelleştirilecek daha yeni bir sürümü.

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

Burada yeniden bayrağı yararlı kanıtlar başka bir senaryo framework yeniden hedefleme olmasıdır. Bir projeden (örneğin, .NET 4.5 için .NET 4), hedef Framework'ü değiştirilirken Update-Package-yeniden projede yüklü tüm NuGet paketlerinin doğru derlemelerine başvurular güncelleştirebilirsiniz.

## <a name="edit-package-sources-within-visual-studio"></a>Paket kaynaklarını Visual Studio'dan Düzenle

NuGet önceki sürümlerinde, silme ve paket kaynağı yeniden ekleyerek gerekli Visual Studio Seçenekleri iletişim kutusu içinde bir paket kaynağından güncelleştiriliyor.  NuGet 2.1, bu iş akışı Yapılandırması kullanıcı arabirimi birinci sınıf bir işlev olarak güncelleştirme destekleyerek artırır.

![Paket Yöneticisi'ni yapılandırma iletişim kutusu](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

NuGet 2.1 birçok hata düzeltmeleri içerir. Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
