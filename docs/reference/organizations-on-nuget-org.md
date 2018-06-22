---
title: Kuruluşların nuget.org üzerinde
description: Nuget.org üzerinde kuruluşlar, şirket ortamında bir ekip veya grup tarafından yayımlanan paketlerini yönetmek için yardımcı olur.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34449584"
---
# <a name="organization-on-nugetorg"></a>Nuget.org kuruluşunda

Kuruluşlar, işletmelerin ve paketleri tek nuget.org kimliğini kullanarak işbirliği yapmak için açık kaynaklı proje etkinleştirin. Bir paket tüketici için bir kuruluş hesabı nuget.org var olan bir kullanıcı hesabı ile aynı görünür.

## <a name="user-accounts-vs-organization-accounts"></a>Kuruluş hesapları ve kullanıcı hesapları

Kullanıcı hesabınızın nuget.org kimliğinizi ve kuruluşların herhangi bir sayıda üyesi olabilir. Bir paket, bir kullanıcı hesabına ait olabilir gibi bir kuruluş hesabına ait olabilir. Paket Tüketiciler, bir kullanıcı hesabı veya kuruluş hesabı arasındaki fark görmüyorum: hem paket olarak görünür `owners`.

Bir kuruluş hesabı bir veya daha fazla kullanıcı hesapları üyeleri sahiptir. Bu üyeler, sahipliği için tek bir kimlik korurken paket kümesini yönetebilirsiniz.

## <a name="adding-a-new-organization"></a>Yeni bir kuruluş ekleme

Yeni bir kuruluş eklemek için nuget.org hesabınızdaki seçin, ardından seçin **kuruluşlar Yönet...**  menü komutu:

![Nuget.org Yöneticisi kuruluşlar için menü seçeneği](media/org-manage-option.png)

Sonraki sayfada seçin **yeni bir kuruluş eklemek** düğmesi:

![Düğme nuget.org üzerinde yeni bir kuruluş oluşturun](media/org-add-new-option.png)

Sonraki sayfada kuruluş adı ve e-posta adresini belirtin. Kullanıcı hesapları aynı ad kuruluş hesaplarında paylaşmak olduğundan, kuruluş adını diğer tüm var olan kuruluş veya kullanıcı hesapları farklı olmalıdır. E-posta adresi, ayrıca tüm hesapları arasında benzersiz olmalıdır.

![Nuget.org üzerinde yeni bir kuruluş sayfa ekleyin](media/org-add-new-page.png)

Kuruluş hesap oluşturulduktan sonra yönetici ve kuruluş için paketleri göndermek ve kuruluş üye ekleyebilirsiniz.

### <a name="transform-existing-account-to-an-organization"></a>Bir kuruluş için mevcut hesap dönüştürme

> [!Warning]
> Hesap dönüştürme işlemi geri alınamaz: kuruluş bir kullanıcı hesabı için geri dönüştürülemez.

Paketleri tek bir kullanıcı hesabı kullanarak bir ekip halinde yönetme ve bu hesap bir kuruluşa, kullanım dönüştürmek istiyorsanız **kuruluş hesabınıza dönüştürme** seçeneği **kuruluşlarınyönetme** sayfa:

![Var olan bir hesap bir kuruluşa dönüştürmek için nuget.org seçeneği](media/org-transform-option.png)

Sonraki sayfada kuruluş yöneticisi olarak atayın ve sonra seçmek için farklı bir kullanıcı hesabı belirtin **dönüştürme**.

![Bir kuruluş için bir kullanıcı hesabı dönüştürme bilgilerini girme](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Kuruluş üyeleri yönetme

Kuruluş yöneticisi olarak, her üyenin nuget.org sağlayarak üye ekleyebilir *kullanıcı hesabı adı*; e-posta adresleri kullanılamaz. Ardından her üye bir ortak çalışanı veya aşağıdaki izinlere sahip yönetici olarak işaretleyin:

| İzin | Ortak çalışanı | Yönetici |
| --- | --- | --- |
| Kuruluşun paketlerini yönetme<br/>(yeni paketleri göndermek, güncelleştirmek veya var olan paketler unlist) | Evet | Evet |
| Değişiklik kuruluş meta verileri<br/>(e-posta adresi, bildirim ayarları) | Hayır | Evet |
| Kuruluş üyeleri yönetme | Hayır | Evet |
| İstek veya kuruluş paketler için co-ownership istekleri hareket | Hayır | Evet |

## <a name="managing-packages"></a>Paketlerini yönetme

Hesabınızın ve hangisinin kullandığınız üyesi tüm kuruluşlar arasında tüm paketleri görüntüleyebilirsiniz [paketlerini Yönet](https://www.nuget.org/account/Packages) sayfası. Belirli bir kuruluş veya hesabınız için belirli paketleri görüntülemek için üst hesapları filtresini kullanma sağ sayfasının.

![Hesap filtresiyle paketlerini yönetme](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Kuruluş için paketler aktarma
Bazı paketlerinizin yeni oluşturulan bir kuruluşa aktarmak istiyorsanız, bunu paket birlikte kendi kuruluş hesabı isteyen ve kendiniz sahibi olarak kaldırarak yapabilirsiniz. Kuruluşun bir yöneticiyseniz sahipliği kabul etmek için gerekli onay yok yok. Ancak, bir ortak çalışanı varsa, kuruluşunuzun sahibi olarak ekleme sahipliği kabul etmek için Yöneticiler birini gerektirir.

## <a name="publishing-packages"></a>Paketleri yayımlama

Bir kullanıcı hesabına paketleri yayımlama gibi kuruluş için paketleri yayımlama: doğrudan nuget.org için paket yüklemek veya paket Ftp'den `nuget push` veya `dotnet nuget push` CLI komutları.

### <a name="uploading-packages"></a>Karşıya yükleme paketleri

Ne zaman doğrudan karşıya yüklediğiniz yeni bir paket üzerinde [nuget.org karşıya yükleme](https://www.nuget.org/packages/manage/upload) sayfasında atadığınız paket sahibi bir kullanıcı ya da kuruluş hesabı:

![Hesap seçeneğiyle paketi yükleme](media/org-upload-option.png)

### <a name="using-api-keys"></a>API anahtarları kullanma

Bir paketi göndermeyi `nuget push` veya `dotnet nuget push` CLI komutları, bu komutları tarafından gerekli bir API anahtarı alması gerekir. Ayrıntılar için bkz [bir paketi yayımlamaya](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Yeni bir API anahtarı oluştururken uygun kuruluşta seçin **paket sahibinden** açılır. Oluşturduğunuz tüm API anahtarı yalnızca seçilen kuruluşa geçerlidir:

![Hesap seçeneğiyle API anahtarı](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Bir kuruluş kaldırma

Bir kullanıcı olarak, kendiniz bir kuruluştan seçerek silebilirsiniz `X` kuruluş üyeliğinizi tarafından gösterilen düğmesi:

![Bir kuruluştan bir kullanıcı hesabını kaldırma](media/org-remove-self-option.png)

Yöneticiler, diğer yöneticiler de dahil olmak üzere kuruluş tarafından herhangi bir üyesi kaldırabilir. Bir kuruluş için tek Yönetici sizseniz, yönetici olarak başka bir üye eklemek sürece kendiniz kaldıramazsınız.

### <a name="deleting-an-organization-account"></a>Bir kuruluş hesabı silme

Bu özellik yakında çıkıyor.
