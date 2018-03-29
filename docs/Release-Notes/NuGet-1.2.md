---
title: NuGet 1.2 sürüm notları | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 1.2 için sürüm notları.
keywords: Özellikler, dcr bilinen sorunlar, NuGet 1.2 sürüm notları, hata düzeltmeleri eklendi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0d95f41c5bc5d490764c9f128ee621e1037cef66
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2 sürüm notları

[NuGet 1.0 ve 1.1 sürüm notları](../release-notes/nuget-1.1.md) | [NuGet 1.3 sürüm notları](../release-notes/nuget-1.3.md)

NuGet 1.2, 30 Mart 2011'de serbest bırakıldı.

## <a name="new-features"></a>Yeni Özellikler

### <a name="framework-profile-support"></a>Framework profili desteği

Sahip NuGet en başından itibaren desteklenen kitaplıkları hedef farklı çerçeveleri. Ancak artık Windows Phone profili gibi belirli profillerini hedef derlemeleri paketleri içerebilir. Belirli bir profil çerçevenin hedef profil kısaltması tarafından izlenen bir tire ekleyin. Örneğin, bir Windows Phone (diğer adıyla Windows Phone 7) çalıştıran SilverLight hedeflemek için aşağıdaki ekran görüntüsünde gösterildiği gibi sl3 wp klasöründe bir derlemeyi koyabilirsiniz.

![Framework profil klasörü düzeni](./media/framework-profile-support.png)

Neden biz yalnızca bilinen ad "wp7" kullanılacak seçmediyseniz isteyebilir. Parçası olarak, biz bekleme Windows Phone 7 Silverlight daha yeni bir sürümü gelecekte çalışabilir, olduğunuz atamak; bu durumda hangi framework profil hakkında daha fazla belirli olması gerekebilir.

### <a name="automatically-add-binding-redirects"></a>Otomatik olarak bağlama yeniden yönlendirmeleri ekleyin

Tanımlayıcı adlı derlemeler ile bir paket yüklerken, NuGet şimdi burada bağlama sırada Projeyi derlemek ve otomatik olarak eklemek için yapılandırma dosyasına eklenecek yönlendirmeleri proje gerektirdiği durumlar algılayabilir. Bölüm 3 David Ebbo'nın blog gönderisine dizisinin NuGet başlıklı sürüm üzerinde "[Birleştirici bağlama yeniden yönlendirmelerini aracılığıyla](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" Bu özelliğin amacı, daha ayrıntılı ele alınmaktadır.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Framework'te derleme başvurularını (GAC) belirtme

Bazı durumlarda, bir paket, .NET Framework derleme bağlı. Kesinlikle olarak bakıldığında, her zaman paketinizi tüketici framework derleme başvurusu ise gerekli değildir. Ancak bazı durumlarda, geliştirici paketinizi kullanmak için bu derlemesindeki türler karşı kod gerektiği zaman gibi önemlidir. Yeni `frameworkAssemblies` öğesi, meta veri öğesinin alt öğesi bir dizi belirtmenize olanak verir `frameworkAssembly` Framework derlemesi GAC içinde işaret öğeleri. Framework'te derleme indirimlere unutmayın.
Bunlar .NET Framework'ün bir parçası olarak her makinede olduğu varsayılır gibi bu derlemeler paketinize dahil edilmez. Aşağıdaki tabloda özniteliklerini listeler `frameworkAssembly` öğesi.


|Öznitelik |Açıklama|
|----------------|-----------|
|**assemblyName**|*Gerekli*. Gibi derlemenin adını `System.Net`.|
|**targetFramework**|*İsteğe bağlı*. Framework ve profil adı (veya diğer) belirtebilirsiniz, "net40" veya "sl4" gibi bu framework derleme uygulanır. Açıklanan aynı biçimi kullanır [destekleyen birden çok hedef çerçeveyi](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe, API anahtarı kimlik bilgilerini depolamak bulabildiği

Nuget.exe komut satırı aracını kullanırken, API anahtarınıza depolamak için şimdi SetApiKey komutunu kullanabilirsiniz. Bu şekilde, bir paket itme her zaman belirtmek gerekmez. API anahtarınıza nuget.exe ile kaydetme hakkında daha fazla ayrıntı için [yayımlama bir paketi üzerinde belgeleri okuyun](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Paket Gezgini
Paket Explorer NuGet 1.2 desteklemek için güncelleştirildi. Daha fazla bilgi için kullanıma [paket Explorer sürüm notları](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Diğer özellikler/düzeltmeleri

Önceki listede en dikkat çeken birçok biz Uygulanmayan Özellikler ve biz düzeltilen yoktu. Tüm içinde tüm biz uygulanan/sabit [59 iş öğelerini](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) bu sürümde.

## <a name="known-issues"></a>Bilinen Sorunlar

* **1.2 paketini uyumsuzluk**: paketler komut satırı aracı en son sürümü ile oluşturulmuş, daha eski sürümleriyle NuGet VS eklentisini (örneğin, 1.1) nuget.exe (> 1.2) çalışmaz. Uyumsuz şeması hakkında bir şey bildiren bir hata iletisi alıyorsanız, bu hatayla çalışıyor. Lütfen NuGet en son sürüme güncelleştirin.
* **NuGet.Server uyumsuzluk**: NuGet.Server projesi kullanarak akış bir iç NuGet koyduysanız proje NuGet.Server en son sürümü ile güncelleştirmeniz gerekir.
* **İmza uyuşmazlığı hatası**: İmza uyuşmazlığı hakkında bir ileti ile yükseltme sırasında bir hatayla çalıştırırsanız, NuGet önce kaldırın ve ardından yüklemeniz gerekir. Bu listede bizim [bilinen sorunlar sayfa](../release-notes/known-issues.md) daha fazla ayrıntı sağlar. Sorun yalnızca Visual Studio 2010 SP1 çalıştıran etkiler ve NuGet yüklü 1.0 yanlış imzalı bir sürümüne sahip. Bu sorun, çok fazla kişi etkilemeyecek döndürmemelidir şekilde bu sürümü yalnızca kısa bir süre için CodePlex Web sitesinden kullanılabilir hale getirildi.