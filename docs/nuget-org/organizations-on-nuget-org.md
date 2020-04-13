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
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="f8a1b-103">NuGet.org'daki kuruluşunuz</span><span class="sxs-lookup"><span data-stu-id="f8a1b-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="f8a1b-104">Kuruluşlar, işletmelerin ve açık kaynak projelerinin tek bir NuGet.org kimliği kullanarak paketler üzerinde işbirliği yapmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="f8a1b-105">Paket tüketicisi için, bir kuruluş hesabı NuGet.org'daki varolan bir kullanıcı hesabıyla aynı görünür.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="f8a1b-106">Kuruluş hesapları ve bireysel hesaplar</span><span class="sxs-lookup"><span data-stu-id="f8a1b-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="f8a1b-107">Kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel (kullanıcı) hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="f8a1b-108">Bu üyeler, sahiplik için tek bir kimlik korurken bir dizi paketi yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="f8a1b-109">Bireysel hesabınız NuGet.org'daki kimliğinizdir ve herhangi bir sayıda kuruluşun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="f8a1b-110">Paket, tek bir hesaba ait olduğu gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="f8a1b-111">Paket tüketicileri tek bir hesap la kuruluş hesabı arasında herhangi `owners`bir fark görmezler: her ikisi de paket olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="f8a1b-112">Yeni bir kuruluş ekleme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-112">Adding a new organization</span></span>

<span data-ttu-id="f8a1b-113">Yeni bir kuruluş eklemek için NuGet.org hesabınızı seçin ve ardından **Kuruluşları Yönet...** menü komutunu seçin:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Yönetici Organizasyonlar için NuGet.org menü seçeneği](media/org-manage-option.png)

<span data-ttu-id="f8a1b-115">Bir sonraki sayfada **yeni kuruluş ekle** düğmesini seçin:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-115">On the next page, select the **Add new organization** button:</span></span>

![NuGet.org yeni bir kuruluş oluşturmak için düğme](media/org-add-new-option.png)

<span data-ttu-id="f8a1b-117">Bir sonraki sayfada, kuruluş adını ve e-posta adresini girin.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="f8a1b-118">Kuruluş hesapları kullanıcı hesaplarıyla aynı ad alanını paylaştığından, kuruluş adı diğer varolan kuruluş veya kullanıcı hesaplarından farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="f8a1b-119">E-posta adresi de tüm hesaplar arasında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-119">The email address must also be unique across all accounts.</span></span>

![NuGet.org yeni kuruluş sayfası ekleme](media/org-add-new-page.png)

<span data-ttu-id="f8a1b-121">Kuruluş hesabı oluşturulduktan sonra yönetici sizsiniz ve kuruluş için paketler gönderebilir ve kuruluş üyeleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="f8a1b-122">Varolan hesabı bir kuruluşa dönüştürme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="f8a1b-123">Hesap dönüştürme geri alınamaz: Bir kuruluşu kullanıcı hesabına dönüştüremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="f8a1b-124">Paketleri tek bir kullanıcı hesabı kullanarak ekip olarak yönetiyorsanız ve bu hesabı bir kuruluşa dönüştürmek istiyorsanız, Hesabınızı **Kuruluşları Yönet** **sayfasındaki kuruluş seçeneğine dönüştür** seçeneğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Varolan bir hesabı bir kuruluşa dönüştürme seçeneği NuGet.org](media/org-transform-option.png)

<span data-ttu-id="f8a1b-126">Sonraki sayfada, kuruluşun yöneticisi olarak atamak için farklı kullanıcı hesabı belirtin ve **dönüştür'ü**seçin.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Kullanıcı hesabını kuruluşa dönüştürmek için bilgi girme](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="f8a1b-128">Kuruluş üyelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-128">Managing organization members</span></span>

<span data-ttu-id="f8a1b-129">Kuruluş yöneticisi olarak, her üyenin NuGet.org *kullanıcı hesabı adını*sağlayarak üye ekleyebilirsiniz; e-posta adresleri kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="f8a1b-130">Daha sonra her üyeyi aşağıdaki izinlerle ortak çalışan veya yönetici olarak işaretlersiniz:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="f8a1b-131">İzin</span><span class="sxs-lookup"><span data-stu-id="f8a1b-131">Permission</span></span> | <span data-ttu-id="f8a1b-132">İşbirlikçi</span><span class="sxs-lookup"><span data-stu-id="f8a1b-132">Collaborator</span></span> | <span data-ttu-id="f8a1b-133">Yönetici</span><span class="sxs-lookup"><span data-stu-id="f8a1b-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8a1b-134">Kuruluşun paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-134">Manage the organization's packages</span></span><br/><span data-ttu-id="f8a1b-135">(yeni paketler gönderin, varolan paketleri güncelleyin veya listeyi listeleyin)</span><span class="sxs-lookup"><span data-stu-id="f8a1b-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="f8a1b-136">Evet</span><span class="sxs-lookup"><span data-stu-id="f8a1b-136">Yes</span></span> | <span data-ttu-id="f8a1b-137">Evet</span><span class="sxs-lookup"><span data-stu-id="f8a1b-137">Yes</span></span> |
| <span data-ttu-id="f8a1b-138">Kuruluş meta verilerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-138">Change organization metadata</span></span><br/><span data-ttu-id="f8a1b-139">(e-posta adresi, bildirim ayarları)</span><span class="sxs-lookup"><span data-stu-id="f8a1b-139">(email address, notification settings)</span></span> | <span data-ttu-id="f8a1b-140">Hayır</span><span class="sxs-lookup"><span data-stu-id="f8a1b-140">No</span></span> | <span data-ttu-id="f8a1b-141">Evet</span><span class="sxs-lookup"><span data-stu-id="f8a1b-141">Yes</span></span> |
| <span data-ttu-id="f8a1b-142">Kuruluş üyelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-142">Manage organization members</span></span> | <span data-ttu-id="f8a1b-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="f8a1b-143">No</span></span> | <span data-ttu-id="f8a1b-144">Evet</span><span class="sxs-lookup"><span data-stu-id="f8a1b-144">Yes</span></span> |
| <span data-ttu-id="f8a1b-145">Kuruluş paketleri için ortak sahiplik istekleri ni isteme veya bu konuda hareket etme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="f8a1b-146">Hayır</span><span class="sxs-lookup"><span data-stu-id="f8a1b-146">No</span></span> | <span data-ttu-id="f8a1b-147">Evet</span><span class="sxs-lookup"><span data-stu-id="f8a1b-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="f8a1b-148">Paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-148">Managing packages</span></span>

