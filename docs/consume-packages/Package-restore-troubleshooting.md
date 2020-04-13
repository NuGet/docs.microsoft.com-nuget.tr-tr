---
title: Visual Studio'da Sorun Giderme NuGet Paketi Geri Yükleme
description: Visual Studio'da sık karşılaşılan NuGet geri yükleme hatalarının ve bunların nasıl sorun giderilenin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860619"
---
# <a name="troubleshooting-package-restore-errors"></a>Sorun giderme paketi geri yükleme hataları

Bu makalede, paketleri geri ve bunları gidermek için adımlar geri alırken yaygın hatalar üzerinde duruluyor. 

Paket Geri Yükleme, tüm paket bağımlılıklarını proje dosyanızdaki paket başvurularıyla *(.csproj)* veya *packages.config* dosyanızla eşleşen doğru duruma yüklemeye çalışır. (Visual Studio'da, başvurular **Bağımlılıklar \ NuGet** veya **Başvuru düğümü** altında Çözüm Gezgini'nde görünür.) Paketleri geri yüklemek için gerekli adımları izlemek için [paketleri geri yükle'ye](../consume-packages/package-restore.md#restore-packages)bakın. Proje dosyanızdaki paket başvuruları (*.csproj*) veya *packages.config* dosyanız yanlışsa (Paket Geri Yükleme'den sonra istediğiniz durumla eşleşmiyorsa), Paket Geri Yükleme'yi kullanmak yerine paketleri yüklemeniz veya güncelleştirmeniz gerekir.

