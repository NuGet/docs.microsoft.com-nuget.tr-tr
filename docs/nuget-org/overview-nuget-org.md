---
title: NuGet.org’a genel bakış
description: NuGet.org’a genel bakış
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427523"
---
# <a name="overview-of-nugetorg"></a>NuGet.org’a genel bakış

NuGet.org, her gün milyonlarca .NET ve .NET Core geliştiricisi tarafından kullanılan NuGet paketlerinin genel ev sahibidir.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet ekosisteminde NuGet.org rolü

Bir kamu ev sahibi olarak rolünde, NuGet.org kendisi [nuget.org](https://www.nuget.org)100.000'den fazla benzersiz paketlerin merkezi deposu tutar. NuGet.org paketler için tek olası ana bilgisayar değildir. NuGet teknolojisi ayrıca paketleri bulutta (Azure DevOps'lerde gibi) özel olarak, özel bir ağda ve hatta yalnızca yerel dosya sisteminizde barındırmanıza olanak tanır. Farklı bir ev sahibi veya barındırma seçeneğiyle ilgileniyorsanız, [kendi NuGet akışlarınızı barındırma](../hosting-packages/overview.md)ya da barındırma bakın.

NuGet.org, NuGet paketleri için herhangi bir ana bilgisayar gibi, paket *yaratıcıları* ve paket *tüketiciler*arasında bağlantı noktası olarak hizmet vermektedir. İçerik oluşturucular yararlı NuGet paketleri oluşturur ve bunları yayımlar. Tüketiciler daha sonra erişilebilir ana bilgisayarlarda, bu paketleri indirirken ve projelerine dahil ederek kullanışlı ve uyumlu paketleri ararlar. Bir projeye yüklendikten sonra, paketlerin API'leri proje kodunun geri kalanı için kullanılabilir.

![Paket oluşturucular, paket ana bilgisayarlar ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="accounts"></a>Hesaplar

Paketleri NuGet.org yayınlamak için önce [bir bireysel (kullanıcı) hesabı](individual-accounts.md)oluşturursunuz. Bu NuGet.org üzerinde kimliğiniz olur.

NuGet.org ayrıca bir [kuruluş hesabı](organizations-on-nuget-org.md)oluşturmanıza da olanak sağlar. Kuruluş hesabının üyeleri olarak bir veya daha fazla ayrı hesabı vardır. Üyeler, sahiplik için tek bir kimlik korurken bir dizi paketi yönetebilir. Bireysel hesabınız aracılığıyla, herhangi bir sayıda kuruluşun üyesi olabilirsiniz.

Paket, tek bir hesaba ait olduğu gibi bir kuruluş hesabına ait olabilir. Paket tüketicileri tek bir hesap la kuruluş hesabı arasında herhangi `owners`bir fark görmezler: her ikisi de paket olarak görünür.

## <a name="api-keys"></a>API anahtarları

Bir kez bir NuGet paketi *(.nupkg* dosyası) yayınlamak için, NuGet.org edinilen bir [API anahtarı](scoped-api-keys.md) ile birlikte nuget.exe CLI veya dotnet.exe CLI kullanarak NuGet.org yayımlamak.

Bir [paket yayımladığınızda,](../create-packages/creating-a-package.md)CLI komutuna API anahtar değerini eklersiniz.

## <a name="id-prefixes"></a>Kimlik önekleri

Paketleri yayımladığınızda, [kimlik önekleri ayırarak](id-prefix-reservation.md)kimliğinizi rezerve edebilir ve koruyabilirsiniz. Paket yüklerken, paket tüketicilerine tükettikleri paketin tanımlayıcı özelliklerinde aldatıcı olmadığını belirten ek bilgiler verilir.

## <a name="api-endpoint-for-nugetorg"></a>NuGet.org için API bitiş noktası

NuGet.org NuGet istemcileriyle paket deposu olarak kullanmak için aşağıdaki V3 API bitiş noktasını kullanmanız gerekir: 

`https://api.nuget.org/v3/index.json`

Eski istemciler hala NuGet.org ulaşmak için V2 protokolünü kullanabilirsiniz. Ancak, lütfen unutmayın, NuGet istemcileri 3.0 veya daha sonra V2 protokolü kullanarak daha yavaş ve daha az güvenilir hizmet olacaktır:

`https://www.nuget.org/api/v2`(**V2 prototcol azat edilir!**)
