---
title: nuget için project.json Dosya Başvurusu
description: Bazı proje türlerinde project.json, projede kullanılan NuGet paketlerinin listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488292"
---
# <a name="projectjson-reference"></a>project.json referans

*NuGet 3.x+*

Dosya, `project.json` paket yönetim biçimi olarak bilinen projede kullanılan paketlerin listesini tutar. Bu yerini `packages.config` alır ama sırayla NuGet 4.0 + ile [PackageReference](../consume-packages/package-references-in-project-files.md) tarafından yerini alır.

Dosya [`project.lock.json`](#projectlockjson) (aşağıda açıklanan) aynı zamanda istihdam `project.json`projelerde kullanılır.

`project.json`dört üst düzey nesnenin her birinin herhangi bir sayıda alt nesneye sahip olabileceği aşağıdaki temel yapıya sahiptir:

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

Projenizin NuGet paket bağımlılıklarını aşağıdaki şekilde listeler:

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

Bu `dependencies` bölüm, NuGet Paket Yöneticisi iletişim kutusunun projenize paket bağımlılıkları eklediği bölümdür.

Paket numarası, paket yöneticisi konsolunda kullanılan id ile aynı olan nuget.org üzerindeki `Install-Package Microsoft.NETCore`paketin kimliğine karşılık gelir: .

Paketleri geri alırken, sürüm `"5.0.0"` kısıtlaması `>= 5.0.0`ima eder. Yani, 5.0.0 sunucuda kullanılamıyorsa ancak 5.0.1 ise, NuGet 5.0.1 yükler ve yükseltme hakkında sizi uyarır. NuGet aksi takdirde kısıtlama eşleşen sunucuda mümkün olan en düşük sürümü seçer.

Çözüm kuralları hakkında daha fazla ayrıntı için Bağımlılık çözümlemesi'ne bakın. [Dependency resolution](../concepts/dependency-resolution.md)

### <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

Bağımlılıklardan hangi varlıkların üst düzey projeye aktığı, bağımlılık başvurusu ve `include` `exclude` özelliklerinde virgülle sınırlandırılmış etiketler kümesi belirtilerek denetlenir. Etiketler aşağıdaki tabloda listelenmiştir:

| Etiketi ekle/hariç tut | Hedefin etkilenen klasörleri |
| --- | --- |
| içerikDosyalar | İçerik  |
| çalışma zamanı | Çalışma Zamanı, Kaynaklar ve FrameworkAssemblies  |
| derle | Lib |
| derleme | yapı (MSBuild sahne ve hedefleri) |
| yerel | yerel |
| yok | Klasör yok |
| tümü | Tüm klasörler |

'ile `exclude` belirtilenlerden önce gelen `include`etiketler. Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.

Örneğin, bir `build` bağımlılığın `native` klasörlerini ve klasörlerini eklemek için aşağıdakileri kullanın:

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

Bir `content` bağımlılığın `build` ve klasörlerini hariç tutmak için aşağıdakileri kullanın:

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

## <a name="frameworks"></a>Framework’ler

Projenin üzerinde çalıştığı çerçeveleri listeler, `net45`örneğin `netcoreapp` `netstandard`, , .

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Bölümde yalnızca tek bir `frameworks` girişe izin verilir. (Bir istisna, birden çok hedefe izin veren, amortismana uygun DNX takım zinciriyle oluşturulan ASP.NET projeler için `project.json` dosyalardır.)

## <a name="runtimes"></a>Çalıştırma

Uygulamanızın çalıştığı işletim sistemlerini ve mimarileri listeler, `win8-x64` `win8-x86`örneğin `win10-arm`, .

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

Herhangi bir çalışma zamanında çalıştırılabilen bir PCL içeren paketin çalışma zamanı belirtmesi gerekmez. Bu, tüm bağımlılıklar için de geçerli olmalıdır, aksi takdirde çalışma sürelerini belirtmeniz gerekir.


## <a name="supports"></a>Destekleyen

Paket bağımlılıkları için bir denetim kümesi tanımlar. PCL veya uygulamanın nerede çalışmasını beklediğiniz tanımlayabilirsiniz. Kodunuz başka bir yerde çalıştırılabildiği için tanımlar kısıtlayıcı değildir. Ancak bu denetimleri belirtmek NuGet'in listelenen TxM'lerde tüm bağımlılıkların karşıdan olduğunu denetlemesini sağlar. Bunun için değerlere örnek `net46.app` `uwp.10.0.app`olarak şunlar verilebilir: , , vb.

Taşınabilir Sınıf Kitaplığı hedef iletişim kutusunda bir giriş seçtiğinizde bu bölüm otomatik olarak doldurulmalıdır.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Ithalat

İçe alma, TxM `dotnet` kullanan paketlerin dotnet TxM beyan etmeyen paketlerle çalışmasına izin verecek şekilde tasarlanmıştır. `dotnet` Projeniz TxM kullanıyorsa, bağlı olduğunuz tüm paketlerin `dotnet` de bir TxM'si `project.json` olmalıdır, `dotnet` eğer aşağıdakileri `dotnet`eklemediğiniz sürece platformların aşağıdakilerle uyumlu olmasını sağlarsınız:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

TxM kullanıyorsanız, `dotnet` PCL proje sistemi desteklenen `imports` hedeflere göre uygun ifadeyi ekler.

## <a name="differences-from-portable-apps-and-web-projects"></a>Taşınabilir uygulamalardan ve web projelerinden farklar

NuGet tarafından kullanılan `project.json` dosya, ASP.NET Core projelerinde bulunan bir alt kümesidir. ASP.NET Core `project.json` proje meta verileri, derleme bilgileri ve bağımlılıkları için kullanılır. Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı `project.json` dosyalara ayrılır ve daha az bilgi içerir. Önemli farklılıklar şunlardır:

- `frameworks` Bölümde yalnızca bir çerçeve olabilir.

- Dosya, DNX `project.json` dosyalarında gördüğünüz bağımlılıkları, derleme seçeneklerini vb. içeremez. Sadece tek bir çerçeve olabileceği göz önüne alındığında, çerçeveye özgü bağımlılıkları girmek mantıklı değildir.

- Derleme MSBuild tarafından bu nedenle derleme seçenekleri, önişlemci tanımlar, vb MSBuild proje dosyasının bir parçasıdır ve `project.json`.

NuGet 3+'ta, Visual Studio'daki Paket `project.json`Yöneticisi Kullanıcı UI içeriği manipüle ettiği için geliştiricilerin el ile düzenlemesi beklenmez. Bununla birlikte, dosyayı kesinlikle düzenleyebilirsiniz, ancak bir paket geri yüklemebaşlatmak veya başka bir şekilde geri yükleme çağırmak için projeyi oluşturmanız gerekir. Bkz. [Paket geri yükleme.](../consume-packages/package-restore.md)


## <a name="projectlockjson"></a>project.lock.json

Dosya, `project.lock.json` nuget paketlerini kullanan `project.json`projelerde geri alma işleminde oluşturulur. NuGet paketlerin grafiğinde yürürken oluşturulan tüm bilgilerin anlık görüntüsünü tutar ve projenizdeki tüm paketlerin sürümünü, içeriğini ve bağımlılıklarını içerir. Yapı sistemi, projenin kendisindeki yerel paketler klasörüne bağlı kalmak yerine projeyi oluştururken ilgili olan genel bir konumdan paketleri seçmek için bunu kullanır. Bu, birçok ayrı `project.lock.json` `.nuspec` dosya yerine yalnızca okumak gerektiğinden daha hızlı yapı performansı sağlar.

`project.lock.json`paket geri yüklemesi otomatik olarak oluşturulur, böylece kaynak denetiminden `.gitignore` ekleyip `.tfignore` dosyalara eklenebilir (bkz. [Paketler ve kaynak denetimi.](../consume-packages/packages-and-source-control.md) Ancak, kaynak denetimine eklerseniz, değişiklik geçmişi zaman içinde çözülen bağımlılıkdeğişiklikleri gösterir.
