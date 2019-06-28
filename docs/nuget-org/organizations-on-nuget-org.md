---
title: Kuruluşunuz nuget.org
description: NuGet.org üzerindeki kuruluşlar şirket ortamı bir takım veya grup tarafından yayımlanmış paketleri yönetmenize yardımcı olur.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427541"
---
# <a name="your-organization-on-nugetorg"></a>Kuruluşunuz nuget.org

Kuruluşlar, işletmelerin ve açık kaynaklı projelerin paketleri NuGet.org tek bir kimlik kullanarak işbirliği yapmak için etkinleştirin. Bir paket kullanıcısı için bir kuruluş hesabı NuGet.org üzerinde var olan bir kullanıcı hesabı ile aynı görünür.

## <a name="organization-accounts-vs-individual-accounts"></a>Kuruluş hesapları bireysel hesaplar karşılaştırması

Bir kuruluş hesabı bir veya daha fazla kişi (kullanıcı) hesabı, üyelere sahiptir. Bu üyeleri, sahipliği için tek bir kimlik korurken bir dizi paketleri yönetebilirsiniz.

Kişisel hesabınıza kimliğinizi nuget.org ve kuruluşların herhangi bir sayıda üyesi olabilir. Bir paketi tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir. Paketi tüketicileri bir bireysel hesabı veya kuruluş hesabı arasındaki fark görmüyorum: her ikisi de paketi olarak görünen `owners`.

## <a name="adding-a-new-organization"></a>Yeni kuruluş ekleniyor

Yeni bir kuruluş eklemek için nuget.org hesabınızı seçin ve ardından **kuruluşlar Yönet...**  menü komutu:

![NuGet.org Manager kuruluşlar için menü seçeneği](media/org-manage-option.png)

Sonraki sayfada seçin **yeni kuruluş Ekle** düğmesi:

![NuGet.org yeni bir kuruluş oluşturmak için](media/org-add-new-option.png)

Sonraki sayfada kuruluş adı ve e-posta adresini belirtin. Kullanıcı hesapları olarak aynı ad kuruluş hesapları paylaşma olduğundan, kuruluş adını diğer tüm mevcut kuruluş veya kullanıcı hesapları farklı olması gerekir. E-posta adresi, ayrıca tüm hesapları arasında benzersiz olmalıdır.

![NuGet.org yeni bir kuruluş sayfası ekleyin](media/org-add-new-page.png)

Kuruluş hesabı oluşturulduktan sonra yönetici kuruluş için paketleri göndermek ve kuruluş üyeleri ekleyin.

### <a name="transform-existing-account-to-an-organization"></a>Var olan bir kuruluş hesabına dönüştürme

> [!Warning]
> Hesap dönüştürme bir işlemdir: bir kuruluş için bir kullanıcı hesabı için bir geri dönüştürülemez.

Paketleri tek bir kullanıcı hesabı kullanarak bir takım olarak yönettiğiniz ve bu hesabı bir kuruluşa, kullanım dönüştürmek istiyorsanız **kuruluş hesabınıza dönüştürme** seçeneğini **kuruluşlaryönetme** sayfası:

![NuGet.org seçeneği var olan bir kuruluş hesabına dönüştürmek için](media/org-transform-option.png)

Sonraki sayfada, kuruluş yöneticisi olarak atamak ve ardından farklı bir kullanıcı hesabı belirtmek **dönüştürme**.

