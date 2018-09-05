---
title: NuGet 2.8 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.8 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547465"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 sürüm notları

[2.7.2 NuGet sürüm notları](../release-notes/nuget-2.7.2.md) | [2.8.1 NuGet sürüm notları](../release-notes/nuget-2.8.1.md)

NuGet 2.8 29 Ocak 2014'te yayımlanmıştır.

## <a name="acknowledgements"></a>Onayları

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) - bağımlılık paketlerini kimlik doğrulama paketlerini paketleme.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -persistening kimlik bilgileri akışı güncelleştirildiğinde $metadata soneki kaldırın.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - nuget.exe güncelleştirme komutu için proje dosyasını belirtme desteği.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -ile - IncludeReferencedProjects geçmedi değiştirme belirteçleri.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -büyük paket gönderirken OutOfMemoryException atma nuget.push düzeltin.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -CLI/C++ projesi başka bir projeye başvuruda bulunduğunda düzeltme yanlış hedef yolu.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -varsayılan olarak geliştirme bağımlılıkları olarak yüklenecek paketler izin ver
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -en son düzeltme eki sürümü örtük yükseltmeleri Kaldır
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Birkaç NuGet.Server nuget.exe yansıtma komutu ve diğerleri için geliştirmeler ve hata düzeltmeleri ile.
    - Bu iş, bizim için doğru zamanlama üzerinde çalışan Gregory 2.8 için ana tümleştirin ile birkaç ay içinde yapılmadı.

## <a name="patch-resolution-for-dependencies"></a>Bağımlılıklar için düzeltme eki çözümleme

Paket bağımlılıkları çözümleniyor, NuGet paket bağımlılıkları karşılayan en düşük büyük ve küçük bir paket sürümü seçmek için bir strateji geçmişte uygulamıştır. Birincil ve ikincil sürüm, ancak, düzeltme eki sürümü her zaman için en yüksek sürüm çözümlendi. Davranışı iyi niyetli olsa, bağımlılıkları olan paket yüklemek için gerekircilik eksikliği oluşturuldu. Aşağıdaki örnek göz önünde bulundurun:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

Bu örnekte, olsa bile Developer1 ve Developer2 yüklü PackageA@1.0.0, PackageB farklı bir sürümü ile yukarı her bitişi. NuGet 2.8 düzeltme eki sürümleri için bağımlılık çözümleme davranışı, birincil ve ikincil sürüme davranışını tutarlıdır gibi bu varsayılan davranışı değiştirir. Yukarıdaki örnekte, ardından PackageB@1.0.0 yükleme sonucunda yükleneceğini PackageA@1.0.0bakılmaksızın yeni bir düzeltme eki sürümü.

## <a name="-dependencyversion-switch"></a>-DependencyVersion anahtarı

NuGet 2.8 değiştirir ancak _varsayılan_ davranışı bağımlılıkları çözümlemek için de bağımlılık çözümleme işlemi aracılığıyla - DependencyVersion anahtar üzerinde daha kesin denetim Paket Yöneticisi Konsolu'nda ekler. Çözümleme bağımlılıkları olası en düşük sürüm (varsayılan davranış), en yüksek olası sürümü veya en yüksek ikincil veya düzeltme eki sürümü için anahtar sağlar.  Bu anahtar yalnızca powershell komutu Install-package çalışır.

