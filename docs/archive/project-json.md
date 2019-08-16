---
title: NuGet için Project. JSON dosya başvurusu
description: Bazı proje türlerinde, Project. JSON projede kullanılan NuGet paketlerinin listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488292"
---
# <a name="projectjson-reference"></a>Project. JSON başvurusu

*NuGet 3. x +*

`project.json` Dosya, bir projede kullanılan paketlerin bir listesini tutar ve paket yönetim biçimi olarak bilinir. Onun yerini `packages.config` alır ancak bu, NuGet 4.0 + ile [packagereference](../consume-packages/package-references-in-project-files.md) 'ın yerini almıştır.

Dosya (aşağıda açıklanmıştır), kullanan `project.json`projelerde de kullanılır. [`project.lock.json`](#projectlockjson)

`project.json`Aşağıdaki temel yapıya sahiptir ve burada dört üst düzey nesne herhangi bir sayıda alt nesneye sahip olabilir:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>Bağımlılıklar

Projenizin NuGet paketi bağımlılıklarını aşağıdaki biçimde listeler:

```json
"PackageID" : "version_constraint"
```

Örneğin:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

Bu `dependencies` bölüm, NuGet Paket Yöneticisi iletişim kutusunun projenize paket bağımlılıkları eklediği yerdir.

Paket kimliği, Paket Yöneticisi konsolunda kullanılan kimlikle aynı nuget.org üzerindeki paketin kimliğine karşılık gelir: `Install-Package Microsoft.NETCore`.

Paketleri geri yüklerken, öğesinin `"5.0.0"` sürüm kısıtlaması anlamına gelir. `>= 5.0.0` Diğer bir deyişle, 5.0.0 sunucuda kullanılabilir değilse ancak 5.0.1 ise NuGet, 5.0.1 ' yi yükleyip yükseltme hakkında sizi uyarır. NuGet, kısıtlama ile eşleşen sunucuda mümkün olan en düşük sürümü de seçer.

Çözüm kuralları hakkında daha fazla bilgi için bkz. [bağımlılık çözünürlüğü](../concepts/dependency-resolution.md) .

### <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

Bağımlılıklardan en üst düzey projeye akan varlıkların, `include` bağımlılık başvurusunun ve `exclude` özelliklerinde virgülle ayrılmış bir etiket kümesi belirtilerek denetlenir. Etiketler aşağıdaki tabloda listelenmiştir:

| Dahil etme/hariç tutma etiketi | Hedefin etkilenen klasörleri |
| --- | --- |
| contentFiles | İçerik  |
| çalışma zamanı | Çalışma zamanı, kaynaklar ve FrameworkAssemblies  |
| se | LIB |
| derleme | Build (MSBuild props ve targets) |
| yerel | yerel |
| yok | Klasör yok |
| tüm | Tüm klasörler |

İle belirtilen Etiketler `exclude` , ile `include`belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir. Örneğin, `include="runtime, compile" exclude="compile"` ile `include="runtime"`aynıdır.

Örneğin, bir bağımlılığın `build` ve `native` klasörlerinin dahil olması için aşağıdakileri kullanın:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Bir bağımlılığın `content` ve `build` klasörlerinin hariç tutulması için aşağıdakileri kullanın:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Çerçeveler

Projenin üzerinde çalıştığı çerçeveleri listeler, örneğin `net45` `netcoreapp` `netstandard`,,.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

`frameworks` Bölümünde yalnızca tek bir girdiye izin verilir. (Bir özel durum `project.json` , birden çok hedefe izin veren kullanım dışı DNX araç zinciri ile oluşturulan ASP.net projelerine yönelik dosyalardır.)

## <a name="runtimes"></a>Zamanları

Uygulamanızın üzerinde çalıştığı işletim sistemlerini ve mimarilerini listeler, örneğin `win10-arm` `win8-x64` `win8-x86`,,.

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Herhangi bir çalışma zamanı üzerinde çalışabilecek bir PCL içeren paketin çalışma zamanı belirtmesi gerekmez. Bu, herhangi bir bağımlılıkda doğru olmalıdır, aksi takdirde çalışma zamanlarını belirtmeniz gerekir.


## <a name="supports"></a>Desteklememektedir

Paket bağımlılıkları için bir denetim kümesi tanımlar. PCL veya uygulamayı hangi noktada çalıştıracağınızı belirtebilirsiniz. Kodunuzun başka bir yerde çalıştırılabilmesi için tanımlar kısıtlayıcı değildir. Ancak bu denetimlerin belirlenmesi, tüm bağımlılıkların listelenen TxMs üzerinde karşılanıp karşılanmadığını, NuGet denetimi yapar. Bunun değerlerine örnek olarak şunlar verilebilir: `net46.app`, `uwp.10.0.app`, vb.

Bu bölüm, taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir giriş seçtiğinizde otomatik olarak doldurulmalıdır.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>İşlemlerinin

İçeri aktarmalar, `dotnet` bir DotNet TXD bildirmeyin paketlerle çalışmak üzere TXD kullanan paketlere izin vermek için tasarlanmıştır. Projeniz `dotnet` TXI kullanıyorsa, `dotnet` platformların ile `project.json` `dotnet`uyumlu olmasını sağlamak için aşağıdaki öğesine eklemediğiniz sürece bağlı olduğunuz tüm `dotnet` paketler bir TXD içermelidir.

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

`dotnet` TXD 'yi kullanıyorsanız, PCL proje sistemi desteklenen hedeflere göre uygun `imports` ifadeyi ekler.

## <a name="differences-from-portable-apps-and-web-projects"></a>Taşınabilir uygulamalardan ve Web projelerinden farklılıklar

NuGet tarafından kullanılan dosya ASP.NET Core projelerinde bulunan bir alt kümesidir. `project.json` ASP.NET Core `project.json` , proje meta verileri, derleme bilgileri ve Bağımlılıklar için kullanılır. Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı dosyalara bölünür ve `project.json` daha az bilgi içerir. Önemli farklar şunlardır:

- `frameworks` Bölümde yalnızca bir çerçeve olabilir.

- Bu dosya DNX `project.json` dosyalarında gördüğünüz bağımlılıklar, derleme seçenekleri vb. içeremez. Yalnızca tek bir çerçeve olabilir. Bu, çerçeveye özgü bağımlılıklar girmek mantıklı değildir.

- Derleme MSBuild, derleme seçenekleri, Önişlemci tanımlar, vb., MSBuild proje dosyasının `project.json`tüm parçasıdır.

NuGet 3 + ' de, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi `project.json`içeriği yaparken geliştiricilerin el ile düzenlemesi beklenmez. Yani, dosyayı kesinlikle düzenleyebilirsiniz, ancak bir paket geri yüklemeyi başlatmak veya geri yüklemeyi başka bir şekilde çağırmak için projeyi derlemeniz gerekir. Bkz. [paket geri yükleme](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

Dosya, kullanan `project.json`projelerde NuGet paketlerini geri yükleme işleminde oluşturulur. `project.lock.json` NuGet olarak oluşturulan tüm bilgilerin bir anlık görüntüsünü tutar ve kuruluşunuzdaki tüm paketlerin sürümünü, içeriğini ve bağımlılıklarını içerir. Yapı sistemi, projenin kendisindeki yerel paketler klasörüne bağlı olmak yerine, projeyi oluştururken uygun olan küresel bir konumdan paket seçmek için bunu kullanır. Bu, çok sayıda ayrı `project.lock.json` `.nuspec` dosya yerine yalnızca okunması gerektiğinden daha hızlı derleme performansına neden olur.

`project.lock.json`paket geri yükleme sırasında otomatik olarak oluşturulur. bu nedenle, `.gitignore` ve `.tfignore` dosyalarına ekleyerek kaynak denetiminden atlanabilir (bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md). Ancak, kaynak denetimine eklerseniz, değişiklik geçmişi zaman içinde çözümlenen bağımlılıklarda yapılan değişiklikleri gösterir.
