---
title: NuGet çapraz platform kimlik doğrulaması eklentisi
description: NuGet.exe, dotnet.exe, msbuild.exe ve Visual Studio için NuGet çapraz platform kimlik doğrulaması eklentileri
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: d80339eb81ade1cf2c323a604cc4fac06dcb1012
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981060"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet çapraz platform kimlik doğrulaması eklentisi

4.8 +, istemciler (NuGet.exe, Visual Studio, dotnet.exe ve MSBuild.exe), üst kısmındaki yerleşik bir kimlik doğrulama eklentisini kullanabileceğiniz tüm NuGet sürümünde [çapraz platform eklentileri NuGet](NuGet-Cross-Platform-Plugins.md) modeli.

## <a name="authentication-in-dotnetexe"></a>Dotnet.exe kimlik doğrulaması

Visual Studio ve NuGet.exe varsayılan etkileşimli olarak var. NuGet.exe sağlamak için bir anahtar içeren [etkileşimli olmayan](../../tools/nuget-exe-CLI-Reference.md).
Buna ek olarak NuGet.exe ve Visual Studio eklentileri giriş kullanıcıdan.
İçinde dotnet.exe yoktur hiç sormak ve etkileşimli olmayan bir varsayılandır.

Cihaz akışı dotnet.exe içinde kimlik doğrulama mekanizmasıdır. Zaman geri yükleme veya paket işlemi işlemi engeller ve kullanıcıya nasıl için tam kimlik doğrulamaları sağlanacaktır komut satırında yönergeleri etkileşimli olarak çalıştırılır.
Kullanıcı kimlik doğrulaması tamamlandığında işlemi devam eder.

Etkileşimli işlem yapmak için bir geçmelidir `--interactive`.
Şu anda yalnızca dolayımsız `dotnet restore` ve `dotnet add package` komutları destekleyen etkileşimli bir anahtar.
Etkileşimli anahtarı olmadan yoktur `dotnet build` ve `dotnet publish`.

## <a name="authentication-in-msbuild"></a>MSBuild içinde kimlik doğrulaması

Dotnet.exe, MSBuild.exe varsayılan olmayan cihaz akışını etkileşimli MSBuild.exe kimlik doğrulama mekanizması olan benzer.
Geri yüklemeyi duraklatmak ve kimlik doğrulaması için beklemesi izin vermek için geri yükleme işlemi çağırma `msbuild /t:restore /p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Platformlar arası kimlik doğrulaması eklentisi oluşturma

Örnek uygulama bulunabilir [Microsoft kimlik bilgisi sağlayıcı eklentisi](https://github.com/Microsoft/artifacts-credprovider).

Eklentileri NuGet istemci araçları tarafından ortaya konan güvenlik gereksinimlerine uyup çok önemlidir.
Gereken en düşük sürümü için bir kimlik doğrulama eklentisini olacak şekilde bir eklenti *2.0.0*.
NuGet için desteklenmeyen bir işlem talepleri el sıkışması eklentisi ve sorgu gerçekleştirir.
Çapraz platform eklentisi NuGet edinmek [iletişim kuralı iletileri](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) belirli iletileri hakkında daha fazla ayrıntı için.

NuGet günlük düzeyini ayarlamak ve uygun olduğunda eklentisi için proxy bilgilerini belirtin.
NuGet, eklenti için günlük düzeyi ayarladıktan sonra için NuGet günlüğü yalnızca kabul edilebilir konsoludur.

- .NET framework eklenti kimlik doğrulama davranışı

.NET Framework, eklentiler bir kullanıcıdan bir iletişim kutusu biçiminde bir giriş için izin verilir.

- .NET core eklentisi kimlik doğrulama davranışı

' De .NET Core, bir iletişim kutusu gösterilemiyor. Eklentileri cihaz akışı kimlik doğrulaması yapmak için kullanmanız gerekir.
Eklenti kullanıcı yönergeleri için NuGet günlük iletileri gönderebilir.
Günlük düzeyi eklentisi için ayarlandıktan sonra günlük kullanılabilir olduğunu unutmayın.
NuGet komut satırından etkileşimli herhangi bir giriş olmayacaktır.

İstemci eklentisi edinin kimlik doğrulama kimlik bilgileri olan çağırdığında, eklentileri etkileşim geçiş için uygun ve iletişim anahtar saygı gerekir. 

Aşağıdaki tabloda, eklenti tüm birleşimlerini nasıl davranacağı özetlenmektedir.

| IsNonInteractive | CanShowDialog | Eklenti davranışı |
| ---------------- | ------------- | --------------- |
| true | true | IsNonInteractive anahtar iletişim geçiş daha önceliklidir. Eklenti, bir iletişim kutusu açılır izin verilmiyor. Bu birleşim yalnızca .NET Framework eklenti için geçerlidir |
| true | false | IsNonInteractive anahtar iletişim geçiş daha önceliklidir. Eklenti engellemek için izin verilmiyor. Bu birleşim yalnızca .NET Core eklentileri için geçerlidir |
| false | true | Eklenti, bir iletişim kutusu göstermelidir. Bu birleşim yalnızca .NET Framework eklenti için geçerlidir |
| false | false | Eklenti iletişim kutusu göstermek can değil. Eklenti cihaz akış Günlükçü üzerinden bir yönerge ileti günlüğü tarafından kimlik doğrulaması yapmak için kullanmanız gerekir. Bu birleşim yalnızca .NET Core eklentileri için geçerlidir |

Lütfen aşağıdaki özellikleri için bir eklenti yazmadan önce bakın.

- [NuGet paketini indirme eklentisi](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet kimlik doğrulama eklentisini plat çapraz](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
