---
title: NuGet paket yazarları üzerinde Project. JSON etkisi
description: NuGet 3. x içindeki Project. JSON uygulamasının uygulamanın desteklenmeyen özellikler, içerik ve paket biçimi gibi paket yazarlarıyla nasıl etkilendiğine ilişkin ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488192"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Paket oluştururken Project. json ' un etkileri

> [!Important]
> Bu içerik kullanımdan kaldırılmıştır. Projeler ya `packages.config` ya da packagereference biçimlerini kullanmalıdır.

NuGet `project.json` 3 + ' de kullanılan sistem, paket yazarlarını aşağıdaki bölümlerde açıklandığı gibi çeşitli yollarla etkiler.

## <a name="changes-affecting-existing-packages-usage"></a>Mevcut paketlerin kullanımını etkileyen değişiklikler

Geleneksel NuGet paketleri geçişli dünyaya taşınmayan bir özellik kümesini destekler.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Yükleme ve kaldırma betikleri yoksayıldı

[Bağımlılık çözümlemesi](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)bölümünde açıklanan geçişli geri yükleme modelinin "paket yükleme süresi" kavramı yoktur. Bir paket mevcut değil veya yok, ancak paket yüklendiğinde oluşan tutarlı bir işlem yok.

Ayrıca, yüklenen betikler yalnızca Visual Studio 'da desteklenmektedir. Diğer Ides 'ler, bu tür betikleri desteklemeyi denemek için Visual Studio genişletilebilirlik API 'sini sahte ve ortak düzenleyiciler ve komut satırı araçlarında hiçbir destek yoktu.

### <a name="content-transforms-are-not-supported"></a>İçerik dönüştürmeleri desteklenmez

Betikleri yüklemeye benzer şekilde, dönüşümler paket yüklemesi üzerinde çalışır ve genellikle ıdempotent değildir. Artık bir yük süresi olmadığından, XDT dönüşümü ve benzer özellikler desteklenmez ve bu tür bir paket geçişli bir senaryoda kullanılıyorsa yok sayılır.

### <a name="content"></a>İçerik

Geleneksel NuGet paketleri, kaynak kodu ve yapılandırma dosyaları gibi içerik dosyalarını aktarıyor. Genellikle iki senaryoda kullanılır:

1. Kullanıcının bunları daha sonra düzenleyebilmesi için ilk dosyalar projeye bırakılmış. Ortak örnek, varsayılan yapılandırma dosyalarıdır.

1. Projede yüklü olan derlemeler için companmı olarak kullanılan içerik dosyaları. Buradaki örnek, bir derleme tarafından kullanılan bir logo görüntüsü olacaktır.

İçerik desteği şu anda betiklerin ve dönüştürmelerdeki benzer nedenlerle devre dışıdır, ancak içerik için destek tasarlama sürecimiz vardır.

İçerik dosyaları yine de paketler içinde taşınırlar ve şu anda yok sayılır, ancak son kullanıcı bunları yine de doğru noktaya kopyalayabilir.

İçerik dosyalarını geri getirme tekliflerinden birini görebilir ve ilerleme durumunu takip edebilirsiniz: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Paket yazarları için etki

Yukarıdaki özellikleri kullanan paketlerin farklı bir mekanizma kullanması gerekir. Bunun için en yaygın faydalı mekanizma, tam olarak desteklenmeye devam eden MSBuild hedefleri/props olacaktır. Yapı sistemi, pakette diğer kuralları da çekmeyi seçebilir. Bu, MSBuild hedeflerinin yanı sıra Roslyn Çözümleyicileri de desteklenir. `packages.config` Ve`project.json` senaryolarına yönelik hedefleri ve Çözümleyicileri destekleyen paketler oluşturmak mümkündür.

Projeyi kolay bir şekilde değiştirmeye çalışan paketler, genellikle çok sınırlı bir dizi senaryoda çalışır ve bunun yerine paketin nasıl kullanılacağına ilişkin bir Benioku veya bir kılavuz sağlamalıdır.

Birçok mevcut paketin aşağıda açıklanan paket biçimini kullanması gerekmez.

Biçim, yerel içeriği ilk sınıf senaryosu olarak sunar. Bu, yönetilen derlemelerin, hedef platforma bağlı olarak yönetilen derlemelerle birlikte ikili uygulamalar göndermek için donanım uygulamalarına yakın dayanmasıdır. Örneğin, System. ıO. Compression paketi bu teknolojinin kullanılmasıyla sorumludur. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Özet ' te, yukarıdaki işlev kesinlikle gerekli değilse, burada açıklanan biçim yalnızca NuGet 3. x + tarafından desteklenene kadar, mevcut paket biçimiyle bir çıkartma önerilir.

Paketler, için dolgu oluşturuluyor aracılığıyla her iki `packages.config` `project.json` senaryo için de çalışacak şekilde oluşturulabilir; ancak, yukarıda bahsedilen kullanım dışı özellikler olmadan paketleri geleneksel olarak yapılandırmak genellikle daha kolay bir yöntemdir.

## <a name="3x-package-format"></a>3. x paket biçimi

3\. x paket biçimi, NuGet 2. x ' in ötesinde birkaç ek özellik sağlar:

1. Derleme için kullanılan bir başvuru bütünleştirilmiş kodu ve farklı platformlarda/cihazlarda çalışma zamanı için kullanılan bir uygulama derlemeleri kümesi tanımlama. Tüketicileriniz için ortak bir yüzey alanı sağlarken platforma özgü API 'lerden yararlanmanızı sağlar. Bu, özellikle de ara taşınabilir kitaplıkların yazılmasını kolaylaştırır.

1. Paketlerin platformlar (işletim sistemleri veya CPU mimarisi) üzerinde özetlemesini sağlar.

1. Platforma özgü uygulamaların eşlik eden paketlere ayrılmasını sağlar.

1. Birinci sınıf vatandaşlık olarak yerel bağımlılıkları destekler.
