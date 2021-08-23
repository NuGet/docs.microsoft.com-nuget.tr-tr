---
title: Güvenli yazılım tedarik zinciri için en iyi uygulamalar
description: NuGet & GitHub kullanarak yazılım tedarik zincirinizin güvenliğini sağlamaya yönelik en iyi uygulamalar.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726983"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Güvenli yazılım tedarik zinciri için en iyi uygulamalar

Açık kaynak her yerde. Bu, birçok özel kod tabanı ve topluluk projesinde bulunur. Kuruluşlar ve bireyler için bugün soru, açık kaynak kodu, ne kadar kullandığınız açık kaynak kodu ve ne kadarını kullandıklarından bağımsız değildir.

Yazılım tedarik zincirinde nelerin olduğunu bilmiyorsanız, bağımlılıklarınızın birindeki bir yukarı akış güvenlik açığı önemli olabilir, sizin ve müşterilerinizin olası bir uzlaşmaya karşı savunmasız olduğunu fark edebilir. Bu belgede, "yazılım sağlama Zinciri" teriminin ne anlama geldiğini, ne kadar önemli olduğunu ve projenizin tedarik zincirinizin en iyi yöntemlerle güvenliğini nasıl sağlayabileceğinize ilişkin daha ayrıntılı bilgi göndereceğiz.

![Octoverse 2020-açık kaynak durumu](media/opensource-percent.png)

## <a name="dependencies"></a>Bağımlılıklar 

Yazılım tedarik zinciri terimi, yazılımlarınıza ve nereden geldiğini gösteren her şeye başvurmak için kullanılır. Bu, yazılım tedarik zincirinizin bağımlı olduğu bağımlılıklarınızın bağımlılıklarıdır ve özelliklerdir. Bir bağımlılık, yazılımınızın çalışması için gereken şeydir. Kod, ikili dosyalar veya başka bileşenler ve nereden geldiği, örneğin bir depo veya paket yöneticisi olabilir.

Kodu kimin yazdığı, katkıda bulunduğu zaman, güvenlik sorunları, bilinen güvenlik açıkları, desteklenen sürümler, lisans bilgileri ve işlemin herhangi bir noktasında dokunduğu her türlü şey hakkında kim olduğunu içerir.

Tedarik zincirinizin yanı sıra, derleme ve paketleme betikleri ya da uygulamanızın dayandığı altyapıyı çalıştıran yazılımlar gibi tek bir uygulamanın ötesinde yığınınızın diğer bölümlerini de kapsar.

## <a name="vulnerabilities"></a>Güvenlik Açıkları

Günümüzde yazılım bağımlılıkları daha fazla. Kendi kendinize yazmak zorunda olmayan işlevler için, projelerinizin yüzlerce açık kaynaklı bağımlılığı kullanması oldukça yaygındır. Bu, uygulamanızın büyük bir kısmının yazmayacağınız koddan oluştuğu anlamına gelebilir. 

![Octoverse 2020-Dependencies durumu](media/dependencies.png)

Üçüncü tarafınız veya açık kaynaklı bağımlılıklarda olası güvenlik açıkları, sizin yazdığınız kod kadar sıkı bir şekilde denetleyemezsiniz ve bu da tedarik zincirinizdeki olası güvenlik riskleri oluşturabilir.

Bu bağımlılıklardan birinde bir güvenlik açığı varsa, bir güvenlik açığına de sahip olursunuz. Bağımlılıklarınızın biri bile farkında olmadan değişebilir, bu da korbir olabilir. Bir güvenlik açığı bugün bağımlılığı içinde olsa da açıktan yararlanılamaz, gelecekte de açıktan yararlanabilir. 

Binlerce açık kaynaklı geliştiricilerin ve kitaplık yazarlarının işinin yararlanması, binlerce yabancıların doğrudan üretim kodunuza etkin bir şekilde katkıda bulunabilmesine yol açabiliyor. Yazılım tedarik zincirinizin üzerinden ürününüz, düzeltme eki yüklenmemiş güvenlik açıklarına, masum hatalara veya hatta bağımlılıklara karşı kötü amaçlı saldırılara karşı etkilenir.

## <a name="supply-chain-compromises"></a>Tedarik zinciri ile mücadele

