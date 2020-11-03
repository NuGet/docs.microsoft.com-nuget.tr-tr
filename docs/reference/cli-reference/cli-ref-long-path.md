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
# <a name="long-path-support-nuget-cli"></a><span data-ttu-id="342b0-103">Uzun yol desteği (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="342b0-103">Long Path Support (NuGet CLI)</span></span>

<span data-ttu-id="342b0-104">**Uygulama hedefi:** &bullet; **desteklenen tüm sürümler:** 4.8 +</span><span class="sxs-lookup"><span data-stu-id="342b0-104">**Applies to:** all &bullet; **Supported versions:** 4.8+</span></span>

<span data-ttu-id="342b0-105">NuGet.exe 4,8 ve üzeri, paket, geri yükleme, yükleme ve dosya yolları gerektiren çoğu senaryo için dosyalar ve dizinler için uzun yolları destekler.</span><span class="sxs-lookup"><span data-stu-id="342b0-105">NuGet.exe 4.8 and later support long paths for files and directories for scenarios like Pack, Restore, Install, and most other scenarios that need file paths.</span></span>

## <a name="required-operating-system"></a><span data-ttu-id="342b0-106">Gerekli Işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="342b0-106">Required Operating System</span></span>

-   <span data-ttu-id="342b0-107">Windows 10 (sürüm 1607 veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="342b0-107">Windows 10 (version 1607 or later)</span></span>
-   <span data-ttu-id="342b0-108">4.6.2 veya sonraki sürümlere .NET Framework yükseltiyorsanız Windows 10 (Temmuz 2015 sürümü veya sürüm 1511).</span><span class="sxs-lookup"><span data-stu-id="342b0-108">Windows 10 (July 2015 release or version 1511) if you upgrade .NET Framework to versions 4.6.2 or later.</span></span>
-   <span data-ttu-id="342b0-109">Windows Server 2016 (tüm sürümler)</span><span class="sxs-lookup"><span data-stu-id="342b0-109">Windows Server 2016 (all versions)</span></span>

## <a name="enable-win32-long-paths-group-policy"></a><span data-ttu-id="342b0-110">"Win32 uzun yollar" grup ilkesi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="342b0-110">Enable "Win32 Long Paths" Group Policy</span></span>

<span data-ttu-id="342b0-111">Bir grup ilkesi ayarlayarak bu sistemlerde uzun yol desteğini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="342b0-111">One needs to enable long path support on those systems by setting a group policy.</span></span>

<span data-ttu-id="342b0-112">Adımlar:</span><span class="sxs-lookup"><span data-stu-id="342b0-112">Steps:</span></span>
1. <span data-ttu-id="342b0-113">**Grup İlkesi düzenleyiciyi** Başlat-arama çubuğunda "Grup ilkesini Düzenle" yazın veya Çalıştır komutundan (Windows-R) "gpedit. msc" komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="342b0-113">Launch **Group Policy Editor** - Type "Edit group policy" in the Start search bar or Run "gpedit.msc" from the Run command (Windows-R).</span></span>
2. <span data-ttu-id="342b0-114">**Yerel Grup İlkesi Düzenleyicisi** , "yerel bilgisayar Ilkesi/bilgisayar yapılandırması/Yönetim Şablonları/tüm ayarlar/Win32 uzun yollarını etkinleştir" i etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="342b0-114">In the **Local Group Policy Editor** , enable "Local Computer Policy/Computer Configuration/Administrative Templates/All Settings/Enable Win32 long paths".</span></span>

![Uzun yol Ilkesi](media/LongPathPolicy.png)


> [!Note]
> <span data-ttu-id="342b0-116">Uzun yolları desteklemek için diğer NuGet araçlarının etkinleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="342b0-116">Enabling Other NuGet Tools to Support Long Paths</span></span>
>
> -   <span data-ttu-id="342b0-117">DotNet CLı, işletim sistemi veya sürümden bağımsız olarak uzun yolları destekler.</span><span class="sxs-lookup"><span data-stu-id="342b0-117">Dotnet CLI supports long paths regardless of the operating system or version.</span></span>
> -   <span data-ttu-id="342b0-118">Visual Studio veya `msbuild -t:restore` uzun yolları henüz desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="342b0-118">Visual Studio or `msbuild -t:restore` does not yet support long paths.</span></span>
> -   <span data-ttu-id="342b0-119">Geri yükleme ve diğer komutları yürütmek için NuGet kitaplıklarını kullanan yazılım, Windows bildiriminde da ayarlandıklarında ve ' de ' ye ve ' `longPathAware` `UseLegacyPathHandling` e ' App.Config ye, `false` [daha fazla bilgi görüntülemek](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10) için NuGet.exe çalıştığı sistemlerde uzun yolları destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="342b0-119">Software that uses NuGet Libraries to execute restore and other commands, will support long paths on the same systems that NuGet.exe works on, if they also set `longPathAware` in their windows manifest and configure `UseLegacyPathHandling` to `false` via App.Config [See more information](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)</span></span>