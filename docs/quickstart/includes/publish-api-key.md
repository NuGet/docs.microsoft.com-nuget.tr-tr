1. [Nuget.org hesabınızda oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) veya zaten yoksa, bir hesap oluşturun.

1. Kullanıcı adınıza (sağ üstte) seçin ve ardından **API anahtarları**.

1. Seçin **Oluştur**, anahtarınız için bir ad belirtin, seçin **kapsamları seçin > anında iletme**. Altında **API anahtarı**, girin * için **Glob deseni**, ardından **Oluştur**. (Aşağıda kapsamları hakkında daha fazla bilgi için bkz.)

1. Anahtar oluşturulduktan sonra seçin **kopyalama** erişim almak için anahtar CLI'daki gerekir:

    ![API anahtarını Panoya kopyalama](../media/QS_Create-02-APIKey.png)

1. **Önemli**: anahtar üzerinde yeniden daha sonra kopyalanamıyor çünkü anahtarınızı güvenli bir konuma kaydedin. API anahtarı sayfasına geri dönün, kopyalamak için anahtar gerekir. Artık paketler CLI göndermek istemiyorsanız, API anahtarı kaldırabilirsiniz.

Kapsam, farklı amaçlar için ayrı API anahtarları oluşturmanıza olanak sağlar. Her anahtar, sona erme zaman çerçevesi olan ve özel paketler (veya glob desenleri) ile sınırlayabilirsiniz. Her anahtar ayrıca belirli işlemler için kapsamlı: yeni paketleri ve güncelleştirmeler, yalnızca güncelleştirmelerini gönderimini veya delisting anında iletme. Kapsam aracılığıyla yalnızca ihtiyaç duydukları iznine sahip oldukları gibi kuruluşunuz için paketleri yöneten farklı kişiler için API anahtarları oluşturabilirsiniz. Daha fazla bilgi için [Introducing kapsamlı API anahtarları](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).