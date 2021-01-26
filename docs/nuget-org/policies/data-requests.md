---
title: Kullanıcı veri Istekleri
description: Kullanıcı verilerini dışa ve silmeyi isteme ilkeleri
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775723"
---
# <a name="user-data-requests"></a>Kullanıcı veri Istekleri

nuget.org kullanıcılar, [NuGet.org](https://www.nuget.org)aracılığıyla bilgi silme isteklerini ve bilgi dışarı aktarma isteklerini gönderebilir. Her iki tür de destek istekleri biçiminde gönderilir ve 30 gün içinde nuget.org yöneticileri tarafından yürütülür.

Aşağıdaki kullanıcı verilerine doğrudan nuget.org üzerinden erişilebilir:

* E-posta adresi, oturum açma hesabı, profil resmi ve e-posta bildirim ayarları gibi hesap ile ilgili veriler
* Sahip olan API anahtarları
* Sahip olunan paketlerin listesi

Bu veriler, destek isteği aracılığıyla dışarıya aktarılmış verilere dahil değildir.

## <a name="identifying-customer-data"></a>Müşteri verilerini tanımlama

Müşteri verileri, nuget.org Kullanıcı hesabı adı olarak tanımlanabilir.

## <a name="deleting-customer-data"></a>Müşteri verilerini silme

Nuget.org 'ten Kullanıcı verilerini silme isteğinde bulunan:

1. Kullanıcının [NuGet.org](https://www.nuget.org) 'de oturum açması gerekir
1. Kullanıcının, hesabı için bir istek göndermesi gerekir [NuGet.org/Account/Delete](https://www.nuget.org/account/delete)

Yalnızca paketlerin sahibi olan kullanıcıların, hesaplarının silinmesini istemeden önce yeni sahipleri bulması önerilir. Paket sahipliği aktarılmadıysa, NuGet paketi listelenmemiş olur ve sonuç olarak, Visual Studio 'da veya nuget.org web sitesinde arama sorgularında artık kullanılamaz. Hesabı silmeden önce, nuget.org yöneticileri sahip oldukları paketlerin yeni sahiplerini bulmak için kullanıcıyla birlikte çalışır.

Hesap silme eylemi, istek tarihinden itibaren 30 gün içinde nuget.org Yöneticisi tarafından tamamlanır.

Hesap silme işleminden sonra, tüm Kullanıcı verileri nuget.org sisteminden kaldırılır ve aşağıdaki eylemler gerçekleştirilir:

* Silinen hesabın kaydı nuget.org olur
* Sahip olunan tüm API anahtarları silinir
* Tüm ayrılmış ad alanları serbest bırakılır
* Tüm paket sahipliği kaldırılır

Sahip olunan *paketler silinmez.* Arama sonuçlarından etkilenmese de, bunlara bağlı projelere paket geri yüklemesi aracılığıyla erişilebilir kalırlar.

## <a name="exporting-customer-data"></a>Müşteri verilerini dışa aktarma

Nuget.org 'de oturum açtıktan sonra, Kullanıcı [NuGet.org/policies/Contact](https://www.nuget.org/policies/Contact) aracılığıyla bir dışarı aktarma isteği gönderebilir

İçe aktarılmış veriler, kullanıcının bir Azure blobu aracılığıyla indirileceği 48 saat için kullanılabilir hale getirilir. 48 saat sonra, erişim süresi dolar ve Kullanıcı gerektiğinde yeni bir dışarı aktarma isteği göndermesi gerekir.

İçe aktarılmış veriler şunları içerir:

* Kullanıcının destek istekleri
* Kullanıcı eylemleri (paketi Yayımla, hesabı oluştur) denetim günlüklerinde kalıcı olarak
* IIS günlüklerinde kalıcı olarak herhangi bir Kullanıcı bilgisi
