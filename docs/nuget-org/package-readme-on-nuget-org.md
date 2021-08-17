---
title: NuGet. org üzerinde paket benioku dosyası
description: NuGet. org üzerindeki benioku dosyalarının nasıl işlendiği ve sorunlar içinde çalıştırdığınızda ne yapacaklarına ilişkin ayrıntılı açıklama.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: ac0e89c1f5ef9eb19c29646bcc76bcb0b460c5cd
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209949"
---
# <a name="package-readme-on-nugetorg"></a>NuGet. org üzerinde paket benioku dosyası

paketinizin ayrıntılarını kullanıcılarınız için daha zengin ve bilgilendirici hale getirmek üzere [NuGet paketinize bir benioku dosyası ekleyin](/nuget/reference/msbuild-targets#packagereadmefile) !

bu, kullanıcıların paket ayrıntıları sayfasını NuGet. org üzerinde ne zaman görebilecekleri ve iyi bir izlenim yapmak için gerekli olan ilk öğelerden biridir!

> [!IMPORTANT]
> NuGet. org yalnızca [markaşağı](https://daringfireball.net/projects/markdown/) içindeki readme dosyalarını ve sınırlı bir etki alanı kümesinden görüntüleri destekler. benioku dosyanızın NuGet. org üzerinde doğru şekilde çalıştığından emin olmak için görüntüler ve [desteklenen markaşağı özellikleri](#supported-markdown-features) [için izin verilen etki alanlarımıza](#allowed-domains-for-images-and-badges) bakın.

## <a name="what-should-my-readme-include"></a>Benioku dosyası neleri içersin?

Benioku 'nize aşağıdaki öğeleri dahil etmeyi göz önünde bulundurun:
* Paketinizin ne olduğuna ve ne yaptığını bir giriş, hangi sorunları çözüyor?
* Paketinize nasıl başladıysanız? belirli gereksinimler var mı?
* Benioku dosyasına dahil edilmediği daha kapsamlı belgelere bağlantı sağlar.
* En az birkaç kod parçacığı/örnek veya örnek görüntü.
* Proje sorunları, Twitter, hata İzleyicisi veya başka bir platforma bağlantı gibi geri bildirimin nerede ve nasıl kaydedileceği.
* Uygulanabiliyorsa, katkıda bulunun.

Göz önünde bulundurun, yüksek kaliteli okumalar çok çeşitli biçimlerde, şekillerde ve boyutlarda gelebilir! NuGet. org üzerinde zaten kullanılabilir bir paketiniz varsa, `readme.md` deponuzda NuGet. org ayrıntı sayfanıza kadar çok alan bir veya başka bir belge dosyası zaten var.

## <a name="preview-your-readme"></a>Benioku dosyanızı önizleyin

benioku dosyanızı NuGet. org üzerinde canlı olmadan önce önizlemek için, [NuGet. org üzerinde Upload package web portalını](/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) kullanarak paketinizi yükleyin ve meta veri önizlemenin "benioku dosyası" bölümüne gidin. Şuna benzer şekilde görünecektir:

![Benioku dosyası önizlemesi](media\readme-upload-preview.PNG)

Olası kullanıcılara harika bir ilk izlendiğinden emin olmak için, [görüntü uyumluluğu](#allowed-domains-for-images-and-badges) ve [desteklenen biçimlendirme](#supported-markdown-features) için Benioku dosyanızı gözden geçirmek ve önizlemek için zaman ayırarak kullanın! paketinizdeki hataları düzeltmek için NuGet. org dosyasında yayımlandığında, düzeltme ile güncelleştirilmiş bir paket sürümü göndermeniz gerekir. Her şeyin önceden iyi göründüğünden emin olmak, yolun ölçeğini artırarak tasarruf edebilirsiniz.
## <a name="allowed-domains-for-images-and-badges"></a>Görüntüler ve rozetler için izin verilen etki alanları

güvenlik ve gizlilik endişeleri nedeniyle NuGet. org, resimlerin ve rozetlerin güvenilen konaklara işlenebileceği etki alanlarını kısıtlar. 

NuGet. org, aşağıdaki güvenilen etki alanlarından, rozetler dahil tüm görüntülerin işlenmesine izin verir:
* api.bintray.com
* api.codacy.com
* app.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* cdn.jsdelivr.net
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* i.imgur.com
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

İzin verilenler listesine başka bir etki alanı eklenmesi gerektiğini düşünüyorsanız, lütfen [bir sorun](https://github.com/NuGet/NuGetGallery/issues) olup olmadığını ve gizlilik ve güvenlik uyumluluğu için mühendislik ekibimiz tarafından incelendiğini göreceksiniz. Göreli yerel yolları ve desteklenmeyen etki alanlarından barındırılan görüntüleri içeren görüntüler işlenmez ve yalnızca paket sahiplerine görünür olan Benioku dosyası Önizleme ve paket ayrıntıları sayfasında bir uyarı oluşturur.

## <a name="supported-markdown-features"></a>Desteklenen markın özellikleri
[Markaşağı](https://daringfireball.net/projects/markdown/) , düz metin biçimlendirme söz dizimine sahip hafif bir biçimlendirme dilidir. NuGet. org benioku dosyaları, [markdig](https://github.com/lunet-io/markdig) ayrıştırma altyapısı aracılığıyla [commonmark](https://commonmark.org/) uyumlu markaşağı 'yi destekler.

NuGet. org şu anda aşağıdaki markın özelliklerini desteklemektedir:
* [Üst Bilgiler](https://spec.commonmark.org/0.29/#atx-headings)
* [Görüntüler](https://spec.commonmark.org/0.29/#images)
* [Ek vurgu](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listeler](https://spec.commonmark.org/0.29/#lists)
* [Bağlantılar](https://spec.commonmark.org/0.29/#links)
* [Teklifleri engelle](https://spec.commonmark.org/0.29/#block-quotes)
* [Ters eğik çizgi çıkışları](https://spec.commonmark.org/0.29/#backslash-escapes)
* [Kod yayılmaları](https://spec.commonmark.org/0.29/#code-spans)
* [Görev listeleri](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tablolar](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Bildirimlerde emoji](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Otomatik bağlantılar](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

