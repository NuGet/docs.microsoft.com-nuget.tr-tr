#### <a name="windows"></a><span data-ttu-id="a71de-101">Windows</span><span class="sxs-lookup"><span data-stu-id="a71de-101">Windows</span></span>

1. <span data-ttu-id="a71de-102">Ziyaret [nuget.org/downloads](https://nuget.org/downloads) ve NuGet 3.3 ya da daha yüksek seçin (2.8.6 Mono ile uyumlu değil).</span><span class="sxs-lookup"><span data-stu-id="a71de-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="a71de-103">En son sürümü her zaman önerilir ve 4.1.0+ için nuget.org paketlerini yayımlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a71de-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="a71de-104">Her yükleme içindir `nuget.exe` dosyasını doğrudan.</span><span class="sxs-lookup"><span data-stu-id="a71de-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="a71de-105">Dosyasını tercih ettiğiniz bir klasöre kaydetmek için tarayıcınızı isteyin.</span><span class="sxs-lookup"><span data-stu-id="a71de-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="a71de-106">Dosya *değil* yükleyici; doğrudan tarayıcıdan çalıştırırsanız herhangi bir şey göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a71de-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="a71de-107">Yerleştirdiğiniz klasörü Ekle `nuget.exe` , yol ortam değişkenine yerden CLI aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a71de-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="a71de-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="a71de-108">macOS/Linux</span></span>

<span data-ttu-id="a71de-109">Davranışları, işletim sistemi dağıtımı tarafından biraz değişebilir.</span><span class="sxs-lookup"><span data-stu-id="a71de-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="a71de-110">Yükleme [Mono 4.4.2 ya da daha sonra](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="a71de-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="a71de-111">Bir kabuk isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a71de-111">Execute the following commands at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```

1. <span data-ttu-id="a71de-112">Aşağıdaki komut dosyası için uygun dosya için işletim sisteminizi ekleyerek bir diğer ad oluşturun (genellikle `~/.bash_aliases` veya `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="a71de-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="a71de-113">Kabuk yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a71de-113">Reload the shell.</span></span>  <span data-ttu-id="a71de-114">Test yüklemesi girerek `nuget` hiçbir parametre.</span><span class="sxs-lookup"><span data-stu-id="a71de-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="a71de-115">NuGet CLI Yardım görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="a71de-115">NuGet CLI help should display.</span></span>