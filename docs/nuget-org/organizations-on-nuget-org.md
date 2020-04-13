---
title: NuGet.org'daki kuruluşunuz
description: NuGet.org kuruluşlar, grup tarafından veya bir ekip, şirket ortamında yayınlanan paketleri yönetmenize yardımcı olur.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427541"
---
# <a name="your-organization-on-nugetorg"></a>NuGet.org'daki kuruluşunuz

Kuruluşlar, işletmelerin ve açık kaynak projelerinin tek bir NuGet.org kimliği kullanarak paketler üzerinde işbirliği yapmasına olanak tanır. Paket tüketicisi için, bir kuruluş hesabı NuGet.org'daki varolan bir kullanıcı hesabıyla aynı görünür.

## <a name="organization-accounts-vs-individual-accounts"></a>Kuruluş hesapları ve bireysel hesaplar

Kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel (kullanıcı) hesabı vardır. Bu üyeler, sahiplik için tek bir kimlik korurken bir dizi paketi yönetebilir.

Bireysel hesabınız NuGet.org'daki kimliğinizdir ve herhangi bir sayıda kuruluşun üyesi olabilir. Paket, tek bir hesaba ait olduğu gibi bir kuruluş hesabına ait olabilir. Paket tüketicileri tek bir hesap la kuruluş hesabı arasında herhangi `owners`bir fark görmezler: her ikisi de paket olarak görünür.

## <a name="adding-a-new-organization"></a>Yeni bir kuruluş ekleme

Yeni bir kuruluş eklemek için NuGet.org hesabınızı seçin ve ardından **Kuruluşları Yönet...** menü komutunu seçin:

![Yönetici Organizasyonlar için NuGet.org menü seçeneği](media/org-manage-option.png)

Bir sonraki sayfada **yeni kuruluş ekle** düğmesini seçin:

![NuGet.org yeni bir kuruluş oluşturmak için düğme](media/org-add-new-option.png)

Bir sonraki sayfada, kuruluş adını ve e-posta adresini girin. Kuruluş hesapları kullanıcı hesaplarıyla aynı ad alanını paylaştığından, kuruluş adı diğer varolan kuruluş veya kullanıcı hesaplarından farklı olmalıdır. E-posta adresi de tüm hesaplar arasında benzersiz olmalıdır.

![NuGet.org yeni kuruluş sayfası ekleme](media/org-add-new-page.png)

Kuruluş hesabı oluşturulduktan sonra yönetici sizsiniz ve kuruluş için paketler gönderebilir ve kuruluş üyeleri ekleyebilirsiniz.

### <a name="transform-existing-account-to-an-organization"></a>Varolan hesabı bir kuruluşa dönüştürme

> [!Warning]
> Hesap dönüştürme geri alınamaz: Bir kuruluşu kullanıcı hesabına dönüştüremezsiniz.

Paketleri tek bir kullanıcı hesabı kullanarak ekip olarak yönetiyorsanız ve bu hesabı bir kuruluşa dönüştürmek istiyorsanız, Hesabınızı **Kuruluşları Yönet** **sayfasındaki kuruluş seçeneğine dönüştür** seçeneğini kullanın:

![Varolan bir hesabı bir kuruluşa dönüştürme seçeneği NuGet.org](media/org-transform-option.png)

Sonraki sayfada, kuruluşun yöneticisi olarak atamak için farklı kullanıcı hesabı belirtin ve **dönüştür'ü**seçin.

![Kullanıcı hesabını kuruluşa dönüştürmek için bilgi girme](media/org-transform-page.png)

## <a name="managing-organization-members"></a>Kuruluş üyelerini yönetme

Kuruluş yöneticisi olarak, her üyenin NuGet.org *kullanıcı hesabı adını*sağlayarak üye ekleyebilirsiniz; e-posta adresleri kullanılamaz. Daha sonra her üyeyi aşağıdaki izinlerle ortak çalışan veya yönetici olarak işaretlersiniz:

