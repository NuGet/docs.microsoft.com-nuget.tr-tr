---
title: NuGet paket bağımlılığı çözümlemesi
description: NuGet paketinin bağımlılıklarının çözümlenme ve hem NuGet 2. x hem de NuGet 3. x + ' da yüklendiği işlemle ilgili ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 4b95251e4b055523a9533b4125589b2650be932d
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231090"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet paket bağımlılıklarını çözümler

Bir [geri yükleme](../consume-packages/package-restore.md) işleminin parçası olarak yüklenmekte olan bir paketin yüklenmesi veya yeniden yüklenmesi her seferinde, NuGet, ilk paketin bağımlı olduğu ek paketleri de yükler.

Bu anlık bağımlılıklar daha sonra kendi bağımlılıkları olabilir ve bu da rastgele bir derinliğe devam edebilir. Bu, tüm düzeylerde paketler arasındaki ilişkileri açıklayan bir *bağımlılık grafiği* olarak adlandırılan öğeleri oluşturur.

Birden çok paketin aynı bağımlılığı varsa, aynı paket KIMLIĞI birden çok kez grafikte görünebilir ve potansiyel olarak farklı sürüm kısıtlamalarına sahip olabilir. Ancak, belirli bir paketin yalnızca bir sürümü bir projede kullanılabilir; Bu nedenle NuGet, hangi sürümün kullanıldığını seçmelidir. Tam işlem, kullanılmakta olan paket yönetimi biçimine bağlıdır.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference ile bağımlılık çözümlemesi

, PackageReference biçimini kullanarak projelere paket yüklerken, NuGet ilgili dosyadaki düz bir paket grafiğine başvurular ekler ve çakışmaları önceden çözer. Bu işlem *geçişli geri yükleme*olarak adlandırılır. Paketleri yeniden yükleme veya geri yükleme işlemi daha sonra grafikte listelenen paketlerin indirilerek daha hızlı ve öngörülebilir yapılar elde edilir. Ayrıca, 2,8 gibi yüzen sürümlerden de yararlanabilirsiniz.\*, bir paketin en son sürümünü kullanmak üzere projeyi değiştirmeyi önlemek için.

