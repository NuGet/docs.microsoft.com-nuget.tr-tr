---
title: NuGet platformlar arası eklentiler
description: NuGet. exe, DotNet. exe, MSBuild. exe ve Visual Studio için NuGet platformlar arası eklentileri
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380496"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="f0bf9-103">NuGet platformlar arası eklentiler</span><span class="sxs-lookup"><span data-stu-id="f0bf9-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="f0bf9-104">NuGet 4.8 + platformlar arası eklentiler için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="f0bf9-105">Bu, bir işlem kuralları kümesine uyması gereken yeni bir eklenti genişletilebilirlik modeli oluşturarak ile elde edildi.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="f0bf9-106">Eklentiler, NuGet Istemcilerinin ayrı bir işlemde başlatması için kendi içinde bulunan yürütülebilir dosya (.NET Core World ' te çalıştırılabilir).</span><span class="sxs-lookup"><span data-stu-id="f0bf9-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="f0bf9-107">Bu bir kez doğru yazma, her yerde çalışan eklenti.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="f0bf9-108">Bu, tüm NuGet istemci araçlarıyla çalışır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="f0bf9-109">Eklentiler .NET Framework (NuGet. exe, MSBuild. exe ve Visual Studio) ya da .NET Core (DotNet. exe) olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="f0bf9-110">NuGet Istemcisi ve eklentisi arasındaki sürümlü bir iletişim protokolü tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="f0bf9-111">Başlangıç el sıkışması sırasında, 2 işlem protokol sürümü üzerinde anlaşacak.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="f0bf9-112">Tüm NuGet istemci araçları senaryolarını kapsayacak şekilde, bunlardan biri hem .NET Framework hem de .NET Core eklentisine gerek duyar.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="f0bf9-113">Aşağıda, eklentilerin istemci/çerçeve birleşimleri açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="f0bf9-114">İstemci aracı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-114">Client tool</span></span>  | <span data-ttu-id="f0bf9-115">Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="f0bf9-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0bf9-116">Visual Studio</span></span> | <span data-ttu-id="f0bf9-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-117">.NET Framework</span></span> |
| <span data-ttu-id="f0bf9-118">DotNet. exe</span><span class="sxs-lookup"><span data-stu-id="f0bf9-118">dotnet.exe</span></span> | <span data-ttu-id="f0bf9-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f0bf9-119">.NET Core</span></span> |
| <span data-ttu-id="f0bf9-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="f0bf9-120">NuGet.exe</span></span> | <span data-ttu-id="f0bf9-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-121">.NET Framework</span></span> |
| <span data-ttu-id="f0bf9-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="f0bf9-122">MSBuild.exe</span></span> | <span data-ttu-id="f0bf9-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-123">.NET Framework</span></span> |
| <span data-ttu-id="f0bf9-124">Mono üzerinde NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="f0bf9-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="f0bf9-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="f0bf9-126">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f0bf9-126">How does it work</span></span>

<span data-ttu-id="f0bf9-127">Üst düzey iş akışı aşağıdaki gibi açıklanabilir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="f0bf9-128">NuGet kullanılabilir eklentileri bulur.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="f0bf9-129">Uygun olduğunda NuGet, eklentileri öncelik sırasıyla yineleyebilir ve tek tek başlatır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="f0bf9-130">NuGet, isteğe hizmet veren ilk eklentiyi kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="f0bf9-131">Eklentiler artık gerekli olmadığında kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="f0bf9-132">Genel eklenti gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="f0bf9-132">General plugin requirements</span></span>

<span data-ttu-id="f0bf9-133">Geçerli protokol sürümü *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="f0bf9-134">Bu sürüm altında, gereksinimler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="f0bf9-135">Windows ve mono üzerinde çalışacak geçerli, güvenilir bir Authenticode imza Derlemeleriyle aynı.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="f0bf9-136">Henüz Linux ve Mac üzerinde çalıştırılan derlemeler için özel bir güven gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="f0bf9-137">İlgili sorun</span><span class="sxs-lookup"><span data-stu-id="f0bf9-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="f0bf9-138">NuGet istemci araçlarının geçerli güvenlik bağlamı altında durum bilgisiz başlatma desteği.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="f0bf9-139">Örneğin, NuGet istemci araçları daha sonra açıklanan eklenti protokolünün dışında yükseltme veya ek başlatma gerçekleştirmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="f0bf9-140">Açıkça belirtilmediği takdirde etkileşimli değil.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="f0bf9-141">Anlaşmalı eklenti Protokolü sürümüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="f0bf9-142">Makul bir zaman dönemi içindeki tüm isteklere yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="f0bf9-143">Devam eden tüm işlemler için iptal isteklerini dikkate alarak.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="f0bf9-144">Teknik belirtim aşağıdaki özelliklere göre daha ayrıntılı olarak açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="f0bf9-145">NuGet paketi Indirme eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="f0bf9-146">NuGet çapraz Plat kimlik doğrulama eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="f0bf9-147">İstemci-eklentisi etkileşimi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-147">Client - Plugin interaction</span></span>

<span data-ttu-id="f0bf9-148">NuGet istemci araçları ve eklentileri, JSON ile standart akışlar (stdin, stdout, stderr) üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="f0bf9-149">Tüm veriler UTF-8 kodlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="f0bf9-150">Eklentiler "-Plugin" bağımsız değişkeniyle başlatılır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="f0bf9-151">Bir Kullanıcı bu bağımsız değişken olmadan bir eklenti yürütülebiliri doğrudan başlattığında, eklenti bir protokol el sıkışması için beklemek yerine bilgilendirici bir ileti verebilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="f0bf9-152">Protokol el sıkışma zaman aşımı 5 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="f0bf9-153">Eklenti, kurulumu olabildiğince kısa bir süre içinde tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="f0bf9-154">NuGet istemci araçları, bir NuGet kaynağı için hizmet dizinini geçirerek bir eklentinin desteklenen işlemlerini sorgular.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="f0bf9-155">Bir eklenti desteklenen hizmet türlerinin varlığını denetlemek için hizmet dizinini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="f0bf9-156">NuGet istemci araçları ve eklentisi arasındaki iletişim çift yönlüdür.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="f0bf9-157">Her istekte 5 saniyelik bir zaman aşımı vardır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="f0bf9-158">İşlemlerin daha uzun sürme olması gerekiyorsa, isteğin zaman aşımına uğramasını engellemek için ilgili işlemin bir ilerleme iletisi göndermesi gerekir. 1 dakika sonra bir eklenti boşta kabul edilir ve kapatılır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="f0bf9-159">Eklenti yükleme ve bulma</span><span class="sxs-lookup"><span data-stu-id="f0bf9-159">Plugin installation and discovery</span></span>

<span data-ttu-id="f0bf9-160">Eklentiler, kural tabanlı bir dizin yapısı aracılığıyla keşfedilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="f0bf9-161">CI/CD senaryoları ve Power Users, davranışı geçersiz kılmak için ortam değişkenlerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="f0bf9-162">Ortam değişkenlerini kullanırken yalnızca mutlak yollara izin verilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="f0bf9-163">@No__t-0 ve `NUGET_NETCORE_PLUGIN_PATHS` ' in yalnızca NuGet araçları 'nın ve sonraki sürümlerin 5.3 + sürümü ile kullanılabildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="f0bf9-164">`NUGET_NETFX_PLUGIN_PATHS`-.NET Framework tabanlı araç (NuGet. exe/MSBuild. exe/Visual Studio) tarafından kullanılacak eklentileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="f0bf9-165">@No__t-0 ' a kadar önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="f0bf9-166">(Yalnızca NuGet sürümü 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="f0bf9-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="f0bf9-167">`NUGET_NETCORE_PLUGIN_PATHS`-.NET Core tabanlı araç (DotNet. exe) tarafından kullanılacak eklentileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="f0bf9-168">@No__t-0 ' a kadar önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="f0bf9-169">(Yalnızca NuGet sürümü 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="f0bf9-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="f0bf9-170">`NUGET_PLUGIN_PATHS`-bu NuGet işlemi için kullanılacak eklentileri tanımlar, öncelik korunur.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="f0bf9-171">Bu ortam değişkeni ayarlandıysa, kural tabanlı bulmayı geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="f0bf9-172">Çerçeveye özgü değişkenlerden biri belirtilmişse yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="f0bf9-173">@No__t-0 ' daki NuGet giriş konumu Kullanıcı konumu.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="f0bf9-174">Bu konum geçersiz kılınamaz.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-174">This location cannot be overriden.</span></span> <span data-ttu-id="f0bf9-175">.NET Core ve .NET Framework eklentileri için farklı bir kök dizin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="f0bf9-176">Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-176">Framework</span></span> | <span data-ttu-id="f0bf9-177">Kök bulma konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="f0bf9-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f0bf9-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="f0bf9-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="f0bf9-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="f0bf9-180">Her eklenti kendi klasörüne yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="f0bf9-181">Eklenti giriş noktası, yüklü klasörün adı, .NET Core için. dll uzantıları ve .NET Framework için. exe uzantısı olur.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="f0bf9-182">Şu anda eklentilerin yüklenmesi için Kullanıcı hikayesi yok.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="f0bf9-183">Gerekli dosyaları önceden belirlenmiş konuma taşımak basittir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="f0bf9-184">Desteklenen işlemler</span><span class="sxs-lookup"><span data-stu-id="f0bf9-184">Supported operations</span></span>

<span data-ttu-id="f0bf9-185">Yeni eklenti Protokolü altında iki işlem desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="f0bf9-186">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-186">Operation name</span></span> | <span data-ttu-id="f0bf9-187">En düşük protokol sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-187">Minimum protocol version</span></span> | <span data-ttu-id="f0bf9-188">En düşük NuGet istemci sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="f0bf9-189">Paketi indir</span><span class="sxs-lookup"><span data-stu-id="f0bf9-189">Download Package</span></span> | <span data-ttu-id="f0bf9-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f0bf9-190">1.0.0</span></span> | <span data-ttu-id="f0bf9-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="f0bf9-191">4.3.0</span></span> |
| [<span data-ttu-id="f0bf9-192">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="f0bf9-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="f0bf9-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="f0bf9-193">2.0.0</span></span> | <span data-ttu-id="f0bf9-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="f0bf9-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="f0bf9-195">Doğru çalışma zamanı altında eklenti çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f0bf9-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="f0bf9-196">DotNet. exe senaryolarında NuGet için, eklentiler DotNet. exe ' nin söz konusu çalışma zamanının altında yürütebilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="f0bf9-197">Bu, uyumlu bir DotNet. exe/eklenti birleşiminin kullanıldığından emin olmak için eklenti sağlayıcıdır ve tüketicidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="f0bf9-198">Örnek olarak, Kullanıcı-konum eklentilerine yönelik olası bir sorun oluşabilir. 2,0 çalışma zamanı altındaki bir DotNet. exe, 2,1 çalışma zamanı için yazılmış bir eklenti kullanmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="f0bf9-199">Özellikleri önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="f0bf9-199">Capabilities caching</span></span>

<span data-ttu-id="f0bf9-200">Eklentilerin güvenlik doğrulaması ve örnekleme maliyetlidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="f0bf9-201">İndirme işlemi kimlik doğrulama işleminden daha sık yapılır, ancak ortalama NuGet kullanıcısının yalnızca bir kimlik doğrulama eklentisine sahip olma olasılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="f0bf9-202">Bu deneyimi geliştirmek için, NuGet verilen istek için işlem taleplerini önbelleğe alacak.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="f0bf9-203">Bu önbellek, eklenti anahtarı eklenti yolu olacak şekilde eklenti başına ve bu özellik önbelleğinin süresi 30 gündür.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="f0bf9-204">Önbellek `%LocalAppData%/NuGet/plugins-cache` ' da bulunur ve `NUGET_PLUGINS_CACHE_PATH` ortam değişkeniyle geçersiz kılınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="f0bf9-205">Bu [önbelleği](../../consume-packages/managing-the-global-packages-and-cache-folders.md)temizlemek için, birisi `plugins-cache` seçeneğiyle Yereller komutunu çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="f0bf9-206">@No__t-0 Yereller seçeneği artık eklenti önbelleğini de silecek.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="f0bf9-207">Protokol iletileri dizini</span><span class="sxs-lookup"><span data-stu-id="f0bf9-207">Protocol messages index</span></span>

<span data-ttu-id="f0bf9-208">Protokol sürümü *1.0.0* iletileri:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="f0bf9-209">Close</span><span class="sxs-lookup"><span data-stu-id="f0bf9-209">Close</span></span>
    * <span data-ttu-id="f0bf9-210">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-211">İstek yük içermez</span><span class="sxs-lookup"><span data-stu-id="f0bf9-211">The request will contain no payload</span></span>
    * <span data-ttu-id="f0bf9-212">Yanıt beklenmez.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-212">No response is expected.</span></span>  <span data-ttu-id="f0bf9-213">Doğru yanıt, eklenti işleminin hemen çıkmak için gereken bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="f0bf9-214">Paketteki dosyaları Kopyala</span><span class="sxs-lookup"><span data-stu-id="f0bf9-214">Copy files in package</span></span>
    * <span data-ttu-id="f0bf9-215">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-216">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-216">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-217">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-217">the package ID and version</span></span>
        * <span data-ttu-id="f0bf9-218">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-218">the package source repository location</span></span>
        * <span data-ttu-id="f0bf9-219">hedef dizin yolu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-219">destination directory path</span></span>
        * <span data-ttu-id="f0bf9-220">paketteki hedef dizin yoluna kopyalanacak numaralandırılabilir dosyalar</span><span class="sxs-lookup"><span data-stu-id="f0bf9-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="f0bf9-221">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-221">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-222">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-223">işlem başarılı olduysa, hedef dizindeki kopyalanmış dosyalar için bir dizi tam yol</span><span class="sxs-lookup"><span data-stu-id="f0bf9-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="f0bf9-224">Paket dosyasını Kopyala (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="f0bf9-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="f0bf9-225">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-226">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-226">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-227">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-227">the package ID and version</span></span>
        * <span data-ttu-id="f0bf9-228">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-228">the package source repository location</span></span>
        * <span data-ttu-id="f0bf9-229">Hedef dosya yolu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-229">the destination file path</span></span>
    * <span data-ttu-id="f0bf9-230">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-230">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-231">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="f0bf9-232">Kimlik bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-232">Get credentials</span></span>
    * <span data-ttu-id="f0bf9-233">İstek yönü: eklenti > NuGet</span><span class="sxs-lookup"><span data-stu-id="f0bf9-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f0bf9-234">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-234">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-235">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-235">the package source repository location</span></span>
        * <span data-ttu-id="f0bf9-236">geçerli kimlik bilgileri kullanılarak paket kaynak deposundan alınan HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="f0bf9-237">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-237">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-238">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-239">varsa, bir Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-239">a username, if available</span></span>
        * <span data-ttu-id="f0bf9-240">bir parola varsa</span><span class="sxs-lookup"><span data-stu-id="f0bf9-240">a password, if available</span></span>

5.  <span data-ttu-id="f0bf9-241">Paketteki dosyaları al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-241">Get files in package</span></span>
    * <span data-ttu-id="f0bf9-242">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-243">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-243">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-244">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-244">the package ID and version</span></span>
        * <span data-ttu-id="f0bf9-245">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-245">the package source repository location</span></span>
    * <span data-ttu-id="f0bf9-246">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-246">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-247">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-248">işlem başarılı olursa paketteki dosya yollarının numaralandırılabilir olması</span><span class="sxs-lookup"><span data-stu-id="f0bf9-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="f0bf9-249">İşlem taleplerini al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-249">Get operation claims</span></span> 
    * <span data-ttu-id="f0bf9-250">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-251">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-251">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-252">paket kaynağı için hizmet dizini. JSON</span><span class="sxs-lookup"><span data-stu-id="f0bf9-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="f0bf9-253">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-253">the package source repository location</span></span>
    * <span data-ttu-id="f0bf9-254">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-254">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-255">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-256">işlem başarılı olduysa, desteklenen işlem sayısı (ör.: paket indirme).</span><span class="sxs-lookup"><span data-stu-id="f0bf9-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="f0bf9-257">Bir eklenti paket kaynağını desteklemiyorsa, eklenti boş bir desteklenen işlemler kümesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="f0bf9-258">Bu ileti, *2.0.0*sürümünde güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="f0bf9-259">Bu, geriye dönük uyumluluğu korumak için istemcsahiptir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="f0bf9-260">Paket karmasını al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-260">Get package hash</span></span>
    * <span data-ttu-id="f0bf9-261">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-262">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-262">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-263">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-263">the package ID and version</span></span>
        * <span data-ttu-id="f0bf9-264">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-264">the package source repository location</span></span>
        * <span data-ttu-id="f0bf9-265">karma algoritması</span><span class="sxs-lookup"><span data-stu-id="f0bf9-265">the hash algorithm</span></span>
    * <span data-ttu-id="f0bf9-266">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-266">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-267">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-268">işlem başarılı olduysa, istenen karma algoritmasını kullanan bir paket dosyası karması</span><span class="sxs-lookup"><span data-stu-id="f0bf9-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="f0bf9-269">Paket sürümlerini al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-269">Get package versions</span></span>
    * <span data-ttu-id="f0bf9-270">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-271">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-271">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-272">paket KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="f0bf9-272">the package ID</span></span>
        * <span data-ttu-id="f0bf9-273">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-273">the package source repository location</span></span>
    * <span data-ttu-id="f0bf9-274">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-274">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-275">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-276">işlem başarılı olduysa paket sürümleri Numaralandırılabilir</span><span class="sxs-lookup"><span data-stu-id="f0bf9-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="f0bf9-277">Hizmet dizinini al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-277">Get service index</span></span>
    * <span data-ttu-id="f0bf9-278">İstek yönü: eklenti > NuGet</span><span class="sxs-lookup"><span data-stu-id="f0bf9-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="f0bf9-279">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-279">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-280">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-280">the package source repository location</span></span>
    * <span data-ttu-id="f0bf9-281">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-281">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-282">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-283">işlem başarılı olduysa hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="f0bf9-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="f0bf9-284">Masını</span><span class="sxs-lookup"><span data-stu-id="f0bf9-284">Handshake</span></span>
     * <span data-ttu-id="f0bf9-285">İstek yönü: NuGet <-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="f0bf9-286">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-286">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-287">Geçerli eklenti Protokolü sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="f0bf9-288">desteklenen en düşük eklenti Protokolü sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="f0bf9-289">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-289">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-290">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="f0bf9-291">işlem başarılı olduysa, anlaşmalı protokol sürümü.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="f0bf9-292">Bir hata, eklentinin sonlandırılmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="f0bf9-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="f0bf9-293">Initialize</span></span>
     * <span data-ttu-id="f0bf9-294">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f0bf9-295">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-295">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-296">NuGet istemci aracı sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="f0bf9-297">NuGet istemci aracı etkin dili.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="f0bf9-298">Bu, kullanılıyorsa ForceEnglishOutput ayarını dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="f0bf9-299">varsayılan protokol varsayılan istek zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="f0bf9-300">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-300">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-301">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="f0bf9-302">Bir hata, eklentinin sonlandırılmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="f0bf9-303">Günlük</span><span class="sxs-lookup"><span data-stu-id="f0bf9-303">Log</span></span>
     * <span data-ttu-id="f0bf9-304">İstek yönü: eklenti > NuGet</span><span class="sxs-lookup"><span data-stu-id="f0bf9-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="f0bf9-305">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-305">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-306">istek için günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-306">the log level for the request</span></span>
         * <span data-ttu-id="f0bf9-307">günlüğe kaydedilecek ileti</span><span class="sxs-lookup"><span data-stu-id="f0bf9-307">a message to log</span></span>
     * <span data-ttu-id="f0bf9-308">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-308">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-309">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="f0bf9-310">NuGet işlemini izle çıkış çıkışı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="f0bf9-311">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f0bf9-312">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-312">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-313">NuGet işlem KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="f0bf9-313">the NuGet process ID</span></span>
     * <span data-ttu-id="f0bf9-314">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-314">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-315">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="f0bf9-316">Önceden getirme paketi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-316">Prefetch package</span></span>
     * <span data-ttu-id="f0bf9-317">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f0bf9-318">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-318">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-319">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="f0bf9-319">the package ID and version</span></span>
         * <span data-ttu-id="f0bf9-320">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-320">the package source repository location</span></span>
     * <span data-ttu-id="f0bf9-321">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-321">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-322">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="f0bf9-323">Kimlik bilgilerini ayarla</span><span class="sxs-lookup"><span data-stu-id="f0bf9-323">Set credentials</span></span>
     * <span data-ttu-id="f0bf9-324">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f0bf9-325">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-325">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-326">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-326">the package source repository location</span></span>
         * <span data-ttu-id="f0bf9-327">kullanılabiliyorsa, bilinen son paket kaynağı Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="f0bf9-328">kullanılabiliyorsa, bilinen son paket kaynak parolası</span><span class="sxs-lookup"><span data-stu-id="f0bf9-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="f0bf9-329">kullanılabiliyorsa, bilinen son Proxy Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="f0bf9-330">kullanılabiliyorsa, bilinen son proxy parolası</span><span class="sxs-lookup"><span data-stu-id="f0bf9-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="f0bf9-331">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-331">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-332">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="f0bf9-333">Günlük düzeyini ayarla</span><span class="sxs-lookup"><span data-stu-id="f0bf9-333">Set log level</span></span>
     * <span data-ttu-id="f0bf9-334">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="f0bf9-335">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-335">The request will contain:</span></span>
         * <span data-ttu-id="f0bf9-336">Varsayılan günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-336">the default log level</span></span>
     * <span data-ttu-id="f0bf9-337">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-337">A response will contain:</span></span>
         * <span data-ttu-id="f0bf9-338">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="f0bf9-339">Protokol sürümü *2.0.0* iletileri</span><span class="sxs-lookup"><span data-stu-id="f0bf9-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="f0bf9-340">Işlem taleplerini al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-340">Get Operation Claims</span></span>

* <span data-ttu-id="f0bf9-341">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="f0bf9-342">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-342">The request will contain:</span></span>
        * <span data-ttu-id="f0bf9-343">paket kaynağı için hizmet dizini. JSON</span><span class="sxs-lookup"><span data-stu-id="f0bf9-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="f0bf9-344">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-344">the package source repository location</span></span>
    * <span data-ttu-id="f0bf9-345">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-345">A response will contain:</span></span>
        * <span data-ttu-id="f0bf9-346">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="f0bf9-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="f0bf9-347">işlem başarılı olduysa, desteklenen işlem sayısı.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="f0bf9-348">Bir eklenti paket kaynağını desteklemiyorsa, eklenti boş bir desteklenen işlemler kümesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="f0bf9-349">Hizmet dizini ve paket kaynağı null ise, eklenti kimlik doğrulamasıyla yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="f0bf9-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="f0bf9-350">Kimlik doğrulama kimlik bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="f0bf9-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="f0bf9-351">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="f0bf9-352">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f0bf9-352">The request will contain:</span></span>
    * <span data-ttu-id="f0bf9-353">Kullanılmamışsa</span><span class="sxs-lookup"><span data-stu-id="f0bf9-353">Uri</span></span>
    * <span data-ttu-id="f0bf9-354">ısretry</span><span class="sxs-lookup"><span data-stu-id="f0bf9-354">isRetry</span></span>
    * <span data-ttu-id="f0bf9-355">Etkileşimsiz</span><span class="sxs-lookup"><span data-stu-id="f0bf9-355">NonInteractive</span></span>
    * <span data-ttu-id="f0bf9-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="f0bf9-356">CanShowDialog</span></span>
* <span data-ttu-id="f0bf9-357">Bir yanıt şunu içerir</span><span class="sxs-lookup"><span data-stu-id="f0bf9-357">A response will contain</span></span>
    * <span data-ttu-id="f0bf9-358">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="f0bf9-358">Username</span></span>
    * <span data-ttu-id="f0bf9-359">istemcisiyle yönetilen bir cihaz için)</span><span class="sxs-lookup"><span data-stu-id="f0bf9-359">Password</span></span>
    * <span data-ttu-id="f0bf9-360">İleti</span><span class="sxs-lookup"><span data-stu-id="f0bf9-360">Message</span></span>
    * <span data-ttu-id="f0bf9-361">Kimlik doğrulama türleri listesi</span><span class="sxs-lookup"><span data-stu-id="f0bf9-361">List of Auth Types</span></span>
    * <span data-ttu-id="f0bf9-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="f0bf9-362">MessageResponseCode</span></span>