![DependencyVersion anahtarı](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion özniteliği

-DependencyVersion anahtar çağrısından belirtilmezse, yukarıda NuGet ayrıca olanağı tanıdı yeni bir öznitelik Nuget.Config dosyasında ayarlanacak - DependencyVersion anahtarı yanı sıra varsayılan değer nedir, tanımlama Install-package. Bu değer, NuGet Paket Yöneticisi iletişim kutusu için herhangi bir yükleme paketi işlemi tarafından da kanalla. Bu değeri ayarlamak için Nuget.Config dosyanızda aşağıdaki özniteliği ekleyin:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Önizleme - whatif ile NuGet işlemleri

NuGet paketlerinden bazıları ayrıntılı bağımlılık grafikleri olabilir ve bu nedenle, bir yükleme sırasında yararlı, kaldırma veya yükleyebilir ilk ne olacağını görmek için güncelleştirme işlemi. NuGet 2.8 Install-package, kaldırma paketi ve tüm kapatma komutu uygulanacak paketlerin görselleştirme etkinleştirmek için güncelleştirme paketi komutları standart PowerShell - whatif anahtar ekler. Örneğin, çalışan `install-package Microsoft.AspNet.WebApi -whatif` boş bir ASP.NET Web uygulaması aşağıdaki verir.

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

## <a name="downgrade-package"></a>İndirgeme paket

Bu yeni özellikler araştırmak için bir paket yayım öncesi bir sürümü yükleyin ve ardından en son kararlı sürüme geri karar vermektir. NuGet 2.8 önce bu ön sürüm paketi ve bağımlılıklarını kaldırmak ve ardından önceki bir sürümünü yükleme çok adımlı bir işlemin değildi. NuGet 2.8 ile ancak, güncelleştirme paketini şimdi tüm paket kapatma (örneğin paket Bağımlılık ağacı) önceki sürümüne geri döner.

## <a name="development-dependencies"></a>Geliştirme bağımlılıkları

Farklı türlerde özellikleri geliştirme süreci iyileştirmek için kullanılan araçları dahil olmak üzere NuGet paketleri - olarak sunulabilir. Yeni bir paket geliştirirken ınstrumental olabilir, ancak daha sonra yayımlandığında bu bileşenlerin yeni paketi bir bağımlılık kabul edilmemelidir. NuGet 2.8 sağlayan, kendini tanıtmak bir paket `.nuspec` dosyası bir developmentDependency olarak. Yüklendiğinde, bu meta veriler ayrıca eklenecek `packages.config` dosya projenin içine paketi yüklendi. Olduğunda, `packages.config` dosya için NuGet bağımlılıklarını sırasında analiz daha sonra `nuget.exe pack`, geliştirme bağımlılıkları olarak işaretlenmiş olan bu bağımlılıkların dışında bırakır.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Farklı platformlar için tek tek packages.config dosyaları

Birden çok hedef platformlar için uygulama geliştirirken, farklı proje dosyalarının her biri kendi yapı ortamları için çok yaygındır. Paketleri farklı platformları için destek farklı düzeylerde olduğundan da farklı proje dosyalarındaki farklı NuGet paketlerini kullanmak için yaygındır. NuGet 2.8 sağlayan geliştirilmiş destek bu senaryo için farklı oluşturarak `packages.config` farklı platforma özgü proje dosyaları için dosyaları.

![Birden çok package.config dosyaları](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Geri dönüş için yerel önbellek

NuGet paketleri genellikle uzak bir Galeriden gibi kullanılır ancak [NuGet galerisinde](http://www.nuget.org/) ağ bağlantısını kullanarak, burada istemci bağlı değil birçok senaryo vardır. Bir ağ bağlantısı olmadan NuGet istemci bile bu paketleri zaten istemcinin makinede yerel NuGet önbelleğini olduğu durumlarda paketler - başarılı bir şekilde yükleyebilmesi için o değildi. 2.8 NuGet Paket Yöneticisi konsolu için geri dönüş otomatik önbellek ekler. Örneğin, ne zaman ağ bağdaştırıcısının bağlantısının kesilmesini ve jQuery yükleme, konsol aşağıda gösterilmiştir:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Önbellek temel özellik, herhangi belirli komut satırı bağımsız değişkenlerini gerektirmez. Ayrıca, geri dönüş önbelleği şu anda yalnızca Paket Yöneticisi Konsolu'nda çalışır - davranışı Paket Yöneticisi iletişim kutusunda şu anda çalışmıyor.

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet istemcisi güncelleştirmelerini

NuGet 2.8 yanı sıra, WebMatrix için NuGet uzantısı da ile sunulan büyük özelliklerin çoğunu içerecek şekilde güncelleştirildi [NuGet 2.5](../release-notes/nuget-2.5.md). 'Tümünü Güncelleştir', 'Minimum NuGet sürümü' ve içerik dosyaları üzerine yazmak için izin verme gibi yeni özellikler içerir.

WebMatrix 3'te, NuGet paket yöneticisini uzantısı güncelleştirmek için:

1. WebMatrix 3'ı açın
1. Şerit'te uzantılar simgesine tıklayın
1. Güncelleştirmeler sekmesini seçin.
1. NuGet Paket Yöneticisi için 2.5.0 güncelleştirmek için tıklayın
1. WebMatrix 3'ü yeniden başlatın ve kapatın

WebMatrix için NuGet takımın ilk sürüm NuGet paket yöneticisini uzantısı'nın budur.  Kod Microsoft tarafından açık kaynaklı NuGet projeye yakın zamanda katkıda. Daha önce NuGet tümleştirme Webmatrix'e oluşturulmuştur ve webmatrix'ten bant dışı güncelleştirilemedi.  NuGet istemci araçları geri kalanı yanı sıra güncelleştirmek daha fazla özelliği artık sahibiz.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

Yapılan önemli hata düzeltmeleri biriydi performans geliştirmesinden-package-komut yeniden yükleyin.

Bu özellikler ve yukarıda sözü edilen performans düzeltme ek olarak, bu sürümü NuGet, ayrıca diğer birçok hata düzeltmeleri içerir. Sürümünde giderilen 181 toplam sorunlar oluştu. Tam bir listesi için iş öğeleri NuGet 2.8 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
