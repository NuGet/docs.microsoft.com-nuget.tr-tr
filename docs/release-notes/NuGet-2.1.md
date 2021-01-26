---
title: NuGet 2,1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,1 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777027"
---
# <a name="nuget-21-release-notes"></a>NuGet 2,1 sürüm notları

[NuGet 2,0 sürüm notları](../release-notes/nuget-2.0.md)  |  [NuGet 2,2 sürüm notları](../release-notes/nuget-2.2.md)

NuGet 2,1, 4 Ekim 2012 ' de yayımlanmıştır.

## <a name="hierarchical-nugetconfig"></a>Hiyerarşik Nuget.Config

NuGet 2,1, `NuGet.Config` dosyaları bulmak ve sonra bulunan tüm dosyalar kümesinden yapılandırmayı oluşturmak için, NuGet ayarlarını Denetim konusunda daha fazla esneklik sağlar.  Örnek olarak, bir ekibin diğer iç bağımlılıkların CI derlemeleri için iç paket deposuna sahip olduğu senaryoyu göz önünde bulundurun. Tek bir projenin klasör yapısı aşağıdaki gibi görünebilir:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Ayrıca, çözüm için paket geri yüklemesi etkinleştirilmişse, aşağıdaki klasör de mevcuttur:

```
C:\myteam\solution1\.nuget
```

Takımın çalıştığı tüm projeler için ekibin iç paket deposunu kullanabilmesi için, bu dosyayı makinedeki her proje için kullanılabilir hale getirmekle, yeni bir Nuget.Config dosyası oluşturabilir ve c:\Team klasörüne yerleştirebilirsiniz. Her proje için bir paket klasörünü specificbir yol yoktur.

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

Şimdi, aşağıda gösterildiği gibi c:\myteam altındaki herhangi bir klasörden ' nuget.exe Sources ' komutunu çalıştırarak kaynağın eklendiğini görebiliriz:

