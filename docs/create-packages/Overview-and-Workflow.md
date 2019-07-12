---
title: Genel bakış ve NuGet paketleri oluşturma iş akışı
description: Oluşturma ve yayımlama işleminin diğer belirli bölümlerine bağlantılar içeren bir NuGet paketi işleminin genel bakış.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 58ad05cb854c8f7233d90d03c1b320f8797ca2ab
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842397"
---
# <a name="package-creation-workflow"></a>Paket oluşturma iş akışı

Paket oluşturma, paketleme ve diğerleri, genel nuget.org galeri ya da kuruluşunuzdaki özel bir galeri aracılığıyla paylaşmak istediğiniz derlenmiş kod (genellikle .NET derlemelerini) başlar. Paket de paketi yüklendiğinde görüntülenen bir benioku dosyası gibi ek dosyalar içerebilir ve bazı proje dosyaları dönüştürmeleri içerebilir.

Bir paket, yalnızca kendi herhangi bir kod içeren olmadan herhangi bir sayıda diğer bağımlılıkları çekmek için de görebilir. Bu tür bir paket birden çok bağımsız paketlerini oluşan bir SDK'sı sunmak için kullanışlı bir yoldur. Diğer durumlarda, yalnızca sembol paketi içerebilir (`.pdb`) hata ayıklama yardımcı olmak için dosyaları.

> [!Note]
> Diğer geliştiriciler tarafından kullanılmaya bir paket oluşturduğunuzda, bunlar iş üzerinde bir bağımlılık sürüp anlamak önemlidir. Bu nedenle, oluşturma ve bir paket yayımlama hataları düzeltiyor ve diğer güncelleştirmeler yapma taahhüdü ayrıca gelir veya çok az yapmayı paketi olarak kullanılabilir açık kaynak diğerleri tutmak için yardımcı olabilmemiz için.

Her durumda, paket oluşturma tanımlayıcısını, sürüm numarası, lisans, telif hakkı bilgileri ve diğer tüm gerekli içeriği karar ile başlar. Bunu yaptıktan sonra her şeyi birlikte yerleştirmenin "paketi" komutunu kullanabilirsiniz bir `.nupkg` dosya. Bu dosya için bir NuGet akışı, nuget.org gibi yayımlanabilir.

> [!Tip]
> Bir NuGet paketi ile `.nupkg` ZIP dosyası yalnızca bir uzantısıdır. Kolayca bir paket içeriğini incelemek için uzantı değiştirme `.zip` ve içerikleri her zamanki şekilde genişletin. Yalnızca uzantı değiştirdiğinizden emin olun geri `.nupkg` bir konağa karşıya yüklemeyi yeniden denemeden önce.

Öğrenin ve oluşturma süreci anlamak için başlayın [paket oluşturma](../create-packages/creating-a-package.md) hangi kılavuzları, ortak çekirdek süreçler tüm paketler için.

Burada, paketiniz için bir dizi diğer seçenekleri göz atabilirsiniz:

- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md) bir paket için farklı bir .NET Framework ile birden çok çeşitleri oluşturmayı açıklar.
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md) nasıl bir paket birden çok dil kaynakları ile ve yerelleştirilmiş ayrı uydu paketlerin nasıl kullanılacağına yönelik açıklar.
- [Yayın öncesi paketleri](../create-packages/prerelease-packages.md) sürüm alfa, beta ve ilgilenen müşteriler için rc paketler gösterilmektedir.
- [Kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md) hem tek yönlü belirteci değişiklik projeye eklenir ve Değiştir dosyalarında nasıl yapabileceğiniz açıklanır `web.config` ve `app.config` paket kaldırıldığında ayrıca desteklenen çıkış ayarları .
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md) kitaplığınızı için hata ayıklama sırasında kodunuzda adım tüketicilerin izin semboller sağlama için yönergeler sunar.
- [Paket sürümü oluşturma](../reference/package-versioning.md) bağımlılıklarınızı (paketinizi tükettiğiniz diğer paketleri) için izin tam sürümünü belirlemek nasıl ele alınmaktadır.
- [Yerel paketler](../create-packages/native-packages.md) C++ Tüketiciler için paket oluşturma işlemi açıklanmaktadır.
- [İmzalama paketleri](../create-packages/sign-a-package.md) bir paket için bir dijital imza ekleme işlemi açıklanır.

Ardından nuget.org için bir paketi yayımlamaya hazır olduğunuzda, basit işlemde izleyin [paket yayımlama](../nuget-org/publish-a-package.md).

Nuget.org yerine özel bir akış kullanmak istiyorsanız, bkz. [barındırma paketleri genel bakış](../hosting-packages/overview.md)
