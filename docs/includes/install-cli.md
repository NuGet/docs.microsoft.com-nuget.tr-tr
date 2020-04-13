---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610523"
---
#### <a name="windows"></a><span data-ttu-id="6802b-101">Windows</span><span class="sxs-lookup"><span data-stu-id="6802b-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="6802b-102">NuGet.exe 5.0 ve daha sonra .NET Framework 4.7.2 veya daha sonra yürütmek için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6802b-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="6802b-103">nuget.org/downloads ziyaret [edin](https://nuget.org/downloads) ve NuGet 3.3 veya üzerini seçin (2.8.6 Mono ile uyumlu değildir).</span><span class="sxs-lookup"><span data-stu-id="6802b-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="6802b-104">En son sürüm her zaman önerilir ve paketleri nuget.org yayınlamak için 4.1.0+ gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6802b-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="6802b-105">Her karşıdan `nuget.exe` yükleme doğrudan dosyadır.</span><span class="sxs-lookup"><span data-stu-id="6802b-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="6802b-106">Tarayıcınıza dosyayı seçtiğiniz bir klasöre kaydetmesi için talimat ver.</span><span class="sxs-lookup"><span data-stu-id="6802b-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="6802b-107">Dosya yükleyici *değildir;* doğrudan tarayıcıdan çalıştırdığınızda hiçbir şey görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6802b-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="6802b-108">CLI aracını `nuget.exe` her yerden kullanmak için PATH ortamı değişkeninize yerleştirdiğiniz klasörü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6802b-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="6802b-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="6802b-109">macOS/Linux</span></span>

<span data-ttu-id="6802b-110">Davranışlar işletim sistemi dağılımına göre biraz farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="6802b-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="6802b-111">[Mono 4.4.2 veya sonrası](https://www.mono-project.com/docs/getting-started/install/)yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6802b-111">Install [Mono 4.4.2 or later](https://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="6802b-112">Aşağıdaki komutu bir kabuk isteminde yürüt:</span><span class="sxs-lookup"><span data-stu-id="6802b-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="6802b-113">İşletim sisteminiz için uygun dosyaya aşağıdaki komut dosyasını `~/.bash_aliases` `~/.bash_profile`ekleyerek bir takma ad oluşturun (genellikle veya):</span><span class="sxs-lookup"><span data-stu-id="6802b-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="6802b-114">Kabuğu yeniden doldur.</span><span class="sxs-lookup"><span data-stu-id="6802b-114">Reload the shell.</span></span>  <span data-ttu-id="6802b-115">Hiçbir parametre ile `nuget` girerek yüklemeyi test edin.</span><span class="sxs-lookup"><span data-stu-id="6802b-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="6802b-116">NuGet CLI yardım görüntülemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="6802b-116">NuGet CLI help should display.</span></span>
