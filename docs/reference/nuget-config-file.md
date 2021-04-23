---
title: nuget.config dosya başvurusu
description: Config, Bindingyönlendirmeler, Packageresist, çözüm ve packageSource bölümlerini içeren dosya başvurusunu NuGet.Config.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 38620058bccde876152328302a6049f011c149db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901869"
---
# <a name="nugetconfig-reference"></a>`nuget.config` başvurunun

NuGet davranışı, `NuGet.Config` `nuget.config` [yaygın NuGet yapılandırmalarında](../consume-packages/configuring-nuget-behavior.md)açıklandığı gibi farklı veya dosyalardaki ayarlarla denetlenir.

`nuget.config``<configuration>`, daha sonra bu konuda açıklanan bölüm öğelerini içeren üst düzey bir düğüm içeren BIR XML dosyasıdır. Her bölüm sıfır veya daha fazla öğe içerir. [Örnekler yapılandırma dosyasına](#example-config-file)bakın. Ayar adları büyük/küçük harfe duyarlıdır ve değerler [ortam değişkenlerini](#using-environment-variables)kullanabilir.

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>yapılandırma bölümü

[ `nuget config` Komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak ayarlanbilen çeşitli yapılandırma ayarlarını içerir.

`dependencyVersion` ve `repositoryPath` yalnızca kullanan projeler için geçerlidir `packages.config` . `globalPackagesFolder` yalnızca PackageReference biçimini kullanan projeler için geçerlidir.

| Anahtar | Değer |
| --- | --- |
| dependencyVersion ( `packages.config` yalnızca) | `DependencyVersion`Anahtar doğrudan belirtilmediğinde, paket yükleme, geri yükleme ve güncelleştirme için varsayılan değer `-DependencyVersion` . Bu değer, NuGet Paket Yöneticisi Kullanıcı arabirimi tarafından da kullanılır. Değerler,,, `Lowest` `HighestPatch` `HighestMinor` `Highest` . |
| globalPackagesFolder (yalnızca PackageReference kullanan projeler) | Varsayılan genel paketler klasörünün konumu. Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux). Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir. Bu ayar, `NUGET_PACKAGES` Öncelik alan ortam değişkeni tarafından geçersiz kılınır. |
| Depoyolu ( `packages.config` yalnızca) | Varsayılan klasör yerine NuGet paketlerinin yükleneceği konum `$(Solutiondir)/packages` . Göreli bir yol, projeye özgü `nuget.config` dosyalarda kullanılabilir. Bu ayar, `NUGET_PACKAGES` Öncelik alan ortam değişkeni tarafından geçersiz kılınır. |
| defaultPushSource | Bir işlem için başka bir paket kaynağı bulunmazsa varsayılan olarak kullanılması gereken paket kaynağının URL 'sini veya yolunu tanımlar. |
| http_proxy http_proxy. User http_proxy. Password no_proxy | Paket kaynaklarına bağlanırken kullanılacak proxy ayarları; `http_proxy` biçiminde olmalıdır `http://<username>:<password>@<domain>` . Parolalar şifrelenir ve el ile eklenemez. İçin `no_proxy` , değer, proxy sunucusunu atlayan etki alanlarının virgülle ayrılmış listesidir. Ayrıca, bu değerler için http_proxy ve no_proxy ortam değişkenlerini kullanabilirsiniz. Daha fazla bilgi için bkz. [NuGet proxy ayarları](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Paket yüklemesi için paket imzalarını doğrulamak ve geri yüklemek için kullanılan doğrulama modunu belirtir. Değerler `accept` , `require` . Varsayılan olarak olur `accept` .

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
| enabled | NuGet 'in otomatik geri yükleme yapıp yapamadığını gösteren bir Boole değeri. Ayrıca, `EnableNuGetPackageRestore` `True` yapılandırma dosyasında bu anahtarı ayarlamak yerine, ortam değişkenini bir değeriyle ayarlayabilirsiniz. |
| otomatik | Bir derleme sırasında NuGet 'in eksik paketleri denetleyip denetmeyeceğini belirten bir Boole değeri. |

**Örnek**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>çözüm bölümü

`packages`Kaynak denetimine bir çözüm klasörünün eklenip eklenmeyeceğini denetler. Bu bölüm yalnızca `nuget.config` bir çözüm klasöründeki dosyalarda kullanılabilir.

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

`packageSources`,, `packageSourceCredentials` , `apikeys` `activePackageSource` `disabledPackageSources` Ve `trustedSigners` tüm çalışmaları birlikte çalışarak, NuGet 'in yükleme, geri yükleme ve güncelleştirme işlemleri sırasında paket depolarıyla nasıl çalıştığını yapılandırır.

Komutu [ `nuget sources` genellikle](../reference/cli-reference/cli-ref-sources.md) bu ayarları yönetmek için kullanılır, ancak `apikeys` [ `nuget setapikey` komutu](../reference/cli-reference/cli-ref-setapikey.md)kullanılarak yönetilir ve `trustedSigners` [ `nuget trusted-signers` komutu](../reference/cli-reference/cli-ref-trusted-signers.md)kullanılarak yönetilir.

Nuget.org için kaynak URL 'sinin olduğunu unutmayın `https://api.nuget.org/v3/index.json` .

### <a name="packagesources"></a>packagesonak

Bilinen tüm paket kaynaklarını listeler. Geri yükleme işlemleri sırasında ve PackageReference biçimi kullanılarak herhangi bir proje için sıra yok sayılır. NuGet, kullanan projelerle ilgili güncelleştirme ve güncelleştirme işlemlerine yönelik kaynakların sırasını duyar `packages.config` .

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
> `<clear />`Belirli bir düğüm için olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar. [Ayarların nasıl uygulandığı hakkında daha fazla bilgi edinin](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Genellikle ve anahtarlarıyla belirtilen kaynaklar için Kullanıcı adlarını ve parolaları depolar `-username` `-password` `nuget sources` . `-storepasswordincleartext`Seçeneği de kullanılmamışsa parolalar varsayılan olarak şifrelenir.
İsteğe bağlı olarak, anahtarla geçerli kimlik doğrulama türleri de belirtilebilir `-validauthenticationtypes` .

| Anahtar | Değer |
| --- | --- |
| username | Kaynağın düz metin olarak Kullanıcı adı. |
| password | Kaynak için şifrelenmiş parola. Şifrelenmiş parolalar yalnızca Windows 'da desteklenir ve yalnızca aynı makinede kullanıldığında ve özgün şifrelemeyle aynı kullanıcı aracılığıyla şifresi çözülür. |
| cleartextpassword | Kaynak için şifrelenmemiş parola. Note: ortam değişkenleri, geliştirilmiş güvenlik için kullanılabilir. |
| validauthenticationtypes | Bu kaynak için geçerli kimlik doğrulama türlerinin virgülle ayrılmış listesi. `basic`Sunucu ntlm veya anlaşma duyurur ise ve şirket içi Azure DevOps Server BIR Pat kullanırken, kimlik bilgilerinizin temel mekanizma kullanılarak gönderilmesi gerekiyorsa, bunu olarak ayarlayın. Diğer geçerli değerler,,, ve içerir, `negotiate` `kerberos` `ntlm` `digest` ancak bu değerlerin yararlı olması çok düşüktür. |

**Örnek:**

Yapılandırma dosyasında, `<packageSourceCredentials>` öğesi ilgili her kaynak adı için alt düğümleri içerir (ad içindeki boşluklar ile değiştirilmiştir `_x0020_` ). Diğer bir deyişle, "contoso" ve "test kaynağı" adlı kaynaklar için, şifreli parolalar kullanılırken yapılandırma dosyası aşağıdakileri içerir:

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

Bir ortam değişkeninde depolanan şifrelenmemiş parolaları kullanırken:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
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

Ayrıca, geçerli kimlik doğrulama yöntemleri sağlanabilir:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys tuşları

[ `nuget setapikey` Komutuyla](../reference/cli-reference/cli-ref-setapikey.md)ayarlanan API anahtarı kimlik doğrulaması kullanan kaynaklar için anahtarları depolar.

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
| (kaynağın adı) veya `All` | Anahtar bir kaynağın adı ise, değer kaynak yolu veya URL olur. Eğer `All` değeri, `(Aggregate source)` Aksi durumda devre dışı bırakılmayan tüm paket kaynaklarını birleştirmek için olmalıdır. |

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

Yükleme veya geri yükleme sırasında pakete izin vermek için kullanılan güvenilen İmzalayanları depolar. Kullanıcı öğesine ayarlandığında bu liste boş olamaz `signatureValidationMode` `require` . 

Bu bölüm, [ `nuget trusted-signers` komutuyla](../reference/cli-reference/cli-ref-trusted-signers.md)birlikte güncelleştirilemeyebilir.

**Şema**:

Güvenilen bir imzalayan `certificate` , belirli bir İmzalayanın tanımlayan tüm sertifikaları içeren bir öğe koleksiyonuna sahiptir. Güvenilen bir imzalayan ya da olabilir `Author` `Repository` .

Güvenilen bir *Depo* Ayrıca `serviceIndex` Depo için (geçerli bir URI olması gerekir `https` ) belirtir ve isteğe bağlı olarak, `owners` belirli bir depodan güvenilir olan daha fazla sayıda kısıtlamak için noktalı virgülle ayrılmış bir liste belirtebilir.

Bir sertifika parmak izi için kullanılan desteklenen karma algoritmaları `SHA256` , ve ' dir `SHA384` `SHA512` .

Bir ise `certificate` , `allowUntrustedRoot` `true` imza doğrulamasının parçası olarak sertifika zincirini oluştururken, belirtilen sertifikanın güvenilmeyen bir köke zincirine izin verileceğini belirtir.

**Örnek**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
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

Varsayılan paket yönetim biçimini *packages.config* ya da packagereference olarak ayarlar. SDK stilindeki projeler her zaman PackageReference kullanır.

| Anahtar | Değer |
| --- | --- |
| biçim | Varsayılan paket yönetimi biçimini gösteren bir Boole değeri. İse `1` Format, PackageReference olur. İse `0` , biçim *packages.config*. |
| devre dışı | İlk paket yüklemesi sırasında varsayılan bir paket biçimi seçme isteminin gösterilip gösterilmeyeceğini belirten bir Boole değeri. `False` istemi gizler. |

**Örnek**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Ortam değişkenlerini kullanma

`nuget.config`Çalışma zamanında ayarları uygulamak için değerler (NuGet 3.4 +) cinsinden ortam değişkenlerini kullanabilirsiniz.

Örneğin, `HOME` Windows üzerindeki ortam değişkeni olarak ayarlandıysa `c:\users\username` , `%HOME%\NuGetRepository` yapılandırma dosyasındaki değeri olarak çözümlenir `c:\users\username\NuGetRepository` .

Windows stili ortam değişkenlerini (başladığı ve bitişi%) kullanmanız gerektiğini unutmayın Mac/Linux üzerinde bile. `$HOME/NuGetRepository`Yapılandırma dosyasında bulunması çözümlenmeyecektir. Mac/Linux üzerinde değeri `%HOME%/NuGetRepository` olarak çözümlenir `/home/myStuff/NuGetRepository` .

Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından sabit değeri kullanır. Örneğin `%MY_UNDEFINED_VAR%/NuGetRepository` , şu şekilde çözümlenir `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

Aşağıdaki tabloda, NuGet.Config dosyaları için environnment değişken sözdizimi ve yol ayırıcı desteği gösterilmektedir.

### <a name="nugetconfig-environment-variable-support"></a>`NuGet.Config` ortam değişkeni desteği

| Syntax | Dizin ayırıcı | Windows nuget.exe | Windows dotnet.exe | Mac nuget.exe (mono) | Mac dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Yes | Yes | Yes | Yes |
| `%MY_VAR%` | `\`  | Yes | Yes | Hayır | Hayır |
| `$MY_VAR` | `/`  | Hayır | Hayır | Hayır | Hayır |
| `$MY_VAR` | `\`  | Hayır | Hayır | Hayır | Hayır |


## <a name="example-config-file"></a>Örnek yapılandırma dosyası

Aşağıda, `nuget.config` isteğe bağlı olanlar dahil olmak üzere bir dizi ayarı gösteren örnek bir dosya verilmiştir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
