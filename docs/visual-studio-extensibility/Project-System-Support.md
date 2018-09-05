---
title: Visual Studio Proje sistemi için NuGet desteği
description: Üçüncü taraf proje türleri için Visual Studio Proje sistemi NuGet tümleştirilmesi.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551376"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Visual Studio Proje sistemi için NuGet desteği

Visual Studio'da üçüncü taraf proje türlerini desteklemek için NuGet 3.x+ destekler [ortak proje System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), ve NuGet 3.2 + CPS olmayan proje sistemlerini de destekler.

Proje sistemi, NuGet ile tümleştirmek için bu konuda açıklanan tüm proje özellikleri için kendi destek tanıtma gerekir.

> [!Note]
> Projenize yüklemek için paketler etkinleştirmek için projenizin gerçekten olmayan yetenekleri bildirmeyin. NuGet istemci yanı sıra proje özellikleri Visual Studio ve diğer Uzantılar özelliklerinin çoğu bağlıdır. Projenizin özelliklerini yanlışlıkla reklam bu bileşenler, çalışmasına ve kullanıcılarınızın deneyimini düşmesine yol açabilir.

## <a name="advertise-project-capabilities"></a>Proje Özellikleri tanıtma

NuGet istemci paketler temel proje türüyle uyumlu belirler [projenin özelliklerini](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)aşağıdaki tabloda açıklandığı gibi.

| Özellik | Açıklama |
| --- | --- |
| AssemblyReferences | Proje derleme başvuruları (WinRTReferences benzersiz) desteklediğini belirtir. |
| DeclaredSourceItems | Kaynak Proje öğelerinde bildirir, proje tipik bir MSBuild Projesi (DNX değil) olduğunu gösterir. |
| UserSourceItems|Kullanıcıya rastgele dosyalar, projeye eklemek için izin verildiğini gösterir. |

Proje CPS tabanlı sistemler için sizin için bu bölümün geri kalanında açıklanan proje özellikleri uygulama ayrıntılarını gerçekleştirilmedi. Bkz: [CPS projelerinde proje özellikleri bildirme](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>VsProjectCapabilitiesPresenceChecker uygulama

`VsProjectCapabilitiesPresenceChecker` Sınıfı uygulanmalı `IVsBooleanSymbolPresenceChecker` arabirimi, şu şekilde tanımlanır:

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

Bu arabirim için bir örnek uygulama, ardından şöyle olacaktır:

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

Özelliklerini eklemek/kaldırmak unutmayın `ActualProjectCapabilities` küme, ne proje sisteminizi gerçekten desteklediğine temel. Bkz: [proje özellikleri belgeleri](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) tam açıklamaları için.

## <a name="responding-to-queries"></a>Sorgularına yanıt

Bir proje bu özelliği destekleyen bildirir `VSHPROPID_ProjectCapabilitiesChecker` özelliği aracılığıyla `IVsHierarchy::GetProperty`. Örneği döndürmelidir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, tanımlanan `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` derleme. Yükleyerek bu derlemeye başvuru [kendi NuGet paketi](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Örneğin, aşağıdaki ekleyebilirsiniz `case` deyimi, `IVsHierarchy::GetProperty` yöntemin `switch` deyimi:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE desteği

NuGet, başvurular, içerik öğeleri eklemek için proje sistemi sürücüleri ve MSBuild aktarır çağırarak [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), üst düzey Visual Studio Otomasyon arabirimi olduğu. DTE zaten uygulayabilir COM arabirimleri kümesidir.

DTE proje türünüzü CPS alıyorsa, sizin için uygulanır.
