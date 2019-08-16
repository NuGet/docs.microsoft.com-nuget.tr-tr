---
title: Proje biçimini tanımla
description: Proje biçiminizi nasıl kullanacağınızı açıklar
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488488"
---
# <a name="identify-the-project-format"></a>Proje biçimini tanımla

NuGet tüm .NET projeleriyle birlikte çalışmaktadır. Ancak, proje biçimi (SDK stili veya SDK olmayan stili), NuGet paketlerini tüketmek ve oluşturmak için kullanmanız gereken bazı araç ve yöntemleri belirler. SDK stili projeler [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanır. NuGet paketlerini tüketmek ve oluşturmak için kullandığınız yöntemler ve araçlar proje biçimine bağlı olduğundan, proje türünü tanımlamak önemlidir. SDK olmayan stil projeleri için, Yöntemler ve araçlar projenin `PackageReference` biçime geçirilme biçimine de bağlıdır.

Projenizin SDK stili olup olmadığı veya proje oluşturmak için kullanılan yönteme bağlı olup olmadığı. Aşağıdaki tabloda, Visual Studio 2017 ve sonraki sürümlerini kullanarak oluşturduğunuzda projeniz için varsayılan proje biçimi ve ilişkili CLı aracı gösterilmektedir.

| Proje&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Varsayılan proje biçimi | CLı aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Notlar |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK stili | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 ' den önce oluşturulan projeler SDK olmayan stillerdir. CLI `nuget.exe` kullanın. |
| .NET Core | SDK stili | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 ' den önce oluşturulan projeler SDK olmayan stillerdir. CLI `nuget.exe` kullanın. |
| .NET Framework | SDK olmayan stil | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | Diğer yöntemler kullanılarak oluşturulan .NET Framework projeleri SDK stilinde projeler olabilir. Bunlar için bunun yerine [DotNet CLI](../install-nuget-client-tools.md#dotnetexe-cli) kullanın. |
| [Geçirilen](../consume-packages/migrate-packages-config-to-package-reference.md) .NET projesi | SDK olmayan stil| Paket oluşturmak için, paketler oluşturmak üzere [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) kullanın. | Paket `msbuild -t:pack` oluşturmak için önerilir. Aksi takdirde, [DotNet CLI](../install-nuget-client-tools.md#dotnetexe-cli)kullanın. Geçirilen projeler SDK stilinde projeler değildir. |

## <a name="check-the-project-format"></a>Proje biçimini denetle

Projenin SDK stili biçim olup olmadığı konusunda emin değilseniz, proje dosyasındaki `<Project>` öğesinde SDK özniteliğini arayın (için C#, bu, *. csproj dosyasıdır). Varsa, proje bir SDK stili projem olur.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Visual Studio 'da proje biçimini denetleme

Visual Studio 'da çalışıyorsanız, aşağıdaki yöntemlerden birini kullanarak proje biçimini hızlıca kontrol edebilirsiniz:

- Çözüm Gezgini projeye sağ tıklayın ve **MyProjectName. csproj Düzenle**' yi seçin.

   Bu seçenek yalnızca SDK stili özniteliği kullanan projeler için Visual Studio 2017 ' den itibaren kullanılabilir. Aksi takdirde, diğer yöntemi kullanın.

   ![Proje dosyasını düzenleme](media/edit-project-file.png)

   SDK stili bir proje, proje dosyasında [SDK özniteliğini](/dotnet/core/tools/csproj#additions) gösterir.
   
- **Proje** menüsünden **Projeyi Kaldır** ' ı seçin (veya projeye sağ tıklayıp **Projeyi Kaldır**' ı seçin).

   Bu proje, proje dosyasında SDK özniteliğini içermez. Bu bir SDK stili proje değildir.

   ![Projeyi Kaldır](media/unload-project.png)

   Ardından, yüklenmeyen projeye sağ tıklayın ve **MyProjectName. csproj öğesini Düzenle**' yi seçin.

## <a name="see-also"></a>Ayrıca bkz.

- [DotNet CLı ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Visual Studio ile .NET Standard paketleri oluşturma](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [.NET Framework paketi oluşturma ve yayımlama (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md)
