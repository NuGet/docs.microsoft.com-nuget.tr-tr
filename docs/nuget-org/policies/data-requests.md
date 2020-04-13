---
title: Kullanıcı Veri İstekleri
description: Kullanıcı verilerinin dışa aktarılmasını ve silinilmesini isteme ilkeleri
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427514"
---
# <a name="user-data-requests"></a>Kullanıcı Veri İstekleri

nuget.org kullanıcılar [nuget.org](https://www.nuget.org)üzerinden bilgi silme isteklerini ve bilgi verme isteklerini gönderebilirler. Her iki tür de destek istekleri şeklinde gönderilir ve 30 gün içinde nuget.org yöneticileri tarafından yürütülür.

Aşağıdaki kullanıcı verilerine nuget.org aracılığıyla doğrudan erişilebilir:

* E-posta adresi, giriş hesabı, profil resmi ve e-posta bildirim ayarları gibi hesapla ilgili veriler
* Sahip OLUNan API Anahtarları
* Sahip olunan paketler listesi

Bu veriler, destek isteği yoluyla dışa aktarılan verilere dahil edilmez.

## <a name="identifying-customer-data"></a>Müşteri verilerinin tanımlanması

Müşteri verileri nuget.org kullanıcı hesabı adları olarak tanımlanabilir.

## <a name="deleting-customer-data"></a>Müşteri verilerini silme

Kullanıcı verilerinin nuget.org silen isteği için:

1. Kullanıcı [nuget.org](https://www.nuget.org) oturum açmalı
1. Kullanıcı, hesabının [silinmesi](https://www.nuget.org/account/delete) için bir istek nuget.org/account/delete

Paketlerin tek sahibi olan kullanıcıların, hesaplarının silinmesini istemeden önce yeni sahipler bulmaları tavsiye edilir. Paket sahipliği aktarılamazsa, NuGet paketi liste dışı kalır ve sonuç olarak Visual Studio'daki arama sorgularında veya nuget.org web sitesinde kullanılamaz. Hesabı silmeden önce, nuget.org yöneticileri sahip oldukları paketler için yeni sahipler bulmak için kullanıcıyla birlikte çalışır.

Hesap silme eylemi, istek tarihinden itibaren 30 gün içinde nuget.org yöneticisi tarafından tamamlanır.

Hesap silme işleminde, kullanıcının tüm verileri nuget.org sisteminden kaldırılır ve aşağıdaki işlemler yapılır:

* Silinen hesap nuget.org ile kayıt dışı olur
* Sahip olunan tüm API Anahtarları silinir
* Tüm ayrılmış ad alanları serbest bırakılır
* Herhangi bir paket sahipliği kaldırılır

Sahip olunan paketler *silinmez.* Arama sonuçlarından listelenmemiş olsalar da, bunlar paket geri yükleme yoluyla bunlara bağlı projelere kullanılabilir durumda kalır.

## <a name="exporting-customer-data"></a>Müşteri verilerini dışa aktarma

nuget.org oturum açmadan sonra, kullanıcı [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) aracılığıyla bir dışa aktarma isteği gönderebilir

İhraç edilen veriler, Azure Blob üzerinden indirilebilmek için kullanıcıya 48 saat süreyle kullanıma sunulur. 48 saat sonra erişimin süresi doluyor ve kullanıcı nın gerektiğinde yeni bir dışa aktarma isteği göndermesi gerekir.

Dışa aktarılan veriler şunları içerir:

* Kullanıcının destek istekleri
* Denetim günlüklerinde kalıcı olarak kullanıcının eylemleri (paket yayınlama, hesap oluşturma)
* IIS günlüklerinde kalıcı olan tüm kullanıcı bilgileri