Bir tedarik zincirinin geleneksel tanımı üretilenden gelir; Bu, bir şeyi oluşturmak ve sağlamak için gereken işlem zinciridir. Planlama, malzemeler, üretim ve perakende tedarik bilgilerini içerir. Bir yazılım tedarik zinciri, malzemeler yerine kod olarak benzerdir. Üretim yerine geliştirme aşamasındadır. Kod, temelden değil, tedarikçilere, ticari veya açık kaynaktan kaynaklıdır ve genel olarak, açık kaynak kodu depolardan gelir. Bir depodan kod eklemek, ürününüzün bu koda bir bağımlılık aldığı anlamına gelir.

Yazılım tedarik zinciri saldırılarına bir örnek, kötü amaçlı kod bir bağımlılığa tam olarak eklendiğinde, kodu kurbanlarına dağıtmak için bu bağımlılığın Arz Zinciri kullanılarak oluşur. Tedarik zinciri saldırıları gerçek bir sayıdır. Bir tedarik zincirine saldırmak için, kötü amaçlı kodu doğrudan yeni bir katkı olarak ekleme, katkıda bulunan hesabını diğerleri olmadan yaşıyorsanız veya hatta bağımlılığın bir parçası olmayan yazılımları dağıtmak için bir imzalama anahtarıyla ödün veren birçok yöntem vardır.

Bir yazılım tedarik zinciri saldırısı, bir saldırganın kötü amaçlı yazılım eklemesi veya gelecekteki erişim için bir arka kapı sağlaması için bir fırsatın başıdır.

