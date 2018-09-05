---
title: 2.8.2 NuGet sürüm notları
description: NuGet 2.8.2 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551154"
---
# <a name="nuget-282-release-notes"></a>2.8.2 NuGet sürüm notları

[2.8.1 NuGet sürüm notları](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 22 Mayıs 2014'te yayımlanmıştır.  Bu sürüm yalnızca değişiklikleri nuget.exe komut satırı, NuGet.Server paket ve diğer NuGet paketleri dahil.  Yayın, bir Visual Studio Uzantısı'nı güncelleştirilmiş veya WebMatrix genişletmesi içermiyordu.

## <a name="notable-updates"></a>Önemli güncelleştirmeler

Nuget.exe komut satırı ve NuGet.Server paket (şirket içinde barındırılan NuGet akışları için) en önemli güncelleştirmeler yoktu.

### <a name="important-nugetexe-bug-fixes"></a>Önemli nuget.exe hata düzeltmeleri

1. [nuget.exe gönderme başarısız olur ve yeniden deneniyor tutar](https://nuget.codeplex.com/workitem/4000)
1. [Temel kimlik doğrulama kimlik bilgileri doğru biçimde göndermez nuget.exe anında iletme](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe anında iletme geçici yeniden yönlendirme izleyin gerekmez](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Önemli NuGet.Server hata düzeltmesi

1. [Yanlış değerini NuGet.Server tarafından döndürülen IsAbsoluteLatestVersion](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Güncelleştirme paketleri

Nuget.exe komut satırı ve NuGet.Server düzeltmeleri NuGet paket güncelleştirmelerini gönderilir.  Diğer paketler de 2.8.2 ile güncelleştirildi vardı.

Güncelleştirilmiş paket listesi aşağıda verilmiştir:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (paket, uzantı)

## <a name="all-changes"></a>Tüm değişiklikler
Sürümünde giderilen 10 sorunlar oluştu. Tam bir listesi için iş öğeleri Nuget'te 2.8.2, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
