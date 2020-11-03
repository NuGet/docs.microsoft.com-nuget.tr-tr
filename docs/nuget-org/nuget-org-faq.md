---
title: NuGet.org Frequently-Asked soruları
description: NuGet Galerisi ile çalışmaya yönelik sık sorulan sorular ve yanıtlar.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7076378b53c439eef51a243fa6efcfb01b8cfa73
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237912"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org sık sorulan sorular

## <a name="license-terms"></a>Lisans koşulları

**Bir paket belirli lisans bilgilerini sağlamıyorsa varsayılan lisans koşulları nelerdir?**

Her paket, pakete dahil edilen koşullara tabidir. Herhangi bir pakete erişmeden, yüklemeden veya almadan önce geçerli koşulları gözden geçirmeniz gerekir. NuGet.org 'de paket sayfasında **Lisans bilgileri** bağlantısını kullanın.

Bir paket Lisans koşullarını belirtmezse, NuGet.org paketi sayfasındaki **kişi sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılarından sizin için herhangi bir fikri mülkiyet hakkı vermez ve üçüncü taraflar tarafından sunulan bilgilerden sorumlu değildir.

## <a name="managing-packages-on-nugetorg"></a>NuGet.org 'de paketleri yönetme

**Karşıya yüklendikten sonra paket meta verilerini düzenleyebilir miyim?**

NuGet tüm paketlerin imzalanmasını önerir. Paket imzalama tasarım prensibi, imzalanmış paket içeriğinin, nuspec içeren sabit olması gerekir. Paket meta verilerinin düzenlenmesiyle birlikte, var olan imzaları geçersiz kılarak nuspec üzerinde değişikliklere neden olur. Paket oluşturulduktan sonra paket meta verilerinin düzenlenmesinin gerekli olmaması için mevcut iş akışlarının değiştirilmesini öneririz.

Paketiniz için listelenen bağımlılıkların paketin kendisinden otomatik olarak oluşturulduğunu ve düzenlenemeyeceğini unutmayın.

