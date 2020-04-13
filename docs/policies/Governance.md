---
title: NuGet Proje Yönetimi
description: NuGet'in, taahhüt edenlerin, katkıda bulunanların ve kullanıcıların rolleri ve sorumlulukları da dahil olmak üzere yönetim modeli.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2aaaf41b3fc4ef3621333e5099780b5d7ef393bc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64500391"
---
# <a name="nuget-governance"></a>NuGet yönetimi

> Bu belge Oxford Üniversitesi'nin [Hayırsever Diktatör Yönetim Modeli'ne](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) dayanmaktadır. Bir [Creative Commons Attribution-ShareAlike 2.0 İngiltere: İngiltere & Galler Lisansı](http://creativecommons.org/licenses/by-sa/2.0/uk/)altında lisanslanmıştır.

NuGet projesi hayırsever bir diktatör tarafından yönetilir ve toplum tarafından yönetilir. Diğer bir zamanda, toplum projenin günlük bakımına aktif olarak katkıda bulunur, ancak genel stratejik çizgi hayırsever diktatör tarafından çizilir. Anlaşmazlık durumunda, son sözü hayırsever diktatör söyler.

Toplum içindeki anlaşmazlıkları çözmek ve projenin eşgüdümlü bir şekilde ilerlemesini sağlamak hayırsever diktatörün görevidir. Buna karşılık, toplumun görevi, hayırsever diktatörün kararlarını aktif katılım ve katkı yoluyla yönlendirmektir.

## <a name="roles-and-responsibilities"></a>Roller ve sorumluluklar

Burada açıklanan dört rol vardır: Hayırsever Diktatör, Committers, Katkıda Bulunanlar ve Kullanıcılar.

### <a name="benevolent-dictator"></a>Hayırsever diktatör

NuGet çekirdek ekibi, hayırsever diktatör veya proje lideri olarak kendini atanır. Ancak, topluluk her zaman çatal yeteneğine sahip olduğundan, takım tamamen topluma karşı sorumlu. Proje liderliğinin toplumu bir bütün olarak anlaması ve mümkün olduğunca çok çelişkili ihtiyacı karşılamaya ve projenin uzun vadede ayakta kalmasını sağlaması beklenmektedir.

Pek çok yönden, hayırsever diktatörün rolü diktatörlükten çok diplomasi ile ilgilidir. Önemli olan, proje genişledikçe, doğru insanların bu konuda nüfuz sahibi olmasını ve proje liderliğinin vizyonunun arkasında toplum tarafından miting edeyim. Müşteri adayının görevi, iş verenlerin (aşağıya bakın) proje adına doğru kararları vermelerini sağlamaktır. Genel olarak konuşursak, taahhüt edenler projenin stratejisiyle uyumlu olduğu sürece, proje kurşunu onların istedikleri gibi ilerlemelerini sağlayacaktır.

Ayrıca, .NET Foundation personeli, etki alanı kayıtları ve teknik hizmetler (örn. kod imzalama) dahil olmak üzere iş işlemleri amacıyla nuget için projenin birincil veya ilk temas noktası olduğunu düşünmektedir.

### <a name="committers"></a>Taahhüt edenler

Taahhüt edenler, NuGet'e sürekli değerli katkılarda bulunan ve Hayırsever Diktatör tarafından atanan katkıda bulunankişilerdir. Atandıktan sonra, committers hem depoya doğrudan kod yazmak ve başkalarının katkılarını ekrana güvenilir. Committers genellikle geliştiriciler, ancak başka şekillerde katkıda bulunabilir.

Tipik olarak, bir taahhüter projenin belirli bir yönü üzerinde duruluyor ve onlara toplumun saygısını ve proje liderliğini kazandıracak bir uzmanlık ve anlayış düzeyi getirir. Taahhüt edenin rolü resmi bir değil, sadece toplumun etkili üyelerinin proje kurşun rehberlik ve destek için onlara bakar gibi varsayalım bir pozisyon.

NuGet'in genel yönü söz konusu olduğunda, taahhüt edenlerin hiçbir yetkisi yoktur. Ancak, proje kurşun kulak var. Liderin toplumun ihtiyaçlarının ve kolektif hedeflerinin farkında olmasını sağlamak ve projeye uygun katkıların geliştirilmesine veya ortaya konmasına yardımcı olmak bir taahhütçerin görevidir. Genellikle, committers sorumluluk kendi belirli alanları üzerinde gayri resmi kontrol verilir ve doğrudan kaynak kodun belirli alanları değiştirmek için haklar atanır. Diğer bir nokta, söz edenlerin açık karar verme yetkisi olmamasına rağmen, genellikle eylemlerinin müşteri adayıtarafından alınan kararlarla eş anlamlı olduğunu anlarlar.

### <a name="contributors"></a>Katkıda Bulunanlar

Katkıda bulunanlar, NuGet'e yamalar gönderen topluluk üyeleridir. Bu düzeltme etekleri bir kerelik bir olay olabilir veya zaman içinde oluşabilir. Beklentiler, katkıda bulunanların ilk başta küçük olan ve katkıda bulunan, taahhüt eden ve proje lideri katılımcının yamaları kalitesinde güven oluşturduğunda daha da büyüyen düzeltmeleridir. Katkıda bulunanlar ilişkili ürün sürüm notları belgesinde tanınır.

Bir katılımcının ilk düzeltme eki depoya konmadan önce, [bir Katılımcı Lisans Sözleşmesi](http://en.wikipedia.org/wiki/Contributor_License_Agreement) veya .NET Vakfı'na bir atama sözleşmesi imzalamaları gerekir. Yama sunulabilir ve tartışılabilir, ancak uygun evraklar yerinde olmadan depoya işitedilemez. Katılımcı lisans sözleşmesi almak için lütfen e-posta yoluyla [contributions@nuget.org](mailto:contributions@nuget.org)bir istek gönderin.

Katkıda bulunmak için aşağıdaki depolardan birine çekme isteği gönderin:

- [NuGet İstemci](https://github.com/NuGet/NuGet.Client)
- [NuGet Galerisi](https://github.com/nuget/nugetgallery)
- [NuGet Dokümanlar](https://github.com/nuget/nugetdocs)

Çekme isteği göndermek için ayrıntılı işlem depoya göre değişir:

- [NuGet Client ve NuGet Gallery için katkı talimatları](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [NuGet Dokümanları için katkı talimatları](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Kullanıcılar

Kullanıcılar, paket tüketicileri ve/veya yazarlar olarak NuGet'e ihtiyacı olan ve kullanan topluluk üyeleridir. Kullanıcılar topluluğun en önemli üyeleridir: onlar olmadan, projenin hiçbir amacı olmazdı. Herkes bir kullanıcı olabilir; belirli bir gereksinim yoktur.

Kullanıcılar mümkün olduğunca NuGet ve topluluk hayatına katılmaya teşvik edilmelidir. Kullanıcı katkıları, proje ekibinin bu kullanıcıların gereksinimlerini karşıladıklarından emin olmasını sağlar. Yaygın kullanıcı etkinlikleri aşağıdakileri içerir, ancak bunlarla sınırlı değildir:

- Projenin kullanımını savunmak
- Yeni bir kullanıcının bakış açısından proje güçlü ve zayıf yönleri hakkında geliştiricileri bilgilendirmek
- Manevi destek sağlanması (bir teşekkür uzun bir yol gidiyor)
- Dokümantasyon ve öğreticiler yazma
- Hata raporları ve özellik istekleri dosyalama
- Hata bashes gibi topluluk etkinliklerine katılma
- Tartışma panolarına veya forumlara katılma

Proje ve topluluğuyla etkileşime devam eden kullanıcılar, kendilerini giderek daha fazla işin içinde bulurlar. Bu tür kullanıcılar daha sonra, yukarıda açıklandığı gibi katkıda bulunabilir.

## <a name="package-succession-under-special-circumstances"></a>Özel koşullar altında paket veraset

Bir NuGet hesap sahibinin aciz veya vefat ettiği talihsiz bir durumda, ilgili hesabın tek mülkiyetinin bulunduğu ve paketin OSI onaylı bir lisans altında yayınlandığı pakete uygun sahibi/s'leri eklemek için toplulukla birlikte [çalışacağız.](https://opensource.org/licenses/alphabetical) Sahiplik talebinde bulunmak için bize aşağıdaki belgeleri göndermeniz gerekir:

1. Devlet tarafından verilmiş fotoğraflı kimliğinin fotokopisi.
1. Önceki hesap sahibinin durumunu kanıtlayan aşağıdaki belgelerden biri: 
    - Önceki hesap sahibi vefat etmişse, resmi, devlet tarafından verilmiş bir ölüm belgesi veya
    - Aciz bir hesap sahibinin bakımından sorumlu bir tıp uzmanı tarafından imzalanmış bir belge gibi onaylı bir belge.
1. Mülkiyet hakkınızı kanıtlayan aşağıdaki belgelerden biri: 
    - Hesap sahibinin sağ kalan eşi olduğunuzu gösteren evlilik cüzdanı,
    - İmzalı vekaletname,
    - Sizi vasi veya lehdar olarak adlandıran bir vasiyet veya güven belgesinin fotokopisi,
    - Hesap sahibi nin doğum belgesi, eğer onların ebeveyniyseniz, ya da,
    - Hesap sahibinin yasal vasisiyseniz vesayet evrakları.

Bu politikayı iptal etmek istiyorsanız, lütfen bize kimliği ve [support@nuget.org](mailto:support@nuget.org) paketin sürümünü içeren bir e-posta gönderin.

## <a name="transparency"></a>Saydamlık

Açık kaynak projesinin yönetimine toplumun güvenini niçin inşa etmek, projenin başarısı için hayati önem taşımaktadır. Bu amaçla, karar verme şeffaf, açık bir şekilde yapılmalıdır. Projenin yönü ile ilgili tartışmalar genel olarak yapılmalıdır. Toplum asla Yardımsever Diktatör'ün bir kararıyla hazırlıksız yakalanmamalı. Ayrıca, topluluk üyelerinin bir kararın tüm geçmişini ve içeriğini anlayabilmeleri için proje kararları hakkındaki tartışmalar arşivlenmelidir.
