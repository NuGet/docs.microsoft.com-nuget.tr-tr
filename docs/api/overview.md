---
title: NuGet sunucu API 'sine genel bakış
description: NuGet sunucu API 'SI, paketleri indirmek, meta verileri getirmek, yeni paketleri yayımlamak vb. için kullanılabilen bir HTTP uç noktası kümesidir.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237815"
---
# <a name="nuget-server-api"></a>NuGet Server API

NuGet sunucu API 'SI, paketleri indirmek, meta verileri getirmek, yeni paketleri yayımlamak ve resmi NuGet istemcilerinde bulunan diğer birçok işlemi gerçekleştirmek için kullanılabilen bir HTTP uç noktası kümesidir.

Bu API, Visual Studio 'da NuGet istemcisi, nuget.exe ve .NET CLı tarafından, gibi NuGet işlemlerini gerçekleştirmek için kullanılır [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) , Visual Studio Kullanıcı arabiriminde arama yapın ve [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md) .

Not Bazı durumlarda nuget.org, diğer paket kaynakları tarafından zorlanan ek gereksinimlere sahiptir. Bu farklılıklar [NuGet.org protokolleri](nuget-protocols.md)tarafından belgelenmiştir.

Basit bir numaralandırma ve kullanılabilir nuget.exe sürümlerinin indirilmesi için uç noktada [tools.js](tools-json.md) bakın.

## <a name="service-index"></a>Hizmet dizini

API için giriş noktası, iyi bilinen bir konumdaki JSON belgesidir. Bu belgeye **hizmet dizini** adı verilir. Nuget.org için hizmet dizininin konumu `https://api.nuget.org/v3/index.json` .

Bu JSON belgesi, farklı işlevler sağlayan ve farklı kullanım durumlarını karşılayan *kaynakların* listesini içerir.

API 'YI destekleyen istemciler, ilgili paket kaynaklarına bağlanma yoluyla bu hizmet dizin URL 'sinden bir veya daha fazlasını kabul etmelidir.

Hizmet dizini hakkında daha fazla bilgi için bkz. [API başvurusu](service-index.md).

## <a name="versioning"></a>Sürüm Oluşturma

API, NuGet 'in HTTP protokolünün sürüm 3 ' ü. Bu protokol bazen "v3 API" olarak adlandırılır. Bu başvuru belgeleri, protokolün "API" gibi bu sürümüne başvuracaktır.

Hizmet dizini şema sürümü, `version` hizmet dizinindeki özelliği tarafından belirtilir. Sürüm dizesinin ana sürüm numarası olan API mantarihlerinin `3` . Hizmet dizini şemasında, önemli olmayan değişiklikler yapıldığından, sürüm dizesinin ikincil sürümü artar.

Eski istemciler (örneğin, nuget.exe 2. x) v3 API 'YI desteklemez ve burada belgelenmeyen eski v2 API 'sini desteklemez.

NuGet v3 API 'SI, resmi NuGet istemcisinin 2. x sürümü tarafından uygulanan OData tabanlı protokol olan v2 API 'sinin ardıl sürümü olduğu için adlandırılır. V3 API 'SI ilk olarak resmi NuGet istemcisinin 3,0 sürümü tarafından desteklenmektedir ve NuGet istemcisi, 4,0 ve üzerinde en son ana protokol sürümüdür. 

İlk çıkarılmasından bu yana, API 'de bölünmez olmayan protokol değişiklikleri yapılmıştır.

## <a name="resources-and-schema"></a>Kaynaklar ve şema

**Hizmet dizini** çeşitli kaynakları açıklar. Geçerli desteklenen kaynaklar kümesi aşağıdaki gibidir:

