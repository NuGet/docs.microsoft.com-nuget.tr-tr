---
title: "NuGet ekosistemine genel bakış | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Kapsamlı kaynaklar NuGet kaynakları, Microsoft olmayan NuGet projeleri, yardımcı programlar ve eğitim malzemelerinizin de dahil olmak üzere NuGet ekosistemindeki."
keywords: "NuGet ekosistemi, Microsoft olmayan NuGet projeleri, NuGet açık kaynak, NuGet yardımcı programlar, NuGet eğitim malzemelerini"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet ekosistemine genel bakış

Giriş 2010 olduğuna göre NuGet artırmak ve farklı yönlerini geliştirme süreçleri otomatik hale getirmek için harika bir fırsat sunulan.

NuGet açık kaynaklı bir izin veren altında olduğundan [Apache v2 lisans](http://choosealicense.com/licenses/apache/), diğer projeler NuGet yararlanabilir ve şirketler ürünlerinin onun için desteği oluşturabilir. Açık kaynaklı proje mı Kurumsal uygulama geliştirme, NuGet ve diğer uygulamalar üzerinde ve NuGet geçici yerleşik araçları geniş ekosistemiyle yazılım geliştirme sürecini iyileştirmek için sağlama.

Tüm bu projeleri Geliştirici Katkıları nedeniyle yenilik imkanınız olur. Ayrıca NuGet için katkıda yalnızca gibi bu projeler katkısı raporlama kusurları ve geribildirim sağlama, belgeleri yazma ve mümkün olduğunda kod katkıda bulunan yeni özellik fikirleri tarafından olun.

## <a name="net-foundation-projects"></a>.NET foundation projeleri

NuGet Microsoft geliştirme platformu için ücretsiz, açık kaynaklı paket yönetim sistemi sağlar. Oluşturan bir hizmetler kümesi olan yanı sıra birkaç istemci araçları oluşur [resmi NuGet galerisinde](http://www.nuget.org). Birleştirilmiş, bunlar tarafından yönetilen NuGet proje form [.NET Foundation](http://www.dotnetfoundation.org/).

NuGet kuruluşu, GitHub üzerinde çeşitli depoları içerir. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) tüm depoları genel bir bakış ve çeşitli NuGet bileşenleri nerede sağlar.

## <a name="microsoft-projects"></a>Microsoft projeleri

Microsoft, NuGet geliştirme için yaygın katıldığını. Microsoft çalışanlar tarafından bir katkılar de açık kaynaklıdır olan ve (telif hakları dahil olmak üzere) .NET Foundation'a bağışlanır.

## <a name="non-microsoft-projects"></a>Microsoft olmayan projeleri

Diğer birçok kişiler ve şirketler NuGet ekosistemi önemli ölçüde katkıda yaptınız. Burada listelenen her proje, çekirdek NuGet Bileşenler'den farklı bir lisansa sahip olabilir, böylece Lisans Koşulları'nı kullanmadan önce kabul edilebilir olduğundan emin olun:

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
- [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin ve MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Diğer NuGet tabanlı yardımcı programları

Bu araçlar ve yardımcı programlar NuGet üzerinde oluşturulmuş şunlardır:

- [Glimpse'in uzantıları](http://getglimpse.com/Packages) (eklentileri olan paketleri)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS modülleri getirilen Orchard Galerisi'nde barındırılan NuGet akışı bir v1'den)
- [NuGet sunucu Java uygulaması](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (yeni TWİTLEME bot yayınlar paketi Twitter)
- [DefinitelyTyped](http://definitelytyped.org/) ([otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript türü [tanımları için NuGet yayımlanan](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Eğitim malzemelerini ve başvurular

Genellikle bir yeni aracın veya teknoloji kullanarak bir öğrenme eğrisi ile birlikte gelir. Luckily sizin için NuGet tüm eğri hiçbir hızı yüksek öğrenme var! Aslında, herkes için [paketleri kullanma başlamak](../quickstart/use-a-package.md) hızlı bir şekilde.

Başka bir deyişle, paketleri yazma – ve özellikle iyi paketleri – otomatik derleme ve dağıtım işlemleri NuGet benimsemenin ile birlikte, aşağıdaki kaynaklarla biraz daha uzun harcama gerektirir:

- [NuGet Blog](http://blog.nuget.org/)
- [NuGet takım Twitter'da@nuget](http://twitter.com/nuget)
- Kitaplar:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 temelleri](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Tek paketler için belgeler

[NuDoq](http://nudoq.org) kolay erişim, güncelleştirmeleri ve NuGet paketleri için belgeler sağlar.

NuDoq düzenli olarak nuget.org galeri sunucuyu en son paket güncelleştirmelerini tarar, ayıklar ve kitaplığı belgeleri dosyaları işler ve site uygun şekilde güncelleştirir.

## <a name="adding-your-project"></a>Projenize ekleme

Bu sayfaya değerli bir toplama olacak NuGet ekosistemi proje varsa, lütfen bu sayfaya bir düzen içeren bir çekme isteği gönderin.
