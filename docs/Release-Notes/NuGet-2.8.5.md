---
title: "NuGet 2.8.5 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.5 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.5 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 sürüm notları

[NuGet 2.8.3 Sürüm Notları](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 sürüm notları](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5, 30 Mart 2015 yayımlanmıştır. Küçük bir güncelleştirmesidir bizim 2.8.3 VSIX bazı düzeltmeler hedeflenen.

Bu sürümde için NuGet Paket Yöneticisi iletişim için destek eklenmiştir [DNX hedef Framework adlar](https://github.com/aspnet/dnx).  Desteklenen bu yeni framework adları şunlardır:

* **core50** - A 'base' hedef framework ad (TFM) çekirdek CLR ile uyumludur.
* **dnx452** - tam 4.5.2 kullanarak A TFM DNX tabanlı belirli uygulamaları framework sürümü
* **dnx46** - framework'ün tam 4.6 sürümünü kullanarak bir TFM DNX tabanlı belirli uygulamaları
* **dnxcore50** - framework çekirdek 5.0 sürümünü kullanarak bir TFM DNX tabanlı belirli uygulamaları

Bir hata FSharp projelere düzgün şekilde yüklenmesini önlenmiş bu paketleri düzeltildi:

https://nuget.Codeplex.com/workitem/4400