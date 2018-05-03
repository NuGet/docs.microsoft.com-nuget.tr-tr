---
title: NuGet 2.8 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.8 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f472f1370bfedaf04ebe889c0da01155b8aec22
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 sürüm notları

[NuGet 2.7.2 sürüm notları](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 ile sürüm notları](../release-notes/nuget-2.8.1.md)

NuGet 2.8 29 Ocak 2014'te yayımlanmıştır.

## <a name="acknowledgements"></a>Katkıda Bulunanlar

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) - bağımlılık paket kimliğini doğrulama paketler, paket.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -kimlik bilgilerini persistening akış $metadata soneki kaldırılır.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - nuget.exe güncelleştirme komutu için proje dosyası belirtme desteği.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -değiştirme belirteçleri ile IncludeReferencedProjects - geçmedi.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -büyük paket Ftp'den zaman OutOfMemoryException atma nuget.push düzeltin.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -proje başka bir CLI/C++ projesi başvurduğunda düzeltme yanlış hedef yolu.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -varsayılan olarak geliştirme bağımlılıklar olarak yüklenecek paketleri izin ver
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -kaldırma en son düzeltme eki sürümü örtük yükseltme
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Birkaç düzeltmeler ve NuGet.Server, nuget.exe yansıtma komutu ve başkaları için hata.
    - Bu iş bizimle sağ zamanlama üzerinde çalıştığı Gregory 2.8 için ana şekilde entegre olan birkaç ay gerçekleştirilir.

## <a name="patch-resolution-for-dependencies"></a>Bağımlılıklar için düzeltme eki çözümleme

Paket bağımlılıklarını çözülürken NuGet tarihsel olarak, paket bağımlılıkları karşılayan düşük birincil ve ikincil Paket sürümü seçmek için bir strateji uyguladı. Birincil ve ikincil sürüm, ancak, düzeltme eki sürümü her zaman en yüksek sürüme çözümlendi. Davranış iyi niyetli olsa, bağımlılıkları olan paketleri yüklemek için determinism eksikliği oluşturulur. Aşağıdaki örnek göz önünde bulundurun:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Bu örnekte, Developer1 ve Developer2 rağmen yüklü PackageA@1.0.0, her sona erdi yukarı PackageB farklı bir sürümü ile. Düzeltme eki sürümleri için bağımlılık çözümleme davranışı birincil ve ikincil sürümleri için davranış ile tutarlı olacak şekilde, bu varsayılan davranışı NuGet 2.8 değiştirir. Yukarıdaki örnekte, daha sonra PackageB@1.0.0 yükleme sonucunda yükleneceğini PackageA@1.0.0ne olursa olsun, düzeltme eki sürümü.

## <a name="-dependencyversion-switch"></a>-DependencyVersion anahtarı

NuGet 2.8 değişir ancak _varsayılan_ davranışı bağımlılıkları çözümlemek için ayrıca - DependencyVersion anahtar aracılığıyla bağımlılık çözümleme işlemi üzerinde daha kesin bir denetim Paket Yöneticisi konsolunda ekler. Anahtarı, olası en düşük sürüm (varsayılan davranış), en yüksek olası sürümünü veya en yüksek ikincil ya da düzeltme eki sürüme çözümleme bağımlılıkları sağlar.  Bu anahtar yalnızca powershell komutu Install-package için çalışır.

