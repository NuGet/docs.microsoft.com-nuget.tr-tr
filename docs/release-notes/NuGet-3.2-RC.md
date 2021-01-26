---
title: NuGet 3,2 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,2 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8132affb8273604ae79d4e1f85e6072d8eaf5ad6
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780290"
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3,2 RC sürüm notları

[NuGet 3.1.1 sürüm notları](../release-notes/nuget-3.1.1.md)  |  [NuGet 3,2 sürüm notları](../release-notes/nuget-3.2.md)

NuGet 3,2 sürüm adayı, 3.1.1 sürümü için geliştirmeler ve düzeltmeler koleksiyonu olarak 2 Eylül 2015 ' de yayımlanmıştır.  Ayrıca, bunlar ilk olarak yeni dist.nuget.org deposuna yayınlanan ilk yayınlardır.

## <a name="new-features"></a>Yeni Özellikler

* Aynı klasörde yaşayan projeler artık `project.json` Bu klasörde her bir projeye özgü farklı dosyalara sahip olabilir.  Her proje için, `project.json` Dosya `{ProjectName}.project.json` ve NuGet, bu içeriği her bir proje için uygun şekilde başvuracak ve kullanacak şekilde adlandırın.  Bu, yeni bir özelliği destekler  [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` Artık göreli yol olarak bir globalPackagesFolder destekler- [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Komut satırı güncelleştirmeleri

Bu, NuGet v3 sunucularını destekleyen ve bir dosyayla yönetilen projeler için paketleri geri yükleyen nuget.exe istemcisinin ilk sürümüdür `project.json` .

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Bu sürümde, istemciyle etkileşimi geliştirmek için ele alınan bir dizi kimliği doğrulanmış akış sorunu vardı.

* Yükleme/geri yükleme etkileşimleri yalnızca kimliği doğrulanmış akışa ilk istek için kimlik bilgilerini gönderir- [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Push komutu kimlik bilgilerini yapılandırmadan çözümlemez- [1248](https://github.com/NuGet/Home/issues/1248)
* Kullanıcı Aracısı ve üst bilgiler artık istatistik izlemeye yardımcı olmak için NuGet depolarına gönderilir- [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Uzak bir NuGet deposu ile çalışmaya çalışırken ağ başarısızlıklarını daha iyi işleyebilmek için çeşitli geliştirmeler yaptık:

* Uzak akışlara bağlanamadığınızda geliştirilen hata iletileri- [1238](https://github.com/NuGet/Home/issues/1238)
* Hata durumu oluştuğunda NuGet restore komutu düzgün bir şekilde 1 döndürecek şekilde düzeltildi- [1186](https://github.com/NuGet/Home/issues/1186)
* Şimdi HTTP 5xx hatalarında en fazla 5 deneme için her 200ms 'e ağ bağlantısı yeniden deneniyor- [1120](https://github.com/NuGet/Home/issues/1120)
* Gönderme komutu sırasında sunucu yeniden yönlendirme yanıtlarının geliştirilmiş işlemesi- [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Artık Nuget.Config bir bağımsız değişken olarak, URL 'YI veya depo adını destekler- [1046](https://github.com/NuGet/Home/issues/1046)
* Geri yükleme sırasında bir depoda bulunmayan eksik paketler artık uyarılar [1038](https://github.com/NuGet/Home/issues/1038) yerine hata olarak raporlanır
* UNIX/Linux senaryoları için \r\n çok partwebrequest işleme düzeltildi- [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Çeşitli komutlarla ilgili bazı düzeltmeler vardır:

* Push komutu artık bir paket kaynağına karşı uygulamadan önce GET yapmaz- [1237](https://github.com/NuGet/Home/issues/1237)
* List komutu artık sürüm numaralarını yinelememe- [1185](https://github.com/NuGet/Home/issues/1185)
* -Build bağımsız değişkeni ile paket artık C# 6,0- [1107](https://github.com/NuGet/Home/issues/1107) ' i desteklemektedir
* Visual Studio 2015- [1048](https://github.com/NuGet/Home/issues/1048) ile oluşturulmuş bir F # projesi paketedilmeye çalışılırken düzeltilen sorunlar
* Paketler zaten mevcutsa, şimdi geri yükleme işlemi yapılmaz- [1040](https://github.com/NuGet/Home/issues/1040)
* Dosya hatalı biçimlendirilmişse geliştirilmiş hata iletileri `packages.config` - [1034](https://github.com/NuGet/Home/issues/1034)
* `-SolutionDirectory`Göreli yollarla çalışacak anahtarla geri yükleme komutu düzeltildi- [992](https://github.com/NuGet/Home/issues/992)
* Çözüm genelinde güncelleştirmeyi desteklemek için geliştirilmiş güncelleştirilmiş komut- [924](https://github.com/NuGet/Home/issues/924)

Bu sürümde giderilen sorunların tam listesi NuGet GitHub [komut satırı kilometre taşında](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)bulunabilir.

## <a name="visual-studio-extension-updates"></a>Visual Studio Uzantı güncelleştirmeleri

### <a name="new-features-in-visual-studio"></a>Visual Studio 'da yeni özellikler

* Çözüm düğümündeki Çözüm Gezgini, çözüm oluşturmadan paketlerin geri yüklenmesine izin veren yeni bir bağlam menüsü öğesi eklenmiştir ([1274](https://github.com/NuGet/Home/issues/1274)).

![Yeni ' paket geri yükleme ' bağlam menü öğesi](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Visual Studio 'da güncelleştirmeler ve düzeltmeler

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Kimliği doğrulanmış akışlara yönelik düzeltmeler, uzantısında de toplanır.  Aşağıdaki kimlik doğrulama öğeleri de uzantısında giderilmiştir:

* Artık NuGet v3 kimlik doğrulamalı akışlar, v2 kimliği doğrulanmış akışlar yerine düzgün şekilde değerlendiriliyor- [1216](https://github.com/NuGet/Home/issues/1216)
* V2 akışlarını kullanarak ve iletişim kurarak projelerde kimlik doğrulama kimlik bilgileri için düzeltme isteği `project.json` - [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Ağ bağlantısı, Visual Studio 'daki kullanıcı arabiriminden etkilendi ve bunu aşağıdaki düzeltmelerle ilgilentik:

* Paket sürümlerinin yerel önbelleğinin Bakımı geliştirildi- [1096](https://github.com/NuGet/Home/issues/1096)
* Bir v3 akışına bağlanılırken, artık bunu v2 akışı olarak kabul etmeye çalışmayacak hata davranışı değiştirilmiştir- [1253](https://github.com/NuGet/Home/issues/1253)
* Birden çok paket kaynağına sahip bir paket yüklerken yükleme hatalarının önlenmesi Şu anda kaldırılıyor- [1183](https://github.com/NuGet/Home/issues/1183)

Yapı işlemleriyle etkileşimlerin işlenmesini geliştirdik:

* Artık tek bir proje için paketleri geri yükleme başarısız olursa proje oluşturmaya devam ediliyor- [1169](https://github.com/NuGet/Home/issues/1169)
* Çözümdeki başka bir proje tarafından bağımlı olan bir projeye paket yükleme bir çözümü yeniden derlemeyi zorlar- [981](https://github.com/NuGet/Home/issues/981)
* Projedeki değişiklikleri düzgün şekilde geri almak için başarısız paket yüklemeleri düzeltildi- [1265](https://github.com/NuGet/Home/issues/1265)
* `developmentDependency`1263 içindeki bir pakette özniteliğin yanlışlıkla kaldırılması düzeltildi `packages.config`  -  [](https://github.com/NuGet/Home/issues/1263)
* Artık öğesine yapılan çağrılar `install.ps1` doğru bir `$package.AssemblyReferences` nesne geçti- [1245](https://github.com/NuGet/Home/issues/1245)
* Proje hatalı durumda iken UWP projelerindeki paketlerin kaldırma işlemini artık engellememe- [1128](https://github.com/NuGet/Home/issues/1128)
* Ve projelerinin bir karışımını içeren `packages.config` çözümler `project.json` artık ikinci bir yapı işlemi gerekmeden düzgün şekilde oluşturulmuştur- [1122](https://github.com/NuGet/Home/issues/1122)
* Farklı bir klasöre bağlanalındıklarında veya farklı bir klasörde bulunuyorsa app.config dosyaları doğru bir şekilde bulma- [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP projeleri artık listelenmemiş paketleri yükleyebilir- [1109](https://github.com/NuGet/Home/issues/1109)
* Bir çözüm kayıtlı durumda olmadığı sürece paket geri yüklemesine artık izin verilir- [1081](https://github.com/NuGet/Home/issues/1081)


Yapılandırma dosyalarında güncelleştirmelerin işlenmesi düzeltildi:

* Yönetilen projenin sonraki yapılarında bir paketten teslim edilen bir hedef dosyayı artık kaldırmamakta `project.json` - [1288](https://github.com/NuGet/Home/issues/1288)
* ASP.NET 5 çözüm derlemesi sırasında Nuget.Config dosyaları artık değiştirilmeyen- [1201](https://github.com/NuGet/Home/issues/1201)
* Paket güncelleştirmesi sırasında izin verilen sürüm kısıtlamasını artık değiştirme- [1130](https://github.com/NuGet/Home/issues/1130)
* Kilit dosyaları artık derleme sırasında kilitli olarak kalıyor- [1127](https://github.com/NuGet/Home/issues/1127)
* Şimdi değiştirme `packages.config` ve güncelleştirmeler sırasında yeniden yazma- [585](https://github.com/NuGet/Home/issues/585)


TFS kaynak denetimi ile etkileşimler geliştirilmiştir:

* TFS- [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980) ' e bağlanan paketler için artık başarısız yükleme
* TFS 2013 tümleştirmesi 'ne izin vermek için NuGet Kullanıcı arabirimi düzeltildi- [1071](https://github.com/NuGet/Home/issues/1071)
* Paketler klasöründen düzgün şekilde geri yüklenen paketlere yönelik düzeltilen başvurular- [1004](https://github.com/NuGet/Home/issues/1004)

Son olarak, bu öğeleri de geliştirdik:

* Yönetilen projeler için azaltılmış günlük iletilerinin ayrıntı `project.json` düzeyi- [1163](https://github.com/NuGet/Home/issues/1163)
* Artık Kullanıcı arabirimindeki bir paketin yüklü sürümünü düzgün şekilde görüntülüyor- [1061](https://github.com/NuGet/Home/issues/1061)


Visual Studio uzantısı için ele alınan sorunların tamamı NuGet GitHub [3,2 kilometre taşında](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2) bulunabilir

## <a name="known-issues"></a>Bilinen Sorunlar

GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)