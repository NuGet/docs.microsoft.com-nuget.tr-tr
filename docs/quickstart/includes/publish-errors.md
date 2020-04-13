---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496004"
---
<span data-ttu-id="0f681-101">Komuttaki `push` hatalar genellikle sorunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f681-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="0f681-102">Örneğin, projenizdeki sürüm numarasını güncelleştirmeyi unutmuş olabilirsiniz ve bu nedenle zaten var olan bir paketi yayımlamaya çalışıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="0f681-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="0f681-103">Ayrıca, ana bilgisayarda zaten var olan bir tanımlayıcıyı kullanarak bir paketi yayımlamaya çalışırken de hatalar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0f681-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="0f681-104">Adı "AppLogger", örneğin, zaten var.</span><span class="sxs-lookup"><span data-stu-id="0f681-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="0f681-105">Böyle bir durumda, `push` komut aşağıdaki hatayı verir:</span><span class="sxs-lookup"><span data-stu-id="0f681-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="0f681-106">Yeni oluşturduğunuz geçerli bir API anahtarı kullanıyorsanız, bu ileti hatanın "izin" kısmından tamamen açık olmayan bir adlandırma çakışması gösterir.</span><span class="sxs-lookup"><span data-stu-id="0f681-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="0f681-107">Paket tanımlayıcısını değiştirin, projeyi yeniden oluşturun, `.nupkg` dosyayı yeniden `push` oluşturun ve komutu yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="0f681-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>