![Bir kuruluş için bir kullanıcı hesabı dönüştürme bilgileri girme](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Kuruluş üyeleri yönetme

Kuruluş yöneticisi olarak, her üyenin NuGet.org sağlayarak üyeler ekleyebilirsiniz *kullanıcı hesabı adı*; e-posta adresleri kullanılamaz. Ardından her üye bir ortak çalışanı veya aşağıdaki izinlere sahip yönetici olarak işaretleyin:

| İzin | Ortak çalışanı | Yönetici |
| --- | --- | --- |
| Kuruluşun paketlerini yönetme<br/>(yeni bir paket gönderin, güncelleştirmek veya mevcut paketlerini listeden Kaldır) | Evet | Evet |
| Değişiklik kuruluş meta verileri<br/>(e-posta adresi, bildirim ayarları) | Hayır | Evet |
| Kuruluş üyelerini Yönet | Hayır | Evet |
| İstek veya kuruluş paketleri co-ownership isteklerinde ile harekete geçme | Hayır | Evet |

## <a name="managing-packages"></a>Paketleri yönetme

Hesabınızı ve hangi kullandığınız üyesi tüm kuruluşlar arasında tüm paketleri görüntüleyebilirsiniz [paketlerini Yönet](https://www.nuget.org/account/Packages) sayfası. Hesabınız veya belirli kuruluşlarla özgü paketleri görüntülemek için üst kısımdaki hesapları filtreyi kullanın sayfanın sağ.

![Hesap filtreyle paketlerini yönetme](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Bir kuruluş için paketleri aktarma
Yeni oluşturulan bir kuruluş bazı paketlerinizi aktarmak istiyorsanız, kuruluş hesabı paket birlikte kendi isteyen ve ardından kendiniz sahibi olarak kaldırarak bunu yapabilirsiniz. Kuruluşun bir yöneticiyseniz sahipliği kabul etmek için gerekli bir onay yok yoktur. Ancak, bir ortak çalışanı varsa, sahibi olarak kuruluş ekleme sahipliği kabul etmek için Yöneticiler birini gerektirir.

## <a name="publishing-packages"></a>Paket yayımlama

Bir kullanıcı hesabına paketleri gibi bir kuruluşa paketlerini Yayımla: doğrudan NuGet.org için paket yüklemek veya paket gönderme `nuget push` veya `dotnet nuget push` CLI komutları.

### <a name="uploading-packages"></a>Paket karşıya yükleniyor

Karşıya yüklerken, doğrudan yeni bir paket üzerinde [NuGet.org karşıya](https://www.nuget.org/packages/manage/upload) sayfasında, atadığınız paket sahibi bir kullanıcı veya kuruluş hesabı:

![Hesap seçeneği ile paketini karşıya yükleyin](media/org-upload-option.png)

### <a name="using-api-keys"></a>API anahtarları kullanma

Bir paket göndermeyi `nuget push` veya `dotnet nuget push` CLI komutları, bu komutlar tarafından gereken bir API anahtarı alması gerekir. Ayrıntılar için bkz [paket yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).

Yeni bir API anahtarı oluştururken, uygun kuruluştaki seçin **paket sahibinden** açılır. Oluşturduğunuz herhangi bir API anahtarı yalnızca seçilen kuruluş için geçerlidir:

![Hesap seçeneği sahip API anahtarı](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Bir kuruluş kaldırılıyor

Bir kullanıcı olarak, kendiniz bir kuruluştan seçerek kaldırabilirsiniz **X** kuruluş üyeliğinizin tarafından gösterilen düğmesi:

![Bir kuruluştan bir kullanıcı hesabı kaldırma](media/org-remove-self-option.png)

Yöneticiler, diğer yöneticiler dahil kuruluştan herhangi bir üyesi kaldırabilir. Tek bir kuruluş yöneticisi değilseniz, başka bir üyesi bir yönetici eklemediğiniz sürece kendiniz kaldırılamıyor.

### <a name="deleting-an-organization-account"></a>Bir kuruluş hesabı siliniyor

Tıklayarak bir kuruluş hesabı silebilirsiniz **Sil** kuruluş sayfanızın gösterilen düğmesi.

![Bir kuruluş siliniyor](media/org-delete-option.png)

Kuruluş silmek için onu tıklayarak onaylamanız gerekir **Sil kuruluş** onay düğmesini.