Kaynak adı                                                        | Gerekli | Açıklama
-------------------------------------------------------------------- | -------- | -----------
[Katalog](catalog-resource.md)                                       | hayır       | Tüm paket olaylarının tam kaydı.
[PackageBaseAddress](package-base-address-resource.md)               | yes      | Paket içeriğini al (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | hayır       | Paket ayrıntıları Web sayfasına erişmek için bir URL oluşturun.
[PackagePublish](package-publish-resource.md)                        | yes      | Paketleri gönder ve Sil (veya listeden kaldır).
[RegistrationsBaseUrl](registration-base-url-resource.md)            | yes      | Paket meta verilerini alın.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | hayır       | Rapor kötüye kullanımı Web sayfasına erişmek için bir URL oluşturun.
[Imza](repository-signatures-resource.md)            | hayır       | Depo imzalama için kullanılan sertifikaları alın.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | hayır       | Alt dizeden paket kimliklerini ve sürümlerini bulur.
[SearchQueryService](search-query-service-resource.md)               | yes      | Paketleri anahtar sözcüğe göre filtreleyin ve arayın.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | hayır       | Sembol paketlerini gönder.

Genel olarak, bir API kaynağı tarafından döndürülen tüm ikili olmayan veriler JSON kullanılarak serileştirilir. Hizmet dizinindeki her kaynak tarafından döndürülen yanıt şeması, bu kaynak için ayrı ayrı tanımlanır. Her kaynak hakkında daha fazla bilgi için yukarıda listelenen konulara bakın.

Gelecekte protokol geliştikçe, JSON yanıtlarına yeni özellikler eklenebilir. İstemcinin gelecekte kanıt sağlaması için, uygulamanın yanıt şemasının nihai olduğunu varsaymamalıdır ve ek verileri içerememelidir. Uygulamanın anladığı tüm özellikler yok sayılacak.

> [!Note]
> Bir kaynak `SearchAutocompleteService` hiçbir otomatik tamamlama davranışı uygulamadığınızda, düzgün şekilde devre dışı bırakılmalıdır. `ReportAbuseUriTemplate`Uygulanmamıştır, resmi NuGet istemcisi NuGet. org 'ın uygunsuz kullanım URL 'sine geri döner ( [NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)tarafından izlenir). Diğer istemciler, kullanıcıya bir rapor kötüye kullanımı URL 'SI göstermeyebilir.

### <a name="undocumented-resources-on-nugetorg"></a>Nuget.org üzerinde belgelenmemiş kaynaklar

Nuget.org üzerindeki v3 hizmeti dizininde, yukarıda belgelenmeyen bazı kaynaklar bulunur. Bir kaynağı belgeleme konusunda birkaç neden vardır.

İlk olarak, nuget.org uygulamasının uygulama ayrıntısı olarak kullanılan kaynakları belgeliyoruz. `SearchGalleryQueryService` Bu kategoriye girer. [Nugetgallery](https://github.com/NuGet/NuGetGallery) bu kaynağı, veritabanı kullanmak yerine, bazı v2 (OData) sorgularını arama dizinimize devretmek için kullanır. Bu kaynak ölçeklenebilirlik nedenleriyle sunulmuştur ve dış kullanım için tasarlanmamıştır.

İkinci olarak, resmi istemcinin RTM sürümünde hiçbir şekilde gönderilmeyen kaynakları belgeliyoruz.
`PackageDisplayMetadataUriTemplate` ve `PackageVersionDisplayMetadataUriTemplate` Bu kategoriye girer.

Üçüncü olarak, v2 protokolüyle sıkı bir şekilde bağlanmış olan ve kendisi bilinçli olarak belgelenmemiş olan kaynakları belgeliyoruz. `LegacyGallery`Kaynak bu kategoriye girer. Bu kaynak, bir v3 hizmet dizininin karşılık gelen v2 kaynak URL 'sini işaret etmesine olanak tanır. Bu kaynak tarafından desteklenir `nuget.exe list` .

Bir kaynak burada açıklanmadığımızda, bunlara bir bağımlılık *yapmamanız önemle* önerilir. Bu belgelenmemiş kaynakların davranışını kaldırabilir veya değiştirebiliriz. Bu, uygulamanızı beklenmedik yollarla bozabilecek.

## <a name="timestamps"></a>Zaman damgaları

API tarafından döndürülen tüm zaman damgaları UTC, aksi durumda [ıso 8601](https://www.iso.org/iso-8601-date-and-time-format.html) temsili kullanılarak belirtilir. 

## <a name="http-methods"></a>HTTP yöntemleri

Fiil   | Kullanın
------ | -----------
GET    | Genellikle verileri alarak salt okunurdur bir işlem gerçekleştirir.
HEAD   | Karşılık gelen istek için yanıt üst bilgilerini getirir `GET` .
PUT    | Mevcut olmayan veya varsa, güncelleştiren bir kaynak oluşturur. Bazı kaynaklar güncelleştirmeyi desteklemiyor olabilir.
DELETE | Bir kaynağı siler veya listesini kaldırır.

## <a name="http-status-codes"></a>HTTP durum kodu

Kod | Açıklama
---- | -----
200  | Başarılı olur ve bir yanıt gövdesi vardır.
201  | Başarılı ve kaynak oluşturuldu.
202  | Başarılı oldu, istek kabul edildi ancak bazı işler hala tamamlanmamış ve zaman uyumsuz olarak tamamlandı olabilir.
204  | Başarılı, ancak yanıt gövdesi yok.
301  | Kalıcı bir yeniden yönlendirme.
302  | Geçici yeniden yönlendirme.
400  | URL 'deki veya istek gövdesindeki parametreler geçerli değil.
401  | Belirtilen kimlik bilgileri geçersiz.
403  | Verilen kimlik bilgileri verilen eyleme izin verilmiyor.
404  | İstenen kaynak yok.
409  | İstek, var olan bir kaynakla çakışıyor.
500  | Hizmet beklenmeyen bir hatayla karşılaştı.
503  | Hizmet geçici olarak kullanılamıyor.

`GET`BIR API uç noktasına yapılan herhangi bir istek, http yeniden yönlendirme (301 veya 302) döndürebilir. İstemciler, üstbilgiyi gözlemleyerek `Location` ve daha sonra yayımlayarak bu yeniden yönlendirmeleri düzgün şekilde işlemelidir `GET` . Belirli uç noktalarla ilgili belgeler, yeniden yönlendirmelerin nerede kullanılabileceğini açıkça çağırmaz.

500 düzeyinde bir durum kodu söz konusu olduğunda, istemci makul bir yeniden deneme mekanizması uygulayabilir. Resmi NuGet istemcisi, 500 düzeyinde bir durum kodu veya TCP/DNS hatası ile karşılaşıldığında üç kez yeniden dener.

## <a name="http-request-headers"></a>HTTP istek üstbilgileri

Ad                     | Açıklama
------------------------ | -----------
X-NuGet-ApiKey           | Gönderme ve silme için gerekli, bkz. [ `PackagePublish` kaynak](package-publish-resource.md)
X-NuGet-Client-Version   | **Kullanım dışı** ve değiştirilmiş `X-NuGet-Protocol-Version`
X-NuGet-protokol-sürümü | Yalnızca nuget.org üzerinde bazı durumlarda gereklidir, bkz. [NuGet.org Protocols](NuGet-Protocols.md)
X-NuGet-oturum kimliği       | *Isteğe bağlı* . NuGet istemcileri v 4.7 + aynı NuGet istemci oturumunun parçası olan HTTP isteklerini belirler.

, `X-NuGet-Session-Id` İçinde tek bir geri yükleme ile ilgili tüm işlemler için tek bir değere sahiptir `PackageReference` . Otomatik tamamlama ve geri yükleme gibi diğer senaryolar için `packages.config` kodun birbirine nasıl bağlı olduğu ile ilgili birkaç farklı oturum kimliği olabilir.

## <a name="authentication"></a>Kimlik Doğrulaması

Kimlik doğrulaması, tanımlanacak paket kaynak uygulamasına bırakılır. Nuget.org için yalnızca kaynak, `PackagePublish` Özel BIR API anahtarı üst bilgisi aracılığıyla kimlik doğrulaması gerektirir. Ayrıntılar için bkz. [ `PackagePublish` kaynak](package-publish-resource.md) .
