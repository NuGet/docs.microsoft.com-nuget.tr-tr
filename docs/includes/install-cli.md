---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610523"
---
#### <a name="windows"></a>Windows

> [!Note]
> NuGet. exe 5,0 ve üzeri .NET Framework 4.7.2 veya üzeri bir sürümü gerektirir.

1. [NuGet.org/downloads](https://nuget.org/downloads) ziyaret edin ve NuGet 3,3 veya üstünü seçin (2.8.6 Mono ile uyumlu değildir). En son sürüm her zaman önerilir ve nuget.org 'e paket yayımlamak için 4.1.0 + gerekir.
1. Her indirme işlemi doğrudan `nuget.exe` dosyasıdır. Tarayıcınızı, dosyayı seçtiğiniz bir klasöre kaydetmesini isteyin. Dosya bir yükleyici *değil* ; doğrudan tarayıcıdan çalıştırırsanız hiçbir şey görmezsiniz.
1. Her yerden CLı aracını kullanmak için `nuget.exe` yerleştirdiğiniz klasörü PATH ortam değişkenine ekleyin.

#### <a name="macoslinux"></a>macOS/Linux

Davranışlar, işletim sistemi dağıtımına göre biraz farklılık gösterebilir.

1. [Mono 4.4.2 veya üstünü](https://www.mono-project.com/docs/getting-started/install/)yükler.

1. Bir kabuk isteminde aşağıdaki komutu yürütün:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Aşağıdaki betiği işletim sistemi için uygun dosyaya ekleyerek (genellikle `~/.bash_aliases` veya `~/.bash_profile`) bir diğer ad oluşturun:

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Kabuğu yeniden yükleyin.  Parametresiz `nuget` girerek yüklemeyi test edin. NuGet CLı yardımı görüntülenmelidir.
