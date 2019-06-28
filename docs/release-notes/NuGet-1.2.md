---
title: NuGet 1.2 sürüm notları
description: NuGet 1.2 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426183"
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 sürüm notları

[NuGet 1.0 ve 1.1 sürüm notları](../release-notes/nuget-1.1.md) | [1.3 NuGet sürüm notları](../release-notes/nuget-1.3.md)

NuGet 1.2, 30 Mart 2011'de yayınlanmıştır.

## <a name="new-features"></a>Yeni Özellikler

### <a name="framework-profile-support"></a>Framework profili desteği

Sahip NuGet en başından itibaren desteklenen kitaplıkları hedef farklı çerçeveler. Ancak, Windows Phone profili gibi belirli profiller hedef derlemeler paketler artık içerebilir. Belirli bir profili bir framework'ün hedef profil kısaltması tarafından izlenen bir kısa çizgi ekleyin. Örneğin, Windows Phone (Windows Phone 7 olarak da bilinir) üzerinde çalışan SilverLight hedeflemek için aşağıdaki ekran görüntüsünde gösterildiği gibi sl3 wp klasöründe bir derleme koyabilirsiniz.

![Framework profil klasör düzeni](./media/framework-profile-support.png)

Neden biz yalnızca "wp7" bilinen adı olarak kullanılacak seçmediyseniz isteyebilir. Kısmen biz kapasitesinden Windows Phone 7 daha yeni bir Silverlight sürümü gelecekte çalışabilir, olduğunuz hedefleyen bu durumda hangi framework profil hakkında daha fazla belirli olması gerekebilir.

### <a name="automatically-add-binding-redirects"></a>Otomatik bağlama yeniden yönlendirmeleri ekleyin

Bir paket tanımlayıcı adlandırılmış derlemeler ile yüklerken, NuGet şimdi burada bağlama yönlendirmeleri, projeyi derleyin ve bunları otomatik olarak eklemek yapılandırma dosyası eklenecek proje ihtiyaç duyması algılayabilir. Bölüm 3 David Ebbo'nın blog gönderisi serisinin NuGet başlıklı sürüm üzerinde "[bağlama yeniden yönlendirmelerini aracılığıyla Birleştirici](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" Bu özelliğin amacı, daha ayrıntılı ele alınmaktadır.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Framework'te derleme başvuruları (GAC) belirtme

Bazı durumlarda, bir paket, .NET Framework derleme bağlı olabilir. NET olarak söylemek gerekirse, her zaman paketinizin tüketici framework derlemesine başvuru gerekli değildir. Ancak bazı durumlarda, geliştiriciye paketiniz kullanmak için bu bütünleştirilmiş kodundaki türler karşı kod gerektiğinde gibi önemli değildir. Yeni `frameworkAssemblies` öğesi, meta veri öğesi alt öğesi bir kümesini belirlemenizi sağlar `frameworkAssembly` Framework derlemenin GAC'deki işaret eden öğeler. Framework'te derleme indirimlere unutmayın.
Bu derlemeleri gibi bunlar her makinede .NET Framework'ün bir parçası olarak olduğu varsayılır paketinize dahil edilmez. Aşağıdaki tabloda öznitelikleri listeler `frameworkAssembly` öğesi.


|Öznitelik |Açıklama|
|----------------|-----------|
|**AssemblyName**|*Gerekli*. Gibi derlemenin adı `System.Net`.|
|**targetFramework**|*İsteğe bağlı*. Framework ve profili adı (veya diğer) belirtmeye izin verir "net40" veya "sl4" gibi bu framework derlemesine geçerli. Açıklanan aynı biçimi kullanır [birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe, API anahtarı kimlik bilgilerini saklamak amacıyla kuramıyor

Nuget.exe komut satırı aracını kullanarak, API anahtarınızı depolamak için artık SetApiKey komutunu kullanabilirsiniz. Bu şekilde, paket her itme yapışınızda bunu belirtmeniz gerekmez. API anahtarınızı nuget.exe ile kaydetme hakkında daha fazla ayrıntı için [bir paket yayımlama hakkında belgeleri okuyun](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Paket Gezgini
Paket Gezgini NuGet 1.2 desteklemek için güncelleştirildi. Daha fazla bilgi için kullanıma [paket Gezgini sürüm notları](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Diğer özellikler/düzeltmeleri

Önceki listede olan en dikkat çeken birçok özelliklerini uyguladık ve hataları düzelttik. Boyutunda uygulanan/düzelttik [59 iş öğelerini](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) bu sürümde.

## <a name="known-issues"></a>Bilinen Sorunlar

* **1.2 paketini uyumsuzluk**: Komut satırı aracının en son sürüm ile oluşturulan paketler, nuget.exe (> 1.2) NuGet VS eklentisini (örneğin, 1.1), önceki sürümlerle çalışmaz. Uyumsuz şeması hakkında bir şeyler belirten bir hata iletisi karşılaşırsanız, bu hatayla çalışıyor. Lütfen NuGet en son sürüme güncelleştirin.
* **NuGet.Server uyumsuzluk**: NuGet.Server Proje akışa bir iç NuGet düzenliyoruz. Bu projeyi NuGet.Server en son sürümüyle güncelleştirmek gerekir.
* **İmza türde bir eşleşmeme hatası**: Bir imza uyuşmazlığı hakkında bir ileti ile yükseltme sırasında bir hatayla çalıştırırsanız, NuGet önce kaldırın ve ardından yüklemeniz gerekir. Listede bu bizim [bilinen sorunlar sayfasında](../release-notes/known-issues.md) daha fazla ayrıntı sağlar. Sorunun yalnızca Visual Studio 2010 SP1 çalıştıran etkiler ve NuGet yüklü 1.0 yanlış imzalı bir sürümüne sahip. Bu sorun pek çok etkilenme şekilde bu sürümü yalnızca kısa bir süre için CodePlex Web sitesinden sunulmuştur.