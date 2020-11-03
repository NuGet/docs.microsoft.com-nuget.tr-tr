---
title: NuGet 1,2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,2 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237198"
---
# <a name="nuget-12-release-notes"></a>NuGet 1,2 sürüm notları

[NuGet 1,0 ve 1,1 sürüm notları](../release-notes/nuget-1.1.md)  |  [NuGet 1,3 sürüm notları](../release-notes/nuget-1.3.md)

NuGet 1,2, 30 Mart 2011 ' de yayımlanmıştır.

## <a name="new-features"></a>Yeni Özellikler

### <a name="framework-profile-support"></a>Çerçeve profili desteği

Başlangıçtan itibaren, desteklenen NuGet kütüphaneleri farklı çerçeveleri hedeflemelidir. Ancak artık paketler, Windows Phone profili gibi belirli profilleri hedefleyen derlemeler içerebilir. Bir çerçevenin belirli bir profilini hedeflemek için, ardından profil kısaltması gelen bir tire ekleyin. Örneğin, bir Windows Phone (diğer adıyla Windows Phone 7) çalışan SilverLight 'ı hedeflemek için, aşağıdaki ekran görüntüsünde gösterildiği gibi bir derlemeyi SL3-WP klasörüne yerleştirebilirsiniz.

![Çerçeve profili klasör düzeni](./media/framework-profile-support.png)

Bilinen ad olarak "wp7" kullanmayı görmediğimiz bir sorun. Bir parçası olarak, Windows Phone 7 ' nin ileride Silverlight 'ın daha yeni bir sürümünü çalıştırabileceğini benimsemeyi bekleme. Bu durumda, hangi çerçeve profilinin hangi çerçevede daha özel olması gerektiği konusunda daha fazla olması gerekebilir.

### <a name="automatically-add-binding-redirects"></a>Otomatik bağlama yeniden yönlendirmeleri Ekle

Güçlü adlandırılmış derlemelere sahip bir paket yüklerken, NuGet artık projenin derlenmesi ve otomatik olarak eklemesi için yapılandırma dosyasına bağlama yeniden yönlendirmeleri eklemesi gereken durumları algılayabilir. NuGet sürüm oluşturma sırasında "[bağlama yeniden yönlendirmeleri aracılığıyla birleştirme](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" başlıklı David Ebbo 'nın blog gönderisi serisinin 3. bölümü, bu özelliğin amacını daha ayrıntılı olarak ele almaktadır.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Çerçeve derleme başvurularını belirtme (GAC)

Bazı durumlarda, bir paket .NET Framework bir derlemeye bağlı olabilir. Kesinlikle konuşuyor, paketinizin tüketicisinin Framework derlemesine başvurması her zaman gerekli değildir. Ancak bazı durumlarda, örneğin, geliştiricinin paketinizi kullanabilmesi için bu derlemedeki türlere karşı kod kullanması gerektiğinde önemlidir. `frameworkAssemblies`Meta veri öğesinin bir alt öğesi olan yeni öğesi, `frameworkAssembly` GAC Içindeki bir Framework derlemesine işaret eden bir öğe kümesi belirtmenize olanak tanır. Çerçeve derlemesinde vurgu notuna göz önünde edin.
Bu derlemeler, .NET Framework bir parçası olarak her makinede olduğu varsayılarsa paketinize dahil edilmez. Aşağıdaki tablo, öğesinin özniteliklerini listelemektedir `frameworkAssembly` .


|Öznitelik |Açıklama|
|----------------|-----------|
|**assemblyName**|*Gerekli* . Bütünleştirilmiş kodun adı `System.Net` .|
|**targetFramework**|*Isteğe bağlı* . Bu çerçeve derlemesinin "net40" veya "SL4" gibi uyguladığı bir çerçeve ve profil adı (veya diğer ad) belirtilmesine izin verir. [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)bölümünde açıklanan biçimi kullanır.|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>nuget.exe artık API anahtarı kimlik bilgilerini depolayabiliyor

nuget.exe komut satırı aracını kullanırken, API anahtarınızı depolamak için artık SetApiKey komutunu kullanabilirsiniz. Bu şekilde, paketini her gönderişinizde belirtmeniz gerekmez. API anahtarınızı nuget.exe kaydetme hakkında daha fazla ayrıntı için, [paket yayımlama belgelerini okuyun](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Paket Gezgini
Paket Gezgini, NuGet 1,2 ' i destekleyecek şekilde güncelleştirilmiştir. Daha fazla bilgi için, [Paket Gezgini sürüm notlarına](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0)göz atın.

## <a name="other-featuresfixes"></a>Diğer özellikler/düzeltmeler

Önceki liste, uyguladığımız birçok özelliğin ve düzelttiğimiz hataların en belirgin bulgıydı. Tümü içinde, bu sürümde [59 iş öğesi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) uyguladık/düzeltildi.

## <a name="known-issues"></a>Bilinen Sorunlar

* **1,2 paket uyumsuzluğu** : komut satırı aracının en son sürümüyle oluşturulan paketler nuget.exe (> 1,2), NuGet vs eklentisinin eski sürümleriyle (1,1 gibi) çalışmaz. Uyumsuz şemayla ilgili bir şeyi belirten bir hata mesajınızı çalıştırırsanız, bu hatayla çalışıyorsunuz demektir. Lütfen NuGet 'i en son sürüme güncelleştirin.
* **NuGet. Server uyumsuzluğu** : NuGet. Server projesini kullanarak dahili bir NuGet akışı barındırıyorsanız, bu projeyi NuGet. Server ' ın en son sürümüyle güncelleştirmeniz gerekir.
* **Imza uyumsuzluğu hatası** : bir imza uyumsuzluğu hakkında bir iletiyle birlikte yükseltme sırasında hata halinde çalıştırırsanız, önce NuGet 'i kaldırmanız ve ardından yüklemeniz gerekir. Bu, daha fazla ayrıntı sağlayan [Bilinen Sorunlar sayfamızda](../release-notes/known-issues.md) listelenmiştir. Sorun yalnızca çalışan Visual Studio 2010 SP1 'i etkiler ve hatalı imzalı bir NuGet 1,0 sürümü yüklü. Bu sürüm kısa bir süre boyunca yalnızca CodePlex Web sitesinden kullanıma sunulmuştur. bu sorunun çok fazla kişiyi etkilememesi gerekir.