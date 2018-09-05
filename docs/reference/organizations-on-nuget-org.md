---
title: Nuget.org üzerindeki kuruluşlar
description: Nuget.org üzerindeki kuruluşlar şirket ortamı bir takım veya grup tarafından yayımlanmış paketleri yönetmenize yardımcı olur.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551234"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="ff990-103">Nuget.org kuruluş</span><span class="sxs-lookup"><span data-stu-id="ff990-103">Organization on nuget.org</span></span>

<span data-ttu-id="ff990-104">Kuruluşlar, işletmelerin ve açık kaynaklı projelerin paketleri nuget.org tek kimlik kullanarak işbirliği yapmak için etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ff990-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="ff990-105">Bir paket kullanıcısı için bir kuruluş hesabı nuget.org üzerinde var olan bir kullanıcı hesabı ile aynı görünür.</span><span class="sxs-lookup"><span data-stu-id="ff990-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="ff990-106">Kuruluş hesapları ve kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="ff990-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="ff990-107">Kullanıcı hesabınızın kimliğinizi nuget.org ve kuruluşların herhangi bir sayıda üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff990-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="ff990-108">Bir paket, bir kullanıcı hesabına ait olabilir gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff990-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="ff990-109">Paketi tüketicileri bir kullanıcı hesabı veya kuruluş hesabı arasındaki fark görmüyorum: her ikisi de paketi olarak görünen `owners`.</span><span class="sxs-lookup"><span data-stu-id="ff990-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="ff990-110">Bir kuruluş hesabı bir veya daha fazla kullanıcı hesabı, üyelere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ff990-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="ff990-111">Bu üyeleri, sahipliği için tek bir kimlik korurken bir dizi paketleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff990-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="ff990-112">Yeni kuruluş ekleniyor</span><span class="sxs-lookup"><span data-stu-id="ff990-112">Adding a new organization</span></span>

<span data-ttu-id="ff990-113">Yeni bir kuruluş eklemek için nuget.org hesabınızı seçin ve ardından **kuruluşlar Yönet...**  menü komutu:</span><span class="sxs-lookup"><span data-stu-id="ff990-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Nuget.org Manager kuruluşlar için menü seçeneği](media/org-manage-option.png)

<span data-ttu-id="ff990-115">Sonraki sayfada seçin **yeni kuruluş Ekle** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="ff990-115">On the next page, select the **Add new organization** button:</span></span>

![Nuget.org yeni bir kuruluş oluşturmak için](media/org-add-new-option.png)

<span data-ttu-id="ff990-117">Sonraki sayfada kuruluş adı ve e-posta adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="ff990-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="ff990-118">Kullanıcı hesapları olarak aynı ad kuruluş hesapları paylaşma olduğundan, kuruluş adını diğer tüm mevcut kuruluş veya kullanıcı hesapları farklı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff990-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="ff990-119">E-posta adresi, ayrıca tüm hesapları arasında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff990-119">The email address must also be unique across all accounts.</span></span>

![Nuget.org yeni bir kuruluş sayfası ekleyin](media/org-add-new-page.png)

<span data-ttu-id="ff990-121">Kuruluş hesabı oluşturulduktan sonra yönetici kuruluş için paketleri göndermek ve kuruluş üyeleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff990-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="ff990-122">Var olan bir kuruluş hesabına dönüştürme</span><span class="sxs-lookup"><span data-stu-id="ff990-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="ff990-123">Hesap dönüştürme bir işlemdir: bir kuruluş için bir kullanıcı hesabı için bir geri dönüştürülemez.</span><span class="sxs-lookup"><span data-stu-id="ff990-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="ff990-124">Paketleri tek bir kullanıcı hesabı kullanarak bir takım olarak yönettiğiniz ve bu hesabı bir kuruluşa, kullanım dönüştürmek istiyorsanız **kuruluş hesabınıza dönüştürme** seçeneğini **kuruluşlaryönetme** sayfası:</span><span class="sxs-lookup"><span data-stu-id="ff990-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Nuget.org seçeneği var olan bir kuruluş hesabına dönüştürmek için](media/org-transform-option.png)

