---
title: NuGet Paket Bağımlılık Çözümü
description: NuGet paketinin bağımlılıklarının çözülüp hem NuGet 2.x hem de NuGet 3.x+'ta yüklendiği işlemle ilgili ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428830"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet paket bağımlılıklarını nasıl çözer?

Bir paket yüklendiğinde veya yeniden yüklendiğinde, bu da geri [yükleme](../consume-packages/package-restore.md) işleminin bir parçası olarak yüklenmesini de içerir, NuGet ayrıca ilk paketin bağlı olduğu ek paketleri de yükler.

Bu acil bağımlılıklar daha sonra da keyfi bir derinliğe devam edebilir kendi bağımlılıkları olabilir. Bu, tüm düzeylerdeki paketler arasındaki ilişkileri açıklayan bağımlılık *grafiği* olarak adlandırılan bir grafik üretir.

Birden çok paket aynı bağımlılığa sahipse, aynı paket kimliği grafikte birden çok kez görünebilir ve bu da farklı sürüm kısıtlamalarıyla olabilir. Ancak, belirli bir paketin yalnızca bir sürümü projede kullanılabilir, bu nedenle NuGet hangi sürümün kullanılacağını seçmelidir. Tam işlem, kullanılan paket yönetim biçimine bağlıdır.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference ile bağımlılık çözümü

Paket Başvurusu biçimini kullanarak projelere paketleri yüklerken, NuGet uygun dosyadaki düz paket grafiğine referanslar ekler ve çakışmaları önceden giderir. Bu işlem *geçişli geri yükleme*olarak adlandırılır. Paketleri yeniden yüklemek veya geri yüklemek, grafikte listelenen paketleri indirme işlemidir ve bu da daha hızlı ve daha öngörülebilir yapılara neden olur. Ayrıca, 2,8 gibi kayan sürümlerden de yararlanabilirsiniz. \*, bir paketin en son sürümünü kullanmak için projeyi değiştirmemek için.