<span data-ttu-id="f8a1b-149">Hesabınızdaki tüm paketleri ve üyesi olduğunuz tüm kuruluşları [Paketleri Yönet](https://www.nuget.org/account/Packages) sayfasında görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="f8a1b-150">Hesabınıza veya belirli bir kuruluşa özgü paketleri görüntülemek için sayfanın sağ üst kısmındaki hesap filtresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Hesap filtresi ile paketleri yönetme](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="f8a1b-152">Paketleri kuruluşa aktarma</span><span class="sxs-lookup"><span data-stu-id="f8a1b-152">Transferring packages to an organization</span></span>
<span data-ttu-id="f8a1b-153">Paketlerinizin bir kısmını yeni oluşturulan bir kuruluşa aktarmak istiyorsanız, bunu kuruluş hesabından paketin ortak sahibi olmasını isteyerek ve ardından kendinizi sahip olarak kaldırarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="f8a1b-154">Kuruluşun yöneticisiyseniz, sahipliği kabul etmek için onay gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="f8a1b-155">Ancak, ortak çalışansanız, kuruluşun sahibi olarak eklenmesi için yöneticilerden birinin sahipliği kabul etmesi şarttır.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="f8a1b-156">Yayımlama paketleri</span><span class="sxs-lookup"><span data-stu-id="f8a1b-156">Publishing packages</span></span>

<span data-ttu-id="f8a1b-157">Paketleri kullanıcı hesabına yayımladığınızdan gibi bir kuruluşa yayımlarsınız: paketi doğrudan NuGet.org yükleyerek veya paketi `nuget push` CLI `dotnet nuget push` komutları aracılığıyla iterek.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="f8a1b-158">Paket yükleme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-158">Uploading packages</span></span>

<span data-ttu-id="f8a1b-159">[NuGet.org Upload](https://www.nuget.org/packages/manage/upload) sayfasına doğrudan yeni bir paket yüklediğinizde, paket sahibini bir kullanıcı veya kuruluş hesabına atarsınız:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Hesap seçeneği ile paket yükleme](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="f8a1b-161">API tuşlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="f8a1b-161">Using API keys</span></span>

<span data-ttu-id="f8a1b-162">Bir paketi `nuget push` veya `dotnet nuget push` CLI komutları üzerinden itmek için, bu komutlar tarafından gerekli bir API anahtarı almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="f8a1b-163">Ayrıntılar için [bkz.](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)</span><span class="sxs-lookup"><span data-stu-id="f8a1b-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="f8a1b-164">Yeni bir API anahtarı oluştururken, **Paket Sahibi** açılır durumda uygun kuruluşu seçin.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="f8a1b-165">Oluşturduğunuz herhangi bir API anahtarı yalnızca seçilen kuruluş için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Hesap seçeneği ile API anahtarı](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="f8a1b-167">Bir kuruluşu kaldırma</span><span class="sxs-lookup"><span data-stu-id="f8a1b-167">Removing an organization</span></span>

<span data-ttu-id="f8a1b-168">Kullanıcı olarak, kuruluş üyeliğinizin gösterdiği **X** düğmesini seçerek kendinizi kuruluştan kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8a1b-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Kullanıcı hesabını kuruluştan kaldırma](media/org-remove-self-option.png)

<span data-ttu-id="f8a1b-170">Yöneticiler, diğer yöneticiler de dahil olmak üzere herhangi bir üyeyi kuruluştan kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="f8a1b-171">Bir kuruluşun tek yöneticisiyseniz, yönetici olarak başka bir üye eklemediğiniz sürece kendinizi kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="f8a1b-172">Kuruluş hesabını silme</span><span class="sxs-lookup"><span data-stu-id="f8a1b-172">Deleting an organization account</span></span>

<span data-ttu-id="f8a1b-173">Kuruluş sayfanızda gösterilen **Sil** düğmesini tıklatarak bir kuruluş hesabını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Kuruluşu silme](media/org-delete-option.png)

<span data-ttu-id="f8a1b-175">Organizaiton'u silmek için, organizasyon onayını **sil** düğmesini tıklatarak onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8a1b-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
