---
title: NuGet komut satırı arabirimi (CLI) başvurusu
description: CLI nuget.exe için komut satırı başvurusu dizini
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: ed91a31505ab1de9447cdbeb87c8ad08f7ba56d8
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-cli-reference"></a>NuGet CLI başvurusu

NuGet komut satırı arabirimi (CLI), `nuget.exe`, tam kapsamı yüklemek, oluşturmak, yayımlama ve proje dosyalarına herhangi bir değişiklik yapmadan paketlerini yönetmek için NuGet işlevselliği sağlar.

Herhangi bir komutu kullanmak için bir komut penceresi açın veya kabuk bash ardından Çalıştır `nuget` gibi ardından komut ve uygun seçenekleri `nuget help pack` (paketi komutunda yardımını görüntülemek için).

Bu belge NuGet CLI en son sürümünü yansıtır. Kullanmakta olduğunuz herhangi belirli bir sürümü için tam Ayrıntılar için Çalıştır `nuget help` istenen komutu.

## <a name="installing-nugetexe"></a>Nuget.exe yükleme

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> NuGet CLI Visual Studio'da Paket Yöneticisi konsolu içinde kullanılabilir yapmak için bkz: [konsolunda nuget.exe CLI kullanarak](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Kullanılabilirlik

Bkz: [Özellik kullanılabilirliği](../install-nuget-client-tools.md#feature-availability) tam Ayrıntılar için.

- Tüm komutlar Windows üzerinde kullanılabilir.
- Tüm komutlar için belirtilenler dışında Mono üzerinde çalışan nuget.exe çalışmak `pack`, `restore`, ve `update`.
- `pack`, `restore`, `delete`, `locals`, Ve `push` komutlardır ayrıca dotnet CLI Mac ve Linux üzerinde kullanılabilir.

## <a name="commands-and-applicability"></a>Komutlar ve Uygulanabilirlik

Kullanılabilir komutlar ve paket oluşturma, paket tüketim ve/veya bir ana bilgisayara bir paket yayımlama için Uygulanabilirlik:

| Sık kullanılan komutlar | Geçerli rolleri | NuGet sürümü | Açıklama |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Oluşturma | 2.7+ | NuGet paket oluşturur bir `.nuspec` veya proje dosyası. Mono üzerinde çalışırken, bir proje dosyasından paket oluşturma desteklenmiyor. |
| [push](cli-ref-push.md) | Yayımlama | Tümü | Bir paket için paket kaynağı yayımlar. |
| [config](cli-ref-config.md) | Tümü | Tümü | Alır veya NuGet yapılandırma değerlerini ayarlar. |
| [help or ?](cli-ref-help.md) | Tümü | Tümü | Bilgi veya bir komutla ilgili Yardım yardımını görüntüler. |
| [locals](cli-ref-locals.md) | Tüketim | 3.3+ | Listeler konumlarını *paketleri genel*, *http önbellek*, ve *temp* klasörleri ve bu klasörleri içeriğini temizler. |
| [restore](cli-ref-restore.md) | Tüketim | 2.7+ | Paket Yönetimi biçime tarafından başvurulan tüm paketler geri yükler. Mono üzerinde çalışırken, PackageReference biçimi kullanarak paketleri geri yüklenmesi desteklenmez. |
| [setapikey](cli-ref-setapikey.md) | Yayımlama, tüketim | Tümü | Bu paket kaynağına erişimi için bir anahtar gerektirdiğinde verilen paket kaynağı için bir API anahtarı kaydeder. |
| [spec](cli-ref-spec.md) | Oluşturma | Tümü | Oluşturan bir `.nuspec` dosya, bir Visual Studio Proje dosyası oluşturma belirteçleri kullanarak. |

| İkincil komutları | Geçerli rolleri | NuGet sürümü | Açıklama |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Yayımlama | 3.3+ | Bir paket hiyerarşik düzenini kullanarak bir HTTP olmayan paket kaynağı ekler. HTTP kaynakları için kullanmak *itme*. |
| [delete](cli-ref-delete.md) | Yayımlama | Tümü | Bir paketi paket kaynağında unlists ya da kaldırır. |
| [init](cli-ref-init.md) | Oluşturma | 3.3+ | Paketleri bir klasörden hiyerarşik düzenini kullanarak bir paket kaynağı ekler. |
| [install](cli-ref-install.md) | Tüketim | Tümü | Geçerli bir pakete bir yükler proje ancak projeleri değiştirmeyin veya dosyaları başvuru. |
| [list](cli-ref-list.md) | Tüketim, belki de yayımlama | Tümü | Belirli bir kaynaktan paketleri görüntüler. |
| [mirror](cli-ref-mirror.md) | Yayımlama | 3.2 +'da kullanım dışıdır | Bir paketi ve bağımlılıklarını bir kaynaktan bir hedef havuz yansıtır. |
| [sources](cli-ref-sources.md) | Tüketim, yayımlama | Tümü | Yapılandırma dosyalarında paket kaynaklarını yönetir. |
| [update](cli-ref-update.md) | Tüketim | Tümü | Bir projenin paketler için en son sürümleri güncelleştirir. Mono üzerinde çalışırken desteklenmez. |

Farklı komutlar çeşitli kullanmak [ortam değişkenleri](cli-ref-environment-variables.md).

NuGet CLI komutları geçerli rolleri tarafından:

| Rol | Komutlar |
| --- | --- |
| Tüketim | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Oluşturma | `config`, `help`, `init`, `pack`, `spec` |
| Yayımlama | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Örneğin, geliştiriciler paketleri, yalnızca kullanma ile ilgili yalnızca NuGet komutların bu alt anlamanız.

> [!Note]
> Komut seçenek adları büyük/küçük harfe duyarsızdır. Kullanım dışı bırakılmıştır seçenekleri bu başvurusunda gibi eklenmemiştir `NoPrompt` (değiştirilmiştir `NonInteractive`) ve `Verbose` (değiştirilmiştir `Verbosity`).
