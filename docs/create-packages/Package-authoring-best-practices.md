---
title: Paket yazma en iyi uygulamaları
description: yüksek kaliteli NuGet paketleri oluşturmak için en iyi uygulamalar genel kılavuzu.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: ec1532900bed7d13ea2400afe9f855105a5c2fde
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209897"
---
# <a name="package-authoring-best-practices"></a>Paket yazma en iyi uygulamaları

bu kılavuz, NuGet paketi yazarlarına yüksek kaliteli paketler oluşturmak ve yayımlamak için hafif bir başvuru sağlamak üzere tasarlanmıştır. Birincil olarak meta veriler ve paketleme gibi pakete özgü en iyi yöntemlere odaklanacaktır. Yüksek kaliteli kitaplıklar oluşturmaya yönelik daha ayrıntılı öneriler için bkz. .NET [Açık Kaynak Kitaplığı Kılavuzu](/dotnet/standard/library-guidance/).

## <a name="types-of-recommendations"></a>Öneri türleri

Her makalede dört tür öneri sunulmaktadır: **Do**, **düþünün**, **önleyin** ve **Not**. Önerinin türü, ne kadar yakından izlenmeli olduğunu gösterir.

Neredeyse her zaman bir **Do** önerisi izlemeniz gerekir. Örnek:

✔️, paketinizin ne olduğunu açıklayan kısa bir açıklama içerir.

Diğer yandan, önerilerin genellikle izlenmesi gerektiğine **dikkat** edin, ancak kuralın meşru özel durumları vardır:

✔️ NuGet önek ayırma [ölçütlerine](../nuget-org/id-prefix-reservation.md)uyan bir ön ek içeren bir NuGet paket adı seçmeyi düşünün.

Genellikle iyi bir fikir olmayan ancak kuralın bölünmesi bazen anlamlı hale getirmeyen önerilerden **kaçının** :

❌tam bir sürümü talep eden NuGet paket başvurularına kaçının.

Son **olarak, önermeyin,** neredeyse asla yapmanız gereken bir şeyi gösterir:

❌`LicenseUrl`Meta veri özelliğini kullanmayın.

## <a name="create-a-nuget-package"></a>NuGet paketi oluşturma

