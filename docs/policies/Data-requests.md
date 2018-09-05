---
title: Kullanıcı veri isteği sayısı
description: Kullanıcı verileri istemeye ilişkin ilkeler dışarı aktarma ve silme
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548060"
---
# <a name="user-data-requests"></a>Kullanıcı veri isteği sayısı

nuget.org kullanıcılar bilgi delete isteklerini ve bilgi dışarı aktarma isteklerini gönderebildiği [nuget.org](https://www.nuget.org). Her iki türü de destek biçiminde gönderilen istekleri ve bu yürütülebilir nuget.org yöneticileri tarafından 30 gün içinde.

Aşağıdaki kullanıcı verilerini doğrudan nuget.org erişilebilir:

* E-posta adresi, oturum açma hesabı, profil resminizi ve e-posta bildirimi ayarları gibi veri hesabıyla ilgili
* Sahip olunan API anahtarları
* Sahip olunan paketlerin listesi

Bu veriler üzerinden destek isteği dışarı aktarılan verileri bulunmamaktadır.

## <a name="identifying-customer-data"></a>Müşteri verileri tanımlama

Müşteri verilerini nuget.org kullanıcı hesabı adları tanımlanabilir.

## <a name="deleting-customer-data"></a>Müşteri verileri silme

Nuget.org adresinden kullanıcı verilerini silme isteği için:

1. Kullanıcı için oturum gerekir [nuget.org](https://www.nuget.org)
1. Kullanıcı hesabı silinecek bir istek göndermeniz gerekir [nuget.org/account/delete](https://www.nuget.org/account/delete)

Paketleri tek sahipleri olan kullanıcı hesabı silindi olmasını isteyen önce yeni sahipleri bulun önerilir. Paket Sahiplik devredildikten değil, NuGet paketi listelenmemiş ve sonuç olarak, artık Visual Studio'da veya nuget.org Web sitesinde arama sorgularında kullanılabilir. Hesabı silmeden önce nuget.org Yöneticiler kullanıcı oldukları paketleri yeni sahipleri bulun çalışın.

Hesap silme eylemi nuget.org yönetici tarafından istek tarihten itibaren 30 gün içinde tamamlanır.

Temel hesabını silme işlemi, tüm kullanıcı verilerini olması kaldırıldı nuget.org sistemden ve şu işlemler uygulanır:

* Silinmiş hesap ile nuget.org kaydı olur
* Tüm API anahtarları silinir ait
* Tüm ayrılmış ad alanlarından yayımlanan
* Herhangi bir paket sahipliği kaldırılır

Sahip olunan paketleri *değil* silindi. Listelenmemiş Arama sonuçlarından rağmen bunlara bağımlı projeler için paket geri yükleme yoluyla kullanılabilir kalır.

## <a name="exporting-customer-data"></a>Müşteri verilerini dışarı aktarma

Oturum açma işleminden sonra nuget.org için bir kullanıcı bir dışarı aktarma isteği aracılığıyla gönderebilir [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

Dışarı aktarılan verileri 48 saattir kullanıcıya aracılığıyla bir Azure Blob indirme için kullanılabilir hale getirilir. 48 saat sonra erişim süresi ve kullanıcı, gerektiği gibi yeni bir dışa aktarma isteği göndermeniz gerekir.

Dışarı aktarılan verileri içerir:

* Kullanıcının destek istekleri
* Kullanıcının eylemlerini (paket yayımlama, hesabı oluşturma) denetim günlüklerinde kalıcı olarak
* IIS günlükleri kalıcı olarak herhangi bir kullanıcı bilgisi
