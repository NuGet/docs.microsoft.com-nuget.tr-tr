---
title: NuGet 5,7 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,7 sürüm notları.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508793"
---
# <a name="nuget-57-release-notes"></a>NuGet 5,7 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir | .NET SDK 'ları 'nda kullanılabilir |
|:---|:---|:---|
| [**5.7.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |
| [**5.7.1**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,7](https://visualstudio.microsoft.com/downloads/) | [3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi

## <a name="summary-whats-new-in-57"></a>Özet: 5,7 sürümündeki yenilikler

### <a name="features-added-in-this-release"></a>Bu yayına eklenen özellikler

* NuGet paket başvuruları için extern diğer ad desteği eklendi- [#4989](https://github.com/NuGet/Home/issues/4989)

* Bir veri kaynağı paylaşmasına ve resfreshing- [#8294](https://github.com/NuGet/Home/issues/8294) azaltmalarına Izin vererek yüklü ve güncelleştirme sekmeleri daha hızlı bir şekilde geçiş yapıldı

* MSBuild statik grafik API 'lerini (dotnet.exe) çağırarak geri yüklemeyi daha hızlı hızlı hale getirme () [#9644](https://github.com/NuGet/Home/issues/9644)

* PackageReference projeleri için Visual Studio kısmi geri yüklemesi eklendi (Hayır-op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)

* Visual Studio Paket Yöneticisi Kullanıcı arabirimi, HTTP isteği başına istenen sayıda sonuçtan daha fazlasını döndüren hatalı oluşturulmuş paket kaynaklarını ararken daha az zaman çöker. - [#8478](https://github.com/NuGet/Home/issues/8478)

* VS geri yükleme 'de SDK olmayan stil projelerine yönelik PackageVersion bilgilerinin tümleştirilmesi eklendi [#9236](https://github.com/NuGet/Home/issues/9236)

* nuget.exe güncelleştirme `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783) için destek eklendi

* %APPDATA%\NuGet dizininde birden çok yapılandırma dosyası desteği eklendi- [#9394](https://github.com/NuGet/Home/issues/9394)

* DeterministicSourcePaths artık NuGet kaynak paketlerini Account- [#9431](https://github.com/NuGet/Home/issues/9431) olarak alıyor

* Inugetprojectservice. Getınstalsenpackagesasync genişletilebilirlik API- [#9702](https://github.com/NuGet/Home/issues/9702) eklendi

* Bir çözüme/projeye gerek olmadan geri dönüş klasörlerini numaralandırmak için birlikte çalışma API 'SI eklendi- [#9395](https://github.com/NuGet/Home/issues/9395)

* `latest`#8808 için seçenek `-MSBuildVersion`  -  [](https://github.com/NuGet/Home/issues/8808) eklendi

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hatalar:**

* DotNet CLı geri yükleme içinde, kimlik bilgisi eklentileri başlatırken, ortam değişkeni tanımlanmamışsa, sistem yolundaki DotNet CLı 'yi deneyin `DOTNET_HOST_PATH`  . - [#7438](https://github.com/NuGet/Home/issues/7438)

* nuget.exe spec, #8696 yerine, telif hakkı yyyy sabit kodlanmış metin ile bir telif hakkı etiketi oluşturuyor `$copyright$`  -  [](https://github.com/NuGet/Home/issues/8696)

* NuGet.exe, derleme adı değiştirilirse bir csproj paketi sırasında yer tutucuları ve AssemblyInfo özniteliklerini yoksayarak, ' yazarlar Required ' özel durumunu oluşturur. [#4234](https://github.com/NuGet/Home/issues/4234)

* HttpRequestMessage, SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661) desteklenmeyen birden çok kez yeniden kullanılabilir

* NuGet. Indexing 5.6.0 Preview 3 ve üzeri farklı bir ortak anahtar belirteci kullanır [#9481](https://github.com/NuGet/Home/issues/9481)

* NuGet paketi oluşturma sırasında TreatWarningsAsErrors 'ı kabul edin- [#7404](https://github.com/NuGet/Home/issues/7404)

* [CPVM] Birden çok P2P projesi için daha eski bir paket ( [#9549](https://github.com/NuGet/Home/issues/9549) )

* "Araştır" sekmesi, arama kutusuyla sola hizalı değil [#9559](https://github.com/NuGet/Home/issues/9559)

* Yüklü sürüm, birden çok sürüme sahip bir paket kimliği için çözüm düzeyi PM Kullanıcı arabirimindeki yerleşik simgesiyle tutarsız- [#9321](https://github.com/NuGet/Home/issues/9321)

* Sızıntı: PartCreationPolicy (CreationPolicy. NonShared) NuGet. SolutionRestoreManager. Restoreoperationgünlükçü- [#9595](https://github.com/NuGet/Home/issues/9595)

* İşlem dışı geri yüklemeler içinde varlık dosyasını okumaktan kaçının- [#9693](https://github.com/NuGet/Home/issues/9693)

* NuGet. Protocol, bir sürümün indirme sayısını aramadan almayı desteklemez- [#9086](https://github.com/NuGet/Home/issues/9086)

* JObject bağımlılıklarını azaltarak PackageMetadataResourceV3 bellek performansını geliştirme- [#9719](https://github.com/NuGet/Home/issues/9719)

**Tasarım değişiklik istekleri:**

* `<owners>`Öğe gereksiz olduğunda gizlenmiş [#5134](https://github.com/NuGet/Home/issues/5134)

* Interbir ETW olayları olarak oturum açma kimliği Izleme- [#9593](https://github.com/NuGet/Home/issues/9593)

* Geri yükleme sırasında, CPVM kullanıcılarına özelliğin önizlemede olduğunu bildirmek için bir bilgi iletisi eklendi [#9340](https://github.com/NuGet/Home/issues/9340)

* Çözüm Gezgini paket/proje geçişli bağımlılıklarını varlık dosyasından doldur- [#9580](https://github.com/NuGet/Home/issues/9580)

* Yüklenen paketler sekmesi, paket listesini sayfaduymamalıdır- [#6995](https://github.com/NuGet/Home/issues/6995)

**[Bu yayında düzeltilen tüm sorunların listesi-5,7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**

### <a name="community-contributions"></a>Topluluk katkıları

Bu NuGet yayınını harika hale getirmek için size yardımcı olan tüm katkıda bulunanlar için teşekkürler!

|Sağlayan|PR 'ler|Sorunlar|
|----|----|----|
|[campersau](https://github.com/campersau)|[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)|NuGet. Protocol, bir sürümün indirme sayısını aramadan almayı desteklemez- [#9086](https://github.com/NuGet/Home/issues/9086) </br>HttpRequestMessage, SocketHttpHandler- [#8661](https://github.com/NuGet/Home/issues/8661) desteklenmeyen birden çok kez yeniden kullanılabilir|
|[Joseph Musser (jnm2)](https://github.com/jnm2)|[3241](https://github.com/NuGet/NuGet.Client/pull/3241)|`<owners>`Öğe gereksiz olduğunda gizlenmiş [#5134](https://github.com/NuGet/Home/issues/5134)|
|[Volodymyr Shkolka (kara ad)](https://github.com/BlackGad)|[3273](https://github.com/NuGet/NuGet.Client/pull/3273)|NuGet, Istemci sertifikaları gerektiren HTTPS kaynaklarından geri yüklenemiyor- [#5773](https://github.com/NuGet/Home/issues/5773)|
|[Marius Ungureanu (Therzok)](https://github.com/Therzok)|[3357](https://github.com/NuGet/NuGet.Client/pull/3357)|HttpSourceAuthenticationHandler SemaphoreSlim ileride sağlama- [#9463](https://github.com/NuGet/Home/issues/9463)|
|[Sunner (SuNNjek)](https://github.com/SuNNjek)|[3088](https://github.com/NuGet/NuGet.Client/pull/3088)|nuget.exe spec, #8696 yerine, telif hakkı yyyy sabit kodlanmış metin ile bir telif hakkı etiketi oluşturuyor `$copyright$`  -  [](https://github.com/NuGet/Home/issues/8696)|
|[Zeytin Spinelli (kayvier-Spinelli)](https://github.com/olivier-spinelli)|[3335](https://github.com/NuGet/NuGet.Client/pull/3335)|DotNet CLı geri yükleme içinde, kimlik bilgisi eklentileri başlatırken, ortam değişkeni tanımlanmamışsa, sistem yolundaki DotNet CLı 'yi deneyin `DOTNET_HOST_PATH`  . - [#7438](https://github.com/NuGet/Home/issues/7438)|
|[goyızasılı](https://github.com/goyzhang)|[3370](https://github.com/NuGet/NuGet.Client/pull/3370)|`latest`#8808 için seçenek `-MSBuildVersion`  -  [](https://github.com/NuGet/Home/issues/8808) eklendi|

## <a name="summary-whats-new-in-571"></a>Özet: 5.7.1 'daki yenilikler

* . Nupkg. Metadata dosyasını yükleme kaynağını içerecek şekilde genişletin- [#10354](https://github.com/NuGet/Home/issues/10354)

* Geri yükleme günlüğü sırasında günlük paketi contenthash (ayıklama sırasında)- [#10384](https://github.com/NuGet/Home/issues/10384)

* Normal ayrıntı düzeyinde geri yükleme yaparken, bir paketin hangi kaynak olarak geri yüklendiğini günlüğe kaydet- [#10461](https://github.com/NuGet/Home/issues/10461)

**[Bu yayında düzeltilen tüm sorunların listesi-5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**

**[Bu sürümdeki işlemelerin listesi-5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**
