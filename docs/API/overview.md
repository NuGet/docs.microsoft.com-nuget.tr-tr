---
title: "Genel bakış, NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 8c81f1ac-18c7-44d1-b2e3-584fe85dee6f
description: "NuGet paketlerini indirmek, meta veri Getir, yeni paketler, vb. yayımlamak için kullanılan HTTP uç noktalar kümesi API'dir."
keywords: "NuGet V3 API, NuGet V2 API, NuGet JSON, NuGet kayıt API'si, NuGet API düz kapsayıcı, NuGet nupkg API, NuGet meta veriler API, NuGet arama API, NuGet itme API, NuGe yayımlama API'sı, NuGet Sil API, NuGet unlist API, NuGet Protokolü"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 05ed17f12f413d29d97a253d7d55f154d4910834
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-api"></a>NuGet API

NuGet paketlerini indirmek ve meta veri Getir, yeni paketleri yayımlama ve çoğu diğer resmi NuGet istemcileri kullanılabilir işlemleri için kullanılan HTTP uç noktalar kümesi API'dir.

Bu API gibi NuGet işlemleri gerçekleştirmek için Visual Studio, nuget.exe ve .NET CLI NuGet istemcisi tarafından kullanılır [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), Visual Studio kullanıcı Arabirimi aramada ve [ `nuget.exe push` ](../tools/cli-ref-push.md).

Not Bazı durumlarda, nuget.org başka bir paket kaynak tarafından zorlanmaz ek gereksinimlere sahiptir. Bu farklılıklar tarafından belgelenen [nuget.org protokolleri](nuget-protocols.md).

## <a name="service-index"></a>Hizmet dizini

İyi bilinen bir konumda bir JSON belgesi API'si için giriş noktasıdır. Bu belge denir **Hizmeti dizini**.
Nuget.org hizmet dizin konumuna `https://api.nuget.org/v3/index.json`.

Bu JSON belgesi bir listesini içeren *kaynakları* farklı işlevsellik sağlar ve farklı kullanım durumları karşılamak.

API desteği istemciler ilgili paket kaynaklarına bağlanma yolu olarak bir veya daha fazla bu hizmeti dizin URL'si kabul etmelidir.

