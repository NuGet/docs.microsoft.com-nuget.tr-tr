---
title: NuGet CLI ortam değişkenleri
description: Nuget.exe ortam değişkenleri için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: fd5824d1c5e05df08301dac1cf656ba1d5ca75cd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551744"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI ortam değişkenleri

Nuget.exe CLI davranışını etkileyen nuget.exe bilgisayar genelinde kullanıcı veya işlem düzeylerini ortam değişkenleri, bir dizi yapılandırılabilir. Ortam değişkenleri her zaman herhangi bir ayarı geçersiz kılma `NuGet.Config` dosyaları izin vererek, derleme sunucuları, herhangi bir dosya değiştirmeden uygun ayarları değiştirmek için.

Genel olarak, doğrudan komut satırında veya NuGet yapılandırma dosyalarında belirtilen önceliği vardır, ancak birkaç özel durum vardır gibi *FORCE_NUGET_EXE_INTERACTIVE*. Bu nuget.exe farklı bilgisayarlar arasında farklı davranır bulursanız, bir ortam değişkeni neden olabilir. Örneğin, Azure Web Apps (dağıtım sırasında kullanılan) Kudu sahip *NUGET_XMLDOC_MODE* kümesine *atla* paket geri yükleme performansını hızlandırmak ve disk alanından kazanmak için.

| Değişken | Açıklama | Açıklamalar |
| --- | --- | --- |
| http_proxy | NuGet HTTP işlemleri için kullanılan http Proxy'i. | Bu olarak belirtilecek `http://<username>:<password>@proxy.com`. |
| no_proxy | Proxy kullanarak atlamak için etki alanlarını yapılandırır. | Etki alanları (,) virgülle ayrılmış olarak belirtildi. |
| EnableNuGetPackageRestore | NuGet örtük olarak izni, geri yükleme paketi tarafından gerekip gerekmediğini vermelisiniz varsa için bayrak. | Belirtilen bayrak olarak kabul edildiği *true* veya *1*, bayrak olarak kabul başka bir değer ayarlanmadı. |
| NUGET_EXE_NO_PROMPT | Yüklediğinizde kimlik bilgileri için exe engeller. | Null veya boş dize değerlendirilir dışında herhangi bir değer bu bayrak kümesi/true. |
| FORCE_NUGET_EXE_INTERACTIVE | Etkileşimli mod zorlamak için genel ortam değişkeni'ni kullanın. | Null veya boş dize değerlendirilir dışında herhangi bir değer bu bayrak kümesi/true. |
| NUGET_PACKAGES | İçin kullanılacak yol *genel paketleri* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Mutlak yol belirtildi. |
| NUGET_FALLBACK_PACKAGES | Genel geri dönüş paketleri klasörler. | Noktalı virgülle (;) ayrılmış mutlak klasör yolları. |
| NUGET_HTTP_CACHE_PATH | İçin kullanılacak yol *http önbellek* üzerinde açıklandığı gibi klasör [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). | Mutlak yol belirtildi. |
| NUGET_PERSIST_DG | Dg dosyaları (MSBuild'den toplanan veriler) kalıcı olmadığını belirten bayrak. | Belirtildiği şekilde *true* veya *false* (varsayılan), NUGET_PERSIST_DG_PATH ayarlanmamış olması halinde, geçici dizine (geçerli ortam temp dizini klasöründe NuGetScratch) depolanır. |
| NUGET_PERSIST_DG_PATH | Dg dosyaların kalıcı olması için yolu. | Mutlak yol belirtilen, bu seçenek, yalnızca kullanılan zaman *NUGET_PERSIST_DG* ayarlanır true. |
| NUGET_RESTORE_MSBUILD_ARGS | Ek MSBuild bağımsız değişkenleri ayarlar. | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild günlük ayrıntı düzeyini ayarlar. | Varsayılan değer *sessiz* ("/ v: q"). Olası değerler *q [uiet]*, *m [en az sıfır]*, *n [ormal]*, *d [ayrıntılı]*, ve *tanı [tanısı]*. |
| NUGET_SHOW_STACK | (Yığın izlemesi de dahil olmak üzere) tam özel durum kullanıcıya görüntülenip görüntülenmeyeceğini belirler. | Belirtildiği şekilde *true* veya *false* (varsayılan). |
| NUGET_XMLDOC_MODE | Derlemeleri XML belgeleri dosyası ayıklama nasıl işleneceğini belirler. | Desteklenen modlar *atla* (XML belge dosyalarını ayıklamak değil), *sıkıştırma* (zip arşivi olarak XML belge dosyalarını depolamak) veya *hiçbiri* (varsayılan, normal XML belge dosyalarını kabul dosyaları). |
| NUGET_CERT_REVOCATION_MODE | Nasıl bir paketi imzalamak için kullanılan sertifika iptal durumunu kontrol belirler, imzalı bir paketi yüklendiğinde veya geri pefromed olur. Ayarlandığında değil, varsayılan olarak `online`.| Olası değerler *çevrimiçi* (varsayılan), *çevrimdışı*.  İlgili [NU3028](../reference/errors-and-warnings/NU3028.md) |