<span data-ttu-id="ff990-126">Sonraki sayfada, kuruluş yöneticisi olarak atamak ve ardından farklı bir kullanıcı hesabı belirtmek **dönüştürme**.</span><span class="sxs-lookup"><span data-stu-id="ff990-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Bir kuruluş için bir kullanıcı hesabı dönüştürme bilgileri girme](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="ff990-128">Kuruluş üyeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="ff990-128">Managing organization members</span></span>

<span data-ttu-id="ff990-129">Kuruluş yöneticisi olarak, her üyenin nuget.org sağlayarak üyeler ekleyebilirsiniz *kullanıcı hesabı adı*; e-posta adresleri kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="ff990-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="ff990-130">Ardından her üye bir ortak çalışanı veya aşağıdaki izinlere sahip yönetici olarak işaretleyin:</span><span class="sxs-lookup"><span data-stu-id="ff990-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="ff990-131">İzin</span><span class="sxs-lookup"><span data-stu-id="ff990-131">Permission</span></span> | <span data-ttu-id="ff990-132">Ortak çalışanı</span><span class="sxs-lookup"><span data-stu-id="ff990-132">Collaborator</span></span> | <span data-ttu-id="ff990-133">Yönetici</span><span class="sxs-lookup"><span data-stu-id="ff990-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ff990-134">Kuruluşun paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="ff990-134">Manage the organization's packages</span></span><br/><span data-ttu-id="ff990-135">(yeni bir paket gönderin, güncelleştirmek veya mevcut paketlerini listeden Kaldır)</span><span class="sxs-lookup"><span data-stu-id="ff990-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="ff990-136">Evet</span><span class="sxs-lookup"><span data-stu-id="ff990-136">Yes</span></span> | <span data-ttu-id="ff990-137">Evet</span><span class="sxs-lookup"><span data-stu-id="ff990-137">Yes</span></span> |
| <span data-ttu-id="ff990-138">Değişiklik kuruluş meta verileri</span><span class="sxs-lookup"><span data-stu-id="ff990-138">Change organization metadata</span></span><br/><span data-ttu-id="ff990-139">(e-posta adresi, bildirim ayarları)</span><span class="sxs-lookup"><span data-stu-id="ff990-139">(email address, notification settings)</span></span> | <span data-ttu-id="ff990-140">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff990-140">No</span></span> | <span data-ttu-id="ff990-141">Evet</span><span class="sxs-lookup"><span data-stu-id="ff990-141">Yes</span></span> |
| <span data-ttu-id="ff990-142">Kuruluş üyelerini Yönet</span><span class="sxs-lookup"><span data-stu-id="ff990-142">Manage organization members</span></span> | <span data-ttu-id="ff990-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff990-143">No</span></span> | <span data-ttu-id="ff990-144">Evet</span><span class="sxs-lookup"><span data-stu-id="ff990-144">Yes</span></span> |
| <span data-ttu-id="ff990-145">İstek veya kuruluş paketleri co-ownership isteklerinde ile harekete geçme</span><span class="sxs-lookup"><span data-stu-id="ff990-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="ff990-146">Hayır</span><span class="sxs-lookup"><span data-stu-id="ff990-146">No</span></span> | <span data-ttu-id="ff990-147">Evet</span><span class="sxs-lookup"><span data-stu-id="ff990-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="ff990-148">Paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="ff990-148">Managing packages</span></span>

