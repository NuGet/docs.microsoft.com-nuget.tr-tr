---
title: NuGet çoklu platform kimlik doğrulaması eklentisi
description: NuGet. exe, DotNet. exe, MSBuild. exe ve Visual Studio için NuGet platformlar arası kimlik doğrulama eklentileri
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317275"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet çoklu platform kimlik doğrulaması eklentisi

Sürüm 4.8 + ' de tüm NuGet istemcileri (NuGet. exe, Visual Studio, DotNet. exe ve MSBuild. exe), [NuGet platformlar arası eklenti](NuGet-Cross-Platform-Plugins.md) modelinin üzerinde oluşturulmuş bir kimlik doğrulama eklentisi kullanabilir.

## <a name="authentication-in-dotnetexe"></a>DotNet. exe ' de kimlik doğrulaması

Visual Studio ve NuGet. exe varsayılan olarak etkileşimlidir. NuGet. exe [etkileşimli olmayan](../nuget-exe-CLI-Reference.md)hale getirmek için bir anahtar içerir.
Ayrıca, NuGet. exe ve Visual Studio eklentileri kullanıcıdan giriş ister.
DotNet. exe ' de istem yoktur ve varsayılan değer etkileşimsiz olur.

DotNet. exe ' deki kimlik doğrulama mekanizması cihaz akışdır. Geri yükleme veya paket ekleme işlemi etkileşimli olarak çalıştırıldığında, işlem blokları ve Kullanıcı kimlik doğrulamaları nasıl tamamlanacaktır komut satırında sağlanır.
Kullanıcı kimlik doğrulamasını tamamladığında işlem devam edecektir.

İşlemi etkileşimli hale getirmek için bir geçişi `--interactive`gerekir.
Şu anda yalnızca açık `dotnet restore` ve `dotnet add package` komutlar etkileşimli bir anahtarı destekler.
`dotnet build` Ve`dotnet publish`üzerinde etkileşimli bir anahtar yoktur.

## <a name="authentication-in-msbuild"></a>MSBuild 'te kimlik doğrulaması

DotNet. exe ' ye benzer şekilde, MSBuild. exe varsayılan olarak etkileşimli olmayan MSBuild. exe kimlik doğrulama mekanizması cihaz akışdır.
Geri yüklemenin duraklamasını ve kimlik doğrulaması beklemesini sağlamak için geri yükleme `msbuild -t:restore -p:NuGetInteractive="true"`çağrısı yapın.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Platformlar arası kimlik doğrulama eklentisi oluşturma

Örnek bir uygulama, [Microsoft kimlik bilgisi sağlayıcısı eklentisi](https://github.com/Microsoft/artifacts-credprovider)' nde bulunabilir.

Eklentilerin NuGet istemci araçları tarafından belirlenen güvenlik gereksinimlerine uygun olması çok önemlidir.
Bir eklentinin kimlik doğrulama eklentisi olması için gereken en düşük sürüm *2.0.0*' dir.
NuGet, desteklenen işlem talepleri için eklenti ve sorgu ile el sıkışma gerçekleştirecek.
Belirli iletiler hakkında daha fazla ayrıntı için lütfen NuGet platformlar arası eklenti [protokol iletilerine](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) bakın.

NuGet, günlük düzeyini ayarlar ve uygun olduğunda eklenti için proxy bilgilerini sağlar.
NuGet konsolunda günlüğe kaydetme yalnızca NuGet, günlük düzeyini eklenti olarak ayarladıktan sonra kabul edilebilir.

- .NET Framework eklentisi kimlik doğrulama davranışı

.NET Framework, eklentilerden bir iletişim kutusu biçiminde kullanıcıdan giriş yapmasına izin verilir.

- .NET Core eklentisi kimlik doğrulama davranışı

.NET Core 'da bir iletişim kutusu gösterilemez. Eklentiler kimlik doğrulamak için cihaz akışını kullanmalıdır.
Eklenti, Kullanıcı talimatlarına sahip NuGet 'e günlük iletileri gönderebilir.
Günlük düzeyi eklentiye ayarlandıktan sonra günlüğe kaydetme 'nin kullanılabilir olduğunu unutmayın.
NuGet, komut satırından etkileşimli giriş almaz.

İstemci eklentiyi bir Get kimlik doğrulama kimlik bilgileriyle çağırdığında, eklentilerin etkileşim anahtarına uyması ve iletişim kutusu anahtarına uyması gerekir. 

Aşağıdaki tabloda, eklentinin tüm birleşimler için nasıl davranması özetlenmektedir.

| IBU etkileşimsiz | CanShowDialog | Eklenti davranışı |
| ---------------- | ------------- | --------------- |
| true | true | Etkileşimli olmayan anahtar, iletişim kutusu anahtarından önceliklidir. Eklentinin bir iletişim kutusu açmasına izin verilmiyor. Bu bileşim yalnızca .NET Framework eklentileri için geçerlidir |
| true | false | Etkileşimli olmayan anahtar, iletişim kutusu anahtarından önceliklidir. Eklentinin engellenmesine izin verilmiyor. Bu bileşim yalnızca .NET Core eklentileri için geçerlidir |
| false | true | Eklenti bir iletişim kutusu göstermelidir. Bu bileşim yalnızca .NET Framework eklentileri için geçerlidir |
| false | false | Eklenti bir iletişim kutusu gösteremez/gösteremez. Eklenti, günlükçü aracılığıyla bir yönerge iletisini günlüğe kaydederek kimlik doğrulamak için cihaz akışını kullanmalıdır. Bu bileşim yalnızca .NET Core eklentileri için geçerlidir |

Bir eklenti yazmadan önce lütfen aşağıdaki özelliklere bakın.

- [NuGet paketi Indirme eklentisi](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet çapraz Plat kimlik doğrulama eklentisi](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
