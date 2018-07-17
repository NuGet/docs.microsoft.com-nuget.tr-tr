---
title: NuGet CLI uzun yol desteği
description: Nuget.exe uzun yol desteği için başvuru
author: zhili1208
ms.author: lzhi
manager: rob
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 0119be3fd8fd6c2e06e0135de5e498e0730bb0cc
ms.sourcegitcommit: a76ecc58f41c2c5b3536ff4a3f3fcbdf5258177c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39072750"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="57a1b-103">Uzun yol desteği (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="57a1b-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="57a1b-104">**İçin geçerlidir:** tüm &bullet; **desteklenen sürümler:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="57a1b-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="57a1b-105">NuGet.exe 4,8 ve sonrasında destek uzun yollar dosyaları ve dizinleri senaryoları için paketi, geri yükleme, yükleme ve dosya yolları gereken Çoğu senaryoda ister.</span><span class="sxs-lookup"><span data-stu-id="57a1b-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="57a1b-106">Gerekli işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="57a1b-106">Required Operating System</span></span>

-   <span data-ttu-id="57a1b-107">Windows 10 (sürüm 1607 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="57a1b-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="57a1b-108">Windows 10 (Temmuz 2015 sürüm veya sürüm 1511) .NET Framework 4.6.2 sürümüne yükseltirseniz veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="57a1b-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="57a1b-109">Windows Server 2016 (tüm sürümler)</span><span class="sxs-lookup"><span data-stu-id="57a1b-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="57a1b-110">"Win32 uzun yollar" Grup İlkesi'ni etkinleştir</span><span class="sxs-lookup"><span data-stu-id="57a1b-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="57a1b-111">Bir Grup İlkesi bu sistemlerde uzun yol desteğini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57a1b-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="57a1b-112">Adımlar:</span><span class="sxs-lookup"><span data-stu-id="57a1b-112">Steps:</span></span>
1. <span data-ttu-id="57a1b-113">Başlatma **Grup İlkesi Düzenleyicisi** - türü "Başlangıç Arama çubuğuna Grup İlkesi düzenleme" veya "gpedit.msc" Run komutu (Windows-R) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="57a1b-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="57a1b-114">İçinde **yerel Grup İlkesi Düzenleyicisi**, etkinleştir "Yerel Bilgisayar İlkesi/Bilgisayar Yapılandırması/Yönetim Şablonları/tüm ayarları/etkinleştirme Win32 uzun yollar".</span><span class="sxs-lookup"><span data-stu-id="57a1b-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Uzun yol İlkesi](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="57a1b-116">Uzun yollar desteklemek için diğer NuGet araçları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="57a1b-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="57a1b-117">DotNet CLI sürümü ve işletim sistemi ne olursa olsun uzun yollar destekler.</span><span class="sxs-lookup"><span data-stu-id="57a1b-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="57a1b-118">Visual Studio veya msbuild/t: Restore uzun yollar henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="57a1b-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="57a1b-119">Geri yükleme ve diğer komutları yürütmek için NuGet kitaplıklarını kullanan yazılım destekleyeceği uzun yollar aynı sistemlerde NuGet.exe üzerinde çalışan, ayrıca ayarlarsanız longPathAware kendi Windows bildirim ve UseLegacyPathHandling false App.Config aracılığıylayapılandırma[ Daha fazla bilgi](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="57a1b-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

