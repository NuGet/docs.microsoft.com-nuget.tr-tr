---
title: NuGet 2,8 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,8 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429054"
---
# <a name="nuget-28-release-notes"></a>NuGet 2,8 sürüm notları

NuGet [2.7.2 sürüm notları](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 sürüm notları](../release-notes/nuget-2.8.1.md)

NuGet 2,8, 29 Ocak 2014 tarihinde yayınlandı.

## <a name="acknowledgements"></a>Bildirimler

1. [Ltakaynakları Lyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) -paket paketleme, bağımlılık paketlerinin kimliği doğrulanıyor.
2. [Maaron Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -akış kimlik bilgilerini sürekli olarak $Metadata son eki kaldırın.
3. [Filıp de Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) -NuGet. exe Update komutu için proje dosyası belirtme desteği.
4. [Juan Gonzataz](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) değiştirme belirteçleri-ınclubir başvuru kimliği ile geçirilmedi.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -büyük paketi gönderirken NuGet. Push oluşturma OutOfMemoryException 'ı atma.
6. [Wouter Valeştirir](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -proje başka bir CLI/C++ projeye başvurduğunda yanlış hedef yolu düzeltir.
7. [Adam Canph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -paketlerin varsayılan olarak geliştirme bağımlılıkları olarak yüklenmesine izin ver
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -en son düzeltme eki sürümüne örtük yükseltmeleri kaldırın
9. [Gregvandenbkaback](https://www.codeplex.com/site/users/view/vdbg)
    - NuGet. Server, NuGet. exe yansıtma komutu ve diğerleri için çeşitli hata düzeltmeleri ve geliştirmeleri.
    - Bu iş, 2,8 için ana öğe ile tümleştirilmesine yönelik doğru zamanlamaya göre bizimle birlikte çalışarak, çok sayıda aya göre yapılmıştı.

## <a name="patch-resolution-for-dependencies"></a>Bağımlılıklar için düzeltme eki çözme

Paket bağımlılıkları çözümlenirken, NuGet, paketteki bağımlılıkları karşılayan en düşük ana ve ikincil paket sürümünü seçme stratejisini değiştirdi. Ancak, büyük ve küçük sürümden farklı olarak, düzeltme eki sürümü her zaman en yüksek sürüme çözümlenmelidir. Davranış iyi bir şekilde olsa da, bağımlılıkları olan paketleri yüklemek için bir belirleyici eksiklik oluşturmıştı. Aşağıdaki örnek göz önünde bulundurun:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Bu örnekte, Developer1 ve Developer2 PackageA@1.0.0yüklü olsa da, her biri PackageB 'nin farklı bir sürümüyle sona ermiştir. NuGet 2,8, düzeltme eki sürümleri için bağımlılık çözümleme davranışı büyük ve küçük sürümlerin davranışıyla tutarlı olacak şekilde bu varsayılan davranışı değiştirir. Yukarıdaki örnekte, daha yeni düzeltme eki sürümünden bağımsız olarak, PackageA@1.0.0yükleme sonucu olarak PackageB@1.0.0 yüklenir.

## <a name="-dependencyversion-switch"></a>-DependencyVersion anahtarı

NuGet 2,8, bağımlılıkları çözümlemek için _varsayılan_ davranışı değiştirse de, Paket Yöneticisi konsolundaki-dependencyversion anahtarı aracılığıyla bağımlılık çözümleme işlemi üzerinde daha kesin denetim de ekler. Anahtar olası en düşük sürüme (varsayılan davranış), mümkün olan en yüksek sürüme veya en yüksek alt veya düzeltme eki sürümüne bağımlılıkları çözmeyi sağlar.  Bu anahtar yalnızca PowerShell komutunda install-Package için geçerlidir.

![DependencyVersion anahtarı](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion özniteliği

Yukarıda açıklanan-DependencyVersion anahtarına ek olarak, NuGet. config dosyasında varsayılan değerin ne olduğunu tanımlayan NuGet. config dosyasında yeni bir öznitelik ayarlama yeteneği de vardır; örneğin,-DependencyVersion anahtarı bir çağrısında belirtilmemişse, Install-Package. Bu değer, herhangi bir paket yüklemesi işlemi için NuGet Paket Yöneticisi Iletişim kutusu tarafından da kullanılacaktır. Bu değeri ayarlamak için aşağıdaki özniteliği NuGet. config dosyanıza ekleyin:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>-WhatIf Ile NuGet Işlemlerini önizleyin

Bazı NuGet paketlerinde derin bağımlılık grafikleri bulunabilir ve bu nedenle, ne olacağını görmek için yükleme, kaldırma veya güncelleştirme işlemi sırasında yararlı olabilir. NuGet 2,8, standart PowerShell-whatIf anahtarını Install-Package, Uninstall-Package ve Update-Package komutlarına ekleyerek komutun uygulanacağı paketlerin tüm kapanışına görselleştirmeyi etkinleştirir. Örneğin, boş bir ASP.NET Web uygulamasında `install-package Microsoft.AspNet.WebApi -whatif` çalıştırmak aşağıdakileri verir.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Paketi düşürme

Yeni özellikleri araştırmak ve sonra son kararlı sürüme geri alma kararı vermek için bir paketin ön sürümü sürümünün yüklenmesi yaygın olmayan bir durumdur. NuGet 2,8 ' den önce bu, ön sürüm paketini ve bağımlılıklarını kaldırıp daha sonra önceki sürümü yüklerken çok adımlı bir işlemdir. Ancak NuGet 2,8 ile, güncelleştirme paketi artık tüm paket kapatılmasını (ör. paketin bağımlılık ağacı) önceki sürüme geri alacak.

## <a name="development-dependencies"></a>Geliştirme bağımlılıkları

Geliştirme sürecini iyileştirmek için kullanılan araçlar da dahil olmak üzere birçok farklı özellik türü NuGet paketleri olarak teslim edilebilir. Bu bileşenler, yeni bir paket geliştirilirken, daha sonra yayımlandığında yeni paketin bağımlılığı olarak düşünülmemelidir. NuGet 2,8, bir paketin `.nuspec` dosyasında kendisini bir developmentDependency olarak tanımlamasına olanak sağlar. Yüklendiğinde, bu meta veriler paketin yüklendiği projenin `packages.config` dosyasına da eklenecektir. Bu `packages.config` dosya daha sonra `nuget.exe pack`sırasında NuGet bağımlılıkları için çözümlendikten sonra, bu bağımlılıklar geliştirme bağımlılıkları olarak işaretlenmiş bağımlılıkları hariç bırakır.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Farklı platformlar için bağımsız paket. config dosyaları

Birden çok hedef platform için uygulama geliştirirken, ilgili Yapı ortamlarının her biri için farklı proje dosyaları olması yaygındır. Farklı proje dosyalarındaki farklı NuGet paketlerini kullanmak da yaygındır, çünkü paketler farklı platformlar için farklı destek düzeylerine sahiptir. NuGet 2,8, platforma özgü farklı proje dosyaları için farklı `packages.config` dosyaları oluşturarak bu senaryoya yönelik gelişmiş destek sağlar.

![Birden çok Package. config dosyası](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Yerel önbelleğe geri dön

NuGet paketleri genellikle bir ağ bağlantısı kullanan [NuGet Galerisi](http://www.nuget.org/) gibi uzak bir galeriden tüketilebilse de, istemcinin bağlı olmadığı birçok senaryo vardır. Ağ bağlantısı olmadan, NuGet istemcisi paketleri başarılı bir şekilde yükleyemedi-bu paketler, yerel NuGet önbelleğindeki istemci makinesinde zaten mevcut olduğunda bile. NuGet 2,8, Paket Yöneticisi konsoluna otomatik önbellek geri dönüşü ekler. Örneğin, ağ bağdaştırıcısının bağlantısını kesip jQuery yüklerken, konsol aşağıdakileri gösterir:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Önbellek geri dönüş özelliği belirli bir komut bağımsız değişkeni gerektirmez. Ayrıca, şu anda önbellek geri dönüşü yalnızca Paket Yöneticisi konsolunda çalışır; bu davranış Şu anda Paket Yöneticisi iletişim kutusunda çalışmıyor.

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet Istemci güncelleştirmeleri

NuGet 2,8 ile birlikte, WebMatrix için NuGet uzantısı da [nuget 2,5](../release-notes/nuget-2.5.md)ile sunulan birçok önemli özelliği içerecek şekilde güncelleştirildi. Yeni yetenekler arasında ' Tümünü Güncelleştir ', ' en düşük NuGet sürümü ' ve içerik dosyalarının üzerine yazılmasına izin verme gibi yenilikler bulunur.

WebMatrix 3 ' teki NuGet Paket Yöneticisi uzantınızı güncelleştirmek için:

1. WebMatrix 'i aç 3
1. Şeritteki uzantılar simgesine tıklayın
1. Güncelleştirmeler sekmesini seçin
1. NuGet paket yöneticisini 2.5.0 olarak güncelleştirmek için tıklayın
1. WebMatrix 'i kapat ve yeniden Başlat 3

Bu, NuGet ekibinin WebMatrix için NuGet Paket Yöneticisi uzantısının ilk sürümüdür.  Kod son zamanlarda Microsoft tarafından açık kaynaklı NuGet projesine katkıda bulundu. Daha önce, NuGet tümleştirmesi WebMatrix 'te oluşturulmuştur ve WebMatrix 'ten bant dışında güncellenemedi.  Artık NuGet 'in istemci araçlarının geri kalanı ile birlikte daha fazla güncelleştirme özelliği sunuyoruz.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

Güncelleştirme-paket-yeniden yükleme komutunda performans iyileştirmesinden oluşan önemli hata düzeltmelerinden biri.

Bu özelliklere ve belirtilen performans düzeltmesine ek olarak, NuGet 'in bu sürümü diğer birçok hata düzeltmesini de içerir. Yayında ele alınan toplam 181 sorun oluştu. NuGet 2,8 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu yayın Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)' ni görüntüleyin.
