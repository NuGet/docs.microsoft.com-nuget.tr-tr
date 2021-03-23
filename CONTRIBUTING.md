---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859574"
---
Katkı çok büyük veya çok küçük.

1. [Docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/)üzerinde düzenlenecek sayfayı ziyaret edin ve sağ üst köşedeki **Düzenle** düğmesine tıklayın. Bu, sizi depoya uygun markaşağı sayfasına getirir.
1. Marklt 'ı düzenleyin:
    1. Görüntüler dahil ediyorsanız (genellikle PNG 'leri kullanın), bunları konunun klasöründeki medya klasörüne yerleştirin. Bağlantılar daha sonra `media/<image_name>.png` .
    1. Bu DocSet içindeki diğer sayfalara yönelik göreli bağlantılar `../<folder>/<topic-file>.md` , eğitimi de içeren biçimde olmalıdır `.md` . Aynı klasörde başka bir konuya bağlantı oluşturuyorsanız, bu durumda `../<folder>/` atlanabilir. Bağlayıcıları kullanırken, her zaman ' dan önce dahil etmeyi unutmayın `.md` `#` .
    1. Dış bağlantıları, özellikle de docs.microsoft.com (veya daha eski içerik için msdn.microsoft.com) kullanılırken, başka bir dildeki bir okuyucunun kullanılabilir olması durumunda aynı dildeki bir hedef sayfada yer alması için "en-US" gibi herhangi bir dil etiketini atlayın.
1. İşiniz bittiğinde, aşağıdan bir kayıt iletisi girin ve **dosya değişikliği öner**' e tıklayın.
1. Değişiklik için bir çekme isteği gönderin. Düzenli aralıklarla PR 'ler gözden geçiririz.
1. Teşekkür ederiz!

Yeni bir konu oluşturuyorsanız şunları göz önünde bulundurun:

1. Yeni konuyu her zaman uygun bir alt klasöre yerleştirin ve burada kullanılan dosya adları için kuralları izleyin.
1. Diğer konularda gördüğünüz şekilde bir meta veri bloğu dahil etmeniz gerekir. Normal varsayılanlar (örneğin, MS. Workload ve MS. gözden geçireni), üzerindeki docs/docjx.jsiçinde ayarlanır, bu nedenle yalnızca aşağıdakileri değiştirmeniz gerekir:

  - title: arama sonuçlarında görünen başlık. SEO için bu ideal olarak, makalenin en üst düzey # (H1) ile aynı değildir.
  - Açıklama: arama sonuçlarında görünen makalenin Özeti.
  - Yazar: yazarın GitHub KIMLIĞI, bu makaleye ilişkin sorun dosyaları atanır.
  - MS. Author: Yazar bir Microsoft çalışanı ise, bu Microsoft diğer addır. Diğer kanallardan gelen geri bildirimleri raporlamak ve iletmek için kullanılır.
  - Yönetici: varsa yazarın yöneticisinin Microsoft diğer adı.
  - MS. Date: makalenin en son düzeltilmesi veya tarihin aa/gg/yyyy biçiminde incelenmesi (önde sıfır kullanın). Bu, yenilik hakkında bir iletişim kurudur, bu nedenle küçük değişiklikler için, yalnızca daha önemli düzeltmeler veya bir değişiklik olmasa bile makalenin yeniden doğrulanması durumunda güncelleştirilmemiş.
  - MS. Topic: raporlardaki makaleyi kategorilere ayırmak için kullanılır. Aşağıdaki tabloya bakın. Makalelerin çoğu "kavramsal" dir. 
1. Sayfanızı eklemenin yanı sıra, bu sayfaya bir bağlantı eklemek için docs/TOC. MD 'yi düzenleyin.
1. TOC 'ye bir üst düzey düğüm ekliyorsanız, docs/index. MD içinde de bir giriş yapın.

| MS. Topic kategorisi | Açıklama |
| --- | --- |
| yordam | Başka bir içeriğe sahip olmayan içerikler için kullanın. Bu, docfx.jsüzerinde varsayılan olarak ayarlanır. |
| genel bakış | Genel Bakış veya Kullanıcı Kılavuzu makaleleri için, genellikle yalnızca TOC 'deki bir "genel bakış" düğümü altında yaşayan kişiler için kullanın. |
| hızlı başlangıç | TOC 'nin hızlı başlangıç yönergelerine göre yazıldığı "hızlı başlangıç" düğümü altında herhangi bir şey. |
| öğretici | "Öğretici" düğümü altında, eğitim yönergelerine göre yazılan TOC 'de her şey. |
| reference | Otomatik olarak oluşturulmayan herhangi bir başvuru türü makale. |
| makale | Topluluk tarafından katkıda bulunulan içerik (diğer bir deyişle, mühendislik ekibinin dışından veya Microsoft 'un docs ekibinin dışında herhangi bir şey) için kullanın. |
