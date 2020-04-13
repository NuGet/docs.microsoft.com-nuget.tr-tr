---
title: Proje biçimini tanımlama
description: Proje biçiminizin nasıl kimliklendirilebildiğini açıklar
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488488"
---
# <a name="identify-the-project-format"></a>Proje biçimini tanımlama

NuGet tüm .NET projeleri ile çalışır. Ancak, proje biçimi (SDK stili veya SDK tarzı olmayan) NuGet paketlerini tüketmek ve oluşturmak için kullanmanız gereken araçlar ve yöntemlerden bazılarını belirler. SDK tarzı projeler [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanır. NuGet paketlerini tüketmek ve oluşturmak için kullandığınız yöntemler ve araçlar proje biçimine bağlı olduğundan proje türünü belirlemek önemlidir. SDK tarzı olmayan projelerde, yöntem ve araçlar da projenin biçime geçirilip `PackageReference` geçirilemediğine bağlıdır.

Projenizin SDK tarzı olup olmaması, projeyi oluşturmak için kullanılan yönteme bağlıdır. Aşağıdaki tablo, Visual Studio 2017 ve sonraki sürümleri kullanarak oluşturduğunuzda projeniz için varsayılan proje biçimini ve ilişkili CLI aracını gösterir.

| Proje&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Varsayılan proje biçimi | CLI aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Notlar |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK stili | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 öncesinde oluşturulan projeler SDK tarzı değildir. CLI'yi kullanın. `nuget.exe` |
| .NET Core | SDK stili | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017 öncesinde oluşturulan projeler SDK tarzı değildir. CLI'yi kullanın. `nuget.exe` |
| .NET Framework | SDK tarzı olmayan | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | .DIĞER yöntemler kullanılarak oluşturulan NET Framework projeleri SDK tarzı projeler olabilir. Bunlar için [dotnet CLI'yi](../install-nuget-client-tools.md#dotnetexe-cli) kullanın. |
| [Geçirilen](../consume-packages/migrate-packages-config-to-package-reference.md) .NET projesi | SDK tarzı olmayan| Paket oluşturmak için, paketleri oluşturmak için [msbuild -t:pack'i](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) kullanın. | Paketleri oluşturmak `msbuild -t:pack` için, önerilir. Aksi takdirde, [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli)kullanın. Geçirilen projeler SDK tarzı projeler değildir. |

## <a name="check-the-project-format"></a>Proje biçimini denetleme

Projenin SDK tarzı biçiminde olup olmadığından emin değilseniz, proje dosyasındaki `<Project>` öğedeki SDK özniteliğini arayın (C#, bu *.csproj dosyasıdır). Varsa, proje SDK tarzı bir projedir.

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

## <a name="check-the-project-format-in-visual-studio"></a>Visual Studio'da proje biçimini kontrol edin

Visual Studio'da çalışıyorsanız, aşağıdaki yöntemlerden birini kullanarak proje biçimini hızlı bir şekilde kontrol edebilirsiniz:

- Solution Explorer'da projeyi sağ tıklatın ve **myprojectname.csproj'u edin'i**seçin.

   Bu seçenek yalnızca Visual Studio 2017'den itibaren SDK stili özniteliği kullanan projeler için kullanılabilir. Aksi takdirde, diğer yöntemi kullanın.

   ![Proje dosyasını düzenlemesi](media/edit-project-file.png)

   SDK tarzı bir proje, proje dosyasında [SDK özniteliğini](/dotnet/core/tools/csproj#additions) gösterir.
   
- **Project** menüsünden **Project'i Boşalt'ı** seçin (veya projeyi sağ tıklatın ve **Project'i Boşalt'ı**seçin).

   Bu proje, proje dosyasına SDK özniteliğini içermez. Bu Bir SDK tarzı proje değildir.

   ![Projeyi boşaltma](media/unload-project.png)

   Ardından, boşaltılan projeyi sağ tıklatın ve **myprojectname.csproj'u edit'i**seçin.

## <a name="see-also"></a>Ayrıca bkz.

- [dotnet CLI ile .NET Standart Paketleri Oluşturun](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Visual Studio ile .NET Standart Paketleri Oluşturun](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Bir .NET Framework paketi oluşturma ve yayımla (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet paketi ve MSBuild hedefleri olarak geri yükleme](../reference/msbuild-targets.md)
