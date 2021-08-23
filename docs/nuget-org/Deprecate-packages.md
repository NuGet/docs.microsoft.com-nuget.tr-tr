---
title: Nuget.org'de paketleri kullanımdan nuget.org
description: Paketlerin kullanımdan kullanımdan nasıl kullanım dışı olduğu ve istemcilerin bu bilgileri nasıl gösteriyor olduğuyla ilgili ayrıntılı açıklama
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 4a6dbd645cb72b0085fd0347def58ade134fc5ee
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726970"
---
# <a name="deprecating-packages"></a>Paketleri kullanım dışı

Bir paketi artık korumadıysanız veya paketinizin tüketicilerini başka bir pakete taşımaya teşvik etmek için paketi kullanım dışı abilirsiniz. 

Paketi kullanımdan kaldırdık, aşağıda **açıklanan şekilde paketinizi** listeye alamadan farklıdır:
* **Bir paketin** liste dışı listesi, arama sonuçlarında gizlenen bir paketin bulunmasına engel olur. 
* **Bir paketin kullanım** dışı olması, paketinizin mevcut tüketicilerinin paketi yüklemiş veya projelerinde kullanmış olup olduklarını bulmalarına olanak sağlar. Ayrıca, kullanımdan kullanımdan nedenin ve sizin belirttiğiniz (paket yayımcısı) alternatif bir önerilen paket hakkında bilgi sağlar. Bir paketi kullanımdan kaldırdık, paketinlistelerini geri alamaz. 

Yayımcı olarak, hem liste dışı hem de kullanım dışı paketleri seçebilirsiniz.

## <a name="deprecation-workflow"></a>Kullanım dışı iş akışı
1. Bir paketi kullanımdan silmek için Paketleri **yönet'e gidin ve** Kullanım dışı **bırak'ı seçin:**

    ![Paketi kullanım dışı bırak seçeneğine gidin](media/deprecation-select-option.png)

2. Kullanımdan silmek istediğiniz sürümü seçin. Tüm sürümleri kullanımdan silmek için Tüm sürümleri seç **seçeneğini** belirleyin.

    ![Kullanım dışı olacak paket sürümlerini seçme](media/deprecation-select-version.png)

3. Kullanım dışı için bir neden seçin. Paket artık bakımda yoksa Eski **seçeneğini** belirleyin. Belirli bir sürümde kritik bir hata varsa Kritik hatalar **var seçeneğini** belirleyin. Başka bir nedenle Diğer'i **seçin.** Her zaman alternatif bir önerilen paket (ve sürüm) ve sahiplere özel bir ileti belirtebilirsiniz. 

    ![Alternatif paket önerisi ve özel ileti seçme nedenleri](media/deprecation-save.png)

> [!Note]
> Özel ileti yalnızca istemcilerde nuget.org istemcilerden gösterilmez. Şu anda ve gibi `dotnet.exe` istemciler NuGet Paket Yöneticisi özel iletiyi göstermemektedir.

## <a name="client-experience-for-deprecated-packages"></a>Kullanım dışı paketler için istemci deneyimi
Bir paket kullanım dışı kaldıktan sonra, tüketicileri bu paket hakkında aşağıdaki yollarla (kullanılan istemciye bağlı olarak) bilgi alır.

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 sürüm 16.3'te başlayarak kullanılabilir*

