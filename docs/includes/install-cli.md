#### <a name="windows"></a>Windows
1. Ziyaret [nuget.org/downloads](https://nuget.org/downloads) ve NuGet 3.3 ya da daha yüksek seçin (2.8.6 Mono ile uyumlu değil). En son sürümü her zaman önerilir ve 4.1.0+ için nuget.org paketlerini yayımlamak için gereklidir.
2. Her yükleme içindir `nuget.exe` dosyasını doğrudan. Dosyasını tercih ettiğiniz bir klasöre kaydetmek için tarayıcınızı isteyin. Dosya *değil* yükleyici; doğrudan tarayıcıdan çalıştırırsanız herhangi bir şey göremezsiniz.
3. Yerleştirdiğiniz klasörü Ekle `nuget.exe` , yol ortam değişkenine yerden CLI aracını kullanın.

#### <a name="macoslinux"></a>macOS/Linux
Davranışları, işletim sistemi dağıtımı tarafından biraz değişebilir.

1. Yükleme [Mono 4.4.2 ya da daha sonra](http://www.mono-project.com/docs/getting-started/install/).
2. Bir kabuk isteminde aşağıdaki komutları çalıştırın:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Aşağıdaki komut dosyası için uygun dosya için işletim sisteminizi ekleyerek bir diğer ad oluşturun (genellikle `~/.bash_aliases` veya `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Kabuk yeniden yükleyin.  Test yüklemesi girerek `nuget` hiçbir parametre. NuGet CLI Yardım görüntülemelidir.