![DependencyVersion anahtarı](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion özniteliği

-DependencyVersion anahtar çağrısından içinde belirtilmezse, yukarıda NuGet yeteneği izin yeni bir öznitelik Nuget.Config dosyasındaki ayarlamak için ayrıntılı - DependencyVersion anahtar yanı sıra varsayılan değer nedir, tanımlama Install-package. Bu değer ayrıca herhangi bir yükleme paketi işlem için NuGet Paket Yöneticisi iletişim kutusu tarafından uygulanır. Bu değeri ayarlamak için aşağıdaki öznitelik Nuget.Config dosyanıza ekleyin:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Önizleme NuGet - whatIf işlemleriyle

Bazı NuGet paketleri derin bağımlılık grafikleri olabilir ve bu nedenle, bir yükleme sırasında yararlı, kaldırma veya yükleyebilir ilk ne olacağını görmek için güncelleştirme işlemi. NuGet 2.8 Install-package, kaldırma paket ve paketleri komutu uygulanacak olan tüm kapatması görselleştirme etkinleştirmek için güncelleştirme paketi komutları standart PowerShell - whatif anahtar ekler. Örneğin, çalışan `install-package Microsoft.AspNet.WebApi -whatif` boş bir ASP.NET Web uygulama aşağıdaki verir.

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

## <a name="downgrade-package"></a>İndirgeme paketi

Bu yeni özellikler araştırmak için bir paket yayın öncesi bir sürümünü yükleyin ve ardından en son kararlı sürüme geri almak karar vermektir. Yayın öncesi paketi ve bağımlılıklarını kaldırmayı ve sonra önceki sürümü yükleme çok adımlı bir işlemi, bu NuGet 2.8 önce. NuGet 2.8 ile ancak, güncelleştirme paketini şimdi tüm paketi Kapatılmak üzere (örneğin paketin bağımlılığı ağacı) önceki sürümüne geri döner.

## <a name="development-dependencies"></a>Geliştirme bağımlılıkları

Farklı türlerde yetenekleri geliştirme sürecinin iyileştirmek için kullanılan araçları dahil olmak üzere NuGet paketleri - olarak alınabilir. Yeni bir paket geliştirmede enstrümental olabileceği daha sonra yayımlandığında bu bileşenlerin bir bağımlılık yeni paket düşünülmemelidir. NuGet 2.8 etkinleştirir kendisini tanımlamak bir paket `.nuspec` dosyası bir developmentDependency olarak. Yüklendiğinde, bu meta veriler ayrıca eklenir `packages.config` paketi yüklendi içine proje dosyası. Olduğunda, `packages.config` dosya sırasında NuGet bağımlılıklar için analiz daha sonra `nuget.exe pack`, geliştirme bağımlılıklar olarak işaretlenmiş bu bağımlılıkların dışında bırakır.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Farklı platformlar için tek tek packages.config dosyaları

Birden çok hedef platformlar için uygulama geliştirirken, her ilgili derleme ortamları için farklı proje dosyalarına sahip yaygındır. Paketleri farklı platformlar için destek değişen düzeylerde olduğundan ayrıca farklı proje dosyalarında farklı NuGet paketlerini kullanmak için yaygındır. NuGet 2.8 sağlayan geliştirilmiş destek bu senaryo için farklı oluşturarak `packages.config` farklı platforma özgü proje dosyaları için dosyaları.

![Birden çok package.config dosyaları](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Yerel önbelleğe almak için geri dönüş

NuGet paketleri genellikle uzak galerisinden gibi tüketilen olsa [NuGet galerisinde](http://www.nuget.org/) ağ bağlantısını kullanarak, burada istemci bağlı değil birçok senaryo vardır. Bir ağ bağlantısı NuGet istemci bile bu paketleri zaten istemcinin makinede yerel NuGet önbellekteki zamanki paketleri - başarıyla yüklemek mümkün değildi. NuGet 2.8 otomatik önbellek geri dönüş için Paket Yöneticisi konsolu ekler. Örneğin, ne zaman ağ bağdaştırıcısı kesme ve jQuery yükleme, konsol aşağıda gösterilmiştir:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Önbellek geri dönüş özelliğinin tüm belirli komut bağımsız değişkenleri gerektirmez. Ayrıca, geri dönüş önbelleği şu anda yalnızca Paket Yöneticisi konsolunda çalışır - davranışı Paket Yöneticisi iletişim kutusunda şu anda çalışmıyor.

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet istemcisi güncelleştirir

NuGet 2.8 yanı sıra, WebMatrix için NuGet uzantısı da ile teslim önemli özelliklerin çoğunu içerecek şekilde güncelleştirildi [NuGet 2.5](../release-notes/nuget-2.5.md). Yeni Özellikler 'Tümünü Güncelleştir', 'Minimum NuGet sürümü' ve içerik dosyaların üzerine yazılması için izin verme gibi içerir.

WebMatrix 3'te, NuGet Paket Yöneticisi uzantısı güncelleştirmek için:

1. WebMatrix 3 açın
1. Şerit'te uzantıları simgesine tıklayın
1. Güncelleştirmeler sekmesini seçin
1. NuGet Paket Yöneticisi için 2.5.0 güncelleştirmek için tıklatın
1. Kapatın ve WebMatrix 3 başlatın

WebMatrix NuGet Paket Yöneticisi uzantısı'nın sürüm ilk NuGet ekibin budur.  Kodu son Microsoft tarafından açık kaynak NuGet projeye katkıda bulunan. Daha önce NuGet tümleştirme Webmatrix'e yerleşik ve webmatrix'ten bant dışı güncelleştirilemedi.  Biz artık daha fazla NuGet istemci araçları rest yanı sıra güncelleştirme olanağınız vardır.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

Yapılan önemli hata düzeltmeleri birinde performans geliştirmesi güncelleştirme paketindeki-komutu yeniden yükleyin.

Bu özellikler ve daha önce bahsedilen performans düzeltme ek olarak, bu sürümü NuGet, diğer birçok hata düzeltmeleri de içerir. Sürümde ele 181 toplam sorunları vardı. İş tam listesi için öğeleri NuGet 2.8 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
