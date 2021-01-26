---
title: NuGet 3.2.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.2.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776517"
---
# <a name="nuget-321-release-notes"></a>NuGet 3.2.1 sürüm notları

[NuGet 3,2 sürüm notları](../release-notes/nuget-3.2.md)  |  [NuGet 3,3 sürüm notları](../release-notes/nuget-3.3.md)

Komut satırı için NuGet 3.2.1, 3,2 sürümünde en iyi duruma getirme ve düzeltmeler ile 12 Ekim 2015 ' de yayımlanmıştır ve [Dist.NuGet.org](http://dist.nuget.org/index.html)adresinden edinilebilir.

## <a name="improvements"></a>Geliştirmeleri

* NuGet artık özgün büyük küçük harfe sahip yapılandırma dosyasını kullanır `NuGet.Config` .  Büyük/küçük harfe duyarlı işletim sistemlerinde bu önemli [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet geri yükleme artık `*.xproj` 1227 ile işlenmesi gereken DNX projelerini () yoksayacak `dnu` [](https://github.com/NuGet/Home/issues/1227)
* `index.json`Ve paket kayıt verileriyle çalışırken iyileştirilmiş ağ kullanımı [1426](https://github.com/NuGet/Home/issues/1426)
* V2 Hizmetleri [1448](https://github.com/NuGet/Home/issues/1448) ile daha sağlam olması için geliştirilmiş kaynak indirme işlemesi

## <a name="fixes"></a>Düzeltmeler

* NuGet güncelleştirmesi doğru güncelleştirme `.csproj` / `.vcxproj` başvuruları [1483](https://github.com/NuGet/Home/issues/1483)
* Bir SpecialFolders. UserProfile bulunamıyorsa, artık yerel bir. NuGet klasörünün oluşturulmasını önlüyordur [1531](https://github.com/NuGet/Home/issues/1531)
* İndirme sırasında bozuk yerel önbellekteki paketlerin işlenmesi [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Komut satırı ve Visual Studio uzantısı için ele alınan sorunların tam listesi NuGet GitHub [3.2.1 kilometre taşında](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) bulunabilir

## <a name="known-issues"></a>Bilinen Sorunlar

GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)