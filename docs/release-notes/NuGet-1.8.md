---
title: NuGet 1.8 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.8 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546627"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 sürüm notları

[1.7 NuGet sürüm notları](../release-notes/nuget-1.7.md) | [2.0 NuGet sürüm notları](../release-notes/nuget-2.0.md)

NuGet 1.8 23 Mayıs 2012 tarihinde yayınlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.

Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi edinmek veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 uyumsuz Windows XP ile yayımlanan düzeltme

Kısa bir süre içinde NuGet 1.8 yayımlandıktan sonra bir şifreleme değişiklik 1.8 kullanıcılar Windows XP kesildi öğrendiniz.

Bu sorunu gideren bir düzeltme beri yayımladık.  Visual Studio uzantı Galerisi aracılığıyla NuGet güncelleştirerek bu düzeltmeyi alırsınız.

## <a name="features"></a>Özellikler

### <a name="satellite-packages-for-localized-resources"></a>Uydu paketleri için yerelleştirilmiş kaynaklar
NuGet 1.8 artık ayrı paketler için .NET Framework'ün uydu derleme özellikleri benzer yerelleştirilmiş kaynaklar oluşturma özelliği destekler.  Uydu paket herhangi bir NuGet paketi eklenmesi birkaç kuralları ile aynı şekilde oluşturulur:

* Standart biriyle eşleşen bir sonek uydu paket Kimliğini ve dosya adı içermelidir [dizeleri .NET Framework tarafından kullanılan kültür](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* İçinde `.nuspec` dosya, uydu paket tanımlamanız gerekir dil öğesi Kimliğinde kullanılan aynı kültür dizesiyle
* Uydu paket bağımlılık olarak tanımlamalıdır kendi `.nuspec` yalnızca dil soneki eksi aynı Kimliğe sahip paketi, çekirdek paket dosyasına.  Çekirdek paketini depo başarılı yükleme için kullanılabilir olması gerekir.

Yerelleştirilmiş kaynakları bir paketi yüklemek için bir geliştirici açıkça depodan yerelleştirilmiş paketi seçer. Şu anda NuGet galerisinde uydu paketleri için özel olarak değerlendirilmesi herhangi bir türden vermez.

![Paket Yöneticisi iletişim yerelleştirilmiş pacakges ile](./media/dlg-w-loc-packs.png)

Uydu paketi, çekirdek paket bağımlılık listelediği için uydu ve çekirdek paketler NuGet paketleri klasöre çekilir ve yüklü.

![Yerelleştirilmiş paketler ile paketler klasörü](./media/fldr-loc-packs.png)

Ayrıca, uydu paket yükleme, çalışırken NuGet kültür dizesi adlandırma kuralı da tanır ve böylece .NET Framework tarafından çekilmesi ardından yerelleştirilmiş kaynak derlemesi çekirdek paket içindeki doğru alt klasörü içine kopyalar.

![Çekirdek paket klasörüne kopyalanan kaynağı klasörü](./media/fldr-copied-loc.png)

Uydu paketlerle Not mevcut bir hatayı olan NuGet için yerelleştirilmiş kaynaklar kopyalamaz `bin` Web sitesi projeleri için klasör.  Bu sorun, NuGet sonraki sürümde düzeltilecektir.

Uydu paketleri oluşturup kullanacağınızı nasıl yazılacağını gösteren tam bir örnek için bkz: [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Paket geri yükleme onayı
NuGet 1.8 sürümünde, biz paket geri yükleme, kullanıcı gizliliğini korumak için önemli bir kısıtlama desteklemek için öğrenmeniz açıklanmıştır. Bu kısıtlama, projeler ve açıkça geri yükleme paketini onay için paket geri yükleme kullanan çözümler oluşturan geliştiriciler yapılandırılmış paket kaynaklarından paketleri indirmek için çevrimiçi olma gerektirir.

Bu onay sağlamak için 2 yolu vardır. İlk, aşağıda gösterildiği gibi Paket Yöneticisi'ni yapılandırma iletişim kutusunda bulunabilir.  Bu yöntem öncelikle Geliştirici makineleri için tasarlanmıştır.

![Paket Yöneticisi'ni yapılandırma iletişim kutusu](./media/pr-consent-configdlg.png)

İkinci yöntem, değeri "true" değişken "EnableNuGetPackageRestore" ortam ayarlamaktır.  Bu yöntem, CI veya yapı sunucuları gibi katılımsız makineler içindir.

Şimdi, yukarıda belirtildiği gibi biz yalnızca bu özellik için öğrenmeniz NuGet 1.8 ile düzenlenir.  Pratikte, bu tüm özelliği etkinleştirmek için mantığı ekledik ancak bunu şu anda bu sürümde uygulandığını anlamına gelir. Etkinleştirilir, ancak sonraki NuGet, böylece biz başlattığınızda, bu nedenle etkilenmiş değil ve ortamınızı uygun şekilde yapılandırabilirsiniz, bunun farkında olabildiğince çabuk yapmak istedik şekilde sürümünü zorunlu onay kısıtlaması.

Daha fazla ayrıntı için lütfen bkz [team blog gönderisi](http://blog.nuget.org/20120518/package-restore-and-consent.html) bu özelliği.

### <a name="nugetexe-performance-improvements"></a>nuget.exe performans geliştirmeleri
Paketler paralel olarak indirip yükleme komutunu değiştirerek, NuGet 1.8 önemli ölçüde performans geliştirmeleri nuget.exe – ve uzantı paket geri getirir.  Yüksek düzey testi performans 6 paketleri projeye yüklemek için yaklaşık %35 NuGet 1.8 tarafından artırır gösterir.  25 paketlerin sayısını artırmayı yaklaşık 60 oranında bir performans kazancı gösterir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
Özellikle Windows 8 Express tümleştirme paket geri yükleme onayı ile bağlantılı olarak 1.8 NuGet Paket Yöneticisi konsolu ve paket geri yükleme iş akışı, Otomasyona oldukça hata düzeltmeleri içerir.
Tam bir listesi için iş öğeleri NuGet 1.8 sürümünde, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