Hizmet dizini hakkında daha fazla bilgi için bkz: [kendi API Başvurusu](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

NuGet HTTP Protokolü sürüm 3 API'dir. Bu protokol bazen "V3 API." adlandırılır Bu başvuru belgeleri yalnızca "API'SİYLE." protokolünün bu sürüme başvurur

Hizmet dizini şema sürümü belirtilir `version` Hizmeti dizini özelliği. Sürüm dizesi bir ana sürüm numarası olan API olması zorunlu tutulmuştur `3`. Hizmet dizin şemasına yapılan bölünemez değişiklikler gibi sürüm dizesinin alt sürümü artırılır.

Eski istemciler (nuget.exe gibi 2.x) değil V3 API desteği ve yalnızca eski V2 olan burada belgelenmemiştir API'sini destekler.

OData tabanlı bir protokol resmi NuGet istemcisi 2.x sürümü tarafından uygulanan olduğu V2 API ardılı olduğu için NuGet V3 API şekilde adlandırılır. V3 API, ilk resmi NuGet istemci 3.0 sürümü tarafından desteklenen ve son ana Protokolü sürüm 4.0 NuGet istemci tarafından ve hala desteklenmektedir. 

İlk sürüm olduğundan API'sine bölünemez Protokolü değişiklikler yapıldı.

## <a name="resources-and-schema"></a>Kaynakları ve şema

**Hizmeti dizini** çeşitli kaynaklar açıklanır. Desteklenen kaynakların geçerli kümesi aşağıdaki gibidir:

Kaynak adı                                                          | Gerekli | Açıklama
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | Evet      | Anında iletme ve silme (veya unlist) paketleri.
[`SearchQueryService`](search-query-service-resource.md)               | Evet      | Filtre ve paketleri anahtar sözcüğe göre arayın.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | Evet      | Paket meta verileri alın.
[`PackageBaseAddress`](package-base-address-resource.md)               | Evet      | Paket içeriğini (.nupkg) alın.
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Yok       | Paket kimliği ve sürümleri tarafından alt dizeyi bulur.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Yok       | "Rapor kötüye" web sayfasına erişmek için bir URL oluşturur.
[`Catalog`](catalog-resource.md)                                       | Yok       | Tüm paket olayları tam kaydı.

Genel olarak, bir API kaynak tarafından döndürülen tüm ikili olmayan veriler JSON kullanarak serileştirilir. Hizmet dizindeki her bir kaynağın tarafından döndürülen yanıt şeması, bu kaynak için ayrı ayrı tanımlanır. Her kaynak hakkında daha fazla bilgi için yukarıda listelenen konulara bakın.

> [!Note]
> Ne zaman bir kaynak uygulamıyor `SearchAutocompleteService` herhangi otomatik tamamlama davranışı düzgün bir şekilde devre dışı bırakılmalıdır. Zaman `ReportAbuseUriTemplate` , kötüye URL resmi NuGet istemci geri döner nuget.org rapor uygulanmadı (tarafından izlenen [NuGet/giriş #4924](https://github.com/NuGet/Home/issues/4924)). Diğer istemciler, sadece bir rapor kötüye URL kullanıcıya göstermemeyi tercih edebilirler.

## <a name="timestamps"></a>Zaman damgaları

API tarafından döndürülen tüm zaman damgaları UTC ya da aksi takdirde kullanarak belirtilen [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) gösterimi. 

## <a name="http-methods"></a>HTTP yöntemleri

Fiil   | Bir yönetim grubuna bağlanmak veya bağlı bir yönetim grubunun özelliklerini düzenlemek için Yönetim çalışma alanında
------ | -----------
AL    | Genellikle veri alma salt okunur bir işlemi gerçekleştirir.
HEAD   | Karşılık gelen için yanıt üstbilgilerini getirir `GET` isteği.
PUT    | Mevcut değil veya mevcut değilse, güncelleştirmeleri bir kaynak oluşturur. Bazı kaynaklar güncelleştirme desteklemiyor olabilir.
DELETE | Bir kaynak unlists veya siler.

## <a name="http-status-codes"></a>HTTP durum kodları

Kod | Açıklama
---- | -----
200  | Başarılı, ve bir yanıt gövdesi yok.
201  | Başarı ve kaynak oluşturuldu.
202  | Başarılı, istek kabul ancak bazı iş hala zaman uyumsuz olarak tamamlanmamış ve tamamlanmış olabilir.
204  | Başarılı, ancak hiç yanıt gövdesi.
301  | Kalıcı bir yeniden yönlendirme.
302  | Geçici bir yeniden yönlendirme.
400  | URL'deki veya istek gövdesinde parametreler geçerli değil.
401  | Sağlanan kimlik bilgileri geçersiz.
403  | Sağlanan kimlik bilgileri verilen eyleme izin verilmiyor.
404  | İstenen kaynak yok.
409  | Mevcut bir kaynağı isteği çakışıyor.
500  | Hizmet beklenmeyen bir hatayla karşılaştı.
503  | Hizmet geçici olarak kullanılamıyor.

Tüm `GET` API uç noktasına yapılan istek HTTP yeniden yönlendirmesi (301 veya 302) döndürebilir. İstemcileri işleyebilmesini gibi yeniden yönlendirmeleri izlenerek `Location` başlığı ve bir sonraki Yürütülüyor `GET`. Özel uç noktaları ile ilgili belgelere, burada yeniden yönlendirmeleri kullanılabilir çıkışı açıkça çağırmayacaktır.

500 düzeyi durum kodu söz konusu olduğunda, istemci makul yeniden deneme mekanizması uygulayabilirsiniz. Üç kez herhangi bir 500 düzeyi durum kodu veya TCP/DNS hatası karşılaşıldığında resmi NuGet istemci yeniden deneme sayısı.

## <a name="http-request-headers"></a>HTTP isteği üstbilgileri

Ad                     | Açıklama
------------------------ | -----------
X-NuGet-apikey ile yapılan           | Anında iletme ve silme için gerekir, bkz: [ `PackagePublish` kaynak](package-publish-resource.md)
X-NuGet-istemci-sürüm   | **Kullanım dışı** ve tarafından değiştirildi`X-NuGet-Protocol-Version`
X-NuGet-Protocol-sürüm | Bazı durumlarda yalnızca nuget.org üzerinde gerekli, bkz: [nuget.org protokolleri](NuGet-Protocols.md)

## <a name="authentication"></a>Kimlik doğrulaması

Kimlik doğrulaması tanımlamak için paket kaynağı uygulaması kadar bırakılır. Nuget.org, yalnızca için `PackagePublish` kaynak, özel bir API anahtar üstbilgi aracılığıyla kimlik doğrulaması gerektirir. Bkz: [ `PackagePublish` kaynak](package-publish-resource.md) Ayrıntılar için.
