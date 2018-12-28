---
title: NuGet 4.9 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere 4.9 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 7dcb2e430ad80815f716f5567b511ff08acfe31b
ms.sourcegitcommit: a9babe261f67da0f714d168d04ea54a66628974b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/21/2018
ms.locfileid: "53735142"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="58a9b-103">NuGet 4.9 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="58a9b-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="58a9b-104">NuGet dağıtım araçları:</span><span class="sxs-lookup"><span data-stu-id="58a9b-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="58a9b-105">NuGet sürüm</span><span class="sxs-lookup"><span data-stu-id="58a9b-105">NuGet version</span></span> | <span data-ttu-id="58a9b-106">Visual Studio sürümü içinde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="58a9b-106">Available in Visual Studio version</span></span>| <span data-ttu-id="58a9b-107">.NET SDK'sı sürümünü kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="58a9b-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| <span data-ttu-id="58a9b-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="58a9b-108">**4.9.0**</span></span> | <span data-ttu-id="58a9b-109">Visual Studio 2017 sürüm 15.9.0</span><span class="sxs-lookup"><span data-stu-id="58a9b-109">Visual Studio 2017 version 15.9.0</span></span> | <span data-ttu-id="58a9b-110">2.1.500, 2.2.100</span><span class="sxs-lookup"><span data-stu-id="58a9b-110">2.1.500, 2.2.100</span></span> |
| <span data-ttu-id="58a9b-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="58a9b-111">**4.9.1**</span></span> | <span data-ttu-id="58a9b-112">yok</span><span class="sxs-lookup"><span data-stu-id="58a9b-112">n/a</span></span> | <span data-ttu-id="58a9b-113">yok</span><span class="sxs-lookup"><span data-stu-id="58a9b-113">n/a</span></span> |
| [<span data-ttu-id="58a9b-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="58a9b-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="58a9b-115">Visual Studio 2017 sürüm 15.9.4</span><span class="sxs-lookup"><span data-stu-id="58a9b-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="58a9b-116">2.1.502, 2.2.101</span><span class="sxs-lookup"><span data-stu-id="58a9b-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |

## <a name="summary-whats-new-in-490"></a><span data-ttu-id="58a9b-117">Özet: 4.9.0 yenilikler</span><span class="sxs-lookup"><span data-stu-id="58a9b-117">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="58a9b-118">İmzalama: Güvenilen yazarlar ve depoları NuGet.Config içinde - listelenen bir dizi kullanımını zorunlu ClientPolicies etkinleştirme [#6961](https://github.com/NuGet/Home/issues/6961), [blog gönderisi](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="58a9b-118">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="58a9b-119">Paketi sembolleri içeren--snupkg dosyalar için Sembol sunucusu - kabul etmek için nuget Protokolü anlamak için anında iletme geliştirmek için ".snupkg" dosyaları oluşturma [#6878](https://github.com/NuGet/Home/issues/6878), [blog gönderisi](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="58a9b-119">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="58a9b-120">NuGet kimlik bilgisi eklentisi V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="58a9b-120">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="58a9b-121">Müstakil NuGet paketlerini - lisans - [#4628](https://github.com/NuGet/Home/issues/4628), [Duyurusu](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="58a9b-121">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="58a9b-122">Kabul etme "GeneratePathProperty" meta verilerini oluşturmak için PackageReference etkinleştirme bir paket MSBuild özelliği için başına "Foo.Bar\1.0\" dizin - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="58a9b-122">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="58a9b-123">Müşteri başarı ile NuGet işlemleri - geliştirmek [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="58a9b-123">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="58a9b-124">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="58a9b-124">Issues fixed in this release</span></span>

* <span data-ttu-id="58a9b-125">Uyarıları PackageExtraction tarafından oluşturulan hatalara (aracılığıyla WarnAsErrors) yükseltilmiş etrafında - ayıklanan paket asla terk [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="58a9b-125">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="58a9b-126">Hatalı imzalanmış paketleri sone ermemlidir genel paketleri klasöründe - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="58a9b-126">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="58a9b-127">bağlama yeniden yönlendirme oluşturma atlamayın cephe derlemeleri - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="58a9b-127">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="58a9b-128">Kayan aralıkları - VersionRange eşittir karşılaştırma değil [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="58a9b-128">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="58a9b-129">Geri yükleme: yeni .NET Core 2.1 HTTP kullanarak performans gerilemesi yığınını - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="58a9b-129">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="58a9b-130">Güncelleştirme paketi değişiklik PrivateAssets - PackageReference'nın [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="58a9b-130">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="58a9b-131">İmzalama: bir paket çok fazla paket giriş varsa imzalama başarısız olması (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="58a9b-131">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="58a9b-132">"dotnet nuget anında iletme" kod yolu, yeni kimlik bilgisi sağlayıcısı - desteklemelidir [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="58a9b-132">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="58a9b-133">Yürütme eklentileri (gibi docker gerçekleşir) sabit kültür ile-destek [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="58a9b-133">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="58a9b-134">nuget kaynağı ekleme NuGet.config - kimlik bilgilerinin silemediğini [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="58a9b-134">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="58a9b-135">bir devDependency PackageReference yükleme excludeassets için varsayılan derleme - = [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="58a9b-135">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="58a9b-136">Proje uyumsuz - ise tüm projeler ve hatayı Göster görüntülenecek migrator seçeneği düzeltme [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="58a9b-136">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="58a9b-137">"dotnet Paketi Ekle" varlıklar dosyasına - gerçekleştirdiği geri işlemesi gerektiğini [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="58a9b-137">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="58a9b-138">İmzalama: imzalama ilgili hata iletileri - geliştirmek [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="58a9b-138">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="58a9b-139">[Test hatası] zh-TW Dize "Paket Yöneticisi Konsolu" Paket Yöneticisi konsolu - yerelleştirmek değil [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="58a9b-139">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="58a9b-140">"Proje bilgileri bulmak için yapılandırılamıyor" geçici hata iletisi ve iç karşılaştırması - biraz daha belirli [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="58a9b-140">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="58a9b-141">Nuget paketinin - nuspec sürüm etiketi yanlış kullanırken faydasız hata iletisi [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="58a9b-141">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="58a9b-142">DCR - imzalama: NuGet protokolünü destekler: RepositorySignatures/4.9.0 kaynak - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="58a9b-142">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="58a9b-143">-DCR. nupkg.metadata dosya artık - içerir "içerik-hash" - Paket ayıklama sırasında oluşturulur [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="58a9b-143">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="58a9b-144">-Mono üzerinde yürütülürken authenticode Doğrulamayı atla eklentileri için - DCR [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="58a9b-144">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="58a9b-145">Bu sürümde 4.9.0 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="58a9b-145">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="58a9b-146">Özet: 4.9.1 yenilikler</span><span class="sxs-lookup"><span data-stu-id="58a9b-146">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="58a9b-147">Bir yazma okumak için destek eklemek için bir yeni komut güvenilen-İmzalayanları - aracılığıyla nuget.config [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="58a9b-147">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="58a9b-148">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="58a9b-148">Issues fixed in this release</span></span>

* <span data-ttu-id="58a9b-149">Lisans bağlantı oluşturma - düzeltme [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="58a9b-149">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="58a9b-150">Hata kodları imzaları doğrulamak için gerileme- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="58a9b-150">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="58a9b-151">Lisans bilgileri - NuGet.Build.Tasks.Pack paket yok [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="58a9b-151">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="58a9b-152">Bu sürümde 4.9.1 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="58a9b-152">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="58a9b-153">Özet: 4.9.2 yenilikler</span><span class="sxs-lookup"><span data-stu-id="58a9b-153">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="58a9b-154">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="58a9b-154">Issues fixed in this release</span></span>

* <span data-ttu-id="58a9b-155">Bir boşluk - kaynak adı içerdiğinde VS/dotnet.exe/nuget.exe/msbuild.exe geri yükleme kimlik bilgileri kullanmaz [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="58a9b-155">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="58a9b-156">LicenseAcceptanceWindow ve LicenseFileWindow erişilebilirlik sorunları - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="58a9b-156">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="58a9b-157">FormatException içinde DateTime.Parse DateTimeConverter - düzeltme [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="58a9b-157">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="58a9b-158">Bu sürümde 4.9.2 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="58a9b-158">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="known-issues"></a><span data-ttu-id="58a9b-159">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="58a9b-159">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="58a9b-160">DotNet nuget push--etkileşimli Mac üzerinde bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="58a9b-160">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="58a9b-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="58a9b-161"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="58a9b-162">Sorun</span><span class="sxs-lookup"><span data-stu-id="58a9b-162">Issue</span></span>
<span data-ttu-id="58a9b-163">`--interactive` Bağımsız değişken dotnet CLI tarafından iletilmez değil ve hataya neden olur `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="58a9b-163">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="58a9b-164">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="58a9b-164">Workaround</span></span>
<span data-ttu-id="58a9b-165">Etkileşimli seçeneğiyle gibi diğer dotnet komutu çalıştırmak `dotnet restore --interactive` ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="58a9b-165">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="58a9b-166">Ardından kimlik doğrulama kimlik bilgisi sağlayıcı tarafından önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="58a9b-166">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="58a9b-167">Ardından çalıştırın `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="58a9b-167">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="58a9b-168">.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="58a9b-168">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="58a9b-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="58a9b-169"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="58a9b-170">Sorun</span><span class="sxs-lookup"><span data-stu-id="58a9b-170">Issue</span></span>
<span data-ttu-id="58a9b-171">DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="58a9b-171">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="58a9b-172">Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="58a9b-172">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="58a9b-173">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="58a9b-173">Workaround</span></span>
<span data-ttu-id="58a9b-174">Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing.</span><span class="sxs-lookup"><span data-stu-id="58a9b-174">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="58a9b-175">`<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.</span><span class="sxs-lookup"><span data-stu-id="58a9b-175">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
