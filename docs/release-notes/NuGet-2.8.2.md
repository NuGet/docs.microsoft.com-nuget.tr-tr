---
title: NuGet 2.8.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.2 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780368"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 sürüm notları

[NuGet 2.8.1 sürüm notları](../release-notes/nuget-2.8.1.md)  |  [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2, 22 Mayıs 2014 tarihinde yayınlandı.  Bu sürüm yalnızca nuget.exe komut satırına, NuGet. Server paketine ve diğer NuGet paketlerine yapılan değişiklikleri içerir.  Sürüm, güncelleştirilmiş bir Visual Studio uzantısı veya WebMatrix uzantısı içermiyordu.

## <a name="notable-updates"></a>Önemli güncelleştirmeler

En önemli güncelleştirmeler nuget.exe komut satırı ve NuGet. Server paketidir (Şirket içinde barındırılan NuGet akışları için).

### <a name="important-nugetexe-bug-fixes"></a>Önemli nuget.exe hata düzeltmeleri

1. [nuget.exe gönderimi başarısız oluyor ve yeniden denemeyi sürdüyor](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe gönderimi temel kimlik doğrulama kimlik bilgilerini doğru göndermez](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe gönderimi geçici yeniden yönlendirmeye uymalıdır](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Önemli NuGet. sunucu hata onarımı

1. [NuGet. Server tarafından döndürülen yanlış IsAbsoluteLatestVersion değeri](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Paketler güncelleştirildi

nuget.exe komut satırı ve NuGet. Server düzeltmeleri NuGet paket güncelleştirmeleri olarak gönderilir.  2.8.2 ile güncelleştirilmiş başka paketler de vardı.

Güncelleştirilmiş paketlerin listesi aşağıdadır:

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (uzantı değil, paket)

## <a name="all-changes"></a>Tüm değişiklikler
Yayında ele alınan 10 sorun oluştu. NuGet 2.8.2 'te düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)' ni görüntüleyin.
