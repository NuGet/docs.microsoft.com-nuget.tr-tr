---
title: "NuGet paketi yüklemesi yolları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Bir projeye diskte ve geçerli proje dosyalarına olanlar da dahil olmak üzere NuGet paketlerini yükleme işlemi açıklanmaktadır."
keywords: "NuGet paketleri, NuGet paket referanslarını yükleniyor NuGet, NuGet paketi tüketim yükleyin"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Bir NuGet paketi yüklemek için farklı yollar

NuGet paketlerini karşıdan yüklenir ve aşağıdaki yöntemlerden birini kullanarak yüklü (bkz [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md) Bunlar zaten yüklü yoksa):

| Yöntem | Açıklama |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | (Tüm platformlar) Tarafından tanımlanan paketi indirir \<paket_adı\>, bir klasöre geçerli dizinin içeriğini genişletir ve proje dosyasına bir başvuru ekler. Ayrıca indirir ve bağımlılıkları yükler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet komutları](../tools/dotnet-commands.md)</li></ul> |
| Paket Yöneticisi kullanıcı Arabirimi (Visual Studio) | (Windows ve Mac) Üzerinden, Gözat, seçebilir ve paketleri ve bunların bağımlılıklarını bir projeye yükle bir kullanıcı Arabirimi sağlar. Yüklü paketler başvuruları proje dosyasına ekler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi kullanıcı Arabirimi başvurusu (Windows)](../tools/package-manager-ui.md)</li><li>[NuGet paketini projenize (Mac) dahil olmak üzere](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Paket Yöneticisi Konsolu (Visual Studio)<br/>`Install-Package <package_name>` | (Yalnızca Windows) İndirir ve tarafından tanımlanan paketi yükler \<paket_adı\> çözümdeki belirtilen projeye sonra proje dosyasına bir başvuru ekler. Ayrıca indirir ve bağımlılıkları yükler.<ul><li>[Paket (dotnet CLI) yükleme ve kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi konsolu Kılavuzu](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (Tüm platformlar) Tarafından tanımlanan paketi indirir \<paket_adı\> ve geçerli dizinde bir klasöre içeriğinin genişletir; listelenen tüm paketler de indirebilirsiniz bir `packages.config` dosyası. Ayrıca indirir ve bağımlılıkları yükler, ancak proje dosyalarına hiçbir değişiklik yapmaz.<ul><li>[Yükleme komutu](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Genel yükleme işlemi

Genel olarak, NuGet paket yükleme istenir şunları yapar:

1. Paket edinin:
    - İstenen paketin bir önbellekte olup olmadığını denetle (bkz [NuGet önbelleği yönetme](managing-the-nuget-cache.md)).
    - Paket önbellekte değilse, listelenen kaynaklardan gelen paket indirme girişiminde [yapılandırma dosyalarını](Configuring-NuGet-Behavior.md).
      - Kullanarak projeleri için `packages.config` başvuru biçimi, NuGet sırayı yapılandırmasında kaynakları kullanır.
      - PackageReference biçimi kullanarak projeleri için NuGet önce yerel klasörleri olan kaynakları denetler ağ paylaşımları üzerindeki kaynakları denetler, sonra HTTP (Internet) kaynakları denetler.
      - Genel olarak, belirli bir tanımlayıcı ve sürüm numarası ile verilen herhangi bir paket tam olarak aynı bulduğunda ne olursa olsun kaynağında olduğundan NuGet kaynakları denetler sipariş özellikle anlamlı değil.
    - NuGet paketi başarıyla kaynaklardan biri satın aldıysanız, önbelleğe ekler. Aksi takdirde yükleme başarısız olur.

1. Paketini projeye genişletin.
    - Paketin içeriği uygun bir alt klasöre unzipping genişleyen anlamına gelir. Bir kopyasını `.nupkg` kendisi de alt klasöründe yerleştirilir.
    - Paket bir Visual Studio veya .NET Core projeye yüklü ise yalnızca projenin hedef çerçevesi için ilgili dosyaların genişletilir. Nuget.exe komut satırını kullanarak yüklediğinizde, tüm derlemelerde genişletilir.

1. Paket Visual Studio veya CLI dotnet içinde yüklediyseniz uygun proje dosyasına bir başvuru eklenir (veya `packages.config` bazı Visual Studio Proje türleri için).

## <a name="related-topics"></a>İlgili konular

- [Genel bakış ve iş akışı paket tüketimi](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md)
- [NuGet önbelleğini yönetme](managing-the-nuget-cache.md)
