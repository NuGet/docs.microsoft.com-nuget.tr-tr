---
title: Kullanıcı veri istekleri
description: Kullanıcı verileri isteyen ilkeleri dışarı aktarma ve silin
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33086219"
---
# <a name="user-data-requests"></a>Kullanıcı veri istekleri

nuget.org kullanıcılar bilgi delete isteklerini ve yanıtlarını bilgileri verme aracılığıyla gönderebilir [nuget.org](https://www.nuget.org). Her iki tür destek biçiminde gönderilen istekleri ve bu yürütülebilir nuget.org yöneticiler tarafından 30 gün içinde.

Aşağıdaki kullanıcı verilerini nuget.org doğrudan erişilebilir.

* E-posta adresi, oturum açma hesabı, profil resmi ve e-posta bildirim ayarları gibi veri hesabıyla ilgili
* Ait API anahtarları
* Sahibi olan paketlerin listesini

Bu verileri destek isteği verilen verileri bulunmamaktadır.

## <a name="identifying-customer-data"></a>Müşteri verileri tanımlama

Müşteri verileri nuget.org kullanıcı hesabı adları tanımlanabilir.

## <a name="deleting-customer-data"></a>Müşteri verileri silme

Nuget.org silme kullanıcı verilerini istemek için:

1. Kullanıcı oturumu için açma gerekir [nuget.org](https://www.nuget.org)
1. Kullanıcı hesaplarında silinmesi için bir istek göndermelisiniz [nuget.org/account/delete](https://www.nuget.org/account/delete)

Paketleri tek sahipleri olan kullanıcılar, silinen kendi hesabınız için onay isteyen önce yeni sahipleri bulmak için önerilir. Paket sahipliği aktarılmayan ise NuGet paketi listelenmemiş olur ve sonuç olarak, artık Visual Studio veya nuget.org Web sitesinde arama sorgularında kullanılabilir değildir. Hesabı silmeden önce oldukları paketleri yeni sahipleri bulmak için kullanıcıyla nuget.org Yöneticiler çalışır.

Hesap silme eylemi nuget.org yönetici tarafından istek tarihten itibaren 30 gün içinde tamamlanır.

Hesap silme, üzerine kullanıcının verilerin tümü olduğu kaldırılması nuget.org sistemden ve şu işlemler uygulanır:

* Silinen hesap ile nuget.org kaydı olur
* Tüm API anahtarları silinmiş ait
* Tüm ayrılmış ad alanlarından yayımlanan
* Tüm paket sahipliği kaldırılır

Ait paketleri *değil* silindi. Listede bulunmayan Arama sonuçlarından rağmen bunlara bağımlı projeleri için paket geri yüklemesi aracılığıyla kullanılabilen kalırlar.

## <a name="exporting-customer-data"></a>Müşteri verileri dışarı aktarma

Oturum açma işleminden sonra nuget.org için bir kullanıcı bir dışarı aktarma isteği aracılığıyla gönderebilirsiniz [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Verilen verileri 48 saat için bir Azure Blob üzerinden yükleme için kullanıcıya kullanılabilir hale getirilir. 48 saat sonra erişim süresi ve kullanıcı, gerektiğinde yeni bir dışarı aktarma isteği göndermeniz gerekir.

Dışarı aktarılan verileri şunları içerir:

* Kullanıcının destek istekleri
* Kullanıcının Eylemler (paket yayımlama, hesabı oluşturun) denetim günlüklerini kalıcı olarak
* IIS günlüklerine kalıcı olarak herhangi bir kullanıcı bilgisi
