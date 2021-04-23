---
title: NuGet paketleri ve kaynak denetimi
description: Sürüm denetimi ve kaynak denetim sistemleri içindeki NuGet paketlerinin nasıl değerlendirildiğinin ve git ve TFVC ile paketlerin nasıl devralınmasında dikkat edilecek noktalar.
author: JonDouglas
ms.author: jodou
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: fa3ec6992002224c9fb56a53aee9096e6d2c6fbb
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901674"
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a>Kaynak denetim sistemlerinde NuGet paketlerini atlama

Geliştiriciler tipik olarak kaynak denetim depolarından NuGet paketlerini atlayın ve bir projenin bağımlılıklarını yapılandırmadan önce yeniden yüklemek için [paket geri yükleme](package-restore.md) ' ye güvenir.

Paket geri yüklemeye bağlı olma nedenleri şunları içerir:

1. Git gibi dağıtılmış sürüm denetim sistemleri, depo içindeki her dosyanın her bir sürümünün tam kopyalarını içerir. Sık güncellenen ikili dosyalar, önemli blobu ve deponun kopyalanması için geçen süreyi uzunlukla düşürür.
1. Paketler depoya dahil edildiğinde, geliştiriciler,, projedeki sabit kodlanmış yol adlarına yol açabilecek şekilde, NuGet aracılığıyla paketlere başvurmak yerine disk üzerindeki paket içeriklerine doğrudan başvuru eklemeye tabi olur.
1. Hala kullanımda olan herhangi bir paket klasörünü silmemenizi güvence altına aldığınızdan emin olmak için, kullanılmayan paket klasörlerinin çözümünüzü temizlemek daha zor hale gelir.
1. Paketleri atlayarak, kodunuzun ve bağlı olduğunuz diğer kişilerin paketleri arasındaki sahipliğinin Temizleme sınırlarını koruursunuz. Birçok NuGet paketi zaten kendi kaynak denetimi depolarında saklanır.

Paket geri yükleme, NuGet ile varsayılan davranış olsa da, bu makalede açıklandığı gibi, bazı el ile yapılan diğer işler, &mdash; `packages` &mdash; kaynak denetiminden, bu makaledeki paketleri atlamak için gereklidir.

## <a name="omitting-packages-with-git"></a>Git ile paketleri atlama

[. Gitignore dosyasını](https://git-scm.com/docs/gitignore) , NuGet paketleri ( `.nupkg` ) `packages` klasörünü ve diğer şeyleri göz ardı etmek için kullanın `project.assets.json` . Başvuru için bkz. [ `.gitignore` Visual Studio projeleri için örnek](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):

Dosyanın önemli kısımları `.gitignore` şunlardır:

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

## <a name="omitting-packages-with-team-foundation-version-control"></a>Team Foundation Sürüm Denetimi paketlerini atlama

> [!Note]
> Projenizi kaynak denetimine eklemeden *önce* mümkünse bu yönergeleri izleyin. Aksi takdirde, `packages` klasörü deponuzdan el ile silin ve devam etmeden önce bu değişikliği iade edin.

Seçili dosyalar için TFVC ile kaynak denetimi tümleştirmesini devre dışı bırakmak için:

1. `.nuget`Çözüm klasörünüzde (dosyanın olduğu) adlı bir klasör oluşturun `.sln` .
    - İpucu: Windows 'ta, bu klasörü Windows Gezgini 'nde oluşturmak için, adın `.nuget.` sonundaki noktayla *birlikte* kullanılması gerekir.

1. Bu klasörde adlı bir dosya oluşturun ve dosyayı `NuGet.Config` düzenlenmek üzere açın.

1. Aşağıdaki metni minimum olarak ekleyin; burada [Disablesourcecontrolinteize](../reference/nuget-config-file.md#solution-section) ayarı Visual Studio 'yu klasördeki her şeyi atlayacak şekilde bildirir `packages` :

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. TFS 2010 veya önceki bir sürümünü kullanıyorsanız, `packages` çalışma alanı eşlemelerinizde klasörü gizlerin.

1. TFS 2012 veya üzeri sürümlerde veya Visual Studio Team Services ile `.tfignore` [sunucuya dosya ekleme](/vsts/tfvc/add-files-server?view=vsts#tfignore&preserve-view=true)bölümünde açıklandığı gibi bir dosya oluşturun. Bu dosyada, `\packages` Depo düzeyindeki klasöre yapılan değişiklikleri ve diğer birkaç ara dosyayı açıkça yoksaymak için aşağıdaki içeriği ekleyin. (Dosya adını izleyen noktayla kullanarak Windows Gezgini 'nde oluşturabilirsiniz `.tfignore.` , ancak önce "bilinen dosya uzantılarını gizle" seçeneğini devre dışı bırakmanız gerekebilir.):

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

1. `NuGet.Config` `.tfignore` Kaynak denetimi ekleyin ve değişikliklerinizi iade edin.
