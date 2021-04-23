---
title: NuGet.org üzerinde paket Benioku dosyası
description: NuGet.org üzerindeki benioku dosyalarının nasıl işlendiği ve sorunlarla çalışırken ne yapacaklarına ilişkin ayrıntılı açıklama.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902255"
---
# <a name="package-readme-on-nugetorg"></a>NuGet.org üzerinde paket Benioku dosyası

Paketinizin ayrıntılarını kullanıcılarınız için daha zengin ve bilgilendirici hale getirmek üzere [NuGet paketinize bir Benioku dosyası ekleyin](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) !

Bu, kullanıcıların paket ayrıntıları sayfasını NuGet.org üzerinde görüntülerken göreceği ilk öğeden biridir ve iyi bir izlenmenin yapılması için gereklidir!

> [!IMPORTANT]
> NuGet.org yalnızca [Markaşağı](https://daringfireball.net/projects/markdown/) içindeki Readme dosyalarını ve sınırlı bir etki alanı kümesindeki görüntüleri destekler. Benioku dosyanızın NuGet.org üzerinde doğru bir şekilde çalıştığından emin olmak için görüntüler ve [desteklenen Markaşağı özellikleri](#supported-markdown-features) [için izin verilen etki alanlarına](#allowed-domains-for-images-and-badges) bakın.

## <a name="what-should-my-readme-include"></a>Benioku dosyası neleri içersin?

Benioku 'nize aşağıdaki öğeleri dahil etmeyi göz önünde bulundurun:
* Paketinizin ne olduğuna ve ne yaptığını bir giriş, hangi sorunları çözüyor?
* Paketinize nasıl başladıysanız? belirli gereksinimler var mı?
* Benioku dosyasına dahil edilmediği daha kapsamlı belgelere bağlantı sağlar.
* En az birkaç kod parçacığı/örnek veya örnek görüntü.
* Proje sorunları, Twitter, hata İzleyicisi veya başka bir platforma bağlantı gibi geri bildirimin nerede ve nasıl kaydedileceği.
* Uygulanabiliyorsa, katkıda bulunun.

Göz önünde bulundurun, yüksek kaliteli okumalar çok çeşitli biçimlerde, şekillerde ve boyutlarda gelebilir! NuGet.org ' de kullanıma sunulan bir paketiniz zaten varsa, `readme.md` deponuzda NuGet.org details sayfanıza yönelik harika bir dosya olan bir veya başka bir belge dosyası zaten var.

## <a name="preview-your-readme"></a>Benioku dosyanızı önizleyin

Benioku dosyanızı NuGet.org üzerinde canlı olmadan önce önizlemek için, [NuGet.org ' deki paket Web portalını karşıya yükle](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) ' yi kullanarak paketinizi karşıya yükleyin ve meta veri önizlemesinin "Benioku dosyası" bölümüne gidin. Şuna benzer şekilde görünecektir:

![Benioku dosyası önizlemesi](media\readme-upload-preview.PNG)

Olası kullanıcılara harika bir ilk izlendiğinden emin olmak için, [görüntü uyumluluğu](#allowed-domains-for-images-and-badges) ve [desteklenen biçimlendirme](#supported-markdown-features) için Benioku dosyanızı gözden geçirmek ve önizlemek için zaman ayırarak kullanın! NuGet.org 'de yayımlandıktan sonra paketinizdeki hataları düzeltmek için, düzeltme ile güncelleştirilmiş bir paket sürümü göndermeniz gerekecektir. Her şeyin önceden iyi göründüğünden emin olmak, yolun ölçeğini artırarak tasarruf edebilirsiniz.
## <a name="allowed-domains-for-images-and-badges"></a>Görüntüler ve rozetler için izin verilen etki alanları

Güvenlik ve gizlilik sorunları nedeniyle, NuGet.org resimlerin ve rozetlerin güvenilir ana bilgisayarlara işlenebileceği etki alanlarını kısıtlar. 

NuGet.org, aşağıdaki güvenilen etki alanlarından, rozetler dahil tüm görüntülerin işlenmesine izin verir:
* api.bintray.com
* api.codacy.com
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
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

İzin verilenler listesine başka bir etki alanı eklenmesi gerektiğini düşünüyorsanız, lütfen [bir sorun](https://github.com/NuGet/NuGetGallery/issues) olup olmadığını ve gizlilik ve güvenlik uyumluluğu için mühendislik ekibimiz tarafından incelendiğini göreceksiniz. Göreli yerel yolları ve desteklenmeyen etki alanlarından barındırılan görüntüleri içeren görüntüler işlenmez ve yalnızca paket sahiplerine görünür olan Benioku dosyası Önizleme ve paket ayrıntıları sayfasında bir uyarı oluşturur.

## <a name="supported-markdown-features"></a>Desteklenen markın özellikleri
[Markaşağı](https://daringfireball.net/projects/markdown/) , düz metin biçimlendirme söz dizimine sahip hafif bir biçimlendirme dilidir. NuGet.org Benioku dosyaları, [markdig](https://github.com/lunet-io/markdig) ayrıştırma altyapısı aracılığıyla [commonmark](https://commonmark.org/) uyumlu markaşağı 'yi destekler.

NuGet.org Şu anda aşağıdaki Markaşağı özelliklerini desteklemektedir:
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

