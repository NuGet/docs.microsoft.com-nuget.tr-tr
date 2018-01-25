---
title: "Visual Studio 2017 ile .NET standart 2.0 NuGet paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 05/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "NuGet kullanarak .NET standart 2.0 NuGet paketleri oluşturma bir uçtan uca Kılavuz 4.x ve Visual Studio 2017."
keywords: "bir paket, .NET standart paketleri, .NET Core oluşturun"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aae38dd141c688a6eccc18cabea9e8245dbc36c5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Visual Studio 2017 ile .NET standart 2.0 paketleri oluşturma

*NuGet 4.x+ ve MSBuild 15.3 Visual Studio 2017 güncelleştirme 3 ve sonraki sürümlerle koşuluyla + için geçerlidir. Visual Studio 2017 önceki sürümleri için bu yönergeler için standart 1.4 .NET 1. 6 değiştirerek geçerli \<TargetFramework\> özelliği. Ayrıca bkz. [.NET standart paketleri oluşturmak Visual Studio 2015 ile](../guides/create-net-standard-packages-vs2015.md) NuGet 3.x+ ile çalışmak için.*

[.NET standart Kitaplığı](/dotnet/articles/standard/library) olduğu .NET API'lerini biçimsel belirtimini hedeflenen böylece büyük bütünlüğünü .NET ekosistemi oluşturma tüm .NET çalışma zamanları üzerinde kullanılabilir olması. .NET standart kitaplığı, iş yükünü bağımsız uygulamak tüm .NET platformları için BCL (temel sınıf kitaplığı) API'leri Tekdüzen kümesini tanımlar. Bunu tüm .NET çalışma zamanları arasında kullanılabilir PCLs üretmek için geliştiricilere olanak sağlar ve azaltır değilse platforma özgü koşullu derleme yönergeleri paylaşılan kod ortadan kaldırır.

Bu kılavuzda .NET standart kitaplığı 2.0 ile Visual Studio 2017 hedefleyen bir nuget paketi oluşturmada size anlatılmaktadır.

## <a name="pre-requisites"></a>Ön koşullar

Visual Studio 2017 güncelleştirme 3 ile bu gözden geçirme gerektiren **.NET Core platformlar arası geliştirme** iş yükü. Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/), ya da Professional ve Enterprise sürümleri kullanın.

İş yükü şu şekilde görünür Visual Studio yükleyicisinde gerektirir:

![Visual Studio yükleyicisi .NET core platformlar arası geliştirme iş yükü](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>.NET standart sınıf kitaplığı proje oluşturma

1. Visual Studio'da **Dosya > Yeni > Proje**, genişletin **Visual C# > .NET standart** düğümü, select **sınıf kitaplığı (Net standart)**, AppLogger için adı değiştirin ve Tamam'ı tıklatın.

    ![Yeni sınıf kitaplığı proje oluşturma](media/NuGet4-02-NewProject.png)

1. Derleme yapılandırmasını değiştirme **sürüm**.
1. Sağ `AppLogger` seçin Çözüm Gezgini'nde projeye **özellikleri**seçin **yapı** sekmesinde, onay kutusunu için **XML belge dosyası**ve ayarlayın yalnızca filename `AppLogger.xml`. Projeyi kaydedin.

1. Kodunuzu bileşenine (hangi açıkça yalnızca konsola ileti çıkarır) aşağıdaki gibi ekleyin:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. (Sürüm yapılandırmasıyla) projeyi oluşturun ve DLL ve XML dosyaları içinde üretilir denetleyin `bin\Release\netstandard2.0` klasör.

## <a name="edit-metadata-in-the-csproj-file"></a>.Csproj dosyasındaki meta verilerini düzenleme

Paket meta verileri doğrudan yer alan NuGet 4.0 ve .NET Core projelerle `.csproj` yerine dış dosyaları gibi dosya bir `.nuspec`. Meta verilerin tam açıklamasını bulunan [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md#pack-target).

1. Select Çözüm Gezgini'nde projeye sağ tıklayın **Düzenle AppLogger.csproj**ve ardından aşağıdaki gibi paket bilgileri içerecek şekilde ilk özellik grubu düzenleyin:

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. Projeyi kaydedin sonra çözüme sağ tıklayın ve seçin **yapı çözümü** bu kez doğru meta verilerle bir paket için tüm dosyaları yeniden oluşturulacak.

## <a name="package-the-component"></a>Paket bileşeni

NuGet 4.0 destekleyen MSBuild sürümü 15.1 + (MSBuild 15.3 Visual Studio 2017 güncelleştirme 3'ü bir parçası olarak dahil) kullanarak bir paketi hedef proje içerdiğinde gerekli paket meta verileri önceki bölümde eklendiği gibi. Bu şekilde MSBuild çağırmak için yalnızca paketi hedef aynı klasörde komut satırında belirtin `.csproj` dosyası:

    msbuild /t:pack /p:Configuration=Release

Ek seçeneklerle için `msbuild /t:pack`gibi içerik dosyalarını, simgeler ve kaynak kodu, bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md#pack-target).

Herhangi bir durumda, yukarıdaki komut oluşturur `AppLogger.YOUR_NAME.1.0.0.nupkg` içinde `bin\Release` klasörü varsayılan olarak, bu yapılandırma oluşturur. Atlarsanız `/p` anahtarı, varsayılan yapılandırmayı olacaktır `Debug`. 

Gibi bir araç bu dosyayı açmayı [NuGet paketi Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ve tüm düğümleri genişleterek, aşağıdaki içeriği görürsünüz:

![NuGet paket AppLogger paket gösteren Gezgini](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> A `.nupkg` yalnızca bir ZIP dosyasını farklı bir uzantıya sahip bir dosyadır. Ayrıca paket içeriğini, daha sonra değiştirerek inceleyebilirsiniz `.nupkg` için `.zip`, ancak uzantı nuget.org için bir paket karşıya yüklemeden önce geri yüklemek unutmayın.

Paketinizi diğer geliştiricileri için kullanılabilir yapmak için yönergeleri izleyin [bir paketi yayımlamaya](../create-packages/publish-a-package.md).

## <a name="related-topics"></a>İlgili konular

- [Proje dosyalarını başvurularında paketini](../consume-packages/package-references-in-project-files.md) paketinizi proje dosyasında doğrudan açıklayan tüm ayrıntılarını açıklar.
- [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../schema/msbuild-targets.md) kullanmak için tüm seçenekleri açıklar `msbuild /t:pack` paketi oluşturmak için.
- [.NET standart kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Core için .NET Framework'bağlantı noktası oluşturma](/dotnet/articles/core/porting/index)
