---
title: NuGet.org’a genel bakış
description: NuGet.org’a genel bakış
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901882"
---
# <a name="overview-of-nugetorg"></a>NuGet.org’a genel bakış

NuGet.org, her gün milyonlarca .NET ve .NET Core geliştiricisi tarafından çalıştırılan NuGet paketlerinin ortak bir ana konağından oluşur.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>NuGet ekosistemindeki NuGet.org rolü

Ortak ana bilgisayar olarak rolünde, NuGet.org, [NuGet.org](https://www.nuget.org)adresinden 100.000 benzersiz paketin üzerinden merkezi depoyu saklar. NuGet.org, paketler için mümkün olan tek konak değildir. NuGet teknolojisi Ayrıca, paketleri bulutta (Azure DevOps gibi), özel bir ağda veya hatta yalnızca yerel dosya sisteminizde barındırmanıza olanak sağlar. Farklı bir konak veya barındırma seçeneği ile ilgileniyorsanız, bkz. [kendi NuGet akışlarınızı barındırma](../hosting-packages/overview.md).

NuGet paketleri için herhangi bir konak gibi NuGet.org, paket *oluşturucular* ve paket *tüketicileri* arasındaki bağlantı noktası olarak görev yapar. Creators Build yararlı NuGet paketleri ve bunları yayımlayın. Müşteriler daha sonra, bu paketleri projelerinde, indirerek ve dahil olmak üzere erişilebilir konaklarda kullanışlı ve uyumlu paketler arar. Bir projeye yüklendikten sonra paketlerin API 'Leri proje kodunun geri kalanı tarafından kullanılabilir.

![Paket oluşturucular, paket konakları ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="accounts"></a>Hesaplar

Paketleri NuGet.org üzerinde yayımlamak için önce bir [bireysel (Kullanıcı) hesabı](individual-accounts.md)oluşturursunuz. Bu, NuGet.org adresindeki kimliğiniz olur.

NuGet.org Ayrıca, bir [kuruluş hesabı](organizations-on-nuget-org.md)oluşturmanıza de olanak tanır. Bir kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel hesabı vardır. Üyeler, sahiplik için tek bir kimliği koruyarak bir paket kümesini yönetebilir. Bireysel hesabınız sayesinde, herhangi bir sayıda kuruluşun üyesi olabilirsiniz.

Bir paket, tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir. Paket tüketicileri, tek bir hesap veya kuruluş hesabı arasında herhangi bir farklılık görmez: her ikisi de paket olarak görünürler `owners` .

## <a name="api-keys"></a>API anahtarları

Yayımlamak üzere bir NuGet paketine (*. nupkg* dosyası) sahip olduktan sonra, NuGet.org ' den elde edilen bir [API anahtarı](scoped-api-keys.md) ile birlikte nuget.exe CLI veya dotnet.exe CLI kullanarak bunu NuGet.org olarak yayımlayabilirsiniz.

[Bir paket yayımladığınızda](../create-packages/creating-a-package.md), CLı komutuna API anahtarı değerini dahil edersiniz.

## <a name="id-prefixes"></a>KIMLIK önekleri

Paketleri yayımladığınızda kimlik [öneklerini](id-prefix-reservation.md)ayırarak kimliğinizi ayırabilir ve koruyabilirsiniz. Paket yüklerken, paket tüketicileri, kullandıkları paketin kendi tanımlama özelliklerinde yanıltıcı olmadığını belirten ek bilgilerle sağlanır.

## <a name="api-endpoint-for-nugetorg"></a>NuGet.org için API uç noktası

NuGet.org 'i NuGet istemcilerinde bir paket deposu olarak kullanmak için aşağıdaki v3 API uç noktasını kullanmanız gerekir: 

`https://api.nuget.org/v3/index.json`

Daha eski istemciler NuGet.org ulaşmak için v2 protokolünü kullanmaya devam edebilir. Ancak, bkz. NuGet istemcileri 3,0 veya üzeri, v2 protokolünü kullanarak daha yavaş ve daha az güvenilir hizmete sahip olacaktır:

`https://www.nuget.org/api/v2` (**V2 Protokolü kullanım dışıdır!**)
