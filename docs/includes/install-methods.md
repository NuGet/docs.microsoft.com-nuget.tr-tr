Bir paketi yükleniyor üç şekilde olur:

| Yöntem | Açıklama | Başvuru |
| --- | --- | --- |
| CLI nuget.exe:`nuget install <package_name>` | Tarafından tanımlanan paketi indirir \<paket_adı\> ve geçerli dizinde bir klasöre içeriğinin genişletir. Hiç paket belirtilirse, projenin içinde listelenen tüm paketler yükler `packages.config` dosya. Tüm proje dosyalarını hiçbir değişiklik yapılmadı. Bağımlılıkları da karşıdan ve genişletilmiş. | [CLI başvurusu](../tools/nuget-exe-CLI-Reference.md) |
| Paket Yöneticisi Konsolu (Visual Studio):`Install-Package <package_name>` | İndirir ve geçerli projenin sonra güncelleştirme paketi bir bağımlılık olarak listelemek için proje dosyası içine paketi yükler. | [Paket Yöneticisi konsolu Kılavuzu](../tools/Package-Manager-Console.md) |
| Paket Yöneticisi kullanıcı Arabirimi (Visual Studio) | Üzerinden, Gözat, seçebilir ve paket bir projeye yüklemek için bir kullanıcı Arabirimi sağlar. Paketi bir bağımlılık olarak listelemek için proje dosyasını güncelleştirir. | [Paket Yöneticisi kullanıcı Arabirimi başvurusu](../tools/Package-Manager-UI.md) |