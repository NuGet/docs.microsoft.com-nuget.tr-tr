---
title: NuGet paketleri ve kaynak denetimi | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c874e6f-99eb-46dd-997f-f67d98d0237e
description: "Sürüm denetimi ve kaynak denetim sistemleri içindeki NuGet paketleri kabul etme ve git ve TFVC'yi paketlerle atlayın durumları."
keywords: "Depoları NuGet kaynak denetimi, NuGet sürüm denetimi, NuGet ve git, NuGet ve TFS, NuGet ve TFVC'yi, atlama paketleri, kaynak denetimi depoları, sürüm denetimi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c73dea74f2363f49fb476a5812c29de63fec89a3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Kaynak Denetim sistemleri NuGet paketlerini atlama

Geliştiriciler genellikle kendi kaynak denetimi depoları NuGet paketleri atlayın ve bunun yerine Bel [paket geri yükleme](../consume-packages/package-restore.md) bir yapı önce bir proje bağımlılıklarınızı yeniden yüklemek için.

Paket geri yükleme bağlı nedenleri şunlardır:

1. Git gibi dağıtılmış sürüm denetim sistemleri her sürüm deposu içinde her dosyanın tam kopyalarını içerir. Sık sık güncelleştirilen ikili dosyaları için önemli oluşan şişirmeyi sağlama ve depoyu kopyalayın süresini düşey çizgi ise uzar.
1. Paketleri depoya eklendiğinde, geliştiricilerin, doğrudan paket içeriğini başvuru paketler sabit kodlanmış yol adları projesinde açabilir NuGet aracılığıyla yerine disk eklemek zararlardan önerilir.
1. Paket klasörleri hala kullanımda silmeyin emin olmak gereksinim duyduğunuz çözümünüzün herhangi kullanılmayan paket klasörlerinin temiz zor olur.
1. Paketleri kaldırarak sahipliği temiz sınırlarının kodunuzu, bağlı diğer paketleri arasındaki korur. Birçok NuGet paketleri kendi kaynak denetimi depoları zaten saklanır.

Paket geri yüklemesi varsayılan davranışı NuGet ile el ile bazı iş paketleri atlamak gerekli olsa da&mdash;öğesine, `packages` projenizdeki klasöre&mdash;kaynak denetiminden aşağıdaki bölümlerde açıklandığı gibi.

## <a name="omitting-packages-with-git"></a>Git paketlerle atlama

Kullanım [.gitignore dosyası](https://git-scm.com/docs/gitignore) eklenmesini önlemek için `packages` kaynak denetimi klasöründe. Başvuru için bkz: [örnek `.gitignore` Visual Studio projeleri için](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Önemli kısımlarını `.gitignore` dosyası:

```
# Ignore NuGet Packages
*.nupkg

# Ignore the packages folder
**/packages/*

# Include packages/build/, which is used as an MSBuild target
!**/packages/build/

# Uncomment if necessary; generally it's regenerated when needed
#!**/packages/repositories.config

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json; project.assets.json is used in conjunction with the PackageReference format.
project.lock.json
project.assets.json
*.nuget.props
```

## <a name="omitting-packages-with-team-foundation-version-control"></a>Team Foundation sürüm denetimi paketlerle atlama

> [!Note]
> Bu yönergeleri mümkünse *önce* projenizi kaynak denetimine ekleme. Aksi takdirde, el ile silmeniz `packages` klasöründen depo ve devam etmeden önce bu değişikliği denetleyin.

Seçili dosyaları için TFVC'yi kaynak denetimi tümleştirmesi devre dışı bırakmak için:

1. Adlı bir klasör oluşturun `.nuget` çözüm klasördeki (burada `.sln` dosyası).
    - İpucu: Kullanın adı, Windows bu klasörü Windows Gezgini'nde oluşturmak için `.nuget.` *ile* sondaki noktayı.

1. Bu klasörde adlı bir dosya oluşturun `NuGet.Config` ve düzenlemek için açın.

1. Minimum olarak aşağıdaki metni ekleyin nerede [disableSourceControlIntegration](../Schema/nuget-config-file.md#solution-section) ayarı bildirir her şeyi atlamak için Visual Studio `packages` klasörü:

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

   ```
   # Ignore NuGet Packages
   *.nupkg   

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Include package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. Ekleme `NuGet.Config` ve `.tfignore` kaynak denetimi ve yaptığınız değişiklikleri denetlemek için.
