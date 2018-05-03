---
title: nuget.config dosya başvurusu
description: NuGet.Config dosya başvurusu yapılandırma, bindingRedirects, packageRestore, çözüm ve packageSource bölümler dahil olmak üzere.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 871cd05ed010d2a31348151de6b7e225ed2dc915
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nugetconfig-reference"></a>nuget.config başvurusu

NuGet davranışı farklı ayarları tarafından denetlenir `NuGet.Config` dosyaları açıklandığı gibi [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` bir üst düzey içeren bir XML dosyası `<configuration>` düğümü, bu konuda açıklanan bölümünün öğeleri içerir. Her bölüm sıfır veya daha fazla içerir `<add>` öğeleriyle `key` ve `value` öznitelikleri. Bkz: [örnekler yapılandırma dosyası](#example-config-file). Ayar adları büyük küçük harf duyarsız ve değerleri kullanabilir [ortam değişkenleri](#using-environment-variables).

Bu konuda:

- [yapılandırma bölümü](#config-section)
- [bindingRedirects bölümü](#bindingredirects-section)
- [packageRestore bölümü](#packagerestore-section)
- [Çözüm bölümü](#solution-section)
- [Paket kaynak bölümler](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [Ortam değişkenlerini kullanma](#using-environment-variables)
- [Örnek yapılandırma dosyası](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>yapılandırma bölümü

Kullanılarak ayarlanabilir çeşitli yapılandırma ayarlarını içeren [ `nuget config` komutu](../tools/cli-ref-config.md).

`dependencyVersion` ve `repositoryPath` kullanarak projeleri için geçerli `packages.config`. `globalPackagesFolder` PackageReference biçimini kullanarak projeler için geçerlidir.

| Anahtar | Değer |
| --- | --- |
| dependencyVersion (`packages.config` yalnızca) | Varsayılan `DependencyVersion` paketi yükle, geri yükleme ve güncelleştirme için değer olduğunda `-DependencyVersion` anahtar doğrudan belirtilmedi. Bu değer ayrıca NuGet Paket Yöneticisi kullanıcı Arabirimi tarafından kullanılır. Değerler `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (PackageReference yalnızca kullanarak projeleri) | Varsayılan Genel paketler klasörü konumu. Varsayılan değer `%userprofile%\.nuget\packages` (Windows) veya `~/.nuget/packages` (Mac/Linux). Göreli bir yol projeye özgü içinde kullanılabilir `nuget.config` dosyaları. Bu ayar önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı. |
| repositoryPath (`packages.config` yalnızca) | NuGet paketleri yerine varsayılan yükleme konumu `$(Solutiondir)/packages` klasörü. Göreli bir yol projeye özgü içinde kullanılabilir `nuget.config` dosyaları. Bu ayar önceliklidir NUGET_PACKAGES ortam değişkeni tarafından geçersiz kılındı. |
| defaultPushSource | URL veya bir işlem için başka bir paket kaynaklarını bulunursa, varsayılan olarak kullanılması gereken paket kaynağının yolunu tanımlar. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Proxy ayarlarını; paket kaynaklarına bağlanırken kullanmak için `http_proxy` biçiminde olmalıdır `http://<username>:<password>@<domain>`. Parolaları şifrelenir ve el ile eklenemez. İçin `no_proxy`, değer atlama proxy sunucusu etki alanları virgülle ayrılmış bir listesi verilmiştir. Alternatif olarak, bu değerleri http_proxy ve no_proxy ortam değişkenleri kullanabilirsiniz. Daha fazla bilgi için bkz: [NuGet proxy ayarlarını](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |

**Örnek**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a>bindingRedirects bölümü

Bir paketi yüklendiğinde NuGet otomatik bağlama yeniden yönlendirmeleri yapar olup olmadığını yapılandırır.

| Anahtar | Değer |
| --- | --- |
| Atla | Otomatik bağlama yeniden yönlendirmeleri Atla görüntülenmeyeceğini gösteren bir Boole değeri. Varsayılan olarak yanlıştır. |

**Örnek**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore bölümü

Denetimleri paket geri yüklemesi sırasında oluşturur.

| Anahtar | Değer |
| --- | --- |
| Etkin | NuGet otomatik geri yükleme gerçekleştirmek olup olmadığını gösteren bir Boole değeri. Ayrıca ayarlayabilirsiniz `EnableNuGetPackageRestore` ortam değişkeni değerini `True` yapılandırma dosyasında bu anahtarı ayarı yerine. |
| otomatik | NuGet bir yapı sırasında eksik paketleri denetleyip denetlemeyeceğini gösteren bir Boole değeri. |

**Örnek**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Çözüm bölümü

Denetimleri olup olmadığını `packages` klasörü, çözümün kaynak denetiminde yer almaktadır. Bu bölüm yalnızca çalışır `nuget.config` bir çözüm klasördeki dosyaları.

| Anahtar | Değer |
| --- | --- |
| disableSourceControlIntegration | Kaynak denetimi ile çalışırken, paketler klasörü yoksay tutulmayacağını gösteren bir Boole değeri. Varsayılan değer false'tur. |

**Örnek**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Paket kaynak bölümleri

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, Ve `disabledPackageSources` birlikte yükleme, geri yükleme ve güncelleştirme işlemi sırasında NuGet paketi depoları ile nasıl çalıştığını yapılandırmak için tüm iş.

[ `nuget sources` Komutu](../tools/cli-ref-sources.md) genellikle dışında bu ayarları yönetmek için kullanılan `apikeys` hangi kullanılarak yönetilir [ `nuget setapikey` komutu](../tools/cli-ref-setapikey.md).

Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Tüm bilinen paket kaynaklarını listeler. Geri yükleme işlemleri sırasında ve PackageReference biçimini kullanarak herhangi bir projeyle sırası göz ardı edilir. NuGet kaynakları sırasını yükleme için uyar ve güncelleştirme işlemleri kullanarak projeleri ile `packages.config`.

| Anahtar | Değer |
| --- | --- |
| Paket kaynağı atamak (ad) | Yolu veya paket kaynağının URL'si. |

**Örnek**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Kullanıcı adları ve parolalar genellikle ile belirtilen kaynakları için depolar `-username` ve `-password` ile geçer `nuget sources`. Parolalar, varsayılan olarak şifrelenir, sürece `-storepasswordincleartext` seçeneği de kullanılır.

| Anahtar | Değer |
| --- | --- |
| Kullanıcı adı | Düz metin kaynak için kullanıcı adı. |
| Parola | Kaynağı şifrelenmiş parolası. |
| cleartextpassword | Kaynak şifrelenmemiş parola. |

**Örnek:**

Yapılandırma dosyasındaki `<packageSourceCredentials>` öğesi her bir geçerli kaynak adı için alt düğümleri içerir (adında boşluk ile değiştirilir `_x0020_`). Diğer bir deyişle, "Contoso" ve "Test kaynağı" adlı kaynakları için yapılandırma dosyası aşağıdaki şifrelenmiş parolalar kullanırken içerir:

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

### <a name="apikeys"></a>apikeys

Depolar kümesiyle olarak API anahtar kimlik doğrulaması kullanan kaynakları tuşları [ `nuget setapikey` komutu](../tools/cli-ref-setapikey.md).

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

Şu anda devre dışı bırakılmış kaynakları tanımlanır. Boş olabilir.

| Anahtar | Değer |
| --- | --- |
| (kaynak adı) | Kaynak devre dışı olup olmadığını gösteren bir Boole değeri. |

**Örnek:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(yalnızca 2.x; içinde kullanım dışı 3.x+)*

Şu anda etkin kaynağını tanımlayan veya toplama tüm kaynakları gösterir.

| Anahtar | Değer |
| --- | --- |
| (kaynak adı) veya `All` | Anahtar bir kaynak adı ise, kaynak yolu veya URL'si değerdir. Varsa `All`, değer olmalıdır `(Aggregate source)` Aksi durumda devre dışı tüm paket kaynaklarını birleştirmek için. |

**Örnek**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a>Ortam değişkenlerini kullanma

Ortam değişkenleri kullanabilirsiniz `nuget.config` değerleri (ayarları uygulamak için NuGet 3.4 +) çalışma süresi.

Örneğin, varsa `HOME` Windows ortam değişkeni ayarlanır `c:\users\username`, ardından değeri `%HOME%\NuGetRepository` dosya yapılandırmada çözümler `c:\users\username\NuGetRepository`.

Benzer şekilde, varsa `HOME` Mac/Linux'ta kümesine `/home/myStuff`, ardından `$HOME/NuGetRepository` dosya yapılandırmada çözümler `/home/myStuff/NuGetRepository`.

Bir ortam değişkeni bulunmazsa, NuGet yapılandırma dosyasından hazır değeri kullanır.

## <a name="example-config-file"></a>Örnek yapılandırma dosyası

Aşağıda `nuget.config` çeşitli ayarlar gösterilmektedir dosyası:

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
</configuration>
```
