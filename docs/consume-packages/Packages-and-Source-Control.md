---
title: NuGet Paketleri ve Kaynak Kontrolü
description: Sürüm kontrol ve kaynak kontrol sistemleri içinde NuGet paketlerinin nasıl tedavi edilecek ve git ve TFVC ile paketleri nasıl atlatırsınız hakkında dikkat edilmesi gerekenler.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9d9ea10ccd32bb65ad0d62b591f5e2cb58ea3427
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69019987"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Kaynak kontrol sistemlerinde NuGet paketlerini atlayarak

Geliştiriciler genellikle NuGet paketlerini kaynak denetim depolarından atlar ve bunun yerine bir projenin bağımlılıklarını oluşturmadan önce yeniden yüklemek için [paket geri yüklemesine](package-restore.md) güvenirler.

Paket geri yüklemeye güvenmenedenleri şunlardır:

1. Git gibi dağıtılmış sürüm kontrol sistemleri, depodaki her dosyanın her sürümünün tam kopyalarını içerir. Sık sık güncelleştirilen ikili dosyalar önemli şişkinliğe yol açar ve depoyu klonlamak için gereken süreyi uzatır.
1. Paketler depoya dahil edildiğinde, geliştiriciler projede sabit kodlanmış yol adlarına yol açabilecek NuGet aracılığıyla paketlere başvurmak yerine doğrudan diskteki paket içeriğine referans eklemekle yükümlüdürler.
1. Hala kullanılmakta olan paket klasörlerini silmediğinizden emin olmanız gerektiğinden, çözümünüzü kullanılmayan paket klasörlerinden temizlemek zorlaşır.
1. Paketleri atlayarak, kodunuz la bağlı olduğunuz diğer paketler arasındaki sahiplik sınırlarını korursunuz. Birçok NuGet paketi zaten kendi kaynak denetim depolarında muhafaza edilir.

Paket geri yükleme NuGet ile varsayılan davranış olmasına rağmen, bu&mdash;makalede `packages` açıklandığı gibi,&mdash;yani, kaynak denetiminden projenizdeki klasörü atlamak için bazı el ile çalışma gereklidir.

## <a name="omitting-packages-with-git"></a>Git ile paketleri atlayarak

NuGet paketlerini (`.nupkg`) klasörü ve `packages` `project.assets.json`diğer şeylerin yanı sıra yoksaymak için [.gitignore dosyasını](https://git-scm.com/docs/gitignore) kullanın. Referans için Visual [ `.gitignore` Studio projeleri için örneğe](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)bakın:

Dosyanın `.gitignore` önemli bölümleri şunlardır:

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Team Foundation Sürüm Kontrolü ile paketleri atlayarak

> [!Note]
> Projenizi kaynak denetimine eklemeden *önce* mümkünse bu yönergeleri izleyin. Aksi takdirde, klasörü `packages` deponuzdan el ile silin ve devam etmeden önce bu değişikliği iade edin.

Seçili dosyalar için Kaynak Denetimi tümleştirmesini TFVC ile devre dışı kalmak için:

1. Çözüm klasörünüzde (dosyanın `.nuget` `.sln` olduğu yerde) adlandırılan bir klasör oluşturun.
    - İpucu: Windows'da, Windows Gezgini'nde bu `.nuget.` klasörü oluşturmak için, sondaki *noktaile* adı kullanın.

1. Bu klasörde, adlı `NuGet.Config` bir dosya oluşturun ve düzenleme için açın.

1. Devre [dışı kalanSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ayarı Visual Studio'ya `packages` klasördeki her şeyi atlamasını söylediği aşağıdaki metni minimum olarak ekleyin:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. TFS 2010 veya daha erken kullanıyorsanız, çalışma alanı eşlemelerinizde klasörü `packages` göşeyin.

1. TFS 2012 veya sonraki veya Visual Studio Team `.tfignore` Services [ile, Sunucuya Dosya Ekle'de](/vsts/tfvc/add-files-server?view=vsts#tfignore)açıklandığı gibi bir dosya oluşturun. Bu dosyada, depo düzeyinde `\packages` klasörde yapılan değişiklikleri ve birkaç diğer ara dosyaları açıkça yok saymak için aşağıdaki içeriği ekleyin. (Dosyayı Windows Gezgini'nde a `.tfignore.` adını kullanarak oluşturabilirsiniz, ancak önce "Bilinen dosya uzantılarını gizle" seçeneğini devre dışı bırakabilirsiniz.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Kaynak `NuGet.Config` `.tfignore` denetimi ne ekler ve değişikliklere iade edin.
