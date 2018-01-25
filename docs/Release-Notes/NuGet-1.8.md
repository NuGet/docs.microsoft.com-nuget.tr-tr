---
title: "NuGet 1.8 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.8 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 1.8 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e77c8a7cc2096e11571025b2a55bc6f20dfa4351
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 sürüm notları

[NuGet 1.7 Sürüm Notları](../release-notes/nuget-1.7.md) | [NuGet 2.0 sürüm notları](../release-notes/nuget-2.0.md)

NuGet 1.8 23 Mayıs 2012'de serbest bırakıldı.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.

Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.  Bkz: [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) daha fazla bilgi için veya [VS düzeltme doğrudan gidin](http://bit.ly/vsixcertfix).

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>Windows XP ile NuGet 1.8 uyumsuz yayımlanan düzeltme

Kısa süre içinde NuGet 1.8 yayımlandıktan sonra bir şifreleme değişiklik 1.8 kullanıcılar Windows XP ihlal öğrendiniz.

Bu sorunu giderir bir düzeltme beri yayımlandı.  NuGet Visual Studio uzantısı Galerisine güncelleştirerek bu düzeltme alırsınız.

## <a name="features"></a>Özellikler

### <a name="satellite-packages-for-localized-resources"></a>Yerelleştirilmiş kaynaklar için uydu paketleri
NuGet 1.8 artık yerelleştirilmiş kaynaklar, .NET Framework uydu derleme yeteneklerini benzer için ayrı paketler oluşturma olanağı destekler.  Bir uydu paketi, başka bir NuGet paketi birkaç kuralları eklenmesi ile aynı şekilde oluşturulur:

* Uydu paket kimliği ve dosya adı standart biriyle eşleşen bir sonek içermelidir [kültür .NET Framework tarafından kullanılan dizeleri](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* İçinde `.nuspec` dosya, uydu paket tanımlamanız gerekir language öğesi Kimliğinde kullanılan aynı kültür dizesiyle
* Uydu paket bağımlılık olarak tanımlamanız gerekir, `.nuspec` paket dil soneki eksi aynı Kimliğe sahip yalnızca kendi çekirdek paket dosyasına.  Çekirdek paket yüklemenin başarılı deposunda kullanılabilir olması gerekir.

Yerelleştirilmiş kaynaklar ile bir paketi yüklemek için bir uygulama geliştiricisi açıkça depodan yerelleştirilmiş paket seçer. Şu anda NuGet galerisinde özel işleme uydu paketlerden herhangi bir tür sağlamaz.

![Yerelleştirilmiş pacakges ile Paket Yöneticisi iletişim kutusu](./media/dlg-w-loc-packs.png)

Çekirdek paket için bir bağımlılık uydu paketini listeler için uydu ve çekirdek paketleri NuGet paketleri klasörüne çekilen ve yüklü.

![Yerelleştirilmiş paketleriyle paketler klasörü](./media/fldr-loc-packs.png)

Ayrıca, uydu paketi yüklerken, çalışırken NuGet da kültür dize adlandırma kuralı tanır ve böylece .NET Framework tarafından çekilebilir sonra yerelleştirilmiş kaynak assembly çekirdek paket içinde doğru alt klasörü içine kopyalar.

![Çekirdek paket klasörüne kopyalanan kaynak klasör ile](./media/fldr-copied-loc.png)

Uydu paketlerle not etmek için var olan bir hata olduğundan NuGet yerelleştirilmiş kaynaklar kopyalamaz `bin` Web sitesi projeleri için klasör.  Bu sorunu NuGet sonraki sürümde düzeltilecektir.

Oluşturma ve uydu paketlerini kullanma gösteren tam bir örnek için bkz: [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Paket geri yükleme onayı
NuGet 1.8 içinde kullanıcı gizliliğini korumak için paket geri yüklemesi üzerinde önemli bir kısıtlama desteklemek için geçişteki düzenlenir. Bu kısıtlama, projeler ve paket geri yükleme için açıkça onaylaması için paket geri yüklemesi kullanarak çözümler oluşturan geliştiriciler yapılandırılmış paket kaynaklardan paketlerini indirmek için çevrimiçi olma gerektirir.

Bu onay vermeniz 2 yolu vardır. İlk aşağıda gösterildiği gibi Paket Yöneticisi yapılandırma iletişim bulunabilir.  Bu yöntem, öncelikle Geliştirici makineler için tasarlanmıştır.

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/pr-consent-configdlg.png)

İkinci ortam değişkeni "EnableNuGetPackageRestore" "true" değerini ayarlamak için yöntemidir.  Bu yöntem CI veya yapı sunucuları gibi katılımsız makineler yöneliktir.

Şimdi, yukarıda belirtildiği gibi biz yalnızca bu özellik için geçişteki NuGet 1.8 yerleştirilmiş.  Pratikte, bu özelliği etkinleştirmek için mantığı tümünün ekledik olsa da, bunu şu anda bu sürümde uygulandığını anlamına gelir. Etkin olacaktır, ancak, sonraki ortamınızı uygun şekilde yapılandırabilir ve biz başlattığınızda, bu nedenle etkilenmiş değil, farkında mümkün olan en kısa sürede yaptığınız istedik şekilde NuGet sürümü zorunlu izin kısıtlaması.

Daha fazla ayrıntı için lütfen bkz. [ekip Web günlüğü postası](http://blog.nuget.org/20120518/package-restore-and-consent.html) bu özelliği.

### <a name="nugetexe-performance-improvements"></a>nuget.exe performans iyileştirmeleri
İndirmek ve paralel olarak paketleri yüklemek için yükleme komut değiştirerek, NuGet 1.8 önemli ölçüde performans artışı nuget.exe – ve uzantı paket geri yüklemesi tarafından getirir.  Yüksek düzey sınama 6 paket bir projeye yüklemeye yönelik performans NuGet 1.8 yaklaşık %35 tarafından artırır gösterir.  25 paketlerin sayısını artırmak hakkında 60 oranında bir performans kazancı gösterir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
Paket geri yükleme izniniz ve Windows 8 Express tümleştirme özellikle ilgili olarak NuGet 1.8 Paket Yöneticisi konsolunda ve paket geri yükleme iş akışı, bir Vurgu ile çeşitli hata düzeltmeleri içerir.
İş tam listesi için öğeleri NuGet 1.8 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
