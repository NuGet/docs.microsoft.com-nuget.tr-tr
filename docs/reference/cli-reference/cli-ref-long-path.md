---
title: NuGet CLı uzun yol desteği
description: NuGet. exe uzun yol desteği başvurusu
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 42b5b7d863d22d7aad99a65700ca11bcc2861db1
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328308"
---
# <a name="long-path-support-nuget-cli"></a>Uzun yol desteği (NuGet CLı)

**Uygulama hedefi:** desteklenen &bullet; tüm **sürümler:** 4.8 +

NuGet. exe 4,8 ve üzeri, dosya ve dizinlerin paket, geri yükleme, yükleme ve dosya yollarına ihtiyacı olan çoğu senaryo gibi senaryolar için uzun yollarını destekler.

## <a name="required-operating-system"></a>Gerekli Işletim sistemi

-   Windows 10 (sürüm 1607 veya üzeri)
-   4\.6.2 veya sonraki sürümlere .NET Framework yükseltiyorsanız Windows 10 (Temmuz 2015 sürümü veya sürüm 1511).
-   Windows Server 2016 (tüm sürümler)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 uzun yollar" grup ilkesi etkinleştir

Bir grup ilkesi ayarlayarak bu sistemlerde uzun yol desteğini etkinleştirmeniz gerekir.

Olanları
1. **Grup İlkesi düzenleyiciyi** Başlat-arama çubuğunda "Grup ilkesini Düzenle" yazın veya Çalıştır komutundan (Windows-R) "gpedit. msc" komutunu çalıştırın.
2. **Yerel Grup İlkesi Düzenleyicisi**, "yerel bilgisayar Ilkesi/bilgisayar yapılandırması/Yönetim Şablonları/tüm ayarlar/Win32 uzun yollarını etkinleştir" i etkinleştirin.

![Uzun yol Ilkesi](media/LongPathPolicy.png)


> [!Note]
> Uzun yolları desteklemek için diğer NuGet araçlarının etkinleştirilmesi
>
> -   DotNet CLı, işletim sistemi veya sürümden bağımsız olarak uzun yolları destekler.
> -   Visual Studio veya MSBuild-t:restore uzun yolları henüz desteklemiyor.
> -   Geri yükleme ve diğer komutları yürütmek için NuGet kitaplıklarını kullanan yazılımlar, aynı zamanda Windows bildiriminde longPathAware ayarlar ve App. config [aracılığıyla UseLegacyPathHandling ' i yanlış olarak yapılandırırsanız, NuGet. exe ' nin üzerinde çalıştığı sistemlerde uzun yolları destekleyecektir. Daha fazla bilgi görüntüleyin](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