![Octoverse 2020-güvenlik açığı yaşam döngüsünün durumu](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Düzeltme eki yüklenmemiş yazılım

Bugün açık kaynak kullanımı önemlidir ve kısa süre içinde yavaşmak beklenmez. Açık kaynaklı yazılım kullanmayı durdurduğumuz için, zincir güvenliği sağlama tehdidi düzeltme eki yüklenmemiş bir yazılımdır. Bunun farkında olmak üzere, projenizin bağımlılığının güvenlik açığına sahip olduğu riski nasıl ele alabilirsiniz?

- **Ortamınızda ne olduğunu bilin.** Bu, güvenlik açıkları veya lisanslama kısıtlamaları gibi bağımlılıkların risklerini anlamak için bağımlılıklarınızın ve tüm geçişli bağımlılıkların bulunmasını gerektirir.
- **Bağımlılıklarınızı yönetin.** Yeni bir güvenlik açığı bulunduğunda, etkilenip etkilenmediğinizi belirlemelisiniz ve gerekiyorsa, en son sürüme ve güvenlik düzeltme ekine güncelleştirme yapın. Bu, yeni bağımlılıklar oluşturan veya eski bağımlılıkları düzenli olarak denetleyen değişiklikleri gözden geçirmek için özellikle önemlidir.
- **Tedarik zincirinizi izleyin.** Bu, bağımlılıklarınızı yönetmek için yaptığınız denetimleri denetleyerek. Bu, bağımlılıklarınız için daha kısıtlayıcı koşulların karşılanmasını zorlamanıza yardımcı olur.

![Octoverse 2020-Danışma durumu](media/advisories.png)

NuGet ve GitHub sağladığı çeşitli araçlar ve teknikler ele alınacaktır. bu, günümüzde projenizin içindeki olası riskleri karşılamak için kullanabilirsiniz. 

## <a name="knowing-what-is-in-your-environment"></a>Ortamınızda nelerin olduğunu bilme

### <a name="nuget-dependency-graph"></a>NuGet bağımlılık grafiği

**📦 Paket tüketicisi**

projenizdeki NuGet bağımlılıklarınızı doğrudan ilgili proje dosyasına bakarak görebilirsiniz.

Bu genellikle iki konumdan birinde bulunur:

-   [`packages.config`](../reference/packages-config.md) – Proje kökünde bulunur.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Proje dosyasında bulunur. 

NuGet bağımlılıklarınızı yönetmek için kullandığınız yönteme bağlı olarak, bağımlılıklarınızı doğrudan [Çözüm Gezgini](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) veya [NuGet Paket Yöneticisi](../consume-packages/install-use-packages-visual-studio.md)görüntülemek için Visual Studio de kullanabilirsiniz.

CLı ortamları için, [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) projenizi veya çözümünüzün bağımlılıklarını listelemek için komutunu kullanabilirsiniz. 

NuGet bağımlılıklarını yönetme hakkında daha fazla bilgi için [aşağıdaki belgelere bakın](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>GitHub bağımlılık grafı 

**📦 Paket tüketicisi | 📦🖊 Paket yazarı**

projenizin bağımlı olduğu paketleri ve ona bağlı olan depoları görmek için GitHub bağımlılık grafiğini kullanabilirsiniz. Bu, bağımlılıklarında algılanan güvenlik açıklarını görbaşlamanıza yardımcı olabilir.

GitHub depo bağımlılıkları hakkında daha fazla bilgi için [aşağıdaki belgelere bakın](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Bağımlılık sürümleri

**📦 Paket tüketicisi | 📦🖊 Paket yazarı**

Güvenli bir bağımlılık zinciri zinciri sağlamak için, tüm bağımlılıklarınızın & araçları, bilinen güvenlik açıklarına en son işlevselliği ve güvenlik düzeltme eklerini dahil edecek şekilde en son kararlı sürüme düzenli olarak güncelleştirildiğinden emin olmak isteyeceksiniz. Bağımlılıklarınız, bağımlı olduğunuz kodu, kullandığınız ikili dosyaları ve diğer bileşenleri içerebilir. Bu şunlar olabilir:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK & çalışma zamanı](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [NuGet paketleri](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Bağımlılıklarınızı yönetin

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>kullanım dışı ve güvenlik açığı bağımlılıkları NuGet

**📦 Paket tüketicisi | 📦🖊 Paket yazarı**

Proje veya çözümünüz içinde olabilecek bilinen ve kullanılmayan bağımlılıkları listelemek için [DotNet CLI](/dotnet/core/tools/dotnet-list-package) kullanabilirsiniz. Bilinen kullanım dışı bırakma `dotnet list package --deprecated` `dotnet list package --vulnerable` ve güvenlik açıklarının bir listesini sağlamak için komutunu kullanabilirsiniz.

### <a name="github-vulnerable-dependencies"></a>GitHub güvenlik açığı bağımlılıkları

**📦 Paket tüketicisi | 📦🖊 Paket yazarı**

projeniz GitHub üzerinde barındırılıyorsa, projenizdeki güvenlik güvenlik açıklarını ve hataları bulmak için [GitHub güvenlik](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) özelliğinden yararlanarak, bir çekme isteğini kod tabanınıza göre açarak bağımlılıkları düzeltir. 

["Sola Ötele"](https://en.wikipedia.org/wiki/Shift-left_testing) hareketinin bir hedefi, sunulmadan önce güvenlik açığı olan bağımlılıkları yakalamak. Bağımlılıklarınız hakkında, lisansları, geçişli bağımlılıklar ve bağımlılıkların yaşı gibi bilgiler, yalnızca bunu yapmanıza yardımcı olur.

Bağımlı Kabot uyarıları & güvenlik güncelleştirmeleri hakkında daha fazla bilgi için [aşağıdaki belgelere bakın](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>NuGet akışlar

**📦 Paket tüketicisi**

birden çok ortak & özel NuGet kaynak akışı kullanırken, bir paket herhangi bir akışdan indirilebilir. Yapınızı [bağımlılık karışıklık](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)gibi bilinen saldırılara karşı öngörülebilir ve güvenli hale geldiğinden emin olmak için, paketlerinizin hangi belirli akışların geldiğini bilmek en iyi uygulamadır. Koruma için yukarı akış özelliklerine sahip tek bir akış veya özel akış kullanabilirsiniz.

Paket akışlarınızın güvenliğini sağlama hakkında daha fazla bilgi için bkz. [özel paket akışlarını kullanırken riski azaltmak için 3 yol](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>İstemci güven ilkeleri

**📦 Paket tüketicisi**

Oturum açmanız gereken paketlerin imzalanabilmesi için kullanabileceğiniz ilkeler vardır. bu, yazar imzalandığı sürece bir paket yazarına güvenmesini veya NuGet. org tarafından imzalanan belirli bir kullanıcı veya hesaba aitse bir pakete güvenmesini sağlar.

İstemci güven ilkelerini yapılandırmak için [aşağıdaki belgelere bakın](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Dosyaları kilitle

**📦 Paket Tüketicisi**

Kilit dosyaları, paketinizin içeriğinin karması depolar. Yüklemek istediğiniz paketin içerik karması kilit dosyasıyla eşlanıyorsa, paketin yinelenebilir olmasını sağlar.

Kilit dosyalarını etkinleştirmek için [aşağıdaki belgelere bakın.](../consume-packages/package-references-in-project-files.md#locking-dependencies)

## <a name="monitor-your-supply-chain"></a>Tedarik zincirinizi izleme

### <a name="github-secret-scanning"></a>GitHub'da gizli dizi tarama

**📦🖊 Paket Yazarı**

GitHub yanlışlıkla işlenen gizli dizilerin sahte NuGet önlemek için api anahtarlarının depolarını tarar. 

Gizli tarama hakkında daha fazla bilgi edinmek için [bkz. Gizli bilgi tarama hakkında.](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)

### <a name="author-package-signing"></a>Paket İmzalama Yazma

**📦🖊 Paket Yazarı**

[Yazar imzalama,](../reference/signed-packages-reference.md) paket yazarının kimliğini bir pakete damgalamasını ve bir tüketicinin sizin kimliğinizi doğrulamasını sağlar. Bu sizi içerik üzerinde oynanmaya karşı korur ve paketin kaynağı ve paketin orijinalliği hakkında tek bir gerçeklik kaynağı olarak görev sağlar. İstemci güven ilkeleriyle bir araya geldiğinde, paketin belirli bir yazardan geldiğini doğruabilirsiniz.

Paket imzalamak için bkz. [Paket imzalama.](../create-packages/sign-a-package.md)

### <a name="two-factor-authentication-2fa"></a>Two-Factor Kimlik Doğrulaması (2FA)

**📦🖊 Paket Yazarı**

İki faktörlü kimlik doğrulamasını (2FA) etkinleştirmek, [GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) veya [NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)genel paket deposunda oturum aken ek bir güvenlik katmanı ekleyebilir. Bilgisayarınızı korumak için iki faktörlü kimlik doğrulamasını etkinleştirmeniz önerilir.

### <a name="package-id-prefix-reservation"></a>Paketleme kimlik ön eki ayırma 

**📦🖊 Paket Yazarı**

Paketlerinizin kimliğini korumak için, paket kimliği ön ekin belirtilen ölçütlere uygun şekilde denk geliyorsa eşleşen bir sahibi ilişkilendirmek üzere ilgili ad alanınıza bir paket kimliği ön [eki ayırmanız gerekir.](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) 

Kimlik ön eklerini ayırma hakkında bilgi edinmek için bkz. [Paket Kimliği ön eki rezervasyonu.](../nuget-org/id-prefix-reservation.md)

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Güvenlik açığı olan bir paketi kullanımdan kaldırdık ve listeden kaldırdık

**📦🖊 Paket Yazarı**

.NET paket ekosistemini, yazmanız gereken bir pakette güvenlik açığı olduğunu fark ettiyken korumak için paketi kullanımdan sildi ve paket arayan kullanıcılardan gizlenecek şekilde listeye dahil etmek için en iyi şekilde çalışın. Kullanım dışı ve listelenmemiş bir paket kullanıyorsanız, paketi kullanmaktan kaçınabilirsiniz.

Bir paketin kullanım dışı ve listelerini nasıl geri alınarak silinecek hakkında bilgi edinmek için, paketlerin kullanım dışı ve listelerini geri alama [ile](../nuget-org/deprecate-packages.md) ilgili [aşağıdaki belgelere bakın.](../nuget-org/policies/deleting-packages.md#unlisting-a-package)

## <a name="summary"></a>Özet

Yazılım tedarik zinciriniz, kodunuzla ilgili olan veya onu etkileyen her şeydir. Tedarik zinciri güvenliğinin tehlikeye atları gerçek ve popülerliği artsa da hala nadirdir; Bu nedenle, en önemli şey bağımlılıklarınızı  fark etme, bağımlılıklarınızı yönetme ve tedarik zincirinizi izleme ile tedarik **zincirinizi korumaktır.**

Tedarik zincirinizi görüntüleme, yönetme ve NuGet [ve](/learn/modules/maintain-secure-repository-github/) izleme konusunda daha etkili olmak için NuGet ve GitHub sağlayan çeşitli yöntemler hakkında bilgi öğrendiniz.

Dünyanın yazılımının güvenliğini sağlama hakkında daha fazla bilgi için bkz. [Octoverse 2020 Güvenlik Raporu'nun Durumu.](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)
