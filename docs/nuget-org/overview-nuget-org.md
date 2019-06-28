---
title: NuGet.org genel bakış
description: NuGet.org genel bakış
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427523"
---
# <a name="overview-of-nugetorg"></a>NuGet.org genel bakış

NuGet.org, her gün çalışan NuGet paketlerinin milyonlarca .NET ve .NET Core geliştiricileri tarafından ortak bir ana bilgisayardır.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet.org rolünde NuGet ekosistemi

Ortak bir konak olarak kendi rolünde merkezi depo 100. 000'den benzersiz paket NuGet.org kendisi tutar [nuget.org](https://www.nuget.org). NuGet.org paketler için yalnızca ana bilgisayar değil. NuGet teknoloji Ayrıca, özel olarak bulutta paketlerini barındıracak sağlar (gibi Azure DevOps üzerine), özel bir ağda veya hatta yalnızca yerel dosya sisteminize. Bir farklı bir konak ya da barındırma seçeneği ilgileniyorsanız bkz [kendi NuGet akışlarınızı barındırma](../hosting-packages/overview.md).

NuGet.org, NuGet paketleri için herhangi bir ana bilgisayara gibi hizmet paketi arasında bir bağlantı noktası olarak *creators* ve paket *tüketiciler*. Creators yararlı NuGet paketleri oluşturun ve yayımlayın. Tüketiciler kullanışlı ve uyumlu paketleri indirme ve bu paketleri, projelere dahil etme erişilebilen konaklarda öğesini arayın. Bir projede yüklendikten sonra paketleri API'leri proje kodunu geri kalanı için kullanılabilir.

![Paket oluşturucuları, paket konaklar ve paketi tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="accounts"></a>Hesaplar

Paketleri NuGet.org üzerinde yayımlamak için önce oluşturduğunuz bir [tek (kullanıcı) hesabı](individual-accounts.md). Bu, kimliğinizi nuget.org olur.

NuGet.org ayrıca oluşturmanıza imkan tanır bir [kuruluş hesabı](organizations-on-nuget-org.md). Bir kuruluş hesabı, bir veya daha fazla bireysel hesaplar, üyelere sahiptir. Üyeleri paketleri bir dizi sahipliği için tek bir kimlik korurken yönetebilir. Kişisel hesabınıza kuruluşların herhangi bir sayıda üyesi olabilir.

Bir paketi tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir. Paketi tüketicileri bir bireysel hesabı veya kuruluş hesabı arasındaki fark görmüyorum: her ikisi de paketi olarak görünen `owners`.

## <a name="api-keys"></a>API anahtarları

Bir NuGet paketini aldıktan sonra ( *.nupkg* dosya) yayımlamak için nuget.org'da nuget.exe CLI veya dotnet.exe CLI ile birlikte kullanarak yayımladığınız bir [API anahtarı](scoped-api-keys.md) NuGet.org adresinden alınan.

Olduğunda, [paket yayımlama](../create-packages/creating-a-package.md), CLI komutu API anahtar değeri içerir.

## <a name="id-prefixes"></a>Kimlik ön ekleri

Paketleri yayımladığınızda, ayırabilir ve tarafından kimliğinizi korumak [kimliği ön ekleri ayırma](id-prefix-reservation.md). Bir paketi yüklerken paketi tüketicileri tüketen paket tanımlayıcı özelliklerini aldatıcı olmadığını belirten ek bilgiler sağlanır.

## <a name="api-endpoint-for-nugetorg"></a>NuGet.org için API uç noktası

NuGet.org bir paket deposu NuGet istemcileri ile kullanmak için aşağıdaki V3 API uç noktası kullanmanız gerekir: 

`https://api.nuget.org/v3/index.json`

Eski istemciler V2 Protokolü NuGet.org ulaşmak için kullanmaya devam edebilirsiniz. Ancak, lütfen unutmayın, NuGet 3.0 veya üstü istemcilerin daha yavaş ve V2 protokolünü kullanarak güvenilir hizmet daha az olacaktır:

`https://www.nuget.org/api/v2` (**V2 iletişim kuralı kullanım dışı!** )
