---
title: Yerel NuGet paketleri oluşturma
description: Yönetilen kod yerine C++ kodunu içerir yerel NuGet paketleri oluşturma ile ilgili ayrıntılar C++ projelerinde kullanın.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 086084bdfae5eace0b0a6aab17140a1fa48ae977
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817066"
---
# <a name="creating-native-packages"></a><span data-ttu-id="b70d0-103">Yerel paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b70d0-103">Creating native packages</span></span>

<span data-ttu-id="b70d0-104">Yerel bir paket içinde C++ projeleri kullanılması izin veren, yönetilen kod yerine yerel C++ kod içerir.</span><span class="sxs-lookup"><span data-stu-id="b70d0-104">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="b70d0-105">(Bkz [yerel C++ paketleri](../consume-packages/finding-and-choosing-packages.md#native-c-packages) Tüket bölümdeki.)</span><span class="sxs-lookup"><span data-stu-id="b70d0-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="b70d0-106">Bir C++ projesinde tüketilebilir olması için bir paket hedeflemelidir `native` framework.</span><span class="sxs-lookup"><span data-stu-id="b70d0-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="b70d0-107">Olmadığından şu anda bu framework NuGet olarak ile ilişkili tüm sürüm numaralarını tüm C++ projeleri aynı değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="b70d0-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="b70d0-108">Eklediğinizden emin olun *yerel* içinde `<tags>` bölümü, `.nuspec` o etiketinde arayarak paketinizi bulun diğer geliştiricilere yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="b70d0-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="b70d0-109">Hedefleme yerel NuGet paketlerini `native` dosyalarında sağlamak `\build`, `\content`, ve `\tools` klasörleri; `\lib` (NuGet C++ projesi başvurular doğrudan de ekleyemiyor) Bu durumda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="b70d0-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="b70d0-110">Bir paketi ayrıca hedefleri ve özellik dosyaları içerebilir `\build` NuGet paketi tüketen projelere otomatik olarak içeri aktaracak.</span><span class="sxs-lookup"><span data-stu-id="b70d0-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="b70d0-111">Bu dosyalar paket kimliği ile aynı adlandırılmalıdır `.targets` ve/veya `.props` uzantıları.</span><span class="sxs-lookup"><span data-stu-id="b70d0-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="b70d0-112">Örneğin, [cpprestsdk](https://nuget.org/packages/cpprestsdk/) paketi içeren bir `cpprestsdk.targets` dosyasını kendi `\build` klasör.</span><span class="sxs-lookup"><span data-stu-id="b70d0-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="b70d0-113">`\build` Klasörü tüm NuGet paketleri ve yalnızca yerel paketleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b70d0-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="b70d0-114">`\build` Klasörü hedef çerçeveyi tıpkı dikkate alır `\content`, `\lib`, ve `\tools` klasörler.</span><span class="sxs-lookup"><span data-stu-id="b70d0-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="b70d0-115">Oluşturabileceğiniz yani bir `\build\net40` klasör ve `\build\net45` klasörü ve NuGet içeri aktarır uygun özellik ve hedefleri dosyaları projeye.</span><span class="sxs-lookup"><span data-stu-id="b70d0-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="b70d0-116">(MSBuild hedefleri almak için PowerShell komut dosyası kullanımı gerekli değildir.)</span><span class="sxs-lookup"><span data-stu-id="b70d0-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
