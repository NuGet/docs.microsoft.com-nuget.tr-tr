---
title: NuGet hataları ve Uyarıları başvurusu
description: Uyarıları ve hataları Nuget'ten çeşitli NuGet işlemleri sırasında verilen başvurusunu tamamlayın.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
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
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a>Hatalar ve uyarılar

NuGet 4.3.0+, hataları ve Uyarıları Bu konu başlığı altında açıklandığı gibi numaralı ve ilgili sorunları gidermek amacıyla ayrıntılı bilgi sağlar.

Hatalar ve uyarılar burada listelenen yalnızca [PackageReference tabanlı](../consume-packages/package-references-in-project-files.md) projeleri ve NuGet 4.3.0+. NuGet uyarıları bastırma veya hataları yükseltmesine MSBuild özellikleri de geliştirir. Daha fazla bilgi için bkz: [nasıl yapılır: Derleyici uyarılarını bastırma](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio belgelerinde.

**Hataları**

| Grup | Hata numaraları |
| --- | --- |
| [Geçersiz giriş hataları](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Eksik paket ve proje hataları](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (daha önce NU1607) [NU1108](#nu1108) (daha önce NU1606) |
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
| [İmzalı Paketleri (oluşturma ve doğrulama)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Geçersiz giriş hataları

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Sorunu** | Bir veya daha fazla çerçeveler proje içermiyor. |
| **Örnek ileti** | *Proje projA c:\tmp\projA.csproj içinde herhangi bir hedef çerçeve belirtmiyor* |
| **Çözüm** | Ekleme bir `TargetFramework` veya `TargetFrameworks` belirtilen proje dosyasına özelliği. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Sorunu** | Girişleri Temizle anahtar sözcüğü ile birlikte birleşimi geçersiz. |
| **Örnek ileti** | *'CLEAR' diğer değerler ile birlikte kullanılamaz* |
| **Çözüm** | CLEAR başına kullanın ve diğer tüm girişleri atlayabilirsiniz. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Sorunu** | `PackageTargetFallback` ve `AssetTargetFallback` varlıklar seçmek için farklı bir davranış sağlar ve birlikte kullanılamaz. |
| **Örnek ileti** | *PackageTargetFallback ve AssetTargetFallback birlikte kullanılamaz. Proje ortamından PackageTargetFallback(deprecated) başvuruları kaldırın.* |
| **Çözüm** | Kullanım dışı kaldırmak `PackageTargetFallback` proje öğesi. |

## <a name="missing-package-and-project-errors"></a>Eksik paket ve proje hataları

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık grubunun çözülmesi değil. Bu, paket veya projeleri olmayan türleri için genel bir sorundur. |
| **Örnek ileti** | *System.Missing için net45 çözümlenemiyor* |
| **Çözüm** | Proje dosyasını açın ve bağımlılıklarını listesini inceleyin. Her bir bağımlılığın kullanmakta olduğunuz paket kaynaklarını üzerinde var olduğunu ve paket projenin hedef çerçevesi desteklediğini denetleyin. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Sorunu** | Paketin tüm kaynakları bulunamıyor. |
| **Örnek ileti** | *Paket System.Missing bulunamıyor. Bu kimlikle kaynakları hiç paket yok: dotnet çekirdekli, dotnet roslyn, nuget.org* |
| **Çözüm** | Doğru paket tanımlayıcısı ve sürüm numarasını kullandığınızdan emin olmak için Visual Studio Proje bağımlılıkları inceleyin. Ayrıca denetleyin [NuGet Yapılandırması](../consume-packages/Configuring-NuGet-Behavior.md) paket kaynaklarını tanımlar, kullanılmasını bekler. Sahip paketleri kullanıyorsanız [anlamsal sürüm oluşturma 2.0.0](../reference/package-versioning.md#semantic-versioning-200), lütfen akışı, V3 kullandığınızdan emin olun `https://api.nuget.org/v3/index.json`, [NuGet Yapılandırması](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Sorunu** | Paket tanımlayıcısı bulundu, ancak belirtilen bağımlılık aralıkta bir sürüm kaynakları hiçbirinde bulunamıyor. Aralığın bir paket ve kullanıcı tarafından belirtilen. |
| **Örnek ileti** | *Paketi NuGet.Versioning sürümüyle bulunamadı (> 9.0.1 =)<br/> -nuget.org içinde bulunan 30 sürümler [sürüm en yakın: 4.0.0]<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -9 bulundu NuGetVolatile sürümler [sürüm en yakın: 3.0.0-beta-00032]<br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu* |
| **Çözüm** | Paket sürümü düzeltmek için proje dosyasını düzenleyin. Ayrıca denetleyin [NuGet Yapılandırması](../consume-packages/Configuring-NuGet-Behavior.md) paket kaynaklarını tanımlar, kullanılmasını bekler. Bu paket proje tarafından doğrudan başvurulduğunda requeted version değiştirmeniz gerekebilir. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Sorunu** | Proje kararlı bir sürüm bağımlılığı aralığı için belirtilen ancak hiçbir kararlı sürümleri bu aralıkta bulundu. Yayın öncesi sürümleri bulundu, ancak izin verilmez. |
| **Örnek ileti** | *Sürümüyle kararlı paketi NuGet.Versioning bulunamadı (> 3.0.0 =)<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -NuGetVolatile içinde bulunan 9 sürümler [sürüm en yakın: 3.0.0-beta-00032] <br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu* |
| **Çözüm** |  Yayın öncesi sürümleri dahil etmek için proje dosyasında sürüm aralığı düzenleyin. Bkz: [paket sürüm](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Sorunu** | Bir ProjectReference mevcut olmayan bir dosyaya işaret eder. |
| **Örnek ileti** | *Proje Başvurusu 'c:\a.csproj' yok. Proje başvurusu geçerli olduğunu ve proje dosyasının varolduğunu kontrol edin.* |
| **Çözüm** | Proje dosyası ya da başvuruda bulunulan proje yolunu düzeltin veya başvuruyu kaldırmak üzere Düzenle artık ihtiyaç duyduğunuzda değerlerinin. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Sorunu** | Proje dosyası var, ancak bunun için hiçbir geri yükleme bilgisi verilmedi. |
| **Örnek ileti** | *'C:\a.csproj' için proje bilgileri okunamıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.* |
| **Çözüm** | Visual Studio'da hata projenin, bu durumda yeniden içinde proje, kaldırılmış olduğunu anlamına gelebilir. Komut satırından bu dosya bozuk veya bu özel "içeri aktarmalar sonra" içermiyor anlamına gelebilir proje okumak geri yükleme için gereken hedef. Proje dosyası geçerli olduğundan ve "sonra içeri aktarmalar" hedef içerdiğini denetleyin. |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Sorunu** | Bağımlılık kısıtlamalarını çözümlenemiyor. |
| **Örnek ileti** | *{İd}'için çakışma istekleri giderilemiyor: {çakışma yolu} Framework: {hedef grafik}* |
| **Çözüm** | Bir tam sürümü yerine bağımlılık daha uçlu aralıklarını belirtmek için proje dosyasını düzenleyin. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (daha önce NU1607)

| | |
| --- | --- |
| **Sorunu** | Bağımlılık kısıtlamalarını paketler arasında çözümlenemiyor. |
| **Örnek ileti** | *Sürüm çakışması için NuGet.Versioning algılandı. Paket, bu sorunu çözmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |
| **Çözüm** | Tam sürümleri bağımlılık kısıtlamalar paketlerle sürüm gerekirse artırmak diğer paketleri izin vermez. Gerekli tam sürümü ile doğrudan (proje dosyasında) projesine bir başvuru ekleyin. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (daha önce NU1606)

| | |
| --- | --- |
| **Sorunu** | Döngüsel bağımlılık algılandı. |
| **Örnek ileti** | *Döngü algılandı: A B -> A ->* |
| **Çözüm** | Paket yanlış yazılmış; hatayı düzeltmek için paket sahibine başvurun. |

## <a name="compatibility-errors"></a>Uyumluluk hataları

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık proje Geçerli projeyle uyumlu bir çerçeve içermiyor. Genellikle, projenin hedef çerçevesi Süren proje daha yüksek bir sürüme ' dir. |
| **Örnek ileti** | *Proje nokta netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Proje nokta destekler:<br/> -netstandard1.6 (. NETStandard, sürüm = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, sürüm v1.0 =)* |
| **Çözüm** | Projenin hedef çerçevesi Süren proje eşit veya daha düşük bir sürümden değiştirin. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık paketi projeyle uyumlu tüm varlıkları içermiyor. |
| **Örnek ileti** | *Paket System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Paket System.ComponentModel.EventBasedAsync 4.0.11 destekler:<br/> -monoandroid10 (MonoAndroid, sürüm = v1.0)<br/> -monotouch10 (MonoTouch, sürüm = v1.0)<br/> -net45 (. NETFramework, sürümü v4.5 =)<br/> -netcore50 (. NETCore, sürüm = v5.0)<br/> -netstandard1.0 (. NETStandard, sürüm = v1.0)<br/> -taşınabilir net45 olduğu win8 + wp8 + wpa81 (. NETPortable, sürüm v0.0, profil = Profile259 =)<br/> -olduğu win8 (Windows, sürüm = v8.0)<br/> -wp8 (WindowsPhone, sürüm v8.0 =)<br/> -wpa81 (WindowsPhoneApp, sürüm v8.1 =)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Çözüm** | Projenin hedef çerçevesi paket destekleyen bir değiştirin. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Sorunu** | Paket projenin desteklemiyor `RuntimeIdentifier`. |
| **Örnek ileti** | *System.Example 1.0.0 a.dll için derleme zamanı referans derlemesini üzerinde net461 sağlar, ancak uyumlu çalışma zamanı derlemesi bulunmuyor.* |
| **Çözüm** | Değişiklik `RuntimeIdentifier` gerektiğinde projesinde kullanılan değerler. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Sorunu** | Paket özelliklerini veya şu anda yüklü olan NuGet sürümü tarafından desteklenmeyen çerçeveler gerektirir. |
| **Örnek ileti** | *'NuGet.Versioning' paketi NuGet İstemcisi Sürüm '5.0.0' gerektirir veya üstü, ancak geçerli NuGet sürümü '4.3.0'.* |
| **Çözüm** | NuGet daha yeni bir sürümü yükleyin. Bkz: [yükleme NuGet istemci araçları](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Geçersiz giriş uyarıları

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Sorunu** | Proje geri yükleme çalışması çalışıyor üzerinde bulunamadı. |
| **Örnek ileti** | *'C:\projects\a' klasörü geri yüklenecek bir proje içermiyor.* |
| **Çözüm** | Nuget restore bir proje içeren bir klasörde çalıştırın. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Sorunu** | `RuntimeSupports` Geçersiz bir profil içerir. Genellikle, destekler profili bulunamadı bir `runtime.json` geçerli bağımlılık paketleri dosyasından.|
| **Örnek ileti** | *Bilinmeyen uyumluluk profili: aaa* |
| **Çözüm** | Denetleme `RuntimeSupports` projenizdeki değeri. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık proje Nuget'in geri yükleme hedeflerini içe aktarmaz. Bu NU1105 için benzer ancak burada proje atlanır ve tüm geri yükleme başarısız olmasına neden yerine yoksayıldı. Karmaşık çözümlerinde çoğunlukla diğer geri yükleme desteklemeyebilir proje türleri vardır. |
| **Örnek ileti** | *Proje 'c:\a.csproj' için geri atlanıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.* |
| **Çözüm** | Bu ortak özellik/geri yükleme otomatik olarak içeri hedefleri almayın projelerde meydana gelebilir. Proje geri gerekmez, bu yoksayılabilir. Aksi takdirde, geri yükleme hedeflerini eklemek için etkilenen proje düzenleyin. |

## <a name="unexpected-package-version-warnings"></a>Beklenmeyen Paket sürümü uyarıları

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Sorunu** | Bir doğrudan proje bağımlılığı belirtilen proje daha yüksek bir sürüme indirgenmesine. |
| **Örnek ileti** | *Bağımlılık belirtildi NuGet.Versioning (> = 3.5.0) ancak 4.0.0 NuGet.Versioning ile sonuçlandı.* |
| **Çözüm** | Proje bağımlılığı uygun bir sürüme güncelleştirin. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Sorunu** | Bir paket bağımlılığı alt sınır eksik. Bunu bulmak geri yükleme izin vermeyen *en iyi eşleşmeyi*. Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float. Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir. |
| **Örnek ileti** | *NuGet.Packaging 4.0.0 (bunlar dahil) bir alt sınır için bağımlılık NuGet.Versioning (> 3.5.0) sağlamaz. Yaklaşık en iyi eşleşme 3.6.0, çözüldü.* |
| **Çözüm** | Bu genellikle hata yazma bir pakettir. Bu sorunu çözmek için paket yazarına danışın. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Sorunu** | Bir paket bağımlılığı bulunamadı bir sürüm belirtildi. Genellikle, paket kaynaklarını beklenen alt sınır sürüm içermiyor. Bunun yerine, daha yüksek bir sürüm ne paket karşı yönetilmiyor öğesinden farklı kullanıldı.<br/><br/>Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*. Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float. Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir. |
| **Örnek ileti** | NuGet.Packaging 4.0.0 NuGet.Versioning üzerinde bağlıdır (> = 4.0.0) ancak 4.0.0 bulunamadı. Yaklaşık en iyi eşleşme 5.0.0, çözüldü. |
| **Çözüm** | Beklenen paket bırakılmamışsa değilse bu hata yazma bir paket olabilir. Bu sorunu çözmek için paket yazarına danışın. Paket yayımlanan, kullanmakta olduğunuz paket kaynaklarını üzerinde kullanılabilir olduğunu denetleyin. Özel kaynak kullanıyorsanız, akış paketi güncelleştirmeniz gerekebilir. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Sorunu** | Proje bağımlılığı alt sınır tanımlamıyor.<br/><br/>Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*. Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float. Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir. |
| **Örnek ileti** | *Bağımlılık NuGet.Versioning proje (< 9.0.0 =) doe (bunlar dahil) bir alt sınır içeremez. Alt sınır tutarlı geri yükleme sonuçlar sağlamak için bağımlılık sürümünü içerir.* |
| **Çözüm** | Projenin güncelleştirme `PackageReference` `Version` alt sınır eklenecek özniteliği. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Sorunu** | Bir bağımlılık paketi bir paket geri yükleme sonuçta çözülmüş daha yüksek bir sürüm bir sürüm kısıtlaması belirtildi. Diğer bir deyişle, paketleri çözülürken "en yakın WINS" kural nedeniyle, grafik yakın bir pakette uzaktaki bir paket silmiş. |
| **Örnek ileti** | *Paket indirgeme algılandı: 4.0.0 gelen NuGet.Versioning 3.5.0 için. Paketi farklı bir sürüm seçmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 NuGet.Versioning 4.0.0 ->* |
| **Çözüm** | Proje için kullanmak istediğiniz paketinin daha yüksek sürümünü doğrudan bir başvuru ekleyin. |

## <a name="resolver-conflict-warnings"></a>Çözümleyici çakışma uyarıları

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Sorunu** | Çözümlenen bir paketi bir bağımlılık kısıtlaması izin verdiğinden daha yüksektir. Başka bir deyişle, doğrudan bir proje tarafından başvurulan paket diğer paketlerinden bağımlılık kısıtlamalarını geçersiz kılar.|
| **Örnek ileti** | *Bağımlılık kısıtlaması dışında algılanan Paket sürümü: x 1.0.0 (= 1.0.0) y gerektiriyor, ancak sürüm y 2.0.0 çözülmüş.* |
| **Çözüm** | Bazı durumlarda bu bilinen bir durumdur ve uyarıyı gizlenebilir. Aksi durumda, kendi sürüm kısıtlamaları genişletmek için paketi projenin referansı değiştirin. |

## <a name="package-fallback-warnings"></a>Paket geri dönüş uyarıları

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Sorunu** | `PackageTargetFallback` / `AssetTargetFallback` varlıklar bir paket seçmek için kullanıldı. Uyarı varlıklar % 100 uyumlu olmayabilir bilmenize olanak tanır. |
| **Örnek ileti** | *Paket 'NuGet.Versioning', 'taşınabilir net45 + olduğu win8' yerine projenin hedef çerçevesi 'netstandard1.5' kullanılarak geri yüklendi. Bu paket projenizi ile tamamen uyumlu olmayabilir.* |
| **Çözüm** | Projenin hedef çerçevesi paket destekleyen bir değiştirin. |

## <a name="feed-warnings"></a>Akış uyarıları

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Sorunu** | Akış okunurken bir hata oluştu, `IgnoreFailedSources` ayarlanır için önemli olmayan uyarı dönüştürme true. Bu herhangi bir iletisi içerebilir ve genel. |
| **Örnek ileti** | yok |
| **Çözüm** | Geçerli kaynakları belirtmek için yapılandırmasını düzenleyin. |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet iç hatalar ve uyarılar

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Sorunu** | NuGet from olmayan belirli bir iç hata. |
| **Çözüm** | Daha fazla bilgi için günlükleri denetleyin |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Sorunu** | Belirsiz bir iç uyarıyı NuGet engeller. |
| **Çözüm** | Daha fazla bilgi için günlükleri denetleyin |

## <a name="signed-packages-creation-and-verification"></a>İmzalı Paketleri (oluşturma ve doğrulama)

*NuGet 4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008)  |  [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Sorunu** | Belirli olmayan bir hata paket imzalama ile ilgili ve paket doğrulama imzalanmış. |
| **Çözüm** | Daha fazla bilgi için günlükleri denetleyin. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Sorunu** | Geçersiz bağımsız değişkenler ya da [oturum komutu](../tools/cli-ref-sign.md) veya [komut doğrulama](../tools/cli-ref-verify.md). |
| **Çözüm** | Denetleyin ve sağlanan bağımsız değişkenler düzeltin. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Sorunu** | `-Timestamper` Seçeneği ile belirtilmemiş [nuget oturum komutu](../tools/cli-ref-sign.md). |
| **Örnek ileti** | *'-Timestamper' seçeneği sağlanan değil. İmzalı paket zaman damgalı olmaz.* |
| **Çözüm** | Belirtin `-Timestamper` seçeneğini `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Sorunu** | İmzasız bir paket için sağlanan [nuget doğrulayın komutu](../tools/cli-ref-verify.md). |
| **Çözüm** | Çalıştırma `nuget verify` imzalı paketine sahip. Bkz: [bir paket oturum](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Sorunu** | Paket bütünlük denetimi başarısız oldu, imzalı itibaren imzalı paketi ile uğradığını anlamına gelir. |
| **Çözüm** | Virüsten koruma yazılımı ile bilgisayarınızı tarayın. Ardından paket bilgisayardan kaldırın, yükleyin ve işlemi yeniden deneyin. Sorun devam ederse, paket kaynağının sahibi ve paket sahibine başvurun. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Sorunu** | Sertifika zinciri oluşturma için birincil imza başarısız oldu. Birincil imzalama sertifikası iptal edildi, güvenilmeyen, veya sertifika için iptal bilgilerini kullanılamıyor. |
| **Örnek ileti** | *Uyarı: NU3018: iptal işlevi sertifika için İptal denetleyemedi.* |
| **Çözüm** | Güvenilir ve geçerli bir sertifika kullanın. İnternet bağlantısını denetleyin. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Sorunu** | Sertifika zinciri oluşturma zaman damgası imza için başarısız oldu. Zaman damgası imzalama sertifikası iptal edildi, güvenilmeyen, veya sertifika için iptal bilgilerini kullanılamıyor. |
| **Örnek ileti** | *Uyarı: NU3028: iptal işlevi sertifika için İptal denetleyemedi.* |
| **Çözüm** | Güvenilir ve geçerli bir sertifika kullanın. İnternet bağlantısını denetleyin. |
