---
title: NuGet 4.9 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere 4.9 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453823"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="27864-103">NuGet 4.9 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="27864-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="27864-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.9.0 işlevselliği ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="27864-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="27864-105">Aynı işlevlere komut satırı sürümleri de mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="27864-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="27864-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="27864-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="27864-107">DotNet.exe - [.NET Core SDK'sı 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="27864-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="27864-108">Özet: 4.9.0 yenilikler</span><span class="sxs-lookup"><span data-stu-id="27864-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="27864-109">İmzalama: Etkinleştirme güvenilen yazarlar ve depoları NuGet.Config içinde - listelenen bir dizi kullanımını zorunlu ClientPolicies [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="27864-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="27864-110">Paketi sembolleri içeren--snupkg dosyalar için Sembol sunucusu - kabul etmek için nuget Protokolü anlamak için anında iletme geliştirmek için ".snupkg" dosyaları oluşturma [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="27864-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="27864-111">NuGet kimlik bilgisi eklentisi V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="27864-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="27864-112">Müstakil NuGet paketleri - lisans - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="27864-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="27864-113">Kabul etme "GeneratePathProperty" meta verilerini oluşturmak için PackageReference etkinleştirme bir paket MSBuild özelliği için başına "Foo.Bar\1.0\" dizin - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="27864-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="27864-114">Müşteri başarı ile NuGet işlemleri - geliştirmek [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="27864-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="27864-115">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="27864-115">Issues fixed in this release</span></span>

* <span data-ttu-id="27864-116">Uyarıları PackageExtraction tarafından oluşturulan hatalara (aracılığıyla WarnAsErrors) yükseltilmiş etrafında - ayıklanan paket asla terk [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="27864-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="27864-117">Hatalı imzalanmış paketleri sone ermemlidir genel paketleri klasöründe - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="27864-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="27864-118">bağlama yeniden yönlendirme oluşturma atlamayın cephe derlemeleri - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="27864-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="27864-119">Kayan aralıkları - VersionRange eşittir karşılaştırma değil [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="27864-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="27864-120">Geri yükleme: yeni .NET Core 2.1 HTTP kullanarak performans gerilemesi yığınını - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="27864-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="27864-121">Güncelleştirme paketi değişiklik PrivateAssets - PackageReference'nın [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="27864-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="27864-122">İmzalama: bir paket çok fazla paket giriş varsa imzalama başarısız olması (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="27864-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="27864-123">"dotnet nuget anında iletme" kod yolu, yeni kimlik bilgisi sağlayıcısı - desteklemelidir [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="27864-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="27864-124">Yürütme eklentileri (gibi docker gerçekleşir) sabit kültür ile-destek [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="27864-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="27864-125">nuget kaynağı ekleme NuGet.config - kimlik bilgilerinin silemediğini [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="27864-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="27864-126">bir devDependency PackageReference yükleme excludeassets için varsayılan derleme - = [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="27864-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="27864-127">Proje uyumsuz - ise tüm projeler ve hatayı Göster görüntülenecek migrator seçeneği düzeltme [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="27864-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="27864-128">"dotnet Paketi Ekle" varlıklar dosyasına - gerçekleştirdiği geri işlemesi gerektiğini [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="27864-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="27864-129">İmzalama: imzalama ilgili hata iletileri - geliştirmek [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="27864-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="27864-130">[Test hatası] zh-TW Dize "Paket Yöneticisi Konsolu" Paket Yöneticisi konsolu - yerelleştirmek değil [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="27864-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="27864-131">"Proje bilgileri bulmak için yapılandırılamıyor" geçici hata iletisi ve iç karşılaştırması - biraz daha belirli [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="27864-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="27864-132">Nuget paketinin - nuspec sürüm etiketi yanlış kullanırken faydasız hata iletisi [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="27864-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="27864-133">DCR - imzalama: NuGet protokolünü destekleyen: RepositorySignatures/4.9.0 kaynak - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="27864-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="27864-134">-DCR. nupkg.metadata dosya artık - içerir "içerik-hash" - Paket ayıklama sırasında oluşturulur [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="27864-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="27864-135">-Mono üzerinde yürütülürken authenticode Doğrulamayı atla eklentileri için - DCR [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="27864-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="27864-136">Bu sürümde 4.9.0 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="27864-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="27864-137">Özet: 4.9.1 yenilikler</span><span class="sxs-lookup"><span data-stu-id="27864-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="27864-138">Bir yazma okumak için destek eklemek için bir yeni komut güvenilen-İmzalayanları - aracılığıyla nuget.config [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="27864-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="27864-139">Bu sürümde giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="27864-139">Issues fixed in this release</span></span>

* <span data-ttu-id="27864-140">Lisans bağlantı oluşturma - düzeltme [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="27864-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="27864-141">Hata kodları imzaları doğrulamak için gerileme- [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="27864-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="27864-142">Lisans bilgileri - NuGet.Build.Tasks.Pack paket yok [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="27864-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="27864-143">Bu sürümde 4.9.1 düzeltilen tüm sorunlara listesi</span><span class="sxs-lookup"><span data-stu-id="27864-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="27864-144">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="27864-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="27864-145">bir boşluk - kaynak adı içerdiğinde dotnet.exe/nuget.exe kimlik bilgilerini kullanmaz [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="27864-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="27864-146">Sorun</span><span class="sxs-lookup"><span data-stu-id="27864-146">Issue</span></span>
<span data-ttu-id="27864-147">Kaynak adı bir boşluk olduğunda nuget.exe gibi bir hata oluşturur. `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span><span class="sxs-lookup"><span data-stu-id="27864-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="27864-148">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="27864-148">Workaround</span></span>
<span data-ttu-id="27864-149">Bir boşluk içermemelidir kaynağının adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="27864-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="27864-150">DotNet nuget push--etkileşimli Mac üzerinde bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="27864-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="27864-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="27864-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="27864-152">Sorun</span><span class="sxs-lookup"><span data-stu-id="27864-152">Issue</span></span>
<span data-ttu-id="27864-153">`--interactive` Bağımsız değişken dotnet CLI tarafından iletilmez değil ve hataya neden olur `error: Missing value for option 'interactive'`</span><span class="sxs-lookup"><span data-stu-id="27864-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="27864-154">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="27864-154">Workaround</span></span>
<span data-ttu-id="27864-155">Etkileşimli seçeneğiyle gibi diğer dotnet komutu çalıştırmak `dotnet restore --interactive` ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="27864-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="27864-156">Ardından kimlik doğrulama kimlik bilgisi sağlayıcı tarafından önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="27864-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="27864-157">Ardından çalıştırın `dotnet nuget push`.</span><span class="sxs-lookup"><span data-stu-id="27864-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="27864-158">LicenseAcceptanceWindow ve LicenseFileWindow erişilebilirlik sorunları - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="27864-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="27864-159">Sorun</span><span class="sxs-lookup"><span data-stu-id="27864-159">Issue</span></span>
<span data-ttu-id="27864-160">Lisans kabulü ve lisans dosyası penceresinde klavye ile gezinme erişilebilirlik sorunları ve ekran okuyucu ve JAWS anlatım vardır.</span><span class="sxs-lookup"><span data-stu-id="27864-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="27864-161">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="27864-161">Workaround</span></span>
<span data-ttu-id="27864-162">Geçici çözüm yok.</span><span class="sxs-lookup"><span data-stu-id="27864-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="27864-163">.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız.</span><span class="sxs-lookup"><span data-stu-id="27864-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="27864-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="27864-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="27864-165">Sorun</span><span class="sxs-lookup"><span data-stu-id="27864-165">Issue</span></span>
<span data-ttu-id="27864-166">DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="27864-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="27864-167">Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="27864-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="27864-168">Geçici Çözüm</span><span class="sxs-lookup"><span data-stu-id="27864-168">Workaround</span></span>
<span data-ttu-id="27864-169">Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing.</span><span class="sxs-lookup"><span data-stu-id="27864-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="27864-170">`<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.</span><span class="sxs-lookup"><span data-stu-id="27864-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
