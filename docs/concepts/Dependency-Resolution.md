---
title: NuGet Paketi Bağımlılık Çözümlemesi
description: Bir NuGet paketinin bağımlılıklarını çözümle ve hem NuGet 2.x hem de NuGet 3.x+ üzerine yükleme işlemiyle ilgili ayrıntılar.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 69adbbad20debf2e53f247e85d638b3226c0491d
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323758"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet paket bağımlılıklarını nasıl çözümler?

Geri yükleme işleminin bir parçası olarak yüklemeyi içeren bir paket [](../consume-packages/package-restore.md) her yüklenir veya yeniden yüklenirken, NuGet ilk paketin bağlı olduğu tüm ek paketleri de yüklenir.

Bu anlık bağımlılıkların kendi bağımlılıkları da olabilir ve bu da rastgele bir derinliğe kadar devam eder. Bu, tüm düzeylerde *paketler arasındaki* ilişkileri açıklayan bağımlılık grafı olarak adlandırılan bir grafik üretir.

Birden çok paket aynı bağımlılığına sahipse, grafikte farklı sürüm kısıtlamaları olabilecek şekilde aynı paket kimliği birden çok kez görünebilir. Ancak, bir projede, verilen paketin yalnızca bir sürümü kullanılabilir, bu nedenle NuGet'in hangi sürümün kullan gerektiğini seçmesi gerekir. Tam işlem, kullanılan paket yönetimi biçimine bağlıdır.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference ile bağımlılık çözümlemesi

PackageReference biçimini kullanarak paketleri projelere yüklerken, NuGet uygun dosyada düz bir paket grafiğine başvurular ekler ve çakışmaları zamanından önce çözer. Bu işlem geçişli geri yükleme *olarak adlandırılır.* Paketleri yeniden yüklemek veya geri yüklemek, grafikte listelenen paketlerin indirerek daha hızlı ve tahmin edilebilir derlemeler elde etmektir. Projenin bir paketin en son sürümünü kullanmak üzere değiştirilmesini önlemek için 2.8. gibi kayan \* sürümlerden de faydalanabilirsiniz.