![Üst NuGet yapılandırmadan paket kaynakları](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` dosyalar aşağıdaki sırayla aranır:

1. `.nuget\Nuget.Config`
2. Proje klasöründen köke özyinelemeli ilerleme
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Konfigürasyonlar *ters sırada* uygulanmasından, Yani yukarıdaki sıralamaya bağlı olarak, genel Nuget.Config önce uygulanır ve ardından kök 'ten proje klasörüne ve ardından tarafından oluşturulan Nuget.Config dosyalar gelmelidir `.nuget\Nuget.Config` .  Bu, `<clear/>` bir öğe kümesini yapılandırmadan kaldırmak için öğesini kullanıyorsanız özellikle önemlidir.

## <a name="specify-packages-folder-location"></a>' Paketlerin ' klasör konumunu belirtin

Geçmişte, NuGet çözüm kök klasörü altında bulunan bilinen bir ' Packages ' klasöründen bir çözümün paketlerini yönetilemiştir.  NuGet paketleri yüklü olan çok sayıda farklı çözümü olan geliştirme ekiplerinde, bu paket, dosya sistemindeki birçok farklı yere aynı paketin yüklenmesini sağlayabilir.

NuGet 2,1, dosyadaki öğesi aracılığıyla Packages klasörünün konumu üzerinde daha ayrıntılı denetim sağlar `repositoryPath` `NuGet.Config` .  Önceki hiyerarşik Nuget.Config desteğinin örneğini oluşturmak, C:\team\ ' ın altındaki tüm projelerin aynı paketler klasörünü paylaşmasını istediğinizi varsayalım.  Bunu gerçekleştirmek için aşağıdaki girdiyi öğesine eklemeniz yeterlidir `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

Bu örnekte, paylaşılan dosya, `Nuget.Config` derinliğinden bağımsız olarak C:\myteam altında oluşturulan her proje için paylaşılan paketler klasörünü belirtir. Çözüm kökünün altında var olan bir paket klasörünüz varsa, NuGet paketleri yeni konuma yerleştirebilmeniz için bunu silmeniz gerektiğini unutmayın.

## <a name="support-for-portable-libraries"></a>Taşınabilir kitaplıklar için destek

[Taşınabilir kitaplıklar](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) , .NET 4 ' te ilk kez sunulan ve The.NET Framework sürümlerinden Silverlight 'e Windows Phone ve hatta Xbox 360 ' ye (Şu anda NuGet, Xbox taşınabilir kitaplık hedefini desteklemez) farklı Microsoft platformları üzerinde değişiklik yapılmaksızın çalışabilen derlemeler oluşturmanıza olanak tanıyan bir özelliktir.  NuGet 2,1, Framework sürümleri ve profilleri için [paket kurallarını](../create-packages/supporting-multiple-target-frameworks.md) genişleterek artık bileşik çerçeve ve profil hedef klasörlerine sahip paketler oluşturmanızı sağlayarak taşınabilir kitaplıkları desteklemektedir `lib` .

Örnek olarak, aşağıdaki taşınabilir sınıf kitaplığının kullanılabilir hedef platformlarını göz önünde bulundurun.

![Taşınabilir kitaplık oluşturma iletişim kutusu](./media/releasenotes-21-plib.png)

Kitaplık oluşturulduktan ve komut `nuget.exe pack MyPortableProject.csproj` çalıştırıldıktan sonra, yeni taşınabilir kitaplık paketi klasör yapısı oluşturulan NuGet paketinin içeriği incelenerek görülebilir.

![Taşınabilir Kitaplık paket düzeni](./media/releasenotes-21-plib-layout.png)

Görebileceğiniz gibi, taşınabilir kitaplık klasörü adı kuralı, çerçeve tanımlayıcılarının mevcut [çerçeve adı ve sürüm kurallarını](../reference/target-frameworks.md)izlediği ' Portable-{Framework 1} + {Framework n} ' düzenine uyar. Windows Phone için kullanılan çerçeve tanımlayıcıda ad ve sürüm kuralları için bir özel durum bulundu.  Bu bilinen ad, ' wp ' çerçeve adını (WP7, wp71 veya WP8) kullanmalıdır. Örneğin, ' Silverlight-WP7 ' kullanılması bir hatayla sonuçlanır.

Bu klasör yapısından oluşturulan paketi yüklerken, NuGet artık çerçeve ve profil kurallarını, klasör adında belirtildiği gibi birden çok hedefe uygulayabilir.  NuGet 'in eşleşen kurallarının arkasında "daha belirgin" hedeflerin "daha az spesifik" olarak öncelikli olduğu prensip.  Bu, belirli bir platformu hedefleyen bilinen adların, her ikisi de proje ile uyumluysa taşınabilir dosyalar üzerinde her zaman tercih edildiği anlamına gelir.  Ayrıca, birden çok taşınabilir hedef bir proje ile uyumluysa NuGet, desteklenen platform kümesinin pakete başvuran projeye "en yakın" olduğu bir tane tercih eder.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Windows 8 ve Windows Phone 8 projelerini hedefleme

NuGet 2,1, taşınabilir kitaplık projelerini hedeflemek için destek eklemenin yanı sıra hem Windows 8 Mağazası hem de Windows Phone 8 projeleri için yeni çerçeve adları ve Windows Mağazası için yeni genel adlar ve ilgili platformların gelecek sürümlerinde daha kolay Yönetilecek projeler için de Windows Phone.

Windows 8 Mağaza uygulamaları için tanımlayıcılar şöyle görünür:

| NuGet 2,0 ve öncesi | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, . NETCore45 | Windows, Windows8, Win, Win8 |

<br/>
Windows Phone projeleri için, tanımlayıcılar şöyle görünür:

| Telefon OS | NuGet 2,0 ve öncesi | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-WP | WP, wp7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (Mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (desteklenmiyor) | WP8, WindowsPhone8 |

<br/>
Yukarıdaki değişikliklerin tümünde, eski Framework adları NuGet 2,1 tarafından tam olarak desteklenmeye devam edecektir.  İleri doğru, yeni adların ilgili platformların gelecekteki sürümlerinde daha kararlı olacağı için kullanılması gerekir. Yeni adlar 2,1 ' den önceki NuGet sürümlerinde *desteklenmeyecektir, bu nedenle* anahtarın ne zaman olacağını planlayın.

## <a name="improved-search-in-package-manager-dialog"></a>Paket Yöneticisi Iletişim kutusunda geliştirilmiş arama

Son birkaç yinelemeden sonra, paket aramalarının hızını ve uygunluğunu büyük ölçüde artıran NuGet galerisine değişiklikler yapılmıştır.  Ancak, bu iyileştirmeler nuget.org Web sitesiyle sınırlandırılmıştır.  NuGet 2,1, NuGet Paket Yöneticisi iletişim kutusunda geliştirilmiş arama deneyimini kullanıma sunar.  Örnek olarak, Windows Azure önbelleğe alma önizleme paketini bulmak istediğinizi düşünün.  Bu paket için makul bir arama sorgusu "Azure önbelleği" olabilir.  Paket Yöneticisi iletişim kutusunun önceki sürümlerinde, istenen paket sonuçların ilk sayfasında da listelenmemelidir.  Ancak, NuGet 2,1 ' de, istenen paket artık arama sonuçlarının en üstünde görünür.

![Paket Yöneticisi iletişim kutusu arama](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Paket güncelleştirmesine zorla

NuGet 2,1 ' den önce, büyük bir sürüm numarası olmadığında NuGet bir paketin güncelleştirilmesini atlar.  Bu, özellikle ekibin her bir derleme ile paket sürüm numarasını artırmak istememediği belirli senaryolar için ortaya çıkan, özellikle de derleme veya CI senaryolarında tanıtılmıştır.  İstenen davranış, bir güncelleştirmeyi bağımsız olarak zorlamaktır.  NuGet 2,1 bunu ' REINSTALL ' bayrağıyla gidermektedir.  Örneğin, NuGet 'in önceki sürümleri, daha yeni bir paket sürümüne sahip olmayan bir paketi güncelleştirmeye çalışırken aşağıdakiler ile sonuçlanır:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Yeniden yükleme bayrağıyla, daha yeni bir sürüm olup olmamasına bakılmaksızın paket güncelleştirilir.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Yeniden yükleme bayrağının yararlı olduğu başka bir senaryo Framework 'ün yeniden hedeflemesine yarar. Projenin hedef çerçevesini değiştirirken (örneğin, .NET 4 ' ten .NET 4,5 ' e kadar), Update-Package yeniden yükleme, projede yüklü olan tüm NuGet paketleri için doğru derlemelere başvuruları güncelleştirebilir.

## <a name="edit-package-sources-within-visual-studio"></a>Visual Studio 'Da paket kaynaklarını düzenleme

NuGet 'in önceki sürümlerinde, Visual Studio Seçenekler iletişim kutusunun içinden bir paket kaynağını güncelleştirme, paket kaynağını silme ve yeniden ekleme için gereklidir.  NuGet 2,1, güncelleştirmeyi yapılandırma Kullanıcı arabiriminin ilk sınıf işlevi olarak destekleyerek bu iş akışını geliştirir.

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

NuGet 2,1 birçok hata düzeltmesi içerir. NuGet 2,0 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.
