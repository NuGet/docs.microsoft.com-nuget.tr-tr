---
title: NuGet komut satırı arabirimi (CLı) başvurusu
description: nuget.exe CLı için komut satırı başvuru dizini
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: e9343f1fdddcf839322849925372587e685aef4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623155"
---
# <a name="nuget-cli-reference"></a>NuGet CLı başvurusu

NuGet komut satırı arabirimi (CLı), `nuget.exe` proje dosyalarında hiçbir değişiklik yapılmadan paketleri yüklemek, oluşturmak, yayımlamak ve yönetmek Için NuGet işlevlerinin tam kapsamını sağlar.

Herhangi bir komutu kullanmak için, bir komut penceresi veya bash kabuğu açın ve ardından `nuget` komutu ve `nuget help pack` (Pack komutunda yardım 'ı görüntülemek için) gibi uygun seçenekleri çalıştırın.

Bu belge NuGet CLı 'nın en son sürümünü yansıtır. Kullandığınız herhangi bir sürüm için tam Ayrıntılar için, `nuget help` istediğiniz komut için komutunu çalıştırın.

CLI ile temel komutları kullanmayı öğrenmek için `nuget.exe` bkz. [nuget.exe CLI kullanarak paketleri yüklemek ve kullanmak](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>nuget.exe yükleniyor

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> NuGet CLı 'yı Visual Studio 'da Paket Yöneticisi konsolu içinde kullanılabilir hale getirmek için, bkz. [nuget.exe CLI 'yi konsolda kullanma](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Kullanılabilirlik

Tam Ayrıntılar için [özellik kullanılabilirliğine](../install-nuget-client-tools.md#feature-availability) bakın.

- Tüm komutlar Windows 'da kullanılabilir.
- Tüm komutlar,, ve için belirtilen dışında mono üzerinde çalışan nuget.exe `pack` çalışır `restore` `update` .
- `pack`,, `restore` , `delete` `locals` Ve komutları, `push` DotNet CLI aracılığıyla Mac ve Linux üzerinde de kullanılabilir.

## <a name="commands-and-applicability"></a>Komutlar ve Uygulanabilirlik

Paket oluşturmaya, paket tüketimine ve/veya bir konağa paket yayımlamaya yönelik kullanılabilir komutlar ve uygulanabilirliği:

| Ortak komutlar | Uygulanabilir roller | NuGet sürümü | Açıklama |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Oluşturma | 2.7 + | Bir veya proje dosyasından bir NuGet paketi oluşturur `.nuspec` . Mono üzerinde çalışırken proje dosyasından bir paket oluşturmak desteklenmez. |
| [push](cli-reference/cli-ref-push.md) | Yayımlama | Tümü | Paket kaynağına bir paket yayımlar. |
| [config](cli-reference/cli-ref-config.md) | Tümü | Tümü | NuGet yapılandırma değerlerini alır veya ayarlar. |
| [help or ?](cli-reference/cli-ref-help.md) | Tümü | Tümü | Bir komut için yardım bilgilerini veya yardımı görüntüler. |
| [locals](cli-reference/cli-ref-locals.md) | Tüketim | 3.3 + | *Genel paketler*, *http önbelleği*ve *geçici* klasörlerin konumlarını listeler ve bu klasörlerin içeriğini temizler. |
| [restore](cli-reference/cli-ref-restore.md) | Tüketim | 2.7 + | Kullanımdaki paket yönetimi biçimi tarafından başvurulan tüm paketleri geri yükler. Mono üzerinde çalışırken, PackageReference biçimi kullanılarak paketlerin geri yüklenmesi desteklenmez. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Yayımlama, tüketim | Tümü | Bu paket kaynağı erişim için bir anahtar gerektirdiğinde belirli bir paket kaynağı için bir API anahtarı kaydeder. |
| [spec](cli-reference/cli-ref-spec.md) | Oluşturma | Tümü | Bir `.nuspec` Visual Studio projesinden dosya üretiyorsa belirteçleri kullanarak bir dosya oluşturur. |

| İkincil komutlar | Uygulanabilir roller | NuGet sürümü | Açıklama |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Yayımlama | 3.3 + | Hiyerarşik düzen kullanarak HTTP olmayan bir paket kaynağına bir paket ekler. HTTP kaynakları için *Push*kullanın. |
| [delete](cli-reference/cli-ref-delete.md) | Yayımlama | Tümü | Paket kaynağından bir paketi kaldırır veya listesini kaldırır. |
| [init](cli-reference/cli-ref-init.md) | Oluşturma | 3.3 + | Hiyerarşik düzen kullanarak bir klasörden paket kaynağına paket ekler. |
| [install](cli-reference/cli-ref-install.md) | Tüketim | Tümü | Geçerli projeye bir paket kurar ancak projeleri veya başvuru dosyalarını değiştirmez. |
| [list](cli-reference/cli-ref-list.md) | Tüketim, belki de yayımlanıyor | Tümü | Belirli bir kaynaktaki paketleri görüntüler. |
| [mirror](cli-reference/cli-ref-mirror.md) | Yayımlama | 3.2 + ' da kullanım dışı | Bir paketi ve onun bağımlılıklarını bir kaynaktan hedef depoya yansıtır. |
| [aramanız](cli-reference/cli-ref-search.md) | Tüketim | 5.8 + | Sağlanan sorgu dizesini kullanarak belirli bir kaynağı arar. |
| [sources](cli-reference/cli-ref-sources.md) | Tüketim, yayımlama | Tümü | Yapılandırma dosyalarındaki paket kaynaklarını yönetir. |
| [update](cli-reference/cli-ref-update.md) | Tüketim | Tümü | Bir projenin paketlerini kullanılabilir en son sürümlere güncelleştirir. Mono üzerinde çalışırken desteklenmez. |

Farklı komutlar çeşitli [ortam değişkenlerini](cli-reference/cli-ref-environment-variables.md)kullanır.

Uygun rollere göre NuGet CLı komutları:

| Rol | Komutlar |
| --- | --- |
| Tüketim | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| Oluşturma | `config`, `help`, `init`, `pack`, `spec` |
| Yayımlama | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Yalnızca tüketen paketlerle ilgilenen geliştiriciler, örneğin yalnızca NuGet komutlarının alt kümesini anlamalıdır.

> [!Note]
> Komut seçeneği adları büyük/küçük harfe duyarlıdır. Kullanım dışı olan seçenekler bu başvuruya dahil değildir (örneğin, `NoPrompt` (ile değiştirilmiştir `NonInteractive` ) ve `Verbose` (değiştiren `Verbosity` ).
