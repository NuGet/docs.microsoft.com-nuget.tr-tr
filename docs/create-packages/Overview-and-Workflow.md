---
title: NuGet paketleri oluşturma ile genel bakış ve iş akışı
description: Bir NuGet paketi oluşturma ve yayımlama sürecine genel bir bakış, bu işlemin diğer belirli bölümlerinin bağlantılarıyla birlikte.
author: JonDouglas
ms.author: jodou
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: d34f8e73dce64a58393433637067651fced08173
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774682"
---
# <a name="package-creation-workflow"></a>Paket oluşturma iş akışı

Bir paket oluşturmak, diğer kişilerle paketlemek ve paylaşmak istediğiniz derlenmiş kodla (genellikle .NET derlemeleri), genel nuget.org Galerisi veya kuruluşunuzdaki özel bir galeri aracılığıyla başlar. Paket, paket yüklendiğinde görüntülenen bir Benioku dosyası gibi ek dosyaları da içerebilir ve belirli proje dosyalarına dönüşümler ekleyebilir.

Bir paket, kendi herhangi bir kodunu eklemeden yalnızca herhangi bir sayıda bağımlılığı çekmeye de sunabilir. Bu tür bir paket, birden çok bağımsız paketten oluşan bir SDK 'Yı sunmaya yönelik kullanışlı bir yoldur. Diğer durumlarda, bir paket `.pdb` hata ayıklamaya yardımcı olmak için yalnızca symbol () dosyaları içerebilir.

> [!Note]
> Diğer geliştiriciler tarafından kullanılmak üzere bir paket oluşturduğunuzda, çalışmanız üzerinde bir bağımlılık aldığını anlamak önemlidir. Bu nedenle, bir paketi oluşturma ve yayımlama, Ayrıca hataları düzeltmeye ve diğer güncelleştirmeler yapmaya yönelik bir taahhütte, diğer bir deyişle, diğer kullanıcıların BT 'nin bakımını yapmaya yardımcı olması için paketin açık kaynak olarak kullanılabilir hale getirilmesi da anlamına gelir.

Ne olursa olsun bir paket oluşturmak, tanımlayıcı, sürüm numarası, lisans, telif hakkı bilgileri ve diğer gerekli içeriklere karar vererek başlar. İşiniz bittiğinde, her şeyi bir dosyaya yerleştirmek için "Pack" komutunu kullanabilirsiniz `.nupkg` . Bu dosya, nuget.org gibi bir NuGet akışına yayımlanabilir.

> [!Tip]
> Uzantılı bir NuGet paketi `.nupkg` yalnızca BIR ZIP dosyasıdır. Her paketin içeriğini kolayca incelemek için, uzantıyı `.zip` olarak değiştirin ve içeriği her zamanki gibi genişletin. Uzantıyı `.nupkg` bir konağa yüklemeyi denemeden önce olarak yeniden değiştirmeniz yeterlidir.

Oluşturma sürecini öğrenmek ve anlamak için, tüm paketlerde ortak olan çekirdek süreçler boyunca size kılavuzluk eden [bir paket oluşturmaya](../create-packages/creating-a-package.md) başlayın.

Buradan, paketiniz için birkaç farklı seçenek göz önünde bulundurmanız gerekir:

- [Birden çok hedef çerçeveyi desteklemek](../create-packages/supporting-multiple-target-frameworks.md) , farklı .net çerçeveleri için birden çok çeşitle bir paket oluşturmayı açıklar.
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md) , birden çok dil kaynağı olan bir paketin nasıl yapılandırılacağını ve ayrı yerelleştirilmiş uydu paketlerinin nasıl kullanılacağını açıklar.
- [Yayın öncesi paketleri](../create-packages/prerelease-packages.md) , Alpha, Beta ve RC paketlerinin ilgilenen müşterilere nasıl yayınlanacağını gösterir.
- [Kaynak ve yapılandırma dosyası dönüştürmeleri](../create-packages/source-and-config-file-transformations.md) , bir projeye eklenen dosyalardaki tek yönlü belirteç değiştirme işlemlerini ve `web.config` `app.config` paket kaldırıldığında da desteklenen ayarları değiştirebilir ve bunlarla değişiklik yapabilir.
- [Sembol paketleri](../create-packages/symbol-packages-snupkg.md) , hata ayıklarken tüketicilere, kodlarınızın kodunuzda çalışmasına imkan tanıyan semboller sağlamak için rehberlik sunar.
- [Paket sürümü oluşturma](../concepts/package-versioning.md) , bağımlılıklarınız için izin verilen tam sürümleri (paketinizden kullandığınız diğer paketler) nasıl tanımlayabileceğinizi anlatmaktadır.
- [Yerel paketler](../guides/native-packages.md) , C++ tüketicileri için bir paket oluşturma işlemini açıklar.
- [Imzalama paketleri](../create-packages/sign-a-package.md) , bir pakete dijital imza ekleme işlemini açıklar.

Daha sonra nuget.org ' e bir paket yayımlamaya hazırsanız, [paket yayımlama](../nuget-org/publish-a-package.md)içindeki basit süreci izleyin.

Nuget.org yerine özel bir akış kullanmak istiyorsanız, [barındırma paketlerine genel bakış](../hosting-packages/overview.md) ' a bakın.
