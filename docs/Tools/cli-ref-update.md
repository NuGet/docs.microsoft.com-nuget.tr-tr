---
title: "NuGet CLI güncelleştirme komut | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Nuget.exe güncelleştirme komut başvurusu"
keywords: "nuget güncelleştirme başvuru, güncelleştirme paketi komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a>güncelleştirme komutu (NuGet CLI)

**Uygulandığı öğe:** paketini tüketim &bullet; **desteklenen sürümler:** tüm

Güncelleştirmeleri projesindeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine için. Çalıştırmak için önerilen ['geri'](#restore) çalıştırmadan önce `update`. (Tek tek bir paketi güncelleştirmeye [ `nuget install` ](cli-ref-install.md) servis talebi NuGet en son sürümünü yükler, bir sürüm numarası belirtmeden.)

Not: `update` (Mac OSX veya Linux) Mono altında çalışması CLI ile çalışmaz. Komutu kullanarak projeleri de çalışmıyor `project.json` veya PackageReference yönetim biçimleri.

`update` Komutu derleme başvurularını proje dosyasında aynı zamanda güncelleştirmeleri, olanlar başvuran sağlanan zaten mevcut. Eklenen bütünleştirilmiş güncelleştirilmiş bir paket varsa, yeni bir başvurudur *değil* eklendi. Yeni paket bağımlılıkları da eklenen derleme başvurularını yok. Bu işlemlerin bir güncelleştirme bir parçası olarak dahil etmek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanılarak paketi güncelleştirin.

Bu komut, nuget.exe kendisini güncelleştirmek için de kullanılabilir kullanarak *-self* bayrağı.

## <a name="usage"></a>Kullanım

```
nuget update <configPath> [options]
```

Burada `<configPath>` ya da tanımlayan bir `packages.config` veya proje bağımlılıkları listeler çözüm dosyası.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| ConfigFile | *(2.5 +)*  Uygulamak için NuGet yapılandırma dosyası. Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır. |
| FileConflictAction | *(2.5 +)*  Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar sorulduğunda gerçekleştirilecek eylemi belirtir. Değerler *üzerine yazma, yoksay, hiçbiri*. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| Kimliği | Paketi güncelleştirmeye kimlikleri listesini belirtir. |
| MSBuildPath | *(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Değerleri, 4, 12, 14, 15 desteklenir. MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| Etkileşimli olmayan | Kullanıcı girişi veya onayı için ister gizler. |
| Yayın öncesi | Yayın öncesi sürümler için güncelleştirme sağlar. Bu bayrak, yüklü olan yayın öncesi paket güncelleştirilirken gerekli değildir. |
| RepositoryPath | Paketleri yüklendiği yerel klasörü belirtir. |
| Güvenli | Yüklü paketin yüklü olarak yalnızca aynı birincil ve ikincil sürüm içinde kullanılabilir en yüksek sürüm ile güncelleştirmelerinin belirtir. |
| Kendi kendini | *(1.4 +)*  Nuget.exe en son sürüme; güncelleştirmeleri diğer tüm bağımsız değişkenleri göz ardı edilir. |
| Kaynak | Paket kaynaklarını listesini güncelleştirmeleri için kullanılacak (URL'ler olarak) belirtir. Belirtilmezse, komut yapılandırma dosyalarında sağlanan kaynakları kullanır, bkz: [NuGet yapılandırma davranışı](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *(2.5 +) ayrıntılı*. |
| Sürüm | Bir paket kimliği ile kullanıldığında, güncelleştirme paketi sürümünü belirtir. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="examples"></a>Örnekler

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
