1. [Nuget.org hesabınızda oturum](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) veya zaten yoksa, bir hesap oluşturun.

1. Kullanıcı adınızın (sağ üstte) seçin ve ardından **API anahtarları**.

1. Seçin **oluşturma**, anahtarınız için bir ad, seçin **kapsamları seçin > anında**. Altında **API anahtarı**, girin * için **Glob düzeni**seçeneğini belirleyip **oluşturma**. (Aşağıda kapsamları hakkında daha fazla bilgi için bkz.)

1. Anahtar oluşturulduktan sonra Seç **kopyalama** erişim almak için anahtar CLI gerekir:

    ![API anahtarını Panoya kopyalama](../media/QS_Create-02-APIKey.png)

1. **Önemli**: anahtar üzerinde yeniden daha sonra kopyalanamıyor çünkü anahtarınızı güvenli bir konuma kaydedin. API anahtar sayfasına döndürürse, kopyalanması için anahtarın yeniden oluşturulması gerekir. Artık paketleri CLI itmek istiyorsanız, API anahtarını da kaldırabilirsiniz.

Kapsam, farklı amaçlar için ayrı API anahtarları oluşturmanızı sağlar. Her anahtarı, sona erme zaman dilimi ve belirli paketleri (veya glob desenleri) kapsamlı olabilir. Her anahtar ayrıca belirli işlemler için kapsamlı: yeni paketler ve güncelleştirmeler, güncelleştirmelerinin yalnızca gönderme veya delisting gönderme. Kapsamı aracılığıyla yalnızca ihtiyaç duydukları izinleri sahip olacağı şekilde, kuruluşunuz için paketleri yöneten farklı kişiler için API anahtarları oluşturabilir. Daha fazla bilgi için bkz: [Introducing kapsamlı API anahtarları](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).