NuGet paketi oluşturmak için en son önerilen yol [SDK stili bir projeden](../resources/check-project-format.md)yapılır. [Hedef Framework](/dotnet/standard/frameworks) ve [paket meta verileri](#package-metadata)dahil olmak üzere SDK stili proje özellikleri [Proje dosyasında](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file)tanımlanmıştır.

[Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) veya [dotnet clı](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)'de gerekli özellikleri ve paketleme tanımlayarak SDK stili projenizden bir paket oluşturun.

✔️ SDK stili bir proje oluşturun ve Visual Studio ya da dotnet clı kullanarak paketinizi (paket) oluşturun.

gerekli istemci araçları, proje dosyası örneği ve komutlar dahil paket oluşturmayla ilgili daha ayrıntılı kılavuz için bkz. [dotnet clı kullanarak NuGet paketi oluşturma](./creating-a-package-dotnet-cli.md).

Hangi .NET çerçevelerinin hedeflenecek olduğuna karar vermek için, [platformlar arası hedefleme için en son kılavuzumuza](/dotnet/standard/library-guidance/cross-platform-targeting)bakın.

## <a name="package-metadata"></a>Paket meta verileri

meta veriler, herhangi bir NuGet paketinin temel bir bileşenidir. Meta verilerinizin kalitesi, paketinizin bulunabilirliği, kullanılabilirliği ve güvenilirliğini etkileyebilir büyük ölçüde.

Visual Studio, paket meta verilerini belirtmenin önerilen yolu, Project > [Project Name] özellikleri > paketine gitmektir.

Paket meta verileri öğeleri [doğrudan proje dosyasında da belirtilebilir](./creating-a-package-msbuild.md#set-properties).

Aşağıda, kullanılabilir paket meta verileri öğelerinin bir tablo eşlemesi ve açıklaması verilmiştir:

| Visual Studio özellik adı                       | [Project dosya/MSBuild özellik adı](/dotnet/core/tools/csproj#packagereleasenotes)                              | [Nuspec Özellik adı](/nuget/reference/nuspec#general-form-and-schema)   | Açıklama                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`id`](/nuget/reference/nuspec#id)                                        | Paket adı veya tanımlayıcı.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](/nuget/reference/msbuild-targets#pack-target)                                                      | [`version`](/nuget/reference/nuspec#version)                              | NuGet paket sürümü.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](/nuget/reference/msbuild-targets#pack-target)                                                                 | [`authors`](/nuget/reference/nuspec#authors)                              | Genellikle bireyin veya kuruluşun "asıl adı" olarak kullanılan, paket yazarları için virgülle ayrılmış bir liste.           |
| [`Description`](#description)                     | [`Description`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`description`](/nuget/reference/nuspec#description)                      | Paketin açıklaması.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](/nuget/reference/msbuild-targets#pack-target)                                                               | [`copyright`](/nuget/reference/nuspec#copyright)                          | Paket için telif hakkı ayrıntıları.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)     | [`license type="expression"`](/nuget/reference/nuspec#license)            | Bir SPDX lisans ifadesi.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)           | [`license type="file"`](/nuget/reference/nuspec#license)                  | Özel bir lisans dosyasının yolu.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](/nuget/reference/nuspec#projecturl)                        | Proje giriş sayfası için bir URL.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                      | [`icon`](/nuget/reference/nuspec#icon)                                    | Paket simgesi resim dosyasının yolu.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](/nuget/reference/msbuild-targets#pack-target)                                                       | [`repository url`](/nuget/reference/nuspec#repository)                    | Paketin oluşturulduğu deponun URL 'SI.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](/nuget/reference/msbuild-targets#pack-target)                                                     | [`repository type`](/nuget/reference/nuspec#repository)                   | Depo URL 'SI işaret eden deponun türü ("git").                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](/nuget/reference/msbuild-targets#pack-target)                                                         | [`tags`](/nuget/reference/nuspec#tags)                                    | Paketi tanımlayan etiketlerin ve anahtar sözcüklerin boşlukla ayrılmış bir listesi. Etiketler, paketler aranırken kullanılır.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](/nuget/reference/msbuild-targets#pack-target)                                         | [`releaseNotes`](/nuget/reference/nuspec#releasenotes)                    | Paketin bu sürümünde yapılan değişikliklerin açıklaması.                                                     |
### <a name="package-id"></a>Paket Kimliği

Tamamen yeni bir paket yayımlıyorsanız:

✔️, NuGet. org 'daki mevcut paketlerden benzersiz ve açıkça ayırt edilen bir paket kimliği seçin.
> NuGet. org üzerinde kimliği arayarak veya aşağıdaki bağlantının mevcut olup olmadığını kontrol ederek bir paket kimliğinin benzersiz olup olmadığını kontrol edebilirsiniz: https://www.nuget.org/packages/<package adı \> .

✔️ NuGet [önek ayırma ölçütlerine](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)uyan bir ön ek içeren bir NuGet paket adı seçmeyi düşünün.
> Paketinizin önek kimliğini ayırma, doğrulanan onay işaretine sahip olur: ![ görüntü](media/Verified-check-mark.png)
> 
> Daha fazla bilgi edinmek için [paket kimliği ön ek rezervasyon belgelerine](../nuget-org/id-prefix-reservation.md) göz atın.

### <a name="package-version"></a>Paket Sürümü

✔️ NuGet paketinizin sürümü için [semver](https://semver.org/) kullanmayı düşünün.
> Temelde, bu, ana. Minor. Patch [-ön sürümü] biçiminin kullanıldığı anlamına gelir.

✔️, kararlı olmayan veya önizleme durumunda bir paketi [yayın öncesi paket](./prerelease-packages.md) olarak yayımlamaktır.

Daha gelişmiş yönergeler için bkz. [.NET kitaplığı sürüm oluşturma kılavuzu](/dotnet/standard/library-guidance/versioning) .

### <a name="authors"></a>Yazarlar

✔️ veya kuruluşunuzun "asıl adı" için yazar alanını kullanın.
> örneğin, my NuGet. org kullanıcı adı "jtikan" ise, yazar alanı için "gamze etikan" kullanımı, tüketicilerin bir yazar olarak beni tanımasına yardımcı olabilir. kuruluşumun NuGet. kuruluş kullanıcı adı "contosotoolkit" ise "Contoso Corporation" kullanımı daha tanınabilir ve daha fazla tüketici güveni kullanıyor olabilir.
### <a name="description"></a>Açıklama

✔️, paketinizi anlatmak için kısa bir açıklama (en fazla 4000 karakter) içerir.
> paket açıklamaları NuGet aramada ortaya çıkacak en belirgin alanlardan biridir ve büyük olasılıkla müşterilerin bir paketin kendileri için uygun olup olmadığını belirlemede karşılaştığı ilk şey olacaktır.

### <a name="copyright"></a>Telif Hakkı

✔️ paketinizin "telif hakkı (c) <adı/şirket <Year" ile birlikte copyrighting göz önünde bulundurun \> \> .
>Bir telif hakkı bildirimi temelde, çalışmanızın izniniz olmadan kopyalanamayacağını gösterir. Paketinize bir telif hakkı bildirimi de dahil olmak kolaydır ve hiçbir zarar vermez!

Örnek: telif hakkı (c) contoso 2020

### <a name="licensing"></a>Lisanslama

✔️ [paketinize bir lisans ifadesi veya lisans dosyası dahil](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Lisansı olmayan bir proje, özel bir [telif hakkı](https://choosealicense.com/no-permission/)için varsayılan olarak, projenizi kullanma izni vermediniz anlamına gelir.

❌ Kullanım dışı `LicenseUrl` meta veri özelliğini kullanmayın.
> Bu, URL 'deki lisans değişiklikleri, önceki paket sürümleri için görüntülenmiş lisansı geriye dönük olarak değiştirecek şekilde yasal belirsizliğe neden olur.

#### <a name="if-your-package-is-open-source"></a>Paketiniz [açık kaynak](https://opensource.org/osd) ise

✔️ paketinizin açık kaynak olması için [Açık kaynaklı bir lisans seçin](https://choosealicense.com/) .
> *"Açık kaynak lisanslar, açık kaynak tanımıyla uyumlu olan lisanslardır — kısaca, yazılımın serbestçe kullanılmasına, değiştirilmesine ve paylaşılmalarına izin verir."* -Açık kaynak girişimi. Açık kaynak yazılım ve açık kaynak girişimi hakkında daha fazla bilgi edinmek için kullanıma alın https://opensource.org/ .

✔️ [, paketinize bir lisans ifadesi dahil](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)etmeyi göz önünde bulundurun.
> Lisans ifadeleri en net bir şekilde ortaya çıkmış ve paketinizi kullandıklarında veya lisans değiştirildiyse tüketicilerle daha belirgin hale gelir. 
> [!Note]
> NuGet. org yalnızca açık kaynak girişimi veya ücretsiz yazılım temeli tarafından onaylanan lisanslar için lisans ifadelerini kabul eder.

#### <a name="if-your-package-is-not-open-source"></a>Paketiniz açık kaynak değilse

✔️ [paketinize bir lisans dosyası dahil](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Standart olmayan lisanslar dahil olmak üzere herhangi bir lisans dosyası (.txt veya. MD) paketinize eklenebilir. 

### <a name="project-url"></a>Project 'DEKI

✔️ ilişkili bir proje, depo veya şirket web sitesinin bağlantısını da kullanmayı düşünün.
> Proje sitenizde, kullanıcıların paketiniz hakkında bilmeleri gereken her şey olmalıdır ve büyük olasılıkla kullanıcıların belgeleri arayacağı yerdir.

### <a name="icon"></a>Simge

✔️ görsel açıdan ayırt etmeye yardımcı olmak için [paketinize bir simge dahil](../reference/msbuild-targets.md#packing-an-icon-image-file) etmeyi göz önünde bulundurun. Bu, paket kalitesinin kullanımını iyileştirebilecek görece küçük bir ektir.
> Simgeler tek tek paketlere özgü olabilir veya bir marka logosu olabilir.

✔️, en iyi sonuçları görüntülemek için 128x128 olan ve saydam bir arka plana (PNG) sahip bir görüntü kullanır.
> NuGet görüntünüzü, üzerinde görüntülendiği istemciye otomatik olarak ölçeklendirecektir.

❌ Kullanım dışı `IconUrl` meta veri özelliğini kullanmayın.

### <a name="repository-type-and-url"></a>Depo türü ve URL

✔️ kaynak denetimi meta verilerini otomatik olarak NuGet paketinize ekleyecek ve kitaplığınızı hata ayıklamanın daha kolay hale getirmek için [kaynak bağlantısı](/dotnet/standard/library-guidance/sourcelink) kurmayı düşünün.
> Kaynak bağlantısı `Repository URL` `Repository Type` , paket meta verilerini otomatik olarak ekler. Ayrıca, paket sürümünüzle ilişkili belirli bir yürütmeyi ekler.

### <a name="tags"></a>Etiketler

✔️, keşfedilebilirlik iyileştirmek için paketinize ilişkin önemli koşullara sahip birkaç etiket dahil eder.
> etiketler NuGet. kuruluş 'un arama algoritmasındaki hesaba alınır ve özellikle paket kimliğinde olmayan ancak ilgili olan koşullar için yararlıdır.

Örneğin, konsola günlük dizelerine bir paket yayımladım, şunu dahil ediyorum: "Logging, günlük, konsol, dize, çıkış"

### <a name="release-notes"></a>Sürüm notları

✔️, hangi değişikliklerin yapıldığını açıklayan her güncelleştirme ile sürüm notlarını da dahil etmeyi göz önünde bulundurun.
> Sürüm notları için belirli bir biçim gerekli olmasa da şunları dahil etmenizi öneririz:
>
> 1. Yeni değişiklikler
> 2. Yeni özellikler
> 3. Hata düzeltmeleri
> 
> Deponuzda sürüm notlarını veya bir changelog 'u zaten izliyorsanız ilgili dosyanın bağlantısını da ekleyebilirsiniz.

## <a name="related-topics"></a>İlgili konular

- [Paket (dotnet CLI) oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Paket (Visual Studio) oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)
