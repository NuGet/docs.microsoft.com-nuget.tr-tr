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
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="5388f-103">Nuget.org kuruluşunda</span><span class="sxs-lookup"><span data-stu-id="5388f-103">Organization on nuget.org</span></span>

<span data-ttu-id="5388f-104">Kuruluşlar, işletmelerin ve paketleri tek nuget.org kimliğini kullanarak işbirliği yapmak için açık kaynaklı proje etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5388f-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="5388f-105">Bir paket tüketici için bir kuruluş hesabı nuget.org var olan bir kullanıcı hesabı ile aynı görünür.</span><span class="sxs-lookup"><span data-stu-id="5388f-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="5388f-106">Kuruluş hesapları ve kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="5388f-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="5388f-107">Kullanıcı hesabınızın nuget.org kimliğinizi ve kuruluşların herhangi bir sayıda üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="5388f-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="5388f-108">Bir paket, bir kullanıcı hesabına ait olabilir gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="5388f-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="5388f-109">Paket Tüketiciler, bir kullanıcı hesabı veya kuruluş hesabı arasındaki fark görmüyorum: hem paket olarak görünür `owners`.</span><span class="sxs-lookup"><span data-stu-id="5388f-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="5388f-110">Bir kuruluş hesabı bir veya daha fazla kullanıcı hesapları üyeleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5388f-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="5388f-111">Bu üyeler, sahipliği için tek bir kimlik korurken paket kümesini yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5388f-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="5388f-112">Yeni bir kuruluş ekleme</span><span class="sxs-lookup"><span data-stu-id="5388f-112">Adding a new organization</span></span>

<span data-ttu-id="5388f-113">Yeni bir kuruluş eklemek için nuget.org hesabınızdaki seçin, ardından seçin **kuruluşlar Yönet...**  menü komutu:</span><span class="sxs-lookup"><span data-stu-id="5388f-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Nuget.org Yöneticisi kuruluşlar için menü seçeneği](media/org-manage-option.png)

<span data-ttu-id="5388f-115">Sonraki sayfada seçin **yeni bir kuruluş eklemek** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="5388f-115">On the next page, select the **Add new organization** button:</span></span>

![Düğme nuget.org üzerinde yeni bir kuruluş oluşturun](media/org-add-new-option.png)

<span data-ttu-id="5388f-117">Sonraki sayfada kuruluş adı ve e-posta adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="5388f-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="5388f-118">Kullanıcı hesapları aynı ad kuruluş hesaplarında paylaşmak olduğundan, kuruluş adını diğer tüm var olan kuruluş veya kullanıcı hesapları farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5388f-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="5388f-119">E-posta adresi, ayrıca tüm hesapları arasında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5388f-119">The email address must also be unique across all accounts.</span></span>

![Nuget.org üzerinde yeni bir kuruluş sayfa ekleyin](media/org-add-new-page.png)

<span data-ttu-id="5388f-121">Kuruluş hesap oluşturulduktan sonra yönetici ve kuruluş için paketleri göndermek ve kuruluş üye ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5388f-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="5388f-122">Bir kuruluş için mevcut hesap dönüştürme</span><span class="sxs-lookup"><span data-stu-id="5388f-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="5388f-123">Hesap dönüştürme işlemi geri alınamaz: kuruluş bir kullanıcı hesabı için geri dönüştürülemez.</span><span class="sxs-lookup"><span data-stu-id="5388f-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="5388f-124">Paketleri tek bir kullanıcı hesabı kullanarak bir ekip halinde yönetme ve bu hesap bir kuruluşa, kullanım dönüştürmek istiyorsanız **kuruluş hesabınıza dönüştürme** seçeneği **kuruluşlarınyönetme** sayfa:</span><span class="sxs-lookup"><span data-stu-id="5388f-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Var olan bir hesap bir kuruluşa dönüştürmek için nuget.org seçeneği](media/org-transform-option.png)

