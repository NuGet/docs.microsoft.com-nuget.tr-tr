---
title: NuGet CLı uzun yol desteği
description: NuGet. exe uzun yol desteği başvurusu
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 9b5a97d963eab7fbbde4aefae1c9b1a8bfcdeb11
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036961"
---
# <a name="long-path-support-nuget-cli"></a>Uzun yol desteği (NuGet CLı)

**Uygulama hedefi:** tüm &bullet; **Desteklenen sürümler:** 4.8 +

NuGet. exe 4,8 ve üzeri, dosya ve dizinlerin paket, geri yükleme, yükleme ve dosya yollarına ihtiyacı olan çoğu senaryo gibi senaryolar için uzun yollarını destekler.

## <a name="required-operating-system"></a>Gerekli Işletim sistemi

-   Windows 10 (sürüm 1607 veya üzeri)
-   4\.6.2 veya sonraki sürümlere .NET Framework yükseltiyorsanız Windows 10 (Temmuz 2015 sürümü veya sürüm 1511).
-   Windows Server 2016 (tüm sürümler)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 uzun yollar" grup ilkesi etkinleştir

Bir grup ilkesi ayarlayarak bu sistemlerde uzun yol desteğini etkinleştirmeniz gerekir.

Adımlar:
1. **Grup İlkesi düzenleyiciyi** Başlat-arama çubuğunda "Grup ilkesini Düzenle" yazın veya Çalıştır komutundan (Windows-R) "gpedit. msc" komutunu çalıştırın.
2. **Yerel Grup İlkesi Düzenleyicisi**, "yerel bilgisayar Ilkesi/bilgisayar yapılandırması/Yönetim Şablonları/tüm ayarlar/Win32 uzun yollarını etkinleştir" i etkinleştirin.

![Uzun yol Ilkesi](media/LongPathPolicy.png)


> [!Note]
> Uzun yolları desteklemek için diğer NuGet araçlarının etkinleştirilmesi
>
> -   DotNet CLı, işletim sistemi veya sürümden bağımsız olarak uzun yolları destekler.
> -   Visual Studio veya `msbuild -t:restore` uzun yolları henüz desteklemiyor.
> -   Geri yükleme ve diğer komutları yürütmek için NuGet kitaplıklarını kullanan yazılımlar, aynı zamanda Windows bildiriminde `longPathAware` ayarlamış ve App. config aracılığıyla `false` `UseLegacyPathHandling` yapılandıradıklarında, NuGet. exe ' nin üzerinde çalıştığı sistemlerde uzun yolları destekleyecektir. [daha fazla bilgi Için bkz. daha fazla bilgi](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)

