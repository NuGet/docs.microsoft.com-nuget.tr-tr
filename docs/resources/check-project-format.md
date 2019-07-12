---
title: Proje biçimi tanımlayın
description: Kimlik için projenizi biçimini açıklar
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843520"
---
# <a name="identify-the-project-format"></a>Proje biçimi tanımlayın

NuGet tüm .NET projeleriyle çalışır. Ancak, proje biçimi (SDK stilinde veya SDK stilinde olmayan) bazı araçlar ve kullanmak ve NuGet paketleri oluşturmak için kullanmanız gereken yöntemleri belirler. SDK stili projeleri kullanmak [SDK özniteliği](/dotnet/core/tools/csproj#additions). Kullanma ve NuGet paketleri oluşturmak için kullandığınız araçları ve yöntemleri üzerinde proje biçimi bağımlı olduğundan, proje türünü tanımlamak önemlidir. SDK stili projeleri için Araçlar ve yöntemler de bağımlı olup olmadığını proje için geçirilmiş olan üzerinde `PackageReference` biçimi.

Projenize SDK stilinde olup, projeyi oluşturmak için kullandığınız yönteme bağlıdır. Visual Studio 2017 ve sonraki sürümler kullanarak oluşturduğunuzda varsayılan proje biçimi ve ilişkili CLI aracı projeniz için aşağıdaki tabloda gösterilmektedir.

| Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Varsayılan proje biçimi | CLI aracı&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Notlar |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK stili | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017'den önce oluşturulan projeleri olmayan-SDK-style ' dir. Kullanım `nuget.exe` CLI. |
| .NET Core | SDK stili | [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Visual Studio 2017'den önce oluşturulan projeleri olmayan-SDK-style ' dir. Kullanım `nuget.exe` CLI. |
| .NET Framework | SDK stili | [nuget.exe CLI](../install-nuget-client-tools.md#nugetexe-cli) | Diğer yöntemleri kullanarak oluşturulan .NET framework projeleri SDK stili projeleri olabilir. Bu, [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) yerine. |
| [Geçirilen](../reference/migrate-packages-config-to-package-reference.md) .NET projesi | SDK stili| Paket oluşturmak üzere kullanmak [msbuild - t: paketi](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) paketleri oluşturmak için. | Paket oluşturmayı `msbuild -t:pack` önerilir. Aksi takdirde kullanın [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli). Geçirilen proje SDK stili projeleri değildir. |

## <a name="check-the-project-format"></a>Proje biçimini denetleyin

Proje SDK stilinde biçim olup olmadığından emin değilseniz SDK'sı özniteliğinde arayın `<Project>` öğesi proje dosyasında (için C#, bu *.csproj dosyasıdır). Varsa, projeye bir SDK stilinde bir projedir.

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

## <a name="check-the-project-format-in-visual-studio"></a>Visual Studio'da proje biçimini denetleyin

Visual Studio'da çalışıyorsanız, aşağıdaki yöntemlerden birini kullanarak proje biçimi hızlı bir şekilde denetleyebilirsiniz:

- Çözüm Gezgini'nde projeye sağ tıklayıp **myprojectname.csproj Düzenle**.

   Bu seçenek, yalnızca SDK stilinde öznitelik kullanan projeler için Visual Studio 2017'de başlayarak kullanılabilir. Aksi takdirde, diğer bir yöntem kullanın.

   ![Proje dosyası Düzenle](media/edit-project-file.png)

   SDK stili projeyi gösteren [SDK özniteliği](/dotnet/core/tools/csproj#additions) proje dosyasındaki.
   
- Gelen **proje** menüsünde seçin **projeyi** (veya projeye sağ tıklayıp seçin **projeyi**).

   Bu proje, proje dosyasında SDK özniteliği içermeyecek. SDK stili projesi değil.

   ![Projeyi](media/unload-project.png)

   Ardından bellekten projeye sağ tıklayın ve seçin **myprojectname.csproj Düzenle**.

## <a name="see-also"></a>Ayrıca bkz.

- [Dotnet CLI ile .NET standart paketleri oluşturma](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Visual Studio ile .NET standart paketleri oluşturma](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [.NET Framework paketi (Visual Studio) oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet paketi ve MSBuild hedefleri olarak geri yükleme](../reference/msbuild-targets.md)