NuGet geri yükleme işlemi bir yapıdan önce çalıştığında, önce bellekteki bağımlılıkları giderir, `project.assets.json`sonra ortaya çıkan grafiği adlı bir dosyaya yazar. Ayrıca, kilit dosyası `packages.lock.json` [işlevselliği etkinse,](../consume-packages/package-references-in-project-files.md#locking-dependencies)çözülmüş bağımlılıkları adlı bir kilit dosyasına da yazar.
Varlıklar dosyası, projenin `MSBuildProjectExtensionsPath`'obj' klasörüne varsayılan olarak bulunan bir dosyada bulunur. MSBuild daha sonra bu dosyayı okur ve olası başvuruların bulunabileceği bir klasör kümesine çevirir ve bunları bellekteki proje ağacına ekler.

Dosya `project.assets.json` geçicidir ve kaynak denetimine eklenmemelidir. Her ikisinde de `.gitignore` varsayılan `.tfignore`olarak listelenir. [Bkz. Paketler ve kaynak denetimi.](../consume-packages/packages-and-source-control.md)

### <a name="dependency-resolution-rules"></a>Bağımlılık çözümleme kuralları

Geçişli geri yükleme bağımlılıkları gidermek için dört ana kural uygular: en düşük geçerli sürüm, kayan sürümler, en yakın kazançlar ve kuzen bağımlılıkları.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>En düşük uygulanabilir sürüm

Uygulanabilir en düşük sürüm kuralı, bir paketin bağımlılıkları tarafından tanımlanan mümkün olan en düşük sürümünü geri yükler. Kayan olarak beyan edilmedikçe, uygulama veya sınıf [floating](#floating-versions)kitaplığı üzerindeki bağımlılıklar için de geçerlidir.

Aşağıdaki şekilde, örneğin, 1.0-beta 1.0'dan daha düşük kabul edilir, bu nedenle NuGet 1.0 sürümünü seçer:

![En düşük geçerli sürümü seçme](media/projectJson-dependency-1.png)

Bir sonraki şekilde, sürüm 2.1 akışta kullanılamaz, ancak sürüm kısıtlaması >= 2.1 NuGet bulacağı bir sonraki en düşük sürümü seçtiğinden, bu durumda 2.2:

![Akışta kullanılabilen bir sonraki en düşük sürümü seçme](media/projectJson-dependency-2.png)

Bir uygulama, akışta bulunmayan 1.2 gibi tam bir sürüm numarası belirttiğinde, NuGet paketi yüklemeye veya geri yüklemeye çalışırken bir hatayla başarısız olur:

![NuGet, tam paket sürümü kullanılamadığında bir hata oluşturur](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Kayan sürümler

\* Kayan bağımlılık sürümü karakterle birlikte belirtilir. Örneğin, `6.0.*`. Bu sürüm belirtimi "en son 6.0.x sürümünü kullanın" diyor; `4.*` "en son 4.x sürümünü kullanın" anlamına gelir. Kayan bir sürümü kullanmak, bir bağımlılığın en son sürümüyle güncel tutarken proje dosyasındaki değişiklikleri azaltır.

NuGet kayan bir sürümü kullanırken, sürüm deseniyle eşleşen bir paketin `6.0.*` en yüksek sürümünü çözer, örneğin 6.0 ile başlayan bir paketin en yüksek sürümünü alır:

![Kayan bir sürüm 6.0.* istendiğinde sürüm 6.0.1'i seçme](media/projectJson-dependency-4.png)

> [!Note]
> Kayan sürümlerin ve ön sürüm sürümlerinin davranışı hakkında bilgi [için](package-versioning.md#version-ranges)bkz.


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>En yakın galibiyetler

Bir uygulamanın paket grafiği aynı paketin farklı sürümlerini içeriyorsa, NuGet grafikteki uygulamaya en yakın paketi seçer ve diğer lerini yok sayar. Bu davranış, bir uygulamabağımlılık grafiğinde belirli bir paket sürümünü geçersiz kılmak için izin verir.

Aşağıdaki örnekte, uygulama doğrudan >=2.0 sürüm kısıtlaması ile B Paketine bağlıdır. Uygulama aynı zamanda A paketine de bağlıdır ve bu da B paketine bağlıdır, ancak >=1.0 kısıtlaması ile birlikte. B 2.0 Paketine bağımlılık grafikteki uygulamaya daha yakın olduğundan, bu sürüm kullanılır:

![En Yakın Kazançlar kuralını kullanarak uygulama](media/projectJson-dependency-5.png)

>[!Warning]
> En Yakın Kazançlar kuralı, paket sürümünün düşmesine neden olabilir ve böylece grafikteki diğer bağımlılıkları kırabilir. Bu nedenle bu kural kullanıcıyı uyarmak için bir uyarı ile uygulanır.

Bu kural aynı zamanda büyük bir bağımlılık grafiğiyle (BCL paketlerindekiler gibi) daha fazla verimlilik sağlar, çünkü belirli bir bağımlılık göz ardı edildikten sonra NuGet grafiğin o dalı üzerinde kalan tüm bağımlılıkları da göz ardı eder. Aşağıdaki diyagramda, örneğin, Paket C 2.0 kullanıldığından, NuGet grafikte C Paketinin eski bir sürümüne atıfta bulunan dalları yoksa:

![NuGet grafikteki bir paketi yok saydığında, tüm dalı yoksa](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Kuzen bağımlılıkları

Farklı paket sürümleri uygulamadan grafikte aynı mesafede atıfta bulunulduğunda, NuGet tüm sürüm gereksinimlerini karşılayan en düşük sürümü kullanır [(geçerli en düşük sürüm](#lowest-applicable-version) ve [kayan sürüm](#floating-versions) kurallarında olduğu gibi). Aşağıdaki resimde, örneğin, B Paketinin 2.0 sürümü diğer >=1.0 kısıtlamasını karşılar ve böylece kullanılır:

![Tüm kısıtlamaları karşılayan alt sürümü kullanarak kuzen bağımlılıklarını çözme](media/projectJson-dependency-7.png)

Bazı durumlarda, tüm sürüm gereksinimlerini karşılamak mümkün değildir. Aşağıda gösterildiği gibi, A Paketi tam olarak B 1.0 paketi gerektiriyorsa ve C Paketi B >=2.0 gerektiriyorsa, NuGet bağımlılıkları çözemez ve hata verir.

![Tam sürüm gereksinimi nedeniyle çözülemeyen bağımlılıklar](media/projectJson-dependency-8.png)

Bu gibi durumlarda, en [yakın kazançlar](#nearest-wins) kuralının geçerli olması için üst düzey tüketicinin (uygulama veya paket) B Paketine doğrudan bağımlılığını eklemesi gerekir.

## <a name="dependency-resolution-with-packagesconfig"></a>packages.config ile bağımlılık çözümü

Ile `packages.config`, bir projenin bağımlılıkları `packages.config` düz bir liste olarak yazılır. Bu paketlerin herhangi bir bağımlılıkları da aynı listede yazılır. Paketler yüklendiğinde, NuGet dosyayı `.csproj` `app.config` `web.config`ve diğer dosyaları da değiştirebilir.

Ile, `packages.config`NuGet her bir paketin yüklenmesi sırasında bağımlılık çakışmaları çözmek için çalışır. Diğer bir deyişle, A Paketi yüklüyse ve B Paketine bağlıysa `packages.config` ve B Paketi zaten başka bir şeyin bağımlılığı olarak listelenmişse, NuGet B Paketinin istenen sürümlerini karşılaştırır ve tüm sürüm kısıtlamalarını karşılayan bir sürüm bulmaya çalışır. Özellikle, NuGet bağımlılıkları tatmin eden alt *majör.küçük* sürümü seçer.

Varsayılan olarak, NuGet 2.8 en düşük yama sürümünü arar (Bkz. [NuGet 2.8 sürüm notları).](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) Bu ayarı, komut `DependencyVersion` satırındaki `Nuget.Config` öznitelik ve `-DependencyVersion` anahtar üzerinden denetleyebilirsiniz.  

Bağımlılıkları `packages.config` çözme işlemi, daha büyük bağımlılık grafikleri için karmaşık hale getirir. Her yeni paket yüklemesi tüm grafiğin bir geçiş gerektirir ve sürüm çakışmaları için şansı yükseltir. Bir çakışma oluştuğunda, yükleme durdurulur ve proje belirsiz bir durumda bırakılır, özellikle proje dosyasının kendisinde olası değişiklikler yapılır. Bu, diğer paket yönetim biçimlerini kullanırken bir sorun değildir.

## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

PackageReference biçimini kullanırken, bağımlılıklardan hangi varlıkların üst düzey projeye aktığını denetleyebilirsiniz. Ayrıntılar için [PackageReference'a](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)bakın.

Üst düzey projenin kendisi bir paket olduğunda, `include` `exclude` `.nuspec` dosyada listelenen bağımlılıkları olan ve öznitelikleri ni ve özniteliklerini kullanarak bu akış üzerinde denetime de sahip olursunuz. [Bkz..nuspec Başvuru - Bağımlılıklar](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Referansları hariç alma

Aynı ada sahip derlemelerin projede birden fazla kez başvurulabileceği ve tasarım zamanı ve yapı zamanı hataları üreten senaryolar vardır. Özel bir sürümünü `C.dll`içeren bir proje düşünün ve Aynı `C.dll`zamanda içeren Paket C'ye başvurur. Aynı zamanda proje aynı zamanda C paketine ve `C.dll`B Paketine de bağlıdır. Sonuç olarak, NuGet hangisini `C.dll` kullanacağınızı belirleyemez, ancak B Paketi de buna bağlı olduğundan projenin C Paketine olan bağımlılığını kaldıramaz.

Bunu çözmek için, doğrudan `C.dll` istediğiniz başvuru (veya doğru bir başvuru başka bir paket kullanın) ve sonra tüm varlıklarını hariç C Paketi bir bağımlılık eklemeniz gerekir. Bu, kullanımdaki paket yönetim biçimine bağlı olarak aşağıdaki gibi yapılır:

- [PackageReference](../consume-packages/package-references-in-project-files.md): `ExcludeAssets="All"` bağımlılık ekleyin:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: Yalnızca istediğiniz sürümüreferans `.csproj` `C.dll` böylece dosyadan PackageC için başvuru kaldırın.
    
## <a name="dependency-updates-during-package-install"></a>Paket yükleme sırasında bağımlılık güncelleştirmeleri 

Bağımlılık sürümü zaten memnunsa, bağımlılık diğer paket yüklemeleri sırasında güncelleştirilemiyor. Örneğin, B paketine bağlı olan ve sürüm numarası için 1.0'ı belirten A paketini düşünün. Kaynak deposu, B paketinin 1.0, 1.1 ve 1.2 sürümlerini içerir. A zaten B sürüm 1.0 içeren bir projede yüklüyse, sürüm kısıtlamasını karşıladığı için B 1.0 kullanılmaya devam eder. Ancak, A paketi sürüm 1.1 veya b'nin daha yüksek isteklerini varsa, B 1.2 yüklenirdi. 

## <a name="resolving-incompatible-package-errors"></a>Uyumsuz paket hatalarını çözme

Paket geri yükleme işlemi sırasında "Bir veya daha fazla paket uyumlu değil..." hatasını görebilirsiniz. veya bir paketin projenin hedef çerçevesi ile "uyumlu olmadığını" belirtin.

Bu hata, projenizde başvurulan paketlerden birinin veya birkaçının projenin hedef çerçevesini desteklediğini göstermemesi durumunda oluşur; diğer bir deyişle, `lib` paket, projeyle uyumlu bir hedef çerçeve için klasöründe uygun bir DLL içermez. (Bir liste için [Hedef çerçevelerine](../reference/target-frameworks.md) bakın.) 

Örneğin, bir proje `netstandard1.6` hedefliyorsa ve yalnızca klasörlerde `lib\net20` ve `\lib\net45` klasörlerde DL içeren bir paket yüklemeye çalışırsanız, paket ve muhtemelen bağımlıları için aşağıdaki gibi iletileri görürsünüz:

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

Uyumsuzlukları gidermek için aşağıdakilerden birini yapın:

- Projenizi kullanmak istediğiniz paketler tarafından desteklenen bir çerçeveye yeniden hedefleyin.
- Paketlerin yazarıyla iletişime geçin ve seçtiğiniz çerçeveye destek eklemek için onlarla birlikte çalışın. [nuget.org'daki](https://www.nuget.org/) her paket listeleme sayfasının bu amaçla bir **İletişim Sahipleri** bağlantısı vardır.
