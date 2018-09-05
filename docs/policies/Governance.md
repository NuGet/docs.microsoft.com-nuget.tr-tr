---
title: NuGet proje yönetimi
description: NuGet, kodunuzu, Katkıda Bulunanlar ve kullanıcılar için rol ve Sorumluluk dahil olmak üzere için idare modeli.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2aaaf41b3fc4ef3621333e5099780b5d7ef393bc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549456"
---
# <a name="nuget-governance"></a>NuGet idare

> Bu belge temel aldığı [Benevolent Dictator idare modeli](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) , University Oxford tarafından. Altında lisanslı bir [Creative Commons atıf-Lisansdevam 2.0 UK: İngiltere & Galler lisansı](http://creativecommons.org/licenses/by-sa/2.0/uk/).

NuGet projesi bir Benevolent Dictator tarafından yönetilen ve topluluk tarafından yönetilir. Diğer bir deyişle, topluluk, projenin günlük bakım için etkin olarak katkıda bulunan, ancak genel stratejik çizgi benevolent dictator çizilir. Çözünürlüğünün olması durumunda son sözcüğü benevolent dictator sahiptir.

Topluluk içinde Anlaşmazlıkların çözüm yeri ve proje koordineli bir şekilde ilerleme erişebildiğinden emin olmak için benevolent dictator'ın işi var. Buna karşılık, etkin katılım ve katkı aracılığıyla benevolent dictator kararları kılavuza birliğinin işidir.

## <a name="roles-and-responsibilities"></a>Rolleri ve sorumlulukları

Burada açıklanan dört rolü vardır: Benevolent Dictator, kodunuzu, Katkıda Bulunanlar ve kullanıcılar.

### <a name="benevolent-dictator"></a>Benevolent dictator

NuGet çekirdek ekibi Benevolent Dictator ya da proje lideri olarak kendi kendine kaldırmasını. Ancak, topluluk her zaman çatal özelliği olduğundan, takım topluluğuna tam olarak yanıt verilemeyen olur. Proje lideri bir bütün olarak topluluk anlamak ve çakışan birçok gerektiğinde mümkün olduğunca projenin uzun vadede şekilde kalmıştır sağlarken karşılamak için çaba beklenir.

Birçok yolla benevolent dictator rolünü dictatorship ve diplomacy hakkında daha fazla küçük. Proje genişledikçe doğru kişilere ele etkisi verilir ve topluluk proje lideri sunulmasıyla rallies, anahtar sağlamaktır. Müşteri adayının iş sonra (aşağıya bakın) kodunuzu doğru proje adına kararlar emin emin olmaktır. Genel olarak bakıldığında, kodunuzu içeren projenin stratejisi hizalanır sürece, proje lideri istenen şekilde devam etmek bunları izin verir.

Ayrıca, .NET Foundation personeli proje lideri NuGet iletişim etki alanı kaydı ve teknik hizmetler (örneğin kod imzalama) gibi işle ilgili işlemlerin amacıyla birincil ya da ilk noktası göz önünde bulundurun.

### <a name="committers"></a>Kodunuzu

Kodunuzu sürekli değerli Katkıları için NuGet yaptıktan ve tarafından Benevolent Dictator tayin katkıda bulunanlar ' dir. Tayin sonra kodunuzu üzerine hem depoya doğrudan kod yazma ve diğer Katkıları ekran yararlandı. Kodunuzu genellikle geliştiriciler olur ancak başka yollarla da katkıda bulunabilirsiniz.

Genellikle, bir teslim eden projenin belirli bir yönüne odaklanan ve bir uzmanlık ve bunları topluluğun ve proje lideri saygı işletmeyse anlama düzeyi sunar. Resmi bir teslim eden rolü değil, yalnızca rehberlik ve destek için onlara proje sağlama görünür olarak etkili topluluk üyelerinin varsayar konumu.

Kodunuzu nereye NuGet genel yönünü ilgilidir yetkili vardır. Ancak, proje lideri kulak vardır. Müşteri adayı birliğinin gereksinimlerini ve ortak hedefleri farkında olduğundan emin olun ve geliştirme veya uygun Katkıları projeye çözüleceği yardımcı olması için teslim eden'ın iş var. Genellikle kodunuzu kendi sorumluluk belirli alanları resmi olmayan bir denetime verilir ve doğrudan kaynak kodunun belirli alanları değiştirmek için hakları atanır. Kodunuzu açık karar verme yetkilisi gerekmese de, diğer bir deyişle, bunlar genellikle eylemlerini sağlama tarafından alınan kararları işlevlerindeki olduğunu göreceksiniz.

### <a name="contributors"></a>Katkıda Bulunanlar

Katkıda Bulunanlar NuGet düzeltme eki gönderen topluluk üyeleridir. Bu düzeltme ekleri tek seferlik bir olay veya zaman içinde oluşan olabilir. Beklentileri olan Katkıda Bulunanlar, küçük düzeltme eklerinin gönderme ilk ve katkıda bulunan, kodunuzu ve proje lideri katkıda bulunan kişinin düzeltme ekleri kalitesini ellerde geliştirdim olduğunda daha büyük. Katkıda Bulunanlar, ilişkili ürün sürüm notları adlı belgeyi tanınır.

Depoya katkıda bulunan kişinin ilk düzeltme eki getirilir önce oturum açmaları gerektiğini bir [katkıda bulunan lisans sözleşmesi](http://en.wikipedia.org/wiki/Contributor_License_Agreement) veya .NET Foundation için bir atama anlaşma. Düzeltme eki gönderildi ve ele alınan ancak aslında yerden uygun belgeler olmadan depoya kaydedilmiş olamaz. Katkıda bulunan lisans sözleşmesi elde etmek için lütfen bir isteği e-posta Gönder [ contributions@nuget.org ](mailto:contributions@nuget.org).

Katkıda bulunan olmak için aşağıdaki depolardan birinde bir çekme isteği gönderme:

- [NuGet istemci](https://github.com/NuGet/NuGet.Client)
- [NuGet Galerisi](https://github.com/nuget/nugetgallery)
- [NuGet belgeleri](https://github.com/nuget/nugetdocs)

Bir çekme isteği için ayrıntılı işlem depo değişir:

- [NuGet istemci ile NuGet Galerisi'nin için katkı yönergeleri](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Katkı yönergeleri için NuGet belgeleri](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Kullanıcılar

Kullanıcıların ihtiyacı olan ve NuGet paketi Tüketicileri ve/veya yazarlar olarak kullanmak topluluk üyeleridir. Topluluk üyelerinin en önemli kullanıcılardır: bunlar olmadan proje herhangi bir amacı yoktur. Herhangi bir kullanıcı olabilir. belirli gereksinimler yoktur.

Kullanıcılar, NuGet ve mümkün olduğunca topluluk hayatta katılmaya teşvik. Kullanıcı katkılar, söz konusu kullanıcıların ihtiyaçlarını karşılayan emin olmak proje ekibi etkinleştirin. Genel kullanıcı etkinlikleri içerir ancak bunlarla sınırlı değildir:

- Projeyi kullanıma sağduyulu
- Proje güçlü ve zayıf yeni bir kullanıcının açısından bildiren geliştiriciler
- (Uzun yol teşekkür sağlanabilir) moral desteği sağlama
- Yazma belgeler ve öğreticiler
- Hata raporlarını ve özellik istekleri dosyalama
- Hata bashes gibi topluluk etkinlikleri katılma
- Tartışma panosu veya Forum katılma

Proje ve onun topluluk ile etkileşim kurmak için devam eden kullanıcıların kendilerini daha ilgili hale genellikle bulabilirsiniz. Bu kullanıcılar ardından Katkıda Bulunanlar, yukarıda açıklanan şekilde olacak geçin.

## <a name="package-succession-under-special-circumstances"></a>Paket art arda özel koşullar altında

Burada bir NuGet hesap sahibinin incapacitated veya öldü talihsiz durumda biz burada tek sahipliği söz konusu hesabın sahip ve paket altında yayımlanan paket için uygun sahibi/sn eklemek için toplulukla birlikte çalışabilecek bir [OSI Lisans onaylanan](https://opensource.org/licenses/alphabetical). Sahipliği istemek için bize aşağıdaki belgeler göndermeniz gerekir:

1. Bir kamu verilen fotoğraf kimliğinizi, fotokopi
1. Önceki hesap sahibinin durum kanıtlama aşağıdaki belgeler biri: 
    - Bir resmi, kamu verilen ölüm sertifika öldü, önceki hesap sahibi ise veya
    - Bir sağlık professional incapacitated hesap sahibi sağlık sorumlu tarafından imzalanmış bir sertifika gibi onaylanmış bir belge.
1. Aşağıdaki belgeler, sağda sahipliği kanıtlama biri: 
    - Hesap sahibinin sürdüren bağına sahip olduğunu gösteren marriage sertifikası
    - İmzalı power of avukata
    - Yürütücü veya isim lehtarıdır gibi adlandırma olacaktır ya da güven belgenin kopyasını,
    - Doğum sertifika için hesap sahibi, üst ise veya
    - Hesap sahibinin geçerli bir koruyucu varsa guardianship belgeler.

Lütfen bize bir e-postası gönderin kendinizi bu ilke çağrılırken geçirilmesi gereken fark ederseniz, [ support@nuget.org ](mailto:support@nuget.org) kimliği ve Paket sürümü.

## <a name="transparency"></a>Saydamlık

Açık kaynaklı bir projeyi idare topluluk güven oluşturma, elde edeceği başarı için önemlidir. Bu amaçla, karar alma sürecini saydam ve açık bir şekilde yapılması gerekir. Projenin yönü tartışmasına herkese açık şekilde yapılması gerekir. Topluluk hiçbir zaman yakalanmalıdır geziniyorsanız Benevolent Dictator tarafından karar tarafından. Ayrıca, topluluk üyeleri bir karar ve onun içeriği tüm geçmişini anlayabilmeniz proje kararları hakkında tartışma arşivlenmiş gerekir.
