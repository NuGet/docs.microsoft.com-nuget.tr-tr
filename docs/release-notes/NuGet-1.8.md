---
title: NuGet 1,8 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,8 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9d55534ffe765137731b7fbf4be4bbaa618c769c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236855"
---
# <a name="nuget-18-release-notes"></a>NuGet 1,8 sürüm notları

[NuGet 1,7 sürüm notları](../release-notes/nuget-1.7.md)  |  [NuGet 2,0 sürüm notları](../release-notes/nuget-2.0.md)

NuGet 1,8, 23 Mayıs 2012 ' de yayımlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.

Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.  <https://support.microsoft.com/kb/2581019>Daha fazla bilgi için bkz. veya [doğrudan vs düzeltmesine git](http://bit.ly/vsixcertfix).

Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1,8, Windows XP ile uyumsuz, düzeltme yayımlandı

NuGet 1,8 yayımlandıktan sonra, Windows XP 'de kullanıcılar tarafından 1,8 ' de bir şifreleme değişikliği olduğunu öğrendik.

Bu yana, bu sorunu gideren bir düzeltme yayımladık.  NuGet 'i Visual Studio Uzantı Galerisi aracılığıyla güncelleştirerek bu düzeltmeyi alırsınız.

## <a name="features"></a>Özellikler

### <a name="satellite-packages-for-localized-resources"></a>Yerelleştirilmiş kaynaklar için uydu paketleri
NuGet 1,8 artık yerelleştirilmiş kaynaklar için .NET Framework uydu derleme özelliklerine benzer şekilde ayrı paketler oluşturma özelliğini desteklemektedir.  Uydu paketi, bazı diğer NuGet paketiyle aynı şekilde oluşturulur ve birkaç kural eklenir:

* Uydu paket KIMLIĞI ve dosya adı, [.NET Framework tarafından kullanılan standart kültür dizelerinden](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)biriyle eşleşen bir sonek içermelidir.
* Bu `.nuspec` dosyada uydu paketinin, kimliğinde kullanılan aynı kültür dizesiyle bir dil öğesi tanımlamalıdır
* Uydu paketi, kendi `.nuspec` dosyasında, yalnızca aynı kimliğe sahip olan paket, dil sonekini içeren bir paket olan çekirdek paketine bir bağımlılık tanımlamalıdır.  Yüklemenin başarılı olması için çekirdek paketin depoda kullanılabilir olması gerekir.

Yerelleştirilmiş kaynaklarla bir paket yüklemek için, bir geliştirici doğrudan depodan yerelleştirilmiş paketi seçer. Mevcut olduğunda NuGet Galerisi, uydu paketlerine herhangi bir tür özel işleme vermez.

![Yerelleştirilmiş pacakges ile Paket Yöneticisi iletişim kutusu](./media/dlg-w-loc-packs.png)

Uydu paketi çekirdek paketine bir bağımlılık listelediğinden, hem uydu hem de çekirdek paketleri NuGet paketleri klasörüne çekilir ve yüklenir.

![Yerelleştirilmiş paketleri olan paketler klasörü](./media/fldr-loc-packs.png)

Ayrıca, uydu paketini yüklerken NuGet ayrıca kültür dize adlandırma kuralını tanır ve yerelleştirilmiş kaynak derlemesini, .NET Framework tarafından çekilecek şekilde çekirdek paket içindeki doğru alt klasöre kopyalar.

![Kopyalanmış kaynak klasörü ile çekirdek paket klasörü](./media/fldr-copied-loc.png)

Uydu paketleriyle birlikte var olan bir hata, NuGet 'in yerelleştirilmiş kaynakları `bin` Web sitesi projeleri klasörüne kopyalamamasından biridir.  Bu sorun, NuGet 'in bir sonraki sürümünde düzeltilecektir.

Uydu paketleri oluşturma ve kullanma hakkında ayrıntılı bir örnek için bkz [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) ..

### <a name="package-restore-consent"></a>Paket geri yükleme onayı
NuGet 1,8 ' de, Kullanıcı gizliliğini korumak için paket geri yüklemesi üzerinde önemli bir kısıtlamayı desteklemeye yönelik ön hazırlıkları başlattık 'u geliştirdik. Bu kısıtlama, paket geri yükleme kullanan geliştiricilerin proje ve çözümlerin yapılandırılmış paket kaynaklarından paketleri indirmek üzere paket geri yükleme 'nin çevrimiçi duruma açık olarak izin vermesini gerektirir.

Bu onayı sağlamanın 2 yolu vardır. Birincisi, aşağıda gösterildiği gibi Paket Yöneticisi yapılandırma iletişim kutusunda bulunabilir.  Bu yöntem öncelikle geliştirici makinelerine yöneliktir.

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/pr-consent-configdlg.png)

İkinci yöntem, "Enablenugetpackageresesant" ortam değişkenini "true" değerine ayarlamaya yönelik olur.  Bu yöntem, CI veya yapı sunucuları gibi katılımsız makinelere yöneliktir.

Artık yukarıda belirtildiği gibi, NuGet 1,8 ' de bu özellik için yalnızca ön hazırlıkları başlattık ' u ekledik.  Bu şekilde, bu özellik, özelliği etkinleştirmek için tüm mantığı ekledik, bu sürümde şu anda zorlanmadığını gösterir. Ancak, NuGet 'in bir sonraki sürümünde, ortamınızı uygun şekilde yapılandırabilmek için mümkün olan en kısa sürede haberdar etmeniz ve bu nedenle onay kısıtlamasını zorlayabilmemiz için etkilenmemesi gerekir.

Daha fazla ayrıntı için lütfen bu özelliğin [Takım blog gönderisine](http://blog.nuget.org/20120518/package-restore-and-consent.html) bakın.

### <a name="nugetexe-performance-improvements"></a>nuget.exe performans Iyileştirmeleri
NuGet 1,8, paketleri paralel olarak indirip yüklemek için Install komutunu değiştirerek nuget.exe – ve uzantı paketi geri yüklemesine göre önemli performans geliştirmeleri sunar.  Yüksek düzeyde test, bir projeye 6 paket yükleme performansının NuGet 1,8 ' de yaklaşık %35 oranında artmasını gösterir.  Paket sayısını 25 ' e yükseltmek yaklaşık %60 ' lik bir performans artışı gösterir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1,8, özellikle paket geri yükleme onayı ve Windows 8 Express tümleştirmesi ile ilişkili olduğu için Paket Yöneticisi konsolu ve paket geri yükleme iş akışı üzerinde vurgu içeren birkaç hata düzeltmesi içerir.
NuGet 1,8 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.