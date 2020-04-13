---
title: NuGet paketleri oluşturma genel bakış ve iş akışı
description: Bir NuGet paketi oluşturma ve yayımlama işlemine genel bakış ve sürecin diğer belirli bölümlerine bağlantılar.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488851"
---
# <a name="package-creation-workflow"></a>Paket oluşturma iş akışı

Paket oluşturma, genel nuget.org galerisi veya kuruluşunuzdaki özel bir galeri aracılığıyla paketleyip başkalarıyla paylaşmak istediğiniz derlenmiş kodla (genellikle .NET derlemeleri) başlar. Paket, paket yüklendiğinde görüntülenen okuma memu gibi ek dosyalar da içerebilir ve belirli proje dosyalarına dönüşümler içerebilir.

Bir paket, kendi kodunu içermeden yalnızca herhangi bir sayıda diğer bağımlılıkları çekmede de hizmet edebilir. Böyle bir paket, birden çok bağımsız paketiçeren bir SDK sunmak için kullanışlı bir yoldur. Diğer durumlarda, bir paket hata`.pdb`ayıklama yardımcı olmak için yalnızca sembol ( ) dosyaları içerebilir.

> [!Note]
> Diğer geliştiriciler tarafından kullanılmak üzere bir paket oluşturduğunuzda, bunların işinize bağımlı olduğunu anlamanız önemlidir. Bu nedenle, bir paket oluşturma ve yayımlama da hataları düzeltmek ve diğer güncelleştirmeler yapma, ya da en azından başkalarının korumak için yardımcı olabilir böylece paketi açık kaynak olarak kullanılabilir hale bir taahhüt anlamına gelir.

Durum ne olursa olsun, bir paket oluşturma tanımlayıcısı, sürüm numarası, lisans, telif hakkı bilgileri ve diğer gerekli içeriğe karar vermekle başlar. Bir kez yapıldıktan sonra, her şeyi bir `.nupkg` dosyada bir araya getirmek için "paket" komutunu kullanabilirsiniz. Bu dosya, nuget.org gibi bir NuGet akışında yayınlanabilir.

> [!Tip]
> Uzantılı `.nupkg` bir NuGet paketi sadece bir ZIP dosyasıdır. Herhangi bir paketin içeriğini kolayca incelemek için `.zip` uzantıyı değiştirin ve içeriğini her zamanki gibi genişletin. Bir ana bilgisayara `.nupkg` yüklemeyi denemeden önce uzantıyı geri değiştirdiğinden emin olun.

Oluşturma işlemini öğrenmek ve anlamak için, tüm paketlerde ortak olan temel işlemlerde size yol gösteren [bir paket oluşturma](../create-packages/creating-a-package.md) ile başlayın.

Buradan, paketiniz için diğer seçenekler bir dizi düşünebilirsiniz:

- [Birden Çok Hedef Çerçeveleri destekleyen,](../create-packages/supporting-multiple-target-frameworks.md) farklı .NET Çerçeveleri için birden çok varyantı olan bir paketin nasıl oluşturulacak olduğunu açıklar.
- [Yerelleştirilmiş Paketler oluşturma,](../create-packages/creating-localized-packages.md) bir paketin birden çok dil kaynağıyla nasıl yapılandırılabildiğini ve ayrı yerelleştirilmiş uydu paketlerinin nasıl kullanılacağını açıklar.
- [Ön sürüm Paketleri,](../create-packages/prerelease-packages.md) alfa, beta ve rc paketlerinin ilgilenen müşterilere nasıl yayınlanabildiğini gösterir.
- [Kaynak ve Config Dosya Dönüşümleri,](../create-packages/source-and-config-file-transformations.md) projeye eklenen dosyalarda hem tek yönlü belirteç değiştirmeleri `app.config` yapabileceğinizi hem de paket kaldırıldığında yedeklenen ayarları nasıl değiştirebileceğinizi `web.config` açıklar.
- [Sembol Paketleri,](../create-packages/symbol-packages-snupkg.md) kitaplığınız için tüketicilerin hata ayıklama sırasında kodunuza adım atmasını sağlayan semboller sağlamak için kılavuz sunar.
- [Paket sürümü,](../concepts/package-versioning.md) bağımlılıklarınız için izin verdiğiniz tam sürümleri (paketinizden tükettiğiniz diğer paketler) nasıl tanımlayabileceğinizi tartışır.
- [Yerel Paketler,](../guides/native-packages.md) C++ tüketicileri için bir paket oluşturma işlemini açıklar.
- [İmza Paketleri,](../create-packages/sign-a-package.md) pakete dijital imza ekleme işlemini açıklar.

Daha sonra nuget.org için bir paket yayımlamaya hazır olduğunuzda, [paket yayımla'daki](../nuget-org/publish-a-package.md)basit işlemi izleyin.

nuget.org yerine özel bir özet kullanmak istiyorsanız, [Barındırma Paketlerine Genel Bakış](../hosting-packages/overview.md)
