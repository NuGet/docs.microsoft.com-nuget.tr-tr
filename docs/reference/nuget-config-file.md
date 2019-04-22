---
title: nuget.config dosyası başvurusu
description: NuGet.Config dosyası başvurusu yapılandırma, SecurityPermission packageRestore, çözüm ve packageSource bölümler dahil olmak üzere.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911094"
---
# <a name="nugetconfig-reference"></a>nuget.config başvurusu

NuGet davranışını farklı ayarları tarafından denetlenir `NuGet.Config` dosyaları açıklandığı [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` bir üst düzey içeren bir XML dosyası `<configuration>` düğümü, ardından bu konuda açıklanan bölüm öğeleri içerir. Her bölüm, sıfır veya daha fazla öğe içerir. Bkz: [örnek yapılandırma dosyası](#example-config-file). Ayar adları büyük/küçük harfe ve değerlerini kullanabilirsiniz [ortam değişkenlerini](#using-environment-variables).

Bu konuda:

- [yapılandırma bölümü](#config-section)
- [SecurityPermission bölümü](#bindingredirects-section)
- [packageRestore bölümü](#packagerestore-section)
- [Çözüm bölümü](#solution-section)
- [Paket kaynak bölümler](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [trustedSigners bölümü](#trustedsigners-section)
- [Ortam değişkenlerini kullanma](#using-environment-variables)
- [Örnek yapılandırma dosyası](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>yapılandırma bölümü

Kullanarak ayarlayabileceğiniz çeşitli yapılandırma ayarlarını içeren [ `nuget config` komut](../tools/cli-ref-config.md).

`dependencyVersion` ve `repositoryPath` kullanarak projeleri için geçerli `packages.config`. `globalPackagesFolder` PackageReference biçimini kullanan projeler için geçerlidir.

| Anahtar | Değer |
| --- | --- |
| dependencyVersion (`packages.config` yalnızca) | Varsayılan `DependencyVersion` değeri paket yükleme, geri yükleme ve güncelleştirme, zaman `-DependencyVersion` anahtar doğrudan belirtiliyor. Bu değer ayrıca NuGet Paket Yöneticisi kullanıcı Arabirimi tarafından kullanılır. Değerler `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (PackageReference yalnızca kullanarak projeleri) | Varsayılan Genel paketleri klasörün konumu. Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux). Göreli bir yol projeye özgü kullanılabilir `nuget.config` dosyaları. Bu ayarı önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı. |
| repositoryPath (`packages.config` yalnızca) | NuGet paketleri yerine varsayılan yükleme konumu `$(Solutiondir)/packages` klasör. Göreli bir yol projeye özgü kullanılabilir `nuget.config` dosyaları. Bu ayarı önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı. |
| defaultPushSource | URL veya yol için bir işlem başka bir paket kaynaklarını bulunmazsa, varsayılan olarak kullanılması gereken paket kaynağının tanımlar. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Paket kaynaklarını bağlanırken kullanması için proxy ayarlarını; `http_proxy` biçiminde olması gerektiğini `http://<username>:<password>@<domain>`. Parolaları şifrelenir ve el ile eklenemez. İçin `no_proxy`, değeri etki alanlarının virgülle ayrılmış listesi olduğu proxy sunucusunu atla. Alternatif olarak, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz. Ek ayrıntılar için bkz. [NuGet proxy ayarlarını](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Paket yüklemesi için paket imzaları doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir. Değerler `accept`, `require`. Varsayılan olarak `accept`.

**Örnek**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>SecurityPermission bölümü

Bir paketi yüklendiğinde NuGet otomatik bağlama yeniden yönlendirmeleri yapar paylaşamayacağını yapılandırır.

| Anahtar | Değer |
| --- | --- |
| Atla | Otomatik bağlama yeniden yönlendirmeleri atlanmayacağını belirten bir Boole değeri. Varsayılan olarak yanlıştır. |

**Örnek**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore bölümü

Denetimleri paket geri yükleme sırasında oluşturur.

| Anahtar | Değer |
| --- | --- |
| Etkin | NuGet otomatik geri yükleme gerçekleştirme olup olmadığını gösteren bir Boole değeri. Ayrıca `EnableNuGetPackageRestore` ortam değişkeni değerinin `True` yerine bu anahtarı yapılandırma dosyasında ayarı. |
| otomatik | NuGet eksik paketleri için bir yapı sırasında denetleyin olup olmadığını gösteren bir Boole değeri. |

**Örnek**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Çözüm bölümü

Denetimleri olmadığını `packages` bir çözüm klasörü kaynak denetimine dahil edilir. Bu bölüm yalnızca çalışır `nuget.config` çözüm klasöründe bulunan dosyaları.

| Anahtar | Değer |
| --- | --- |
| disableSourceControlIntegration | Kaynak denetimi ile çalışırken packages klasörünü yoksay verilip verilmeyeceğini gösteren bir Boole değeri. Varsayılan değer false'tur. |

**Örnek**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Paket kaynak bölümler

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` Ve `trustedSigners` birlikte yükleme, geri yükleme ve güncelleştirme işlemleri sırasında NuGet paketi depoları ile nasıl çalıştığını yapılandırmak için tüm işler.

[ `nuget sources` Komut](../tools/cli-ref-sources.md) dışında bu ayarları yönetmek için genel olarak kullanılan `apikeys` hangi kullanılarak yönetilir [ `nuget setapikey` komut](../tools/cli-ref-setapikey.md), ve `trustedSigners` hangi yönetilir kullanarak [ `nuget trusted-signers` komut](../tools/cli-ref-trusted-signers.md).

Nuget.org kaynak URL'si Not `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Tüm bilinen paket kaynaklarını listeler. Geri yükleme işlemleri sırasında ve herhangi bir projeyi PackageReference biçimi kullanarak ile sırası göz ardı edilir. NuGet kaynakları sırasını yükleme için uyar ve güncelleştirme işlemleri kullanarak projeleriyle `packages.config`.

| Anahtar | Değer |
| --- | --- |
| (adı paket kaynağına atamak için) | Yol veya paket kaynağının URL'si. |

**Örnek**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Kullanıcı adları ve parolalar kaynakları, genellikle ile belirtilen için depolar `-username` ve `-password` ile geçer `nuget sources`. Parolaları sürece varsayılan olarak şifrelenmiş `-storepasswordincleartext` seçeneği de kullanılır.

| Anahtar | Değer |
| --- | --- |
| kullanıcı adı | Kaynak düz metin biçiminde kullanıcı adı. |
| password | Kaynağı için şifrelenmiş parola. |
| cleartextpassword | Kaynağı için şifrelenmemiş parola. |

**Örnek:**

Yapılandırma dosyasında `<packageSourceCredentials>` öğeyi içeren her bir geçerli kaynak adı için alt düğümleri (adında boşluklar ile değiştirilir `_x0020_`). Diğer bir deyişle, "Contoso" ve "Test kaynağı" olarak adlandırılan kaynaklar için yapılandırma dosyasına aşağıdaki şifrelenmiş parolalar kullanırken içerir:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

Şifrelenmemiş parolaları kullanırken:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

Depolar ile belirlenen API anahtar kimlik doğrulaması kullanan kaynakları için anahtarları [ `nuget setapikey` komut](../tools/cli-ref-setapikey.md).

| Anahtar | Değer |
| --- | --- |
| (kaynak URL) | Şifrelenmiş API anahtarı. |

**Örnek**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Şu anda devre dışı bırakılmış kaynakları belirledik. Boş olabilir.

| Anahtar | Değer |
| --- | --- |
| (kaynak adı) | Kaynak etkinleştirilip etkinleştirilmeyeceğini gösteren bir Boole değeri. |

**Örnek:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(yalnızca 2.x; 3.x+ içinde kullanım dışı)*

Etkin kaynak tanımlayan veya toplama tüm kaynakları gösterir.

| Anahtar | Değer |
| --- | --- |
| (kaynak adı) veya `All` | Anahtarı bir kaynak adı ise kaynak yolu veya URL değerdir. Varsa `All`, değeri `(Aggregate source)` Aksi durumda devre dışı paket kaynaklarının tümüne birleştirilecek. |

**Örnek**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>trustedSigners bölümü

Depoları İmzalayanları paketi yüklemek veya geri yükleme sırasında izin vermek için kullanılan güvenilir. Kullanıcı ayarlar, bu liste boş olamaz `signatureValidationMode` için `require`. 

Bu bölümde ile güncelleştirilebilir [ `nuget trusted-signers` komut](../tools/cli-ref-trusted-signers.md).

**Şema**:

Güvenilen imzalayan koleksiyonu vardır `certificate` verilen imzalayan tanımlayan tüm sertifikaları listeleme öğeleri. Güvenilen imzalayan olabilir bir `Author` veya `Repository`.

Güvenilen bir *depo* ayrıca belirtir `serviceIndex` deponun (sahip geçerli bir `https` URI'si) ve isteğe bağlı olarak noktalı virgülle ayrılmış listesini belirtebilirsiniz `owners` daha güvenilir kim kısıtlamak için Bu özel depodan.

Sertifika parmak izi için kullanılan desteklenen karma algoritmaları `SHA256`, `SHA384` ve `SHA512`.

Varsa bir `certificate` belirtir `allowUntrustedRoot` olarak `true` verilen sertifika zinciri güvenilmeyen bir kökü için imza doğrulaması bir parçası olarak sertifika zinciri oluşturulurken izin verilir.

**Örnek**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a>Ortam değişkenlerini kullanma

Ortam değişkenleri kullanabilirsiniz `nuget.config` çalışma zamanında değerleri (ayarları uygulamak için NuGet 3.4 +).

Örneğin, varsa `HOME` Windows ortam değişkeni ayarlandığında `c:\users\username`, ardından değerini `%HOME%\NuGetRepository` dosya yapılandırmada çözümler `c:\users\username\NuGetRepository`.

Benzer şekilde, varsa `HOME` Mac/Linux üzerinde ayarlanır `/home/myStuff`, ardından `%HOME%/NuGetRepository` dosya yapılandırmada çözümler `/home/myStuff/NuGetRepository`.

Bir ortam değişkeni bulunamadı, NuGet yapılandırma dosyasından değişmez değer kullanır.

## <a name="example-config-file"></a>Örnek yapılandırma dosyası

Aşağıda bir örnek verilmiştir `nuget.config` ayar gösterilmektedir dosyanın:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
