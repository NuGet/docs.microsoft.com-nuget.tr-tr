---
title: Yerel NuGet paketleri oluşturma | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Yönetilen kod yerine C++ kodunu içerir yerel NuGet paketleri oluşturma ile ilgili ayrıntılar C++ projelerinde kullanın.
keywords: NuGet yerel paketleri, NuGet C++ paketleri, C++ projeleri hedefleyen yerel kod paketleri
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ed33f906f11a80c0d033292f7de151e93b8368fd
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-native-packages"></a><span data-ttu-id="ad3b8-104">Yerel paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad3b8-104">Creating native packages</span></span>

<span data-ttu-id="ad3b8-105">Yerel bir paket içinde C++ projeleri kullanılması izin veren, yönetilen kod yerine yerel C++ kod içerir.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-105">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="ad3b8-106">(Bkz [yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) Tüket bölümdeki.)</span><span class="sxs-lookup"><span data-stu-id="ad3b8-106">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="ad3b8-107">Bir C++ projesinde tüketilebilir olması için bir paket hedeflemelidir `native` framework.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-107">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="ad3b8-108">Olmadığından şu anda bu framework NuGet olarak ile ilişkili tüm sürüm numaralarını tüm C++ projeleri aynı değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-108">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="ad3b8-109">Eklediğinizden emin olun *yerel* içinde `<tags>` bölümü, `.nuspec` o etiketinde arayarak paketinizi bulun diğer geliştiricilere yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-109">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="ad3b8-110">Hedefleme yerel NuGet paketlerini `native` dosyalarında sağlamak `\build`, `\content`, ve `\tools` klasörleri; `\lib` (NuGet C++ projesi başvurular doğrudan de ekleyemiyor) Bu durumda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-110">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="ad3b8-111">Bir paketi ayrıca hedefleri ve özellik dosyaları içerebilir `\build` NuGet paketi tüketen projelere otomatik olarak içeri aktaracak.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-111">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="ad3b8-112">Bu dosyalar paket kimliği ile aynı adlandırılmalıdır `.targets` ve/veya `.props` uzantıları.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-112">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="ad3b8-113">Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi içeren bir `cpprestsdk.targets` dosyasını kendi `\build` klasör.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-113">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="ad3b8-114">`\build` Klasörü tüm NuGet paketleri ve yalnızca yerel paketleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-114">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="ad3b8-115">`\build` Klasörü hedef çerçeveyi tıpkı dikkate alır `\content`, `\lib`, ve `\tools` klasörler.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-115">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="ad3b8-116">Oluşturabileceğiniz yani bir `\build\net40` klasör ve `\build\net45` klasörü ve NuGet içeri aktarır uygun özellik ve hedefleri dosyaları projeye.</span><span class="sxs-lookup"><span data-stu-id="ad3b8-116">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="ad3b8-117">(MSBuild hedefleri almak için PowerShell komut dosyası kullanımı gerekli değildir.)</span><span class="sxs-lookup"><span data-stu-id="ad3b8-117">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
