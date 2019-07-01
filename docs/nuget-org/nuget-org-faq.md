---
title: NuGet.org sık sorulan sorular
description: Sık sorulan sorular ve yanıtlar ile NuGet Galerisi'nin çalışmak için.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c2fc11c0f5dd5d98c40c8b97f9d5a72c4a334b79
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427604"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org sık sorulan sorular

## <a name="license-terms"></a>Lisans koşulları

**Bir paketi belirli bir lisans bilgileri sağlamıyorsa koşulları varsayılan lisans nelerdir?**

Her bir paketi paket ile birlikte gelen koşulları tabidir. Erişim, indirme veya herhangi bir paket alınırken önce hüküm gözden geçirmeniz gerekir. Nuget.org kullanın **lisans bilgilerini** bağlantı paketi sayfasında.

Bir paketi lisans koşulları belirtmezse kullanarak doğrudan paket sahibiyle iletişime geçin **sahipleriyle temas** nuget.org paketi sayfasında bağlantı. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paketi sağlayıcılarından lisans değil ve üçüncü taraflarca sağlanan bilgileri sorumlu değildir.

## <a name="managing-packages-on-nugetorg"></a>Paketleri NuGet.org üzerinde yönetme

**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim?**

NuGet imzalanması için tüm paketleri önerir. Paket imzalama tasarımı prensibi imzalı paket içeriğini nuspec içeren değişmezse, olmasıdır. Paket meta verileri düzenleme, mevcut imza geçersiz kılmalarını nuspec için değişiklikle sonuçlanır. Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde mevcut iş akışları değiştirme öneririz.

Paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez unutmayın.

