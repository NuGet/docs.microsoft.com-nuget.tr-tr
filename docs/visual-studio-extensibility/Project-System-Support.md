---
title: Görsel Stüdyo Proje Sistemi için NuGet Desteği
description: NuGet'in üçüncü taraf proje türleri için Visual Studio proje sistemine entegrasyonu.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495926"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="6b303-103">Visual Studio proje sistemi için NuGet desteği</span><span class="sxs-lookup"><span data-stu-id="6b303-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="6b303-104">Visual Studio'da üçüncü taraf proje türlerini desteklemek için NuGet 3.x+, [Ortak Proje Sistemi'ni (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)ve NuGet 3.2+CPS olmayan proje sistemlerini de destekler.</span><span class="sxs-lookup"><span data-stu-id="6b303-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="6b303-105">NuGet ile tümleştirmek için, bir proje sisteminin bu konuda açıklanan tüm proje yetenekleri için kendi desteğini tanıtması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b303-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="6b303-106">Paketlerin projenize yüklenmesini sağlamak amacıyla projenizin gerçekte sahip olmadığı yetenekleri bildirmeyin.</span><span class="sxs-lookup"><span data-stu-id="6b303-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="6b303-107">Visual Studio ve diğer uzantıların birçok özelliği NuGet istemcisinin yanı sıra proje özelliklerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="6b303-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="6b303-108">Projenizin yanlış reklam cılık yetenekleri bu bileşenlerin arızaya ve kullanıcılarınızın deneyiminin düşmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b303-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="6b303-109">Proje özelliklerinin reklamını yapmak</span><span class="sxs-lookup"><span data-stu-id="6b303-109">Advertise project capabilities</span></span>

<span data-ttu-id="6b303-110">NuGet istemcisi, aşağıdaki tabloda açıklandığı gibi, [proje özelliklerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)göre proje türünüzle hangi paketlerin uyumlu olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="6b303-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="6b303-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="6b303-111">Capability</span></span> | <span data-ttu-id="6b303-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b303-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b303-113">Assemblyreferences</span><span class="sxs-lookup"><span data-stu-id="6b303-113">AssemblyReferences</span></span> | <span data-ttu-id="6b303-114">Projenin montaj başvurularını desteklediğini gösterir (WinRTReferences'tan farklı).</span><span class="sxs-lookup"><span data-stu-id="6b303-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="6b303-115">BeyanEdilenKaynak Öğeleri</span><span class="sxs-lookup"><span data-stu-id="6b303-115">DeclaredSourceItems</span></span> | <span data-ttu-id="6b303-116">Projenin, projenin kendisinde kaynak öğeleri ni beyan ettiği tipik bir MSBuild projesi (DNX değil) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b303-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="6b303-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="6b303-117">UserSourceItems</span></span>|<span data-ttu-id="6b303-118">Kullanıcının projesine rasgele dosyalar eklemesine izin verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b303-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="6b303-119">CPS tabanlı proje sistemleri için, bu bölümün geri kalanında açıklanan proje yetenekleri için uygulama ayrıntıları sizin için yapılmıştır.</span><span class="sxs-lookup"><span data-stu-id="6b303-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="6b303-120">[CpS projelerinde proje özelliklerini bildirmeye](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)bakın.</span><span class="sxs-lookup"><span data-stu-id="6b303-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="6b303-121">VsProjectCapabilitiesPresenceChecker uygulama</span><span class="sxs-lookup"><span data-stu-id="6b303-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="6b303-122">Sınıf `VsProjectCapabilitiesPresenceChecker` aşağıdaki gibi `IVsBooleanSymbolPresenceChecker` tanımlanan arabirimi uygulamalıdır:</span><span class="sxs-lookup"><span data-stu-id="6b303-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="6b303-123">Bu arabirimin örnek bir uygulaması daha sonra olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6b303-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="6b303-124">Proje sisteminizin `ActualProjectCapabilities` gerçekte neyi desteklediğine bağlı olarak kümeden özellikler eklemeyi/kaldırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6b303-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="6b303-125">Tam açıklamalar için [proje özellikleri belgelerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="6b303-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="6b303-126">Sorgulara yanıt verme</span><span class="sxs-lookup"><span data-stu-id="6b303-126">Responding to queries</span></span>

<span data-ttu-id="6b303-127">Bir proje, `VSHPROPID_ProjectCapabilitiesChecker` özelliği ' nin . `IVsHierarchy::GetProperty`</span><span class="sxs-lookup"><span data-stu-id="6b303-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="6b303-128">Derlemede `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` tanımlanan bir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`örneğini döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="6b303-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="6b303-129">[NuGet paketini](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)yükleyerek bu derlemeye başvurun.</span><span class="sxs-lookup"><span data-stu-id="6b303-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="6b303-130">Örneğin, yönteminizin `case` `IVsHierarchy::GetProperty` `switch` deyimine aşağıdaki deyimi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b303-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="6b303-131">DTE Desteği</span><span class="sxs-lookup"><span data-stu-id="6b303-131">DTE Support</span></span>

<span data-ttu-id="6b303-132">NuGet, en üst düzey Visual Studio otomasyon arabirimi olan [DTE'ye](/dotnet/api/envdte.dte?view=visualstudiosdk-2017)çağrıda bulunarak proje sistemini referanslar, içerik öğeleri ve MSBuild içerileri eklemeye yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="6b303-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="6b303-133">DTE, zaten uygulayabileceğiniz bir COM arabirimi kümesidir.</span><span class="sxs-lookup"><span data-stu-id="6b303-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="6b303-134">Proje türünüz CPS'yi temel alırsa, DTE sizin için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="6b303-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
