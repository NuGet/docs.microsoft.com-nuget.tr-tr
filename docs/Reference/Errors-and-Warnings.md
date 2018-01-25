---
title: "NuGet geri yükleme hataları ve Uyarıları başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Tam başvuru için uyarıları ve hataları NuGet paket geri yüklemesi sırasında verilen"
keywords: "NuGet hatalar, NuGet uyarılar tanılama"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
ms.openlocfilehash: 9e22b63636980ce64017c950148d9005bf9c2fb1
ms.sourcegitcommit: ed01eaeef9bf488c36556b97247ca440384c0242
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a>Hatalar ve uyarılar

NuGet 4.3.0, hataları ve Uyarıları Bu konu başlığı altında açıklandığı gibi numaralı ve ilgili sorunları gidermek amacıyla ayrıntılı bilgi sağlar. 

Hatalar ve uyarılar burada listelenen yalnızca [PackageReference tabanlı](../Consume-Packages/Package-References-in-Project-Files.md) projeleri ve NuGet 4.3.0. NuGet uyarıları bastırma veya hataları yükseltmesine MSBuild özellikleri de geliştirir. Daha fazla bilgi için bkz: [nasıl yapılır: Derleyici uyarılarını bastırma](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio belgelerinde.

**Hataları**

| Grup | Hata numaraları |
| --- | --- |
| [Geçersiz giriş hataları](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Eksik paket ve proje hataları](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606) |
| [Uyumluluk hataları](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Uyarıları**

| Grup | Uyarı numaraları |
| --- | --- |
| [Geçersiz giriş uyarıları](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Beklenmeyen Paket sürümü uyarıları](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Çözümleyici çakışma uyarıları](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Paket geri dönüş uyarıları](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Akış uyarıları](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet iç hatalar ve uyarılar](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |

## <a name="invalid-input-errors"></a>Geçersiz giriş hataları

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Sorunu** | Bir veya daha fazla çerçeveler proje içermiyor. |
| **Olası nedenler** | Proje içermiyor. bir `TargetFramework` veya `TargetFrameworks` özelliği. |
| **Örnek ileti** | *Proje projA c:\tmp\projA.csproj içinde herhangi bir hedef çerçeve belirtmiyor* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Sorunu** | Girişleri Temizle anahtar sözcüğü ile birlikte birleşimi geçersiz. |
| **Olası nedenler** | CLEAR diğer girişle birleştirilemez. |
| **Örnek ileti** | *'CLEAR' diğer değerler ile birlikte kullanılamaz* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Sorunu** | `PackageTargetFallback`ve `AssetTargetFallback` varlıklar seçmek için farklı bir davranış sağlar ve birlikte kullanılamaz. |
| **Olası nedenler** | Her ikisi de `PackageTargetFallback` ve `AssetTargetFallback` projede mevcut. |
| **Örnek ileti** | *PackageTargetFallback ve AssetTargetFallback birlikte kullanılamaz. Proje ortamından PackageTargetFallback(deprecated) başvuruları kaldırın.* |

## <a name="missing-package-and-project-errors"></a>Eksik paket ve proje hataları

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık grubunun çözülmesi değil. Bu, paket veya projeleri olmayan türleri için genel bir sorundur. |
| **Olası nedenler** | Proje mevcut olmayan bir öğe üzerinde bir bağımlılık içeriyor. |
| **Örnek ileti** | *System.Missing için net45 çözümlenemiyor* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Sorunu** | Paketin tüm kaynakları bulunamıyor. |
| **Olası nedenler** | Doğru paket kaynağı eksik veya paket tanımlayıcısı geçersiz. |
| **Örnek ileti** | *Paket System.Missing bulunamıyor. Bu kimlikle kaynakları hiç paket yok: dotnet çekirdekli, dotnet roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Sorunu** | Paket tanımlayıcısı bulundu, ancak belirtilen bağımlılık aralıkta bir sürüm kaynakları hiçbirinde bulunamıyor. |
| **Olası nedenler** | Doğru paket kaynağı eksik veya bağımlılık aralığı yanlış. Aralığın bir paket ve kullanıcı tarafından belirtilen. Kullanıcı Bu paket proje tarafından doğrudan başvurulduğunda bir sürüme geçiş yapmanız gerekebilir. |
| **Örnek ileti** | *Paketi NuGet.Versioning sürümüyle bulunamadı (> 9.0.1 =)<br/> -nuget.org içinde bulunan 30 sürümler [sürüm en yakın: 4.0.0]<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -9 bulundu NuGetVolatile sürümler [sürüm en yakın: 3.0.0-beta-00032]<br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Sorunu** | Hiçbir kararlı sürümleri bağımlılık aralığı içinde bulunamadı. Yayın öncesi sürümleri bulundu, ancak izin verilmez. |
| **Olası nedenler** | Proje bağımlılık aralığının kararlı sürüm belirtildi. Kullanıcılar, yayın öncesi sürümleri dahil etmek için sürüm aralığı değiştirmeniz gerekir. |
| **Örnek ileti** | *Sürümüyle kararlı paketi NuGet.Versioning bulunamadı (> 3.0.0 =)<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -NuGetVolatile içinde bulunan 9 sürümler [sürüm en yakın: 3.0.0-beta-00032] <br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Sorunu** | Bir ProjectReference mevcut olmayan bir dosyaya işaret eder. |
| **Olası nedenler** | Proje dosyası diskten eksik veya hatalı bir başvurudur. |
| **Örnek ileti** | *Project reference does not exist 'c:\a.csproj'. Proje başvurusu geçerli olduğunu ve proje dosyasının varolduğunu kontrol edin.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Sorunu** | Proje dosyası var, ancak bunun için hiçbir geri yükleme bilgisi verilmedi. |
| **Olası nedenler** | Visual Studio'da bu projenin yüklenmemiş olduğu anlamına gelebilir. Komut satırından bu dosya bozuk veya bu özel Proje okumak geri yükleme için gerekli içeri aktarmaları hedef sonra içermiyor anlamına gelebilir. |
| **Örnek ileti** | *'C:\a.csproj' için proje bilgileri okunamıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Sorunu** | Bağımlılık kısıtlamalarını çözümlenemiyor. |
| **Olası nedenler** | Paketler bağımlılık paketi uçlu aralıkları yerine tam sürümlerinde içerir. |
| **Örnek ileti** | *{İd}'için çakışma istekleri giderilemiyor: {çakışma yolu} Framework: {hedef grafik}* |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a>NU1107 (daha önce NU1607)

| | |
| --- | --- |
| **Sorunu** | Bağımlılık kısıtlamalarını paketler arasında çözümlenemiyor. |
| **Olası nedenler** | Tam sürümleri bağımlılık kısıtlamalar paketlerle sürüm gerekirse artırmak diğer paketleri izin vermez. |
| **Örnek ileti** | *Sürüm çakışması için NuGet.Versioning algılandı. Paket, bu sorunu çözmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (daha önce NU1606)

| | |
| --- | --- |
| **Sorunu** | Döngüsel bağımlılık algılandı. |
| **Olası nedenler** | Bir paket yanlış yazılmış. |
| **Örnek ileti** | *Döngü algılandı: A B -> A ->* |

## <a name="compatibility-errors"></a>Uyumluluk hataları

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık proje Geçerli projeyle uyumlu bir çerçeve içermiyor. |
| **Olası nedenler** | Projenin hedef çerçevesi Süren proje daha yüksek bir sürüme ' dir. |
| **Örnek ileti** | *Proje nokta netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Proje nokta destekler:<br/> -netstandard1.6 (. NETStandard, sürüm = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, sürüm v1.0 =)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık paketi projeyle uyumlu tüm varlıkları içermiyor. |
| **Olası nedenler** | Paket projenin hedef çerçevesi desteklemiyor. |
| **Örnek ileti** | *Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Sorunu** | Paket projenin desteklemiyor `RuntimeIdentifier`. |
| **Olası nedenler** | Paket geçerli desteklemiyor `RuntimeIdentifier`. Değişiklik `RuntimeIdentifier` gerekirse projesinde kullanılan değerler. |
| **Örnek ileti** | *System.Example 1.0.0 a.dll için derleme zamanı referans derlemesini üzerinde net461 sağlar, ancak uyumlu çalışma zamanı derlemesi bulunmuyor.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Sorunu** | Paket özelliklerini veya şu anda yüklü olan NuGet sürümü tarafından desteklenmeyen çerçeveler gerektirir. |
| **Olası nedenler** | Sorunu düzeltmek için NuGet yükseltin. |
| **Örnek ileti** | *'NuGet.Versioning' paketi NuGet İstemcisi Sürüm '5.0.0' gerektirir veya üstü, ancak geçerli NuGet sürümü '4.3.0'. NuGet yükseltmek için lütfen http://docs.nuget.org/consume/installing-nuget için gidin.* |

## <a name="invalid-input-warnings"></a>Geçersiz giriş uyarıları

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Sorunu** | Proje geri yükleme çalışması çalışıyor üzerinde bulunamadı. |
| **Olası nedenler** | Proje eksik. |
| **Örnek ileti** | *'C:\projects\a' klasörü geri yüklenecek bir proje içermiyor.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Sorunu** | `RuntimeSupports`Geçersiz bir profil içerir. |
| **Olası nedenler** | Destekler profili bulunamadı bir `runtime.json` geçerli bağımlılık paketleri dosyasından. |
| **Örnek ileti** | *Bilinmeyen uyumluluk profili: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık proje Nuget'in geri yükleme hedeflerini içe aktarmaz. Bu NU1105 için benzer ancak burada proje atlanır ve tüm geri yükleme başarısız olmasına neden yerine yoksayıldı. Karmaşık çözümlerinde çoğunlukla diğer geri yükleme desteklemeyebilir proje türleri vardır. |
| **Olası nedenler** | Bu ortak özellik/geri yükleme otomatik olarak içeri hedefleri almayın projelerde meydana gelebilir. Proje geri gerekmez, bu yoksayılabilir. |
| **Örnek ileti** | *Proje 'c:\a.csproj' için geri atlanıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.* |

## <a name="unexpected-package-version-warnings"></a>Beklenmeyen Paket sürümü uyarıları

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Sorunu** | Bir doğrudan proje bağımlılığı belirtilen proje daha yüksek bir sürüme indirgenmesine. |
| **Olası nedenler** | Başka bir bağımlılık paket daha yüksek bir sürüm gereklidir ve paket indirgenmesine. |
| **Örnek ileti** | *Bağımlılık belirtildi NuGet.Versioning (> = 3.5.0) ancak 4.0.0 NuGet.Versioning ile sonuçlandı.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Sorunu** | Bir paket bağımlılığı alt sınır eksik. Bunu bulmak geri yükleme izin vermeyen *en iyi eşleşmeyi*. Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float. Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir. |
| **Olası nedenler** | Bu genellikle hata yazma bir pakettir. |
| **Örnek ileti** | *NuGet.Packaging 4.0.0 (bunlar dahil) bir alt sınır için bağımlılık NuGet.Versioning (> 3.5.0) sağlamaz. Yaklaşık en iyi eşleşme 3.6.0, çözüldü.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Sorunu** | Bir paket bağımlılığı bulunamadı bir sürüm belirtildi. Bunun yerine, daha yüksek bir sürüm ne paket karşı yönetilmiyor öğesinden farklı kullanıldı.<br/><br/>Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*. Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float. Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir. |
| **Olası nedenler** | Paket kaynaklarını beklenen alt sınır sürüm içermiyor. Beklenen paket bırakılmamışsa değilse bu hata yazma bir paket olabilir. |
| **Örnek ileti** | NuGet.Packaging 4.0.0 NuGet.Versioning üzerinde bağlıdır (> = 4.0.0) ancak 4.0.0 bulunamadı. Yaklaşık en iyi eşleşme 5.0.0, çözüldü. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Sorunu** | Proje bağımlılığı alt sınır tanımlamıyor.<br/><br/>Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*. Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float. Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir. |
| **Olası nedenler** | Projenin *PackageReference* *sürüm* özniteliği alt sınırı içerecek şekilde güncelleştirilmesi gerekir. |
| **Örnek ileti** | *Bağımlılık NuGet.Versioning proje (< 9.0.0 =) doe (bunlar dahil) bir alt sınır içeremez. Alt sınır tutarlı geri yükleme sonuçlar sağlamak için bağımlılık sürümünü içerir.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık paketi bir paket geri yükleme sonuçta çözülmüş daha yüksek bir sürüm bir sürüm kısıtlaması belirtildi. |
| **Olası nedenler** | Paketleri çözülürken yakın WINS. Grafikte yakın bir paket uzaktaki bir paket silmiş. |
| **Örnek ileti** | *Paket indirgeme algılandı: 4.0.0 gelen NuGet.Versioning 3.5.0 için. Paketi farklı bir sürüm seçmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 NuGet.Versioning 4.0.0 ->* |

## <a name="resolver-conflict-warnings"></a>Çözümleyici çakışma uyarıları

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık kısıtlaması izin verdiğinden daha yüksek bir çözümleme paketidir. Bazı durumlarda bu bilinen bir durumdur ve uyarıyı gizlenebilir. |
| **Olası nedenler** | Doğrudan bir proje tarafından başvurulan paket diğer paketlerinden bağımlılık kısıtlamalarını geçersiz kılar.   |
| **Örnek ileti** | *Bağımlılık kısıtlaması dışında algılanan Paket sürümü: x 1.0.0 (= 1.0.0) y gerektiriyor, ancak sürüm y 2.0.0 çözülmüş.* |

## <a name="package-fallback-warnings"></a>Paket geri dönüş uyarıları

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Sorunu** | *PackageTargetFallback/AssetTargetFallback* was used to select assets from a package. Bu varlıklar % 100 uyumlu olmayabilir bilmeniz kullanıcı izin vermek için bir uyarıdır. |
| **Olası nedenler** | Paket proje framework desteklemiyor. |
| **Örnek ileti** | *Paket 'NuGet.Versioning', 'taşınabilir net45 + olduğu win8' yerine projenin hedef çerçevesi 'netstandard1.5' kullanılarak geri yüklendi. Bu paket projenizi ile tamamen uyumlu olmayabilir.* |

## <a name="feed-warnings"></a>Akış uyarıları

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Sorunu** | Akış okunurken bir hata oluştu, `IgnoreFailedSources` ayarlanır için önemli olmayan uyarı dönüştürme true. Bu herhangi bir iletisi içerebilir ve genel. |
| **Olası nedenler** | Kaynağı geçersiz. |
| **Örnek ileti** | yok |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet iç hatalar ve uyarılar

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Sorunu** | NuGet from olmayan belirli bir iç hata. |
| **Olası nedenler** | Daha fazla bilgi için günlükleri denetleyin |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Sorunu** | Belirsiz bir iç uyarıyı NuGet engeller. |
| **Olası nedenler** | Daha fazla bilgi için günlükleri denetleyin |
