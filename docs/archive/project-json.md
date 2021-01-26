---
title: NuGet için dosya başvurusunda project.js
description: Bazı proje türlerinde project.js, projede kullanılan NuGet paketlerinin listesini tutar.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775199"
---
# <a name="projectjson-reference"></a>Başvuruya project.js

*NuGet 3. x +*

`project.json`Dosya, bir projede kullanılan paketlerin bir listesini tutar ve paket yönetim biçimi olarak bilinir. Onun yerini alır `packages.config` ancak bu, NuGet 4.0 + Ile [packagereference](../consume-packages/package-references-in-project-files.md) 'ın yerini almıştır.

[`project.lock.json`](#projectlockjson)Dosya (aşağıda açıklanmıştır), kullanan projelerde de kullanılır `project.json` .

`project.json` Aşağıdaki temel yapıya sahiptir ve burada dört üst düzey nesne herhangi bir sayıda alt nesneye sahip olabilir:

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

Paket kimliği, Paket Yöneticisi konsolunda kullanılan kimlikle aynı nuget.org üzerindeki paketin kimliğine karşılık gelir: `Install-Package Microsoft.NETCore` .

Paketleri geri yüklerken, öğesinin sürüm kısıtlaması `"5.0.0"` anlamına gelir `>= 5.0.0` . Diğer bir deyişle, 5.0.0 sunucuda kullanılabilir değilse ancak 5.0.1 ise NuGet, 5.0.1 ' yi yükleyip yükseltme hakkında sizi uyarır. NuGet, kısıtlama ile eşleşen sunucuda mümkün olan en düşük sürümü de seçer.

Çözüm kuralları hakkında daha fazla bilgi için bkz. [bağımlılık çözünürlüğü](../concepts/dependency-resolution.md) .

### <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

Bağımlılıklardan en üst düzey projeye akan varlıkların, `include` bağımlılık başvurusunun ve özelliklerinde virgülle ayrılmış bir etiket kümesi belirtilerek denetlenir `exclude` . Etiketler aşağıdaki tabloda listelenmiştir:

| Dahil etme/hariç tutma etiketi | Hedefin etkilenen klasörleri |
| --- | --- |
| contentFiles | Content  |
| çalışma zamanı | Çalışma zamanı, kaynaklar ve FrameworkAssemblies  |
| derle | LIB |
| derleme | Build (MSBuild props ve targets) |
| yerel | yerel |
| yok | Klasör yok |
| tümü | Tüm klasörler |

İle belirtilen Etiketler `exclude` , ile belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir `include` . Örneğin, `include="runtime, compile" exclude="compile"` ile aynıdır `include="runtime"` .

Örneğin, `build` `native` bir bağımlılığın ve klasörlerinin dahil olması için aşağıdakileri kullanın:

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

`content`Bir bağımlılığın ve klasörlerinin hariç tutulması için `build` aşağıdakileri kullanın:

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

Projenin üzerinde çalıştığı çerçeveleri listeler, örneğin,, `net45` `netcoreapp` `netstandard` .

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Bölümünde yalnızca tek bir girdiye izin verilir `frameworks` . (Bir özel durum, `project.json` birden çok hedefe izin veren kullanım dışı DNX araç zinciri ile oluşturulan ASP.net projelerine yönelik dosyalardır.)

## <a name="runtimes"></a>Zamanları

Uygulamanızın üzerinde çalıştığı işletim sistemlerini ve mimarilerini listeler, örneğin,, `win10-arm` `win8-x64` `win8-x86` .

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


## <a name="supports"></a>Destekleyen

Paket bağımlılıkları için bir denetim kümesi tanımlar. PCL veya uygulamayı hangi noktada çalıştıracağınızı belirtebilirsiniz. Kodunuzun başka bir yerde çalıştırılabilmesi için tanımlar kısıtlayıcı değildir. Ancak bu denetimlerin belirlenmesi, tüm bağımlılıkların listelenen TxMs üzerinde karşılanıp karşılanmadığını, NuGet denetimi yapar. Bunun değerlerine örnek olarak şunlar verilebilir: `net46.app` , `uwp.10.0.app` , vb.

Bu bölüm, taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir giriş seçtiğinizde otomatik olarak doldurulmalıdır.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>İşlemlerinin

İçeri aktarmalar, `dotnet` bir DotNet TXD bildirmeyin paketlerle çalışmak üzere TXD kullanan paketlere izin vermek için tasarlanmıştır. Projeniz `dotnet` TXI kullanıyorsa, `dotnet` `project.json` `dotnet` platformların ile uyumlu olmasını sağlamak için aşağıdaki öğesine eklemediğiniz sürece bağlı olduğunuz tüm paketler bir TXD içermelidir `dotnet` .

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

`dotnet`TXD 'yi kullanıyorsanız, PCL proje sistemi `imports` desteklenen hedeflere göre uygun ifadeyi ekler.

## <a name="differences-from-portable-apps-and-web-projects"></a>Taşınabilir uygulamalardan ve Web projelerinden farklılıklar

`project.json`NuGet tarafından kullanılan dosya ASP.NET Core projelerinde bulunan bir alt kümesidir. ASP.NET Core, `project.json` proje meta verileri, derleme bilgileri ve Bağımlılıklar için kullanılır. Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı dosyalara bölünür ve `project.json` daha az bilgi içerir. Önemli farklar şunlardır:

- Bölümde yalnızca bir çerçeve olabilir `frameworks` .

- Bu dosya DNX dosyalarında gördüğünüz bağımlılıklar, derleme seçenekleri vb. içeremez. `project.json` Yalnızca tek bir çerçeve olabilir. Bu, çerçeveye özgü bağımlılıklar girmek mantıklı değildir.

- Derleme MSBuild, derleme seçenekleri, Önişlemci tanımlar, vb., MSBuild proje dosyasının tüm parçasıdır `project.json` .

NuGet 3 + ' de, `project.json` Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi içeriği yaparken geliştiricilerin el ile düzenlemesi beklenmez. Yani, dosyayı kesinlikle düzenleyebilirsiniz, ancak bir paket geri yüklemeyi başlatmak veya geri yüklemeyi başka bir şekilde çağırmak için projeyi derlemeniz gerekir. Bkz. [paket geri yükleme](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>Üzerinde project.lock.js

`project.lock.json`Dosya, kullanan projelerde NuGet paketlerini geri yükleme işleminde oluşturulur `project.json` . NuGet olarak oluşturulan tüm bilgilerin bir anlık görüntüsünü tutar ve kuruluşunuzdaki tüm paketlerin sürümünü, içeriğini ve bağımlılıklarını içerir. Yapı sistemi, projenin kendisindeki yerel paketler klasörüne bağlı olmak yerine, projeyi oluştururken uygun olan küresel bir konumdan paket seçmek için bunu kullanır. Bu `project.lock.json` , çok sayıda ayrı dosya yerine yalnızca okunması gerektiğinden daha hızlı derleme performansına neden olur `.nuspec` .

`project.lock.json` paket geri yükleme sırasında otomatik olarak oluşturulur. bu nedenle, ve dosyalarına ekleyerek kaynak denetiminden atlanabilir `.gitignore` `.tfignore` (bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md). Ancak, kaynak denetimine eklerseniz, değişiklik geçmişi zaman içinde çözümlenen bağımlılıklarda yapılan değişiklikleri gösterir.
