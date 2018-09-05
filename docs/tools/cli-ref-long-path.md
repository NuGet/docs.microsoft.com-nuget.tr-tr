---
title: NuGet CLI uzun yol desteği
description: Nuget.exe uzun yol desteği için başvuru
author: zhili1208
ms.author: lzhi
ms.date: 07/12/2018
ms.topic: reference
ms.openlocfilehash: 7cd387e3eb05d149da9a88cc1c76dc08588d04b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547832"
---
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="39c5a-103">Uzun yol desteği (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="39c5a-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="39c5a-104">**İçin geçerlidir:** tüm &bullet; **desteklenen sürümler:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="39c5a-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="39c5a-105">NuGet.exe 4,8 ve sonrasında destek uzun yollar dosyaları ve dizinleri senaryoları için paketi, geri yükleme, yükleme ve dosya yolları gereken Çoğu senaryoda ister.</span><span class="sxs-lookup"><span data-stu-id="39c5a-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="39c5a-106">Gerekli işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="39c5a-106">Required Operating System</span></span>

-   <span data-ttu-id="39c5a-107">Windows 10 (sürüm 1607 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="39c5a-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="39c5a-108">Windows 10 (Temmuz 2015 sürüm veya sürüm 1511) .NET Framework 4.6.2 sürümüne yükseltirseniz veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="39c5a-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="39c5a-109">Windows Server 2016 (tüm sürümler)</span><span class="sxs-lookup"><span data-stu-id="39c5a-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="39c5a-110">"Win32 uzun yollar" Grup İlkesi'ni etkinleştir</span><span class="sxs-lookup"><span data-stu-id="39c5a-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="39c5a-111">Bir Grup İlkesi bu sistemlerde uzun yol desteğini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="39c5a-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="39c5a-112">Adımlar:</span><span class="sxs-lookup"><span data-stu-id="39c5a-112">Steps:</span></span>
1. <span data-ttu-id="39c5a-113">Başlatma **Grup İlkesi Düzenleyicisi** - türü "Başlangıç Arama çubuğuna Grup İlkesi düzenleme" veya "gpedit.msc" Run komutu (Windows-R) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39c5a-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="39c5a-114">İçinde **yerel Grup İlkesi Düzenleyicisi**, etkinleştir "Yerel Bilgisayar İlkesi/Bilgisayar Yapılandırması/Yönetim Şablonları/tüm ayarları/etkinleştirme Win32 uzun yollar".</span><span class="sxs-lookup"><span data-stu-id="39c5a-114">In the **Local Group Policy Editor**, enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Uzun yol İlkesi](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="39c5a-116">Uzun yollar desteklemek için diğer NuGet araçları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="39c5a-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="39c5a-117">DotNet CLI sürümü ve işletim sistemi ne olursa olsun uzun yollar destekler.</span><span class="sxs-lookup"><span data-stu-id="39c5a-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="39c5a-118">Visual Studio veya msbuild/t: Restore uzun yollar henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="39c5a-118">Visual Studio or msbuild /t:restore does not yet support long paths.</span></span>
> -   <span data-ttu-id="39c5a-119">Geri yükleme ve diğer komutları yürütmek için NuGet kitaplıklarını kullanan yazılım destekleyeceği uzun yollar aynı sistemlerde NuGet.exe üzerinde çalışan, ayrıca ayarlarsanız longPathAware kendi Windows bildirim ve UseLegacyPathHandling false App.Config aracılığıylayapılandırma[ Daha fazla bilgi](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span><span class="sxs-lookup"><span data-stu-id="39c5a-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set longPathAware in their windows manifest and configure UseLegacyPathHandling to false via App.Config [See more information](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)</span></span>

