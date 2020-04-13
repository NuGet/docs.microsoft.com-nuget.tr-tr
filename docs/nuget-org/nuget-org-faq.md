---
title: NuGet.org Sık Sorulan Sorular
description: NuGet galerisiile çalışmak için sık sorulan sorular ve yanıtlar.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428907"
---
# <a name="nugetorg-frequently-asked-questions"></a>sık sorulan sorulara NuGet.org

## <a name="license-terms"></a>Lisans koşulları

**Bir paket belirli lisans bilgileri sağlamazsa varsayılan lisans koşulları nelerdir?**

Her paket, pakete dahil edilen koşullara tabidir. Paketlere erişmeden, indirmeden veya satın almadan önce geçerli koşulları gözden geçirmelisiniz. NuGet.org, paket sayfasındaki **Lisans Bilgileri** bağlantısını kullanın.

Bir paket lisans koşullarını belirtmiyorsa, NuGet.org paket sayfasındaki **İletişim sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılardan size herhangi bir fikri mülkiyet lisansı vermez ve üçüncü taraflarca sağlanan bilgilerden sorumlu değildir.

## <a name="managing-packages-on-nugetorg"></a>paketleri NuGet.org yönetme

**Paket meta verilerini yüklendikten sonra yeniden yükleyebilir miyim?**

NuGet tüm paketlerin imzalanmasını önerir. Paket imzalamanın tasarım prensibi, imzalanan paket içeriğinin nuspec içeren değişmez olması gerektiğidir. Paket meta verilerinin düzenlenmesi, varolan imzaları geçersiz kAkarak nuspec'te değişikliklere neden olabilir. Paket oluşturulduktan sonra paket meta verilerinin düzenlenmesini gerektirmeyecek şekilde varolan iş akışlarını değiştirmenizi öneririz.

Paketiniz için listelenen bağımlılıkların paketin kendisinden otomatik olarak oluşturulduğunu ve düzenlenemeyeceğini unutmayın.

