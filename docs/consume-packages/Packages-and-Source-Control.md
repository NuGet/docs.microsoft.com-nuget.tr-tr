---
title: NuGet paketleri ve kaynak denetimi
description: İçin nasıl işlemesi gerektiğini NuGet paketleri içinde sürüm denetimi ve kaynak denetimi sistemlerini ve git ve TFVC paketlerle atlamak nasıl konuları.
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 0338c3445b2a3d8169158171d97d1e874533a80a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551805"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>NuGet paketlerini kaynak denetimi sistemlerini atlama

Geliştiriciler genellikle kendi kaynak denetim depolarından NuGet paketlerini atlayın ve bunun yerine dayanır [geri yükleme paketini](package-restore.md) bir yapıdan önce bir proje bağımlılıklarınızı yeniden yüklemek için.

Paket geri yükleme'yi bağlı olan nedenleri şunlardır:

1. Dağıtılmış sürüm denetim sistemleri, Git gibi tam kopyasını havuz içindeki her dosyanın her sürümünü içerir. Sık sık güncelleştirilir ikili dosyalar için önemli bir şişmeye neden ve uygulamanın deposunu kopyalamak için geçen süreyi düşey çizgi ise uzar.
1. Paketleri depoda eklendiğinde, geliştiricilerin doğrudan paket içeriğini, proje adlarında sabit kodlanmış bir yol açabilir ve NuGet aracılığıyla başvuran paketleri yerine disk eklemek için önerilir.
1. Hala kullanımda paket klasörleri silme emin olmak gerek duyduğunuz tüm kullanılmayan paket klasörlerinin çözümünüzü temizlemek daha zor hale gelir.
1. Paketleri gt;(yok) sahiplik temiz sınırları kodunuzu, bağlı diğer paketlerden arasındaki korur. Birçok NuGet paketi zaten kendi kaynak denetimi depoları saklanır.

Paket geri yükleme ile NuGet varsayılan davranışı olsa da, bazı el ile iş paketleri atlamak gerekli olan&mdash;yani `packages` projenizdeki klasöre&mdash;kaynak denetiminden bu makalede açıklandığı gibi.

## <a name="omitting-packages-with-git"></a>Git ile paketleri atlama

Kullanım [.gitignore dosyası](https://git-scm.com/docs/gitignore) NuGet paketlerini yok saymak için (`.nupkg`) `packages` klasöründe ve `project.assets.json`, başka şeylerin yanında. Başvuru için bkz: [örnek `.gitignore` Visual Studio projeleri için](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Önemli bölümleri `.gitignore` dosyası:

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
> Mümkünse bu yönergeleri izleyin *önce* kaynak denetimine projenize ekleme. Aksi takdirde, el ile silmeniz `packages` depo ve devam etmeden önce bu değişikliği iade klasöründen.

Seçili dosyaları için TFVC ile kaynak denetimi tümleştirmesi devre dışı bırakmak için:

1. Adlı bir klasör oluşturun `.nuget` çözüm klasöründe (burada `.sln` dosyasıdır).
    - İpucu: Windows üzerinde bu klasörü Windows Gezgini'nde oluşturmak için adı kullanın `.nuget.` *ile* nokta karakteri.

1. Bu klasörde adlı bir dosya oluşturun `NuGet.Config` ve düzenleme için açın.

1. Minimum olarak aşağıdaki metni ekleyin burada [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) ayarı bildirir her şeyi atlamak için Visual Studio `packages` klasörü:

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. TFS 2010 veya önceki bir sürümü kullanıyorsanız, gizlemek `packages` klasöründe, çalışma alanı eşlemeleri.

1. TFS 2012 veya sonraki sürümünü veya Visual Studio Team Services ile oluşturma bir `.tfignore` dosya çubuğunda açıklandığı [sunucuya AddFiles](/vsts/tfvc/add-files-server.md?view=vsts#tfignore). Bu dosyada, açıkça Değişiklikleri yoksaymak için aşağıdaki içeriği içerir `\packages` depo düzey ve diğer birkaç Ara dosyaları klasörü. (Dosya adını kullanarak Windows Gezgini'nde oluşturabileceğiniz bir `.tfignore.` sondaki noktayı ancak siz ile devre dışı bırakmak için "Bilinen dosya uzantıları gizle" ilk seçenek.):

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

1. Ekleme `NuGet.Config` ve `.tfignore` kaynak denetimi ve değişikliklerinizi iade edin.
