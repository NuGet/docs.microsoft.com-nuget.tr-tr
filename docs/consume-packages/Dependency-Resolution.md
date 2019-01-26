---
title: NuGet paket bağımlılık çözümlemesi
description: Üzerinden bir NuGet paketi bağımlılıkları çözümlendi ve her iki Nuget'te yüklü işlemiyle ilgili ayrıntılar 2.x ve NuGet 3.x+.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a561a49f2e733929e32584adf7b6849ea535c440
ms.sourcegitcommit: 585394f063e95dcbc24d7ac0ce07de643eaf6f4d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55046262"
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet Paket bağımlılıklarını nasıl çözümler?

Bir parçası olarak yüklenen içeren bir paket yüklü veya yeniden, dilediğiniz zaman bir [geri](../consume-packages/package-restore.md) işlemi, NuGet de, ilk paketi bağımlı olduğu tüm ek paketleri yükler.

Bu anında bağımlılıkları, için rasgele bir derinlik devam edebilirsiniz, kendi ilgili bağımlılıkları da olabilir. Bu ne çağrılır oluşturur bir *bağımlılık grafiği* , tüm düzeylerdeki paketleri arasındaki ilişkileri açıklar.

Birden çok paket aynı bağımlılık varsa, ardından aynı paket kimliği grafikte birden çok kez büyük olasılıkla farklı sürüm kısıtlamaları ile görünür. Ancak, NuGet hangi sürümünün kullanıldığını seçmeniz gerekir, böylece bir projede belirli bir paketin yalnızca bir sürümü kullanılabilir. Tam geçiş işlemi kullanılan paket Yönetimi biçimi bağlıdır.

## <a name="dependency-resolution-with-packagereference"></a>PackageReference ile bağımlılık çözümlemesi

Paketleri PackageReference biçimini kullanarak projelere yüklerken, NuGet uygun dosyasında bir düz paket grafik başvuruları ekler ve önceden çakışmaları çözer. Bu işlem olarak adlandırılır *geçişli geri yükleme*. Paketler geri yükleniyor veya yeniden yüklemeyi daha hızlı výsledek grafikte listelenen paketleri indirme işlemi ise ve daha öngörülebilir oluşturur. 2.8 gibi joker karakter (değişken) sürümleri avantajlarından da sürebilir. \*, pahalı önleme ve hata yapmaya açık çağrılar `nuget update` derleme sunucuları ve istemci makineleri.

NuGet geri yükleme işlemi önce bir yapı çalıştırıldığında, bağımlılıkları ilk bellekte giderir ve sonra elde edilen grafiğin adlı bir dosyaya yazar `project.assets.json` içinde `obj` PackageReference kullanarak bir proje klasörü. MSBuild bu dosyasını okur ve burada olası başvuruları bulunabilir ve ardından onları bellek proje ağacında ekler klasörleri kümesine çevirir.

Kilit dosyası geçicidir ve kaynak denetimine eklenmedi. Varsayılan olarak her ikisini de listelenen `.gitignore` ve `.tfignore`. Bkz: [paketleri ve kaynak denetimi](packages-and-source-control.md).

### <a name="dependency-resolution-rules"></a>Bağımlılık çözümlemesi kuralları

Geçişli geri yükleme bağımlılıkları çözümlemek için dört ana kuralları uygular: en düşük uygun sürümü, kayan sürümleri, en yakın WINS ve Kuzen bağımlılıkları.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>En düşük uygun sürümü

