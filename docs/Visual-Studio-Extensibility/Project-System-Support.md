---
title: "NuGet Visual Studio Proje sistemi desteği | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 9d7fa7f6-82ed-4df6-9734-f43a3d8e3b98
description: "Üçüncü taraf proje türleri için Visual Studio Proje sistemine NuGet tümleştirilmesi."
keywords: "NuGet Visual Studio, özel proje türleri, Visual Studio projeleri"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8cad46f18578bec41bd9280985e42972a9b3c1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>NuGet Visual Studio Proje sistemi desteği

Visual Studio'da üçüncü taraf proje türlerini desteklemek için NuGet 3.x+ destekleyen [ortak proje System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), NuGet 3.2 + CPS olmayan proje sistemlerini destekler.

NuGet ile tümleştirmek için bir proje sistem bu konuda açıklanan tüm proje özelliklerini kendi desteği tanıtır gerekir.


> [!NOTE]
> Projenizde yüklemek paketler etkinleştirmek amacıyla projenize gerçekten yok özellikleri bildirme. Proje Özellikleri NuGet istemci yanı sıra Visual Studio ve diğer uzantıları özelliklerinin çoğu bağlıdır. Yanlışlıkla projenizi yeteneklerini reklam çalışmasına bu bileşenler ve kullanıcılarınızın deneyimini düşmesine yol açabilir.

## <a name="advertise-project-capabilities"></a>Proje Özellikleri tanıtma

Hangi paketlerin göre proje türü ile uyumlu olan NuGet istemcisi belirler [projenin özellikleri](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)aşağıdaki tabloda açıklandığı gibi.


|Özellik|Açıklama|
|----------------|-----------|
|AssemblyReferences|Proje derleme başvurularını (WinRTReferences farklı) desteklediğini gösterir|
|DeclaredSourceItems|Proje kaynak öğeleri bildirir, proje tipik bir MSBuild proje (değil DNX) olduğunu belirtir (yerine bir `project.json` klasördeki tüm dosyaları bir derlemenin parçası olduğunu varsayar dosyası).|
|UserSourceItems|Kullanıcı kendi projeye rastgele dosyalar eklemek için izin verildiğini gösterir.|

Proje CPS tabanlı sistemler için sizin için bu bölümün geri kalanında tanımlanan proje özellikleri uygulama ayrıntılarını yapılmış. Bkz: [CPS projelerinde proje özellikleri bildirme](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>VsProjectCapabilitiesPresenceChecker uygulama

`VsProjectCapabilitiesPresenceChecker` Sınıfı uygulanmalı `IVsBooleanSymbolPresenceChecker` şu şekilde tanımlanır arabirimi:

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


Bu arabirim için bir örnek uygulama sonra olacaktır:
    
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

Özelliklerini eklemek/kaldırmak unutmayın `ActualProjectCapabilities` kümesi tabanlı ne proje sisteminizi gerçekte desteklediğine. Bkz: [proje özellikleri belgelerine](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) tam açıklamaları için.

## <a name="responding-to-queries"></a>Sorgularına yanıt

Bir proje destekleyerek bu özelliği bildirir `VSHPROPID_ProjectCapabilitiesChecker` özelliği üzerinden `IVsHierarchy::GetProperty`. Örneği döndürmelidir `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, içinde tanımlanan `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` derleme. Yükleyerek bu derleme başvurusu [NuGet paketi](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Örneğin, aşağıdaki ekleyebilirsiniz `case` deyimi, `IVsHierarchy::GetProperty` yöntemin `switch` deyimi:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE desteği

NuGet başvuruları, içerik öğelerini eklemek için proje sistemi sürücüleri ve MSBuild alır çağırarak [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), üst düzey Visual Studio Otomasyon arabirimi olduğu. DTE zaten uygulayabilir COM arabirimleri kümesidir.

Proje türü üzerinde CPS temel alıyorsa, DTE sizin için uygulanır.
