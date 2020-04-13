---
title: nuget.org'da ambalajları küçümseme
description: Paketleri küçümseme işlemi ve istemcilerin bu bilgileri nasıl gösterdiği hakkında ayrıntılı açıklama
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096879"
---
# <a name="deprecating-packages"></a>Amortisman paketleri

Bir paketi artık muhafaza etmezseniz veya paketinizin tüketicilerini başka bir pakete geçmeye teşvik etmek istiyorsanız, paketi amortismana dahil edebilirsiniz. 

Paket amortismanı, aşağıda açıklandığı gibi paketinizin **listeyi bırakmadan** farklıdır:
* Bir paketin **listelenmesi,** arama sonuçlarında gizli olduğundan bulunmasını engeller. 
* Bir paketin **amortismana sokulmaması,** paketinmevcut tüketicilerinin paketi yüklü veya projelerinde kullanıp kullanmadıklarını öğrenmelerini sağlar. Ayrıca, amortisman nedenini ve sizin (paket yayımcısı) tarafından belirtildiği gibi alternatif bir önerilen paket ilerler. Bir paketi küçümsemek paketin listesini geri almaz. 

Yayımcı olarak, paketleri hem listedışı bırakmayı hem de amortismanı seçebilirsiniz.

## <a name="deprecation-workflow"></a>Amortisman iş akışı
1. Bir paketi amortismana katmayı yönetmek için **paketleri Yönet'e** gidin ve **Amortisman'ı**seçin:

    ![Paket seçeneğini amortismana gitme](media/deprecation-select-option.png)

2. Amortismana uymak istediğiniz sürümü seçin. Tüm sürümü amortismana kayırmak istiyorsanız, **tüm sürümleri seç** seçeneğini belirleyin.

    ![Amortismana uymak için paket sürümlerini seçin](media/deprecation-select-version.png)

3. Amortisman için bir neden seçin. Paket artık korunmazsa, **Eski** seçeneğini seçin. Belirli sürümde kritik bir hata varsa, **kritik hataları seçeneği ni** seçin. Başka bir nedenle **Diğer'i**seçin. Her zaman alternatif bir önerilen paket (ve sürüm) ve sahiplerine özel bir ileti belirtebilirsiniz. 

    ![Alternatif paket önerisi ve özel ileti nedenleri seçin](media/deprecation-save.png)

> [!Note]
> Özel ileti yalnızca nuget.org gösterilir, ancak istemcilerden gösterilmez. Şu anda, `dotnet.exe` nuget paket yöneticisi gibi istemciler özel iletiyi göstermez.

## <a name="client-experience-for-deprecated-packages"></a>Amortismana uyan paketler için müşteri deneyimi
Bir paket amortismana uğradıktan sonra, tüketicilere bu konuda aşağıdaki yollarla bilgi verilir (kullanılan müşteriye bağlı olarak).

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 sürümü16.3'ten itibaren kullanılabilir*

Visual `Installed` Studio, sekmede amortismana lı bir paketin kullanımı konusunda uyarır. Paket ve amortisman bilgileri için bir uyarı gösterir (amortismana neden ve varsa kullanılacak alternatif paket dahil).

   ![Visual Studio'da amortismana küçümşen paketler paket yöneticisisekmesine yüklenmiş](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*.NET SDK 3.0 ile başlayan fiyatlarla*

dotnet.exe kullanıyorsanız, amortisman bilgileriyle `dotnet list package --deprecated` birlikte amortismana alınan paketlerin listesini almak için çözüm veya proje klasöründeki komutu çalıştırabilirsiniz:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
