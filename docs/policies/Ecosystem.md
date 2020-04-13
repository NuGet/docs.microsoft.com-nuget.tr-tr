---
title: NuGet Ekosistemine Genel Bakış
description: NuGet ekosisteminde NuGet kaynakları, Microsoft dışı NuGet projeleri, yardımcı programlar ve eğitim materyalleri dahil olmak üzere kapsamlı kaynaklar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495495"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet ekosistemine genel bakış

2010 yılında piyasaya sürülmesinden bu yana, NuGet geliştirme süreçlerinin farklı yönlerini geliştirmek ve otomatikleştirmek için büyük bir fırsat sundu.

NuGet izin verilen [Apache v2 lisansı](http://choosealicense.com/licenses/apache/)altında açık kaynak olduğundan, diğer projeler NuGet kaldıraç ve şirketler kendi ürünlerinde bunun için destek inşa edebilirsiniz. İster açık kaynak projeleri ister kurumsal uygulama geliştirme olsun, NuGet ve NuGet ve çevresinde yerleşik diğer uygulamalar, yazılım geliştirme sürecinizi geliştirmek için geniş bir araç ekosistemi sağlar.

Tüm bu projeler geliştirici katkıları nedeniyle yenilik yapabiliyor. NuGet'in kendisine katkıda bulunduğugibi, hataları ve yeni özellik fikirlerini bildirerek, geri bildirim sağlayarak, dokümantasyon yazarak ve mümkün olduğunca kod katkıda bulunarak bu projelere de katkıda bulunun.

## <a name="net-foundation-projects"></a>.NET Vakfı projeleri

NuGet, Microsoft geliştirme platformu için ücretsiz, açık kaynak kodlu paket yönetim sistemi sağlar. Bu birkaç istemci araçları yanı sıra [resmi NuGet Galerisi](http://www.nuget.org)oluşturan hizmetler kümesi oluşur. Bunlar birleştiğinde [.NET Foundation](http://www.dotnetfoundation.org/)tarafından yönetilen NuGet projesini oluşturur.

NuGet Organizasyonu GitHub'da çeşitli depolar içerir. [https://github.com/Nuget/Home](https://github.com/Nuget/Home)tüm depolara ve çeşitli NuGet bileşenlerinin nerede bulunacağıhakkında genel bir bakış sağlar.

## <a name="microsoft-projects"></a>Microsoft projeleri

Microsoft, NuGet'in geliştirilmesine büyük katkıda bulunmuştur. Microsoft çalışanları tarafından yapılan tüm katkılar da açık kaynak kodludur ve .NET Foundation'a bağışlanır (telif hakları dahil).

## <a name="non-microsoft-projects"></a>Microsoft dışı projeler

Birçok kişi ve şirket NuGet ekosistemine önemli katkılarda bulunmuştur. Burada listelenen her proje, temel NuGet bileşenlerinden farklı bir lisansa sahip olabilir, bu nedenle lisans koşullarının kullanılmadan önce kabul edilebilir olduğunu onaylayın:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Çikolatalı](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetSunucu](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (veya NuGet-as-a-service)](http://www.myget.org/)
- [NuGet Paket Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Sunucusu](http://nugetserver.net/)
- [Ahtapot Konuşlandırma](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [Sharpdevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin ve MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Diğer NuGet tabanlı yardımcı programlar

Bunlar NuGet üzerine inşa edilmiş araçlar ve yardımcı programlar:

- [Glimpse Uzantıları](http://getglimpse.com/Packages) (eklentiler paketlerdir)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS modülleri, Orchard Galerisi'nde barındırılan v1 NuGet yemlerinden getirilir)
- [NuGet Server'ın Java uygulaması](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting yeni paket yayınlar)
- [DefinitelyTyped](http://definitelytyped.org/) ([Otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Tip [Tanımları NuGet için yayınlandı](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Eğitim materyalleri ve referanslar

Yeni bir araç veya teknoloji kullanarak genellikle bir öğrenme eğrisi ile birlikte gelir. Neyse ki sizin için, NuGet tüm dik öğrenme eğrisi vardır! Aslında, herkes hızlı bir şekilde [paketleri tüketen alabilirsiniz.](../quickstart/use-a-package.md)

Bununla birlikte, paketlerin ve özellikle iyi paketlerin yazılmasının yanı sıra, nuget'i otomatik oluşturma ve dağıtım süreçlerinde benimsemek, aşağıdaki kaynaklarla biraz daha zaman geçirmeyi gerektirir:

- [NuGet Blog](http://blog.nuget.org/)
- [Twitter'da NuGet ekibi,@nuget](http://twitter.com/nuget)
- Kitaplar:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Temel](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Bireysel paketler için belgeler

[NuDoq,](http://nudoq.org) NuGet paketleri için basit erişim, güncellemeler ve belgeler sağlar.

NuDoq düzenli olarak en son paket güncelleştirmeleri için nuget.org galeri sunucusunu yoklar, kitaplık belge dosyalarını boşaltır ve işler ve siteyi buna göre güncelleştirir.

## <a name="adding-your-project"></a>Projenizi ekleme

Bu sayfaya değerli bir ek olacak bir NuGet ekosistem projeniz varsa, lütfen bu sayfaya bir düzenlemesi olan bir çekme isteği gönderin.