NuGet geri yükleme işlemi bir derlemeden önce çalıştır geldiğinde, önce bellekte bağımlılıkları çözümler, ardından sonuçta elde edilen grafiği adlı dosyaya `project.assets.json` yazar. Ayrıca kilit dosyası işlevselliği etkinse çözümlenen bağımlılıkları `packages.lock.json` adlı bir kilit dosyasına [yazar.](../consume-packages/package-references-in-project-files.md#locking-dependencies)
Assets dosyası, varsayılan olarak `MSBuildProjectExtensionsPath` projenin 'obj' klasörünün bulunduğu konumda bulunur. MSBuild daha sonra bu dosyayı okur ve olası başvuruların buluna bir klasör kümesine çevirir ve sonra bunları bellekte proje ağacına ekler.

Dosya `project.assets.json` geçicidir ve kaynak denetimine eklenmemalıdır. Hem hem de içinde varsayılan olarak `.gitignore` `.tfignore` listelenir. Bkz. [Paketler ve kaynak denetimi.](../consume-packages/packages-and-source-control.md)

### <a name="dependency-resolution-rules"></a>Bağımlılık çözümleme kuralları

Geçişli geri yükleme, bağımlılıkları çözümlemek için dört ana kural uygular: en düşük uygulanabilir sürüm, kayan sürümler, en yakın kazançlar ve bağımlılık bağımlılıkları.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>Geçerli en düşük sürüm

En düşük geçerli sürüm kuralı, bağımlılıkları tarafından tanımlandığı şekilde bir paketin mümkün olan en düşük sürümünü geri yüklür. Kayan olarak bildirndiği sürece uygulama veya sınıf kitaplığı bağımlılıkları için de [geçerlidir.](#floating-versions)

Aşağıdaki şekilde, örneğin, 1.0-beta sürümü 1.0'dan düşük olarak kabul edilir, bu nedenle NuGet 1.0 sürümünü seçer:

![En düşük geçerli sürümü seçme](media/projectJson-dependency-1.png)

Sonraki şekilde, sürüm 2.1 akışta kullanılamaz, ancak sürüm kısıtlaması >= 2.1 NuGet tarafından buluna bir sonraki en düşük sürümü seçer( bu durumda 2.2):

![Akışta kullanılabilir bir sonraki en düşük sürümü seçme](media/projectJson-dependency-2.png)

Bir uygulama, akışta mevcut olan 1.2 gibi tam bir sürüm numarası belirtirse, NuGet paketi yükleme veya geri yükleme denemesi sırasında hatayla başarısız olur:

![Tam paket sürümü kullanılabilir değilken NuGet bir hata üretir](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-versions"></a>Kayan sürümler

karakteriyle bir kayan bağımlılık sürümü \* belirtilir. Örneğin, `6.0.*`. Bu sürüm belirtimi "en son 6.0.x sürümünü kullan" şeklindedir; `4.*` " en son 4.x sürümünü kullan" anlamına gelir. Kayan sürümün kullanılması, proje dosyasında yapılacak değişiklik sayısını azaltırken bağımlılığın en son sürümünün kullanılmasını sağlar.

Kayan sürüm kullanırken NuGet, bir paketin sürüm deseniyle eşleşen en yüksek sürümünü çözümler; örneğin, 6.0 ile başlayan bir paketin en yüksek `6.0.*` sürümünü alır:

![Kayan sürüm 6.0.* istenerek 6.0.1 sürümünü seçme](media/projectJson-dependency-4.png)

> [!Note]
> Kayan sürümlerin ve yayın öncesi sürümlerin davranışı hakkında bilgi için [bkz. Paket sürümü.](package-versioning.md#version-ranges)


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>En yakın kazançlar

Bir uygulamanın paket grafiği aynı paketin farklı sürümlerini içerdiğinde, NuGet grafikte uygulamaya en yakın paketi seçer ve diğer tüm sürümleri yoksayır. Bu davranış, bir uygulamanın bağımlılık grafı içinde belirli bir paket sürümünü geçersiz kılmaya olanak sağlar.

Aşağıdaki örnekte uygulama, sürüm kısıtlaması =2.0 olan B paketine >bağlıdır. Uygulama ayrıca Paket A'ya da bağlıdır ve bu paket de B Paketine bağlıdır, ancak =1>1.0 kısıtlamasına bağlıdır. B 2.0 Paketi bağımlılığı grafikte uygulamaya daha yakın olduğundan bu sürüm kullanılır:

![En Yakın Wins kuralını kullanan uygulama](media/projectJson-dependency-5.png)

>[!Warning]
> En Yakın Kazançlar kuralı, paket sürümünün eski sürüme düşürülerek grafikte diğer bağımlılıkların hataya neden olmasıyla sonuçlanabilecek. Bu nedenle bu kural, kullanıcıya uyarı için bir uyarı ile uygulanır.

Bu kural ayrıca büyük bir bağımlılık grafı (örneğin, BCL paketlerine sahip olanlar) ile daha yüksek verimlilikle sonuç verir. Bunun nedeni, verilen bir bağımlılık yoksayılırsa NuGet'in grafiğin bu dalda kalan tüm bağımlılıkları da yoksaymalarıdır. Aşağıdaki diyagramda, örneğin, Paket C 2.0 kullanılırken NuGet grafikte C Paketinin eski bir sürümüne başvuran dalları yoksayır:

![NuGet grafikte bir paketi yoksayıyorsa tüm dalı yoksayıyor](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Bağımlılık bağımlılıkları

Grafikte uygulamadan farklı paket sürümlerine aynı uzaklıkta başvurulsa, NuGet tüm sürüm gereksinimlerini (en düşük [](#lowest-applicable-version) geçerli sürüm ve kayan sürüm kurallarında olduğu gibi) en düşük [sürümü](#floating-versions) kullanır. Aşağıdaki görüntüde, örneğin B Paketinin 2.0 sürümü diğer >=1.0 kısıtlamasını karşılar ve bu nedenle kullanılır:

![Tüm kısıtlamaları karşılar alt sürümünü kullanarak bağımlılık bağımlılıklarını çözme](media/projectJson-dependency-7.png)

Bazı durumlarda tüm sürüm gereksinimlerini karşılamak mümkün değildir. Aşağıda gösterildiği gibi, A Paketi tam olarak B 1.0 Paketini gerektiriyorsa ve C Paketi B paketi >=2.0 gerektiriyorsa, NuGet bağımlılıkları çözümleyemezse ve bir hata verir.

![Tam sürüm gereksinimi nedeniyle çözülemeyen bağımlılıklar](media/projectJson-dependency-8.png)

Bu gibi durumlarda en üst düzey tüketicinin (uygulama veya paket) En Yakın Wins kuralının geçerli olması için B Paketine kendi [doğrudan bağımlılığını eklemesi](#nearest-wins) gerekir.

## <a name="dependency-resolution-with-packagesconfig"></a>packages.config ile bağımlılık packages.config

ile, `packages.config` projenin bağımlılıkları düz bir `packages.config` liste olarak yazılır. Bu paketlerin tüm bağımlılıkları da aynı listede yazılır. Paketler yüklenirken NuGet, , ve diğer tek tek `.csproj` `app.config` dosyaları da `web.config` değiştirebilir.

ile, `packages.config` NuGet her bir paketin yüklenmesi sırasında bağımlılık çakışmalarını çözmeye çalışır. Başka bir ifadeyle, A Paketi yüklenmiyorsa ve Paket B'ye bağlı ise ve B Paketi zaten başka bir şeyin bağımlılığı olarak listelenmişse NuGet, istenen B Paketinin sürümlerini karşılar ve tüm sürüm kısıtlamalarına göre bir sürüm bulmaya `packages.config` çalışır. Özellikle, NuGet bağımlılıkları *karşılar alt ana.ikincil* sürümünü seçer.

Varsayılan olarak, NuGet 2.8 en düşük düzeltme eki sürümünü (bkz. [NuGet 2.8 sürüm notları).](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) Bu ayarı, içinde özniteliği `DependencyVersion` ve komut satırı anahtarı aracılığıyla kontrol etmek `NuGet.Config` `-DependencyVersion` için.  

Bağımlılıkları `packages.config` çözümleme işlemi, daha büyük bağımlılık grafları için karmaşık hale geliyor. Her yeni paket yüklemesi, grafiğin tamamının çapraz geçiş işlemini gerektirir ve sürüm çakışmaları ihtimalini yükselter. Bir çakışma oluştuğunda, yükleme durdurulur ve özellikle de proje dosyasının kendisinde olası değişiklikler olduğunda projeyi belirsiz bir durumda bırakarak. Bu, diğer paket yönetim biçimlerini kullanırken sorun olmaz.

## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

PackageReference biçimini kullanırken, bağımlılıklardan hangi varlıkların en üst düzey projeye akacaklarını kontrol etmek için kullanılabilirsiniz. Ayrıntılar için bkz. [PackageReference](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

Üst düzey proje bir paket olduğunda, dosyada listelenen bağımlılıklarla ve özniteliklerini kullanarak bu `include` `exclude` akış üzerinde de denetime sahip `.nuspec` olursanız. Bkz. [.nuspec Başvurusu - Bağımlılıklar.](../reference/nuspec.md#dependencies)

## <a name="excluding-references"></a>Başvuruları dışlama

Projede aynı adla derlemelere birden çok kez başvurularak tasarım zamanı ve derleme zamanı hataları üreten senaryolar vardır. özel bir sürümünü içeren bir proje düşünün ve içeren `C.dll` Paket C'ye `C.dll` başvurur. Aynı zamanda, proje ayrıca Paket B'ye de bağlıdır ve bu da C paketine ve 'ye `C.dll` bağlıdır. Sonuç olarak, NuGet hangisinin kullanılamayacaklarını belirleyeb, ancak B Paketi de buna bağımlı olduğundan projenin C Paketi bağımlılığını `C.dll` kaldıranın.

Bu sorunu çözmek için doğrudan istediğiniz pakete başvurabilirsiniz (veya doğru pakete başvurulan başka bir paket kullanın) ve ardından tüm varlıklarını dışlamak için C Paketine bir `C.dll` bağımlılık eklemeniz gerekir. Bu, kullanımda paket yönetimi biçimine bağlı olarak aşağıdaki gibi yapılır:

- [PackageReference:](../consume-packages/package-references-in-project-files.md) `ExcludeAssets="All"` bağımlılığına ekleyin:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: Yalnızca istediğiniz sürümüne başvuracak şekilde PackageC `.csproj` başvurularını `C.dll` dosyadan kaldırın.
    
## <a name="dependency-updates-during-package-install"></a>Paket yüklemesi sırasında bağımlılık güncelleştirmeleri 

Bir bağımlılık sürümü zaten karşılanıyorsa, bağımlılık diğer paket yüklemeleri sırasında güncelleştirilmez. Örneğin, B paketine bağlı olan ve sürüm numarası için 1.0'a sahip A paketini düşünün. Kaynak depo B paketinin 1.0, 1.1 ve 1.2 sürümlerini içerir. A zaten B sürüm 1.0 içeren bir projede yüklüyse, sürüm kısıtlamasını karşılasa B 1.0 kullanımda kalır. Ancak, A paketi B'nin 1.1 veya daha yüksek bir sürümünü talep ettiyse B 1.2 yüklenir. 

## <a name="resolving-incompatible-package-errors"></a>Uyumsuz paket hatalarını çözme

Paket geri yükleme işlemi sırasında "Bir veya daha fazla paket uyumlu değil..." hatasını alabilirsiniz veya bir paketin projenin hedef çerçevesiyle "uyumlu değil" olduğunu.

Bu hata, projenize başvurulan paketlerden biri veya daha fazlası projenin hedef çerçevesini desteklemektedir; diğer bir ifadeyle paket, projeyle uyumlu bir hedef çerçeve `lib` için klasöründe uygun bir DLL'ye sahip değildir. (Liste [için bkz.](../reference/target-frameworks.md) Hedef çerçeveler.) 

Örneğin, bir proje hedeflense ve yalnızca ve klasörlerine URL'ler içeren bir paket yükleme girişiminde bulunursanız, paket ve büyük olasılıkla bağımlıları için aşağıdaki gibi `netstandard1.6` `lib\net20` iletiler `\lib\net45` görüyorsunuz:

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

Uyumsuzlukları çözmek için, aşağıdakilerden birini yapın:

- Projenizi kullanmak istediğiniz paketler tarafından desteklenen bir çerçeveye yeniden hedefle.
- Paketlerin yazarına başvurun ve seçtiğiniz çerçeveye destek eklemek için onlarla çalışın. Uygulama sayfasındaki her [paket nuget.org](https://www.nuget.org/) bu amaçla bir **Kişi Sahipleri** bağlantısı vardır.
