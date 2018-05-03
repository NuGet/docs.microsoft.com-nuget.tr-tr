---
title: NuGet için'Project.JSON dosyası başvurusu
description: Bazı proje türleri project.json projesinde kullanılan NuGet paketleri listesini tutar.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 52df5c6a4d5f1c0092a85c124903203da83a1821
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="projectjson-reference"></a>Project.JSON başvurusu

*NuGet 3.x+*

`project.json` Dosyası paket Yönetimi biçimi bilinen bir projesinde kullanılan paketlerin listesini sağlar. Bu yerine geçiyor `packages.config` sırayla yerine geçen ancak [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + ile.

[ `project.lock.json` ](#projectlockjson) (Aşağıda açıklanmıştır) dosyası da kullanan projelerinde kullanılan `project.json`.

`project.json` aşağıdaki temel yapı dört en üst düzey nesnelerin her biri herhangi bir sayıda bağımlı nesnelere sahip olduğu sahiptir:

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

Aşağıdaki biçimde projenizin NuGet paket bağımlılıkları listeler:

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

`dependencies` Bölümdür nerede NuGet Paket Yöneticisi iletişim Paket bağımlılıklarını projenize ekler.

Paket Yöneticisi Konsolu'nda kullanılan kimliği ile aynı nuget.org paket kimliği için paket kimliğine karşılık gelen: `Install-Package Microsoft.NETCore`.

Ne zaman geri yükleme paketleri, sürüm kısıtlaması `"5.0.0"` gelir `>= 5.0.0`. Diğer bir deyişle, 5.0.0 sunucuda kullanılamıyor 5.0.1 varsa, NuGet 5.0.1 yükler ve yükseltme hakkında sizi uyarır. Aksi takdirde NuGet olası en düşük sürüm kısıtlaması eşleşen sunucuda seçer.

Bkz: [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md) çözümleme kuralları hakkında daha fazla ayrıntı için.

### <a name="managing-dependency-assets"></a>Bağımlılık varlıklarını yönetme

Bağımlılıklar hangi varlıklarından en üst düzey projeye akış etiketlerinde virgülle ayrılmış bir dizi belirterek denetlenir `include` ve `exclude` bağımlılık başvurusu özelliklerini. Etiketler listelenen aşağıdaki tabloda:

| Etiket dahil etme/hariç tutma | Hedef etkilenen klasörler |
| --- | --- |
| Content dosyaları | İçerik  |
| çalışma zamanı | Çalışma zamanı, kaynakları ve FrameworkAssemblies  |
| Derleme | LIB |
| derleme | derleme (MSBuild özellik ve hedefleri) |
| yerel | yerel |
| yok | Klasör yok |
| tüm | Tüm klasörleri |

İle belirtilen etiketleri `exclude` ile belirtilen önceliklidir `include`. Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.

Örneğin, dahil etmek için `build` ve `native` bir bağımlılık klasörleri aşağıdakileri kullanın:

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

Dışlanacak `content` ve `build` bir bağımlılık klasörleri aşağıdakileri kullanın:

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

## <a name="frameworks"></a>çerçeveler

Proje gibi çalışan çerçeveleri listeler `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Yalnızca tek bir giriş izin `frameworks` bölümü. (Bir özel durum `project.json` dosyaları yapı kullanım dışı DNX ile olan ASP.NET projeleri için araç için birden çok hedef verir zinciri.)

## <a name="runtimes"></a>Çalışma zamanları

Uygulamanızı gibi çalışan işletim sistemleri ve mimariler listeler `win10-arm`, `win8-x64`, `win8-x86`.

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

Tüm çalışma zamanı çalıştırabilirsiniz PCL içeren bir paket, bir çalışma zamanı belirtmek gerekmez. Bu ayrıca tüm bağımlılıkları true olmalıdır, aksi halde, çalışma zamanları belirtmeniz gerekir.


## <a name="supports"></a>Destekler

Paket bağımlılıklarını denetimleri kümesini tanımlar. Burada, PCL veya çalıştırmak için uygulamayı beklediğiniz tanımlayabilirsiniz. Kodunuz başka bir yerde çalıştırabilir gibi tanımları kısıtlayıcı değildir. Ancak bu denetimlerin belirterek tüm üzerinde listelenen TxMs bağımlılıkların denetleyin NuGet yapar. Bu öğeler için değeri örnekleri: `net46.app`, `uwp.10.0.app`vb.

Taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir giriş seçtiğinizde bu bölümde otomatik olarak doldurulması gerekir.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>İçeri aktarmalar

İçeri aktarmalar kullanmak paketleri izin verecek şekilde tasarlanmıştır `dotnet` dotnet TxM bildirmeyin paketlerle çalışmak üzere TxM. Projenizi kullanıyorsanız `dotnet` TxM sonra bağımlı olan tüm paketleri ayrıca olmalıdır bir `dotnet` TxM, aşağıdaki eklemedikçe, `project.json` olmayan izin vermek için `dotnet` ile uyumlu olacak şekilde platformları `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Kullanıyorsanız `dotnet` TxM sonra PCL proje sistemi ekler uygun `imports` tabanlı desteklenen hedeflerde bildirimi.

## <a name="differences-from-portable-apps-and-web-projects"></a>Taşınabilir uygulamaları ve web projeleri arasındaki farklar

`project.json` NuGet tarafından kullanılan bir alt kümesini ASP.NET Core projelerinde bulunan dosyasıdır. ASP.NET Core içinde `project.json` proje meta veriler, derleme bilgilerini ve bağımlılıklar için kullanılır. Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı dosyalara ayrılır ve `project.json` daha az bilgi içerir. Önemli farklılıklar şunlardır:

- Ayrıca bir Framework'te yalnızca olabilir `frameworks` bölümü.

- Dosya içeremez bağımlılıkları, derleme seçenekleri, DNX içinde gördüğünüz vb. `project.json` dosyaları. Yalnızca tek bir çerçeve o çerçeveye özel bağımlılıkları girmek için doesn't make Sense.

- Derleme tarafından işlenir derleme seçenekleri, önişlemci tanımlar için MSBuild, vb. MSBuild proje dosyası tüm parçası olan ve olmayan `project.json`.

NuGet içinde 3 +, geliştiricilerin el ile düzenleme beklenmez `project.json`Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi içeriği yöneten gibi. Bu, kesinlikle dosyasını düzenleyebilir, ancak paket geri yüklemeyi başlatmak veya başka bir şekilde geri çağırma projeyi derleme da belirtti. Bkz: [paket geri yüklemesi](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` Dosyası kullanmak projelerinde NuGet paketleri geri yüklemeyi sürdürüyor oluşturulur `project.json`. Bir anlık görüntü olarak NuGet paketleri grafik anlatılmaktadır ve sürüm, içeriği ve tüm paketler bağımlılıklarını projenizde içerir oluşturan tüm bilgileri içerir. Derleme sistemi bu paketleri yerine Proje proje yerel paketler klasöründe bağlı olarak oluştururken ilgili genel bir konum seçmek için kullanır. Salt okunur gerekli olduğundan bu daha hızlı derleme performansla sonuçlanır `project.lock.json` birçok yerine ayrı `.nuspec` dosyaları.

`project.lock.json` kaynak denetiminden onu atlanabilir ekleyerek için paket geri yükleme, otomatik olarak oluşturulan `.gitignore` ve `.tfignore` dosyaları (bkz [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md). Ancak, kaynak denetiminde dahil, zaman içinde çözümlenen bağımlılıklar değişiklikleri değişiklik geçmişini gösterir.
