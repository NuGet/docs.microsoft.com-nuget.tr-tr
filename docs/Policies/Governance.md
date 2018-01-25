---
title: "NuGet proje yönetimi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Roller ve sorumluluklar committers, Katkıda Bulunanlar ve kullanıcılar için de dahil olmak üzere NuGet için idare modeli."
keywords: "NuGet idare, NuGet benevolent dictator, committer sorumlulukları, katkıda bulunan sorumlulukları, kullanıcı sorumlulukları"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ea1ddcc3e145afe3b905b23db37e1e61500200bb
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-governance"></a>NuGet idare

> Bu belge temel aldığı [Benevolent Dictator idare modeli](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) , University Oxford tarafından. Altında lisanslanmıştır bir [Creative Commons Attribution ShareAlike 2.0 İngiltere: İngiltere & İngiltere lisans](http://creativecommons.org/licenses/by-sa/2.0/uk/).

NuGet proje Benevolent Dictator tarafından öncülük ve topluluk tarafından yönetilir. Diğer bir deyişle, topluluk, proje günlük bakım için etkin bir şekilde katkıda bulunur, ancak genel stratejik çizgi benevolent dictator çizilir. Çözünürlüğünün durumunda, son sözcük benevolent dictator sahiptir.

Bu benevolent dictator'ın iş topluluk içinde itirazları çözümlemek için ve projeyi koordineli bir şekilde devam edebilir olduğundan emin olmak için olur. Buna karşılık, etkin katılım ve katkı aracılığıyla benevolent dictator kararları kılavuza topluluk'ın iş ediyor.

## <a name="roles-and-responsibilities"></a>Roller ve sorumluluklar

Burada açıklanan dört rolleri vardır: Benevolent Dictator, Committers, Katkıda Bulunanlar ve kullanıcılar.

### <a name="benevolent-dictator"></a>Benevolent dictator

NuGet çekirdek takım Benevolent Dictator ya da proje lideri olarak kendi kendine kaldırmasını ' dir. Ancak, topluluk her zaman çatalı yeteneğine sahip olduğundan, takım topluluğuna tam olarak yanıtlanamaz. Proje lideri bir bütün olarak topluluk anlamak ve çakışan birçok gereksinimleriniz değiştikçe mümkün olduğunca proje uzun vadede şekilde kalmıştır sağlarken karşılamak çalışmalarımızı beklenir.

Birçok yolla benevolent dictator rol dictatorship ve diplomacy hakkında daha fazla küçük. Proje genişlediği sürece doğru kişilerin ele etkisi verilir ve topluluk proje lideri görme rallies, anahtar sağlamaktır. Müşteri adayın iş sonra (aşağıya bakın) committers doğru proje adına kararlar emin emin olmaktır. Committers projenin stratejisi ile hizalanır sürece, genel olarak bakıldığında, proje lideri istenen şekilde devam etmesine imkan tanıyacak.

Ayrıca, .NET Foundation Personel proje lideri NuGet iletişim etki alanı kayıtlar ve teknik Hizmetleri (örneğin kod imzalama) dahil olmak üzere iş işlemlerinin amacıyla birincil ya da ilk noktası göz önünde bulundurun.

### <a name="committers"></a>Committers

Committers kimin sürekli değerli Katkıları Nuget'e yaptıysanız ve Benevolent Dictator tarafından tayin katkıda bulunanlar ' dir. Bir tayin, committers üzerine hem depoya doğrudan kod yazmak ve diğer Katkıları ekran dayanıyordu. Committers geliştiriciler genellikle olan ancak diğer yollarla katkıda bulunabilir.

Genellikle, bir committer proje belirli bir yönüne odaklanır ve uzmanlık ve topluluk ve proje lideri saygı kazandığı anlama düzeyini getirir. Committer rol resmi bir değil, yalnızca proje sağlama arar bunlara yönerge ve Destek olarak etkili topluluk üyeleri varsayın bir konum.

Burada NuGet genel yönünü kaygı yetkisi yok committers var. Ancak, proje lideri kulak vardır. Bu committer'ın işinin sağlama topluluk'in gereksinimlerini ve toplu hedefleri farkında olduğundan emin olun ve geliştirme ya da uygun Katkıları projeye tasarlanmalıdır yardımcı olur. Genellikle, committers kendi belirli sorumluluk alanları üzerinde resmi olmayan denetim verilir ve kaynak kodunun belirli alanları doğrudan değiştirmek için hakları atanır. Committers açık karar verme yetkisine sahip değil rağmen diğer bir deyişle, bunlar genellikle eylemlerini tarafından sağlama kararlara ile eşanlamlıdır bulur.

### <a name="contributors"></a>Katkıda Bulunanlar

Katkıda Bulunanlar NuGet düzeltme eklerini gönderen topluluk üyeleridir. Bu düzeltme ekleri zaman içinde oluşan veya bir kerelik geçişi olabilir. Beklentileri olduğunuz katkıda bulunanlar küçük düzeltme ekleri gönderme ilk ve katkıda bulunan, committers ve proje lideri katkıda bulunanlar düzeltme ekleri kalitesini güveni yerleşik gerektiğinde büyük büyütün. Katkıda Bulunanlar ilişkili ürün sürüm notları belgede tanınır.

Depoya katkıda bulunanlar ilk düzeltme eki yerleştirmeden önce oturum bir [katkıda bulunan Lisans Sözleşmesi'ni](http://en.wikipedia.org/wiki/Contributor_License_Agreement) veya .NET Foundation atama sözleşme. Düzeltme eki gönderildi ve ele alınan ancak aslında deponuza yerinde uygun belgeleri olmadan kaydedilmiş olamaz. Katkıda bulunan Lisans Sözleşmesi'ni almak için lütfen bir istek için e-posta gönderebilirsiniz [ contributions@nuget.org ](mailto:contributions@nuget.org).

Katılımcı olmasını aşağıdaki depoları biri için bir çekme isteği gönder:

- [NuGet Client](https://github.com/NuGet/NuGet.Client)
- [NuGet Galerisi](https://github.com/nuget/nugetgallery)
- [NuGet belgeleri](https://github.com/nuget/nugetdocs)

Bir çekme isteği göndermek için ayrıntılı işlem Deposu değişir:

- [NuGet istemcisiyle NuGet galerisinde katkı yönergeleri](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [NuGet belgeleri için katkı yönergeleri](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Kullanıcılar

İhtiyacı olan ve NuGet, paket tüketiciler ve/veya yazarlar kullanma topluluk üyeleri kullanıcılardır. Kullanıcılar en önemli topluluk üyeleri olan: onlar olmadan proje herhangi bir amacı olurdu. Herhangi bir kullanıcı olabilir; belirli gereksinimler yoktur.

Kullanıcılar, NuGet ve mümkün olduğunca topluluk hayatta katılmaya teşvik. Kullanıcı Katkıları bu kullanıcıların ihtiyaçlarını karşılayan emin olmak proje ekibi etkinleştirin. Genel kullanıcı etkinlikleri içerir, ancak bunlarla sınırlı değildir:

- Proje kullanıma advocating
- Proje güçlü ve yeni kullanıcı açısından zayıf geliştiricileri bildiren
- (Teşekkür ederiz depoladıysanız gider) moral desteği sağlama
- Yazma belgeler ve öğreticiler
- Hata raporları ve özellik istekleri dosyalama
- Hata bashes gibi topluluk olayları katılma
- Katılan tartışma panoları veya forumları

Proje ve kendi topluluk bulunmaya devam kullanıcılar genellikle kendilerini daha da fazla dahil olma bulur. Bu tür kullanıcılar sonra Katkıda Bulunanlar, yukarıda açıklandığı gibi olmasını geçin.

## <a name="package-succession-under-special-circumstances"></a>Paket art arda özel koşullarda

Burada bir NuGet hesap sahibi incapacitated veya vefat talihsiz durumda, biz burada konusu hesabı tek sahipliği var. ve paket altında yayımlanan paket uygun sahibi/s eklemek için topluluğuyla karşılaşmayacağınızı bir [OSI Lisans onaylanan](https://opensource.org/licenses/alphabetical). Sahipliği istemek için bize aşağıdaki belgeler göndermeniz gerekir:

1. Kamu verilen fotoğraf kimliğinizi, fotokopi
1. Önceki hesap sahibinin durum kanıtlama aşağıdaki belgeler biri: 
    - Bir resmi, devlet verilen ölüm sertifika önceki hesap sahibi ölüm, ise veya
    - TIP professional incapacitated hesap sahibi dikkatli sorumlu tarafından imzalanmış bir sertifika gibi sertifikalı bir belge.
1. Sahipliği, sağda kanıtlayan aşağıdaki belgeler biri: 
    - Hesap sahibinin kalan eşinin olduğunu gösteren marriage sertifika
    - İmzalı güç of avukata
    - Yürütücü veya lehtar olarak adlandırma ya da güven belgenin kopyasını,
    - Kendi üst varsa hesap sahibi için Doğum sertifikası veya
    - Hesap sahibinin yasal koruyucu varsa guardianship belgeleri.

Lütfen bize bir e-postası gönderin kendinizi bu ilkeyi çağırma gerekli bulursanız, [ support@nuget.org ](mailto:support@nuget.org) kimliği ve paketin sürümü.

## <a name="transparency"></a>Saydamlık

Açık kaynaklı bir projeyi idare topluluk güven oluşturma kendi başarısı için önemlidir. Bu amaçla kararlar saydam, açık bir şekilde yapılması gerekir. Projenin yönü hakkında tartışma genel olarak yapılmalıdır. Topluluk hiçbir zaman yakalanan hazırlıksız karar Benevolent Dictator tarafından tarafından. Ayrıca, topluluk üyeleri tüm geçmişini kararı ve onun bağlamı anlayabileceği böylece proje kararlarını hakkında tartışma arşivlenmiş gerekir.
