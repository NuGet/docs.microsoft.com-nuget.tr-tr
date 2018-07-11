#### <a name="windows"></a>Windows

1. Ziyaret [nuget.org/downloads](https://nuget.org/downloads) ve NuGet 3.3 veya üstünü seçin (2.8.6 Mono ile uyumlu değil). En son sürümü her zaman önerilir ve 4.1.0+ nuget.org için paketlerini yayımlamak için gereklidir.
1. Her indirme `nuget.exe` doğrudan dosya. Tarayıcınızı seçtiğiniz bir klasöre dosyayı kaydetmeye yönlendirir. Dosya *değil* yükleyici; doğrudan tarayıcıdan çalıştırırsanız herhangi bir şey görmez.
1. Yerleştirdiğiniz klasöre Ekle `nuget.exe` yerden CLI aracı kullanmak için PATH ortam değişkeninize için.

#### <a name="macoslinux"></a>macOS/Linux

Davranışlar, işletim sistemi dağıtım biraz değişebilir.

1. Yükleme [Mono 4.4.2 veya üzeri](http://www.mono-project.com/docs/getting-started/install/).

1. Bir kabuk isteminde aşağıdaki komutu yürütün:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. İşletim sisteminiz için uygun dosyasına aşağıdaki betiği ekleyerek bir diğer ad oluşturma (genellikle `~/.bash_aliases` veya `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Kabuk yeniden yükleyin.  Test yüklemesi girerek `nuget` parametre olmadan. NuGet CLI Yardım görüntülemelidir.
