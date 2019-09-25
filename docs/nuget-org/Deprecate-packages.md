---
title: Nuget.org 'de paketleri kullanımdan kaldırma
description: Paketleri kullanımdan kaldırma işlemi ve istemcilerin bu bilgileri nasıl gösterdiği hakkında ayrıntılı açıklama
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248899"
---
# <a name="deprecating-packages"></a>Paketleri kullanımdan kaldırma

Artık paket bulundurmuyorsa veya paketinizin tüketicilerini başka bir pakete geçiş yapmak istiyorsanız bir paketi kullanımdan kaldırabilirsiniz. 

Paket kullanımdan kaldırma, paketinizin aşağıda açıklandığı gibi **listelenenden** farklıdır:
* Bir paketin **listesinin kaldırılması** , arama sonuçlarında gizlendiğinden bulma işlemini engeller. 
* **Bir paketin** kullanım dışı bırakılması, paketinizin mevcut tüketicilerinin projelerine yüklenip yüklenmediğini veya bu kullanıcılara kullanılmaları halinde bulmasını sağlar. Ayrıca, kullanım dışı bırakma nedenini ve sizin tarafınızdan belirtilen alternatif önerilen paketi (paket yayımcısı) öğrenmelerini sağlar. Bir paketin kullanımdan kaldırılması paketin listesini kaldırma. 

Bir yayımcı olarak, hem listeyi kaldırmayı hem de paketleri kullanımdan kaldırmayı tercih edebilirsiniz.

## <a name="deprecation-workflow"></a>Kullanımdan kaldırma iş akışı
1. Bir paketin kullanımdan kaldırılması için **paketleri Yönet** ' e gidin ve **kullanımdan**Kaldır ' ı seçin:

    ![Kullanımdan Kaldır ' a git paket seçeneği](media/deprecation-select-option.png)

2. Kullanımdan kalkmak istediğiniz sürümü seçin. Tüm sürümü kullanımdan kaldırmayı istiyorsanız **tüm sürümleri Seç** seçeneğini belirleyin.

    ![Kullanımdan kalkmak için paket sürümlerini seçin](media/deprecation-select-version.png)

3. Kullanımdan kaldırma için bir neden seçin. Paket artık korunmuyorsa, **eski** seçeneğini belirleyin. Belirli bir sürüm kritik bir hata kullanıyorsa, **kritik hataları olan** seçeneğini belirleyin. Başka bir nedenle **diğer**' i seçin. Her zaman farklı bir önerilen paket (ve sürüm) ve Sahibe özel bir ileti belirtebilirsiniz. 

    ![Nedenler diğer paket önerisi ve özel ileti seçin](media/deprecation-save.png)

> [!Note]
> Özel ileti yalnızca nuget.org 'de gösterilir ancak istemcilerden gösterilmez. Şu anda, `dotnet.exe` ve NuGet Paket Yöneticisi gibi istemciler özel iletiyi göstermez.

## <a name="client-experience-for-deprecated-packages"></a>Kullanım dışı bırakılan paketler için istemci deneyimi
Bir paket kullanımdan kaldırıldıktan sonra, tüketicileri aşağıdaki yollarla (kullanılan istemciye bağlı olarak) bilgilendirilir.

### <a name="visual-studio"></a>Visual Studio 
*Visual Studio 2019 sürüm 16,3 ' den başlayarak kullanılabilir*

Visual Studio, `Installed` kullanım dışı bırakılan paketin kullanımıyla ilgili olarak uyarır. Bu, pakete ve kullanımdan kaldırılmasıyla ilgili bilgileri (kullanım dışı olma nedeni ve varsa bunun yerine kullanılacak alternatif paket) size yol açacaktır.

   ![Paket Yöneticisi 'nin Visual Studio yüklü sekmesindeki kullanım dışı paketler](media/deprecation-vs.png)

### <a name="dotnetexe"></a>DotNet. exe
*.NET SDK 3,0 ile başlayarak kullanılabilir*

DotNet. exe ' yi kullanırsanız, kullanım dışı bırakılan paketlerin listesini `dotnet list package --deprecated` kullanımdan kaldırma bilgileriyle birlikte çalıştırmak için çözüm veya proje klasörü üzerinde komutunu çalıştırabilirsiniz:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
