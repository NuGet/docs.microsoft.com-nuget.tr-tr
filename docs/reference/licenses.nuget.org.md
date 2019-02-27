# <a name="licensesnugetorg"></a>Licenses.nuget.org

## <a name="rationale"></a>Stratejinin

Sunulmasıyla birlikte [lisans ifadeleri](nuspec.md#license) ayrı lisans tanımlayıcıları, özel durum tanımlayıcıları veya lisans ifadeler için bir başvuru metin sağlayacağını güvenilir bir hizmet için bir gereksinim ortaya çıktı.
Bu hizmet için ek bir gereksinim rot, bağlantı açık değil ve böylece güvenli bir şekilde, geriye dönük uyumluluk için eski istemcileri sağlamak için kullanabiliriz kararlı bir URL şeması sağlamaktır.

Bu rol Licenses.nuget.org karşılar. Nuget.org lisansa lisansı ifade kullanarak belirttiğiniz paketleri için lisans metin başvurusu sağlamak için kullanır. `nuget pack` ya da diğer paket [istemci araçları](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) ayarlamak [ `licenseUrl` ](nuspec.md#licenseurl) geriye doğru desteklemeyen eski istemciler uyum sağlamak için licenses.nuget.org işaret edecek şekilde öğe `license` öğe.

## <a name="protocol"></a>Protokol

Licenses.nuget.org tarayıcılarını kişiler tarafından görüntülenmesine yönelik, makine tarafından okunabilir yanıt sağlanır.
HTTPS protokolü kullanılmalıdır ve istekleri belirli bir biçimde oluşturulmuş beklenir. Yalnızca destekler `GET` istekleri.
Bu lisans deyimlerde ya da lisans özel durum tanımlayıcıları aşağıda belirtilen şekilde girdi olarak kabul eder. Lütfen unutmayın, lisans ifadelerin tüm öğeleri büyük/küçük harfe duyarlıdır ve bu nedenle tüm licenses.nuget.org de büyük küçük harfe duyarlı giriştir.

### <a name="license-expressions"></a>Lisans ifadeleri

#### <a name="request"></a>İstek

Lisans ifadeleri (Önemsiz durumları ifade tek bir lisans oluşuyorsa dahil) sahip olmasını [URL kodlamalı](https://tools.ietf.org/html/rfc3986#section-2.1) ve licenses.nuget.org isteğinde bir yol olarak kullanılır.

| Lisans ifadesi | Kullanılacak URL'si |
|:---|:---|
MIT                                                | https://licenses.nuget.org/MIT
(MIT)                                              | https://licenses.nuget.org/(MIT)
(LGPL 2.0-ile yalnızca FLTK özel durumu veya Apache-2.0+) | https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)

Hizmet, yalnızca lisans tanımlayıcıları ve nuget.org tarafından kabul edilen lisans özel durum tanımlayıcıları destekler. Desteklenmeyen lisans tanımlayıcıları veya lisans özel durum tanımlayıcıları içeren veya lisans ifadesi söz dizimi için uygun değil tüm lisans ifadeleri geçersiz olarak kabul edilir.

#### <a name="response"></a>Yanıt

Licenses.nuget.org geçerli lisans ifadelerle bir HTTP 200 durum kodu ve lisansı ifade açıklamasını içeren bir web sayfası içeren isteklere yanıt verir:
* Lisans ifade sağlandıysa bu lisans başvuru metni içeren bir web sayfası döndürülen bir tek bir lisans tanımlayıcısı içeriyor;
* sağlandıysa lisans ifade bir bileşik lisans ifadesi, tek bir lisans veya lisans özel durumu başvuruları için bağlantılarla birlikte lisans ifadesi içeren bir web sayfası döndürülür.

Bir HTTP 404 yanıt geçersiz lisans ifade sonucu içeren tüm istekleri.

### <a name="license-exceptions"></a>Lisans özel durumları

#### <a name="request"></a>İstek

Lisans özel durum tanımlayıcıları, URL kodlamalı ve licenses.nuget.org isteğine bir yolu olarak kullanılan olması gerekir. Tek bir istekte yalnızca bir tek bir lisans özel durum tanımlayıcısı sağlanabilir. Lisans özel durum tanımlayıcısı yanı sıra herhangi bir ek karakter URL'nin yol kısmı sunabilir.

| Lisans özel durum tanımlayıcısı | Kullanılacak URL'si |
|:---|:---|
FLTK özel durumu            | https://licenses.nuget.org/FLTK-exception
openvpn openssl durum | https://licenses.nuget.org/openvpn-openssl-exception

#### <a name="response"></a>Yanıt

Licenses.nuget.org bir HTTP 200 yanıtı ve belirtilen lisans özel durum başvuru metni içeren bir web sayfası ile bilinen lisans özel durum tanımlayıcıya sahip bir isteğe yanıt verir.

Desteklenmeyen lisans özel durum tanımlayıcı içeren herhangi bir istek, bir HTTP 404 yanıt olarak sonuçlanır.