---
title: "NuGet 3.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 70316f35-f046-4f72-98e0-736de172e918
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.2 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 364a1ac62af25351e78df0b9a506f0919fc8fb61
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-32-release-notes"></a>NuGet 3.2 sürüm notları

[NuGet 3.2 RC sürüm notları](../release-notes/nuget-3.2-RC.md) | [NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md)

NuGet 3.2 yayımlanan 16 Eylül 2015 geliştirmeleri ve 3.1.1 yönelik düzeltmeler koleksiyonu olarak serbest bırakır ve hem de kullanılabilir [dist.nuget.org](http://dist.nuget.org/index.html) ve [Visual Studio Galerisi](https://visualstudiogallery.msdn.microsoft.com/5d345edc-2e2d-4a9c-b73b-d53956dc458d?SRC=Home).

## <a name="new-features"></a>Yeni Özellikler

* Aynı klasörde Canlı projeler artık farklı olabilir `project.json` her proje için belirli o klasördeki dosyaları.  Her proje için ad `project.json` dosya `{ProjectName}.project.json` ve NuGet vereceği tercih her proje için bu yapılandırma için uygun şekilde.  Bu yalnızca yüklü - Windows 10 araçlarını v1.1 ile desteklenen [1102](https://github.com/NuGet/Home/issues/1102)
* NuGet istemcileri desteklemek kullanılan paylaşılan genel paketler klasörü konumunu belirtmek için genel bir NUGET_PACKAGES ortam değişkeni belirtme `project.json` yönetilen Windows 10 araçlarını v1.1 projelerle.

## <a name="command-line-updates"></a>Komut satırı güncelleştirmeleri

Bu NuGet v3 sunucuları destekler nuget.exe istemcisinin ilk sürümünü ve yönetilen projeler için paketler geri bir `project.json` dosyası.

İstemci ile etkileşim artırmak için bu sürümde ele alınan kimliği doğrulanmış akış sorunları vardı.

* Yüklemek / geri yükleme etkileşimleri yalnızca kimliği doğrulanmış akışa - ilk istek için kimlik bilgilerini göndermek [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)
* Anında iletme komutu yapılandırması - kimlik bilgilerini çözümlenmiyor [1248](https://github.com/NuGet/Home/issues/1248)
* Kullanıcı aracısı ve üstbilgileri şimdi gönderildiğinde istatistikleri izlemeyle - yardımcı olmak için NuGet depoları için [929](https://github.com/NuGet/Home/issues/929)

Biz yapılan geliştirmeler daha iyi uzaktan NuGet deposu ile çalışmaya çalışırken ağ hataları işlemek için sayısı:

* Geliştirilmiş hata iletileri oluşturulamıyor, farklı uzak akışlarına - bağlanmak [1238](https://github.com/NuGet/Home/issues/1238)
* NuGet restore komutu bir hata koşulu oluştuğunda - 1 düzgün bir şekilde geri dönmek için düzeltildi [1186](https://github.com/NuGet/Home/issues/1186)
* Artık ağ bağlantıları yeniden deneniyor HTTP 5xx hataları - söz konusu olduğunda 5 deneme sayısı için her 200 MS [1120](https://github.com/NuGet/Home/issues/1120)
* Sunucu yeniden yönlendirme yanıtlarını işlenmesi sırasında bir anında iletme komutu - geliştirilmiş [1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`Şimdi Nuget.Config - bağımsız değişken olarak URL veya depo adından destekler [1046 numaralı](https://github.com/NuGet/Home/issues/1046)
* Bir geri yükleme sırasında bir havuzda bulunan değil eksik paketleri yerine uyarıları hata olarak rapor artık [1038](https://github.com/NuGet/Home/issues/1038)
* UNIX/Linux senaryolarında - \r\n multipartwebrequest işlenmesi düzeltilmiştir [776](https://github.com/NuGet/Home/issues/776)

Çeşitli komutları ile ilgili sorunlar için bir dizi vardır:

* Anında iletme komutu artık kilitlenmiyor GET - paket kaynağını karşı PUT önce [1237](https://github.com/NuGet/Home/issues/1237)
* LIST komutu artık sürüm numaraları - yineler [1185](https://github.com/NuGet/Home/issues/1185)
* Pack yapı bağımsız değişkeniyle şimdi düzgün destekleyen C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* F # projesinde paketi çalışılıyor düzeltilmiş sorunları yerleşik içeren Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)
* Paketler zaten mevcut olduğunda - şimdi no-ops geri [1040](https://github.com/NuGet/Home/issues/1040)
* Geliştirilmiş hata iletileri `packages.config` dosyası hatalı biçimlendirilmiş - [1034](https://github.com/NuGet/Home/issues/1034)
* Göreli yollar ile - çalışmak için restore komutu - SolutionDirectory anahtarıyla düzeltildi [992](https://github.com/NuGet/Home/issues/992)
* Çözüm genelinde güncelleştirmesi - desteklemek için güncelleştirilmiş komutu geliştirilmiş [924](https://github.com/NuGet/Home/issues/924)

Bu sürümde ele sorunların tam listesi NuGet Github'da bulunabilir [komut satırı Kilometre Taşı](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).

## <a name="visual-studio-extension-updates"></a>Visual Studio uzantısı güncelleştirmeleri

### <a name="new-features-in-visual-studio"></a>Visual Studio'da yeni özellikler

* Çözüm Gezgini çözümü oluşturma olmadan geri yüklenecek paketleri sağlar çözüm düğümünde yeni bir bağlam menüsü öğesini eklendi ([1274](https://github.com/NuGet/Home/issues/1274)).

![Yeni 'Paketler geri' bağlam menüsü öğesini](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>Güncelleştirmeler ve düzeltmeler Visual Studio'da

Kimliği doğrulanmış akışları düzeltmelerin toplandı ve uzantısında ele.  Aşağıdaki kimlik doğrulama öğeler de uzantısı'nda ele alınan:

* NuGet v3 doğru şekilde davranma akışları düzgün bir şekilde, kimlik doğrulaması artık yerine v2 akışları - kimlik doğrulaması gibi [1216](https://github.com/NuGet/Home/issues/1216)
* Kimlik doğrulama kimlik bilgilerini kullanarak projeleri için düzeltilen isteği `project.json` ve v2 akışlarıyla - iletişim kurarken [1082](https://github.com/NuGet/Home/issues/1082)

Ağ bağlantısı Visual Studio kullanıcı arabiriminde etkilenen ve biz bu ile aşağıdaki düzeltmeleri ele:

* Paket sürümlerinin - yerel önbelleği bakım geliştirilmiş [1096](https://github.com/NuGet/Home/issues/1096)
* V2 akışı olarak - işlemek için artık girişimi akış v3 bağlanırken hata davranışı değişti [1253](https://github.com/NuGet/Home/issues/1253)
* Şimdi önleme yükleme hataları bir paket birden çok paket kaynaklarıyla - yüklerken [1183](https://github.com/NuGet/Home/issues/1183)

Biz yapı işlemleri ile etkileşim işlenmesini geliştirilmiş:

* Tek bir proje başarısız için - paketleri geri yükleniyor, projeler derlemek etmeden artık [1169](https://github.com/NuGet/Home/issues/1169)
* Bir projeye çözümdeki başka bir projeye göre bağımlı bir paketi yükleniyor zorlar bir çözüm yeniden oluşturma - [981](https://github.com/NuGet/Home/issues/981)
* Başarısız paketi yükler düzgün bir proje - yapılan değişiklikleri geri almak için düzeltildi [1265](https://github.com/NuGet/Home/issues/1265)
* Yanlışlıkla kaldırılmasını düzeltildi `developmentDependency` bir pakette öznitelikte `packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* Çağrılar `install.ps1` şimdi uygun olan `$package.AssemblyReferences` geçirilen - nesnesi [1245](https://github.com/NuGet/Home/issues/1245)
* Artık önleme kaldırır UWP projelerinde paketlerin proje hatalı bir duruma - olsa [1128](https://github.com/NuGet/Home/issues/1128)
* Bir karışımını içeren çözümleri `packages.config` ve `project.json` projeleri şimdi düzgün yerleşiktir saniyenin gerek kalmadan işlemi - yapı [1122](https://github.com/NuGet/Home/issues/1122)
* App.config dosyaları bağlı veya farklı bir klasörde - bulunan düzgün bulma [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)
* UWP projeleri şimdi listelenmemiş paketler - yüklemek [1109](https://github.com/NuGet/Home/issues/1109)
* Paket geri yüklemesi bir çözüm kaydedilen bir duruma - olmamasına karşın şimdi izin [1081](https://github.com/NuGet/Home/issues/1081)

Yapılandırma dosyaları düzeltilen güncelleştirmeleri işleme:

* Artık hedefler dosyası kaldırma teslim sonraki derlemelerini üzerinde paketinden bir `project.json` yönetilen proje - [1288](https://github.com/NuGet/Home/issues/1288)
* Artık ASP.NET 5 çözümü derleme sırasında - Nuget.Config dosyalarını değiştirme [1201](https://github.com/NuGet/Home/issues/1201)
* Paket güncelleştirme sırasında - izin sürümleri kısıtlaması artık değiştirme [1130](https://github.com/NuGet/Home/issues/1130)
* Kilit şimdi dosyalarınız kilitli derleme sırasında - [1127](https://github.com/NuGet/Home/issues/1127)
* Şimdi değiştirme `packages.config` ve güncelleştirmeleri sırasında - yeniden değil [585](https://github.com/NuGet/Home/issues/585)

TFS kaynak denetimindeki ile etkileşim geliştirildi:

* Artık yükler - TFS bağlı olan paketler için başarısız olan [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)
* TFS 2013 tümleştirmesi - izin vermek için düzeltilen NuGet kullanıcı arabirimi [1071](https://github.com/NuGet/Home/issues/1071)
* Paketleri klasöründen - düzgün gelmesini geri Paketlerine yönelik başvuruları düzeltildi [1004](https://github.com/NuGet/Home/issues/1004)

Son olarak, bu öğeler biz de Geliştirilmiş:

* Ayrıntı düzeyini günlük iletilerini azaltılmış `project.json` yönetilen projeleri - [1163](https://github.com/NuGet/Home/issues/1163)
* Bir paketin yüklü olan sürümü kullanıcı arabiriminde - düzgün görüntüleme artık [1061](https://github.com/NuGet/Home/issues/1061)
* Kendi nuspec şimdi belirtilen bağımlılık aralıklarıyla paketleriniz varsa bu bağımlılıkların kararlı Paket sürümü için - yüklü yayın öncesi sürümlerini [1304](https://github.com/NuGet/Home/issues/1304)

Visual Studio uzantısı NuGet Github'da bulunabilir ele sorunların tam listesi [3.2 Kilometre Taşı](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>Bilinen Sorunlar

Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)