Ayrıca, paketler için karşıya yükleme [int.nugettest.org](https://int.nugettest.org) test edin ve bir paket kullanılabilir genel galeride yapmadan paketinizi doğrulamak için harika bir yoludur. API uç noktası: https://apiint.nugettest.org/v3/index.json

**Ben NuGet.org için yayımlanan paket silebilir miyim?**

Genel olarak, yayımlanan NuGet.org için bir paket silindiğinde desteklemez. Daha fazla bilgi edinin bizim [paketleri silme ilkesi](policies/deleting-packages.md).

**Bu ad gelecekte yayımlanacak paketleri için ayrılacak mümkün mü?**

Evet. Şirket için paket kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği öneki isteyerek. Bir paket kimliği öneki isteğinde bulunmak için yönergeleri izleyin. [belgeleri](id-prefix-reservation.md).

**Paketler için mülkiyeti üzerine hak iddia nasıl?**

Bkz: [yönetme paket sahipleri nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Yazılım lisansımın ihlal bir paket sahibi ile nasıl dağıtılsın mı?**

Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek herhangi Anlaşmazlıkların çözüm yeri birlikte çalışmak için NuGet topluluk öneririz. Biz hazırlanmış bir [itiraz çözümleme işlemi](policies/dispute-resolution.md) nuget.org yöneticilerin intercede isteyen önce izlemek için.

**Benim test paketleri nuget.org için karşıya yüklemek için tavsiye edilir?**

Test amaçları için kullanabileceğiniz [int.nugettest.org](https://int.nugettest.org), veya diğer genel NuGet sunucularını [myget.org](https://myget.org) veya [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Paketler için int.nugettest.org karşıya korunmaz unutmayın.

**Paketleri nuget.org için karşıya yükleyebilirsiniz boyutu üst sınırı nedir?**

nuget.org sağlayan paketler en fazla 250MB, ancak paketleri 1 MB'den mümkünse tutulması ve paketleri birbirine bağlamak için bağımlılıklar kullanarak önerilir. Bir kural karşısında, paketler çarpışmalardan kaçınmak için yalnızca bir derleme içerir.

NuGet paketleri başarısız yüklemeler olasılığı daha küçük parçalara değerinden daha büyük paketleriniz varsa bu nedenle indirmek için HTTP kullanır.

Toplam yükleme boyutu için NuGet paketlerinizi tüketicilerinin küçülterek birden çok paketleri arasındaki bağımlılıkları paylaşmak da mümkündür.

Çoğunlukla statik ve hiçbir zaman değişiklik bağımlılıklardır. Kodda bir hatayı düzeltirken, bağımlılıkları güncelleştirilmesi gerekmez. Bağımlılıkları paketlerseniz, her zaman büyük paketler reshipping yukarı bitmelidir. NuGet paketlerini ilgili bağımlılıklarınızı bölerek yükseltme paketinin Tüketiciler için çok daha ayrıntılı sağlar.

## <a name="nugetorg-not-accessible"></a>nuget.org erişilebilir değil

**Neden paketleri indirin veya paketleri nuget.org için Yükle?**

İlk olarak, en son NuGet sürümlerini kullandığınızdan emin olun. Bu sürüm başarısız devam ederseniz [Destek ekibiyle iletişime geçin](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:

- Kullanmakta olduğunuz NuGet sürümü
- Kullanmakta olduğunuz paket kaynakları
- Ayrıntılı ayrıntı düzeyi içeren bir geri yükleme günlüğü
- MTR veya Fiddler izlemeleri (aşağıya bakın)
- Coğrafi konuma
- Makinenizde bir proxy veya güvenlik duvarı olup?
- Bir bulut sağlayıcıları veri merkezi (Azure, AWS vb.) bulunan makinenize var mı? Yanıt Evet ise lütfen sağlayıcıya ve bölge adını belirtin.

*MTR yakalamak için:*

- Gelen WinMTR indirin [http://winmtr.net/download/](http://winmtr.net/)
- Girin `api.nuget.org` tıklayın ve ana bilgisayar adı olarak **Başlat**.
- Bekle **gönderilen** sütun > = 100.

    ![MTR yakalama](media/mtr.png)

- Metin Panoya kopyalayın.

*Fiddler yakalamak için:*

- En son sürümünü yükleyin [Fiddler](http://www.telerik.com/download/fiddler).
- Fiddler'ı başlatın ve trafik yakalama kullanarak devre dışı **Dosya > trafik yakalama** menüsü.
- Tüm oturumlar kaldırın (tüm öğeleri listesinde, tuşuna seçin **Sil** anahtar).
- HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiğini** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.
- Visual Studio’yu kapatın.
- Etkinleştirme **Dosya > trafik yakalama** menüsü.
- Visual Studio ya da nuget.exe .exe başlatın ve çalışmıyor eylemleri gerçekleştirebilirsiniz. Bu eylemler tarafından oluşturulan trafiğin Fiddler'da göstermelidir.
- Bir eylem gerçekleştirdikten sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.

Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` için fiddler'ı aracılığıyla NuGet trafiği yönlendirme.

Bu başarısız olursa deneyin [ipuçları bu StackOverflow gönderide bahsedilen](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>nuget.org hesap yönetimi

### <a name="how-to-recover-nugetorg-password-login"></a>Nuget.org parola oturum açma, kurtarılır nasıl?

Lütfen unutmayın [nuget.org parola oturumu sona ermiştir](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) ve nuget.org için oturum açmak için tek bir kişisel Microsoft hesabı (MSA) veya Azure Active Directory (AAD) hesabı ile yoludur. Ancak, ilişkili MSA/AAD hesaplarınızı erişemiyor olması durumunda nuget.org hesabınızı kurtarmak için parola oturum açma kullanmanız gerekebilir. Bu durumda, aşağıdaki adımları izleyin.
- **Önkoşullar:** Parola kurtarmak istediğiniz hesapla ilişkili e-posta erişimi gerekir.
- Git [unuttunuz parola sayfası](https://www.nuget.org/account/ForgotPassword)
- Girin **e-posta** kurtarmak istediğiniz nuget.org hesabıyla ilişkili olan adresi.
- Tıklayın **Gönder** düğmesi.
- Belirtilen e-posta adresi hesap parolanızı sıfırlamak için bir bağlantı içeren bir e-posta alırsınız. Bu bağlantıya tıklayın ve yeni parolayı ayarlayın. "" Klasörünüzü posta onay bulamazsanız.
- Bunu yaptıktan sonra artık NuGet kullanıcı adı/parola ile oturum açın.
- Kullanıcı adı/parola ile oturum açmak için kullanın **Nuget.org hesabını kullanarak oturum** bağlantısını [nuget.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Hangi Microsoft hesabı nuget.org hesabıma bağlıdır?

Hangi Microsoft hesabı nuget.org hesabınızla ilişkilendirilen unuttuysanız Lütfen yardım almak için aşağıdaki adımları izleyin.
1. Git [nuget.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn) tıklayın **oturum açarken yardıma gereksinim?** bağlantı.
1. Bu Yardım almak için açılır iletişim kutusu gösterir. Nuget.org hesabınız için ilişkili Microsoft hesapları anlamak için bu iletişim kutusunda adımları izleyin.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Nuget.org oturum açmak için kullandığım Microsoft hesabı değiştirmek nasıl?
Nuget.org kullanıcının Microsoft hesabını değiştirmek istiyorsanız, aşağıdaki adımları izleyin. Sağlar deyin Microsoft hesabınızla e-posta `account1@outlook.com` kullanıcıadı nuget.org hesabınızla ilişkilendirilen `MyNuGetAccount`. Oturum başka bir Microsoft hesabı e-posta ile değiştirmek istediğiniz `account2@outlook.com`
1. Lütfen kullanarak oturum **şu anda Microsoft hesabı'nı ilişkili** yani `account1@outlook.com` üzerinde [oturum açma sayfasına](https://www.nuget.org/users/account/LogOn) tıkladıktan sonra **Microsoft'ta oturum açma**.
1. Oturum açtıktan sonra Git, [hesap ayarları](https://www.nuget.org/account) sayfası.
1. Bölümü Genişlet **oturum açma hesabı**. Tıklayarak **hesabı Değiştir** düğmesi.
1. Artık microsoft oturum açma sayfasına yönlendirilirsiniz. Lütfen ilişkilendirme yani değiştirmek istediğiniz hesapla oturum açtığınızdan `account2@outlook.com`. **Not**: tıklayın gerekebilir **oturum out ve farklı bir hesapla oturum** farklı bir Microsoft hesabı ile oturum açma için oturum açma akışını sırasında.
1. Bkz, aşağıdaki gibi bir hata görürseniz [Microsoft hesabı başka bir nuget.org hesabıyla bağlantılı](#microsoft-account-is-linked-with-another-nugetorg-account) daha fazla ayrıntı için.
    >_Microsoft hesabı ile güncelleştirilemedi. ' Firma2 <account2@outlook.com>'. Zaten başka bir NuGet hesabına bağlı olduğunda bu durum gerçekleşebilir. Daha fazla bilgi için desteğe başvurun._

1. İkinci hesabınızla başarıyla kaydolduktan sonra geri nuget.org hesap ayarları sayfanıza yönlendirileceksiniz ve ilişkili oturum açma hesabı olarak yeni bir Microsoft hesabı görmelisiniz. Bundan sonra bu hesabı nuget.org açarken kullanmanız gerekir.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft hesabı ile başka bir nuget.org hesabına bağlanır.

Microsoft oturum açma bilgilerinizi değiştirmeyi denedi ve aşağıdaki hata gördüğünüz takdirde:
> _Microsoft hesabı ile güncelleştirilemedi. ' Firma2 <account2@outlook.com>'. Zaten başka bir NuGet hesabına bağlı olduğunda bu durum gerçekleşebilir. Daha fazla bilgi için desteğe başvurun._

Sağlar deyin denemeye Microsoft değiştirmek için hesap oturumu açma `account1@outlook.com` nuget.org kullanıcının kullanıcı adı ile `MyNuGetAccount1` e-posta ile başka bir Microsoft hesabına `account2@outlook.com`. Ve yukarıdaki hataya bakın.

**Yukarıdaki hatası ne anlama geliyor?**

Bu, başka bir deyişle, yukarıdaki örnekte Microsoft hesabı e-posta ile değiştirilmesi çalıştığınız Microsoft hesabı ile ilişkili olan başka bir nuget.org hesap olduğu anlamına gelir `<account2@outlook.com>` , örneğin kullanıcı adına sahip başka bir nuget.org hesabıyla ilişkilendirilmiş `MyNuGetAccount2`.

Farklı nuget.org hesabıyla bağlantılı bir Microsoft hesabı ile ilişkili oturum açma değiştiremezsiniz.

**Ben başka bir nuget.org hesabı olduğunu nasıl bulabilirim bunun hangi nuget.org hesabı vardı unuttum?**

İkinci Microsoft hesabı ile oturum açma [oturum açma sayfasına](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "oturum açma sayfasına"). Bu, şu anda ikinci bir Microsoft hesabı ile ilişkili nuget.org hesabına günlüğe kaydedecektir. Karşıya yüklenen paketleri görüntülemek ve bu hesapta hesap yönetimi gerçekleştirin.

**Bu ikinci nuget.org hesap hakkında önemsemez, ilk nuget.org hesabının ikinci Microsoft hesabıyla oturum Kimliğimi değiştirmek istiyorum. Ne yapmalıyım?**

İkinci nuget.org hesap konusunda dikkatli olun ve ilişkili Microsoft hesabı e-posta ile yeniden kullanmak istediğiniz değil istediğiniz `account2@outlook.com`. 

Microsoft hesabınız ve nuget.org hesabınız arasındaki ilişkiyi nuget.org hesabı silerek serbest bırakabilirsiniz.
1. Adımlarını izleyin [kullanıcı silme](#how-to-delete-my-nugetorg-account) ikinci nuget.org hesabının `MyNuGetAccount2`. 
1. Bu hesap silindikten sonra adımları yeniden deneyebilir [Microsoft hesabı oturum açma değiştirme](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Bekleyin, ben bu ikinci hesap konusunda çok dikkatli olun. Bu hesap kaybetmek ancak benim ilişkili hesabı oturum açma bilgileri ilk hesabının değiştirmek istemezsiniz.**

Oluşturma/üçüncü bir Microsoft hesabı, örneğin e-posta ile kullanmak ihtiyacınız olacak `account3@outlook.com`. 
1. İlk gereken ikinci Microsoft hesabınız ile oturum açma `account2@outlook.com` nuget.org üzerinde. İlişkili oturum açma bilgileri değiştirin ve üçüncü Microsoft hesabını bu nuget.org hesabıyla ilişkilendirmek için yukarıdaki adımları izleyin.
1. Bittiğinde, ikinci Microsoft hesabınızla e-posta `account2@outlook.com` ilk nuget.org hesabınıza ilişkilendirilecek ücretsizdir `MyNuGetAccount1`. İkinci bir Microsoft hesabı ile microsoft oturum açma bilgileri değiştirmek için yukarıda aynı adımları izleyin.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Microsoft hesabıyla oturum açmayı bana e-postamı başka bir Microsoft hesabıyla bağlantılı gösterir

Microsoft hesabınızla oturum, örneğin e-posta ile oturum açmaya çalıştığınızda `account1@outlook.com` ve bir hatayı aşağıdaki gibi:
> _E-posta hesabıyla 'account1@outlook.com' başka bir microsoft hesabı ile bağlantılıdır._
>
> _Bağlantılı bir Microsoft hesabı güncelleştirmek istiyorsanız hesap ayarları sayfanızdan bunu yapabilirsiniz._

**Yukarıdaki hatası ne anlama geliyor?**

Nuget.org bir hesap oluşturulduğunda, ilgili hesapla ilişkili bir iletişim e-posta adresi yok. Bu, genellikle ilişkili Microsoft hesabı için kullanılan e-posta adresi olarak aynıdır. Ancak, bir iletişim için farklı bir e-posta adresini belirtmek seçebilirsiniz. Bu nedenle, teknik olarak, farklı bir Microsoft hesabı, ile söyleyin olabilir `account2@outlook.com` iletişim e-posta adresi olarak nuget.org hesabıyla bağlantılı `account1@outlook.com`.

Yukarıdaki hata zaten olduğunu nuget.org hesabı iletişim e-posta adresiyle gerektiği anlamına gelir. `account1@outlook.com` ancak e-posta ile başka bir Microsoft hesabıyla ilişkilendirilmiş **olmayan** `account1@outlook.com`.

**Hangi Microsoft hesabı bu nuget.org hesabına bağlı olduğunu nasıl bulabilirim?**

Kullanmanız gereken [Yardım oturum](#which-microsoft-account-is-linked-to-my-nugetorg-account) hangi Microsoft hesabı e-posta adresi ile nuget.org hesaba bağlı kullanıma belirlemeye akış `account1@outlook.com`.

**Bu Hesapla Microsoft Hesabımı geçersiz kılmak istiyorum**

Adımları [kullanın, microsoft oturumu kurulamıyor nasıl kurtarma miyim nuget.org Hesabımı](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) Microsoft hesabınız var olan nuget.org hesabıyla ilişkilendirmek için bölüm.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Microsoft oturum açma, kullanılamıyor nasıl kurtarma miyim nuget.org Hesabımı?

Kullanarak çalıştıysanız [Yardım oturum](#which-microsoft-account-is-linked-to-my-nugetorg-account) ve nuget.org hesabınızla ilişkili Microsoft hesabına erişiminiz yok, Lütfen yeni bir Microsoft hesabı nuget.org hesabınıza bağlamak için aşağıdaki adımları izleyin.
1. **Gereksinim**: Tüm mevcut nuget.org hesapları ile ilişkili olmayan bir Microsoft hesabı için erişim gerekir. Biri yoksa yapabilecekleriniz [oluşturma](https://signup.live.com) biri.
2. Nuget.org hesabınız için kullanıcı adınızı ve parolanızı unuttuysanız, izleyin [parola oturum açma bilgilerinizi kurtarmak için adımlar](#how-to-recover-nugetorg-password-login).
3. [Oturum açma nuget.org'da](https://www.nuget.org/users/account/LogOnNuGetAccount) oturum açma kullanıcı adı/parola kullanarak.
4. Oturum açtıktan sonra Göster açılan iletişim kutusu görürsünüz. en fazla ister aşağıda. Bu parola son veriliyor iletişim kutusudur.
5. **NOT**: Lütfen belirtilen Microsoft hesabı ile oturum açmak için yönerge yoksayın. Artık, herhangi bir Microsoft oturum açmaya nuget.org hesabınıza bağlayabilirsiniz.
6. Düğmesine tıklayın **Microsoft'ta oturum açma** ve bir erişim için 1. adımda bahsedilen sahip Microsoft hesabı ile oturum açın.
7. Hesabınız artık ileriye dönük nuget.org açmak için kullanabileceğiniz yeni bir Microsoft hesabı bağlı.

    ![Bağlantı MSA iletişim kutusu](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Nuget.org Hesabımı bir kuruluş olarak dönüştürmek nasıl?

Hesabınız bir kuruluşun dönüştürmek istediğiniz ve bu hesap zaten bir Microsoft hesabı oturum açma ile ilişkilendirilmiş Lütfen belgelerindeki verilen adımları izleyin [nuget kuruluş üzerindeki kuruluşlar](organizations-on-nuget-org.md).

Ancak, nuget.org hesabınızı bir Microsoft hesabı ile ilişkili/bağlı değilse, bu bir kuruluş hesabına dönüştürmek için aşağıdaki adımları izleyebilirsiniz.
1. **Gereksinim**: Kuruluş hesabı yönetici olarak kullanılacak nuget.org önce oluşturulan ayrı bir hesap olması gerekir. Biri yoksa lütfen [yeni nuget.org hesabı oluşturma](individual-accounts.md)
2. İzleyin [parola oturum açma bilgilerinizi kurtarmak için adımlar](#how-to-recover-nugetorg-password-login) nuget.org hesabınızın bu adımı atlarsanız size parola oturum açma, yoksa.
3. [Oturum açma nuget.org'da](https://www.nuget.org/users/account/LogOnNuGetAccount) oturum açma kullanıcı adı/parola kullanarak.
4. Oturum açtıktan sonra Göster açılan iletişim kutusu görürsünüz. en fazla ister aşağıda. Bu parola son veriliyor iletişim kutusudur. 
    > [!Important]
    > Bu iletişim kutusunu yok sayın **olmayan** tıklayarak **Microsoft'ta oturum açma** düğmesi.

5. [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform) kısmına gidin. Bu bağlama için bir Microsoft hesabı olmadan nuget.org hesabı için bir kuruluş dönüştürmenize olanak tanır.
6. Kişisel nuget.org hesabınız için yönetici kullanıcı adı belirtin/1. adımda oluşturduğunuz hesabı.
7. Bu bir kuruluş hesabına dönüşümü tamamlamak için yönergeleri izleyin.

    ![Bağlantı MSA iletişim kutusu](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Yönetilmeyen Kiracı AAD hesabıyla oturum açma sorunlarını nuget.org?

E-posta hesabı etki alanınızı ile oturum açma akışı sırasında aşağıdaki gibi bir hata görürseniz (@yourdomain.com), nuget.org hesabınızı kurtarmak için aşağıdaki adımlara bakın.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Oturum açma sırasında bu yönetilmeyen duruma şey nedir? Ve bunu şimdi neden oluyor?** 

Hesabınızın daha önce bir kişisel Microsoft hesabı olarak kaydedilmesi gibi görünüyor ve düzgün çalışan, hesabınızı bir Azure Active Directory'de (kimlik doğrulaması yapmak için kullandığımız kimlik hizmeti "Yönetilmeyen" Kiracı olarak kaydedildi ancak artık görünüşe Microsoft hesapları için). 

Bu, olmuş olabilir siz veya kuruluşunuzdaki bir kişi (ile @yourdomain.com e-posta adresi) AAD tümleşik hizmetlerden biri ile kayıtlı veya yaptığınız bir [Azure Active Directory için Self Servis kaydolma](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), gibi oluşturan bir " Yönetilmeyen"Kiracı için kullanılan Microsoft hesabı etki alanı (@yourdomain.com durumunuzdaki). 

**Hesabımı kurtarma neler yapabilirim?**

Şu anda değil hesapları gibi Azure Active Directory'de "Yönetilmeyen" Kiracı hesapları ile kimlik doğrulaması için bize (nuget.org) için bir yolu yoktur. Bu tür hesaplarının kimliğini doğrulamak için daha iyi bir şekilde arıyoruz.

Nuget.org Microsoft hesabınızla oturum istiyorsanız (@yourdomain.com), sizin (veya şirketiniz şirketindeki bir yöneticinin) e-posta adresi ile kullanıcıların kimliğini doğrulamak için bir DNS doğrulaması yaparak AAD sahipliğini talep etmesi gereklidir "@yourdomain.com". Lütfen adımlarını izleyin [etki alanı yönetici devralma işlemini](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) Azure Active directory tarafından belirtilmiştir. Bunu yaptıktan sonra oturum açma bilgilerinizi normal çalışmaya başlayabilirsiniz.

**Tüm ne Hesabımı kurtarmak için diğer yol ise bunu yapmak istemiyor musunuz?**

Yapabilecekleriniz [oluşturma](https://www.microsoft.com/en-us/account) yeni bir Microsoft hesabı (e-posta ile **değil** ilişkili @yourdomain.com). Verilen adımları [nuget.org hesabınızı kurtarın](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) bölümü.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Nuget.org hesabı kullanıcı nasıl değiştirebilirim?

Şunları yapamazsınız. İlkesel size henüz dağıtmadığı kullanıcı adlarını değiştirmek izin vermez. Kullanıcı adınızı değiştirmek için tek yolu, istenilen kullanıcı adı ile yeni bir hesap oluşturmaktır. Öneririz, yeni bir tane oluşturmadan önce var olan hesabınızı silmek, aksi takdirde, kayıtlı bir Microsoft hesabı yeniden mümkün olmayacaktır.
> [!Important]
> Bir kullanıcının silinmesi edebilirsiniz **rezerve** `username`. Aynı kullanıcı adını tekrar tekrar mümkün olmayacaktır ve **bu değişikliği kasası içerir**. Bir kullanıcının kullanıcı adı ile oluşturduysanız, örnek olarak `mycoolname` ve bunun için değiştirmek istediğiniz `MyCoolName`(büyük/küçük harf değişikliklerini) bunu mümkün olmayacak kullanıcı sildikten sonra.

Verilen adımları [nuget.org hesabınızı silme](#how-to-delete-my-nugetorg-account) bölümü ve [yeni bir hesap kaydetmek](individual-accounts.md) doğru kullanıcı adına sahip.

### <a name="how-to-delete-my-nugetorg-account"></a>Nuget.org Hesabımı nasıl?

Hesabınızı silmek için lütfen tek sahibi olduğu tüm paketler sahipliğini aktarma öneririz unutmayın. Daha fazla bilgi edinebilirsiniz [paketinin sahiplerini yönetme](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) yapmak nasıl. Bu da bize isteğiniz hızlandırmak yardımcı olur.

> [!Important]
> Aşağıda, bir kullanıcının silinmesi neden olur:
>  1. İlişkili API anahtarları iptal edin. 
>  2. Herhangi bir alt paket sahibi olarak hesabı kaldırın.
>  3. Bu Hesapla daha önce mevcut tüm kimliği öneki ayırmaları ilişkisini kaldırın.
>  4. Hesap kuruluş üyesi olarak kaldırın.
>  5. Adınızı ayrılmış ve hiç kimse tekrar bizim izinler olmadan yeniden kullanmanız mümkün olacaktır.

Hesap silme işlemine devam etmek için aşağıdaki adımları izleyin.
1. [Oturum açma nuget.org'da](https://www.nuget.org/users/account/LogOn) silmek istediğiniz hesapla.
2. Bu URL'yi tıklayın: [ https://www.nuget.org/account/delete ](https://www.nuget.org/account/delete) hesabı silme isteği göndermek için adımları izleyin.

Müşteri Destek bu isteği işlemek ve hesabını silme işlemi gerçekleştirin.