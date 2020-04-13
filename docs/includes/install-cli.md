---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610523"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet.exe 5.0 ve daha sonra .NET Framework 4.7.2 veya daha sonra yürütmek için gerektirir.

1. nuget.org/downloads ziyaret [edin](https://nuget.org/downloads) ve NuGet 3.3 veya üzerini seçin (2.8.6 Mono ile uyumlu değildir). En son sürüm her zaman önerilir ve paketleri nuget.org yayınlamak için 4.1.0+ gereklidir.
1. Her karşıdan `nuget.exe` yükleme doğrudan dosyadır. Tarayıcınıza dosyayı seçtiğiniz bir klasöre kaydetmesi için talimat ver. Dosya yükleyici *değildir;* doğrudan tarayıcıdan çalıştırdığınızda hiçbir şey görmezsiniz.
1. CLI aracını `nuget.exe` her yerden kullanmak için PATH ortamı değişkeninize yerleştirdiğiniz klasörü ekleyin.

#### <a name="macoslinux"></a>macOS/Linux

Davranışlar işletim sistemi dağılımına göre biraz farklılık gösterebilir.

1. [Mono 4.4.2 veya sonrası](https://www.mono-project.com/docs/getting-started/install/)yükleyin.

1. Aşağıdaki komutu bir kabuk isteminde yürüt:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. İşletim sisteminiz için uygun dosyaya aşağıdaki komut dosyasını `~/.bash_aliases` `~/.bash_profile`ekleyerek bir takma ad oluşturun (genellikle veya):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Kabuğu yeniden doldur.  Hiçbir parametre ile `nuget` girerek yüklemeyi test edin. NuGet CLI yardım görüntülemek gerekir.
