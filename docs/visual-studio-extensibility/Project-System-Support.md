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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Visual Studio proje sistemi için NuGet desteği

Visual Studio'da üçüncü taraf proje türlerini desteklemek için NuGet 3.x+, [Ortak Proje Sistemi'ni (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)ve NuGet 3.2+CPS olmayan proje sistemlerini de destekler.

NuGet ile tümleştirmek için, bir proje sisteminin bu konuda açıklanan tüm proje yetenekleri için kendi desteğini tanıtması gerekir.

> [!Note]
> Paketlerin projenize yüklenmesini sağlamak amacıyla projenizin gerçekte sahip olmadığı yetenekleri bildirmeyin. Visual Studio ve diğer uzantıların birçok özelliği NuGet istemcisinin yanı sıra proje özelliklerine bağlıdır. Projenizin yanlış reklam cılık yetenekleri bu bileşenlerin arızaya ve kullanıcılarınızın deneyiminin düşmesine neden olabilir.

## <a name="advertise-project-capabilities"></a>Proje özelliklerinin reklamını yapmak

NuGet istemcisi, aşağıdaki tabloda açıklandığı gibi, [proje özelliklerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)göre proje türünüzle hangi paketlerin uyumlu olduğunu belirler.

| Özellik | Açıklama |
| --- | --- |
| Assemblyreferences | Projenin montaj başvurularını desteklediğini gösterir (WinRTReferences'tan farklı). |
| BeyanEdilenKaynak Öğeleri | Projenin, projenin kendisinde kaynak öğeleri ni beyan ettiği tipik bir MSBuild projesi (DNX değil) olduğunu gösterir. |
| UserSourceItems|Kullanıcının projesine rasgele dosyalar eklemesine izin verildiğini gösterir. |

CPS tabanlı proje sistemleri için, bu bölümün geri kalanında açıklanan proje yetenekleri için uygulama ayrıntıları sizin için yapılmıştır. [CpS projelerinde proje özelliklerini bildirmeye](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)bakın.

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>VsProjectCapabilitiesPresenceChecker uygulama

Sınıf `VsProjectCapabilitiesPresenceChecker` aşağıdaki gibi `IVsBooleanSymbolPresenceChecker` tanımlanan arabirimi uygulamalıdır:

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

Bu arabirimin örnek bir uygulaması daha sonra olacaktır:

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

Proje sisteminizin `ActualProjectCapabilities` gerçekte neyi desteklediğine bağlı olarak kümeden özellikler eklemeyi/kaldırmayı unutmayın. Tam açıklamalar için [proje özellikleri belgelerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) bakın.

## <a name="responding-to-queries"></a>Sorgulara yanıt verme

Bir proje, `VSHPROPID_ProjectCapabilitiesChecker` özelliği ' nin . `IVsHierarchy::GetProperty` Derlemede `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` tanımlanan bir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`örneğini döndürmelidir. [NuGet paketini](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)yükleyerek bu derlemeye başvurun.

Örneğin, yönteminizin `case` `IVsHierarchy::GetProperty` `switch` deyimine aşağıdaki deyimi ekleyebilirsiniz:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE Desteği

NuGet, en üst düzey Visual Studio otomasyon arabirimi olan [DTE'ye](/dotnet/api/envdte.dte?view=visualstudiosdk-2017)çağrıda bulunarak proje sistemini referanslar, içerik öğeleri ve MSBuild içerileri eklemeye yönlendirir. DTE, zaten uygulayabileceğiniz bir COM arabirimi kümesidir.

Proje türünüz CPS'yi temel alırsa, DTE sizin için uygulanır.
