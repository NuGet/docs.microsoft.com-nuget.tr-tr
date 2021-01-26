---
title: NuGet proje İdaresi
description: Komite, katkıda bulunanlar ve kullanıcılara roller ve sorumluluklar dahil olmak üzere NuGet için idare modeli.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2edaac0218dc936ea6bfe1814c0aab963028ea87
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775597"
---
# <a name="nuget-governance"></a>NuGet idare

> Bu belge, Oxford Üniversitesi tarafından [zararsız olan BenevoödünDictator Idare modelini](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) temel alır. [Creative Commons Attribution-ShareAlike 2,0 UK: England & Wales lisansı](http://creativecommons.org/licenses/by-sa/2.0/uk/)kapsamında lisanslanır.

NuGet projesi bir BenevoödünDictator tarafından sağlanır ve topluluk tarafından yönetilir. Diğer bir deyişle, topluluk projenin günlük bakımına etkin bir şekilde katkıda bulunur, ancak genel stratejik çizgi, benevoödündictator tarafından çizilir. Disevoödündictator, bir anlaşma durumunda son sözcükten oluşur.

Bu, topluluk içindeki anlaşmazlıkların çözülmesi ve projenin eşgüdümlü bir şekilde ilerlemesinin devam ettiğinden emin olmak için benevoödündictator 'in işdir. Buna karşılık, bu, etkin katılım ve katkı aracılığıyla benevocommdictator kararlarına kılavuzluk eden topluluk işdir.

## <a name="roles-and-responsibilities"></a>Roller ve sorumluluklar

Burada açıklanan dört rol vardır: BenevoödünDictator, committers, katkıda bulunanlar ve kullanıcılar.

### <a name="benevolent-dictator"></a>Benevoödündictator

NuGet Core ekibi, BenevoödünDictator veya proje lideri olarak hazırlanmıştır. Ancak, topluluk her zaman çatalla özelliği sağladığından, ekip topluluğa tamamen answerable. Projenin bir bütün olarak topluluğun bir bütün olarak anlaşılması ve projenin uzun vadede daha fazla olması için mümkün olduğunca birçok çakışan gereksinimde karşılanması beklenmektedir.

Birçok şekilde, benevoödündictator 'in rolü, dictatorship hakkında daha az ve daha fazla bilgi. Bu anahtar, projenin genişledikçe doğru kişilerin bunun üzerinde etkisini ve topluluk tarafından proje lideri vizyonunun gerisinde olmasını sağlamaktır. Müşteri adayının işi, bu durumda, komite 'nin (aşağıya bakın) proje adına doğru kararları aldığından emin olur. Genellikle, komite proje stratejisiyle hizalandığı sürece proje lideri, istedikleri gibi ilerleyemez.

Ayrıca, .NET Foundation personeli, etki alanı kayıtları ve teknik hizmetler (örneğin, kod imzalama) dahil iş işlemlerinin amaçları doğrultusunda, projenin NuGet için birincil veya ilk iletişim noktasını gözden geçirin.

### <a name="committers"></a>Yazarlarımız

Komeller, NuGet 'e sürekli değerli katkıları kuran ve BenevocommDictator tarafından bir hayal eden katkıda bulunanlar. Bu konuda, Komite, her ikisi de doğrudan depoya kod yazmak ve diğerlerinin katkılarını ekrana göre belirlenir. Komite, genellikle geliştiricilerdedir ancak başka yollarla katkıda bulunabilir.

Genellikle, bir komite, projenin belirli bir yönünü temel alır ve bir uzmanlık düzeyi getirir ve bu, topluluk ve proje lideri açısından BT 'nin bu şekilde olduğunu öğrenir. Komite rolü resmi bir değil, topluluk üyelerini etkileyen bir konum de proje lideri, rehberlik ve destek için onlara bakar.

Committers, NuGet 'in genel yönlerinin ilgilenme yetkisi yoktur. Ancak, proje liderine sahip olurlar. Bu, müşteri adayının topluluğun ihtiyaçlarını ve toplu amaçlarını farkında olduğundan ve projeye uygun katkıların geliştirilmesi veya bir şekilde yapıldığından emin olmaya yönelik bir işdir. Genellikle, komters, belirli sorumluluk alanlarında resmi olmayan denetim olarak verilirler ve kaynak kodun belirli alanlarında doğrudan değişiklik yapmak için haklar atanır. Diğer bir deyişle, komallara açık karar verme yetkisine sahip olmasa da, genellikle eylemlerinin müşteri adayının yaptığı kararlarla eşanlamlı olduğunu fark ederler.

### <a name="contributors"></a>Katkıda Bulunanlar

Katkıda bulunanlar, NuGet 'e düzeltme ekleri gönderen topluluk üyeleridir. Bu düzeltme ekleri tek seferlik bir oluşum veya zaman içinde meydana gelebilir. Beklentiler, katkıda bulunanların, katılımcı, Komite ve proje lideri, katkıda bulunan yamaların kalitesine göre daha fazla güven elde edildiğinde, ilk başta küçük olan ve daha büyük büyüyerek yamaları göndermektedir. Katkıda bulunanlar, ilişkili ürün sürüm notları belgesinde tanınır.

Bir katkıda bulunan ilk düzeltme eki depoya yerleştirilmeye başlamadan önce, [katılımcı lisans sözleşmesinin](http://en.wikipedia.org/wiki/Contributor_License_Agreement) veya .net Foundation 'a atama sözleşmesinin imzalanmaları gerekir. Düzeltme Eki gönderilebilir ve ele alınabilir, ancak uygun PaperWork yerinde, gerçekten depoya uygulanmamıştır. Katkıda bulunan lisans sözleşmesi almak için lütfen adresine e-posta ile bir istek gönderin [contributions@nuget.org](mailto:contributions@nuget.org) .

Katılımcı olmak için, aşağıdaki depolardan birine bir çekme isteği gönderebilirsiniz:

- [NuGet Istemcisi](https://github.com/NuGet/NuGet.Client)
- [NuGet Galerisi](https://github.com/nuget/nugetgallery)
- [NuGet belgeleri](https://github.com/nuget/nugetdocs)

Çekme isteği göndermeye yönelik ayrıntılı işlem depoya göre değişiklik gösterir:

- [NuGet Istemcisi ve NuGet Galerisi için katkı yönergeleri](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [NuGet belgeleri için katkı yönergeleri](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Kullanıcılar

Kullanıcılar, paket tüketicileri ve/veya yazarlar olarak NuGet kullanması gereken topluluk üyeleridir. Kullanıcılar topluluğun en önemli üyeleridir: Bunlar olmadan, projenin amacı yoktur. Herkes bir kullanıcı olabilir; belirli bir gereksinim yoktur.

Kullanıcıların, NuGet ve topluluğun kullanım ömrü boyunca mümkün olduğunca katılması önerilir. Kullanıcı katkıları, proje ekibinin bu kullanıcıların ihtiyaçlarını yerine getirdikten emin olmasını sağlar. Ortak Kullanıcı etkinlikleri aşağıdakileri içerir ancak bunlarla sınırlı değildir:

- Projenin kullanımı için advotonlu
- Yeni bir kullanıcının perspektifinden proje gücü ve zayıf noktalar geliştiricilere bilgilendirin
- Moral desteği sağlama (uzun bir şekilde teşekkür ederiz)
- Belge ve öğreticiler yazma
- Hata raporlarını ve özellik isteklerini dosyalama
- Hata bashes gibi topluluk olaylarına katılım
- Tartışma panoları veya forumlarında katılım

Proje ve topluluğuyla birlikte çalışmaya devam eden kullanıcılar genellikle kendilerini daha fazla ve daha fazlasını bulacaktır. Bu tür kullanıcılar daha sonra, yukarıda açıklandığı gibi katkıda bulunanlar olmaya devam edebilir.

## <a name="package-succession-under-special-circumstances"></a>Paket özel koşullarda birbirini izleyen

Bir NuGet hesabı sahibinin ya da öldü olduğu talihsiz durumunda, topluluk ile birlikte çalışacağız. Bu, söz konusu hesabın tek sahipliğe sahip olduğu ve paketin bir [OSI onaylanmış lisans](https://opensource.org/licenses/alphabetical)kapsamında yayımlandığı pakete uygun sahip/s eklemek için sizinle birlikte çalışacağız. Sahiplik istemek için aşağıdaki belgeleri bize göndermeniz gerekir:

1. Devlet tarafından verilen fotoğraf KIMLIĞININ photobir kopyası.
1. Aşağıdaki belgelerden biri önceki hesap sahibinin durumunu kanıtlama: 
    - Önceki hesap sahibi öldü veya ise, resmi olarak verilen bir ölüm sertifikası
    - Bir sağlık uzmanı tarafından imzalanan, bir hesap sahibinin ilgilendiğini kabul eden bir sertifika gibi sertifikalı bir belge.
1. Aşağıdaki belgelerden biri, sahipliğine sahip olma hakkını sağlar: 
    - Hesap sahibinin daha fazla eş tutan eşinin olduğunu gösteren Marriage sertifikası,
    - Attorney 'ın imzalı gücü,
    - Bir veya daha fazla Lehli belge adlandırmanın bir kopyasını,
    - Hesap sahibi için Doğum sertifikası, üst öğesi veya,
    - Hesap sahibinin yasal bir koruyucu ise, guardiangemari.

Bu ilkeyi çağırma gereksinimiyle ilgili bilgi edinmek istiyorsanız lütfen [support@nuget.org](mailto:support@nuget.org) PAKETIN kimliği ve sürümü ile birlikte bize e-posta gönderin.

## <a name="transparency"></a>Şeffaflık

Bir açık kaynaklı projenin idaresinde topluluk güveni oluşturmak, başarısı için hayati öneme sahiptir. Bu uçta, karar verme, saydam ve açık bir biçimde yapılmalıdır. Projenin yönü hakkında tartışma genel olarak yapılmalıdır. Topluluk, BenevocommDictator tarafından hiçbir kararı vererek hiçbir şekilde hiçbir şekilde yakalanmamalıdır. Ayrıca, topluluk üyelerinin bir kararın ve bağlamının tüm geçmişini anlayabilmesi için proje kararlarının tartışılması gerekir.
