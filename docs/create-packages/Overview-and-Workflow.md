---
title: Genel bakış ve NuGet paketleri oluşturma iş akışı
description: Oluşturma ve yayımlama işleminin diğer belirli bölümlerine bağlantılar ile bir NuGet paketi işlemine genel bakış.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: a9dd4439f2aa72424187eaa2d9555d5af0e7843d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="package-creation-workflow"></a>Paket oluşturma iş akışı

Paket oluşturma paketini ve diğer ortak nuget.org galeri veya kuruluşunuzdaki özel bir galeri ile paylaşmak istediğiniz derlenmiş kod (genellikle .NET derlemelerini) başlar. Paket da paketi yüklendiğinde görüntülenen bir benioku dosyası gibi ek dosyalar içerebilir ve belirli proje dosyalarına dönüştürmeleri içerebilir.

Bir paket, yalnızca kendi herhangi bir kod içeren olmadan herhangi bir sayıda başka bir bağımlılık çıkarmak için Ayrıca hizmet verebilir. Bu tür bir paket birden çok bağımsız paketlerini oluşan bir SDK sunmak için uygun bir yoludur. Diğer durumlarda, bir paket yalnızca simge içerebilir (`.pdb`) hata ayıklama yardımcı olmak için dosyaları.

> [!Note]
> Diğer geliştiriciler tarafından kullanılmak üzere bir paket oluşturduğunuzda, bunlar bir bağımlılık üzerindeki çalışmanızı kaplayan anlamak önemlidir. Bu nedenle, oluşturma ve yayımlama bir paketi hataları düzelttikten ve diğer güncelleştirmeleri yapma taahhüdü ayrıca anlamına gelir veya çok az yapmayı kullanılabilir olarak paket Kaynağı Aç başkalarının devam ettirmek için yardımcı olacak.

Her durumda, paket oluşturma hangi derlemelerin ve diğer dosyaları paketi oluşturmaya karar ile başlar. Ardından olarak adlandırılan bir bildirim dosyası, oluşturduğunuz bir `.nuspec` tanımlayıcısını, sürüm numarası, telif hakkı bilgileri, MSBuild özellik ve hedefler ve daha fazlasını birlikte paketin içeriğini açıklamak için dosya.

Ne zaman uygun klasörlerdeki tüm gerekli dosyaların hazırladığınız ve uygun oluşturduysanız `.nuspec` dosya, ardından kullandığınız `nuget pack` komutu (veya [MSBuild paketi hedef](../reference/msbuild-targets.md)) her şeyi birlikte içine yerleştirilecek bir `.nupkg` dosya. Ardından hangi ana kullanılabilir diğer geliştiricilerine kolaylaştırır için paketi dağıtmak hazırsınız.

> [!Tip]
> Bir NuGet paketi ile `.nupkg` ZIP dosyası yalnızca bir uzantısıdır. Kolayca herhangi paketin içeriğini incelemek için uzantı değiştirmek `.zip` ve içeriğini normal şekilde genişletin. Yalnızca dahili değiştirdiğinizden emin olun geri `.nupkg` bir ana bilgisayara yüklemeye çalışmadan önce.

Bilgi edinmek ve oluşturma işlemini anlamak için başlayın [paket oluşturma](../create-packages/creating-a-package.md) hangi kılavuzları, ortak çekirdek süreçlerle tüm paketler.

Buradan, paketiniz için bir dizi diğer seçenek düşünebilirsiniz:

- [Birden çok hedef çerçeveyi destekleyen](../create-packages/supporting-multiple-target-frameworks.md) bir paket için farklı .NET Framework ile birden çok çeşitleri oluşturmayı açıklar.
- [Yerelleştirilmiş paketleri oluşturma](../create-packages/creating-localized-packages.md) birden çok dil kaynakları olan bir paketi yapısı ve ayrı yerelleştirilmiş uydu paketlerini kullanma açıklar.
- [Paketleri sürüm öncesi](../create-packages/prerelease-packages.md) alfa, beta ve ilgilendiğiniz Bu müşterileri rc paketleri yayımlamayı gösterilmiştir.
- [Kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md) hem tek yönlü belirteci değişikliklerini projeye eklenir ve değiştirme dosyalarında nasıl yapabileceğiniz açıklanır `web.config` ve `app.config` paket kaldırıldığında de yedeklenen çıkış ayarları .
- [Sembol paketlerini](../create-packages/symbol-packages.md) hata ayıklama sırasında kodunuza adım tüketicilerin izin kitaplığınızın simgelerini sağlama için yönergeler sunar.
- [Sürüm oluşturma paketini](../reference/package-versioning.md) , bağımlılıklar (paketinizi tüketen diğer paketleri) için izin tam sürümünü belirlemek nasıl ele alınmaktadır.
- [Yerel Paketleri](../create-packages/native-packages.md) C++ Tüketiciler için paket oluşturma işlemi açıklanmaktadır.
- [Paket imzalama](../create-packages/sign-a-package.md) bir paket için bir dijital imza ekleme işlemi açıklanmaktadır.

Ardından nuget.org için bir paketi yayımlamaya hazır olduğunuzda, basit işleminde izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).

Nuget.org yerine özel bir akış kullanmak istiyorsanız, bkz: [barındırma paketleri genel bakış](../hosting-packages/overview.md)