---
title: Visual Studio proje sistemi için NuGet desteği
description: NuGet 'i üçüncü taraf proje türleri için Visual Studio proje sistemine tümleştirme.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779406"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Visual Studio proje sistemi için NuGet desteği

Visual Studio 'da üçüncü taraf proje türlerini desteklemek için, NuGet 3. x + [ortak proje sistemini (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)destekler ve NuGet 3.2 +, CPS olmayan proje sistemlerini destekler.

NuGet ile tümleştirilen bir proje sistemi, bu konuda açıklanan tüm proje özellikleri için kendi desteğini tanıtmalıdır.

> [!Note]
> Projenizin gerçekten, kuruluşunuzda yüklenmek üzere paketlerinin etkinleştirilmesi için sahip olmadığı özellikleri bildirme. Visual Studio ve diğer uzantıların pek çok özelliği, NuGet istemcisinin yanı sıra proje özelliklerine bağlıdır. Projenizin özelliklerini özellikle duyurmaya, bu bileşenlere hatalı ve kullanıcılarınızın düşmesine neden olabilir.

## <a name="advertise-project-capabilities"></a>Proje yeteneklerini tanıtma

NuGet istemcisi, aşağıdaki tabloda açıklandığı gibi [projenin özelliklerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)göre proje yazanlarla uyumlu olan paketleri belirler.

| Özellik | Açıklama |
| --- | --- |
| AssemblyReferences | Projenin derleme başvurularını desteklediğini belirtir (Wınrtreferences 'dan farklıdır). |
| DeclaredSourceItems | Projenin projedeki kaynak öğeleri bildirdiği tipik bir MSBuild projesi (DNX değil) olduğunu gösterir. |
| Usersourceıtems|Kullanıcının projesine rastgele dosyalar eklemesine izin verildiğini gösterir. |

CPS tabanlı proje sistemleri için, bu bölümün geri kalanında açıklanan proje özelliklerine yönelik uygulama ayrıntıları sizin için yapılır. Bkz. [CPS projelerinde proje yeteneklerini bildirme](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>VsProjectCapabilitiesPresenceChecker uygulama

`VsProjectCapabilitiesPresenceChecker`Sınıfı, `IVsBooleanSymbolPresenceChecker` aşağıdaki gibi tanımlanan arabirimi uygulamalıdır:

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

Bu arabirimin örnek bir uygulama şöyle olacaktır:

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

`ActualProjectCapabilities`Proje sisteminizin gerçekten ne desteklediğine göre, kümeden Özellik eklemeyi/kaldırmayı unutmayın. Tüm açıklamalar için [Proje özellikleri belgelerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) bakın.

## <a name="responding-to-queries"></a>Sorgulara yanıt verme

Bir proje  `VSHPROPID_ProjectCapabilitiesChecker` , özelliği aracılığıyla özelliğini destekleyerek bu yeteneği bildirir `IVsHierarchy::GetProperty` . Bu, derlemede tanımlanan bir örneğini döndürmelidir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` . [NuGet paketini](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)yükleyerek bu derlemeye başvurun.

Örneğin, aşağıdaki `case` ifadeyi `IVsHierarchy::GetProperty` yönteminizin `switch` ifadesine ekleyebilirsiniz:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE desteği

NuGet, üst düzey Visual Studio Otomasyon arabirimi olan [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017)'ye çağırarak başvuruları, içerik öğelerini ve MSBuild içeri aktarmaları eklemek için proje sistemini çağırır. DTE, zaten uygulayabileceğiniz bir COM arabirimleri kümesidir.

Proje türü CPS 'yi temel alıyorsa, DTE sizin için uygulanır.