<span data-ttu-id="5388f-126">Sonraki sayfada kuruluş yöneticisi olarak atayın ve sonra seçmek için farklı bir kullanıcı hesabı belirtin **dönüştürme**.</span><span class="sxs-lookup"><span data-stu-id="5388f-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Bir kuruluş için bir kullanıcı hesabı dönüştürme bilgilerini girme](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="5388f-128">Kuruluş üyeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="5388f-128">Managing organization members</span></span>

<span data-ttu-id="5388f-129">Kuruluş yöneticisi olarak, her üyenin nuget.org sağlayarak üye ekleyebilir *kullanıcı hesabı adı*; e-posta adresleri kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5388f-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="5388f-130">Ardından her üye bir ortak çalışanı veya aşağıdaki izinlere sahip yönetici olarak işaretleyin:</span><span class="sxs-lookup"><span data-stu-id="5388f-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="5388f-131">İzin</span><span class="sxs-lookup"><span data-stu-id="5388f-131">Permission</span></span> | <span data-ttu-id="5388f-132">Ortak çalışanı</span><span class="sxs-lookup"><span data-stu-id="5388f-132">Collaborator</span></span> | <span data-ttu-id="5388f-133">Yönetici</span><span class="sxs-lookup"><span data-stu-id="5388f-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5388f-134">Kuruluşun paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="5388f-134">Manage the organization's packages</span></span><br/><span data-ttu-id="5388f-135">(yeni paketleri göndermek, güncelleştirmek veya var olan paketler unlist)</span><span class="sxs-lookup"><span data-stu-id="5388f-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="5388f-136">Evet</span><span class="sxs-lookup"><span data-stu-id="5388f-136">Yes</span></span> | <span data-ttu-id="5388f-137">Evet</span><span class="sxs-lookup"><span data-stu-id="5388f-137">Yes</span></span> |
| <span data-ttu-id="5388f-138">Değişiklik kuruluş meta verileri</span><span class="sxs-lookup"><span data-stu-id="5388f-138">Change organization metadata</span></span><br/><span data-ttu-id="5388f-139">(e-posta adresi, bildirim ayarları)</span><span class="sxs-lookup"><span data-stu-id="5388f-139">(email address, notification settings)</span></span> | <span data-ttu-id="5388f-140">Hayır</span><span class="sxs-lookup"><span data-stu-id="5388f-140">No</span></span> | <span data-ttu-id="5388f-141">Evet</span><span class="sxs-lookup"><span data-stu-id="5388f-141">Yes</span></span> |
| <span data-ttu-id="5388f-142">Kuruluş üyeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="5388f-142">Manage organization members</span></span> | <span data-ttu-id="5388f-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="5388f-143">No</span></span> | <span data-ttu-id="5388f-144">Evet</span><span class="sxs-lookup"><span data-stu-id="5388f-144">Yes</span></span> |
| <span data-ttu-id="5388f-145">İstek veya kuruluş paketler için co-ownership istekleri hareket</span><span class="sxs-lookup"><span data-stu-id="5388f-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="5388f-146">Hayır</span><span class="sxs-lookup"><span data-stu-id="5388f-146">No</span></span> | <span data-ttu-id="5388f-147">Evet</span><span class="sxs-lookup"><span data-stu-id="5388f-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="5388f-148">Paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="5388f-148">Managing packages</span></span>

