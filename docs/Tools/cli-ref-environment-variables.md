---
title: "NuGet CLI ortam değişkenleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1f5c31ca-fa0a-4798-a906-110f2c73d00b
description: "Nuget.exe ortam değişkenleri için başvurusu"
keywords: "nuget ortam değişkenleri"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0a1dc2a928da657b0d222c2adc02fbd850b66704
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI ortam değişkenleri

CLI nuget.exe davranışını nuget.exe bilgisayar genelinde kullanıcı etkileyen veya düzeyleri işlem ortam değişkenleri bir dizi yapılandırılabilir.

Genel olarak, doğrudan komut satırında veya NuGet yapılandırma dosyaları belirtilen seçenekler önceliğe sahip, ancak birkaç istisnası vardır gibi *FORCE_NUGET_EXE_INTERACTIVE*. Bu nuget.exe farklı bilgisayarlar arasında farklı şekilde davranan bulursanız, bir ortam değişkeni neden olabilir. Örneğin, Azure Web uygulamaları (dağıtımı sırasında kullanılan) Kudu sahip *NUGET_XMLDOC_MODE* kümesine *atla* paket geri yükleme performansını hızlandırmak ve disk alanı kaydetmek için.

| Değişken | Açıklama | Açıklamalar |
| --- | --- | --- |
| http_proxy | Http proxy NuGet HTTP işlemler için kullanılır. | Bu olarak belirtilen `http://<username>:<password>@proxy.com`. |
| no_proxy | Proxy kullanarak atlamak için etki alanlarını yapılandırır. | Etki alanları virgülle (,) ayırarak olarak belirtilmiş. |
| EnableNuGetPackageRestore | NuGet örtük olarak izni, geri yükleme paketi tarafından gerekip gerekmediğini vermelisiniz varsa için bayrak. | Belirtilen bayrağı belirtilmiş | olarak *true* veya *1*, bayrak olarak kabul başka bir değer ayarlanmamış. |
| NUGET_EXE_NO_PROMPT | Kimlik bilgileri için exe engeller.| Null veya boş dize değerlendirilir dışında herhangi bir değer bu bayrak kümesi/true. |
FORCE_NUGET_EXE_INTERACTIVE | Etkileşimli mod zorlamak için genel bir ortam değişkenidir. | Null veya boş dize değerlendirilir dışında herhangi bir değer bu bayrak kümesi/true. |
| NUGET_PACKAGES | Paketleri Burada depolanan / önbelleğe yolu. | Mutlak yolu belirtilmelidir. |
| NUGET_FALLBACK_PACKAGES | Genel geri dönüş paketleri klasörler. | Noktalı virgül (;) ayrılmış mutlak klasörü yollar. |
| NUGET_HTTP_CACHE_PATH | HTTP Önbellek klasörü. | Mutlak yolu belirtilmelidir. |
| NUGET_PERSIST_DG | Dg dosyaları (MSBuild toplanan verileri) kalıcı ise belirten bayrak. | Olarak belirtilen *true* veya *false* (varsayılan), NUGET_PERSIST_DG_PATH değil ayarlarsanız, geçici dizine (geçerli ortam temp dizininde NuGetScratch klasör) depolanır. |
| NUGET_PERSIST_DG_PATH | Dg dosyaları kalıcı hale getirmek için yolu. | Mutlak yol olarak, bu seçenek yalnızca kullanılan olduğunda belirtilmiştir *NUGET_PERSIST_DG* ayarlanmış true. |
| NUGET_RESTORE_MSBUILD_ARGS | Ek MSBuild bağımsız değişkenleri ayarlar. |
| NUGET_RESTORE_MSBUILD_| Ayrıntı Düzeyi |MSBuild günlük ayrıntı ayarlar. | Varsayılan değer *sessiz* ("/ v: q"). Olası değerler *q [uiet]*, *m [en az sıfır]*, *n [ormal]*, *d [kincil]*, ve *tanı [nostic]*. |
| NUGET_SHOW_STACK | (Yığın izleme dahil) tam özel durum kullanıcıya görüntülenmesi gerekip gerekmediğini belirler. | Olarak belirtilen *true* veya *false* (varsayılan). |
| NUGET_XMLDOC_MODE | Derlemeleri XML belge dosyası ayıklama nasıl işleneceğini belirler. | Desteklenen modlar *atla* (XML belge dosyalarını ayıklayın değil), *Sıkıştır* (zip arşivini XML belge dosyalarını depolamak) veya *hiçbiri* (varsayılan, XML belge dosyalarını normal ele alın dosyaları). |