Visual Studio, sekmede kullanım dışı bir paketin kullanımı hakkında uyarı `Installed` görüntüler. Paket ve kullanımdan kullanım dışı durumuna ilişkin bir uyarı gösterir (kullanım dışı nedeni ve varsa bunun yerine alternatif paket de dahil).

   ![Paket yöneticisinin yüklü Visual Studio paketlerde kullanım dışı paketler](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*.NET SDK 3.0'dan başlayarak kullanılabilir*

Bir dotnet.exe kullanıyorsanız, kullanım dışı paketlerin listesini ve kullanım dışı bilgilerini almak için çözümün veya proje klasöründe `dotnet list package --deprecated` komutunu çalıştırabilirsiniz:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```

## <a name="transfer-popularity-to-a-newer-package"></a>Popülerliği daha yeni bir pakete aktarma

Eski bir paketi kullanım dışı kalan paket yazarları, daha yeni paketin arama derecelendirmesini artırmak için "popülerliğini" daha yeni bir pakete aktarmayı seçebilir. Bu, müşterilerin kullanım dışı paket yerine daha yeni paketi keşfetmelerini sağlar.

Örneğin, iki paketim olduğunu diyelim:

* 3 milyon indirme içeren kullanım `Contoso.Legacy` dışı eski paketim
* En son `Contoso.Latest` paketim, 5 indirme

NuGet.org, daha yüksek indirme/popülerliği olan arama sonuçlarını tercih eder. "Contoso" arama sorgusuyla kullanım dışı olan paketim büyük olasılıkla arama sonuçlarında en son `Contoso.Legacy` paketimin `Contoso.Latest` üzerine çıktı.

Bu sorunu çözmek için, kullanım dışı olan eski paketimin popülerliğini en son paketime aktarmaya uygulayabilirim. Bu, arama `Contoso.Latest` sonuçlarında daha yüksek dereceye neden olurken daha `Contoso.Legacy` düşük dereceye sahip olur. Yalnızca paketlerin dahili popülerlik puanları etkilenir, her paket için gerçek indirme sayısı etkilenmez.

> [!Note]
> Popülerlik aktarımları tüketicilerin eski paketi bulmalarını önemli ölçüde zorlaştırabilir.

Popülerlik aktarımının "Contoso" sorgusu için arama derecelendirmelerini nasıl etkiley etkilerine dair somut bir fikir almak için aşağıdaki tabloya bakın:

| Arama derecelendirmesi    | Popülerlik aktarımı öncesinde        | Popülerlik aktarımının ardından         |
|----------------   |--------------------------------   |--------------------------------   |
| 1                 | *Contoso.Legacy, 3 milyon indirme*    | *Contoso.Latest, 5 indirme*     |
| 2                 | Contoso.Scanner, 2 milyon indirme     | Contoso.Scanner, 2 milyon indirme     |
| 3                 | Contoso.Core, 1,5 milyon indirme     | Contoso.Core, 1,5 milyon indirme     |
| 4                 | Contoso.UI, 1 milyon indirme          | Contoso.UI, 1 milyon indirme          |
| ...               | ...                               | ...                               |
| 20                | *Contoso.Latest, 5 indirme*     | *Contoso.Legacy, 3 milyon indirme*    |

### <a name="popularity-transfer-application-process"></a>Popülerlik aktarımı uygulama işlemi

1. Popülerlik [aktarımı gereksinimlerini gözden geçirme.](#popularity-transfer-requirements)
2. Popülerliği aktaracak olan kullanım dışı paketi ve popülerliği aktarımını alacak kararlı paketlerin listesini içeren [account@nuget.org](mailto:account@nuget.org) e-posta.

Uygulama gönderildikten sonra, size uygulamanın kabul veya ret (reddetmeye neden olan ölçütler) hakkında sizi bilgilendiracağız. Sahip kimliğini onaylamak için ek tanımlama soruları sormamız gerekir.

#### <a name="popularity-transfer-requirements"></a>Popülerlik aktarımı gereksinimleri

* Eski paketler ve yeni paketler tüm sahipleri paylaşmalıdır.
* Yeni paketler, adlandırma ve işlev (yani bir evrim veya yeni nesil) eski paketlerle açıkça ilişkili olması gerekir.
* Eski paketlerin tüm sürümleri kullanım dışı olmalı ve aktarımı alan yeni paketlere işaret etmek gerekir.
* Popülerlik aktarımı kullanıcıların kafa karışıklığına neden NuGet veya arama deneyiminin NuGet kötüleştirmesi gerekir.
* Yeni paketlerin kararlı bir sürümü olması gerekir.
* Eski paket, başka bir kullanım dışı paketten popülerlik aktarımları almamalı.

### <a name="advanced-popularity-transfer-scenarios"></a>Gelişmiş popülarite aktarımı senaryoları

#### <a name="package-consolidations"></a>Paket birleştirmeleri

Kullanım dışı olan birden çok paketin popülerliğini tek bir yeni pakete göre aktarabilirsiniz. Örneğin, 3 paketim olduğunu diyelim:

* Kullanım dışı olan ilk eski paketim, `Contoso.Legacy1`
* Kullanım dışı kalan ikinci eski paketim, `Contoso.Legacy2`
* Yeni birleştirilmiş paketim, `Contoso.Latest`

ve kullanımdan edildikten `Contoso.Legacy1` `Contoso.Legacy2` sonra, popülerliklerini 'ye aktaracak şekilde `Contoso.Latest` uygulayabilirsiniz.

#### <a name="package-splits"></a>Paket bölmeleri

Kullanım dışı bir paketin popülerliği en fazla 5 yeni pakete aktarıldı ve pakete bölündü. Bu, kullanım dışı bir paketin işlevselliği birden çok yeni paket arasında bölündü ise yararlıdır. Örneğin, 3 paketim olduğunu diyelim:

* Kullanım dışı olan eski paketim, `Contoso.Legacy`
* İlk yeni paketim, `Contoso.Web`
* İkinci yeni paketim, `Contoso.Cloud`

`Contoso.Legacy` hem web hem de bulut işlevlerini içerir, ancak bu işlevselliği yeni nesil için farklı paketlere ayırmaya karar verdim. Kullanım dışı verdikten `Contoso.Legacy` sonra, hem hem de 'ye popülerliğini aktarmaya `Contoso.Web` `Contoso.Cloud` uygulayabilirsiniz.

> [!Warning]
> Aktarılan popülerlik tüm yeni paketler arasında bölünecek. Sonuç olarak, kullanım dışı olan paketinizin popülerliğini mümkün olduğunca az pakete aktarmanızı öneririz.

#### <a name="popularity-transfer-chains"></a>Popülerlik aktarım zincirleri

Kullanım dışı olan bir paketin popülerliği zaten kullanım dışı olan başka bir paketten alıyorsa, bu paketin popülerliği aktaramaz. Örneğin, 3 paketim olduğunu diyelim:

* Kullanım dışı olan eski paketim, `Contoso.First`
* Kullanım dışı olan eski paketim, `Contoso.Second`
* Yeni paketim, `Contoso.Latest`

Popülerliğini `Contoso.First` olarak `Contoso.Second,` aktarıyorsa, `Contoso.Second` popülerliğini olarak `Contoso.Latest` aktaramaz. Bunun yerine, Paket birleştirme senaryosuna göre hem `Contoso.First` hem `Contoso.Second` `Contoso.Latest` de'nin popülerliğini ['ye aktarmayı](#package-consolidations) öneririz.
