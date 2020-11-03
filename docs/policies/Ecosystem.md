---
title: NuGet ekosistemine genel bakış
description: NuGet ekosistemindeki NuGet kaynakları, Microsoft olmayan NuGet projeleri, yardımcı programlar ve eğitim malzemeleri dahil kapsamlı kaynaklar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 165587fb64be5a5f4dbfdece7dc3a1e6402b733e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237432"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet ekosistemine genel bakış

NuGet, 2010 'e giriş yaptığından, geliştirme işlemlerinin farklı yönlerini geliştirmek ve otomatikleştirmek için harika bir fırsat sundu.

NuGet, izin veren [Apache v2 lisansı](http://choosealicense.com/licenses/apache/)kapsamında açık kaynak olduğundan, diğer projeler NuGet 'den yararlanabilir ve şirketler ürününde bu ürüne yönelik destek oluşturabilir. NuGet ve üzerinde yerleşik olarak bulunan açık kaynaklı projeler veya kurumsal uygulama geliştirme, NuGet ve diğer uygulamalar, yazılım geliştirme işleminizi iyileştirmeye yönelik geniş bir araç sistemi sağlar.

Bu projelerin tümü, geliştirici katkılarından dolayı yenilik yapın yapabilir. Yalnızca NuGet 'e katkıda bulunarak, kusurları ve yeni özellik fikirlerini bildirerek bu projelere katkı vererek, geri bildirim, belge yazma ve mümkün olduğunda katkıda bulunan kod sağlar.

## <a name="net-foundation-projects"></a>.NET Foundation projeleri

NuGet, Microsoft geliştirme platformu için ücretsiz, açık kaynak paket yönetim sistemi sağlar. Bu, birkaç istemci aracından ve [resmi NuGet galerisini](http://www.nuget.org)oluşturan hizmetler kümesinden oluşur. Bu biçimde, [.net Foundation](http://www.dotnetfoundation.org/)tarafından yönetilen NuGet projesi de birleştirilir.

NuGet organizasyonu GitHub 'daki çeşitli depolar içerir. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) Tüm depolara ve çeşitli NuGet bileşenlerini nerede bulabileceğinizi bir genel bakış sağlar.

## <a name="microsoft-projects"></a>Microsoft projeleri

Microsoft, NuGet 'in geliştirilmesi için kapsamlı olarak katkıda bulunur. Microsoft çalışanları tarafından yapılan tüm katkılar da açık kaynaktır ve .NET Foundation ile donılır (telif hakları dahil).

## <a name="non-microsoft-projects"></a>Microsoft dışı projeler

Diğer birçok kişi ve şirket NuGet ekosistemine önemli bir katkı yaptı. Burada listelenen her proje, çekirdek NuGet bileşenlerinden farklı bir lisansa sahip olabilir, bu nedenle lisans koşullarının kullanılmadan önce kabul edilebilir olduğunu onaylayın:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (veya hizmet olarak NuGet)](http://www.myget.org/)
- [NuGet Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet sunucusu](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (ınedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin ve MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Diğer NuGet tabanlı yardımcı programlar

Bunlar, NuGet üzerine inşa edilen araçlar ve yardımcı araçlardır:

- [Göz at uzantıları](http://getglimpse.com/Packages) (eklentiler, paketlerdir)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS modülleri, Orchard galerisinde barındırılan bir v1 NuGet akışından getirilir)
- [NuGet sunucusunun Java uygulamasını uygulama](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [Nugetlatest](https://twitter.com/NuGetLatest) (Twitter bot yeni paket yayınları için çok fazla)
- [Definitelytyped](http://definitelytyped.org/) ( [NuGet 'e yayınlanan](http://www.nuget.org/packages?q=DefinitelyTyped)[Otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript tür tanımları)

## <a name="training-materials-and-references"></a>Eğitim malzemeleri ve başvuruları

Yeni bir aracın veya teknolojinin kullanılması genellikle bir öğrenme eğrisi ile gelir. Sizin için, NuGet 'in hiç bir içerse öğrenme eğrisi yok! Aslında, herkes paketleri hızlı bir şekilde [kullanmaya](../quickstart/install-and-use-a-package-in-visual-studio.md) başlayabilir.

Diğer bir deyişle, yazma paketleri ve özellikle iyi paketler – otomatik derleme ve dağıtım işlemlerinde NuGet 'in yanı sıra, aşağıdaki kaynaklarla daha fazla zaman harcamayı gerektirir:

- [NuGet blogu](http://blog.nuget.org/)
- [Twitter 'da NuGet ekibi, @nuget](http://twitter.com/nuget)
- Kitap
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 temel bileşenleri](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Ayrı paketlere yönelik belgeler

[Nudoq](http://nudoq.org) , NuGet paketleri için doğrudan erişim ve güncelleştirmeler ve belgeler sağlar.

NuDoq, en son paket güncelleştirmeleri için nuget.org Gallery sunucusunu düzenli olarak yoklar, kitaplık belge dosyalarını paketten kaldırır ve işler ve siteyi uygun şekilde güncelleştirir.

## <a name="adding-your-project"></a>Projenizi ekleme

Bu sayfaya değerli bir NuGet ekosistem projeniz varsa, lütfen bu sayfaya düzenleme ile bir çekme isteği gönderebilirsiniz.