| İzin | İşbirlikçi | Yönetici |
| --- | --- | --- |
| Kuruluşun paketlerini yönetme<br/>(yeni paketler gönderin, varolan paketleri güncelleyin veya listeyi listeleyin) | Evet | Evet |
| Kuruluş meta verilerini değiştirme<br/>(e-posta adresi, bildirim ayarları) | Hayır | Evet |
| Kuruluş üyelerini yönetme | Hayır | Evet |
| Kuruluş paketleri için ortak sahiplik istekleri ni isteme veya bu konuda hareket etme | Hayır | Evet |

## <a name="managing-packages"></a>Paketleri yönetme

Hesabınızdaki tüm paketleri ve üyesi olduğunuz tüm kuruluşları [Paketleri Yönet](https://www.nuget.org/account/Packages) sayfasında görüntüleyebilirsiniz. Hesabınıza veya belirli bir kuruluşa özgü paketleri görüntülemek için sayfanın sağ üst kısmındaki hesap filtresini kullanın.

![Hesap filtresi ile paketleri yönetme](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>Paketleri kuruluşa aktarma
Paketlerinizin bir kısmını yeni oluşturulan bir kuruluşa aktarmak istiyorsanız, bunu kuruluş hesabından paketin ortak sahibi olmasını isteyerek ve ardından kendinizi sahip olarak kaldırarak yapabilirsiniz. Kuruluşun yöneticisiyseniz, sahipliği kabul etmek için onay gerekmez. Ancak, ortak çalışansanız, kuruluşun sahibi olarak eklenmesi için yöneticilerden birinin sahipliği kabul etmesi şarttır.

## <a name="publishing-packages"></a>Yayımlama paketleri

Paketleri kullanıcı hesabına yayımladığınızdan gibi bir kuruluşa yayımlarsınız: paketi doğrudan NuGet.org yükleyerek veya paketi `nuget push` CLI `dotnet nuget push` komutları aracılığıyla iterek.

### <a name="uploading-packages"></a>Paket yükleme

[NuGet.org Upload](https://www.nuget.org/packages/manage/upload) sayfasına doğrudan yeni bir paket yüklediğinizde, paket sahibini bir kullanıcı veya kuruluş hesabına atarsınız:

![Hesap seçeneği ile paket yükleme](media/org-upload-option.png)

### <a name="using-api-keys"></a>API tuşlarını kullanma

Bir paketi `nuget push` veya `dotnet nuget push` CLI komutları üzerinden itmek için, bu komutlar tarafından gerekli bir API anahtarı almanız gerekir. Ayrıntılar için [bkz.](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)

Yeni bir API anahtarı oluştururken, **Paket Sahibi** açılır durumda uygun kuruluşu seçin. Oluşturduğunuz herhangi bir API anahtarı yalnızca seçilen kuruluş için geçerlidir:

![Hesap seçeneği ile API anahtarı](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>Bir kuruluşu kaldırma

Kullanıcı olarak, kuruluş üyeliğinizin gösterdiği **X** düğmesini seçerek kendinizi kuruluştan kaldırabilirsiniz:

![Kullanıcı hesabını kuruluştan kaldırma](media/org-remove-self-option.png)

Yöneticiler, diğer yöneticiler de dahil olmak üzere herhangi bir üyeyi kuruluştan kaldırabilir. Bir kuruluşun tek yöneticisiyseniz, yönetici olarak başka bir üye eklemediğiniz sürece kendinizi kaldıramazsınız.

### <a name="deleting-an-organization-account"></a>Kuruluş hesabını silme

Kuruluş sayfanızda gösterilen **Sil** düğmesini tıklatarak bir kuruluş hesabını silebilirsiniz.

![Kuruluşu silme](media/org-delete-option.png)

Organizaiton'u silmek için, organizasyon onayını **sil** düğmesini tıklatarak onaylamanız gerekir.
