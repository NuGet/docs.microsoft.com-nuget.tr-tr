---
title: NuGet API'si genel bakış
description: NuGet paketlerini indirin, meta verileri getirir, yeni paketleri vb. yayımlamak için kullanılan HTTP uç noktaları bir dizi API'dir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: bb47c72768b0698d8e712c8261321ff38bba2764
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248435"
---
# <a name="nuget-api"></a>NuGet API'si

NuGet paketlerini indirin, meta verileri getirir, yeni paket yayımlamasına ve birçok diğer resmi NuGet istemcisinde bulunan işlemleri için kullanılan HTTP uç noktaları bir dizi API'dir.

Bu API gibi NuGet işlemleri gerçekleştirmek için Visual Studio, nuget.exe ve .NET CLI NuGet istemci tarafından kullanılır [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), Visual Studio kullanıcı arabiriminde, arama ve [ `nuget.exe push` ](../tools/cli-ref-push.md).

Not Bazı durumlarda, nuget.org başka bir paket kaynak tarafından zorlanmaz ek gereksinimleri vardır. Bu farklar tarafından belgelenen [nuget.org protokolleri](nuget-protocols.md).

Basit bir numaralandırma ve indirme kullanılabilir nuget.exe sürümleri için bkz [tools.json](tools-json.md) uç noktası.

## <a name="service-index"></a>Hizmet dizini

İyi bilinen bir konumda bir JSON belgesi API'si için giriş noktasıdır. Bu belge adlı **hizmet dizini**. Hizmet dizini nuget.org için'ın konumudur `https://api.nuget.org/v3/index.json`.

Bu JSON belgesini listesini içeren *kaynakları* farklı işlevsellik ve farklı kullanım durumlarına karşılamak.

API'ı destekleyen istemcilerinin ilgili paket kaynaklarına bağlanma yolu olarak bir veya daha fazla bu hizmet dizini URL'si kabul etmelidir.

Hizmet dizini hakkında daha fazla bilgi için bkz: [, API Başvurusu](service-index.md).

## <a name="versioning"></a>Sürüm oluşturma

NuGet HTTP protokolü sürümü 3 API'dir. Bu protokol bazen "V3 API." adlandırılır Bu başvuru belgeleri protokol bu sürümü yalnızca "API'SİYLE." başvuracaktır.

Hizmet dizini şema sürümü tarafından belirtilen `version` hizmet dizini özelliği. API sürüm dizesi bir ana sürüm numarasını sahip olduğunu taahhütlerin `3`. Hizmet dizin şeması için hataya neden olmayan değişiklikler yapıldıkça, sürüm dizesinin alt sürümü artırılır.

Eski istemciler (nuget.exe gibi 2.x) değil V3 API desteği ve yalnızca eski V2 burada belgelenmemiş API'ı destekler.

OData tabanlı bir protokol sürümü olan 2.x sürümüne resmi bir NuGet istemcisi tarafından uygulanan olduğu V2 API'si ardılı olduğu için NuGet V3 API şekilde adlandırılır. V3 API 3.0 sürümü resmi bir NuGet istemcisi tarafından desteklenen ilk ve son ana Protokolü sürüm 4.0 NuGet istemci tarafından ve hala desteklenmektedir. 

İlk sürüm olduğundan, API'ye bölünemez Protokolü değişiklikler yapılmıştır.

## <a name="resources-and-schema"></a>Kaynaklar ve şema

**Hizmet dizini** çeşitli kaynaklara açıklar. Desteklenen kaynak geçerli kümesini aşağıdaki gibidir:

Kaynak adı                                                           | Gerekli | Açıklama
----------------------------------------------------------------------  | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | evet      | Anında iletme ve silme (veya listeden) paketleri.
[`SearchQueryService`](search-query-service-resource.md)               | evet      | Filtre ve paketleri anahtar sözcüğe göre arayın.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | evet      | Paket meta verilerini alın.
[`PackageBaseAddress`](package-base-address-resource.md)               | evet      | Paket içeriğini (.nupkg) alın.
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Yok       | Paket kimlikleri ve sürümleri tarafından alt dizeyi bulur.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Yok       | "Uygunsuz" web sayfasına erişmek için bir URL oluşturur.
[`RepositorySignatures`](repository-signatures-resource.md)             | Yok      | Depo imzalamak için kullanılan sertifika alın.
[`Catalog`](catalog-resource.md)                                         | Yok      | Tüm paket olayların tam kayıt.
[`SymbolPackagePublish`](symbol-package-publish-resource.md)            | Yok      | Sembol paketleri gönderin.

Genel olarak, bir API kaynak tarafından döndürülen tüm ikili olmayan veriler JSON kullanarak serileştirilir. Hizmet dizini her bir kaynak tarafından döndürülen yanıt şeması, bu kaynak için ayrı ayrı tanımlanır. Her kaynak hakkında daha fazla bilgi için yukarıda listelenen konulara bakın.

