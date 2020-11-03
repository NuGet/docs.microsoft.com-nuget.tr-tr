---
title: NuGet CLı uzun yol desteği
description: nuget.exe uzun yol desteği için başvuru
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 1143da911c80125a9d60e4b98798b11871e9988a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238198"
---
# <a name="long-path-support-nuget-cli"></a>Uzun yol desteği (NuGet CLı)

**Uygulama hedefi:** &bullet; **desteklenen tüm sürümler:** 4.8 +

NuGet.exe 4,8 ve üzeri, paket, geri yükleme, yükleme ve dosya yolları gerektiren çoğu senaryo için dosyalar ve dizinler için uzun yolları destekler.

## <a name="required-operating-system"></a>Gerekli Işletim sistemi

-   Windows 10 (sürüm 1607 veya üzeri)
-   4.6.2 veya sonraki sürümlere .NET Framework yükseltiyorsanız Windows 10 (Temmuz 2015 sürümü veya sürüm 1511).
-   Windows Server 2016 (tüm sürümler)

## <a name="enable-win32-long-paths-group-policy"></a>"Win32 uzun yollar" grup ilkesi etkinleştir

Bir grup ilkesi ayarlayarak bu sistemlerde uzun yol desteğini etkinleştirmeniz gerekir.

Adımlar:
1. **Grup İlkesi düzenleyiciyi** Başlat-arama çubuğunda "Grup ilkesini Düzenle" yazın veya Çalıştır komutundan (Windows-R) "gpedit. msc" komutunu çalıştırın.
2. **Yerel Grup İlkesi Düzenleyicisi** , "yerel bilgisayar Ilkesi/bilgisayar yapılandırması/Yönetim Şablonları/tüm ayarlar/Win32 uzun yollarını etkinleştir" i etkinleştirin.

![Uzun yol Ilkesi](media/LongPathPolicy.png)


> [!Note]
> Uzun yolları desteklemek için diğer NuGet araçlarının etkinleştirilmesi
>
> -   DotNet CLı, işletim sistemi veya sürümden bağımsız olarak uzun yolları destekler.
> -   Visual Studio veya `msbuild -t:restore` uzun yolları henüz desteklemiyor.
> -   Geri yükleme ve diğer komutları yürütmek için NuGet kitaplıklarını kullanan yazılım, Windows bildiriminde da ayarlandıklarında ve ' de ' ye ve ' `longPathAware` `UseLegacyPathHandling` e ' App.Config ye, `false` [daha fazla bilgi görüntülemek](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) için NuGet.exe çalıştığı sistemlerde uzun yolları destekleyecektir.