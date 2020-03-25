---
title: NuGet 5,5 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,5 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148299"
---
# <a name="nuget-55-release-notes"></a>NuGet 5,5 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi

## <a name="summary-whats-new-in-55"></a>Özet: 5,5 sürümündeki yenilikler

* Visual Studio 'da NuGet Paket Yöneticisi Kullanıcı arabirimi için geliştirilmiş erişilebilirlik ve ekran okuyucu deneyimi
    * Ekran okuyucu deneyimlerinde erişilebilirlik sorunları, yüklü metin kutusu için eksik altmetin ve erişilebilir ad, vb. [#9059](https://github.com/NuGet/Home/issues/9059)
    * Paket listesinde ekran okuyucu deneyimlerinde erişilebilirlik sorunları- [#9077](https://github.com/NuGet/Home/issues/9077)
    * Ekran okuyucu deneyimlerinde "tarama", "Install", "Update" sekmeleri ile ilgili erişilebilirlik sorunları- [#9078](https://github.com/NuGet/Home/issues/9078)
    * Ekran okuyucusu "boş", "hiçbir bağımlılık Ciesi", "NuGet. org", "MIT" bağlantı etiketini duyurmaz [#9157](https://github.com/NuGet/Home/issues/9157)

* Yerel akışlar üzerinde barındırılan paketler için Visual Studio Paket Yöneticisi Kullanıcı arabirimindeki kendi kendine içerilen bağımsız simgeler için destek- [#8189](https://github.com/NuGet/Home/issues/8189)

* MSBuild statik grafik API 'Lerini çağırarak değerlendirmeleri hızlandıran `RestoreUseStaticGraphEvaluation` kullanarak önemli ölçüde geliştirilmiş bir işlem temelli geri yükleme performansı- [8791](https://github.com/NuGet/Home/issues/8791)

* Platformlar arası kimlik doğrulama eklentileri ile iyileştirilmiş DotNet. exe güvenilirliği
    * Taskolaydexception ile başarısız dotnet restore- [#7842](https://github.com/NuGet/Home/issues/7842)
    * Eklenti: "bir görev iptal edildi"-Bu nedenle ADO kimlik doğrulamasında sorun oluştu. - [#8528](https://github.com/NuGet/Home/issues/8528)

* `dotnet nuget <add|remove|update|disable|enable|list> source` komutu Ekle- [#4126](https://github.com/NuGet/Home/issues/4126)

* DotNet NuGet Push- [#8778](https://github.com/NuGet/Home/issues/8778) kullanarak `--skip-duplicate` için supmport

* MSBuild/restore ile `packages.config` destek- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hata**

* V3 API 'lerle kendi kendine Güncelleştirici yeniden çalışma- [#4197](https://github.com/NuGet/Home/issues/4197)

* Paket bağımlılığı sürümü ' * ' olarak ayarlandıysa, paket bağımlılığı sürümü yanlış- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry hata iletisi, sorun kaynağını işaret etmiyor- [#7505](https://github.com/NuGet/Home/issues/7505)

* Kilit dosyası "*" senaryolarında kabul edilmez- [#8073](https://github.com/NuGet/Home/issues/8073)

* Visual Studio 'da *, PackageReference (MSBuild/DotNet/VS geri yükleme do) içinde kullanıldığında, NuGet. exe bir paketin en son sürümüne çözümlenmiyor. [#8432](https://github.com/NuGet/Home/issues/8432)

* birden çok hedefleme WPF projesi olan DotNet liste paketi- [#8463](https://github.com/NuGet/Home/issues/8463)

* ConcurrencyUtilities 'i geliştirme (CPU kullanımını azaltma)- [#8653](https://github.com/NuGet/Home/issues/8653)

* Kaldırılan proje senaryolarında DG Spec Önizleme geri yüklemeler- [#8793](https://github.com/NuGet/Home/issues/8793) yazılmamalıdır

* Visual Studio NuGet paketleri (RestoreManagerPackage), çözüm oluşturma olaylarına otomatik olarak yüklenilmesi gerekir- [#8796](https://github.com/NuGet/Home/issues/8796)

* VSSettings init- [#8842](https://github.com/NuGet/Home/issues/8842) kilitlenmesi

* Bir proje çözüm klasörüne yerleştirilirse, VisualStudio araç kutusu bir NuGet paketinden doldurulmamış- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS: çözüm geri yükleme adet sürekli, yarış durumu nedeniyle başarısız oluyor- [#8881](https://github.com/NuGet/Home/issues/8881)

* Yüklü sekmede "yükleniyor.." sabiti ve "arama <term>.. "Güncelleştirmeler sekmesinde- [#8890](https://github.com/NuGet/Home/issues/8890)

* Önbellek süresi dolduktan sonra VS PM Kullanıcı arabiriminde gömülü simgeler eksik- [#9069](https://github.com/NuGet/Home/issues/9069)

* Fireandur PM UI Startup- [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore: ıncludeexcludefiles. Equals (...) uygulama yanlış- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore: PackageSpec. Clone () eşit olmayan kopya oluşturuyor- [#9211](https://github.com/NuGet/Home/issues/9211)

* "Derleme hatalarla bittiğinde her zaman Hata Listesi göster" işaretli olmasa da hata listesi gösteriliyor [#8190](https://github.com/NuGet/Home/issues/8190)

* Statik grafik geri yükleme boş SolutionPath 'e geçmemelidir- [#9061](https://github.com/NuGet/Home/issues/9061)

* Geri yükle: her proje için bir kapanış hesaplandı 4 kez [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore: DependencyGraphSpec. Load (...), JObject- [#9040](https://github.com/NuGet/Home/issues/9040) gerektirmez

* Geri yükleme: büyük nesne yığınında (LOH) büyük dizeler oluşturuldu- [#9031](https://github.com/NuGet/Home/issues/9031)

* Yeni mono üzerinde özel NuGet. exe, MSBuild SDK 'Sı Çözümleyicisi nedeniyle kesintiye uğramayabilir- [8848](https://github.com/NuGet/Home/issues/8848)

* NuGet. dgspec. JSON "başka bir işlem tarafından kullanıldığında geri yükleme başarısız olur"- [8692](https://github.com/NuGet/Home/issues/8692)

**DCR**

* _GetRestoreProjectStyle mantığın bir görevde olması gerekir [#8804](https://github.com/NuGet/Home/issues/8804)

* Yüklü sekmesine varsayılan olarak kullanımdan kaldırma bilgilerini ekleyin- [#8541](https://github.com/NuGet/Home/issues/8541)

**[Bu yayında düzeltilen tüm sorunların listesi-5,5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