Buna ek olarak, [paketleri int.nugettest.org](https://int.nugettest.org) yüklemek, genel galeride bir paket oluşturmadan paketinizi test etmek ve doğrulamak için harika bir yoldur. API Bitiş Noktası:https://apiint.nugettest.org/v3/index.json

**NuGet.org için yayınlanan bir paketi silebilir miyim?**

Genel olarak, NuGet.org için yayınlanan bir paketin silmesidestekliyoruz. Paketleri silme [politikamız](policies/deleting-packages.md)hakkında daha fazla bilgi edinin.

**Gelecekte yayınlanacak paketler için ad ayırmak mümkün mü?**

Evet. Hesabınız için bir paket kimlik öneki isteyerek [NuGet.org](https://www.nuget.org/) paketleri için kimlik rezerve edebilirsiniz. Paket kimlik öneki istemek için [belgelerdeki](id-prefix-reservation.md)yönergeleri izleyin.

**Paketler için sahiplik talebinde nasıl bulunurum?**

Bkz. [NuGet.org'da paket sahiplerini yönetme.](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)

**Yazılım lisansımı ihlal eden bir paket sahibiyle nasıl başa çıkacağım?**

NuGet topluluğunu, paket sahipleri ve diğer yazılım sahipleri arasında ortaya çıkabilecek anlaşmazlıkları çözmek için birlikte çalışmaya teşvik ediyoruz. NuGet.org yöneticilerinin arabuluculuk yapmasını istemeden önce takip etmesi gereken bir [uyuşmazlık çözüm süreci](policies/dispute-resolution.md) hazırlıyoruz.

**Test paketlerimi NuGet.org yüklemem önerilir mi?**

Test amacıyla, [int.nugettest.org](https://int.nugettest.org)veya [myget.org](https://myget.org) veya [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)gibi alternatif genel NuGet sunucularını kullanabilirsiniz.

int.nugettest.org yüklenen paketlerin korunamayabileceğini unutmayın.

**NuGet.org yükleyebileceğim maksimum paket boyutu nedir?**

NuGet.org 250MB'a kadar paketlere izin verir, ancak paketleri mümkünse 1MB'nin altında tutmanızı ve paketleri birbirine bağlamak için bağımlılıkları kullanmanızı öneririz. Başparmak kuralı olarak, paketler çakışmaları önlemek için yalnızca bir derleme içerir.

NuGet paketleri indirmek için HTTP kullanır, böylece daha büyük paketler küçük olanlardan daha başarısız yüklemeolasılığı daha yüksektür.

Birden çok paket arasındaki bağımlılıkları paylaşmak mümkündür, bu da NuGet paketlerinizin tüketicileri için toplam indirme boyutunu küçülttü.

Bağımlılıklar çoğunlukla statiktir ve asla değişmez. Bir hatayı kodda düzeltirken, bağımlılıkların güncelleştirilmesi gerekmeyebilir. Bağımlılıkları paketlerseniz, her seferinde daha büyük paketleri yeniden gönderebilirsiniz. NuGet paketlerini ilgili bağımlılıklara bölerek, yükseltmeler paketinizin tüketicileri için çok daha ince taneli hale getirilmiştir.

## <a name="nugetorg-not-accessible"></a>NuGet.org erişilemedi

**NuGet.org'a neden paket indiremiyorum veya paket yükleyemiyorum?**

Öncelikle NuGet'in en son sürümlerini kullandığınızdan emin olun. Bu sürüm başarısız olmaya devam ederse, [desteğe başvurun](https://www.nuget.org/policies/Contact) ve şular dahil olmak üzere ek bağlantı sorun giderme bilgileri sağlayın:

- Kullanmakta olduğunuz NuGet sürümü
- Kullanmakta olduğunuz paket kaynakları
- Ayrıntılı ayrıntılı ayrıntılı lık içeren bir geri yükleme günlüğü
- MTR veya Fiddler izleri (aşağıya bakın)
- Coğrafi bölgeniz
- Makinenizin proxy veya güvenlik duvarının arkasında olup olmadığı?
- Makineniz bulut sağlayıcılarının veri merkezinde (Azure, AWS vb.) mi bulunuyor? Evet ise, lütfen sağlayıcının ve bölgenin adını verin.

*MTR'yi yakalamak için:*

- [WinMTR'yi](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download)indirin.
- Ana `api.nuget.org` bilgisayar adı olarak girin ve **Başlat'ı**tıklatın.
- **Gönderilen** sütun >= 100 olana kadar bekleyin.

    ![MTR yakalama](media/mtr.png)

- Metni panoya kopyalayın.

*Fiddler'ı yakalamak için:*

- [Fiddler'ın](https://www.telerik.com/download/fiddler)en son sürümünü yükleyin.
- **Dosya > Capture Traffic** menüsünü kullanarak Fiddler'ı başlatın ve trafiği yakalamayı devre dışı bulun.
- Tüm oturumları kaldırın (listedeki tüm öğeleri seçin, **Sil** tuşuna basın).
- **Araçlar > Fiddler Options menüsünün** **HTTPS** sekmesinde Şifre çözme HTTPS trafiğini kontrol ederek Fiddler'ı HTTPS **trafiğini** yakalamak için Fiddler'ı yapılandırın.
- Visual Studio’yu kapatın.
- Trafiği Yakalama menüsünü **> Dosya'yı** etkinleştirin.
- Visual Studio veya nuget.exe .exe'yi başlatın ve çalışmayan eylemleri gerçekleştirin. Bu eylemler tarafından oluşturulan trafik Fiddler'da görünmelidir.
- Eylemler çalıştırdıktan sonra, yakalanan oturumları depolamak için **Dosya > Kaydet > Tüm Oturumları** kullanın.

Not: Fiddler üzerinden `HTTP_PROXY` NuGet `http://127.0.0.1:8888` trafiğini yönlendirmeiçin ortam değişkenini ayarlamak gerekebilir.

Bu başarısız olursa, [bu StackOverflow sonrası belirtilen ipuçlarını](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)deneyin.

## <a name="nugetorg-account-management"></a>NuGet.org hesap yönetimi

### <a name="how-to-recover-nugetorg-password-login"></a>NuGet.org şifre girişi nasıl kurtarılır?

[Parola girişinin NuGet.org durdurulduğunu](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) ve NuGet.org giriş yapmanın tek yolunun kişisel bir Microsoft hesabı (MSA) veya Azure Active Directory (AAD) hesabı olduğunu lütfen unutmayın. Ancak, ilişkili MSA/AAD hesaplarınıza erişemiyorsanız, NuGet.org hesabınızı kurtarmak için parola girişi kullanmanız gerekebilir. Bu durumda aşağıdaki adımları izleyin.
- **Gereksinim:** Parolayı kurtarmanız gereken hesapla ilişkili e-postaya erişmeniz gerekir.
- [Şifreyi Unuttum sayfasına](https://www.nuget.org/account/ForgotPassword) git
- Kurtarmak istediğiniz NuGet.org hesabıyla ilişkili **e-posta** adresini girin.
- **Gönder** düğmesini tıklatın.
- Parolanızı sıfırlamak için bir bağlantı ile belirtilen e-posta adresi hesabına bir e-posta alırsınız. Bu bağlantıyı tıklatın ve yeni şifreyi ayarlayın. Postayı bulamıyorsanız "önemsiz" klasörünüzü kontrol edin.
- Bir kez yapıldıktan sonra, artık NuGet kullanıcı adı / şifre ile giriş yapabilirsiniz.
- Kullanıcı adı/parola ile giriş yapmak için, NuGet.org giriş [sayfasındaki](https://www.nuget.org/users/account/LogOn)Nuget.org hesap bağlantısını **kullanarak Oturum Aç'ı** kullanın.

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Hangi Microsoft hesabı NuGet.org hesabıma bağlı?

NuGet.org hesabınızla hangi Microsoft hesabının ilişkili olduğunu unuttuysanız, yardım almak için lütfen aşağıdaki adımları izleyin.
1. Giriş [NuGet.org](https://www.nuget.org/users/account/LogOn) sayfasına gidin ve **YardımA Gerek'i tıklayın?**
1. Bu, yardım için açılır iletişim kutusunu gösterir. NuGet.org hesabınızla ilişkili Microsoft hesabının(lar) anlaşılması için bu iletişim kutusundaki adımları izleyin.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Giriş için kullandığım Microsoft hesabını NuGet.org nasıl değiştirilir?
NuGet.org kullanıcı için Microsoft hesabını değiştirmek istiyorsanız, aşağıdaki adımları izleyin. E-posta `account1@outlook.com` ile Microsoft hesabınızın kullanıcı adı `MyNuGetAccount`ile NuGet.org hesabınızla ilişkili olduğunu varsayalım. E-posta ile başka bir Microsoft hesabına giriş değiştirmek istiyorsanız`account2@outlook.com`
1. Lütfen **Microsoft ile Oturum Aç'ı**tıklattıktan sonra giriş [sayfasında](https://www.nuget.org/users/account/LogOn) **şu anda ilişkili Microsoft hesabını** `account1@outlook.com` kullanarak oturum açın.
1. Oturum açtıktan sonra [hesap ayarları](https://www.nuget.org/account) sayfanıza gidin.
1. **Giriş Hesabı**bölümünü genişletin. **Hesabı Değiştir** düğmesine tıklayın.
1. Artık microsoft giriş sayfasına yönlendirileceksiniz. Lütfen ilişkilendirme yi değiştirmek istediğiniz hesapla oturum açın. `account2@outlook.com` **Not**: Farklı bir Microsoft hesabıyla oturum açabilmek için oturum açma akışı sırasında Oturum Aç'a tıklayıp **farklı hesaplarla oturum açmanız** gerekebilir.
1. Aşağıdaki gibi bir hata görürseniz, microsoft hesabının daha fazla ayrıntı için [başka bir NuGet.org hesabıyla bağlantılı olduğunu](#microsoft-account-is-linked-with-another-nugetorg-account) görün.
    >_Microsoft hesabını 'account2' <account2@outlook.com>ile güncelleştirmeyi başaramadı. Zaten başka bir NuGet hesabına bağlı ise bu olabilir. Daha fazla bilgi için desteğe başvurun._

1. İkinci hesabınızla başarılı bir şekilde oturum açtıktan sonra, NuGet.org hesap ayarları sayfanıza geri yönlendirilirsiniz ve artık giriş hesabı olarak ilişkili yeni Microsoft hesabını görmeniz gerekir. İleriye dönük olarak, NuGet.org oturum açken bu hesabı kullanmalısınız.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft hesabı başka bir NuGet.org hesabıyla bağlantılıdır.

Microsoft oturumunuzu değiştirmeyi denediyseniz ve aşağıdaki hatayı gördüyseniz:
> _Microsoft hesabını 'account2' <account2@outlook.com>ile güncelleştirmeyi başaramadı. Zaten başka bir NuGet hesabına bağlı ise bu olabilir. Daha fazla bilgi için desteğe başvurun._

Kullanıcı adı `account1@outlook.com` `MyNuGetAccount1` olan NuGet.org kullanıcı için Microsoft hesap oturum açmanızı e-posta `account2@outlook.com`ile başka bir Microsoft hesabına değiştirmeye çalıştığınızı varsaalım. Ve yukarıdaki hatayı görüyorsunuz.

**Yukarıdaki hata ne anlama geliyor?**

Bu, Microsoft hesabıyla ilişkili başka bir NuGet.org hesabı olduğu anlamına gelir, bu hesabı değiştirmeye çalıştığınız başka `<account2@outlook.com>` bir NuGet.org hesabı, örneğin yukarıdaki örnekte e-posta ile Microsoft hesabı, örneğin, kullanıcı adı `MyNuGetAccount2`ile başka bir NuGet.org hesabı ile ilişkilidir.

İlişkili girişi farklı bir NuGet.org hesabına bağlı bir Microsoft hesabıyla değiştiremezsiniz.

**Başka bir NuGet.org hesabım olduğunu unuttum, hangi NuGet.org hesabı olduğunu nasıl öğrenebilirim?**

Giriş sayfasında ikinci Microsoft hesabı ile [giriş](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "giriş sayfası")yapın. Bu, şu anda ikinci Microsoft hesabıyla ilişkili NuGet.org hesabına giriş yapmanızdır. Daha sonra yüklenen paketleri görüntüleyebilir ve bu hesapta hesap yönetimini gerçekleştirebilirsiniz.

**Ben bu ikinci NuGet.org hesabı umurumda değil, ben ikinci Microsoft hesabı ile ilk NuGet.org hesabı için giriş değiştirmek istiyorum. Ne yapacağım?**

İkinci NuGet.org hesabı önemsemiyorsanız ve yine de ilişkili Microsoft hesabını e-posta `account2@outlook.com`ile yeniden kullanmak istiyorsanız. 

NuGet.org hesabını silerek Microsoft hesabı ile NuGet.org hesabı arasındaki ilişkilendirme serbest bırakabilirsiniz.
1. İkinci NuGet.org hesabı `MyNuGetAccount2`için [kullanıcıyı silmek](#how-to-delete-my-nugetorg-account) için adımları izleyin. 
1. Bu hesap silindikten sonra, [Microsoft hesap oturum açma](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)adımlarını yeniden deneyebilirsiniz.

**Bekle, ben de bu ikinci hesabı önemsiyorum. Bu hesabı kaybetmek istemiyorum, ancak ilk hesap için ilişkili hesap girişlerimi değiştirin.**

E-posta `account3@outlook.com`ile üçüncü bir Microsoft hesabı oluşturmanız/kullanmanız gerekir. 
1. İlk olarak, `account2@outlook.com` NuGet.org'da ikinci Microsoft hesabınızla giriş yapmalısınız. İlişkili girişleri değiştirmek ve üçüncü Microsoft hesabını bu NuGet.org hesabıyla ilişkilendirmek için yukarıdaki adımları izleyin.
1. Bir kez yapılırsa, `account2@outlook.com` e-posta ile ikinci Microsoft hesabı `MyNuGetAccount1`ilk NuGet.org hesabınızla ilişkili olmak ücretsizdir. Microsoft oturum açmaoturumlarını ikinci Microsoft hesabına değiştirmek için yukarıdaki adımları izleyin.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Microsoft hesabıyla oturum açma, e-postamın başka bir Microsoft hesabına bağlı olduğunu gösterir

Microsoft hesabınızla oturum açmayı denediyseniz, mesela `account1@outlook.com` e-postayla oturum açın ve aşağıdaki gibi bir hata görürsünüz:
> _E-posta 'account1@outlook.com' ' hesabı başka bir microsoft hesabıyla bağlantılıdır._
>
> _Bağlantılı Microsoft hesabını güncelleştirmek istiyorsanız, bunu hesap ayarları sayfasından yapabilirsiniz._

**Yukarıdaki hata ne anlama geliyor?**

NuGet.org bir hesap oluşturulduğunda, bu hesapla ilişkili bir iletişim e-posta adresi vardır. Bu genellikle ilişkili Microsoft hesabı için kullanılan e-posta adresiyle aynıdır. Ancak, iletişim için farklı bir e-posta adresi belirtmeyi seçebilirsiniz. Yani, teknik olarak, farklı bir Microsoft hesabı `account2@outlook.com` olabilir, bu iletişim e-posta `account1@outlook.com`adresi ile NuGet.org hesaba bağlı olduğunu söylüyorlar .

Yani yukarıdaki hata zaten iletişim e-posta adresi `account1@outlook.com` ile NuGet.org hesabı var ama **e-posta** `account1@outlook.com`ile başka bir Microsoft hesabı ile ilişkili olduğu anlamına gelir .

**Hangi Microsoft hesabının bu NuGet.org hesaba bağlı olduğunu nasıl bulabilirim?**

E-posta [sign in assistance](#which-microsoft-account-is-linked-to-my-nugetorg-account) adresiyle `account1@outlook.com`NuGet.org hesabına hangi Microsoft hesabının bağlı olduğunu anlamak için oturum açma yardımı akışını kullanmalısınız.

**Microsoft hesabımla bu hesabı geçersiz kılmak istiyorum**

Microsoft giriş kullanamayan adımları izleyin, Microsoft hesabınızı mevcut NuGet.org hesabıyla ilişkilendirmek için NuGet.org hesabım bölümünü [nasıl kurtarabilirim.](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Microsoft girişi kullanamıyor, NuGet.org hesabımı nasıl kurtarabilirim?

[Oturum açma yardımını](#which-microsoft-account-is-linked-to-my-nugetorg-account) kullanmayı denediyseniz ve NuGet.org hesabınızla ilişkili Microsoft hesabına erişiminiz yoksa, yeni bir Microsoft hesabını NuGet.org hesabınıza bağlamak için lütfen aşağıdaki adımları izleyin.
1. **Gereksinim**: Varolan NuGet.org hesaplarıyla ilişkili olmayan bir Microsoft hesabına erişmeniz gerekir. Eğer yoksa, bir [oluşturabilirsiniz.](https://signup.live.com)
2. NuGet.org hesabınızın kullanıcı adını ve şifrenizi unuttuysanız, [parolanızı yeniden kaydetme adımlarını](#how-to-recover-nugetorg-password-login)izleyin.
3. Kullanıcı adı/şifre girişi kullanarak [NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) giriş yapın.
4. Oturum açtıktan sonra, açılır pencereiletişiminin aşağıdaki gibi göründüğünü görürsünüz. Bu, parola kesme iletişim kutusudur.
5. **NOT**: Lütfen belirtilen Microsoft hesabıyla giriş talimatını yoksayın. Artık NuGet.org hesabınızı başka bir Microsoft girişine bağlayabilirsiniz.
6. Microsoft ile **Oturum Aç** düğmesine tıklayın ve adım 1'de belirtildiği gibi erişebildiğiniz Microsoft hesabıyla oturum açın.
7. Hesabınız artık, ileriye dönük olarak oturum açmak için kullanabileceğiniz yeni Microsoft hesabına NuGet.org bağlı olacaktır.

    ![Bağlantı MSA İletişim](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>NuGet.org hesabımı bir kuruluşa dönüştürme nasıl?

Hesabınızı bir kuruluşa dönüştürmek istiyorsanız ve bu hesap zaten bir Microsoft hesabı girişiyle ilişkiliyse, lütfen [nuget org'daki kuruluşlar](organizations-on-nuget-org.md)için belgelerde verilen adımları izleyin.

Ancak, NuGet.org hesabınız bir Microsoft hesabıyla ilişkili değilse/bunlara bağlı değilse, bu hesabı bir kuruluşa dönüştürmek için aşağıdaki adımları izleyebilirsiniz.
1. **Gereksinim**: Org hesabında yönetici olarak kullanılmak üzere önce NuGet.org bireysel bir hesap oluşturmanız gerekir. Hesabınız yoksa, lütfen [yeni bir NuGet.org hesabı oluşturun](individual-accounts.md)
2. NuGet.org hesabınız için [parola girişi](#how-to-recover-nugetorg-password-login) nin ardından gelen adımları izleyin, parola girişi yoksa, bunu yaparsanız bu adımı atlayın.
3. Kullanıcı adı/şifre girişi kullanarak [NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) giriş yapın.
4. Oturum açtıktan sonra, açılır pencereiletişiminin aşağıdaki gibi göründüğünü görürsünüz. Bu, parola kesme iletişim kutusudur. 
    > [!Important]
    > Bu iletişim kutusunu yoksay, **Microsoft düğmesiyle Oturum Aç'a tıklamayın.** **do not**

5. [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)Git. Bu, NuGet.org hesabını bir Microsoft hesabına bağlanmadan bir org'a dönüştürmenize olanak sağlar.
6. Adım 1'de oluşturduğunuz kişisel NuGet.org hesabınızın/hesabınızın yönetici kullanıcı adını belirtin.
7. Bu hesabın bir kuruluşa dönüşümünün tamamlanması için yönergeleri izleyin.

    ![Bağlantı MSA İletişim](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Yönetilmeyen kiracıile AAD hesapları için giriş sorunları NuGet.org?

E-posta hesabı etki alanınızla giriş akışınız sırasında@yourdomain.comaşağıdaki gibi bir hata görürseniz, NuGet.org hesabınızı kurtarmak için aşağıdaki adımlara bakın.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Oturum açma sırasında bu yönetilmeyen durum olayı nedir? Peki bu neden şimdi oluyor?** 

Hesabınız daha önce kişisel bir Microsoft hesabı olarak kaydedilmiş gibi görünüyor ve iyi çalıştı, ancak şimdi hesabınız Azure Etkin Dizini'nde (Microsoft hesaplarını doğrulamak için kullandığımız kimlik hizmeti) "Yönetilmeyen" kiracı olarak kaydedilmiş gibi görünüyor. 

Bu durum, siz veya kuruluşunuzdaki @yourdomain.com (e-posta adresiyle) AAD tümleşik hizmetlerinden birine kaydolmuş veya azure [Active Directory için kendi servis kaydı](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup)yapmışsa (sizin@yourdomain.com durumunuzda) kullanılmış Microsoft hesap etki alanı için böyle bir "Yönetilmeyen" kiracı oluşturmuşsa bu durum olabilir. 

**Hesabımı kurtarmak için ne yapabilirim?**

Şu anda Azure Etkin dizininde bu tür "Yönetilmeyen" kiracı hesaplarına sahip hesapların kimliğini doğrulamanın (NuGet.org) bir yolu yoktur. Bu tür hesapları doğrulamak için daha iyi bir yol arıyoruz.

Microsoft hesabınızla@yourdomain.comNuGet.org oturum açmak istiyorsanız, "" e-posta@yourdomain.comadresi olan kullanıcıların kimliğini doğrulamak için bir DNS doğrulaması yaparak AAD'nin mülkiyetini talep etmeniz gerekir. Azure Etkin dizini tarafından belgelenen [etki alanları yöneticisi devralma](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) adımlarını izleyin. Bu işlem yapıldıktan sonra, normal oturum açma nız çalışmaya başlamalıdır.

**Tüm bunları yapmak istemiyorum, hesabımı kurtarmanın başka yolu nedir?**

Yeni bir Microsoft hesabı [oluşturabilirsiniz](https://www.microsoft.com/account) **not** (ilişkili @yourdomain.comolmayan bir e-postayla). NuGet.org hesap [bölümünüzü kurtarmak](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) için verilen adımları izleyin.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>NuGet.org hesabı kullanıcı adımı nasıl değiştiririm?

Yapamazsınız. İlke gereği kullanıcı adlarının değiştirilmesine izin vermiyoruz. Ayrıca, bunu [yapmak, paket sahibine dayalı paket güven ilkeleri](../consume-packages/installing-signed-packages.md#trust-package-owners)tanımlamış olabilecek kullanıcılar için bir kırılma değişikliğidir. Kullanıcı adınızı değiştirmenin tek yolu, istediğiniz kullanıcı adı ile yeni bir hesap oluşturmaktır. Yeni bir hesap oluşturmadan önce mevcut hesabınızı silmenizi öneririz, aksi takdirde kayıtlı Microsoft hesabınızı yeniden kullanamazsınız.
> [!Important]
> Kullanıcının silmesi yine de `username` **rezerve** edecektir. Aynı kullanıcı adını tekrar kullanamazsınız ve **bu kasaların değişimini içerir.** Örnek olarak, kullanıcı adı `mycoolname` olan bir kullanıcı oluşturduysanız `MyCoolName`ve bunu değiştirmek istiyorsanız (kasa değişiklikleri), kullanıcıyı siledikten sonra bu mümkün olmayacaktır.

[NuGet.org hesap bölümünüzü silme](#how-to-delete-my-nugetorg-account) ve doğru kullanıcı adı ile yeni bir hesap [kaydetmek](individual-accounts.md) için verilen adımları izleyin.

### <a name="how-to-delete-my-nugetorg-account"></a>NuGet.org hesabımı nasıl silem?

Hesabınızı silmek için, tek sahibi olduğunuz paketlerin sahipliğini aktarmanızı tavsiye ettiğimizi lütfen unutmayın. Nasıl yapılacağını [paket sahipleri yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg) hakkında daha fazla bilgi edinebilirsiniz. Bu aynı zamanda isteğinizi hızlandırmamıza da yardımcı olacaktır.

Hesabınızı bir kuruluşa dönüştürmek istiyorsanız, [NuGet.org hesabımı bir kuruluşa dönüştürmek için](#how-to-transform-my-nugetorg-account-to-an-organization)verilen adımları izleyin.

> [!Important]
> Kullanıcının silmesi aşağıdaki leri sağlar:
>  1. Kullanıcı adınız rezerve edilecek ve hiç kimse bu hesabı tek bir hesap veya kuruluş hesabı oluşturmak için yeniden kullanamaz
>  1. İlişkili API anahtarı(lar) iptal edin. 
>  1. Herhangi bir alt paket için hesabı sahibi olarak kaldırın.
>  1. Daha önce var olan tüm kimlik öneki rezervasyonlarını bu hesapla ayırın.
>  1. Hesabı herhangi bir kuruluşun üyesi olarak kaldırın.

Hesap silme işlemine devam etmek için aşağıdaki adımları izleyin.
1. Silmek istediğiniz hesapla [NuGet.org giriş](https://www.nuget.org/users/account/LogOn) yapın.
2. Bu url'ye [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) tıklayın: ve hesabı silme isteğini göndermek için adımları izleyin.

Müşteri desteğimiz bu talebi işleyecek ve hesap silme işlemini gerçekleştirecektir.
