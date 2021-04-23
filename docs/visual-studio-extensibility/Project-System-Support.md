---
title: Visual Studio proje sistemi için NuGet desteği
description: NuGet 'i üçüncü taraf proje türleri için Visual Studio proje sistemine tümleştirme.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 9f1ddfd20835cc3a0f9af40a8b4e712c218b31bc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901414"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="fb776-103">Visual Studio proje sistemi için NuGet desteği</span><span class="sxs-lookup"><span data-stu-id="fb776-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="fb776-104">Visual Studio 'da üçüncü taraf proje türlerini desteklemek için, NuGet 3. x + [ortak proje sistemini (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)destekler ve NuGet 3.2 +, CPS olmayan proje sistemlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="fb776-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="fb776-105">NuGet ile tümleştirilen bir proje sistemi, bu konuda açıklanan tüm proje özellikleri için kendi desteğini tanıtmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fb776-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="fb776-106">Projenizin gerçekten, kuruluşunuzda yüklenmek üzere paketlerinin etkinleştirilmesi için sahip olmadığı özellikleri bildirme.</span><span class="sxs-lookup"><span data-stu-id="fb776-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="fb776-107">Visual Studio ve diğer uzantıların pek çok özelliği, NuGet istemcisinin yanı sıra proje özelliklerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fb776-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="fb776-108">Projenizin özelliklerini özellikle duyurmaya, bu bileşenlere hatalı ve kullanıcılarınızın düşmesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="fb776-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="fb776-109">Proje yeteneklerini tanıtma</span><span class="sxs-lookup"><span data-stu-id="fb776-109">Advertise project capabilities</span></span>

<span data-ttu-id="fb776-110">NuGet istemcisi, aşağıdaki tabloda açıklandığı gibi [projenin özelliklerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)göre proje yazanlarla uyumlu olan paketleri belirler.</span><span class="sxs-lookup"><span data-stu-id="fb776-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="fb776-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="fb776-111">Capability</span></span> | <span data-ttu-id="fb776-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fb776-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb776-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="fb776-113">AssemblyReferences</span></span> | <span data-ttu-id="fb776-114">Projenin derleme başvurularını desteklediğini belirtir (Wınrtreferences 'dan farklıdır).</span><span class="sxs-lookup"><span data-stu-id="fb776-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="fb776-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="fb776-115">DeclaredSourceItems</span></span> | <span data-ttu-id="fb776-116">Projenin projedeki kaynak öğeleri bildirdiği tipik bir MSBuild projesi (DNX değil) olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fb776-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="fb776-117">Usersourceıtems</span><span class="sxs-lookup"><span data-stu-id="fb776-117">UserSourceItems</span></span>|<span data-ttu-id="fb776-118">Kullanıcının projesine rastgele dosyalar eklemesine izin verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="fb776-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="fb776-119">CPS tabanlı proje sistemleri için, bu bölümün geri kalanında açıklanan proje özelliklerine yönelik uygulama ayrıntıları sizin için yapılır.</span><span class="sxs-lookup"><span data-stu-id="fb776-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="fb776-120">Bkz. [CPS projelerinde proje yeteneklerini bildirme](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="fb776-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="fb776-121">VsProjectCapabilitiesPresenceChecker uygulama</span><span class="sxs-lookup"><span data-stu-id="fb776-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="fb776-122">`VsProjectCapabilitiesPresenceChecker`Sınıfı, `IVsBooleanSymbolPresenceChecker` aşağıdaki gibi tanımlanan arabirimi uygulamalıdır:</span><span class="sxs-lookup"><span data-stu-id="fb776-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="fb776-123">Bu arabirimin örnek bir uygulama şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="fb776-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="fb776-124">`ActualProjectCapabilities`Proje sisteminizin gerçekten ne desteklediğine göre, kümeden Özellik eklemeyi/kaldırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fb776-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="fb776-125">Tüm açıklamalar için [Proje özellikleri belgelerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="fb776-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="fb776-126">Sorgulara yanıt verme</span><span class="sxs-lookup"><span data-stu-id="fb776-126">Responding to queries</span></span>

<span data-ttu-id="fb776-127">Bir proje  `VSHPROPID_ProjectCapabilitiesChecker` , özelliği aracılığıyla özelliğini destekleyerek bu yeteneği bildirir `IVsHierarchy::GetProperty` .</span><span class="sxs-lookup"><span data-stu-id="fb776-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="fb776-128">Bu, derlemede tanımlanan bir örneğini döndürmelidir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` .</span><span class="sxs-lookup"><span data-stu-id="fb776-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="fb776-129">[NuGet paketini](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)yükleyerek bu derlemeye başvurun.</span><span class="sxs-lookup"><span data-stu-id="fb776-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="fb776-130">Örneğin, aşağıdaki `case` ifadeyi `IVsHierarchy::GetProperty` yönteminizin `switch` ifadesine ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fb776-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="fb776-131">DTE desteği</span><span class="sxs-lookup"><span data-stu-id="fb776-131">DTE Support</span></span>

<span data-ttu-id="fb776-132">NuGet, üst düzey Visual Studio Otomasyon arabirimi olan [DTE](/dotnet/api/envdte.dte)'ye çağırarak başvuruları, içerik öğelerini ve MSBuild içeri aktarmaları eklemek için proje sistemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="fb776-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="fb776-133">DTE, zaten uygulayabileceğiniz bir COM arabirimleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="fb776-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="fb776-134">Proje türü CPS 'yi temel alıyorsa, DTE sizin için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fb776-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
