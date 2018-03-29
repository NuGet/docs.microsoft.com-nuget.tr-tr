---
title: NuGet paketi yüklemesi yolları | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: overview
ms.prod: nuget
ms.technology: ''
description: Bir projeye diskte ve geçerli proje dosyalarına olanlar da dahil olmak üzere NuGet paketlerini yükleme işlemi açıklanmaktadır.
keywords: NuGet paketleri, NuGet paket referanslarını yükleniyor NuGet, NuGet paketi tüketim yükleyin
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b8cce7bd6c1bd73eb018b8891ddd72b2f4432d55
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Bir NuGet paketi yüklemek için farklı yollar

NuGet paketlerini karşıdan yüklenir ve aşağıdaki tabloda yöntemlerden birini kullanarak yüklü (bkz [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md) Bunlar zaten yüklü yoksa). Paket bir önbellekten alınabilir yerine indirilir.

| Yöntem | Açıklama |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet add package <package_name>` | (Tüm platformlar) Tarafından tanımlanan paketini alır \<paket_adı\>, bir klasöre geçerli dizinin içeriğini genişletir ve proje dosyasına bir başvuru ekler. Ayrıca alır ve bağımlılıkları yükler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[DotNet paket komut ekleme](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Paket Yöneticisi kullanıcı Arabirimi (Visual Studio) | (Windows ve Mac) Üzerinden, Gözat, seçebilir ve belirtilen paket kaynağından projesine paketleri ve bağımlılıklarını yüklemek bir kullanıcı Arabirimi sağlar. Yüklü paketler başvuruları proje dosyasına ekler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi kullanıcı Arabirimi başvurusu (Windows)](../tools/package-manager-ui.md)</li><li>[NuGet paketini projenize (Mac) dahil olmak üzere](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Paket Yöneticisi Konsolu (Visual Studio)<br/>`Install-Package <package_name>` | (Yalnızca Windows) Alır ve tarafından tanımlanan paketi yükler \<paket_adı\> çözümdeki belirtilen projesine seçili kaynağından sonra proje dosyasına bir başvuru ekler. Ayrıca alır ve bağımlılıkları yükler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi konsolu Kılavuzu](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (Tüm platformlar) Tarafından tanımlanan paketini alır \<paket_adı\> ve geçerli dizinde bir klasöre içeriğinin genişletir; listelenen tüm paketler de alabilirsiniz bir `packages.config` dosyası. Aynı zamanda alır ve bağımlılıkları yükler, ancak proje dosyalarına hiçbir değişiklik yapmaz veya `packages.config`.<ul><li>[Yükleme komutu](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Bir paketi yüklendiğinde ne olur

Kısaca, farklı NuGet araçları genellikle paketine bir başvuru proje dosyasında oluşturma veya `packages.config`, etkili bir şekilde paketi yükler bir paket geri yüklemesi gerçekleştirin. Özel durum `nuget install`, hangi yalnızca genişletir pakete bir `packages` klasörü ve diğer dosyaları değiştirmez.

Genel işlem aşağıdaki gibidir:

1. (Dışındaki tüm Araçlar `nuget.exe`) sürümü ve paket tanımlayıcı proje dosyasına kaydedin veya `packages.config`.

1. Paket edinin:
    - Paket (tam tanımlayıcı ve sürüm numarası tarafından) zaten içinde yüklü olup olmadığını denetle *paketleri genel* açıklandığı gibi klasör [genel paketleri ve önbellek klasör yönetimi](managing-the-global-packages-and-cache-folders.md).

    - Paketi içinde değilse *paketleri genel* klasörü, listede, listelenen kaynaklardan alma denemesi [yapılandırma dosyalarını](Configuring-NuGet-Behavior.md). Çevrimiçi kaynaklar için ilk paketi sürece önbellekten alma denemesi `-NoCache` ile belirtilen `nuget.exe` komutları veya `--no-cache` ile belirtilen `dotnet restore`. (Visual Studio ve `dotnet add package` önbelleği her zaman kullanın.) Bir paketi önbellekten kullanılırsa, "ÖNBELLEK" çıktısında görüntülenir. Önbellek zaman aşımı değeri 30 dakika vardır.

    - Paket önbellekte değilse yapılandırmasında listelenen kaynaklardan indirme girişiminde. Bir paket yüklediyseniz, "GET" ve "Tamam" çıkışında görünür.

    - Paket başarıyla tüm kaynaklardan alınamıyor, bir hata ile bu noktada gibi yüklenmesi başarısız olur [NU1103](../reference/errors-and-warnings.md#nu1103). Not Bu hatalardan `nuget.exe` komutları göster yalnızca son kaynağı işaretli, ancak gelir paket herhangi bir kaynaktan kullanılabilir değildi.

    Paket alınırken zaman NuGet yapılandırması kaynaklarında sırasını uygulanabilir:
      - PackageReference biçimini kullanarak projeleri için HTTP kaynakları denetlemeden önce NuGet kaynakları yerel klasör ve ağ paylaşımları denetler.
      - Kullanarak projeleri için `packages.config` yönetim biçimi, NuGet sırayı yapılandırmasında kaynakları kullanır. Bu durumda kaynak sıralama göz ardı geri yükleme işlemleri, bir özel durumdur ve hangi kaynak ilk yanıt gelen paket NuGet kullanır.
      - Genel olarak, belirli bir tanımlayıcı ve sürüm numarası ile verilen herhangi bir paket tam olarak aynı bulduğunda ne olursa olsun kaynağında olduğundan NuGet kaynakları denetler sipariş özellikle anlamlı değil.

1. (Dışındaki tüm Araçlar `nuget.exe`) paketi ve diğer bilgileri bir kopyasını kaydedin *http önbellek* açıklandığı gibi klasör [genel paketleri ve önbellek klasör yönetimi](managing-the-global-packages-and-cache-folders.md).

1. İndirdiyseniz, paketi kullanıcı başına yüklemek *paketleri genel* klasör. NuGet her paket tanımlayıcısı için bir alt klasör oluşturur, ardından paketin yüklü her sürümü için alt klasörler oluşturur.

1. Diğer proje dosyaları ve klasörleri güncelleştirin:

    - Projeler için depolanan paket bağımlılık grafiğinin güncelleştirme PackageReference, kullanarak `obj/project.assets.json`. Paket içeriğini kendilerini tüm proje klasörüne kopyalanmaz.
    - Kullanarak projeleri için `packages.config`, projenin içinde projenin hedef çerçevesi eşleşen genişletilmiş paketi parçaları kopyalama `packages` klasör. (Kullanırken `nuget install`, tüm genişletilmiş paketi çünkü kopyalanır `nuget.exe` hedef Framework'ü tanımlamak için proje dosyalarını inceleyin değil.)
    - Güncelleştirme `app.config` ve/veya `web.config` paketi kullanıyorsa [kaynak ve yapılandırma dosyası dönüşümleri](../create-packages/source-and-config-file-transformations.md).

1. Alt düzey bağımlılıkları yükleyin zaten projede yüklü değilse. Bu işlem işleminde, paket sürümlerinin açıklandığı gibi güncelleştirebilir [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).

1. (Yalnızca visual Studio) Paketin Benioku dosyası varsa, bir Visual Studio penceresinde görüntüler.

## <a name="related-articles"></a>İlgili makaleler

- [Genel bakış ve iş akışı paket tüketimi](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [NuGet önbellek ve paketleri genel klasörleri yönetme](managing-the-global-packages-and-cache-folders.md)
- [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md)
