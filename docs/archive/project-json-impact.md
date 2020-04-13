---
title: NuGet paket yazarları üzerinde project.json etkisi
description: NuGet 3.x'te project.json uygulamasının desteklenmeyen özellikler, içerik ve paket biçimi gibi paket yazarlarını nasıl etkilediğine ilişkin ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488192"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Paket oluştururken project.json'un etkisi

> [!Important]
> Bu içerik amortismana hazırdır. Projeler `packages.config` de PackageReference biçimlerini kullanmalıdır.

NuGet 3+'da kullanılan `project.json` sistem, aşağıdaki bölümlerde açıklandığı gibi paket yazarlarını çeşitli şekillerde etkiler.

## <a name="changes-affecting-existing-packages-usage"></a>Varolan paket kullanımını etkileyen değişiklikler

Geleneksel NuGet paketleri, geçişli dünyaya taşınamayan bir dizi özelliği destekler.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Komut dosyalarını yükleme ve kaldırma

[Bağımlılık çözümünde](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)açıklanan geçişli geri yükleme modelinde "paket yükleme süresi" kavramı yoktur. Paket var veya yok, ancak paket yüklendiğinde oluşan tutarlı bir işlem yoktur.

Ayrıca, yükleme komut dosyaları yalnızca Visual Studio'da desteklendi. Diğer IDA'lar bu tür komut dosyalarını desteklemek için Visual Studio genişletilebilirlik API'si ile alay etmek zorunda kaldı ve ortak editörler ve komut satırı araçlarında destek yoktu.

### <a name="content-transforms-are-not-supported"></a>İçerik dönüşümleri desteklenmiyor

Komut dosyalarını yüklemeye benzer şekilde, dönüşümler paket yüklemede çalışır ve genellikle idempotent değildir. Artık yükleme zamanı olmadığından, XDT Dönüşümü ve benzeri özellikler desteklenmez ve böyle bir paket geçişli bir senaryoda kullanılırsa yoksayılır.

### <a name="content"></a>İçerik

Geleneksel NuGet paketleri, kaynak kodu ve yapılandırma dosyaları gibi içerik dosyalarını göndermiştir. Genellikle iki senaryoda kullanılır:

1. Kullanıcının bunları daha sonra düzenlemesi için projeye bırakılan ilk dosyalar. Yaygın örnek varsayılan yapılandırma dosyalarıdır.

1. Projede yüklü olan derlemelere yardımcı olarak kullanılan içerik dosyaları. Buradaki örnek, bir derleme tarafından kullanılan bir logo görüntüsü olacaktır.

İçerik desteği şu anda komut dosyaları ve dönüşümler için benzer nedenlerle devre dışı bırakılmıştır, ancak içerik için destek tasarlama aşamasındayız.

İçerik dosyaları hala paketler içinde taşınabilir ve şu anda yoksayılır, ancak son kullanıcı bunları yine de doğru noktaya kopyalayabilir.

İçerik dosyalarını geri getirmek için önerilerden birini görebilir ve [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)ilerlemeyi buradan takip edebilirsiniz: .

## <a name="impact-for-package-authors"></a>Paket yazarlar için etki

Yukarıdaki özellikleri kullanan paketlerfarklı bir mekanizma kullanmak zorunda kalacak. Bunun için en yaygın olarak yararlı mekanizma tam olarak desteklenmeye devam msbuild hedefleri / sahne olacaktır. Yapı sistemi paketteki diğer kuralları almayı seçebilir. Bu şekilde MSBuild hedefleri yanı sıra Roslyn analizörleri desteklenir. Hedefleri ve çözümleyicileri `packages.config` destekleyen `project.json` paketler oluşturmak mümkündür.

Başlatmayı kolaylaştırmak için projeyi değiştirmeye çalışan paketler genellikle çok sınırlı bir senaryo kümesinde çalışır ve bunun yerine bir okuma veya paketin nasıl kullanılacağı nasıI rehberlik sağlamalıdır.

Varolan paketlerin çoğunun aşağıda açıklanan paket biçimini kullanması gerekmez.

Biçim, birinci sınıf bir senaryo olarak yerel içeriği etkinleştirirken. Bu, yönetilen derlemelerin, hedef platforma dayalı yönetilen derlemelerin yanında ikili uygulamaları sevk etmek için donanım uygulamalarına yakın bağlı olduğu anlamına gelir. Örneğin System.IO.Compression paketi bu teknolojiyi kullanmaktadır. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Özetle, yukarıdaki işlevsellik kesinlikle gerekli değilse, burada açıklanan biçim yalnızca NuGet 3.x+ tarafından desteklendirildiği için mevcut paket biçimine uymanızı öneririz.

Şimleme yoluyla hem de `packages.config` `project.json` senaryolar için çalışacak paketler oluşturmak mümkün olabilir, ancak yukarıda belirtilen amortismana uygun özellikler olmadan paketleri geleneksel şekilde yapılandırmak genellikle daha kolaydır.

## <a name="3x-package-format"></a>3.x paket formatı

3.x paket biçimi NuGet 2.x ötesinde birkaç ek özellik sağlar:

1. Derleme için kullanılan bir başvuru derlemesi ve farklı platformlarda/cihazlarda çalışma zamanı için kullanılan bir dizi uygulama derlemesi tanımlama. Bu da tüketicileriçin ortak bir yüzey alanı sağlarken platforma özgü API'lerden yararlanmanızı sağlar. Özellikle bu, ara taşınabilir kitaplıkların yazılmasını kolaylaştırır.

1. Paketlerin işletim sistemleri veya CPU mimarisi gibi platformlarda dönmesini sağlar.

1. Platforma özgü uygulamaların eş ekibe ayrılmasına olanak sağlar.

1. Birinci sınıf vatandaş olarak yerel bağımlılıkları destekleyin.
