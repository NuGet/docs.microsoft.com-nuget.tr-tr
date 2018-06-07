---
title: NuGet CLI ortam değişkenleri
description: Nuget.exe ortam değişkenleri için başvurusu
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 50bf8b469eda423db7665323823a2daf3f3aa41d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817079"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI ortam değişkenleri

CLI nuget.exe davranışını nuget.exe bilgisayar genelinde kullanıcı etkileyen veya düzeyleri işlem ortam değişkenleri bir dizi yapılandırılabilir. Ortam değişkenleri her zaman tüm ayarları geçersiz kılar `NuGet.Config` izin vererek dosyaları, derleme sunucuları dosyalarla değiştirmeden uygun ayarları değiştirmek için.

Genel olarak, doğrudan komut satırında veya NuGet yapılandırma dosyaları belirtilen seçenekler önceliğe sahip, ancak birkaç istisnası vardır gibi *FORCE_NUGET_EXE_INTERACTIVE*. Bu nuget.exe farklı bilgisayarlar arasında farklı şekilde davranan bulursanız, bir ortam değişkeni neden olabilir. Örneğin, Azure Web uygulamaları (dağıtımı sırasında kullanılan) Kudu sahip *NUGET_XMLDOC_MODE* kümesine *atla* paket geri yükleme performansını hızlandırmak ve disk alanı kaydetmek için.

| Değişken | Açıklama | Açıklamalar |
| --- | --- | --- |
| http_proxy | Http proxy NuGet HTTP işlemler için kullanılır. | Bu olarak belirtilen `http://<username>:<password>@proxy.com`. |
| no_proxy | Proxy kullanarak atlamak için etki alanlarını yapılandırır. | Etki alanları virgülle (,) ayırarak olarak belirtilmiş. |
| EnableNuGetPackageRestore | NuGet örtük olarak izni, geri yükleme paketi tarafından gerekip gerekmediğini vermelisiniz varsa için bayrak. | Belirtilen bayrak olarak değerlendirilir *true* veya *1*, bayrak olarak kabul başka bir değer ayarlanmamış. |
| NUGET_EXE_NO_PROMPT | Kimlik bilgileri için exe engeller. | Null veya boş dize değerlendirilir dışında herhangi bir değer bu bayrak kümesi/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Etkileşimli mod zorlamak için genel bir ortam değişkenidir. | Null veya boş dize değerlendirilir dışında herhangi bir değer bu bayrak kümesi/true. |
| NUGET_PACKAGES | İçin kullanılacak yol *paketleri genel* açıklandığı gibi klasör [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Mutlak yolu belirtilmelidir. |
| NUGET_FALLBACK_PACKAGES | Genel geri dönüş paketleri klasörler. | Noktalı virgül (;) ayrılmış mutlak klasörü yollar. |
| NUGET_HTTP_CACHE_PATH | İçin kullanılacak yol *http önbellek* açıklandığı gibi klasör [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Mutlak yolu belirtilmelidir. |
| NUGET_PERSIST_DG | Dg dosyaları (MSBuild toplanan verileri) kalıcı ise belirten bayrak. | Olarak belirtilen *true* veya *false* (varsayılan), NUGET_PERSIST_DG_PATH değil ayarlarsanız, geçici dizine (geçerli ortam temp dizininde NuGetScratch klasör) depolanır. |
| NUGET_PERSIST_DG_PATH | Dg dosyaları kalıcı hale getirmek için yolu. | Mutlak yol olarak, bu seçenek yalnızca kullanılan olduğunda belirtilmiştir *NUGET_PERSIST_DG* ayarlanmış true. |
| NUGET_RESTORE_MSBUILD_ARGS | Ek MSBuild bağımsız değişkenleri ayarlar. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild günlük ayrıntı ayarlar. | Varsayılan değer *sessiz* ("/ v: q"). Olası değerler *q [uiet]*, *m [en az sıfır]*, *n [ormal]*, *d [kincil]*, ve *tanı [nostic]*. |
| NUGET_SHOW_STACK | (Yığın izleme dahil) tam özel durum kullanıcıya görüntülenmesi gerekip gerekmediğini belirler. | Olarak belirtilen *true* veya *false* (varsayılan). |
| NUGET_XMLDOC_MODE | Derlemeleri XML belge dosyası ayıklama nasıl işleneceğini belirler. | Desteklenen modlar *atla* (XML belge dosyalarını ayıklayın değil), *Sıkıştır* (zip arşivini XML belge dosyalarını depolamak) veya *hiçbiri* (varsayılan, XML belge dosyalarını normal ele alın dosyaları). |
