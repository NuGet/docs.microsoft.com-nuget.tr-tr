---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610523"
---
#### <a name="windows"></a><span data-ttu-id="aa891-101">Windows</span><span class="sxs-lookup"><span data-stu-id="aa891-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="aa891-102">NuGet. exe 5,0 ve üzeri .NET Framework 4.7.2 veya üzeri bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="aa891-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="aa891-103">[NuGet.org/downloads](https://nuget.org/downloads) ziyaret edin ve NuGet 3,3 veya üstünü seçin (2.8.6 Mono ile uyumlu değildir).</span><span class="sxs-lookup"><span data-stu-id="aa891-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="aa891-104">En son sürüm her zaman önerilir ve nuget.org 'e paket yayımlamak için 4.1.0 + gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa891-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="aa891-105">Her indirme işlemi doğrudan `nuget.exe` dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="aa891-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="aa891-106">Tarayıcınızı, dosyayı seçtiğiniz bir klasöre kaydetmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="aa891-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="aa891-107">Dosya bir yükleyici *değil* ; doğrudan tarayıcıdan çalıştırırsanız hiçbir şey görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa891-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="aa891-108">Her yerden CLı aracını kullanmak için `nuget.exe` yerleştirdiğiniz klasörü PATH ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aa891-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="aa891-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="aa891-109">macOS/Linux</span></span>

<span data-ttu-id="aa891-110">Davranışlar, işletim sistemi dağıtımına göre biraz farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="aa891-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="aa891-111">[Mono 4.4.2 veya üstünü](https://www.mono-project.com/docs/getting-started/install/)yükler.</span><span class="sxs-lookup"><span data-stu-id="aa891-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="aa891-112">Bir kabuk isteminde aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="aa891-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="aa891-113">Aşağıdaki betiği işletim sistemi için uygun dosyaya ekleyerek (genellikle `~/.bash_aliases` veya `~/.bash_profile`) bir diğer ad oluşturun:</span><span class="sxs-lookup"><span data-stu-id="aa891-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="aa891-114">Kabuğu yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="aa891-114">Reload the shell.</span></span>  <span data-ttu-id="aa891-115">Parametresiz `nuget` girerek yüklemeyi test edin.</span><span class="sxs-lookup"><span data-stu-id="aa891-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="aa891-116">NuGet CLı yardımı görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="aa891-116">NuGet CLI help should display.</span></span>