En düşük uygun sürüm kuralı bağımlılıklarını tarafından tanımlandığı şekilde bir paketin olası en düşük sürümü geri yükler. Ayrıca uygulama veya sınıf kitaplığı bağımlılıkları olarak bildirilmedikleri sürece geçerli [kayan](#floating-versions).

NuGet seçer 1.0 sürümü için aşağıdaki şekilde, örneğin, 1.0 beta 1.0 düşük olarak kabul edilir:

![Geçerli en düşük sürüm seçme](media/projectJson-dependency-1.png)

Sonraki şekilde, sürüm 2.1 akış üzerinde kullanılabilir değil ancak sürüm kısıtlaması olduğundan > bulabildiği, bu durumda 2.2 sonraki en düşük sürüm 2.1 NuGet Çekmeleri =:

![Özet akışı kullanılabilir bir sonraki en düşük sürüm seçme](media/projectJson-dependency-2.png)

Akış üzerinde kullanılabilir değil, 1.2 gibi bir tam sürüm numarası uygulamanın belirttiğinde, NuGet yükleyin veya paket geri yükleme girişimi sırasında bir hatayla başarısız:

![Tam paket sürümünün kullanılabilir olmadığı durumlarda NuGet bir hata oluşturur.](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>Kayan sürümleri (joker karakter)

Bir kayan veya joker karakter bağımlılık sürümü ile belirtilen \* joker karakter, 6.0 olduğu gibi.\*. Bu sürüm belirtimi "6.0.x en son sürümü kullan;" diyor. 4.\* anlamına gelir "en son 4.x sürümü kullanın." Joker karakter kullanarak, bir değişiklik kullanıcı uygulamanın gerek kalmadan gelişen devam etmek için bağımlılık paketini (veya paket) sağlar.

Joker karakter kullanırken, NuGet örneğin 6.0 sürüm deseni ile eşleşen bir paketin en yüksek sürümü çözümler. \* en yüksek sürüm 6.0 ile başlayan bir paketin alır:

![Sürüm 6.0.1 kayan bir sürüm olduğunda 6.0 seçme. * İstenen](media/projectJson-dependency-4.png)

> [!Note]
> Joker karakterler ve yayın öncesi sürümleri davranışı hakkında bilgi için [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>En yakın WINS

Bir uygulama için paket grafı aynı paketin farklı sürümlerini içerdiğinde, NuGet paketi uygulamaya grafikteki en yakın ve diğer tüm yok sayar seçer. Bu davranış, bağımlılık grafiği herhangi bir belirli bir paket sürümü geçersiz kılmak bir uygulama sağlar.

Aşağıdaki örnekte, uygulamanın doğrudan paket B ile bir sürüm kısıtlamasını bağımlı > 2.0 =. Uygulamanın sırayla Ayrıca paket B, ancak ile bağlı bir paket de bağımlı bir > = 1,0 kısıtlaması. Grafik uygulamada nearer to Paket B 2.0 bağımlı olduğundan, bu sürüm kullanılır:

![En yakın WINS kural kullanarak uygulama](media/projectJson-dependency-5.png)

>[!Warning]
> En yakın WINS kural diğer bağımlılıkları grafikte bozucu olabilecek böylece paket sürümünün indirgeme neden olabilir. Bu nedenle bu kural bir uyarı ile kullanıcıyı uyarmak için uygulanır.

NuGet belirli bir bağımlılık göz ardı edilir sonra da bu dalı grafiğin kalan tüm bağımlılıkları yoksayar. çünkü bu kural ayrıca verimliliği (örneğin BCL paketleri olanlar) büyük bir bağımlılık grafiği ile sonuçlanır. Paket C 2.0 kullanıldığından Aşağıdaki diyagramda, örneğin, NuGet paket C: daha eski bir sürümüne başvuruda bulunan herhangi bir dal graftaki yoksayar.

![Graftaki bir paket NuGet yoksayar, tüm bu dalı yoksayar.](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Kuzen bağımlılıkları

Farklı bir paket sürümleri için grafikteki aynı uzaklıkta uygulamadan adlandırılır, tüm sürüm gereksinimlerini karşılayan en düşük sürüm NuGet kullanır (olduğu gibi [en düşük uygun sürüm](#lowest-applicable-version) ve [ Kayan sürümleri](#floating-versions) kuralları). Aşağıdaki görüntüde, örneğin, paket B 2.0 sürümünü diğer karşılayan > = 1,0 kısıtlaması ve bu nedenle kullanılır:

![Tüm kısıtlamalar karşılayan daha düşük sürümünü kullanarak Kuzen bağımlılıkları çözümleniyor](media/projectJson-dependency-7.png)

Bazı durumlarda, tüm sürüm gereksinimlerini karşılamak mümkün değildir. Aşağıda gösterildiği gibi bir paket tam olarak 1.0 B paketi gerektirir ve paket C gerektiriyorsa Paket B > 2.0, =, NuGet bağımlılıklarını çözümlenemiyor ve bir hata verir.

![Çözümlenemeyen bağımlılıklar nedeniyle bir tam sürüm gereksinimi](media/projectJson-dependency-8.png)

Bu gibi durumlarda, üst düzey bir tüketici (uygulama veya Paketle) doğrudan kendi bağımlılık Paket B eklemeniz gerekir böylece [yakın WINS](#nearest-wins) kural uygular.

## <a name="dependency-resolution-with-packagesconfig"></a>Bağımlılık çözümlemesi packages.config ile

İle `packages.config`, bir proje bağımlılıklarınızı yazılır `packages.config` düz liste olarak. Bu paketlerin herhangi bir bağımlılığın aynı listesinde de yazılır. NuGet paketleri yüklendiğinde, ayrıca değişiklik yapabileceğiniz `.csproj` dosyası `app.config`, `web.config`ve diğer tek tek dosyaları.

İle `packages.config`, NuGet tek tek her paket yüklemesi sırasında bağımlılık çakışmaları dener. Bir paket yüklendiği ve paket B ve paket B bağlıdır, diğer bir deyişle, zaten listede `packages.config` bir bağımlılık, başka bir NuGet paketi istenen B sürümlerini karşılaştırır ve tüm sürüm karşılayan bir sürümünü bulmaya çalışır kısıtlamaları. Özellikle, NuGet alt seçer *AnaSürüm.altsürüm* bağımlılıkları karşılayan sürümü.

Varsayılan olarak, en düşük düzeltme eki sürümü için NuGet 2.8 görünür (bkz [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)). Bu ayar aracılığıyla denetleyebilirsiniz `DependencyVersion` özniteliğini `Nuget.Config` ve `-DependencyVersion` anahtarını komut satısına.  

`packages.config` Bağımlılıkları çözümlemek için daha büyük bir bağımlılık grafikleri karmaşık alır için işlem. Her yeni paket yükleme, tüm grafik geçişini gerektirir ve sürüm çakışmaları için Fırsat başlatır. Bir çakışma oluştuğunda, proje proje dosyasına olası değişiklikler ile özellikle belirsiz bir durumda bırakarak yükleme durduruldu. Bu sorun diğer paket Yönetimi biçimleri kullanırken değil.

## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

PackageReference biçimini kullanırken, hangi üst düzey proje bağımlılıkları akışına varlıklarından denetleyebilirsiniz. Ayrıntılar için bkz [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).

Üst düzey proje kendisi bir paketi olduğunda, bu akış bir denetime kullanarak'iniz de `include` ve `exclude` içinde listelenen bağımlılıkları özniteliklerle `.nuspec` dosya. Bkz: [.nuspec başvuru - bağımlılıkları](../reference/nuspec.md#dependencies).

## <a name="excluding-references"></a>Başvuruları hariç

Hangi derlemelerin aynı ada sahip birden çok kez bir projede, tasarım zamanı ve derleme zamanı hataları üreten başvurabilecek senaryo vardır. Özel bir sürümünü içeren bir projeye göz önünde bulundurun `C.dll`ve ayrıca içeren bir paket C başvurur `C.dll`. Aynı zamanda, projenin de Ayrıca paket C bağımlı bir paket B bağlıdır ve `C.dll`. NuGet, sonuç olarak, belirlenemiyor `C.dll` kullanmak için ancak yalnızca paket B de ona bağımlı olduğundan paket C bağımlı projenin kaldırılamıyor.

Bu sorunu çözmek için doğrudan başvurmalıdır `C.dll` , istediğiniz (veya doğru olanı başvuran başka bir paket kullanın) ve ardından paketi hariç tüm varlıklar üzerinde C bağımlılık ekleme. Bu gibi paket Yönetimi biçime bağlı olarak gerçekleştirilir:

- [PackageReference](../consume-packages/package-references-in-project-files.md): ekleme `ExcludeAssets="All"` bağımlılık olarak:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" ExcludeAssets="All" />
    ```

- `packages.config`: PackageC başvurusunu kaldırın `.csproj` yalnızca sürümü başvurduğu dosyasını `C.dll` istediğiniz.
    
## <a name="dependency-updates-during-package-install"></a>Paket bağımlılık güncelleştirirken yükleyin 

Bağımlılık, bağımlılık sürümü zaten getirildiyse diğer paket yüklemeleri sırasında güncelleştirilmez. Örneğin, paket B paketine bağlıdır ve 1.0 için sürüm numarasını belirten bir düşünün. Sürümlerinde 1.0, 1.1 ve 1.2 b paketinin kaynak deposu içerir A B sürüm 1.0 zaten var. bir projede yüklediyseniz, sürüm kısıtlamasını karşılayan çünkü B 1.0 kullanımda kalır. Bir paket istekleri sürüm 1.1 veya üzeri b olsaydı, ancak daha sonra B 1.2 yüklenecek. 

## <a name="resolving-incompatible-package-errors"></a>Uyumsuz paket hatalarını çözme

Sırasında paket geri yükleme işlemi, "bir veya daha fazla paket uyumlu değil..." veya bir paketi "uyumlu değil" hatasıyla karşılaşabilirsiniz projenin hedef çerçevesi ile.

Bu hata, bir veya daha fazla paket, projenizde başvurulan projenin hedef çerçevesi destekledikleri göstermez oluşur; diğer bir deyişle, paketi uygun bir DLL içinde içermiyor, `lib` proje ile uyumlu bir hedef çerçeve için klasör. (Bkz [hedef çerçeveyi](../reference/target-frameworks.md) bir listesi.) 

Örneğin, bir projenin hedeflediği `netstandard1.6` ve DLL içinde sadece içeren bir paket yüklemeye `lib\net20` ve `\lib\net45` klasörleri ve ardından paketi ve muhtemelen Etkilenenleri için şunun gibi iletilerine bakın:

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

Uyumsuzluk çözmek için şunlardan birini yapın:

- Kullanmak istediğiniz paketleri tarafından desteklenen bir çerçeve için projenizi yeniden hedeflendi.
- Paketleri yazarıyla iletişime geçin ve bunları seçtiğiniz çerçeveniz için destek eklemek için bunlarla çalışabilirsiniz. Sayfa üzerinde listeleme her paket [nuget.org](https://www.nuget.org/) sahip bir **kişi sahipleri** bu amaç için bağlantı.