Gelecekte Protokolü geliştikçe yeni özellikleri JSON yanıtlarını eklenebilir. İstemcinin geleceğe hazır olması için uygulama yanıt şeması kalıcıdır ve ek veri içeremez varsaymanız gerekir değil. Uygulama anlamadığı tüm özellikleri yok sayılır.

> [!Note]
> Ne zaman bir kaynak uygulamıyor `SearchAutocompleteService` herhangi bir otomatik tamamlama davranış düzgün bir şekilde devre dışı bırakılmalıdır. Zaman `ReportAbuseUriTemplate` , uygunsuz kullanım bildirme URL'si resmi NuGet istemci geri döner nuget.org bildirin uygulanmamış (tarafından izlenen [NuGet/giriş #4924](https://github.com/NuGet/Home/issues/4924)). Diğer istemciler yalnızca bir rapor Uygunsuz kullanım bildirme URL'si kullanıcıyı gösterme kullanmamayı seçebilirsiniz.

## <a name="timestamps"></a>Zaman damgaları

API tarafından döndürülen tüm zaman damgaları UTC ya da aksi takdirde kullanarak belirtilen [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) gösterimi. 

## <a name="http-methods"></a>HTTP yöntemleri

Fiili   | Bir yönetim grubuna bağlanmak veya bağlı bir yönetim grubunun özelliklerini düzenlemek için Yönetim çalışma alanında
------ | -----------
GET    | Genellikle veri alma salt okunur bir işlemi gerçekleştirir.
HEAD   | Yanıt üstbilgileri için karşılık gelen getirir `GET` isteği.
PUT    | Mevcut değil veya mevcut değilse, güncelleştirmeleri bir kaynak oluşturur. Bazı kaynaklar güncelleştirme desteklemiyor olabilir.
DELETE | Bir kaynak unlists veya siler.

## <a name="http-status-codes"></a>HTTP durum kodları

Kod | Açıklama
---- | -----
200  | Başarı ve yanıt gövdesi yok.
201  | Başarı ve kaynak oluşturuldu.
202  | Başarılı, isteği kabul etti ancak bazı iş hala zaman uyumsuz olarak tamamlanmamış ve tamamlanmış olabilir.
204  | Başarılı, ancak hiç yanıt gövdesi.
301  | Kalıcı bir yeniden yönlendirme.
302  | Geçici bir yeniden yönlendirme.
400  | URL veya istek gövdesinde parametreleri geçerli değil.
401  | Sağlanan kimlik bilgileri geçersiz.
403  | Sağlanan kimlik bilgilerini belirtilen eyleme izin verilmiyor.
404  | İstenen kaynak yok.
409  | Mevcut bir kaynağı isteği çakışıyor.
500  | Hizmet beklenmeyen bir hatayla karşılaştı.
503  | Hizmet geçici olarak kullanılamıyor.

Tüm `GET` bir API uç noktası için yapılan istek HTTP yeniden yönlendirmesi (301 veya 302) döndürebilir. İstemciler düzgün olarak işleyebileceğiniz gibi yeniden yönlendirmeleri gözlemleyerek `Location` başlığı ve bir sonraki kesme `GET`. Özel uç noktaları ile ilgili belgeler, burada yeniden yönlendirmeleri kullanılabilir kullanıma açıkça çağırmayacaktır.

Bir düzey 500 durum kodu söz konusu olduğunda istemci, makul bir yeniden deneme mekanizması uygulayabilirsiniz. Üç kez herhangi bir düzey 500 durum kodu veya TCP/DNS hatası ile karşılaşıldığında resmi NuGet istemci yeniden deneme sayısı.

## <a name="http-request-headers"></a>HTTP isteği üstbilgileri

Ad                     | Açıklama
------------------------ | -----------
X-NuGet-ApiKey           | Push ve delete için gerekli bkz [ `PackagePublish` kaynak](package-publish-resource.md)
X-NuGet-Client-Version   | **Kullanım dışı** tarafından değiştirildi `X-NuGet-Protocol-Version`
X-NuGet-protokol-sürüm | Nuget.org üzerindeki yalnızca belirli durumlarda gerekli bkz [nuget.org protokolleri](NuGet-Protocols.md)
X-NuGet-Session-Id       | *İsteğe bağlı*. NuGet istemcileri v4.7 + aynı NuGet istemci oturumunun parçası olan HTTP isteklerini belirleyin. İçin `PackageReference` geri yükleme işlemleri, tek bir oturum kimliği, otomatik tamamlama, gibi diğer senaryolar için olan ve `packages.config` geri yükleme kodunu nasıl katılır nedeniyle birkaç farklı bir oturum kimliği olabilir.

## <a name="authentication"></a>Kimlik doğrulaması

Kimlik doğrulaması tanımlamak için paket kaynağı uygulaması kadar bırakılır. Nuget.org, yalnızca için `PackagePublish` kaynak, özel bir API anahtarı üstbilgi aracılığıyla kimlik doğrulaması gerektirir. Bkz: [ `PackagePublish` kaynak](package-publish-resource.md) Ayrıntılar için.
