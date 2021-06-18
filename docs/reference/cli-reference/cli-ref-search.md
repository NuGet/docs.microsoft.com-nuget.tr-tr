---
title: NuGet CLI arama komutu
description: nuget.exe search komutu için başvuru
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323667"
---
# <a name="search-command-nuget-cli"></a>search komutu (NuGet CLI)

**Uygulama: paket** tüketimi &bullet; **Desteklenen sürümler:** 5.8+

Sağlanan sorgu dizesini kullanarak verilen kaynağı arar. Kaynak belirtilmezse%AppData%\NuGet\NuGet.Config tanımlanan tüm kaynaklar kullanılır.

## <a name="usage"></a>Kullanım

```cli
nuget search [search terms] [options]
```

burada arama terimlerinin, paketlerin, etiketlerin ve paket açıklamalarının adları, bu terimlerin kullanıcı adlarında olduğu gibi nuget.org.

## <a name="options"></a>Seçenekler

| Ad | Açıklama | Kullanım |
| ---  |     ---     |  :-:  |
| Önkeser | Yayın öncesi paketler varsayılan olarak dahil değildir, ancak bu bağımsız değişken kullanılarak dahil olabilir | -PreRelease |
| Kaynak | Kaynaklarda varsayılan kaynakları sorgulamak yerine aranacak belirli paket __nuget.config__ | -Source `<Source URL>`|
| Take | Geri dönecek sonuç sayısı. Varsayılan değer 20'dir. | -Take `<positive integer>` |
| Ayrıntı Düzeyi | Çıkışta görüntülenmek için ayrıntı düzeyi. Varsayılan değer _normaldir._ (Aşağıdaki nota bakın)  | -Ayrıntılılık `<quiet|normal|detailed>` |
| Help | Komutun yardım bilgilerini görüntüler | -Help |

Ayrıca [bkz. Ortam değişkenleri](cli-ref-environment-variables.md)

> [!NOTE] 
> AyrıntılıLık Düzeyleri:
> * _quiet_ - Paket Kimliği, Sürüm
> * _normal_ - Paket Kimliği, Sürüm, İndirmeler, Açıklama Önizlemesi
> * _ayrıntılı_ - Paket Kimliği, Sürüm, İndirmeler, Tam Açıklama, Sorgu URL'si gibi diğer bilgiler

## <a name="examples"></a>Örnekler

Varsayılan kaynaklardan *günlük* kaydı ile ilgili paketleri arayın:
```
nuget search logging
```
Ayrıntılı *ayrıntılı* günlük kaydı ile ilgili paketleri arayın:
```
nuget search logging -Verbosity detailed
```
İlgili *paketleri günlüğe* kaydetme araması ve yalnızca ilk 5 sonucu gösterme:
```
nuget search logging -Take 5
```
Belirtilen *kaynak/akıştan* yayın öncesi sürümler de dahil olmak üzere JSON ile ilgili paketleri arayın:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Birden çok *kaynak/akıştan JSON* ile ilgili paketleri arayın:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