Buradaki talimatlar sizin için işe yaramazsa, senaryonuzu daha dikkatli inceleyebilmemiz için [lütfen GitHub'da bir sorun dosyalayın.](https://github.com/NuGet/docs.microsoft.com-nuget/issues) "Bu sayfa yararlı mı?" daha fazla bilgi için sizinle iletişim kurma olanağı vermediği için bu sayfada görünebilecek denetimi denetleyin.

## <a name="quick-solution-for-visual-studio-users"></a>Visual Studio kullanıcıları için hızlı çözüm

Visual Studio kullanıyorsanız, önce aşağıdaki gibi paket geri yüklemeyi etkinleştirin. Aksi takdirde izleyen bölümlere devam edin.

1. **NuGet Paket Yöneticisi > Paket Yöneticisi Ayarları** menü komutu > Araçlar'ı seçin.
1. Paket Geri **Yükleme**altında her iki seçeneği de ayarlayın.
1. **Tamam'ı**seçin.
1. Projenizi yeniden oluşturun.

![Araç/Seçenekler'de NuGet paketini geri yüklemeyi etkinleştirme](../consume-packages/media/restore-01-autorestoreoptions.png)

Bu ayarlar dosyanızda `NuGet.config` da değiştirilebilir; [onay](#consent) bölümüne bakın. Projeniz MSBuild tümleşik paket geri yüklemesini kullanan eski bir projeyse, otomatik paket geri yüklemesine [geçiş](package-restore.md#migrate-to-automatic-package-restore-visual-studio) yapmanız gerekebilir.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Bu proje, bu bilgisayarda eksik olan NuGet paketine(ler) başvurur

Tam hata iletisi:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Bu hata, bir veya daha fazla NuGet paketine başvuru içeren bir proje oluşturmaya çalıştığınızda oluşur, ancak bu paketler şu anda bilgisayara veya projeye yüklenmez.

- [PackageReference](package-references-in-project-files.md) yönetim biçimini kullanırken, hata paketin [genel paketleri ve önbellek klasörlerini yönetmede](managing-the-global-packages-and-cache-folders.md)açıklandığı gibi *genel paketler* klasörüne yüklenmediğini gösterir.
- [packages.config](../reference/packages-config.md)kullanırken, hata paketin çözüm kökündeki `packages` klasöre yüklü olmadığı anlamına gelir.

Bu durum genellikle, projenin kaynak kodunu kaynak denetiminden veya başka bir karşıdan yüklemeden aldığınızda oluşur. Paketler genellikle kaynak denetiminden veya karşıdan yüklemelerden atlanır, çünkü nuget.org gibi paket akışlarından geri yüklenebilirler (bkz. [Paketler ve kaynak denetimi).](Packages-and-Source-Control.md) Bunları da dahil etmek aksi takdirde depo şişirme veya gereksiz yere büyük .zip dosyaları oluşturmak olacaktır.

Proje dosyanız paket konumlarına mutlak yollar içeriyorsa ve projeyi taşırsanız hata da olabilir.

Paketleri geri yüklemek için aşağıdaki yöntemlerden birini kullanın:

- Proje dosyasını taşıdıysanız, paket başvurularını güncelleştirmek için dosyayı doğrudan güncelleştirin.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([otomatik geri yükleme](package-restore.md#restore-packages-automatically-using-visual-studio) veya manuel geri [yükleme](package-restore.md#restore-packages-manually-using-visual-studio))
- [dotnet CLI](package-restore.md#restore-using-the-dotnet-cli)
- [nuget.exe CLI](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Başarılı bir geri yüklemeden sonra, paket *genel paketler* klasöründe bulunmalıdır. PackageReference kullanan projeler için, geri `obj/project.assets.json` yükleme dosyayı yeniden oluşturmalı; kullanan `packages.config`projeler için, paket projenin `packages` klasöründe görünmelidir. Proje artık başarıyla inşa edilmelidir. Değilse, sizi takip edebilmemiz için [GitHub'da bir sorun](https://github.com/NuGet/docs.microsoft.com-nuget/issues) dosyalayabilirsiniz.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>Varlıklar dosya project.assets.json bulunamadı

Tam hata iletisi:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Dosya, `project.assets.json` gerekli tüm paketlerin bilgisayara yüklendiğinden emin olmak için kullanılan PackageReference yönetim biçimini kullanırken projenin bağımlılık grafiğini tutar. Bu dosya paket geri yüklemesi yoluyla dinamik olarak oluşturulduğundan, genellikle kaynak denetimine eklenmez. Sonuç olarak, bu hata, paketleri otomatik olarak geri `msbuild` yüklemeyen bir araçla bir proje inşa ederken oluşur.

Bu durumda, `msbuild -t:restore` ardından `msbuild`çalıştırın `dotnet build` , veya kullanın (paketleri otomatik olarak geri yükleyin). Ayrıca [önceki bölümde](#missing)paket geri yükleme yöntemlerinden herhangi birini kullanabilirsiniz.

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Bir veya daha fazla NuGet paketinin geri yüklenmesi gerekir, ancak onay verilmediği için bu durum olamaz

Tam hata iletisi:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Bu hata, Paket geri yüklemenin NuGet yapılandırmanızda devre dışı bırakıldığını gösterir.

Visual Studio [kullanıcıları için Hızlı çözüm](#quick-solution-for-visual-studio-users)altında daha önce açıklandığı gibi Visual Studio'daki geçerli ayarları değiştirebilirsiniz.

Bu ayarları doğrudan ilgili `nuget.config` dosyada (genellikle `%AppData%\NuGet\NuGet.Config` Windows ve `~/.nuget/NuGet/NuGet.Config` Mac/Linux'ta) da ayarlayabilirsiniz. Altındaki `enabled` `packageRestore` tuşların `automatic` True olarak ayarlandıklarına emin olun:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> `packageRestore` Ayarları doğrudan olarak `nuget.config`ayarlarsanız, seçenekler iletişim kutusu geçerli değerleri göstersin diye Visual Studio'yu yeniden başlatın.

## <a name="other-potential-conditions"></a>Diğer potansiyel koşullar

- Eksik dosyalar nedeniyle yapı hatalarıyla karşılaşabilirsiniz ve bunları indirmek için NuGet geri yüklemesini kullanacağınızı söyleyen bir ileti ile karşılaşabilirsiniz. Ancak, geri yükleme çalıştıran "Tüm paketler zaten yüklü ve geri yüklenmesi için hiçbir şey yok" diyebilir. Bu durumda, klasörü `packages` (kullanırken) `packages.config` `obj/project.assets.json` veya dosyayı (PackageReference kullanırken) silin ve yeniden geri yükleyin. Hata hala devam ederse, `nuget locals all -clear` `dotnet locals all --clear` genel paketleri ve [önbellek klasörlerini yönetmede](managing-the-global-packages-and-cache-folders.md)açıklandığı gibi *genel paketleri* ve önbellek klasörlerini temizlemek için komut satırından kullanın.

- Kaynak denetiminden proje alırken, proje klasörleriniz salt okunur olarak ayarlanabilir. Klasör izinlerini değiştirin ve paketleri yeniden geri geri getirmeye çalışın.

- NuGet'in eski bir sürümünü kullanıyor olabilirsiniz. En son önerilen sürümler için [nuget.org/downloads](https://www.nuget.org/downloads) kontrol edin. Visual Studio 2015 için 3.6.0'ı öneriyoruz.

Başka sorunlarla karşılaşırsanız, sizden daha fazla ayrıntı alabilmemiz için [GitHub'da bir sorun](https://github.com/NuGet/docs.microsoft.com-nuget/issues) dosyalayAbilirsiniz.
