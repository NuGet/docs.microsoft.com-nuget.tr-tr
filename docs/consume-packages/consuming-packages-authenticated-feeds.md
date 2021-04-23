---
title: Kimliği doğrulanmış akışlardan paketleri kullanma
description: Tüm NuGet istemci senaryolarında kimliği doğrulanmış akışlardan paketleri kullanma
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901518"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Kimliği doğrulanmış akışlardan paketleri kullanma

Nuget.org [genel akışına](https://api.nuget.org/v3/index.json)ek olarak, NuGet istemcilerinin dosya akışlarıyla ve özel http akışlarıyla etkileşim kurma olanağı vardır.


Özel http akışlarıyla kimlik doğrulaması yapmak için 2 yaklaşımlar şunlardır:

* [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials) kimlik bilgilerini ekleme
* Kullanılan istemciye bağlı olarak birçok genişletilebilirlik modelinden birini kullanarak kimlik doğrulaması yapın.

## <a name="nuget-clients-authentication-extensibility"></a>NuGet istemcilerinin kimlik doğrulama genişletilebilirliği

Çeşitli NuGet istemcileri için, özel akış sağlayıcısı kimlik doğrulamasından sorumludur.
Tüm NuGet istemcilerinin bunu desteklemeye yönelik genişletilebilirlik yöntemleri vardır. Bunlar, kimlik bilgilerini almak için NuGet ile iletişim kurabilen bir Visual Studio uzantısıdır veya bir eklentidir.

### <a name="visual-studio"></a>Visual Studio

NuGet, Visual Studio 'da akış sağlayıcılarının müşterilerine uygulayabilen ve sunabilmeniz için bir arabirim sunar. Daha fazla ayrıntı için lütfen [Visual Studio kimlik bilgisi sağlayıcısı oluşturma](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)hakkındaki belgelere bakın.

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio için kullanılabilir NuGet kimlik bilgileri sağlayıcıları

Azure DevOps 'u desteklemek için Visual Studio 'da yerleşik olarak bulunan bir kimlik bilgisi sağlayıcısı vardır.


Kullanılabilir eklenti kimlik bilgileri sağlayıcıları şunları içerir:

* [Visual Studio için MyGet kimlik bilgileri sağlayıcısı](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

`nuget.exe`Bir akış ile kimlik doğrulaması yapmak için kimlik bilgileri gerektiğinde, bunları aşağıdaki şekilde arar:

1. Dosyalardaki kimlik bilgilerini arayın `NuGet.config` .
1. V2 eklenti kimlik bilgisi sağlayıcılarını kullanma
1. V1 eklenti kimlik bilgisi sağlayıcılarını kullanma
1. Ardından NuGet, kullanıcıdan komut satırında kimlik bilgilerini ister.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe ve v2 kimlik bilgileri sağlayıcıları

Sürüm `4.8` NuGet sürümünde yeni bir kimlik doğrulama eklentisi mekanizması tanımlanmış ve bundan sonra v2 kimlik bilgileri sağlayıcıları olarak anılacaktır.
Bu sağlayıcıların yüklenmesi ve bulunması için bkz. [NuGet platformlar arası eklentileri](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe ve v1 kimlik bilgileri sağlayıcıları

Sürüm `3.3` NuGet sürümünde kimlik doğrulama eklentileri 'nin ilk sürümü tanıtılmıştır.
Bu sağlayıcıların yüklenmesi ve bulunması için [nuget.exe kimlik bilgileri sağlayıcılarına](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery) başvurur

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe için kullanılabilir kimlik bilgileri sağlayıcıları

* [Azure DevOps v2 kimlik bilgileri sağlayıcıları](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) veya [Azure Artifacts kimlik bilgisi sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 sürüm 15,9 ve sonraki sürümlerde, Azure DevOps kimlik bilgisi sağlayıcısı Visual Studio 'da paketlenmiştir.
`nuget.exe`Bu belirli Visual Studio araç takımından MSBuild kullanıyorsa, eklenti otomatik olarak keşfedilir.

### <a name="dotnetexe"></a>dotnet.exe

`dotnet.exe`Bir akış ile kimlik doğrulaması yapmak için kimlik bilgileri gerektiğinde, bunları aşağıdaki şekilde arar:

1. Dosyalardaki kimlik bilgilerini arayın `NuGet.config` .
1. V2 eklenti kimlik bilgisi sağlayıcılarını kullanma

, Varsayılan olarak `dotnet.exe` etkileşimli değildir, bu nedenle, `--interactive` kimlik doğrulaması için engelleme aracını almak üzere bir bayrak geçirmeniz gerekebilir.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe ve v2 kimlik bilgileri sağlayıcıları

SDK sürümünde `2.2.100` , NuGet tüm istemcilerde çalışacak bir kimlik doğrulama eklentisi mekanizması tanımladı.
Bu sağlayıcıların yüklenmesi ve bulunması için bkz. [NuGet platformlar arası eklentileri](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe için kullanılabilir kimlik bilgileri sağlayıcıları

* [Azure Artifacts kimlik bilgisi sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

`MSBuild.exe`Bir akış ile kimlik doğrulaması yapmak için kimlik bilgileri gerektiğinde, bunları aşağıdaki şekilde arar:

1. Dosyalardaki kimlik bilgilerini ara `NuGet.config`
1. V2 eklenti kimlik bilgisi sağlayıcılarını kullanma

Varsayılan olarak `MSBuild.exe` etkileşimli değildir, bu nedenle, bir `/p:NuGetInteractive=true` Aracı kimlik doğrulama için engellemek için özelliği ayarlamanız gerekebilir.

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe ve v2 kimlik bilgileri sağlayıcıları

Visual Studio 2019 güncelleştirme 9 ' da, NuGet tüm istemcilerde çalışacak bir kimlik doğrulama eklentisi mekanizması tanımladı.
Bu sağlayıcıların yüklenmesi ve bulunması için bkz. [NuGet platformlar arası eklentileri](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>MSBuild.exe için kullanılabilir kimlik bilgileri sağlayıcıları

* [Azure Artifacts kimlik bilgisi sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 güncelleştirme 9 ve üzeri sürümlerde, Azure DevOps kimlik bilgisi sağlayıcısı Visual Studio 'da paketlenmiştir. Ek adım gerekmez.
