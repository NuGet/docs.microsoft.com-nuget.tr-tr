---
title: NuGet. config dosyası başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, Solution ve packageSource bölümlerini içeren NuGet. config dosyası başvurusu.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317216"
---
# <a name="nugetconfig-reference"></a>NuGet. config başvurusu

NuGet davranışı, [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi `NuGet.Config` farklı dosyalardaki ayarlarla denetlenir.

`nuget.config`, daha sonra bu konuda açıklanan bölüm öğelerini içeren `<configuration>` üst düzey bir düğüm içeren bir XML dosyasıdır. Her bölüm sıfır veya daha fazla öğe içerir. [Örnekler yapılandırma dosyasına](#example-config-file)bakın. Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.

Bu konuda:

- [yapılandırma bölümü](#config-section)
- [Bindingyönlendirmeler bölümü](#bindingredirects-section)
- [Packageresesme bölümü](#packagerestore-section)
- [çözüm bölümü](#solution-section)
- [Paket kaynağı bölümleri](#package-source-sections):
  - [packagesonak](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledpackagesonak](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [trustedSigners bölümü](#trustedsigners-section)
- [Ortam değişkenlerini kullanma](#using-environment-variables)
- [Örnek yapılandırma dosyası](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>yapılandırma bölümü

Komutu kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir. [ `nuget config` ](../reference/cli-reference/cli-ref-config.md)

`dependencyVersion`ve `repositoryPath` yalnızca kullanan `packages.config`projeler için geçerlidir. `globalPackagesFolder`yalnızca PackageReference biçimini kullanan projeler için geçerlidir.

| Anahtar | Değer |
| --- | --- |
| dependencyversion (`packages.config` yalnızca) | Anahtar doğrudan `DependencyVersion` belirtilmediğinde, paket yükleme, geri yükleme ve güncelleştirme için varsayılan değer. `-DependencyVersion` Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır. Değerler,,, .`Highest` `Lowest` `HighestPatch` `HighestMinor` |
| globalPackagesFolder (yalnızca PackageReference kullanan projeler) | Varsayılan genel paketler klasörünün konumu. Varsayılan `%userprofile%\.nuget\packages` değer (Windows) veya `~/.nuget/packages` (Mac/Linux). Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir. Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır. |
| depoyolu (`packages.config` yalnızca) | Varsayılan `$(Solutiondir)/packages` klasör yerine NuGet paketlerinin yükleneceği konum. Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir. Bu ayar, öncelik veren NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılınır. |
| defaultPushSource | Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar. |
| http_proxy http_proxy. User http_proxy. Password no_proxy | Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` biçiminde`http://<username>:<password>@<domain>`olmalıdır. Parolalar şifrelenir ve el ile eklenemez. İçin `no_proxy`, değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir. Bu değerler için http_proxy ve no_proxy ortam değişkenlerini alternatif olarak kullanabilirsiniz. Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir. `accept`Değerler, .`require` Varsayılan olarak `accept`.

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
| Atla | Otomatik bağlama yeniden yönlendirmelerinin atlanıp atlanmayacağını belirten bir Boole değeri. Varsayılan olarak yanlıştır. |

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
| Etkinletir | NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri. Ayrıca, `EnableNuGetPackageRestore` yapılandırma dosyasında bu anahtarı ayarlamak `True` yerine, ortam değişkenini bir değeriyle ayarlayabilirsiniz. |
| otomatik | Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri. |

**Örnek**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>çözüm bölümü

Kaynak denetimine bir `packages` çözüm klasörünün eklenip eklenmeyeceğini denetler. Bu bölüm yalnızca `nuget.config` bir çözüm klasöründeki dosyalarda kullanılabilir.

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

`packageSources` ,`packageSourceCredentials` ,,`trustedSigners`Vetüm çalışmaları birlikte çalışarak, NuGet 'in yükleme, geri yükleme ve güncelleştirme işlemleri sırasında paket depolarıyla nasıl çalıştığını yapılandırır. `disabledPackageSources` `apikeys` `activePackageSource`

[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)Komutu genellikle Bu`apikeys` ayarları yönetmek için kullanılır, ancak komutu kullanılarak yönetilir ve komutu kullanılarak yönetilir. [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md)

Nuget.org için kaynak URL 'sinin olduğunu `https://api.nuget.org/v3/index.json`unutmayın.

### <a name="packagesources"></a>packagesonak

Bilinen tüm paket kaynaklarını listeler. Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır. NuGet, kullanan `packages.config`projelerle ilgili güncelleştirme ve güncelleştirme işlemlerine yönelik kaynakların sırasını duyar.

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

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Genellikle `-username` ve `-password` anahtarlarıyla belirtilenkaynaklariçinKullanıcıadlarınıveparolalarıdepolar.`nuget sources` `-storepasswordincleartext` Seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.

| Anahtar | Değer |
| --- | --- |
| kullanıcı adı | Kaynağın düz metin olarak Kullanıcı adı. |
| password | Kaynak için şifrelenmiş parola. |
| cleartextpassword | Kaynak için şifrelenmemiş parola. |

**Örnek:**

Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar ile `_x0020_`değiştirilmiştir). Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:

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

Komutuyla ayarlanan API anahtarı kimlik doğrulaması kullanan kaynaklar için anahtarları depolar. [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)

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
| (kaynağın adı) veya`All` | Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur. Eğer `All`değeri, aksi durumda `(Aggregate source)` devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için olmalıdır. |

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

Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar. Kullanıcı `signatureValidationMode` öğesine`require`ayarlandığında bu liste boş olamaz. 

Bu bölüm, [ `nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.

**Şema**:

Güvenilen bir imzalayan, belirli bir İmzalayanın `certificate` tanımlayan tüm sertifikaları içeren bir öğe koleksiyonuna sahiptir. Güvenilen bir imzalayan ya da `Author` `Repository`olabilir.

Güvenilen bir *Depo* Ayrıca depo `serviceIndex` için (geçerli `https` bir URI olması gerekir) belirtir ve isteğe bağlı olarak, bu belirli `owners` bir istemciden güvenilir bir şekilde kısıtlamak için noktalı virgülle ayrılmış bir liste belirtebilir Depo.

Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları, `SHA256`ve `SHA384` `SHA512`' dir.

Bir `certificate` ise, imza `true` doğrulamasının parçası olarak sertifika zincirini oluştururken, belirtilen sertifikanın güvenilmeyen bir köke zincirine izin verileceğini belirtir `allowUntrustedRoot` .

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

Çalışma zamanında ayarları uygulamak için değerler `nuget.config` (NuGet 3.4 +) cinsinden ortam değişkenlerini kullanabilirsiniz.

Örneğin, `HOME` Windows üzerindeki ortam değişkeni olarak `c:\users\username`ayarlandıysa `%HOME%\NuGetRepository` , yapılandırma dosyasındaki değeri olarak `c:\users\username\NuGetRepository`çözümlenir.

Benzer şekilde, Mac/Linux `%HOME%/NuGetRepository` , olarak `/home/myStuff`ayarlanmışsa yapılandırma dosyasında olarak `/home/myStuff/NuGetRepository`çözümlenir. `HOME`

Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır.

## <a name="example-config-file"></a>Örnek yapılandırma dosyası

Aşağıda, bir dizi `nuget.config` ayarı gösteren örnek bir dosya verilmiştir:

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
