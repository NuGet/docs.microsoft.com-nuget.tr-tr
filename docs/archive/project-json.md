---
title: NuGet için Project.JSON dosyası başvurusu
description: Bazı proje türlerinde project.json projede kullanılan NuGet paketleri listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547790"
---
# <a name="projectjson-reference"></a>Project.JSON başvurusu

*NuGet 3.x+*

`project.json` Dosyası bir paket Yönetimi biçimi olarak bilinen, bir projede kullanılan paketler listesini tutar. Sürümlereni `packages.config` sırayla yerine geçen ancak [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + ile.

[ `project.lock.json` ](#projectlockjson) (Aşağıda açıklanmıştır) dosyası da kullanan projelerinde kullanılan `project.json`.

`project.json` aşağıdaki temel yapısını dört üst düzey nesnelerin her biri herhangi bir sayıda alt nesneler burada sahip sahiptir:

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

## <a name="dependencies"></a>Bağımlılıkları

NuGet Paket bağımlılıklarını projenizin aşağıdaki biçimde listeler:

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

`dependencies` Bölümdür burada NuGet Paket Yöneticisi iletişim paket bağımlılıkları projenize ekler.

Nuget.org, Paket Yöneticisi Konsolu'nda kullanılan kimliği ile aynı paket kimliği için paket kimliği karşılık gelir: `Install-Package Microsoft.NETCore`.

Ne zaman geri yükleme paketleri sürüm kısıtlamasını `"5.0.0"` gelir `>= 5.0.0`. Diğer bir deyişle, sunucuda 5.0.0 kullanılamıyor, ancak 5.0.1 olduğundan, NuGet 5.0.1 yükler ve yükseltme hakkında sizi uyarır. NuGet, aksi takdirde olası en düşük sürüm kısıtlaması eşleşen sunucuda seçer.

Bkz: [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md) çözümleme kuralları hakkında daha fazla ayrıntı için.

### <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

Hangi bağımlılıklar varlıklarından en üst düzey projeye akış etiketleri virgülle ayrılmış bir dizi belirterek denetlenir `include` ve `exclude` bağımlılık başvurusu özellikleri. Etiketleri listelenen aşağıdaki tabloda:

| Etiket Ekle/Dışla | Etkilenen hedef klasör |
| --- | --- |
| contentFiles | İçerik  |
| çalışma zamanı | Çalışma zamanı, kaynaklar ve FrameworkAssemblies  |
| Derleme | lib |
| derleme | derleme (MSBuild özellikler ve hedefler) |
| yerel | yerel |
| yok | Klasör yok |
| tüm | Tüm klasörler |

İle belirtilen etiketlere `exclude` ile belirtilenler üzerinde önceliklidir `include`. Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.

Örneğin, dahil etmek için `build` ve `native` klasörleri, bağımlılık aşağıdakileri kullanın:

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

Dışlanacak `content` ve `build` klasörleri, bağımlılık aşağıdakileri kullanın:

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

Listeler gibi proje üzerinde çalıştığı çerçeveleri `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Yalnızca tek bir giriş izin `frameworks` bölümü. (Bir özel durum `project.json` dosyaları derleme kullanım dışı DNX ile olan ASP.NET projeleri için araç için birden çok hedef sağlayan zinciri.)

## <a name="runtimes"></a>Çalışma zamanları

Gibi uygulamanızın üzerinde çalıştığı işletim sistemleri ve mimariler listeler `win10-arm`, `win8-x64`, `win8-x86`.

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

Herhangi bir çalışma zamanı üzerinde çalışabilen bir PCL içeren bir paket, bir çalışma zamanı belirtmeniz gerekmez. Bu ayrıca herhangi bir bağımlılığın true olmalıdır, aksi takdirde, çalışma zamanları belirtmeniz gerekir.


## <a name="supports"></a>Destekler

Paket bağımlılıkları için denetimleri kümesini tanımlar. Burada, PCL veya uygulamanın çalışmasını beklediğiniz tanımlayabilirsiniz. Tanımları kısıtlayıcı olmayan kod başka bir yerde çalıştırmak mümkün olabilir. Ancak bu denetimleri belirten tüm bağımlılıklar üzerinde listelenen TxMs karşılanır denetleyin NuGet yapar. Örnek değerler için bu şunlardır: `net46.app`, `uwp.10.0.app`vb.

Bu bölümde, taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir girişi seçtiğinizde otomatik olarak doldurulur.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>İçeri aktarmalar

İçeri aktarmalar kullanan paketleri izin verecek şekilde tasarlanmıştır `dotnet` TxM bir dotnet TxM bildirmeyin paketlerle çalışılacak. Projenizi kullanıyorsa `dotnet` TxM sonra bağlı olduğu tüm paketleri ayrıca olmalıdır bir `dotnet` TxM, aşağıdaki eklemediğiniz sürece, `project.json` olmayan izin vermek için `dotnet` platformları ile uyumlu olacak şekilde `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Kullanıyorsanız `dotnet` TxM ardından PCL proje sistemi ekler uygun `imports` tabanlı desteklenen hedeflerde bildirimi.

## <a name="differences-from-portable-apps-and-web-projects"></a>Taşınabilir uygulamaları ve web projeleri arasındaki farklar

`project.json` NuGet tarafından kullanılan dosya, ASP.NET Core projelerinde bulunan özelliklerinin bir alt kümesidir. ASP.NET core'da `project.json` proje meta verileri, derleme bilgilerini ve bağımlılıklar için kullanılır. Diğer proje sistemleri kullanıldığında, bu üç şey ayrı dosyalar halinde bölme ve `project.json` daha az bilgi içerir. Önemli farklar şunlardır:

- Ayrıca bir framework yalnızca olabilir `frameworks` bölümü.

- Dosya içeremez bağımlılıkları, derleme seçenekleri vb. DNX içinde gördüğünüz `project.json` dosyaları. Yalnızca olabilir koşuluyla, tek bir çerçeve bu çerçeveye özgü bağımlılıkları girmek için anlam ifade etmez.

- Derleme tarafından işlenir derleme seçenekleri, önişlemci tanımlar için MSBuild, vb. tüm MSBuild proje dosyası parçası olan ve olmayan `project.json`.

Nuget'te 3 +, geliştiricilerin el ile düzenlemek için beklenmiyor `project.json`gibi Visual Studio'da Paket Yöneticisi UI içeriği yönetir. Bu, dosyanın kesinlikle düzenleyebilirsiniz; ama bir paket geri yüklemeyi başlatmak veya başka bir şekilde geri çağırma için projeyi oluşturmalısınız da belirtti. Bkz: [paket geri yükleme](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` Kullanılan projelerde NuGet paketlerini geri yükleme işleminde dosya oluşturulduğunda `project.json`. Bu bir anlık görüntüsünü NuGet paketleri grafiği size yol gösterir ve projenizde sürüm, içeriği ve Paket bağımlılıklarını içerir oluşturulan tüm bilgileri içerir. Derleme sistemi, bu paket yerine projeyi yerel paketleri klasöründe bağlı olarak projeyi derlerken ilgili genel bir konum seçmek için kullanır. Salt okunur olarak gerekli olduğundan bu daha hızlı derleme performansla sonuçlanır `project.lock.json` birçok yerine ayrı `.nuspec` dosyaları.

`project.lock.json` kaynak denetiminden bu atlanabilir ekleyerek için paket geri yükleme, otomatik olarak oluşturulan `.gitignore` ve `.tfignore` dosyaları (bkz [paketleri ve kaynak denetimi](../consume-packages/packages-and-source-control.md). Kaynak denetimine dahil, ancak zaman içinde çözümlenen bağımlılıklar değişiklikleri değişiklik geçmişini gösterir.
