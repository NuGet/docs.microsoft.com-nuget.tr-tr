---
title: NuGet CLı ortam değişkenleri
description: NuGet. exe ortam değişkenlerine yönelik başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b04efaecce1d5bc892dfc48ae3e872d80aad209d
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328353"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLı ortam değişkenleri

NuGet. exe CLı 'nın davranışı, bilgisayar genelinde, Kullanıcı veya işlem düzeylerinde NuGet. exe ' yi etkileyen bir dizi ortam değişkeni aracılığıyla yapılandırılabilir. Ortam değişkenleri, her zaman `NuGet.Config` dosyalardaki ayarları geçersiz kılar ve derleme sunucularının herhangi bir dosyayı değiştirmeden uygun ayarları değiştirmesine izin verir.

Genel olarak, komut satırında veya NuGet yapılandırma dosyalarında doğrudan belirtilen seçenekler önceliğe sahiptir, ancak *FORCE_NUGET_EXE_INTERACTIVE*gibi birkaç özel durum vardır. NuGet. exe ' nin farklı bilgisayarlar arasında farklı davrandığını fark ederseniz, bir ortam değişkeni nedeni olabilir. Örneğin, Azure Web Apps kudu (dağıtım sırasında kullanılır), paket geri yükleme performansını hızlandırmak ve disk alanından tasarruf etmek için *NUGET_XMLDOC_MODE* *olarak ayarlanmıştır* .

NuGet CLı, proje dosyalarını okumak için MSBuild kullanır. Tüm ortam değişkenleri, MSBuild değerlendirmesi sırasında [Özellikler](/visualstudio/msbuild/msbuild-command-line-reference) olarak kullanılabilir.
NuGet paketinde belgelenen özelliklerin listesi [ve MSBuild hedefleri olarak geri yükleme](../msbuild-targets.md#restore-properties) , ortam değişkenleri olarak da ayarlanabilir.

| Değişken | Açıklama | Açıklamalar |
| --- | --- | --- |
| http_proxy | NuGet HTTP işlemleri için kullanılan http proxy 'si. | Bu, olarak `http://<username>:<password>@proxy.com`belirtilir. |
| no_proxy | Proxy 'yi kullanarak atlamak için etki alanlarını yapılandırır. | Virgülle (,) ayrılmış etki alanları olarak belirtilir. |
| EnableNuGetPackageRestore | NuGet 'in, geri yükleme sırasında Package gerekliyse, açıkça izin verip vermediği için bayrak. | Belirtilen bayrak *doğru* veya *1*olarak kabul edilir, bayrak ayarlanmamış gibi başka bir değer kabul edilir. |
| NUGET_EXE_NO_PROMPT | Kimlik bilgilerini sormak için exe 'yi engeller. | Null veya boş dize hariç herhangi bir değer, bu bayrak ayarlanmış/doğru olarak değerlendirilir. |
| FORCE_NUGET_EXE_INTERACTIVE | Etkileşimli moda zorlamak için genel ortam değişkeni. | Null veya boş dize hariç herhangi bir değer, bu bayrak ayarlanmış/doğru olarak değerlendirilir. |
| NUGET_PACKAGES | Genel paketleri [ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi *genel paketler* klasörü için kullanılacak yol. | Mutlak yol olarak belirtilir. |
| NUGET_FALLBACK_PACKAGES | Küresel geri dönüş paketleri klasörleri. | Noktalı virgülle ayrılmış mutlak klasör yolları (;). |
| NUGET_HTTP_CACHE_PATH | [Genel paketleri ve önbellek klasörlerini yönetme](../../consume-packages/managing-the-global-packages-and-cache-folders.md)konusunda açıklandığı gibi, *http önbelleği* klasörü için kullanılacak yol. | Mutlak yol olarak belirtilir. |
| NUGET_PERSIST_DG | DG dosyalarının (MSBuild 'ten toplanan verilerin) kalıcı olup olmadığını belirten bayrak. | *True* veya *false* olarak belirtilir (varsayılan), NUGET_PERSIST_DG_PATH ayarlanmadı ayarı geçici dizine (geçerli ortamda geçici dizinde nugetkaralama klasörü) depolanacaktır. |
| NUGET_PERSIST_DG_PATH | DG dosyalarını kalıcı hale getirme yolu. | Mutlak yol olarak belirtilen bu seçenek yalnızca *NUGET_PERSIST_DG* true olarak ayarlandığında kullanılır. |
| NUGET_RESTORE_MSBUILD_ARGS | Ek MSBuild bağımsız değişkenlerini ayarlar. | Aynı bağımsız değişkenleri MSBuild. exe ' ye nasıl geçicağiyle aynı şekilde geçirin. Komut satırından değer çubuğuna foo bir proje özelliği ayarlamaya bir örnek/p: foo = bar olacaktır |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild günlüğü ayrıntı düzeyini ayarlar. | Varsayılan değer *quiet* ("/v: q"). Olası değerler *q [UIET]* , *m [inhayvan]* , *n [ormal]* , *d [ekuyruklu]* ve *diag [nostic]* . |
| NUGET_SHOW_STACK | Tam özel durumun (yığın izleme dahil) kullanıcıya görüntülenip görüntülenmeyeceğini belirler. | *Doğru* veya *yanlış* olarak belirtilir (varsayılan). |
| NUGET_XMLDOC_MODE | Derlemeler XML belgesi dosya ayıklamanın nasıl işleneceğini belirler. | Desteklenen modlar *atlayın* (XML belge dosyalarını ayıklamayın), *Sıkıştır* (XML doc dosyalarını zip arşivi olarak depola) veya *none* (varsayılan, XML doc dosyalarını normal dosyalar olarak değerlendir). |
| NUGET_CERT_REVOCATION_MODE | Bir paketi imzalamak için kullanılan sertifikanın iptal durumu denetiminin, imzalanmış bir paket yüklenirken veya geri yüklendiğinde gerçekleştirileceğini belirler. Ayarlanmazsa, varsayılan olarak `online`olur.| Olası değerler *çevrimiçi* (varsayılan), *çevrimdışı*.  [NU3028](../errors-and-warnings/NU3028.md) ile ilgili |

