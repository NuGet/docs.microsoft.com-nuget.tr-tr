---
title: NuGet. config dosyası başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, Solution ve packageSource bölümlerini içeren NuGet. config dosyası başvurusu.
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230532"
---
# <a name="nugetconfig-reference"></a>NuGet. config başvurusu

NuGet davranışı, [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi farklı `NuGet.Config` veya `nuget.config` dosyalardaki ayarlarla denetlenir.

`nuget.config`, daha sonra bu konuda açıklanan bölüm öğelerini içeren üst düzey bir `<configuration>` düğümü içeren bir XML dosyasıdır. Her bölüm sıfır veya daha fazla öğe içerir. [Örnekler yapılandırma dosyasına](#example-config-file)bakın. Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>yapılandırma bölümü

[`nuget config` komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir.

`dependencyVersion` ve `repositoryPath` yalnızca `packages.config`kullanan projelere uygulanır. `globalPackagesFolder` yalnızca PackageReference biçimi kullanan projeler için geçerlidir.

| Anahtar | Değer |
| --- | --- |
| dependencyVersion (yalnızca`packages.config`) | `-DependencyVersion` anahtarı doğrudan belirtilmediğinde paket yükleme, geri yükleme ve güncelleştirme için varsayılan `DependencyVersion` değeri. Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır. Değerler `Lowest`, `HighestPatch`, `HighestMinor``Highest`. |
| globalPackagesFolder (yalnızca PackageReference kullanan projeler) | Varsayılan genel paketler klasörünün konumu. Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux). Göreli bir yol, projeye özgü `nuget.config` dosyalarında kullanılabilir. Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır. |
| Depoyolu (yalnızca`packages.config`) | Varsayılan `$(Solutiondir)/packages` klasörü yerine NuGet paketlerinin yükleneceği konum. Göreli bir yol, projeye özgü `nuget.config` dosyalarında kullanılabilir. Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır. |
| defaultPushSource | Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar. |
| http_proxy http_proxy. User http_proxy. Password no_proxy | Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` `http://<username>:<password>@<domain>`biçiminde olmalıdır. Parolalar şifrelenir ve el ile eklenemez. `no_proxy`, değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir. Ayrıca, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz. Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir. Değerler `accept`, `require`. 
          `accept` değerini varsayılan olarak alır.

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

## <a name="bindingredirects-section"></a>Bindingyönlendirmeler bölümü

Bir paket yüklendiğinde NuGet 'in otomatik bağlama yeniden yönlendirmelerini yapıp yönlendirmeyeceğini yapılandırır.

| Anahtar | Değer |
| --- | --- |
| Atla | Otomatik bağlama yeniden yönlendirmelerinin atlanıp atlanmayacağını belirten bir Boole değeri. Varsayılan değer false. |

**Örnek**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Packageresesme bölümü

Derlemeler sırasında paket geri yüklemeyi denetler.

| Anahtar | Değer |
| --- | --- |
| enabled | NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri. Ayrıca, yapılandırma dosyasında bu anahtarı ayarlamak yerine `EnableNuGetPackageRestore` ortam değişkenini `True` bir değerle ayarlayabilirsiniz. |
| otomatik | Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri. |

**Örnek**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>çözüm bölümü

Bir çözümün `packages` klasörünün kaynak denetimine dahil edilip edilmeyeceğini denetler. Bu bölüm yalnızca bir çözüm klasöründeki `nuget.config` dosyalarında geçerlidir.

| Anahtar | Değer |
| --- | --- |
| Disablesourcecontrolintefini | Kaynak denetimiyle çalışırken paketler klasörünün yoksayılıp yoksayılmadığını gösteren bir Boole değeri. Varsayılan değer false'tur. |

**Örnek**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Paket kaynak bölümleri

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` ve `trustedSigners`, yükleme, geri yükleme ve güncelleştirme işlemleri sırasında NuGet 'in paket depolarıyla nasıl çalıştığını yapılandırmak için birlikte çalışır.

[`nuget sources` komutu](../reference/cli-reference/cli-ref-sources.md) genellikle bu ayarları yönetmek için kullanılır; [`nuget setapikey` komutu](../reference/cli-reference/cli-ref-setapikey.md)kullanılarak yönetilen `apikeys` ve [`nuget trusted-signers` komutu](../reference/cli-reference/cli-ref-trusted-signers.md)kullanılarak yönetilen `trustedSigners`.

Nuget.org için kaynak URL 'sinin `https://api.nuget.org/v3/index.json`olduğunu unutmayın.

### <a name="packagesources"></a>packagesonak

Bilinen tüm paket kaynaklarını listeler. Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır. NuGet, `packages.config`kullanarak projelerle ilgili Install ve Update işlemlerine yönelik kaynak sırasını uyar.

| Anahtar | Değer |
| --- | --- |
| (paket kaynağına atanacak ad) | Paket kaynağının yolu veya URL 'SI. |

**Örnek**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> Belirli bir düğüm için `<clear />` mevcut olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar. [Ayarların nasıl uygulandığı hakkında daha fazla bilgi edinin](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Genellikle `-username` ve `-password` anahtarlarıyla belirtilen `nuget sources`olan kaynaklar için Kullanıcı adlarını ve parolaları depolar. `-storepasswordincleartext` seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.

| Anahtar | Değer |
| --- | --- |
| kullanıcı adı | Kaynağın düz metin olarak Kullanıcı adı. |
| password | Kaynak için şifrelenmiş parola. |
| cleartextpassword | Kaynak için şifrelenmemiş parola. |

**Örnek:**

Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar `_x0020_`ile değiştirilmiştir). Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:

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

Şifrelenmemiş parolalar kullanırken:

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

### <a name="apikeys"></a>apikeys tuşları

API anahtar kimlik doğrulaması kullanan kaynaklar için [`nuget setapikey` komutuyla](../reference/cli-reference/cli-ref-setapikey.md)ayarlanan anahtarları depolar.

| Anahtar | Değer |
| --- | --- |
| (kaynak URL) | Şifrelenmiş API anahtarı. |

**Örnek**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledpackagesonak

Şu anda devre dışı olan kaynaklar tanımlandı. Boş olabilir.

| Anahtar | Değer |
| --- | --- |
| (kaynağın adı) | Kaynağın devre dışı olup olmadığını gösteren bir Boole değeri. |

**Örnek:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(yalnızca 2. x, 3. x + ' de kullanım dışı)*

Şu anda etkin olan kaynağı tanımlar veya tüm kaynakların toplamasını gösterir.

| Anahtar | Değer |
| --- | --- |
| (kaynağın adı) veya `All` | Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur. `All`, aksi durumda devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için değer `(Aggregate source)` olmalıdır. |

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

Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar. Kullanıcı `require``signatureValidationMode` ayarladığında bu liste boş olamaz. 

Bu bölüm [`nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.

**Şema**:

Güvenilen bir imzalayan, belirli bir İmzalayanın tanımlayan tüm sertifikaların listelendiği `certificate` öğeleri koleksiyonuna sahiptir. Güvenilen bir imzalayan bir `Author` veya `Repository`olabilir.

Güvenilen *Depo* Ayrıca, deponun `serviceIndex` (geçerli bir `https` URI olması gerekir) belirtir ve isteğe bağlı olarak, belirli bir depodan daha fazla güvenilir olan bir `owners` noktalı virgülle ayrılmış listesi belirtebilir.

Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları `SHA256`, `SHA384` ve `SHA512`.

Bir `certificate` `true` `allowUntrustedRoot` belirtiyorsa, belirtilen sertifikanın, imza doğrulamasının bir parçası olarak sertifika zincirini oluştururken güvenilmeyen bir köke zincirine izin verilir.

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

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders bölümü

*(3,5 +)* Paket, geri dönüş klasörlerinde bulunursa hiçbir işin gerçekleştirilmesi gerekmediği için paketleri önceden yüklemeye yönelik bir yol sağlar. Geri dönüş paketi klasörleri, genel paket klasörüyle aynı klasöre ve dosya yapısına sahiptir: *. nupkg* var ve tüm dosyalar ayıklandı.

Bu yapılandırma için arama mantığı:

- Paketin/sürümün zaten indirildiğini görmek için genel paket klasörüne bakın.

- Paket/sürüm eşleşmesi için geri dönüş klasörlerine bakın.

Her iki arama başarılı olursa, indirme gerekmez.

Bir eşleşme bulunmazsa, NuGet dosya kaynaklarını ve ardından http kaynakları ' nı denetleyip paketleri indirir.

| Anahtar | Değer |
| --- | --- |
| (geri dönüş klasörünün adı) | Geri dönüş klasörünün yolu. |

**Örnek**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement bölümü

Varsayılan paket yönetim biçimini Package *. config* ya da packagereference olarak ayarlar. SDK stilindeki projeler her zaman PackageReference kullanır.

| Anahtar | Değer |
| --- | --- |
| biçim | Varsayılan paket yönetimi biçimini gösteren bir Boole değeri. `1`, format, PackageReference olur. `0`, biçim *Packages. config*olur. |
| devre dışı | İlk paket yüklemesi sırasında varsayılan bir paket biçimi seçme isteminin gösterilip gösterilmeyeceğini belirten bir Boole değeri. `False`, istemi gizler. |

**Örnek**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Ortam değişkenlerini kullanma

Çalışma zamanında ayarları uygulamak için, `nuget.config` değerlerinde (NuGet 3.4 +) ortam değişkenlerini kullanabilirsiniz.

Örneğin, Windows üzerinde `HOME` ortam değişkeni `c:\users\username`olarak ayarlanırsa, yapılandırma dosyasındaki `%HOME%\NuGetRepository` değeri `c:\users\username\NuGetRepository`olarak çözümlenmektedir.

Windows stili ortam değişkenlerini (başladığı ve bitişi%) kullanmanız gerektiğini unutmayın Mac/Linux üzerinde bile. Yapılandırma dosyasında `$HOME/NuGetRepository` olması çözümlenmeyecektir. Mac/Linux üzerinde `%HOME%\NuGetRepository` değeri `/home/myStuff/NuGetRepository`çözümlenir.

Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır.

## <a name="example-config-file"></a>Örnek yapılandırma dosyası

Aşağıda, isteğe bağlı olanlar dahil olmak üzere bir dizi ayarı gösteren örnek bir `nuget.config` dosyası verilmiştir:

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