<span data-ttu-id="ff990-149">Hesabınızı ve hangi kullandığınız üyesi tüm kuruluşlar arasında tüm paketleri görüntüleyebilirsiniz [paketlerini Yönet](https://www.nuget.org/account/Packages) sayfası.</span><span class="sxs-lookup"><span data-stu-id="ff990-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="ff990-150">Hesabınız veya belirli kuruluşlarla özgü paketleri görüntülemek için üst kısımdaki hesapları filtreyi kullanın sayfanın sağ.</span><span class="sxs-lookup"><span data-stu-id="ff990-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Hesap filtreyle paketlerini yönetme](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="ff990-152">Bir kuruluş için paketleri aktarma</span><span class="sxs-lookup"><span data-stu-id="ff990-152">Transferring packages to an organization</span></span>
<span data-ttu-id="ff990-153">Yeni oluşturulan bir kuruluş bazı paketlerinizi aktarmak istiyorsanız, kuruluş hesabı paket birlikte kendi isteyen ve ardından kendiniz sahibi olarak kaldırarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff990-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="ff990-154">Kuruluşun bir yöneticiyseniz sahipliği kabul etmek için gerekli bir onay yok yoktur.</span><span class="sxs-lookup"><span data-stu-id="ff990-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="ff990-155">Ancak, bir ortak çalışanı varsa, sahibi olarak kuruluş ekleme sahipliği kabul etmek için Yöneticiler birini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ff990-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="ff990-156">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="ff990-156">Publishing packages</span></span>

<span data-ttu-id="ff990-157">Bir kullanıcı hesabına paketleri gibi bir kuruluşa paketlerini Yayımla: doğrudan nuget.org için paket yüklemek veya paket gönderme `nuget push` veya `dotnet nuget push` CLI komutları.</span><span class="sxs-lookup"><span data-stu-id="ff990-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="ff990-158">Paket karşıya yükleniyor</span><span class="sxs-lookup"><span data-stu-id="ff990-158">Uploading packages</span></span>

<span data-ttu-id="ff990-159">Karşıya yüklerken, doğrudan yeni bir paket üzerinde [nuget.org karşıya yükleme](https://www.nuget.org/packages/manage/upload) sayfasında, atadığınız paket sahibi bir kullanıcı veya kuruluş hesabı:</span><span class="sxs-lookup"><span data-stu-id="ff990-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Hesap seçeneği ile paketini karşıya yükleyin](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="ff990-161">API anahtarları kullanma</span><span class="sxs-lookup"><span data-stu-id="ff990-161">Using API keys</span></span>

<span data-ttu-id="ff990-162">Bir paket göndermeyi `nuget push` veya `dotnet nuget push` CLI komutları, bu komutlar tarafından gereken bir API anahtarı alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff990-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="ff990-163">Ayrıntılar için bkz [paket yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="ff990-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="ff990-164">Yeni bir API anahtarı oluştururken, uygun kuruluştaki seçin **paket sahibinden** açılır.</span><span class="sxs-lookup"><span data-stu-id="ff990-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="ff990-165">Oluşturduğunuz herhangi bir API anahtarı yalnızca seçilen kuruluş için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="ff990-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Hesap seçeneği sahip API anahtarı](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="ff990-167">Bir kuruluş kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="ff990-167">Removing an organization</span></span>

<span data-ttu-id="ff990-168">Bir kullanıcı olarak, kendiniz bir kuruluştan seçerek kaldırabilirsiniz `X` kuruluş üyeliğinizin tarafından gösterilen düğmesi:</span><span class="sxs-lookup"><span data-stu-id="ff990-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Bir kuruluştan bir kullanıcı hesabı kaldırma](media/org-remove-self-option.png)

<span data-ttu-id="ff990-170">Yöneticiler, diğer yöneticiler dahil kuruluştan herhangi bir üyesi kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="ff990-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="ff990-171">Tek bir kuruluş yöneticisi değilseniz, başka bir üyesi bir yönetici eklemediğiniz sürece kendiniz kaldırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="ff990-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="ff990-172">Bir kuruluş hesabı siliniyor</span><span class="sxs-lookup"><span data-stu-id="ff990-172">Deleting an organization account</span></span>

<span data-ttu-id="ff990-173">Bu özellik yakında kullanıma sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff990-173">This feature is coming soon.</span></span>
