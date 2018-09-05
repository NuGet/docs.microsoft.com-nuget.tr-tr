---
title: NuGet 3.2 RC sürüm notları
description: NuGet 3.2 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eafdedc3ad022a6794dbeb390de87d7f317e28f1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551504"
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC sürüm notları

[3.1.1 NuGet sürüm notları](../release-notes/nuget-3.1.1.md) | [3.2 NuGet sürüm notları](../release-notes/nuget-3.2.md)

NuGet 3.2 Sürüm Adayı bırakıldığını 2 Eylül 2015 geliştirmeleri ve düzeltmeleri 3.1.1 koleksiyonu olarak bırakın.  Ayrıca, yeni dist.nuget.org depoya önce yayımlanan ilk sürümleri şunlardır.

## <a name="new-features"></a>Yeni Özellikler

* Aynı klasörde Canlı projeleri artık farklı olabilir `project.json` her projeye özgü söz konusu klasördeki dosyalar.  Her proje için adı `project.json` dosya `{ProjectName}.project.json` NuGet doğru başvuru ve içeriğin her proje için uygun şekilde kullanın.  Bu, yeni bir özelliği destekler [1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config` artık bir globalPackagesFolder göreli yol - destekleyen [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>Komut satırı güncelleştirmeleri

Bu NuGet v3 sunucuları destekler nuget.exe istemcisinin ilk sürümünü ve yönetilen projeler için paketler geri yükleme ile bir `project.json` dosya.

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>Birkaç istemcisi ile arası etkileşimi geliştirmek için bu sürümde giderilen kimliği doğrulanmış akış sorun oluştu.

* Yükleme / geri yükleme etkileşimler yalnızca kimliği doğrulanmış akış - ilk istek için kimlik bilgilerini göndermek [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Anında iletme komutu yapılandırması - kimlik bilgilerinden çözümlenmiyor [1248](https://github.com/NuGet/Home/issues/1248)
* Kullanıcı aracısı ve üst bilgileri artık gönderildiğinde istatistikleri izlemeyle - yardımcı olmak için NuGet depoları için [929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>Daha iyi bir uzak NuGet deposu ile çalışacak şekilde çalışırken ağ hataları işlemek için iyileştirmeler yaptık:

* Geliştirilmiş hata iletileri alınamıyor, - uzak akışlarına bağlanmak [1238](https://github.com/NuGet/Home/issues/1238)
* Bir hata koşulu olduğunda - 1 düzgün bir şekilde geri dönmek için NuGet geri yükleme komutu düzeltildi [1186](https://github.com/NuGet/Home/issues/1186)
* Artık ağ bağlantıları yeniden deneniyor en fazla 5 kez deneyip HTTP 5xx hataları - söz konusu olduğunda her 200 ms cezası [1120](https://github.com/NuGet/Home/issues/1120)
* Sunucu yeniden yönlendirme yanıtlarını işlenmesi sırasında bir anında iletme command - geliştirilmiş [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source` Nuget.Config - bağımsız değişken olarak URL ya da Depo adı artık destekliyor [1046 numaralı](https://github.com/NuGet/Home/issues/1046)
* Depo bir geri yükleme sırasında bulunan değil eksik paketleri yerine uyarıları hata olarak rapor artık [1038](https://github.com/NuGet/Home/issues/1038)
* UNIX/Linux senaryoları - \r\n multipartwebrequest işlenmesini düzeltildi [776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>Bir dizi çeşitli komutlara sahip sorunlar için düzeltme vardır:

* Anında iletme komutu artık bir GET - paket kaynağını karşı PUT önce yapar [1237](https://github.com/NuGet/Home/issues/1237)
* LIST komutu artık sürüm numaraları - yineler [1185](https://github.com/NuGet/Home/issues/1185)
* Pack - derleme bağımsız değişkeniyle artık düzgün bir şekilde destekleyen C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Bir F # projesi paketi çalışılıyor düzeltilen sorunları ile Visual Studio 2015 - oluşturulan [1048](https://github.com/NuGet/Home/issues/1048)
* Paketler zaten mevcut olduğunda - şimdi no-ops geri [1040](https://github.com/NuGet/Home/issues/1040)
* Geliştirilmiş hata iletileri `packages.config` dosya hatalı biçimlendirilmiş - [1034](https://github.com/NuGet/Home/issues/1034)
* Geri yükleme komutu düzeltildi `-SolutionDirectory` göreli yollar - çalışmak için anahtar [992](https://github.com/NuGet/Home/issues/992)
* Geliştirilmiş çözüm çapında güncelleştirmesi - desteklemek için güncelleştirilmiş komut [924](https://github.com/NuGet/Home/issues/924)

Bu sürümde giderilen sorunların tam listesi NuGet Github'da bulunabilir [komut satırı kilometre](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Visual Studio uzantı güncelleştirmeleri

### <a name="new-features-in-visual-studio"></a>Visual Studio'da yeni özellikler

* Çözüm Gezgini'nde çözüm düğümüne çözümü geri yüklenecek paketler izin veren yeni bir bağlam menüsü öğesi eklendi ([1274](https://github.com/NuGet/Home/issues/1274)).

![Yeni 'Paket geri yükleme' bağlam menü öğesi](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Güncelleştirmeleri ve düzeltmeleri Visual Studio'da

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>Kimliği doğrulanmış akışları için düzeltmeler sağlık dökümü ve uzantısında ele.  Aşağıdaki kimlik doğrulama öğeler de uzantısı'nda ele alınan:

* NuGet v3 doğru değerlendirmesini düzgün bir şekilde kimliği doğrulanmış akışları artık yerine v2 kimliği doğrulanmış akışları - gibi [1216](https://github.com/NuGet/Home/issues/1216)
* Kimlik doğrulama kimlik bilgilerini kullanarak projeleri için düzeltilen isteği `project.json` ve v2 akışlarıyla - iletişim kurarken [1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>Ağ bağlantısı Visual Studio kullanıcı arabiriminde etkilenen ve biz bunu aşağıdaki düzeltmeleri ile ele:

* Paket sürümlerinin - yerel önbellek bakım geliştirilmiş [1096](https://github.com/NuGet/Home/issues/1096)
* V2 akışı - değerlendirilecek artık girişimi için akışı bir v3 bağlanılırken hata davranışına değiştirilen [1253](https://github.com/NuGet/Home/issues/1253)
* Artık önleme yükleme hataları bir paket birden çok paket kaynaklarıyla - yüklerken [1183](https://github.com/NuGet/Home/issues/1183)

Yapı işlemleri etkileşim işlenmesini geliştirdik:

* Tek bir projeye başarısız için - paketler geri yükleniyor, projeleri derlemek devam etmeden artık [1169](https://github.com/NuGet/Home/issues/1169)
* Çözümdeki başka bir proje tarafından bağımlı olan bir projeye bir paket yükleme zorlar bir çözüm yeniden oluşturma - [981](https://github.com/NuGet/Home/issues/981)
* Başarısız bir paket yüklemeleri düzgün bir şekilde bir takım projesi - yapılan değişiklikleri geri almak için düzeltilen [1265](https://github.com/NuGet/Home/issues/1265)
* Yanlışlıkla kaldırılmasını düzeltildi `developmentDependency` özniteliği bir pakette `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Çağrılar `install.ps1` artık uygun olan `$package.AssemblyReferences` geçirilen - nesnesi [1245](https://github.com/NuGet/Home/issues/1245)
* Artık kaldırır UWP projelerinde paketler projesi hatalı durumda - durumdayken [1128](https://github.com/NuGet/Home/issues/1128)
* Bir karışımını içeren çözümler `packages.config` ve `project.json` projeleri artık düzgün yapılandırıldığı ikinci gerek kalmadan işlem - derleme [1122](https://github.com/NuGet/Home/issues/1122)
* Bağlı veya farklı bir klasörde - yer app.config dosyaları düzgün şekilde bulma [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP projeleri artık listelenmemiş paketler - yükleme [1109](https://github.com/NuGet/Home/issues/1109)
* Paket geri yükleme bir çözüm kaydedilmiş bir durumda - olsa da artık izin [1081](https://github.com/NuGet/Home/issues/1081)


Yapılandırma dosyaları düzeltilen güncelleştirmeler işleme:

* Artık bir hedef dosya kaldırılırken teslim ardışık derlemeler üzerinde bir paketten bir `project.json` yönetilen proje - [1288](https://github.com/NuGet/Home/issues/1288)
* Artık ASP.NET 5 çözüm derleme sırasında - Nuget.Config dosyasının değiştirilmesini [1201](https://github.com/NuGet/Home/issues/1201)
* Artık değiştirilmesine sürümleri kısıtlaması Paketi güncelleştirmesi sırasında - izin [1130](https://github.com/NuGet/Home/issues/1130)
* Kilit artık dosyalarınız kilitli derleme sırasında - [1127](https://github.com/NuGet/Home/issues/1127)
* Artık değiştirme `packages.config` ve güncelleştirmeler sırasında - yeniden değil [585](https://github.com/NuGet/Home/issues/585)


TFS kaynak denetimindeki etkileşim geliştirildi:

* Artık yüklemeler için TFS'ye - bağlı paketleri başarısız [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* TFS 2013'ün tümleştirme - izin vermek için düzeltilen NuGet kullanıcı arabirimi [1071](https://github.com/NuGet/Home/issues/1071)
* Paketleri düzgün bir şekilde paket klasöründen - gelen geri başvuru düzeltildi [1004](https://github.com/NuGet/Home/issues/1004)

Son olarak, bu öğeler de geliştirdik:

* Ayrıntı düzeyini günlük iletilerini azaltılmış için `project.json` yönetilen projeleri - [1163](https://github.com/NuGet/Home/issues/1163)
* Bir paketin yüklü sürümü kullanıcı arabiriminde - düzgün bir şekilde görüntüleme artık [1061](https://github.com/NuGet/Home/issues/1061)


Visual Studio uzantısı NuGet Github'da bulunabilir giderilen sorunların tam bir listesi [3.2 Kilometre Taşı](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Bilinen Sorunlar

Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)