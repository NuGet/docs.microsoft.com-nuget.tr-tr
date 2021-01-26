---
title: NuGet 4,9 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve CCR 'ler dahil olmak üzere NuGet 4,9 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780143"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="cbdb5-103">NuGet 4,9 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="cbdb5-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="cbdb5-104">NuGet dağıtım araçlar:</span><span class="sxs-lookup"><span data-stu-id="cbdb5-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="cbdb5-105">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="cbdb5-105">NuGet version</span></span> | <span data-ttu-id="cbdb5-106">Visual Studio sürümünde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cbdb5-106">Available in Visual Studio version</span></span>| <span data-ttu-id="cbdb5-107">.NET SDK 'ları 'nda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cbdb5-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="cbdb5-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="cbdb5-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="cbdb5-109">Visual Studio 2017 sürüm 15.9.0</span><span class="sxs-lookup"><span data-stu-id="cbdb5-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="cbdb5-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="cbdb5-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="cbdb5-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="cbdb5-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="cbdb5-112">yok</span><span class="sxs-lookup"><span data-stu-id="cbdb5-112">n/a</span></span> | <span data-ttu-id="cbdb5-113">yok</span><span class="sxs-lookup"><span data-stu-id="cbdb5-113">n/a</span></span> |
| [<span data-ttu-id="cbdb5-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="cbdb5-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="cbdb5-115">Visual Studio 2017 sürüm 15.9.4</span><span class="sxs-lookup"><span data-stu-id="cbdb5-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="cbdb5-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="cbdb5-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="cbdb5-117">**4.9.3 &**</span><span class="sxs-lookup"><span data-stu-id="cbdb5-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="cbdb5-118">Visual Studio 2017 sürüm 15.9.6</span><span class="sxs-lookup"><span data-stu-id="cbdb5-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="cbdb5-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="cbdb5-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="cbdb5-120">Özet: 4.9.0 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="cbdb5-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="cbdb5-121">İmzalama: NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961), [blog gönderisine](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html) göre listelenen bir güvenilen yazar ve depo kümesinin kullanımını gerektirmek Için clientpolicies 'yi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbdb5-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="cbdb5-122">". snupkg" dosyalarını paket içinde simgeler içerecek şekilde oluşturma--sembol sunucusu için snupkg dosyalarını kabul etmek üzere NuGet protokolünü anlama- [#6878](https://github.com/NuGet/Home/issues/6878), [blog gönderisi](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="cbdb5-123">NuGet kimlik bilgisi eklentisi v2- [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="cbdb5-124">Self-Contained NuGet paketleri-lisans- [#4628](https://github.com/NuGet/Home/issues/4628), [duyuru](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="cbdb5-125">"Foo. Bar\1.0 \" dizinine- [#6949](https://github.com/NuGet/Home/issues/6949) paket başına MSBuild özelliği oluşturmak Için bir packagereference üzerinde opt" generatepathproperty "meta verilerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="cbdb5-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="cbdb5-126">NuGet işlemleri ile müşteri başarısını geliştirme- [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="cbdb5-127">Bir kilit dosyası kullanarak yinelenebilir paket geri yüklemelerini etkinleştirme- [#5602](https://github.com/NuGet/Home/issues/5602), [duyuru](https://github.com/NuGet/Announcements/issues/28), [blog gönderisi](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cbdb5-128">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-128">Issues fixed in this release</span></span>

