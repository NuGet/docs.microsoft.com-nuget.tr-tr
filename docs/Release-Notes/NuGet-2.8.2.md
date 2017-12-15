---
title: "NuGet 2.8.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.2 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 sürüm notları

[NuGet 2.8.1 ile sürüm notları](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 22 Mayıs 2014'te yayımlanmıştır.  Bu sürüm yalnızca komut satırı nuget.exe, NuGet.Server paket ve diğer NuGet paketleri yapılan değişiklikler dahil.  Yayın güncelleştirilmiş Visual Studio uzantısı veya WebMatrix genişletmesi içermiyordu.

## <a name="notable-updates"></a>Önemli güncelleştirmeleri

Komut satırı nuget.exe ve NuGet.Server paket (kendi kendini barındıran NuGet akışlarını için) en önemli güncelleştirmeleri yoktu.

### <a name="important-nugetexe-bug-fixes"></a>Önemli nuget.exe hata düzeltmeleri

1. [nuget.exe gönderme başarısız olur ve yeniden deneniyor tutar](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe itme temel kimlik doğrulama kimlik bilgileri doğru biçimde göndermez](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe itme geçici yeniden yönlendirme izleyin olmaz](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Önemli NuGet.Server hata düzeltmesi

1. [NuGet.Server tarafından döndürülen IsAbsoluteLatestVersion yanlış değeri](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Güncelleştirme paketleri

NuGet.Server düzeltmeler ve komut satırı nuget.exe NuGet paketi güncelleştirme gönderilir.  Diğer paketleri de 2.8.2 ile güncelleştirilmiş vardı.

Güncelleştirilmiş paketleri listesi aşağıdadır:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (paket, uzantısını değil)

## <a name="all-changes"></a>Tüm değişiklikleri
Sürümde ele 10 sorunları vardı. Tam bir listesi için iş öğeleri NuGet 2.8.2, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