NuGet geri yükleme işlemi bir derlemeden önce çalıştırıldığında, öncelikle bellekte bulunan bağımlılıkları çözer, ardından sonuç grafiğini `project.assets.json`adlı dosyaya yazar. Ayrıca, [dosya kilitleme işlevi etkinse](../consume-packages/package-references-in-project-files.md#locking-dependencies), çözümlenmiş bağımlılıkları `packages.lock.json`adlı bir kilit dosyasına yazar.
Varlıklar dosyası `MSBuildProjectExtensionsPath`konumunda bulunur ve varsayılan olarak projenin ' obj ' klasörüdür. MSBuild sonra bu dosyayı okur ve olası başvuruların bulunabileceği bir klasör kümesine çevirir ve sonra bunları bellekte proje ağacına ekler.

`project.assets.json` dosyası geçicidir ve kaynak denetimine eklenmemelidir. Varsayılan olarak hem `.gitignore` hem de `.tfignore`listelenir. Bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Bağımlılık çözümleme kuralları

Geçişli geri yükleme, bağımlılıkları çözümlemek için dört ana kural uygular: en düşük uygulanabilir sürüm, kayan sürümler, en yakın WINS ve Cousin bağımlılıkları.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>En düşük uygulanabilir sürüm

En düşük uygulanabilir sürüm kuralı, bağımlılıklarıyla tanımlanan bir paketin olası en düşük sürümünü geri yükler. Ayrıca, [kayan](#floating-versions)olarak bildirilmeyen sürece uygulama veya sınıf kitaplığındaki bağımlılıklar için de geçerlidir.

Aşağıdaki şekilde, örneğin, 1,0-Beta 1,0 ' den daha düşük kabul edilir, böylece NuGet 1,0 sürümünü seçer:

![Uygulanabilir en düşük sürümü seçme](media/projectJson-dependency-1.png)

Sonraki şekilde, sürüm 2,1 akışta kullanılamaz, ancak sürüm kısıtlaması > = 2,1, bu 2,2 örnekte, bulabileceği bir sonraki en düşük sürümü seçer:

![Akışta bulunan bir sonraki en düşük sürümü seçme](media/projectJson-dependency-2.png)

Bir uygulama, akışta bulunmayan 1,2 gibi tam bir sürüm numarası belirttiğinde, paketi yüklemeye veya yüklemeye çalışırken NuGet hata vererek başarısız olur:

![Tam paket sürümü kullanılabilir olmadığında NuGet bir hata oluşturuyor](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Kayan sürümler

\* karakteriyle bir kayan bağımlılık sürümü belirtildi. Örneğin, `6.0.*`. Bu sürüm belirtimi "en son 6.0. x sürümünü kullan" ifadesini belirtir. `4.*` "en son 4. x sürümünü kullanın" anlamına gelir. Kayan bir sürümün kullanılması proje dosyasındaki değişiklikleri azaltır ve en son bir bağımlılık sürümüyle güncel tutmaya çalışır.

Bir kayan sürüm kullanırken NuGet, sürüm düzeniyle eşleşen bir paketin en yüksek sürümünü çözümler. Örneğin `6.0.*` 6,0 ile başlayan bir paketin en yüksek sürümünü alır:

![6,0. * kayan sürümü istendiğinde sürüm 6.0.1 seçiliyor](media/projectJson-dependency-4.png)

> [!Note]
> Kayan sürümlerin ve yayın öncesi sürümlerinin davranışı hakkında bilgi için bkz. [paket sürümü oluşturma](package-versioning.md#version-ranges).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>En yakın WINS

Bir uygulamanın paket grafı aynı paketin farklı sürümlerini içerdiğinde, NuGet grafikteki uygulamaya en yakın paketi seçer ve diğerlerini yoksayar. Bu davranış, bir uygulamanın bağımlılık grafiğinde belirli bir paket sürümünü geçersiz kılmasına izin verir.

Aşağıdaki örnekte, uygulama, > = 2.0 sürüm kısıtlaması ile doğrudan B paketine bağlıdır. Uygulama Ayrıca pakete bağımlıdır ve ayrıca, B paketine bağlıdır, ancak bir > = 1.0 kısıtlaması vardır. B 2,0 paketindeki bağımlılık grafikteki uygulamaya yaklaştığında, bu sürüm kullanılır:

![En yakın WINS kuralını kullanan uygulama](media/projectJson-dependency-5.png)

>[!Warning]
> En yakın WINS kuralı, paket sürümünün indirgenmesine neden olabilir ve bu sayede grafikteki diğer bağımlılıkları büyük olasılıkla bozabilir. Bu nedenle, bu kural kullanıcıyı uyarmak için bir uyarıyla uygulanır.

Bu kural, büyük bir bağımlılık grafiğine (BCL paketleri gibi) daha fazla verimlilik elde eder, çünkü belirli bir bağımlılık yoksayılırsa NuGet Ayrıca grafiğin o dalında kalan tüm bağımlılıkları yoksayar. Aşağıdaki diyagramda, örneğin, C 2,0 paketi kullanıldığı için, NuGet, grafikteki paket C 'nin eski bir sürümüne başvuran dalları yok sayar:

![NuGet grafikteki bir paketi yok saydığı zaman, tüm dalı yoksayar](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Cousin bağımlılıkları

Farklı paket sürümlerine uygulamanın grafiğinde aynı uzaklıkta başvurulur, NuGet tüm sürüm gereksinimlerini karşılayan en düşük sürümü ( [En düşük ilgili sürüm](#lowest-applicable-version) ve [kayan sürümler](#floating-versions) kuralları) kullanır. Aşağıdaki görüntüde, örneğin B paketinin 2,0 sürümü diğer > = 1.0 kısıtlamasını karşılar ve bu nedenle kullanılır:

![Tüm kısıtlamaları karşılayan alt sürümü kullanarak Cousin bağımlılıkları çözümleniyor](media/projectJson-dependency-7.png)

Bazı durumlarda, tüm sürüm gereksinimlerini karşılamak mümkün değildir. Aşağıda gösterildiği gibi, A paketi tam olarak B 1,0 paketini gerektiriyorsa ve C paketi B > = 2.0 paketini gerektiriyorsa, NuGet bağımlılıkları çözümleyemez ve bir hata verir.

![Kesin bir sürüm gereksinimi nedeniyle çözümlenebilen bağımlılıklar](media/projectJson-dependency-8.png)

Bu durumlarda, en [yakın WINS](#nearest-wins) kuralının uygulanması için üst düzey tüketici (uygulama veya paket) B paketine kendi doğrudan bağımlılığını eklemesi gerekir.

## <a name="dependency-resolution-with-packagesconfig"></a>Packages. config ile bağımlılık çözümlemesi

`packages.config`, projenin bağımlılıkları düz bir liste olarak `packages.config` yazılır. Bu paketlerin tüm bağımlılıkları aynı listeye de yazılır. Paketler yüklendiğinde, NuGet `.csproj` dosyasını, `app.config`, `web.config`ve diğer tek dosyaları da değiştirebilir.

`packages.config`, NuGet her bir paketin yüklenmesi sırasında bağımlılık çakışmalarını çözmeye çalışır. Diğer bir deyişle, A paketi yüklenip B paketine bağlı ise ve B paketi zaten başka bir şeyin bağımlılığı olarak `packages.config` ' de listeleniyorsa, NuGet, istenen paket B 'nin sürümlerini karşılaştırır ve tüm sürüm kısıtlamalarını karşılayan bir sürüm bulmaya çalışır. Özellikle NuGet, bağımlılıkları karşılayan düşük *ana. Minor* sürümünü seçer.

Varsayılan olarak, NuGet 2,8 en düşük düzeltme eki sürümünü arar (bkz. [nuget 2,8 sürüm notları](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Bu ayarı, `Nuget.Config` `DependencyVersion` özniteliği ve komut satırındaki `-DependencyVersion` anahtarı aracılığıyla denetleyebilirsiniz.  

Bağımlılıkları çözümlemek için `packages.config` süreci, daha büyük bağımlılık grafikleri için karmaşıktır. Her yeni paket yüklemesi için tüm grafiğin bir çapraz geçişi gerekir ve sürüm çakışmaları için şans yükseltilir. Bir çakışma oluştuğunda, yükleme durdurulur ve özellikle proje dosyasının kendisinde olası değişiklikler ile projeyi belirsiz bir durumda bırakır. Diğer paket yönetim biçimleri kullanılırken bu bir sorun değildir.

## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

PackageReference biçimini kullanırken, bağımlılıklardan hangi varlıkların en üst düzey projeye akabilir olduğunu denetleyebilirsiniz. Ayrıntılar için bkz. [Packagereference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Üst düzey proje bir paket olduğunda, `include` ve `exclude` özniteliklerini `.nuspec` dosyasında listelenen bağımlılıklarla birlikte kullanarak da bu akış üzerinde denetime sahip olursunuz. Bkz [. nuspec başvurusu-bağımlılıklar](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Başvuruları dışlama

Aynı ada sahip derlemelere bir projede birden fazla kez başvurulabileceği, tasarım zamanı ve derleme zamanı hataları üreten senaryolar vardır. `C.dll`özel bir sürümünü içeren bir proje düşünün ve ayrıca, `C.dll`içeren C paketine başvurur. Aynı zamanda, proje Ayrıca C ve `C.dll`paketine bağlı olan B paketine da bağımlıdır. Sonuç olarak, NuGet hangi `C.dll` kullanacağınızı belirleyemez, ancak B paketi de buna bağlı olduğundan, projenin C paketine yönelik bağımlılığını kaldıramazsınız.

Bu sorunu çözmek için, istediğiniz `C.dll` doğrudan başvurmalı (veya sağ bir referans veren başka bir paket kullanmanız) ve ardından, tüm varlıklarını dışlayan bir Package C 'ye bağımlılık eklersiniz. Bu, kullanımdaki paket yönetimi biçimine bağlı olarak aşağıdaki gibi gerçekleştirilir:

- [Packagereference](../consume-packages/package-references-in-project-files.md): bağımlılıkta `ExcludeAssets="All"` ekleyin:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: `.csproj` dosyasındaki başvuruyu, yalnızca istediğiniz `C.dll` sürümüne başvuracak şekilde kaldırın.
    
## <a name="dependency-updates-during-package-install"></a>Paket yüklemesi sırasında bağımlılık güncelleştirmeleri 

Bağımlılık sürümü zaten karşılandıysa, diğer paket yüklemeleri sırasında bağımlılık güncellenmez. Örneğin, B paketine bağlı A paketini düşünün ve sürüm numarası için 1,0 öğesini belirtin. Kaynak Depo, B paketinin 1,0, 1,1 ve 1,2 sürümlerini içerir. Zaten B sürüm 1,0 içeren bir projede yüklüyse, sürüm kısıtlamasını karşıladığından B 1,0 kullanımda kalır. Ancak, paketi B 'nin 1,1 veya üzeri bir sürümünü isterse, B 1,2 yüklenir. 

## <a name="resolving-incompatible-package-errors"></a>Uyumsuz paket hatalarını çözme

Bir paket geri yükleme işlemi sırasında, "bir veya daha fazla paket uyumlu değil..." hatasını görebilirsiniz. ya da projenin hedef çerçevesiyle bir "uyumlu değil" paketi.

Bu hata, projenizde başvurulan bir veya daha fazla paketin projenin hedef çerçevesini desteklediğini belirtmediğinde oluşur; diğer bir deyişle, paket, proje ile uyumlu bir hedef çerçeve için `lib` klasöründe uygun bir DLL içermez. (Bkz. bir liste için [hedef çerçeveler](../reference/target-frameworks.md) .) 

Örneğin, bir proje `netstandard1.6` hedefliyorsa ve DLL 'Leri içeren bir paketi yalnızca `lib\net20` ve `\lib\net45` klasörlerinde yüklemeye çalışırsanız, paket ve muhtemelen bağımlıları için aşağıdakiler gibi iletiler görürsünüz:

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

Uyumsuzlukları çözümlemek için aşağıdakilerden birini yapın:

- Projenizi kullanmak istediğiniz paketler tarafından desteklenen bir çerçeveye yeniden hedefleyin.
- Paketlerin yazarına başvurun ve seçtiğiniz çerçeve için destek eklemek üzere bunlarla birlikte çalışın. [NuGet.org](https://www.nuget.org/) üzerindeki her paket listeleme sayfasında bu amaçla bir **iletişim sahipleri** bağlantısı bulunur.
