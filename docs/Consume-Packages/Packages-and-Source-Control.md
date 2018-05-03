---
title: NuGet paketleri ve kaynak denetimi
description: Sürüm denetimi ve kaynak denetim sistemleri içindeki NuGet paketleri kabul etme ve git ve TFVC'yi paketlerle atlayın durumları.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 5a36b886c3de1943b99b10faff63f4e244166ceb
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Kaynak Denetim sistemleri NuGet paketlerini atlama

Geliştiriciler genellikle kendi kaynak denetimi depoları NuGet paketleri atlayın ve bunun yerine Bel [paket geri yükleme](package-restore.md) bir yapı önce bir proje bağımlılıklarınızı yeniden yüklemek için.

Paket geri yükleme bağlı nedenleri şunlardır:

1. Git gibi dağıtılmış sürüm denetim sistemleri her sürüm deposu içinde her dosyanın tam kopyalarını içerir. Sık sık güncelleştirilen ikili dosyaları için önemli oluşan şişirmeyi sağlama ve depoyu kopyalayın süresini düşey çizgi ise uzar.
1. Paketleri depoya eklendiğinde, geliştiricilerin, doğrudan paket içeriğini başvuru paketler sabit kodlanmış yol adları projesinde açabilir NuGet aracılığıyla yerine disk eklemek zararlardan önerilir.
1. Paket klasörleri hala kullanımda silmeyin emin olmak gereksinim duyduğunuz çözümünüzün herhangi kullanılmayan paket klasörlerinin temiz zor olur.
1. Paketleri kaldırarak sahipliği temiz sınırlarının kodunuzu, bağlı diğer paketleri arasındaki korur. Birçok NuGet paketleri kendi kaynak denetimi depoları zaten saklanır.

Paket geri yüklemesi varsayılan davranışı NuGet ile el ile bazı iş paketleri atlamak gerekli olsa da&mdash;öğesine, `packages` projenizdeki klasöre&mdash;kaynak denetiminden bu makalede anlatıldığı gibi.

## <a name="omitting-packages-with-git"></a>Git paketlerle atlama

Kullanım [.gitignore dosyası](https://git-scm.com/docs/gitignore) NuGet paketlerini yoksaymak için (`.nupkg`) `packages` klasörünü ve `project.assets.json`, başka şeylerin. Başvuru için bkz: [örnek `.gitignore` Visual Studio projeleri için](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Önemli kısımlarını `.gitignore` dosyası:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Team Foundation sürüm denetimi paketlerle atlama

> [!Note]
> Bu yönergeleri mümkünse *önce* projenizi kaynak denetimine ekleme. Aksi takdirde, el ile silmeniz `packages` klasöründen depo ve devam etmeden önce bu değişikliği denetleyin.

Seçili dosyaları için TFVC'yi kaynak denetimi tümleştirmesi devre dışı bırakmak için:

1. Adlı bir klasör oluşturun `.nuget` çözüm klasördeki (burada `.sln` dosyası).
    - İpucu: Kullanın adı, Windows bu klasörü Windows Gezgini'nde oluşturmak için `.nuget.` *ile* sondaki noktayı.

1. Bu klasörde adlı bir dosya oluşturun `NuGet.Config` ve düzenlemek için açın.

1. Minimum olarak aşağıdaki metni ekleyin nerede [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ayarı bildirir her şeyi atlamak için Visual Studio `packages` klasörü:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. TFS 2010 veya önceki bir sürümünü kullanıyorsanız, gizlemek `packages` çalışma eşlemelerinizin klasöründe.

1. TFS 2012 veya sonraki sürümünü veya Visual Studio Team Services ile oluşturma bir `.tfignore` dosya açıklandığı gibi [AddFiles sunucuya](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore). Bu dosyada yapılan değişiklikler açıkça yoksaymak için aşağıdaki içerik `\packages` depo düzeyi ve diğer birkaç Ara dosyaları klasörü. (Dosya adını kullanarak Windows Gezgini'nde oluşturabileceğiniz bir `.tfignore.` sondaki noktayı, ancak ile devre dışı bırakmak için "Bilinen dosya uzantılarını gizle" ilk seçenek.):

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Ekleme `NuGet.Config` ve `.tfignore` kaynak denetimi ve yaptığınız değişiklikleri denetlemek için.
