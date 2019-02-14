---
title: NuGet 4.9 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere 4.9 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: aa9bf87504477506dbb1e9ac10d5c1d5841c224f
ms.sourcegitcommit: 885973352d31808e3ddbb45da6d6e54d1e4fca9d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56224950"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="3171f-103">NuGet 4.9 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="3171f-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="3171f-104">NuGet dağıtım araçları:</span><span class="sxs-lookup"><span data-stu-id="3171f-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3171f-105">NuGet sürüm</span><span class="sxs-lookup"><span data-stu-id="3171f-105">NuGet version</span></span> | <span data-ttu-id="3171f-106">Visual Studio sürümü içinde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="3171f-106">Available in Visual Studio version</span></span>| <span data-ttu-id="3171f-107">.NET SDK'sı sürümünü kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="3171f-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="3171f-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="3171f-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3171f-109">Visual Studio 2017 sürüm 15.9.0</span><span class="sxs-lookup"><span data-stu-id="3171f-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="3171f-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="3171f-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="3171f-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="3171f-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="3171f-112">yok</span><span class="sxs-lookup"><span data-stu-id="3171f-112">n/a</span></span> | <span data-ttu-id="3171f-113">yok</span><span class="sxs-lookup"><span data-stu-id="3171f-113">n/a</span></span> |
| [<span data-ttu-id="3171f-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="3171f-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="3171f-115">Visual Studio 2017 sürüm 15.9.4</span><span class="sxs-lookup"><span data-stu-id="3171f-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="3171f-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="3171f-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="3171f-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="3171f-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="3171f-118">Visual Studio 2017 sürüm 15.9.6</span><span class="sxs-lookup"><span data-stu-id="3171f-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="3171f-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="3171f-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="3171f-120">Özet: 4.9.0 yenilikler</span><span class="sxs-lookup"><span data-stu-id="3171f-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="3171f-121">İmzalama: Güvenilen yazarlar ve depoları NuGet.Config içinde - listelenen bir dizi kullanımını zorunlu ClientPolicies etkinleştirme [#6961](https://github.com/NuGet/Home/issues/6961), [blog gönderisi](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="3171f-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="3171f-122">Paketi sembolleri içeren--snupkg dosyalar için Sembol sunucusu - kabul etmek için nuget Protokolü anlamak için anında iletme geliştirmek için ".snupkg" dosyaları oluşturma [#6878](https://github.com/NuGet/Home/issues/6878), [blog gönderisi](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="3171f-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="3171f-123">NuGet kimlik bilgisi eklentisi V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="3171f-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="3171f-124">Müstakil NuGet paketlerini - lisans - [#4628](https://github.com/NuGet/Home/issues/4628), [Duyurusu](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="3171f-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="3171f-125">Kabul etme "GeneratePathProperty" meta verilerini oluşturmak için PackageReference etkinleştirme bir paket MSBuild özelliği için başına "Foo.Bar\1.0\" dizin - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="3171f-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="3171f-126">Müşteri başarı ile NuGet işlemleri - geliştirmek [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="3171f-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="3171f-127">Etkinleştirme kilidi kullanarak paket yinelenebilir geri yükler - dosya [#5602](https://github.com/NuGet/Home/issues/5602), [duyuru](https://github.com/NuGet/Announcements/issues/28), [blog gönderisi](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="3171f-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3171f-128">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3171f-128">Issues fixed in this release</span></span>

* <span data-ttu-id="3171f-129">Uyarıları PackageExtraction tarafından oluşturulan hatalara (aracılığıyla WarnAsErrors) yükseltilmiş etrafında - ayıklanan paket asla terk [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="3171f-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="3171f-130">Hatalı imzalanmış paketleri sone ermemlidir genel paketleri klasöründe - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="3171f-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="3171f-131">bağlama yeniden yönlendirme oluşturma atlamayın cephe derlemeleri - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="3171f-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="3171f-132">Kayan aralıkları - VersionRange eşittir karşılaştırma değil [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="3171f-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="3171f-133">Geri yükleme: yeni .NET Core 2.1 HTTP kullanarak performans gerilemesi yığınını - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="3171f-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="3171f-134">Güncelleştirme paketi değişiklik PrivateAssets - PackageReference'nın [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="3171f-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="3171f-135">İmzalama: bir paket çok fazla paket giriş varsa imzalama başarısız olması (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="3171f-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="3171f-136">"dotnet nuget anında iletme" kod yolu, yeni kimlik bilgisi sağlayıcısı - desteklemelidir [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="3171f-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="3171f-137">Yürütme eklentileri (gibi docker gerçekleşir) sabit kültür ile-destek [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="3171f-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="3171f-138">nuget kaynağı ekleme NuGet.config - kimlik bilgilerinin silemediğini [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="3171f-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="3171f-139">bir devDependency PackageReference yükleme excludeassets için varsayılan derleme - = [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="3171f-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="3171f-140">Proje uyumsuz - ise tüm projeler ve hatayı Göster görüntülenecek migrator seçeneği düzeltme [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="3171f-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="3171f-141">"dotnet Paketi Ekle" varlıklar dosyasına - gerçekleştirdiği geri işlemesi gerektiğini [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="3171f-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="3171f-142">İmzalama: imzalama ilgili hata iletileri - geliştirmek [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="3171f-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="3171f-143">[Test hatası] zh-TW Dize "Paket Yöneticisi Konsolu" Paket Yöneticisi konsolu - yerelleştirmek değil [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="3171f-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="3171f-144">"Proje bilgileri bulmak için yapılandırılamıyor" geçici hata iletisi ve iç karşılaştırması - biraz daha belirli [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="3171f-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="3171f-145">Nuget paketinin - nuspec sürüm etiketi yanlış kullanırken faydasız hata iletisi [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="3171f-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="3171f-146">DCR - imzalama: NuGet protokolünü destekler: RepositorySignatures/4.9.0 kaynak - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="3171f-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="3171f-147">-DCR. nupkg.metadata dosya artık - içerir "içerik-hash" - Paket ayıklama sırasında oluşturulur [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="3171f-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="3171f-148">-Mono üzerinde yürütülürken authenticode Doğrulamayı atla eklentileri için - DCR [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="3171f-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="3171f-149">Bu sürümde 4.9.0 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="3171f-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="3171f-150">Özet: 4.9.1 yenilikler</span><span class="sxs-lookup"><span data-stu-id="3171f-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="3171f-151">Bir yazma okumak için destek eklemek için bir yeni komut güvenilen-İmzalayanları - aracılığıyla nuget.config [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="3171f-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3171f-152">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3171f-152">Issues fixed in this release</span></span>

* <span data-ttu-id="3171f-153">Lisans bağlantı oluşturma - düzeltme [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="3171f-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="3171f-154">Hata kodları imzaları doğrulamak için gerileme- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="3171f-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="3171f-155">Lisans bilgileri - NuGet.Build.Tasks.Pack paket yok [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="3171f-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="3171f-156">Bu sürümde 4.9.1 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="3171f-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="3171f-157">Özet: 4.9.2 yenilikler</span><span class="sxs-lookup"><span data-stu-id="3171f-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3171f-158">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3171f-158">Issues fixed in this release</span></span>

* <span data-ttu-id="3171f-159">Bir boşluk - kaynak adı içerdiğinde VS/dotnet.exe/nuget.exe/msbuild.exe geri yükleme kimlik bilgileri kullanmaz [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="3171f-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="3171f-160">LicenseAcceptanceWindow ve LicenseFileWindow erişilebilirlik sorunları - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="3171f-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="3171f-161">FormatException içinde DateTime.Parse DateTimeConverter - düzeltme [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="3171f-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="3171f-162">Bu sürümde 4.9.2 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="3171f-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="3171f-163">Özet: 4.9.3 yenilikler</span><span class="sxs-lookup"><span data-stu-id="3171f-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3171f-164">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3171f-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="3171f-165">"Kilit dosyası kullanarak paket yinelenebilir geri yüklemeler" sorunları</span><span class="sxs-lookup"><span data-stu-id="3171f-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="3171f-166">Karma yanlış için önceden hesaplanan şekilde çalışmamasıyla kilitli modda paketler - önbelleğe alınmış [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="3171f-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="3171f-167">Geri yükleme farklı bir sürüme içinde tanımlanan daha çözümlenir `packages.lock.json` dosya - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="3171f-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="3171f-168">'--kilitli modda / RestoreLockedMode' başvuruları söz konusu olduğunda - alacaklardır geri yükleme hatalarının neden [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="3171f-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="3171f-169">MSBuild SDK'sı Çözümleyicisi çalıştığında SHA - packages.lock.json kullanırken geri yükleme başarısız için bir SDK paketi doğrulamak [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="3171f-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="3171f-170">"Yapılandırılabilir güven ilkelerini kullanarak Bağımlılıklarınızı kilitleme" sorunları</span><span class="sxs-lookup"><span data-stu-id="3171f-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="3171f-171">DotNet.exe değil değerlendirmek güvenilen İmzalayanları imzalanmış paketleri desteklenmez ancak - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="3171f-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="3171f-172">Yapılandırma dosyasında trustedSigners düzenini etkiler güven değerlendirmesi - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="3171f-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="3171f-173">ISettings uygulayamaz [ayarları Düzenleyicisi tarafından neden Güven İlkeleri özelliğini desteklemek için API'leri]- [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="3171f-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="3171f-174">"Hata ayıklama deneyimi geliştirildi" sorunları</span><span class="sxs-lookup"><span data-stu-id="3171f-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="3171f-175">Sembol paketi için .NET Core genel aracı - yayımlanamıyor [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="3171f-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="3171f-176">"Kendi içinde NuGet paketlerini - lisans" sorunları</span><span class="sxs-lookup"><span data-stu-id="3171f-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="3171f-177">Sembol .snupkg paketi kullanırken oluşturulurken bir hata oluştu - lisans dosyası katıştırılmış [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="3171f-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="3171f-178">Bu sürümde 4.9.3 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="3171f-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a><span data-ttu-id="3171f-179">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="3171f-179">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="3171f-180">DotNet nuget push--etkileşimli Mac üzerinde bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="3171f-180">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="3171f-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3171f-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="3171f-182">Sorun</span><span class="sxs-lookup"><span data-stu-id="3171f-182">Issue</span></span>
<span data-ttu-id="3171f-183">`--interactive` Bağımsız değişken dotnet CLI tarafından iletilmez değil ve hataya neden olur `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="3171f-183">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="3171f-184">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="3171f-184">Workaround</span></span>
<span data-ttu-id="3171f-185">Etkileşimli seçeneğiyle gibi diğer dotnet komutu çalıştırmak `dotnet restore --interactive` ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="3171f-185">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="3171f-186">Ardından kimlik doğrulama kimlik bilgisi sağlayıcı tarafından önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3171f-186">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="3171f-187">Ardından çalıştırın `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="3171f-187">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="3171f-188">.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="3171f-188">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3171f-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3171f-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="3171f-190">Sorun</span><span class="sxs-lookup"><span data-stu-id="3171f-190">Issue</span></span>
<span data-ttu-id="3171f-191">DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="3171f-191">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3171f-192">Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="3171f-192">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="3171f-193">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="3171f-193">Workaround</span></span>
<span data-ttu-id="3171f-194">Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing.</span><span class="sxs-lookup"><span data-stu-id="3171f-194">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="3171f-195">`<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.</span><span class="sxs-lookup"><span data-stu-id="3171f-195">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