* <span data-ttu-id="cbdb5-129">Packageayıklama tarafından oluşturulan hatalara (WarnAsErrors aracılığıyla) yapılan uyarılar asla ayıklanan paketi [#7445](https://github.com/NuGet/Home/issues/7445) bırakmamalıdır</span><span class="sxs-lookup"><span data-stu-id="cbdb5-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="cbdb5-130">Hatalı imzalı paketler genel paketler klasöründe sonlanmamalıdır- [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="cbdb5-131">bağlama yeniden yönlendirme oluşturması façlade derlemelerini atmamalıdır- [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="cbdb5-132">VersionRange eşittir, kayan aralıkları karşılaştırmıyor- [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="cbdb5-133">Geri yükleme: yeni .NET Core 2,1 HTTP Stack kullanarak performans gerileme- [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="cbdb5-134">Bir paketin güncelleştirilmesi, PackageReference- [#7285](https://github.com/NuGet/Home/issues/7285) privatevarlıklarını değiştirmemelidir</span><span class="sxs-lookup"><span data-stu-id="cbdb5-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="cbdb5-135">İmzalama: bir pakette çok fazla paket girişi varsa imzalama başarısız olur (>65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="cbdb5-136">"DotNet NuGet Push" kod yolu yeni kimlik bilgisi sağlayıcısını desteklemelidir- [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="cbdb5-137">Sabit kültür ile eklentileri yürütmeyi destekleme (Docker 'da olduğu gibi)- [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="cbdb5-138">NuGet kaynakları ekleme NuGet.config kimlik bilgilerini silmemelidir [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="cbdb5-139">devDependency PackageReference yüklemesi, excludelabs için varsayılan değer olmalıdır = derle- [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="cbdb5-140">Tüm projeler için Migrator seçeneğini düzeltir ve proje uyumsuz ise hatayı göster- [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="cbdb5-141">"DotNet Add Package", yaptığı geri yükleme işlemini varlıklar dosyasına yürütmelidir- [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="cbdb5-142">İmzalama: imzalamayı, ilişkili hata iletilerini geliştirme- [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="cbdb5-143">[Test hatası] [zh-TW] "Paket Yöneticisi konsolu" dizesi, Paket Yöneticisi konsolunda yerelleştirmez- [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="cbdb5-144">"Proje bilgileri bulunamıyor" etrafındaki hata iletisi VS- [#5350](https://github.com/NuGet/Home/issues/5350) içinde biraz daha belirli olmalıdır</span><span class="sxs-lookup"><span data-stu-id="cbdb5-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="cbdb5-145">NuGet paketinin nuspec sürüm etiketi kullanılırken hatalı bir hata iletisi- [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="cbdb5-146">DCR-Imzalama: NuGet protokolünü destekler: kayıt/4.9.0 kaynağı- [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="cbdb5-147">DCR-. nupkg. Metadata dosyası artık paket ayıklama sırasında oluşturulacak-"Content-hash"- [#7283](https://github.com/NuGet/Home/issues/7283) içerir</span><span class="sxs-lookup"><span data-stu-id="cbdb5-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="cbdb5-148">DCR-mono [#7222](https://github.com/NuGet/Home/issues/7222) yürütülürken eklentiler için Authenticode doğrulamasını atlama</span><span class="sxs-lookup"><span data-stu-id="cbdb5-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="cbdb5-149">Bu yayında düzeltilen tüm sorunların listesi 4.9.0</span><span class="sxs-lookup"><span data-stu-id="cbdb5-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="cbdb5-150">Özet: 4.9.1 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="cbdb5-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="cbdb5-151">Yeni bir komut ile nuget.config yazma desteği ekleyin- [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cbdb5-152">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-152">Issues fixed in this release</span></span>

* <span data-ttu-id="cbdb5-153">Lisans bağlantısı oluşturmayı onarma- [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="cbdb5-154">İmzaları doğrulamak için hata kodları gerileme- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="cbdb5-155">NuGet. Build. Tasks. Pack paketinde lisans bilgisi yok- [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="cbdb5-156">Bu yayında düzeltilen tüm sorunların listesi 4.9.1</span><span class="sxs-lookup"><span data-stu-id="cbdb5-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="cbdb5-157">Özet: 4.9.2 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="cbdb5-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cbdb5-158">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-158">Issues fixed in this release</span></span>

* <span data-ttu-id="cbdb5-159">Kaynak adı bir boşluk içeriyorsa VS/dotnet.exe/nuget.exe/msbuild.exe geri yükleme kimlik bilgileri kullanmaz- [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="cbdb5-160">LicenseAcceptanceWindow ve LicenseFileWindow erişilebilirlik sorunları- [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="cbdb5-161">DateTime içinde FormatException dönüştürücüsünü düzeltir- [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="cbdb5-162">Bu yayında düzeltilen tüm sorunların listesi 4.9.2</span><span class="sxs-lookup"><span data-stu-id="cbdb5-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="cbdb5-163">Özet: 4.9.3 & 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="cbdb5-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="cbdb5-164">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="cbdb5-165">"Yinelenebilir paket bir kilit dosyası kullanarak geri yükler" sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="cbdb5-166">Daha önce önbelleğe alınmış paketler için karma yanlış hesaplandığından kilitli mod çalışmıyor- [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="cbdb5-167">Restore, `packages.lock.json` dosya [#7667](https://github.com/NuGet/Home/issues/7667) tanımlı olandan farklı bir sürüme çözümleniyor</span><span class="sxs-lookup"><span data-stu-id="cbdb5-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="cbdb5-168">'--kilitlendi-Mode/RestoreLockedMode ', ProjectReferences dahil edildiğinde smerak eden geri yükleme hatalarıyla neden olur [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="cbdb5-169">MSBuild SDK 'Sı çözümleyici, [#7599](https://github.com/NuGet/Home/issues/7599) packages.lock.jskullanırken geri yükleme başarısız olan bir SDK PAKETI için SHA doğrulaması yapmayı dener</span><span class="sxs-lookup"><span data-stu-id="cbdb5-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="cbdb5-170">"Yapılandırılabilir güven Ilkeleri kullanarak bağımlılıklarınızı kilitleme" sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="cbdb5-171">dotnet.exe imzalı paketler desteklenmediğinden, güvenilen imzalayanlar değerlendirilmemelidir- [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="cbdb5-172">Yapılandırma dosyasındaki trustedSigners 'ın sırası, güven değerlendirmesini etkiler- [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="cbdb5-173">Isettings uygulanamıyor [ayarları güven Ilkeleri desteklemek için yeniden düzenleme API 'Leri nedeniyle oluşur]- [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="cbdb5-174">"Geliştirilmiş hata ayıklama deneyimi" sorunları</span><span class="sxs-lookup"><span data-stu-id="cbdb5-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="cbdb5-175">.NET Core küresel aracı için sembol paketi yayımlanamıyor- [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="cbdb5-176">"Kendi Içinde bulunan NuGet paketleri-Lisans" sorunları</span><span class="sxs-lookup"><span data-stu-id="cbdb5-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="cbdb5-177">Katıştırılmış lisans dosyası kullanılırken symbol. snupkg paketi oluşturulurken hata- [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="cbdb5-178">Bu yayında düzeltilen tüm sorunların listesi 4.9.3 &</span><span class="sxs-lookup"><span data-stu-id="cbdb5-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="cbdb5-179">Özet: 4.9.4 'deki yenilikler</span><span class="sxs-lookup"><span data-stu-id="cbdb5-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="cbdb5-180">Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="cbdb5-181">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="cbdb5-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="cbdb5-182">DotNet NuGet Push--Interactive, Mac 'te bir hata veriyor.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="cbdb5-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="cbdb5-184">Sorun</span><span class="sxs-lookup"><span data-stu-id="cbdb5-184">Issue</span></span>
<span data-ttu-id="cbdb5-185">`--interactive`Bağımsız değişken DotNet CLI tarafından iletilmiyor ve hata ile sonuçlanıyor`error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="cbdb5-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="cbdb5-186">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="cbdb5-186">Workaround</span></span>
<span data-ttu-id="cbdb5-187">Diğer bir DotNet komutunu, gibi etkileşimli seçenekle çalıştırın `dotnet restore --interactive` ve kimlik doğrulaması yapın.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="cbdb5-188">Kimlik doğrulaması daha sonra kimlik bilgisi sağlayıcısı tarafından önbelleğe alınmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="cbdb5-189">Ardından `dotnet nuget push` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="cbdb5-190">.NET Core SDK tarafından yüklenen FallbackFolders paketleri özel olarak yüklenir ve imza doğrulaması başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="cbdb5-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="cbdb5-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="cbdb5-192">Sorun</span><span class="sxs-lookup"><span data-stu-id="cbdb5-192">Issue</span></span>
<span data-ttu-id="cbdb5-193">Birden çok hedef netcoreapp 1. x ve netcoreapp 2. x ' i hedefleyen bir projeyi geri yüklemek için dotnet.exe 2. x kullanırken, geri dönüş klasörü bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="cbdb5-194">Bu, geri yükleme sırasında NuGet paketini geri dönüş klasöründen seçer ve genel paketler klasörüne yüklemeyi dener ve hata veren olağan imza doğrulamasını yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="cbdb5-195">Geçici çözüm</span><span class="sxs-lookup"><span data-stu-id="cbdb5-195">Workaround</span></span>
<span data-ttu-id="cbdb5-196">Geri dönüş klasörünün kullanımını, öğesini Nothing olarak ayarlayarak devre dışı bırakın `RestoreAdditionalProjectSources` .</span><span class="sxs-lookup"><span data-stu-id="cbdb5-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="cbdb5-197">`<RestoreAdditionalProjectSources/>` Bu durum, geri dönüş klasöründen geri yüklenmiş olabilecek NuGet.org 'ten çok sayıda paket indirileceği için bunu dikkatle kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbdb5-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