Ayrıca, paketleri [int.nugettest.org](https://int.nugettest.org) ' ye yüklemek, paketi genel galeride kullanıma açmadan paketinizi test etmek ve doğrulamak için harika bir yoldur. API uç noktası: https://apiint.nugettest.org/v3/index.json

**NuGet.org ' de yayınlanan bir paketi silebilir miyim?**

Genel olarak, NuGet.org 'e yayımlanmış bir paketi silmeyi desteklemiyoruz. [Paketleri silme konusunda ilkeniz](policies/deleting-packages.md)hakkında daha fazla bilgi edinin.

**Gelecekte yayımlanacak paketlere ait adları ayırmak mümkün mü?**

Evet. Hesabınız için bir paket KIMLIĞI öneki isteyerek [NuGet.org](https://www.nuget.org/) üzerindeki paketlerin kimliklerini ayırabilirsiniz. Bir paket KIMLIĞI öneki istemek için [belgelerindeki](id-prefix-reservation.md)yönergeleri izleyin.

**Paketler için talep sahipliği Nasıl yaparım??**

Bkz. [NuGet.org üzerinde paket sahiplerini yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Nasıl yaparım?, yazılım lisansımı ihlal eden bir paket sahibiyle ilgilensin mi?**

NuGet Community 'nin paket sahipleri ve diğer yazılımların sahipleri arasında ortaya çıkabilecek tüm anlaşmazlıkların çözülmesi için birlikte çalışmasını teşvik ediyoruz. NuGet.org yöneticilerinin işlemesini istemeden önce izlenecek bir [itiraz çözümleme süreci](policies/dispute-resolution.md) yaptık.

**Test paketlerimi NuGet.org 'e yüklemeniz önerilir mi?**

Test amacıyla, [int.nugettest.org](https://int.nugettest.org)veya [Myget.org](https://myget.org) ya da [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)gibi alternatif genel NuGet sunucuları kullanabilirsiniz.

İnt.nugettest.org 'e yüklenen paketlerin korunmadığını unutmayın.

**NuGet.org 'e yükleyebilecekleri paketlerin en büyük boyutu nedir?**

NuGet.org, paketlere 250MB 'a kadar izin verir, ancak mümkünse paketleri ve paketleri birbirine bağlamak için bağımlılıkları kullanarak paketlerinizi 1MB altında tutmanız önerilir. Thumb kuralı olarak, paketler çakışmaları önlemek için yalnızca bir derleme içerir.

NuGet, paketleri indirmek için HTTP kullanır, bu nedenle daha büyük paketler, başarısız olan yükleme olasılığının daha büyük bir olasılığını daha yüksektir.

Birden çok paket arasında bağımlılıklar paylaşmak mümkündür ve NuGet paketlerinizin tüketicilerinin Toplam indirme boyutunu daha küçük hale getirir.

Bağımlılıklar genellikle statiktir ve hiçbir şekilde değişmez. Koddaki bir hata düzeltilirken, bağımlılıkların güncelleştirilmesine gerek olmayabilir. Bağımlılıkları paketlemezseniz, her seferinde daha büyük paketleri sonlandırın. NuGet paketlerini ilgili bağımlılıklara bölerek, yükseltme, paketinizin müşterileri için çok daha ayrıntılı bir şekilde yapılır.

## <a name="nugetorg-not-accessible"></a>NuGet.org erişilemiyor

**Paketleri NuGet.org ' den neden indiremiyorum veya paket yüklenemiyor?**

İlk olarak, NuGet 'in en son sürümlerini kullandığınızdan emin olun. Bu sürüm başarısız olmaya devam ederse [desteğe başvurun](https://www.nuget.org/policies/Contact) ve aşağıdakiler dahil olmak üzere ek bağlantı sorunlarını giderme bilgilerini sağlayın:

- Kullanmakta olduğunuz NuGet sürümü
- Kullanmakta olduğunuz paket kaynakları
- Ayrıntılı ayrıntı içeren geri yükleme günlüğü
- MTR veya Fiddler izlemeleri (aşağıya bakın)
- Coğrafi alanı
- Makinenizin bir proxy veya güvenlik duvarının arkasında olup olmadığı?
- Makineniz bulut sağlayıcılarının veri merkezi (Azure, AWS vb.) üzerinde bulunuyor mu? Yanıt Evet ise, lütfen sağlayıcının ve bölgenin adını belirtin.

*MTR 'yi yakalamak için:*

- [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download)'yi indirin.
- `api.nuget.org`Ana bilgisayar adı olarak girin ve **Başlat** ' a tıklayın.
- **Gönderilen** sütun >= 100 olana kadar bekleyin.

    ![MTR yakalama](media/mtr.png)

- Metni panoya kopyala.

*Fiddler 'i yakalamak için:*

- [Fiddler](https://www.telerik.com/download/fiddler)'ın en son sürümünü yükler.
- Fiddler 'ı başlatın ve **dosya > yakalama trafiği** menüsünü kullanarak trafiği yakalamayı devre dışı bırakın.
- Tüm oturumları Kaldır (listedeki tüm öğeleri seçin, **Delete** tuşuna basın).
- **Araç > Fiddler seçenekleri...** menüsündeki **https** sekmesinde **https trafiğinin şifresini çöz** ' ü DENETLEYEREK, Fiddler 'ı HTTPS trafiği yakalamak üzere yapılandırın.
- Visual Studio’yu kapatın.
- **Dosya > yakalama trafiği** menüsünü etkinleştirin.
- Visual Studio veya nuget.exe. exe ' yi başlatın ve çalışmayan eylemleri gerçekleştirin. Bu eylemler tarafından oluşturulan trafiğin Fiddler 'da görünmesi gerekir.
- Eylemler çalıştırıldığında, yakalanan oturumları depolamak için **tüm oturumları > kaydet > dosyayı** kullanın.

Note: `HTTP_PROXY` `http://127.0.0.1:8888` Fiddler aracılığıyla NuGet trafiğini yönlendirmek için ortam değişkenini olarak ayarlamak gerekebilir.

Bu başarısız olursa, [Bu StackOverflow gönderisini belirtilen ipuçlarına](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)deneyin.

## <a name="nugetorg-account-management"></a>NuGet.org hesabı yönetimi

### <a name="how-to-recover-nugetorg-password-login"></a>NuGet.org parola oturumu açma nasıl kurtarılır?

[NuGet.org parola oturum açmanın sonlandırılacağından](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) ve NuGet.org 'de oturum açmanın tek yolu bir kişisel MICROSOFT HESABı (MSA) veya Azure ACTIVE DIRECTORY (AAD) hesabı ile birlikte olduğunu lütfen unutmayın. Bununla birlikte, ilişkili MSA/AAD hesaplarınıza erişemediyseniz, NuGet.org hesabınızı kurtarmak için parola oturum açma kullanmanız gerekebilir. Bu durumda aşağıdaki adımları izleyin.
- **Gereksinim:** Parolayı kurtarmanız gereken hesapla ilişkili e-postaya erişiminizin olması gerekir.
- [Parola unuttum sayfasına](https://www.nuget.org/account/ForgotPassword) gidin
- Kurtarmak istediğiniz NuGet.org hesabı ile ilişkili **e-posta** adresini girin.
- **Gönder** düğmesine tıklayın.
- Parolayı sıfırlamanıza yönelik bir bağlantı ile belirtilen e-posta adresi hesabına bir e-posta alacaksınız. Bu bağlantıya tıklayın ve yeni parolayı ayarlayın. Postanın "önemsiz" klasörünüzü denetlemesini bulamıyorsanız.
- İşiniz bittiğinde, artık NuGet üzerinde Kullanıcı adı/parola ile oturum açabilirsiniz.
- Kullanıcı adı/parola ile oturum açmak için, [NuGet.org oturum açma sayfasında](https://www.nuget.org/users/account/LogOn) **NuGet.org hesabını kullanma** bağlantısını kullanın.

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Hangi Microsoft hesabı NuGet.org hesabımı ile bağlantılı?

NuGet.org hesabınızla ilişkili Microsoft hesabı unuttuysanız, yardım almak için lütfen aşağıdaki adımları izleyin.
1. [NuGet.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn) gidin ve yardım oturum **açmak istiyor musunuz?** bağlantısına tıklayın.
1. Bu, yardım için açılır iletişim kutusunu gösterir. NuGet.org hesabınız için ilişkili Microsoft hesabı (ler) i anlamak için bu iletişim kutusundaki adımları izleyin.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>NuGet.org oturum açma için kullandığım Microsoft hesabı nasıl değiştirilir?
NuGet.org Kullanıcı için Microsoft hesabı değiştirmek istiyorsanız aşağıdaki adımları izleyin. E-posta ile Microsoft hesabı `account1@outlook.com` Kullanıcı adı ile NuGet.org hesabınızla ilişkilendirildiğini söyleyin `MyNuGetAccount` . Oturum açma bilgilerini e-posta ile başka bir Microsoft hesabı değiştirmek istiyor musunuz? `account2@outlook.com`
1. Lütfen **currently associated Microsoft account** `account1@outlook.com` **Microsoft hesabıyla oturum açın** tıkladıktan sonra [oturum açma sayfasında](https://www.nuget.org/users/account/LogOn) , şu anda ilişkili Microsoft hesabı () kullanarak oturum açın.
1. Oturum açtıktan sonra [Hesap ayarları](https://www.nuget.org/account) sayfanıza gidin.
1. **Oturum açma hesabı** için bölümü genişletin. **Hesabı Değiştir** düğmesine tıklayın.
1. Şimdi Microsoft oturum açma sayfasına yönlendirilirsiniz. Lütfen ilişkilendirmeyi değiştirmek istediğiniz hesapla oturum açın, `account2@outlook.com` Örneğin. **Note** : farklı bir Microsoft hesabı oturum açabilmek için oturum açma akışında oturumu Kapat **ve farklı hesapla oturum aç** ' a tıklamanız gerekebilir.
1. Aşağıdaki gibi bir hata görürseniz, daha fazla ayrıntı için Microsoft hesabı bkz. [başka bir NuGet.org hesabıyla bağlantılı](#microsoft-account-is-linked-with-another-nugetorg-account) .
    >_' Account2 ' ile Microsoft hesabı güncelleştirilemedi <account2@outlook.com> . Bu, zaten başka bir NuGet hesabına bağlanmışsa meydana gelebilir. Daha fazla bilgi için desteğe başvurun._

1. İkinci hesabınız ile başarıyla oturum açtıktan sonra, NuGet.org hesap ayarları sayfanıza yönlendirilirsiniz ve artık oturum açma hesabı olarak ilişkili yeni Microsoft hesabı görmeniz gerekir. Bu hesabı iletmek için NuGet.org oturum açarken bu hesabı kullanmanız gerekir.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft hesabı başka bir NuGet.org hesabıyla bağlantılı.

Microsoft oturum açma bilgilerinizi değiştirmeye çalıştıysanız ve aşağıdaki hatayı gördük:
> _' Account2 ' ile Microsoft hesabı güncelleştirilemedi <account2@outlook.com> . Bu, zaten başka bir NuGet hesabına bağlanmışsa meydana gelebilir. Daha fazla bilgi için desteğe başvurun._

NuGet.org kullanıcısı için Microsoft hesabı oturum açma bilgilerini, `account1@outlook.com` `MyNuGetAccount1` e-posta ile başka bir Microsoft hesabı değiştirmeye çalıştığınız için izin verir `account2@outlook.com` . Ve yukarıdaki hatayı görürsünüz.

**Yukarıdaki hata ne anlama geliyor?**

Bu, değiştirmek istediğiniz Microsoft hesabı ilişkili başka bir NuGet.org hesabı olduğu anlamına gelir. Yukarıdaki örnekte, e-posta ile Microsoft hesabı `<account2@outlook.com>` , ki Kullanıcı adı ile başka bir NuGet.org hesabıyla ilişkilendirilir `MyNuGetAccount2` .

Farklı bir NuGet.org hesabına bağlı Microsoft hesabı ilişkili oturum açma bilgilerini değiştiremezsiniz.

**Başka bir NuGet.org hesabım olduğunu unuttum, hangi NuGet.org hesabını olduğunu nasıl bulabilirim?**

[Oturum açma sayfasındaki](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "oturum açma sayfası")ikinci Microsoft hesabı oturum açın. Bu, sizi şu anda ikinci Microsoft hesabı ilişkili olan NuGet.org hesabına kaydeder. Daha sonra yüklenen paketleri görüntüleyebilir ve hesap yönetimini bu hesapta gerçekleştirebilirsiniz.

**Bu ikinci NuGet.org hesabı hakkında ilgilenmedim, ilk NuGet.org hesabı için oturum açma işlemini ikinci Microsoft hesabı değiştirmek istiyorum. Ne yapmalıyım?**

İkinci NuGet.org hesabını ilgilenmek ve yine de ilişkili Microsoft hesabı e-postayla yeniden kullanmak istiyorsanız `account2@outlook.com` . 

NuGet.org hesabını silerek Microsoft hesabı ve NuGet.org hesabı arasındaki ilişkilendirmeyi serbest bırakabilirsiniz.
1. İkinci NuGet.org hesabı için [Kullanıcı silme](#how-to-delete-my-nugetorg-account) adımlarını izleyin `MyNuGetAccount2` . 
1. Bu hesap silindikten sonra [Microsoft hesabı oturum açma adımlarını değiştirmek](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)için adımları yeniden deneyebilirsiniz.

**Bekleyin, bu ikinci hesap hakkında çok dikkat edin. Bu hesabı kaybetmek istemiyorum, ancak ilk hesapta ilişkili hesap oturumlarımı değiştir.**

E-posta ile üçüncü bir Microsoft hesabı oluşturmanız/kullanmanız gerekir `account3@outlook.com` . 
1. İlk olarak, NuGet.org üzerinde ikinci Microsoft hesabı oturum açmalısınız `account2@outlook.com` . İlişkili oturum açmaları değiştirmek ve üçüncü Microsoft hesabı bu NuGet.org hesabıyla ilişkilendirmek için yukarıdaki adımları izleyin.
1. İşiniz bittiğinde, e-posta ile ikinci Microsoft hesabı `account2@outlook.com` ilk NuGet.org Hesabınızla ilişkilendirilebilen ücretsizdir `MyNuGetAccount1` . Microsoft oturum açmaları ikinci Microsoft hesabı değiştirmek için yukarıdaki adımları izleyin.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Microsoft hesabı ile oturum açma, e-postamın başka bir Microsoft hesabı bağlı olduğunu gösteriyor

Microsoft hesabı ile oturum açmaya çalıştıysanız, e-posta ile `account1@outlook.com` aşağıdaki gibi bir hata görürsünüz:
> _' ' E-postasına sahip hesap account1@outlook.com başka bir Microsoft hesabıyla bağlantılı._
>
> _Bağlı Microsoft hesabı güncelleştirmek isterseniz, bunu hesap ayarları sayfasından yapabilirsiniz._

**Yukarıdaki hata ne anlama geliyor?**

NuGet.org üzerinde bir hesap oluşturulduğunda, bu hesapla ilişkili bir iletişim e-posta adresi vardır. Bu, genellikle ilişkili Microsoft hesabı için kullanılan e-posta adresiyle aynıdır. Ancak, iletişim için farklı bir e-posta adresi belirtmeyi seçebilirsiniz. Teknik olarak, farklı bir Microsoft hesabı sahip olabilirsiniz, bununla birlikte `account2@outlook.com` iletişim e-posta adresi olan NuGet.org hesabına bağlı olduğunu varsayalım `account1@outlook.com` .

Bu nedenle yukarıdaki hata, iletişim e-posta adresi olan NuGet.org hesabı zaten var, `account1@outlook.com` ancak **olmayan** bir e-posta ile ilişkili başka bir Microsoft hesabı ile ilişkilendirilir `account1@outlook.com` .

**Bu NuGet.org hesabına hangi Microsoft hesabı bağlandığını Nasıl yaparım? bulun mi?**

E-posta adresi ile NuGet.org hesabına hangi Microsoft hesabı bağlandığını anlamak için [oturum açma Yardım](#which-microsoft-account-is-linked-to-my-nugetorg-account) akışını kullanmanız gerekir `account1@outlook.com` .

**Bu hesabı Microsoft hesabı geçersiz kılmak istiyorum**

Microsoft hesabı mevcut NuGet.org hesabıyla ilişkilendirmek için [Microsoft oturum açma, NuGet.org hesabımı nasıl kurtarırım?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) bölümündeki adımları izleyin.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Microsoft oturum açma kullanılamıyor, NuGet.org hesabımı nasıl kurtarırım?

[Oturum açma yardımını](#which-microsoft-account-is-linked-to-my-nugetorg-account) kullanmaya çalıştıysanız ve NuGet.org hesabınızla ilişkili Microsoft hesabı erişiminiz yoksa, lütfen NuGet.org hesabınıza yeni bir Microsoft hesabı bağlamak için aşağıdaki adımları izleyin.
1. **Gereksinim** : herhangi bir mevcut NuGet.org hesabı ile ilişkilendirilmemiş bir Microsoft hesabı erişiminizin olması gerekir. Bir tane yoksa, bir tane [oluşturabilirsiniz](https://signup.live.com) .
2. NuGet.org hesabınız için Kullanıcı adınızı ve parolanızı unuttuysanız, [parola oturum açma bilgilerinizi kurtarmak için adımları](#how-to-recover-nugetorg-password-login)izleyin.
3. Kullanıcı adı/parola oturum açma bilgilerini kullanarak [NuGet.org 'de oturum açın](https://www.nuget.org/users/account/LogOnNuGetAccount) .
4. Oturum açıldıktan sonra açılır iletişim kutusunun aşağıda gibi göründüğünü görürsünüz. Bu parola ayırma iletişim kutusudur.
5. **Note** : lütfen belirtilen Microsoft hesabı oturum açmak için yönergeyi yoksayın. Artık NuGet.org hesabınızı diğer Microsoft oturum açma bilgilerine bağlayabilirsiniz.
6. Adım 1 ' de belirtildiği gibi düğme **Microsoft hesabıyla oturum açın** tıklayın ve erişiminizin olduğu Microsoft hesabı oturum açın.
7. Hesabınız artık yeni Microsoft hesabı bağlanır, bu da NuGet.org ' de oturum açmak için kullanabilirsiniz.

    ![Bağlama MSA Iletişim kutusu](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>NuGet.org hesabımı kuruluşa dönüştürme

Hesabınızı bir kuruluşa dönüştürmek istiyorsanız ve bu hesap zaten bir Microsoft hesabı oturum açmayla ilişkili ise, lütfen [NuGet org 'daki kuruluşların](organizations-on-nuget-org.md)belgelerinde verilen adımları izleyin.

Ancak, NuGet.org hesabınız ilişkili/bir Microsoft hesabı ile bağlantılı değilse, bu hesabı bir kuruluşa dönüştürmek için aşağıdaki adımları izleyebilirsiniz.
1. **Gereksinim** : kuruluş hesabında yönetici olarak kullanılmak üzere NuGet.org üzerinde ilk kez oluşturulmuş tek bir hesabınız olması gerekir. Bir tane yoksa, lütfen [Yeni bir NuGet.org hesabı oluşturun](individual-accounts.md)
2. Parola oturum açma izniniz yoksa, NuGet.org hesabınız için [parola oturum açma bilgilerinizi kurtarmak için adımları](#how-to-recover-nugetorg-password-login) izleyin.
3. Kullanıcı adı/parola oturum açma bilgilerini kullanarak [NuGet.org 'de oturum açın](https://www.nuget.org/users/account/LogOnNuGetAccount) .
4. Oturum açıldıktan sonra açılır iletişim kutusunun aşağıda gibi göründüğünü görürsünüz. Bu parola ayırma iletişim kutusudur. 
    > [!Important]
    > Bu iletişim kutusunu yoksayın, **Microsoft Ile oturum aç** düğmesine **tıklamayın** .

5. Adresine gidin [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform) . Bu, bir Microsoft hesabı bağlanmadan NuGet.org hesabını bir org 'a dönüştürmenize olanak tanır.
6. Kişisel NuGet.org hesabınız için yönetici kullanıcı adını ve adım 1 ' de oluşturduğunuz hesabı belirtin.
7. Bu hesabın bir kuruluşa dönüştürülmesini tamamlamaya yönelik yönergeleri izleyin.

    ![Bağlama MSA Iletişim kutusu](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Yönetilmeyen kiracı ile AAD hesapları için oturum açma sorunları NuGet.org mi?

E-posta hesabı etki alanınız () ile oturum açma akışınız sırasında aşağıdaki gibi bir hata görürseniz @yourdomain.com , NuGet.org hesabınızı kurtarmak için aşağıdaki adımlara bakın.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Oturum açma sırasında bu yönetilmeyen durum nedir? Bu şimdi neden oluyor?** 

Hesabınız daha önce kişisel bir Microsoft hesabı olarak kaydedilmiş ve sorunsuz çalıştıyordu, ancak artık hesabınızın Azure Active Directory bir "yönetilmeyen" Kiracı olarak kaydedilmiş gibi görünüyor (Microsoft hesaplarının kimliğini doğrulamak için kullandığımız kimlik hizmeti). 

Bu durum, bir veya kuruluşunuzun ( @yourdomain.com e-posta adresi ile) AAD tümleşik hizmetlerinden biriyle kayıtlı olması veya [Azure Active Directory için bir self servis kaydolma](/azure/active-directory/users-groups-roles/directory-self-service-signup)işlemi gerçekleştirmişse (Bu durumda, kullanılan Microsoft hesabı etki alanı için (örneğin,) bir "yönetilmeyen" Kiracı oluşturarak meydana gelir @yourdomain.com . 

**Hesabımı kurtarmak için ne yapabilirim?**

Bu anda, Azure Active Directory 'de "yönetilmeyen" Kiracı hesaplarıyla hesapların kimliğini doğrulamak için (NuGet.org) bir yol yoktur. Bu tür hesapların kimliğini doğrulamak için daha iyi bir yönteme bakıyoruz.

Microsoft hesabı () ile NuGet.org 'de oturum açmak istiyorsanız @yourdomain.com , "" e-posta adresine sahip kullanıcıların kimliğini doğrulamak için BIR DNS doğrulaması gerçekleştirerek (veya şirketinizdeki bir yöneticinin) AAD 'nin sahipliğini talep etmeniz gerekir @yourdomain.com . Lütfen Azure Active Directory tarafından belgelenen [etki alanı yöneticisi](/azure/active-directory/users-groups-roles/domains-admin-takeover) için adımları izleyin. Bu yapıldıktan sonra, normal oturum açma çalışmanız çalışmaya başlar.

**Her şeyi yapmak istemiyorum, hesabımı kurtarmanın diğer yolu nedir?**

Yeni bir Microsoft hesabı [oluşturabilirsiniz](https://www.microsoft.com/account) (ile ilişkili **olmayan** bir e-posta ile @yourdomain.com ). [NuGet.org hesabınızı kurtarma](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) bölümünde verilen adımları izleyin.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>NuGet.org hesabı kullanıcı adınızla Nasıl yaparım? değiştirilsin mi?

Oluşturamazsınız. İlke ne kadar çok Kullanıcı adı değişikliğine izin vermedik. Ayrıca, paket [sahibine bağlı olarak, paket güven ilkeleri](../consume-packages/installing-signed-packages.md#trust-package-owners)tanımlamış olabilecek kullanıcılar için önemli bir değişiklik de vardır. Kullanıcı adınızı değiştirme yöntemi, istenen kullanıcı adına sahip yeni bir hesap oluşturmaktır. Yeni bir hesap oluşturmadan önce mevcut hesabınızı silmenizi öneririz, aksi halde kayıtlı Microsoft hesabı yeniden kullanamazsınız.
> [!Important]
> Kullanıcının silinmesi, ' i **ayırmaya** devam eder `username` . Aynı kullanıcı adını yeniden kullanamayacaksınız ve **Bu, casler değişikliğini içerir** . Örnek olarak, Kullanıcı adı ile bir Kullanıcı oluşturduysanız `mycoolname` ve bunu `MyCoolName` (büyük/küçük harf değişiklikler) olarak değiştirmek istiyorsanız, Kullanıcı silindikten sonra mümkün olmayacaktır.

[NuGet.org hesabınızı silme](#how-to-delete-my-nugetorg-account) bölümünde verilen adımları izleyin ve doğru Kullanıcı adına sahip [Yeni bir hesap kaydedin](individual-accounts.md) .

### <a name="how-to-delete-my-nugetorg-account"></a>NuGet.org hesabımı nasıl silebilirim?

Hesabınızı silmek için, tek sahip olduğunuz tüm paketlerin sahipliğini aktarmanızı öneririz. [Paket sahiplerini yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg) hakkında daha fazla bilgi için bkz. bu konuda daha fazla bilgi edinebilirsiniz. Bu ayrıca isteğinizi hızlandırmamıza yardımcı olur.

Hesabınızı bir kuruluşa dönüştürmek istiyorsanız [NuGet.org hesabını bir kuruluşa dönüştürme](#how-to-transform-my-nugetorg-account-to-an-organization)bölümünde verilen adımları izleyin.

> [!Important]
> Kullanıcı silindiğinde aşağıdakiler olur:
>  1. Kullanıcı adınız ayrılmayacak ve tek bir hesap veya bir kuruluş hesabı oluşturmak için onu yeniden kullanamayacak
>  1. İlişkili API anahtarlarını iptal et. 
>  1. Hesabı herhangi bir alt paketin sahibi olarak kaldırın.
>  1. Daha önce var olan tüm KIMLIK öneki ayırmaları bu hesapla ilişkisini kaldırın.
>  1. Hesabı herhangi bir kuruluşun üyesi olarak kaldırın.

Hesap silmeye devam etmek için aşağıdaki adımları izleyin.
1. NuGet.org 'de silmek istediğiniz hesapla [oturum açın](https://www.nuget.org/users/account/LogOn) .
2. Bu URL 'ye tıklayın: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) ve hesabı silme isteğini göndermek için adımları izleyin.

Müşteri desteğiniz bu isteği işleyecek ve hesap silme işlemini gerçekleştirmeyecektir.