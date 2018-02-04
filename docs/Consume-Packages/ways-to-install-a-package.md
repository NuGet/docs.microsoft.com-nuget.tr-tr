---
title: "NuGet paketi yüklemesi yolları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/30/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Bir projeye diskte ve geçerli proje dosyalarına olanlar da dahil olmak üzere NuGet paketlerini yükleme işlemi açıklanmaktadır."
keywords: "NuGet paketleri, NuGet paket referanslarını yükleniyor NuGet, NuGet paketi tüketim yükleyin"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e48bbe813168e773bc46b7fe25af29785ff75df
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/01/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Bir NuGet paketi yüklemek için farklı yollar

NuGet paketlerini karşıdan yüklenir ve aşağıdaki yöntemlerden birini kullanarak yüklü (bkz [Nuget'i yükle istemci araçları](../install-nuget-client-tools.md) Bunlar zaten yüklü yoksa):

| Yöntem | Açıklama |
| --- | --- |
| dotnet.exe CLI<br/>`dotnet install <package_name>` | (Tüm platformlar) Tarafından tanımlanan paketi indirir \<paket_adı\>, bir klasöre geçerli dizinin içeriğini genişletir ve proje dosyasına bir başvuru ekler. Ayrıca indirir ve bağımlılıkları yükler.<ul><li>[Yükleme ve bir paket (dotnet CLI) kullanma](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[DotNet komutları](../tools/dotnet-commands.md)</li></ul> |
| Paket Yöneticisi kullanıcı Arabirimi (Visual Studio) | (Windows ve Mac) Üzerinden, Gözat, seçebilir ve paketleri ve bunların bağımlılıklarını bir projeye yükle bir kullanıcı Arabirimi sağlar. Yüklü paketler başvuruları proje dosyasına ekler.<ul><li>[Yükleme ve bir paket (Visual Studio) kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi kullanıcı Arabirimi başvurusu (Windows)](../tools/package-manager-ui.md)</li><li>[NuGet paketini projenize (Mac) dahil olmak üzere](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Paket Yöneticisi Konsolu (Visual Studio)<br/>`Install-Package <package_name>` | (Yalnızca Windows) İndirir ve tarafından tanımlanan paketi yükler \<paket_adı\> çözümdeki belirtilen projeye sonra proje dosyasına bir başvuru ekler. Ayrıca indirir ve bağımlılıkları yükler.<ul><li>[Yükleme ve bir paket (Visual Studio) kullanma](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Paket Yöneticisi konsolu Kılavuzu](../tools/package-manager-console.md)</li></ul> |
| nuget.exe CLI<br/>`nuget install <package_name>` | (Tüm platformlar) Tarafından tanımlanan paketi indirir \<paket_adı\> ve geçerli dizinde bir klasöre içeriğinin genişletir; listelenen tüm paketler de indirebilirsiniz bir `packages.config` dosyası. Ayrıca indirir ve bağımlılıkları yükler, ancak proje dosyalarına hiçbir değişiklik yapmaz.<ul><li>[Yükleme komutu](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Genel yükleme işlemi

Genel olarak, NuGet paket yükleme istenir şunları yapar:

1. Paket edinin:
    - İstenen paketin bir önbellekte olup olmadığını denetle (bkz [NuGet önbelleği yönetme](managing-the-nuget-cache.md)).
    - Yapılandırma dosyalarında, listedeki ilk başlayarak listelenen kaynaklardan paketini karşıdan yüklemek paket önbellekte değilse çalışır. Bu davranış nuget.org paketin arayan önce özel paket akışları kullanmanızı sağlar (bkz [NuGet yapılandırma davranışı](configuring-nuget-behavior.md)).
    - NuGet paketi başarıyla kaynaklardan biri satın aldıysanız, önbelleğe ekler. Aksi takdirde yükleme başarısız olur.

1. Paketini projeye genişletin.
    - Paketin içeriği uygun bir alt klasöre unzipping genişleyen anlamına gelir. Bir kopyasını `.nupkg` kendisi de alt klasöründe yerleştirilir.
    - Paket bir Visual Studio veya .NET Core projeye yüklü ise yalnızca projenin hedef çerçevesi için ilgili dosyaların genişletilir. Nuget.exe komut satırını kullanarak yüklediğinizde, tüm derlemelerde genişletilir.

1. Paket Visual Studio veya CLI dotnet içinde yüklediyseniz uygun proje dosyasına bir başvuru eklenir (veya `packages.config` bazı Visual Studio Proje türleri için).

## <a name="related-topics"></a>İlgili konular

- [Genel bakış ve iş akışı paket tüketimi](../consume-packages/overview-and-workflow.md)
- [Bulma ve paketleri seçme](../consume-packages/finding-and-choosing-packages.md)
- [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md)
- [NuGet önbelleği yönetme](managing-the-nuget-cache.md)
