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
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="83689-103">NuGet.org üzerinde paket Benioku dosyası</span><span class="sxs-lookup"><span data-stu-id="83689-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="83689-104">Paketinizin ayrıntılarını kullanıcılarınız için daha zengin ve bilgilendirici hale getirmek üzere [NuGet paketinize bir Benioku dosyası ekleyin](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) !</span><span class="sxs-lookup"><span data-stu-id="83689-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="83689-105">Bu, kullanıcıların paket ayrıntıları sayfasını NuGet.org üzerinde görüntülerken göreceği ilk öğeden biridir ve iyi bir izlenmenin yapılması için gereklidir!</span><span class="sxs-lookup"><span data-stu-id="83689-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="83689-106">NuGet.org yalnızca [Markaşağı](https://daringfireball.net/projects/markdown/) içindeki Readme dosyalarını ve sınırlı bir etki alanı kümesindeki görüntüleri destekler.</span><span class="sxs-lookup"><span data-stu-id="83689-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="83689-107">Benioku dosyanızın NuGet.org üzerinde doğru bir şekilde çalıştığından emin olmak için görüntüler ve [desteklenen Markaşağı özellikleri](#supported-markdown-features) [için izin verilen etki alanlarına](#allowed-domains-for-images-and-badges) bakın.</span><span class="sxs-lookup"><span data-stu-id="83689-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="83689-108">Benioku dosyası neleri içersin?</span><span class="sxs-lookup"><span data-stu-id="83689-108">What should my readme include?</span></span>

<span data-ttu-id="83689-109">Benioku 'nize aşağıdaki öğeleri dahil etmeyi göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="83689-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="83689-110">Paketinizin ne olduğuna ve ne yaptığını bir giriş, hangi sorunları çözüyor?</span><span class="sxs-lookup"><span data-stu-id="83689-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="83689-111">Paketinize nasıl başladıysanız? belirli gereksinimler var mı?</span><span class="sxs-lookup"><span data-stu-id="83689-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="83689-112">Benioku dosyasına dahil edilmediği daha kapsamlı belgelere bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="83689-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="83689-113">En az birkaç kod parçacığı/örnek veya örnek görüntü.</span><span class="sxs-lookup"><span data-stu-id="83689-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="83689-114">Proje sorunları, Twitter, hata İzleyicisi veya başka bir platforma bağlantı gibi geri bildirimin nerede ve nasıl kaydedileceği.</span><span class="sxs-lookup"><span data-stu-id="83689-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="83689-115">Uygulanabiliyorsa, katkıda bulunun.</span><span class="sxs-lookup"><span data-stu-id="83689-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="83689-116">Göz önünde bulundurun, yüksek kaliteli okumalar çok çeşitli biçimlerde, şekillerde ve boyutlarda gelebilir!</span><span class="sxs-lookup"><span data-stu-id="83689-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="83689-117">NuGet.org ' de kullanıma sunulan bir paketiniz zaten varsa, `readme.md` deponuzda NuGet.org details sayfanıza yönelik harika bir dosya olan bir veya başka bir belge dosyası zaten var.</span><span class="sxs-lookup"><span data-stu-id="83689-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="83689-118">Benioku dosyanızı önizleyin</span><span class="sxs-lookup"><span data-stu-id="83689-118">Preview your readme</span></span>

<span data-ttu-id="83689-119">Benioku dosyanızı NuGet.org üzerinde canlı olmadan önce önizlemek için, [NuGet.org ' deki paket Web portalını karşıya yükle](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) ' yi kullanarak paketinizi karşıya yükleyin ve meta veri önizlemesinin "Benioku dosyası" bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="83689-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="83689-120">Şuna benzer şekilde görünecektir:</span><span class="sxs-lookup"><span data-stu-id="83689-120">It should look something like this:</span></span>

![Benioku dosyası önizlemesi](media\readme-upload-preview.PNG)

<span data-ttu-id="83689-122">Olası kullanıcılara harika bir ilk izlendiğinden emin olmak için, [görüntü uyumluluğu](#allowed-domains-for-images-and-badges) ve [desteklenen biçimlendirme](#supported-markdown-features) için Benioku dosyanızı gözden geçirmek ve önizlemek için zaman ayırarak kullanın!</span><span class="sxs-lookup"><span data-stu-id="83689-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="83689-123">NuGet.org 'de yayımlandıktan sonra paketinizdeki hataları düzeltmek için, düzeltme ile güncelleştirilmiş bir paket sürümü göndermeniz gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="83689-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="83689-124">Her şeyin önceden iyi göründüğünden emin olmak, yolun ölçeğini artırarak tasarruf edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83689-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="83689-125">Görüntüler ve rozetler için izin verilen etki alanları</span><span class="sxs-lookup"><span data-stu-id="83689-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="83689-126">Güvenlik ve gizlilik sorunları nedeniyle, NuGet.org resimlerin ve rozetlerin güvenilir ana bilgisayarlara işlenebileceği etki alanlarını kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="83689-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="83689-127">NuGet.org, aşağıdaki güvenilen etki alanlarından, rozetler dahil tüm görüntülerin işlenmesine izin verir:</span><span class="sxs-lookup"><span data-stu-id="83689-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="83689-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="83689-128">api.bintray.com</span></span>
* <span data-ttu-id="83689-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="83689-129">api.codacy.com</span></span>
* <span data-ttu-id="83689-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="83689-130">api.codeclimate.com</span></span>
* <span data-ttu-id="83689-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="83689-131">api.dependabot.com</span></span>
* <span data-ttu-id="83689-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="83689-132">api.travis-ci.com</span></span>
* <span data-ttu-id="83689-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="83689-133">api.travis-ci.org</span></span>
* <span data-ttu-id="83689-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="83689-134">app.fossa.io</span></span>
* <span data-ttu-id="83689-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="83689-135">badge.fury.io</span></span>
* <span data-ttu-id="83689-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="83689-136">badgen.net</span></span>
* <span data-ttu-id="83689-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="83689-137">badges.gitter.im</span></span>
* <span data-ttu-id="83689-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="83689-138">bettercodehub.com</span></span>
* <span data-ttu-id="83689-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="83689-139">buildstats.info</span></span>
* <span data-ttu-id="83689-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="83689-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="83689-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="83689-141">ci.appveyor.com</span></span>
* <span data-ttu-id="83689-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="83689-142">circleci.com</span></span>
* <span data-ttu-id="83689-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="83689-143">codecov.io</span></span>
* <span data-ttu-id="83689-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="83689-144">codefactor.io</span></span>
* <span data-ttu-id="83689-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="83689-145">coveralls.io</span></span>
* <span data-ttu-id="83689-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="83689-146">dev.azure.com</span></span>
* <span data-ttu-id="83689-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="83689-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="83689-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="83689-148">gitlab.com</span></span>
* <span data-ttu-id="83689-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="83689-149">img.shields.io</span></span>
* <span data-ttu-id="83689-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="83689-150">isitmaintained.com</span></span>
* <span data-ttu-id="83689-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="83689-151">opencollective.com</span></span>
* <span data-ttu-id="83689-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="83689-152">raw.github.com</span></span>
* <span data-ttu-id="83689-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="83689-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="83689-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="83689-154">snyk.io</span></span>
* <span data-ttu-id="83689-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="83689-155">sonarcloud.io</span></span>
* <span data-ttu-id="83689-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="83689-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="83689-157">İzin verilenler listesine başka bir etki alanı eklenmesi gerektiğini düşünüyorsanız, lütfen [bir sorun](https://github.com/NuGet/NuGetGallery/issues) olup olmadığını ve gizlilik ve güvenlik uyumluluğu için mühendislik ekibimiz tarafından incelendiğini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="83689-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="83689-158">Göreli yerel yolları ve desteklenmeyen etki alanlarından barındırılan görüntüleri içeren görüntüler işlenmez ve yalnızca paket sahiplerine görünür olan Benioku dosyası Önizleme ve paket ayrıntıları sayfasında bir uyarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="83689-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="83689-159">Desteklenen markın özellikleri</span><span class="sxs-lookup"><span data-stu-id="83689-159">Supported Markdown features</span></span>
<span data-ttu-id="83689-160">[Markaşağı](https://daringfireball.net/projects/markdown/) , düz metin biçimlendirme söz dizimine sahip hafif bir biçimlendirme dilidir.</span><span class="sxs-lookup"><span data-stu-id="83689-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="83689-161">NuGet.org Benioku dosyaları, [markdig](https://github.com/lunet-io/markdig) ayrıştırma altyapısı aracılığıyla [commonmark](https://commonmark.org/) uyumlu markaşağı 'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="83689-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="83689-162">NuGet.org Şu anda aşağıdaki Markaşağı özelliklerini desteklemektedir:</span><span class="sxs-lookup"><span data-stu-id="83689-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="83689-163">Üst Bilgiler</span><span class="sxs-lookup"><span data-stu-id="83689-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="83689-164">Görüntüler</span><span class="sxs-lookup"><span data-stu-id="83689-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="83689-165">Ek vurgu</span><span class="sxs-lookup"><span data-stu-id="83689-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="83689-166">Listeler</span><span class="sxs-lookup"><span data-stu-id="83689-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="83689-167">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="83689-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="83689-168">Teklifleri engelle</span><span class="sxs-lookup"><span data-stu-id="83689-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="83689-169">Ters eğik çizgi çıkışları</span><span class="sxs-lookup"><span data-stu-id="83689-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="83689-170">Kod yayılmaları</span><span class="sxs-lookup"><span data-stu-id="83689-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="83689-171">Görev listeleri</span><span class="sxs-lookup"><span data-stu-id="83689-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="83689-172">Tablolar</span><span class="sxs-lookup"><span data-stu-id="83689-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="83689-173">Bildirimlerde emoji</span><span class="sxs-lookup"><span data-stu-id="83689-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="83689-174">Otomatik bağlantılar</span><span class="sxs-lookup"><span data-stu-id="83689-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