<span data-ttu-id="5388f-149">Hesabınızın ve hangisinin kullandığınız üyesi tüm kuruluşlar arasında tüm paketleri görüntüleyebilirsiniz [paketlerini Yönet](https://www.nuget.org/account/Packages) sayfası.</span><span class="sxs-lookup"><span data-stu-id="5388f-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="5388f-150">Belirli bir kuruluş veya hesabınız için belirli paketleri görüntülemek için üst hesapları filtresini kullanma sağ sayfasının.</span><span class="sxs-lookup"><span data-stu-id="5388f-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Hesap filtresiyle paketlerini yönetme](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="5388f-152">Kuruluş için paketler aktarma</span><span class="sxs-lookup"><span data-stu-id="5388f-152">Transferring packages to an organization</span></span>
<span data-ttu-id="5388f-153">Bazı paketlerinizin yeni oluşturulan bir kuruluşa aktarmak istiyorsanız, bunu paket birlikte kendi kuruluş hesabı isteyen ve kendiniz sahibi olarak kaldırarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5388f-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="5388f-154">Kuruluşun bir yöneticiyseniz sahipliği kabul etmek için gerekli onay yok yok.</span><span class="sxs-lookup"><span data-stu-id="5388f-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="5388f-155">Ancak, bir ortak çalışanı varsa, kuruluşunuzun sahibi olarak ekleme sahipliği kabul etmek için Yöneticiler birini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5388f-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="5388f-156">Paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="5388f-156">Publishing packages</span></span>

<span data-ttu-id="5388f-157">Bir kullanıcı hesabına paketleri yayımlama gibi kuruluş için paketleri yayımlama: doğrudan nuget.org için paket yüklemek veya paket Ftp'den `nuget push` veya `dotnet nuget push` CLI komutları.</span><span class="sxs-lookup"><span data-stu-id="5388f-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="5388f-158">Karşıya yükleme paketleri</span><span class="sxs-lookup"><span data-stu-id="5388f-158">Uploading packages</span></span>

<span data-ttu-id="5388f-159">Ne zaman doğrudan karşıya yüklediğiniz yeni bir paket üzerinde [nuget.org karşıya yükleme](https://www.nuget.org/packages/manage/upload) sayfasında atadığınız paket sahibi bir kullanıcı ya da kuruluş hesabı:</span><span class="sxs-lookup"><span data-stu-id="5388f-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Hesap seçeneğiyle paketi yükleme](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="5388f-161">API anahtarları kullanma</span><span class="sxs-lookup"><span data-stu-id="5388f-161">Using API keys</span></span>

<span data-ttu-id="5388f-162">Bir paketi göndermeyi `nuget push` veya `dotnet nuget push` CLI komutları, bu komutları tarafından gerekli bir API anahtarı alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5388f-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="5388f-163">Ayrıntılar için bkz [bir paketi yayımlamaya](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="5388f-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="5388f-164">Yeni bir API anahtarı oluştururken uygun kuruluşta seçin **paket sahibinden** açılır.</span><span class="sxs-lookup"><span data-stu-id="5388f-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="5388f-165">Oluşturduğunuz tüm API anahtarı yalnızca seçilen kuruluşa geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="5388f-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Hesap seçeneğiyle API anahtarı](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="5388f-167">Bir kuruluş kaldırma</span><span class="sxs-lookup"><span data-stu-id="5388f-167">Removing an organization</span></span>

<span data-ttu-id="5388f-168">Bir kullanıcı olarak, kendiniz bir kuruluştan seçerek silebilirsiniz `X` kuruluş üyeliğinizi tarafından gösterilen düğmesi:</span><span class="sxs-lookup"><span data-stu-id="5388f-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Bir kuruluştan bir kullanıcı hesabını kaldırma](media/org-remove-self-option.png)

<span data-ttu-id="5388f-170">Yöneticiler, diğer yöneticiler de dahil olmak üzere kuruluş tarafından herhangi bir üyesi kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="5388f-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="5388f-171">Bir kuruluş için tek Yönetici sizseniz, yönetici olarak başka bir üye eklemek sürece kendiniz kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="5388f-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="5388f-172">Bir kuruluş hesabı silme</span><span class="sxs-lookup"><span data-stu-id="5388f-172">Deleting an organization account</span></span>

<span data-ttu-id="5388f-173">Bu özellik yakında çıkıyor.</span><span class="sxs-lookup"><span data-stu-id="5388f-173">This feature is coming soon.</span></span>
