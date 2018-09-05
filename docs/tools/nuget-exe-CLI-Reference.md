---
title: NuGet komut satırı arabirimi (CLI) başvurusu
description: Nuget.exe CLI için komut satırı başvurusu dizini
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 2743dde63487124c706f2b1521ef2c6c3b28339d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548084"
---
# <a name="nuget-cli-reference"></a>NuGet CLI başvurusu

NuGet komut satırı arabirimi (CLI), `nuget.exe`, tam kapsamı yüklemek, oluşturmak, yayımlamak ve proje dosyaları için hiçbir değişiklik yapmadan paketlerini yönetmek için NuGet işlevsellik sağlar.

Herhangi bir komutu kullanmak için bir komut penceresi açın veya bash Kabuğu sonra Çalıştır `nuget` uygun seçenekleri ve komut örneğindeki gibi `nuget help pack` (Paketi komutu Yardım görüntülemek için).

Bu belgeler, NuGet CLI'ın en son sürümü yansıtır. Kullanmakta olduğunuz herhangi belirli bir sürümünü hakkında tam Ayrıntılar için çalıştırma `nuget help` istenen komutu.

## <a name="installing-nugetexe"></a>Nuget.exe yükleme

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> NuGet CLI Visual Studio'da Paket Yöneticisi konsolu içinde kullanılabilir hale getirmek için bkz: [konsolunda nuget.exe CLI kullanarak](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Kullanılabilirlik

Bkz: [Özellik kullanılabilirliği](../install-nuget-client-tools.md#feature-availability) hakkında tam Ayrıntılar için.

- Tüm komutlar, Windows üzerinde kullanılabilir.
- Nuget.exe için belirtilenler dışında Mono üzerinde çalıştırılan tüm komutları çalışmak `pack`, `restore`, ve `update`.
- `pack`, `restore`, `delete`, `locals`, Ve `push` komutlardır ayrıca dotnet CLI Mac ve Linux'ta kullanılabilir.

## <a name="commands-and-applicability"></a>Komutlar ve uygulanabilirliği

Kullanılabilir komutları ve paket oluşturma, paket tüketim ve/veya bir konağa bir paket yayımlama için Uygulanabilirlik:

| Sık kullanılan komutlar | Geçerli rolleri | NuGet sürüm | Açıklama |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Oluşturma | 2.7+ | Bir NuGet paketi oluşturur bir `.nuspec` ya da proje dosyası. Mono üzerinde çalışırken, bir proje dosyasından paket oluşturma desteklenmiyor. |
| [push](cli-ref-push.md) | Yayımlama | Tümü | Bir paket için bir paket kaynağı yayımlar. |
| [config](cli-ref-config.md) | Tümü | Tümü | Alır veya NuGet yapılandırma değerlerini ayarlar. |
| [help or ?](cli-ref-help.md) | Tümü | Tümü | Yardım bilgileri veya bir komut için yardımı görüntüler. |
| [locals](cli-ref-locals.md) | Tüketim | 3.3+ | Listeler konumlarını *genel paketleri*, *http önbellek*, ve *temp* klasörleri ve bu klasörlerin içeriğini temizler. |
| [restore](cli-ref-restore.md) | Tüketim | 2.7+ | Paket Yönetimi biçime tarafından başvurulan tüm paketleri geri yükler. Mono üzerinde çalışırken PackageReference biçimini kullanarak paketleri geri yüklenmesi desteklenmez. |
| [setapikey](cli-ref-setapikey.md) | Yayımlama, tüketim | Tümü | Belirtilen paket kaynağı için bir API anahtarı, paket kaynağına erişim için bir anahtar gerektirdiğinde kaydeder. |
| [spec](cli-ref-spec.md) | Oluşturma | Tümü | Oluşturur bir `.nuspec` dosya, dosya bir Visual Studio projesinden oluşturuluyor belirteçleri kullanarak. |

| İkincil komutları | Geçerli rolleri | NuGet sürüm | Açıklama |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Yayımlama | 3.3+ | Hiyerarşik yerleşim kullanarak bir HTTP olmayan paket kaynağı için bir paket ekler. HTTP kaynakları için kullanmak *anında iletme*. |
| [delete](cli-ref-delete.md) | Yayımlama | Tümü | Bir paketi paket kaynağından unlists ya da kaldırır. |
| [init](cli-ref-init.md) | Oluşturma | 3.3+ | Paketleri hiyerarşik yerleşim kullanarak bir paket kaynağı bir klasör ekler. |
| [install](cli-ref-install.md) | Tüketim | Tümü | Yükleme paketinin geçerli bir proje ancak projeleri değiştirmeyin veya dosyalarına başvuruda. |
| [list](cli-ref-list.md) | Tüketim, belki de yayımlama | Tümü | Belirli bir kaynaktan alınan paketleri görüntüler. |
| [mirror](cli-ref-mirror.md) | Yayımlama | 3.2 +'da kullanım dışı | Bir paketi ve bağımlılıkları bir kaynaktan bir hedef havuz yansıtır. |
| [sources](cli-ref-sources.md) | Tüketim, yayımlama | Tümü | Yapılandırma dosyalarında paket kaynaklarını yönetir. |
| [update](cli-ref-update.md) | Tüketim | Tümü | Bir projenin paketler için kullanılabilen en sürümlere güncelleştirir. Mono üzerinde çalışırken desteklenmez. |

Farklı komutlar çeşitli kullanın [ortam değişkenlerini](cli-ref-environment-variables.md).

NuGet CLI komutları geçerli rolleri tarafından:

| Rol | Komutlar |
| --- | --- |
| Tüketim | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Oluşturma | `config`, `help`, `init`, `pack`, `spec` |
| Yayımlama | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Örneğin, geliştiricilerin paketler yalnızca kullanma ile ilgili yalnızca bu alt küme NuGet komut anlamanız.

> [!Note]
> Komut seçeneği adları büyük/küçük harfe duyarsızdır. Kullanım dışı bırakılmıştır seçenekleri bu başvuruda gibi bulunmaz `NoPrompt` (yerine `NonInteractive`) ve `Verbose` (yerine `Verbosity`).
