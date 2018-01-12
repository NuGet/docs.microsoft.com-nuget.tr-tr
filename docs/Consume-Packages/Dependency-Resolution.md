---
title: "NuGet paketi bağımlılık çözümleme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "Üzerinden bir NuGet paketin bağımlılıklarını çözümlendi ve her iki NuGet yüklü işlemiyle ilgili ayrıntılar 2.x ve NuGet 3.x+."
keywords: "NuGet Paket bağımlılıklarını, NuGet sürüm oluşturma, bağımlılık sürümleri, sürüm grafiği, sürüm çözünürlüğü, geçişli geri yükleme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 93a3d077a6dd1946485fc8c48f97c8009280890c
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/10/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a>NuGet Paket bağımlılıklarını nasıl çözümler

Bir parçası olarak yüklenen içeren bir paket yüklü veya yeniden, dilediğiniz zaman bir [geri](../consume-packages/package-restore.md) işlemi, NuGet de ilk paket bağımlı olduğu herhangi bir ek paket yükler.

Bu hemen bağımlılıkları da kendi başlarına, için rasgele bir derinliği devam edebilirsiniz bağımlılıkları olabilir. Bu ne adlı üreten bir *bağımlılık grafiğinin* paketleri arasındaki ilişkileri açıklar tüm düzeyleri şunlardır.

Birden çok paket aynı bağımlılık varsa, daha sonra aynı paket kimliği grafikte birden çok kez olası farklı sürüm kısıtlamalarıyla görünebilir. NuGet hangi sürümü seçmeniz gerekir böylece ancak, belirli bir paket yalnızca bir sürümü bir projede kullanılabilir kullanılabilir. Tam işlem kullanılan paket başvuru biçimi bağlıdır.

