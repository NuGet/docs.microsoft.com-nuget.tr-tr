---
title: "NuGet Visual Studio Proje sistemi desteği | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Üçüncü taraf proje türleri için Visual Studio Proje sistemine NuGet tümleştirilmesi."
keywords: "NuGet Visual Studio, özel proje türleri, Visual Studio projeleri"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e2f7c4a32f80b96360f08d04efb8af639af2ddd3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="76f9d-104">NuGet Visual Studio Proje sistemi desteği</span><span class="sxs-lookup"><span data-stu-id="76f9d-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="76f9d-105">Visual Studio'da üçüncü taraf proje türlerini desteklemek için NuGet 3.x+ destekleyen [ortak proje System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), NuGet 3.2 + CPS olmayan proje sistemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="76f9d-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="76f9d-106">NuGet ile tümleştirmek için bir proje sistem bu konuda açıklanan tüm proje özelliklerini kendi desteği tanıtır gerekir.</span><span class="sxs-lookup"><span data-stu-id="76f9d-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="76f9d-107">Projenizde yüklemek paketler etkinleştirmek amacıyla projenize gerçekten yok yetenekleri bildirmeyin.</span><span class="sxs-lookup"><span data-stu-id="76f9d-107">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="76f9d-108">Proje Özellikleri NuGet istemci yanı sıra Visual Studio ve diğer uzantıları özelliklerinin çoğu bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="76f9d-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="76f9d-109">Yanlışlıkla projenizi yeteneklerini reklam çalışmasına bu bileşenler ve kullanıcılarınızın deneyimini düşmesine yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="76f9d-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="76f9d-110">Proje Özellikleri tanıtma</span><span class="sxs-lookup"><span data-stu-id="76f9d-110">Advertise project capabilities</span></span>

<span data-ttu-id="76f9d-111">Hangi paketlerin göre proje türü ile uyumlu olan NuGet istemcisi belirler [projenin özellikleri](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)aşağıdaki tabloda açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="76f9d-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="76f9d-112">Özellik</span><span class="sxs-lookup"><span data-stu-id="76f9d-112">Capability</span></span> | <span data-ttu-id="76f9d-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="76f9d-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="76f9d-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="76f9d-114">AssemblyReferences</span></span> | <span data-ttu-id="76f9d-115">Proje derleme başvurularını (WinRTReferences farklı) desteklediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="76f9d-115">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="76f9d-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="76f9d-116">DeclaredSourceItems</span></span> | <span data-ttu-id="76f9d-117">Proje kaynak öğeleri bildirir, proje tipik bir MSBuild proje (değil DNX) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="76f9d-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="76f9d-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="76f9d-118">UserSourceItems</span></span>|<span data-ttu-id="76f9d-119">Kullanıcı kendi projeye rastgele dosyalar eklemek için izin verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="76f9d-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="76f9d-120">Proje CPS tabanlı sistemler için sizin için bu bölümün geri kalanında tanımlanan proje özellikleri uygulama ayrıntılarını yapılmış.</span><span class="sxs-lookup"><span data-stu-id="76f9d-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="76f9d-121">Bkz: [CPS projelerinde proje özellikleri bildirme](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="76f9d-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="76f9d-122">VsProjectCapabilitiesPresenceChecker uygulama</span><span class="sxs-lookup"><span data-stu-id="76f9d-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="76f9d-123">`VsProjectCapabilitiesPresenceChecker` Sınıfı uygulanmalı `IVsBooleanSymbolPresenceChecker` şu şekilde tanımlanır arabirimi:</span><span class="sxs-lookup"><span data-stu-id="76f9d-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="76f9d-124">Bu arabirim için bir örnek uygulama sonra olacaktır:</span><span class="sxs-lookup"><span data-stu-id="76f9d-124">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="76f9d-125">Özelliklerini eklemek/kaldırmak unutmayın `ActualProjectCapabilities` kümesi tabanlı ne proje sisteminizi gerçekte desteklediğine.</span><span class="sxs-lookup"><span data-stu-id="76f9d-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="76f9d-126">Bkz: [proje özellikleri belgelerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) tam açıklamaları için.</span><span class="sxs-lookup"><span data-stu-id="76f9d-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="76f9d-127">Sorgularına yanıt</span><span class="sxs-lookup"><span data-stu-id="76f9d-127">Responding to queries</span></span>

<span data-ttu-id="76f9d-128">Bir proje destekleyerek bu özelliği bildirir `VSHPROPID_ProjectCapabilitiesChecker` özelliği üzerinden `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="76f9d-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="76f9d-129">Örneği döndürmelidir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, içinde tanımlanan `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` derleme.</span><span class="sxs-lookup"><span data-stu-id="76f9d-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="76f9d-130">Yükleyerek bu derleme başvurusu [NuGet paketi](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="76f9d-130">Reference this assembly by installing the [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="76f9d-131">Örneğin, aşağıdaki ekleyebilirsiniz `case` deyimi, `IVsHierarchy::GetProperty` yöntemin `switch` deyimi:</span><span class="sxs-lookup"><span data-stu-id="76f9d-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="76f9d-132">DTE desteği</span><span class="sxs-lookup"><span data-stu-id="76f9d-132">DTE Support</span></span>

<span data-ttu-id="76f9d-133">NuGet başvuruları, içerik öğelerini eklemek için proje sistemi sürücüleri ve MSBuild alır çağırarak [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), üst düzey Visual Studio Otomasyon arabirimi olduğu.</span><span class="sxs-lookup"><span data-stu-id="76f9d-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="76f9d-134">DTE zaten uygulayabilir COM arabirimleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="76f9d-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="76f9d-135">Proje türü üzerinde CPS temel alıyorsa, DTE sizin için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="76f9d-135">If your project type is based on CPS, DTE is implemented for you.</span></span>