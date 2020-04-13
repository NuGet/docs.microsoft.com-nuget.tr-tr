---
title: NuGet 4.9 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve DCR'ler dahil olmak üzere NuGet 4.9 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496459"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="7d675-103">NuGet 4.9 Yayın Notları</span><span class="sxs-lookup"><span data-stu-id="7d675-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="7d675-104">NuGet dağıtım araçları:</span><span class="sxs-lookup"><span data-stu-id="7d675-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="7d675-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="7d675-105">NuGet version</span></span> | <span data-ttu-id="7d675-106">Visual Studio sürümünde mevcuttur</span><span class="sxs-lookup"><span data-stu-id="7d675-106">Available in Visual Studio version</span></span>| <span data-ttu-id="7d675-107">.NET SDK(ler) adresinde mevcuttur</span><span class="sxs-lookup"><span data-stu-id="7d675-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="7d675-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="7d675-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="7d675-109">Visual Studio 2017 sürümü 15.9.0</span><span class="sxs-lookup"><span data-stu-id="7d675-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="7d675-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="7d675-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="7d675-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="7d675-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="7d675-112">yok</span><span class="sxs-lookup"><span data-stu-id="7d675-112">n/a</span></span> | <span data-ttu-id="7d675-113">yok</span><span class="sxs-lookup"><span data-stu-id="7d675-113">n/a</span></span> |
| [<span data-ttu-id="7d675-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="7d675-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="7d675-115">Visual Studio 2017 sürümü 15.9.4</span><span class="sxs-lookup"><span data-stu-id="7d675-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="7d675-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="7d675-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="7d675-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="7d675-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="7d675-118">Visual Studio 2017 sürümü 15.9.6</span><span class="sxs-lookup"><span data-stu-id="7d675-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="7d675-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="7d675-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="7d675-120">Özeti: 4.9.0 Yenilikler</span><span class="sxs-lookup"><span data-stu-id="7d675-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="7d675-121">İmzalama: Müşteri İlkelerinin NuGet.Config'de listelenen Güvenilir Yazarlar ve Depolar kümesinin kullanılmasını gerektirmesini etkinleştirin - [#6961](https://github.com/NuGet/Home/issues/6961), [blog gönderisi](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="7d675-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="7d675-122">pakette semboller içeren ".snupkg" dosyaları oluşturun - sembol sunucusu için snupkg dosyaları kabul etmek nuget protokolünü anlamak için itme geliştirmek - [#6878](https://github.com/NuGet/Home/issues/6878), [blog yazısı](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="7d675-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="7d675-123">NuGet kimlik bilgileri eklentisi V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="7d675-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="7d675-124">Müstakil NuGet Paketleri - Lisans - [#4628](https://github.com/NuGet/Home/issues/4628), [duyuru](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="7d675-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="7d675-125">"Foo.Bar\1.0\" dizini " için paket başına MSBuild özelliği oluşturmak için bir PackageReference üzerinde "GeneratePathProperty" meta verileri etkinleştirin - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="7d675-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="7d675-126">NuGet işlemleri ile müşteri başarısını artırın - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="7d675-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="7d675-127">Bir kilit dosyası kullanarak tekrarlanabilir paket geri yüklemeleri etkinleştirin - [#5602](https://github.com/NuGet/Home/issues/5602), [duyuru](https://github.com/NuGet/Announcements/issues/28), [blog yazısı](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="7d675-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7d675-128">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="7d675-128">Issues fixed in this release</span></span>

* <span data-ttu-id="7d675-129">PackageExtraction tarafından yükseltilen hatalara yükseltilen uyarılar (WarnAsErrors aracılığıyla) ayıklanan paketi asla çevrede bırakmamalıdır - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="7d675-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="7d675-130">Kötü imzalanmış paketler küresel paketler klasöründe sona ermemelidir - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="7d675-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="7d675-131">bağlama yönlendirme üretimi cephe montajları atlamamalıdır - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="7d675-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="7d675-132">VersionRange Equals kayan aralıkları karşılaştırmaz - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="7d675-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="7d675-133">Geri yükleme: yeni .NET Core 2.1 HTTP yığını nı kullanarak performans regresyonu - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="7d675-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="7d675-134">Paketin Güncellemesi, Bir Paket Referansının PrivateAssets'ini değiştirmemelidir - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="7d675-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="7d675-135">İmzalama: bir paketçok fazla paket girişi varsa imzalama başarısız olmalıdır (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="7d675-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="7d675-136">"dotnet nuget push" codepath yeni kimlik sağlayıcısı desteklemelidir - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="7d675-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="7d675-137">Değişmez kültüre sahip eklentileri yürütmeyi destekleme (docker'da olduğu gibi) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="7d675-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="7d675-138">nuget kaynakları nuget.config gelen kimlik bilgilerini silmek gerekir eklemek - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="7d675-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="7d675-139">devDependency PackageReference yükleme varsayılan excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="7d675-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="7d675-140">tüm projeler için görüntülenecek göçmen seçeneğini düzeltin ve proje uyumsuzsa hata gösterin - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="7d675-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="7d675-141">"dotnet paketi ekle" varlıklar dosyasına gerçekleştirdiği geri yükleme işlemek gerekir - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="7d675-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="7d675-142">İmzalama: ilgili hata iletilerini imzalamayı geliştirme - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="7d675-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="7d675-143">[Test Hatası] [zh-TW] String "Package Manager Console" Package Manager Console'da yerelleştirilmese - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="7d675-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="7d675-144">"Proje bilgilerini bulamıyor" etrafında hata iletisi VS içinde biraz daha spesifik olmalıdır - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="7d675-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="7d675-145">Nuget paketinin nuspec sürüm etiketini yanlış kullanırken yardımcı olmayan hata [iletisi](https://github.com/NuGet/Home/issues/2714) - #2714</span><span class="sxs-lookup"><span data-stu-id="7d675-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="7d675-146">DCR - İmzalama: destek NuGet protokolü: Depoİmzalar/4.9.0 kaynak - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="7d675-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="7d675-147">DCR - .nupkg.metadata dosyası artık paket çıkarma sırasında oluşturulacak - "içerik-karma" içerir - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="7d675-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="7d675-148">DCR - Mono'da çalışırken eklentiler için authenticode doğrulamasını atlayın - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="7d675-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="7d675-149">Bu sürümde düzeltilen tüm sorunların listesi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="7d675-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="7d675-150">Özeti: Yenilikler 4.9.1</span><span class="sxs-lookup"><span data-stu-id="7d675-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="7d675-151">Nuget.config yeni bir komut güvenilir-imzalayanlar aracılığıyla bir yazı okuma için destek ekleyin - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="7d675-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7d675-152">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="7d675-152">Issues fixed in this release</span></span>

* <span data-ttu-id="7d675-153">Lisans bağlantısı oluşturma düzeltme - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="7d675-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="7d675-154">İmzaları doğrulamak için hata kodları regresyon - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="7d675-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="7d675-155">NuGet.Build.Tasks.Pack paketinin lisans bilgileri yok - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="7d675-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="7d675-156">Bu sürümde düzeltilen tüm sorunların listesi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="7d675-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="7d675-157">Özeti: Yenilikler 4.9.2</span><span class="sxs-lookup"><span data-stu-id="7d675-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7d675-158">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="7d675-158">Issues fixed in this release</span></span>

* <span data-ttu-id="7d675-159">VS/dotnet.exe/nuget.exe/msbuild.exe geri yükleme kaynak adı bir boşluk içeriyorsa kimlik bilgileri kullanmaz - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="7d675-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="7d675-160">LisansKabulPencere ve LisansFileWindow Erişilebilirlik sorunları - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="7d675-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="7d675-161">DateTimeConverter'dan DateTime.Parse'de Biçimözel durumu düzelt - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="7d675-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="7d675-162">Bu sürümde düzeltilen tüm sorunların listesi 4.9.2</span><span class="sxs-lookup"><span data-stu-id="7d675-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="7d675-163">Özeti: Yenilikler 4.9.3</span><span class="sxs-lookup"><span data-stu-id="7d675-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7d675-164">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="7d675-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="7d675-165">"Yinelenen Paket Kilit Dosyalarını Kullanarak Geri Yüklenir" Sorunları</span><span class="sxs-lookup"><span data-stu-id="7d675-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="7d675-166">Karma olarak çalışmayan kilitli mod, önceden önbelleğe alınmış paketler için yanlış hesaplanır - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="7d675-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="7d675-167">Geri yükleme, dosyada `packages.lock.json` tanımlanandan farklı bir sürüme gider - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="7d675-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="7d675-168">'--kilitli mod / RestoreLockedMode' ProjectReferences söz konusu olduğunda sahte Geri Yükleme hatalarıneden olur - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="7d675-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="7d675-169">MSBuild SDK çözümleyicisi packages.lock.json kullanırken geri başarısız bir SDK paketi için SHA doğrulamak için çalışır - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="7d675-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="7d675-170">"Yapılandırılabilir Güven İlkelerini Kullanarak Bağımlılıklarınızı Kilitleyin" Sorunları</span><span class="sxs-lookup"><span data-stu-id="7d675-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="7d675-171">dotnet.exe imzalı paketler desteklenmezken güvenilir imzalayanları değerlendirmemelidir - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="7d675-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="7d675-172">Config dosyasındaki güvenilir Signers sırası güven değerlendirmesini etkiler - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="7d675-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="7d675-173">ISettings uygulayamıyorum [Güven İlkeleri özelliğini desteklemek için ayarlar API'lerinin yeniden dizilme neden olur] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="7d675-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="7d675-174">"Geliştirilmiş Hata Ayıklama Deneyimi" Sorunları</span><span class="sxs-lookup"><span data-stu-id="7d675-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="7d675-175">.NET Core Global Tool için sembol paketi yayınlayamıyor - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="7d675-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="7d675-176">"Müstakil NuGet Paketleri - Lisans" Sorunları</span><span class="sxs-lookup"><span data-stu-id="7d675-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="7d675-177">Gömülü lisans dosyası kullanılırken hata oluşturma sembolü .snupkg paketi - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="7d675-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="7d675-178">Bu sürümde düzeltilen tüm sorunların listesi 4.9.3</span><span class="sxs-lookup"><span data-stu-id="7d675-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="7d675-179">Özeti: Yenilikler 4.9.4</span><span class="sxs-lookup"><span data-stu-id="7d675-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="7d675-180">Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır</span><span class="sxs-lookup"><span data-stu-id="7d675-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="7d675-181">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="7d675-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="7d675-182">dotnet nuget push --interactive Mac'te bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="7d675-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="7d675-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="7d675-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="7d675-184">Sorun</span><span class="sxs-lookup"><span data-stu-id="7d675-184">Issue</span></span>
<span data-ttu-id="7d675-185">Bağımsız `--interactive` değişken dotnet cli tarafından iletilmiyor ve hatayla sonuçlanıyor`error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="7d675-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="7d675-186">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="7d675-186">Workaround</span></span>
<span data-ttu-id="7d675-187">Gibi etkileşimli seçeneği ile başka bir `dotnet restore --interactive` dotnet komutu çalıştırın ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="7d675-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="7d675-188">Kimlik doğrulaması daha sonra kimlik bilgisi sağlayıcısı tarafından önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="7d675-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="7d675-189">Ardından `dotnet nuget push` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7d675-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="7d675-190">.NET Core SDK tarafından yüklenen FallbackFolders paketleri özel yüklü ve başarısız imza doğrulama.</span><span class="sxs-lookup"><span data-stu-id="7d675-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="7d675-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="7d675-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="7d675-192">Sorun</span><span class="sxs-lookup"><span data-stu-id="7d675-192">Issue</span></span>
<span data-ttu-id="7d675-193">netcoreapp 1.x ve netcoreapp 2.x'i hedefleyen bir projeyi geri yüklemek için dotnet.exe 2.x kullanırken, geri dönüş klasörü bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="7d675-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="7d675-194">Bu, geri yükleme sırasında, NuGet geri dönüş klasöründen paketi almak ve küresel paketler klasörüne yüklemek ve başarısız olağan imza doğrulama yapmak çalışacağız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d675-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="7d675-195">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="7d675-195">Workaround</span></span>
<span data-ttu-id="7d675-196">Geri dönüş klasörünün kullanımını hiçbir şeye `RestoreAdditionalProjectSources` ayarlayarak devre dışı k.</span><span class="sxs-lookup"><span data-stu-id="7d675-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="7d675-197">`<RestoreAdditionalProjectSources/>`Aksi takdirde geri dönüş klasöründen geri olurdu NuGet.org gelen bir çok paket indirilebilir bir sürü neden olacak gibi dikkatli bir şekilde kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d675-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