Bu konuda:
- [PackageReference ve project.json bir bağımlılık çözümleme](#dependency-resolution-with-packagereference-and-projectjson)
- [Packages.config bir bağımlılık çözümleme](#dependency-resolution-with-packagesconfig)
- [Başvuruları hariç](#excluding-references), bir proje ve bir başkası tarafından üretilen bir derlemeyi belirtilen bir bağımlılık arasında bir çakışma olduğunda gerekli olduğu.
- [Paket sırasında bağımlılık güncelleştirmeleri yükle](#dependency-updates-during-package-install)
- [Uyumsuz paket hatalarını çözme](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a>PackageReference ve project.json bir bağımlılık çözümleme

Paketleri PackageReference kullanarak projelere yüklerken veya `project.json` biçimleri, NuGet uygun dosyasında bir düz paket grafik başvuruları ekler ve önceden çakışmalar çözümlendi. Bu işlem olarak adlandırılır *geçişli geri yükleme*. Yeniden yüklemeyi veya paketleri geri sonra daha hızlı sonuçta grafikte listelenen paketler indirme işlemi ve daha tahmin edilebilir oluşturur. Ayrıca 2.8 gibi joker karakter (kayan) sürümlerinden yararlanabilirsiniz. \*, pahalı önlemenin ve hata potansiyeli çağrıları `nuget update` yapı sunucuları ve istemci makineleri.

NuGet geri yükleme işlemi önce bir yapı çalıştığında, bağımlılıkları ilk bellekte çözümler, ardından, elde edilen grafik adlı bir dosyaya yazar `project.assets.json` içinde `obj` klasörü PackageReference kullanarak bir proje veya adlı bir dosyaya `project.lock.json` yanında `project.json`. MSBuild sonra bu dosyayı okur ve burada olası başvurular bulunabilir ve ardından bunları bellek proje ağacında ekler klasörler kümesi çevirir.

Kilit dosyası geçicidir ve kaynak denetimi eklenmemesi. Hem de varsayılan olarak listelenen `.gitignore` ve `.tfignore`. Bkz: [paketler ve kaynak denetimi](Packages-and-Source-Control.md).

### <a name="dependency-resolution-rules"></a>Bağımlılık çözümleme kurallarını

Geçişli geri yükleme bağımlılıkları çözümlemek için dört ana kuralları uygular: en düşük geçerli sürüm, kayan sürümleri, en yakın WINS ve Kuzen bağımlılıkları.

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a>En düşük geçerli sürüm

En düşük geçerli sürüm kuralı bağımlılıklarını tarafından tanımlandığı şekilde bir paketin olası en düşük sürümü yükler. Ayrıca uygulama veya sınıf kitaplığı bağımlılıkları olarak bildirilir sürece uygulandığı [kayan](#floating-versions).

NuGet 1.0 sürümü seçer şekilde aşağıdaki şekilde, örneğin, 1.0 beta 1.0 düşük olarak kabul edilir:

![Geçerli en düşük sürüm seçme](media/projectJson-dependency-1.png)

Sonraki şekilde, sürüm 2.1 Besleme üzerindeki kullanılabilir değil ancak sürüm kısıtlaması olduğundan > bunu bulabilir, bu durumda 2.2 sonraki en düşük sürüm 2.1 NuGet Çekmeleri =:

![Özet akışı kullanılabilir sonraki en düşük sürüm seçme](media/projectJson-dependency-2.png)

Uygulamanın Besleme üzerindeki kullanılabilir değil, 1.2 gibi bir tam sürüm numarası belirttiğinde NuGet bir hata ile yüklemek veya paket geri yükleme girişimi sırasında başarısız oluyor:

![Bir tam paket sürümü mevcut olmadığında NuGet, bir hata oluşturur.](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a>(Joker karakterler) kayan sürümleri

Bir kayan veya joker karakter bağımlılık sürümü ile belirtilen \* joker karakter olarak 6.0 ile.\*. "En son 6.0.x sürümü kullan"; Bu sürüm belirtimi diyor 4.\* anlamına gelir "kullan en son 4.x sürümünü." Bir joker karakter kullanılması, bir kullanıcı uygulama için bir değişiklik gerektirmeden gelişen devam etmek için bağımlılık paketi (veya paketi) sağlar.

Joker karakter kullanırken, NuGet yüksek paketinin sürümünü, örneğin 6.0 sürüm desenle eşleşen bir çözümler. \* en yüksek sürüm 6.0 ile başlayan bir paketin alır:

![Sürüm 6.0.1 kayan bir sürüm olduğunda 6.0 seçme. * İstenen](media/projectJson-dependency-4.png)

> [!Note]
> Joker karakterler ve yayın öncesi sürümlerini davranışı hakkında bilgi için bkz: [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a>Yakın WINS

Bir uygulama için paket grafik aynı paketin farklı sürümlerini içerdiğinde, NuGet grafiği uygulamada yakın ve diğer tüm yoksayar paketi seçer. Bu davranış herhangi belirli paket sürümünü bağımlılık grafiğinin geçersiz kılmak bir uygulama sağlar.

Aşağıdaki örnekte, uygulamanın doğrudan sürüm kısıtlaması, paket B bağımlı > 2.0 =. Uygulamanın Paket B, aynı ile sırayla de bağlıdır A paketi de bağımlı bir > 1.0 kısıtlaması =. Grafik uygulamada nearer to Paket B 2.0 bağımlı olduğu için bu sürüm kullanılır:

![Yakın WINS kuralı kullanarak uygulama](media/projectJson-dependency-5.png)

>[!Warning]
> Yakın WINS kural böylece büyük olasılıkla başka bir bağımlılık grafikte yeni Paket sürümü, eski sürüme düşürülmesini neden olabilir. Bu nedenle bu kural bir uyarı ile kullanıcıyı uyarmak için uygulanır.

Verilen bir bağımlılık göz ardı sonra NuGet de o şubedeki grafik kalan tüm bağımlılıkları yoksayar çünkü bu kural ayrıca verimliliği büyük bağımlılık grafiğinin (örneğin BCL paketleri olanlar) ile sonuçlanır. Paket C 2.0 kullanıldığından, aşağıdaki çizimde NuGet paketi C: daha eski bir sürümü başvuran tüm dalları grafikte örneğin yoksayar.

![NuGet paket grafikte yoksayar, tüm bu dalı yoksayar](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a>Kuzen bağımlılıkları

Farklı paketi sürümleri için grafikte aynı uzaklıkta uygulamadan adlandırılır NuGet tüm sürüm gereksinimlerini karşılayan en düşük sürüm kullanır (olduğu gibi [en düşük geçerli sürüm](#lowest-applicable-version) ve [ sürümleri kayan](#floating-versions) kuralları). Aşağıdaki resimde, örneğin, paket B 2.0 sürümünü diğer karşılayan > 1.0 kısıtlaması = ve bu nedenle kullanılır:

![Tüm kısıtlamaları karşılayan düşük sürümünü kullanarak Kuzen bağımlılıkları çözümleniyor](media/projectJson-dependency-7.png)

Bazı durumlarda, tüm sürüm gereksinimlerini karşılamak olası değil. Aşağıda gösterildiği gibi paketi A tam olarak paket B 1.0 gerektirir ve paket C gerektiriyorsa Paket B > NuGet bağımlılıklar çözümlenemiyor ve bir hata verir 2.0 =.

![Bir tam sürüm gereksinimini nedeniyle çözülemeyen bağımlılıkları](media/projectJson-dependency-8.png)

Bu durumlarda, üst düzey bir tüketici (uygulama veya Paketle) doğrudan bağımlılık Paket B eklemeniz gerekir böylece [yakın WINS](#nearest-wins) kuralı uygular.

## <a name="dependency-resolution-with-packagesconfig"></a>Packages.config bir bağımlılık çözümleme

İle `packages.config`, bir projenin bağımlılıkları yazılır `packages.config` düz bir liste olarak. Bu paket bağımlılıkları da aynı listesinde yazılır. NuGet paketleri yüklendiğinde, ayrıca değişiklik `.csproj` dosyası `app.config`, `web.config`ve tek tek diğer dosyaları.

İle `packages.config`, NuGet tek tek her paketin yüklenmesi sırasında bağımlılık çakışmaları dener. A paketi yükleniyor ve paket B ve paket B bağlıdır, diğer bir deyişle, zaten listede `packages.config` bir bağımlılık, başka bir NuGet paketi istenen B sürümlerini karşılaştırır ve tüm sürüm karşılayan bir sürümünü bulmaya çalışır kısıtlamaları. Özellikle, NuGet alt seçer *major.minor* bağımlılıkları karşılayan sürümü.

Varsayılan olarak, NuGet 2.7 ve önceki en yüksek çözümler *düzeltme eki* sürüm (kullanarak *major.minor.patch.build* kuralı). [NuGet 2.8 ve daha yüksek](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) için en düşük düzeltme eki sürümü varsayılan olarak aramak için bu davranış değişir. Bu ayarı kullanılarak denetleyebilirsiniz `DependencyVersion` özniteliğini `Nuget.Config` ve `-DependencyVersion` komut satırında geçin.  

`packages.config` Bağımlılıkları çözümleniyor büyük bağımlılık grafikleri için karmaşık alır için işlem. Her yeni paket yükleme tüm grafik çapraz geçişi gerektirir ve sürüm çakışmaları için Fırsat başlatır. Bir çakışma oluştuğunda, özellikle proje dosyasına olası değişiklikleri ile belirlenmemiş bir durum proje bırakarak yükleme durdurulur. Bu sorunu diğer paketi başvurusu biçimleri kullanırken değildir.


## <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

Kullanırken `project.json` veya PackageReference biçimleri, üst düzey proje bağımlılıkları akışına hangi varlıklarından kontrol edebilirsiniz. Ayrıntılar için bkz [project.json](../Schema/project-json.md) ve [paketini proje dosyalarını başvurularında](Package-References-in-Project-Files.md#controlling-dependency-assets).

Üst düzey proje kendisini bir paketi olduğunda, bu akış denetime kullanarak de `include` ve `exclude` listelenen bağımlılıkları özniteliklerle `.nuspec` dosya. Bkz: [.nuspec başvuru - bağımlılıkları](../Schema/nuspec.md#dependencies).

## <a name="excluding-references"></a>Başvuruları hariç

İçinde aynı ada sahip birden çok kez bir projede tasarım zamanı ve derleme zamanı hatalarını oluşturan başvurulan derlemeler senaryo vardır. Özel bir sürümünü içeren bir proje göz önünde bulundurun `C.dll`ve ayrıca içeren paket C başvurur `C.dll`. Aynı anda proje de aynı zamanda paket C bağlıdır Paket B bağlıdır ve `C.dll`. Sonuç olarak, NuGet hangi belirleyemiyor `C.dll` kullanmak için ancak Paket B de ona bağımlı olduğundan paket C projenin bağımlılığını yalnızca kaldıramazsınız.

Bu sorunu çözmek için doğrudan başvurmalıdır `C.dll` sizin (veya doğru olanı başvuran başka bir paket kullanmak) ve ardından bir bağımlılık paketi C tüm varlıklarını dışlar ekleyin. Bu paketi başvurusu biçime bağlı olarak şu şekilde gerçekleştirilir:

- [PackageReference](../consume-packages/package-references-in-project-files.md): eklemek `Exclude="All"` bağımlılık olarak:

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- `packages.config`: PackageC başvurusunu kaldırın `.csproj` yalnızca sürümüne başvuruyor dosyasını `C.dll` istediğiniz.
    
- `project.json`: eklemek `"exclude" : "all"` PackageC bağımlılığı içinde:

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

- İle [paketini proje dosyalarını başvurularında](../consume-packages/package-references-in-project-files.md) (NuGet 4.0 + yalnızca), ekleme `ExcludeAssets="All"` bağımlılık olarak:

    ```xml
    <PackageReference Include="packageC" Version="1.0.0" ExcludeAssets="All" />
    ```

## <a name="dependency-updates-during-package-install"></a>Paket sırasında bağımlılık güncelleştirmeleri yükle 

NuGet ile 2.4.x ve, bağımlılık projede zaten bir paketi yüklendiğinde, mevcut sürümü de bu kısıtlamalar uymazsa bile daha önce bağımlılık sürümü kısıtlamaları karşılayan en son sürümüne güncelleştirilir. 

Örneğin, paket B paketine bağlıdır ve 1.0 için sürüm numarasını belirtir A göz önünde bulundurun. Her iki sürümü 1.0, 1.1 ve 1.2 paketinin B. kaynak deposu içerir A B sürüm 1.0 zaten içeren projede yüklü ise B sürüm 1.2 güncelleştirilir. 

Bağımlılık sürümünü zaten sağlanıyorsa bağımlılık NuGet 2.5 ve daha sonra diğer paket yüklemeleri sırasında güncelleştirilmez. 

Aynı yukarıdaki örnekte, paket B 1.0 projesinde NuGet 2.5 ve daha sonraki bir projesine bırakır paketi yüklerken, olarak zaten sürüm kısıtlamasına. A paketi istekleri sürüm 1.1 veya üstü b olsaydı, ancak, ardından B 1.2 yüklenmesi. 

## <a name="resolving-incompatible-package-errors"></a>Uyumsuz paket hatalarını çözme

Geri yükleme işlemi sırasında bir paket, "bir veya daha fazla paket uyumlu olmadığında..." veya bir paketi "uyumlu değil" hata görebilirsiniz projenin hedef çerçevesi ile.

Bu hata, bir veya daha fazla projenizde başvurulan paketleri projenin hedef çerçevesini destekleyen göstermiyor oluşur; diğer bir deyişle, paketi uygun DLL'de içermiyor kendi `lib` proje ile uyumlu olan bir hedef çerçeve için klasör. (Bkz [hedef çerçeveler](../Schema/Target-Frameworks.md) bir listesi için.) 

Örneğin, bir proje hedefleri, `netstandard1.6` DLL'leri içinde yalnızca içeren bir paket yüklemeyi denerseniz `lib\net20` ve `\lib\net45` klasörleri olduktan sonra paketi ve muhtemelen, bağımlılıklar için aşağıdaki gibi iletileri göreceksiniz:

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

Uyumsuzlukları çözmek için şunlardan birini yapın:

- Kullanmak istediğiniz paketleri tarafından desteklenen bir çerçeve projenize yeniden hedefleyin.
- Paket yazarına başvurun ve onlarla seçilen framework desteği eklemek için çalışma. Üzerinde sayfa listeleme her paket [nuget.org](https://www.nuget.org/) sahip bir **kişi sahipleri** bu amaç için bağlantı.
- **Önerilmez**: geçici bir çözüm olarak için paket yazarına ile çalışırken projeleri hedefleyen `netcore`, `netstandard`, ve `netcoreapp` uyumlu, böylece bu hedefleme paketleri izin verme olarak diğer çerçeveler belirtmek kullanılacak diğer çerçeveler. Bkz: [project.json alır](../Schema/project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback). Bu beklenmeyen davranışları neden şekilde yeniden üzerinde bir güncelleştirme için paket yazarına ile çalışarak paket uyumsuzlukları gidermek en iyisidir.
