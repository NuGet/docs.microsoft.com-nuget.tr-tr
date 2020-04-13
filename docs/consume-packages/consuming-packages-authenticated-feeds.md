---
title: Kimlik doğrulama akışlarından paketleri tüketme
description: Tüm NuGet istemci senaryolarında kimlik doğrulama akışlarından paketleri tüketme
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231793"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Kimlik doğrulama akışlarından paketleri tüketme

[nuget.org genel beslemeye](https://api.nuget.org/v3/index.json)ek olarak, NuGet istemcileri dosya akışları ve özel http akışları ile etkileşim yeteneğine sahiptir.


Özel http beslemeleri ile doğrulamak için, 2 yaklaşımlar şunlardır:

* [NuGet.config'e](../reference/nuget-config-file.md#packagesourcecredentials) kimlik bilgileri ekleme
* Kullanılan istemciye bağlı olarak birçok genişletilebilirlik modellerinden birini kullanarak kimlik doğrulaması yapın.

## <a name="nuget-clients-authentication-extensibility"></a>NuGet istemcilerinin kimlik doğrulama genişletilebilirliği

Çeşitli NuGet istemcileri için, özel özet akışı sağlayıcısının kendisi kimlik doğrulamadan sorumludur.
Tüm NuGet istemcilerinin bunu desteklemek için genişletilebilirlik yöntemleri vardır. Bunlar, kimlik bilgilerini almak için NuGet ile iletişim kurabilen bir Visual Studio uzantısı veya eklentidir.

### <a name="visual-studio"></a>Visual Studio

Visual Studio'da NuGet, besleme sağlayıcılarının müşterilerine uygulayabileceği ve sağlayabileceği bir arabirimi ortaya çıkarır. Daha fazla bilgi için lütfen [Visual Studio kimlik bilgileri sağlayıcısının nasıl oluşturulabildiğini](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)gösteren belgelere bakın.

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio için kullanılabilir NuGet kimlik bilgileri sağlayıcıları

Azure DevOps'leri desteklemek için Visual Studio'da yerleşik bir kimlik bilgisi sağlayıcısı vardır.


Kullanılabilir eklenti kimlik bilgileri sağlayıcıları şunlardır:

* [Visual Studio için MyGet Kimlik Sağlayıcısı](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Bir `nuget.exe` özet akışıyla kimlik bilgilerinin doğrulanması gerektiğinde, bunları aşağıdaki şekilde arar:

1. Dosyalardaki kimlik `NuGet.config` bilgilerine bakın.
1. V2 eklenti kimlik bilgileri sağlayıcılarını kullanma
1. V1 eklenti kimlik bilgileri sağlayıcılarını kullanma
1. NuGet daha sonra komut satırında kimlik bilgileri için kullanıcı ister.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe ve V2 kimlik bilgileri sağlayıcıları

Sürümde `4.8` NuGet yeni bir kimlik doğrulama eklentisi mekanizması tanımlı, bundan sonra V2 kimlik bilgileri sağlayıcıları olarak anılacaktır.
Bu sağlayıcıların kurulumu ve keşfi için [NuGet çapraz platform eklentilerine](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)bakın.

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe ve V1 kimlik bilgileri sağlayıcıları

Sürümde `3.3` NuGet kimlik doğrulama eklentilerinin ilk sürümünü tanıttı.
Bu sağlayıcıların kurulumu ve keşfi için [nuget.exe kimlik bilgileri sağlayıcılarına](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery) başvurun

#### <a name="available-credential-providers-for-nugetexe"></a>nuget.exe için kullanılabilir kimlik bilgileri sağlayıcıları

* [Azure DevOps V2 Kimlik Bilgileri Sağlayıcıları](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) veya [Azure Yapıları Kimlik Bilgileri Sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 sürüm 15.9 ve sonraki sürümlerle Azure DevOps kimlik bilgileri sağlayıcısı Visual Studio'da birlikte sunulur.
Belirli `nuget.exe` bir Visual Studio araç setinden MSBuild kullanıyorsa, eklenti otomatik olarak keşfedilir.

### <a name="dotnetexe"></a>dotnet.exe

Bir `dotnet.exe` özet akışıyla kimlik bilgilerinin doğrulanması gerektiğinde, bunları aşağıdaki şekilde arar:

1. Dosyalardaki kimlik `NuGet.config` bilgilerine bakın.
1. V2 eklenti kimlik bilgileri sağlayıcılarını kullanma

Varsayılan `dotnet.exe` olarak etkileşimli değildir, bu nedenle `--interactive` aracı kimlik doğrulaması için engellemek için bir bayrak geçirmeniz gerekebilir.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe ve V2 kimlik bilgileri sağlayıcıları

SDK `2.2.100` sürümünde, NuGet tüm istemcilerde çalışan bir kimlik doğrulama eklentisi mekanizması tanımlamıştır.
Bu sağlayıcıların kurulumu ve keşfi için [NuGet çapraz platform eklentilerine](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)bakın.

#### <a name="available-credential-providers-for-dotnetexe"></a>dotnet.exe için kullanılabilir kimlik bilgileri sağlayıcıları

* [Azure Yapıları Kimlik Bilgileri Sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>Msbuild.exe

Bir `MSBuild.exe` özet akışıyla kimlik bilgilerinin doğrulanması gerektiğinde, bunları aşağıdaki şekilde arar:

1. Dosyalarda `NuGet.config` kimlik bilgilerini arama
1. V2 eklenti kimlik bilgileri sağlayıcılarını kullanma

Varsayılan `MSBuild.exe` olarak etkileşimli değildir, bu nedenle `/p:NuGetInteractive=true` aracı kimlik doğrulaması için engellemek için özelliği ayarlamanız gerekebilir.

#### <a name="msbuildexe-and-v2-credential-providers"></a>MSBuild.exe ve V2 kimlik bilgileri sağlayıcıları

Visual Studio 2019 Update 9'da NuGet, tüm istemcilerde çalışan bir kimlik doğrulama eklentisi mekanizması tanımladı.
Bu sağlayıcıların kurulumu ve keşfi için [NuGet çapraz platform eklentilerine](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)bakın.

#### <a name="available-credential-providers-for-msbuildexe"></a>MSBuild.exe için kullanılabilir kimlik bilgileri sağlayıcıları

* [Azure Yapıları Kimlik Bilgileri Sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)

Visual Studio 2017 Update 9 ve sonraki bilgileriyle Azure DevOps kimlik bilgileri sağlayıcısı Visual Studio'da birlikte sunulur. Ek adım gerekmez.
