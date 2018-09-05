---
title: NuGet ekosistemine genel bakış
description: NuGet kaynağı, Microsoft NuGet projeler, yardımcı programlar ve eğitim malzemeleri NuGet ekosisteminde kapsamlı kaynaklar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548150"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet ekosistemine genel bakış

NuGet, 2010'daki giriş olduğundan, geliştirmek ve farklı yönlerini geliştirme süreçleri otomatik hale getirmek için harika bir fırsat sunulan.

NuGet, açık kaynak bir esnek altında olduğundan [Apache v2 lisans](http://choosealicense.com/licenses/apache/), diğer projeleri NuGet yararlanabilir ve şirketler ürünlerinin desteği de oluşturabilirsiniz. Açık kaynaklı projelerin mı Kurumsal uygulama geliştirme, NuGet ve diğer uygulamalar üzerinde ve NuGet geçici olarak oluşturulmuş geniş bir ekosistemi araçların yazılım geliştirme sürecini iyileştirmek için sağlayın.

Bu projelerin hepsine Geliştirici Katkıları nedeniyle yenilik. Ayrıca NuGet için yalnızca katkıda bulunuyorsanız katkı bu projeler için raporlama hataları ve geri bildirim sağlama, belgeleri yazma ve mümkün olduğunda kod katkısı yeni özellik fikirleri olun.

## <a name="net-foundation-projects"></a>.NET foundation projeleri

NuGet, ücretsiz, açık kaynaklı paket yönetim sistemi için Microsoft geliştirme platformu sağlar. Kümesini oluşturan Hizmetleri yanı sıra birkaç istemci araçları oluşur [resmi NuGet Galerisi](http://www.nuget.org). Birlikte kullanıldığında bu tabidir NuGet proje formu [.NET Foundation](http://www.dotnetfoundation.org/).

NuGet kuruluş GitHub çeşitli depolarda içerir. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) Tüm depolar genel bir bakış ve çeşitli bileşenleri NuGet nerede bulacağını sağlar.

## <a name="microsoft-projects"></a>Microsoft projeleri

Microsoft, NuGet geliştirilmesini kapsamlı bir şekilde katkılarıyla. Microsoft çalışanları tarafından yapılan tüm katkılar de açık kaynak olan ve (telif hakkı) için .NET Foundation üzerinde Bağış.

## <a name="non-microsoft-projects"></a>Microsoft olmayan projeler

Diğer kişiler ve şirketlerin birçok önemli katkılar NuGet ekosistemine yapıldı. Burada listelenen her bir proje çekirdek NuGet bileşenlerini değerinden farklı bir lisansa sahip, bu nedenle Lisans Koşulları'nı kullanmadan önce kabul edilebilir olduğunu onaylayın:

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
- [NuGet paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet sunucusu](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin ve MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>NuGet tabanlı diğer yardımcı programları

Araçlar ve yardımcı programlar NuGet üzerinde oluşturulmuş şunlardır:

- [Glimpse uzantıları](http://getglimpse.com/Packages) (eklentileri olan paketleri)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS modülleri getirilen Orchard galeride barındırılan NuGet akışı bir v1'den)
- [Java uygulaması NuGet sunucusu](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter yeni TWİTLEME bot yayınlar paketi)
- [DefinitelyTyped](http://definitelytyped.org/) ([otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript türü [tanımları için NuGet yayımlanan](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Eğitim malzemeleri ve başvuruları

Genellikle bir yeni aracın veya teknoloji kullanarak bir öğrenme eğrisi ile birlikte gelir. Neyse ki, NuGet tüm eğri hiçbir seyretmez öğrenme var! Aslında, herkes için [paketleri tüketen başlama](../quickstart/use-a-package.md) hızlı bir şekilde.

Başka bir deyişle, paketleri yazma – ve özellikle de iyi paketler – otomatik derleme ve dağıtım işlemleri NuGet benimsemenin ile birlikte, aşağıdaki kaynaklarla biraz daha fazla zaman harcadığı gerektirir:

- [NuGet blogu](http://blog.nuget.org/)
- [NuGet takım Twitter'da @nuget](http://twitter.com/nuget)
- Kitap:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 temel bileşenleri](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Tek paketler için belgeleri

[NuDoq](http://nudoq.org) kolay erişim ve güncelleştirmeler ve NuGet paketleri için belgeler sağlar.

NuDoq düzenli olarak nuget.org galeri sunucuyu en son paket güncelleştirmeleri tarar, ayıklar ve kitaplık belge dosyaları işler ve site uygun şekilde güncelleştirir.

## <a name="adding-your-project"></a>Projenize ekleme

Bu sayfaya değerli bir toplama olabilecek bir NuGet ekosistemi projeniz varsa, lütfen bu sayfaya bir düzenleme ile bir çekme isteği gönderin.
