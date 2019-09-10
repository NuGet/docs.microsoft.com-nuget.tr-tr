---
title: NuGet platformlar arası eklentiler
description: NuGet. exe, DotNet. exe, MSBuild. exe ve Visual Studio için NuGet platformlar arası eklentileri
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815310"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="d9189-103">NuGet platformlar arası eklentiler</span><span class="sxs-lookup"><span data-stu-id="d9189-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="d9189-104">NuGet 4.8 + platformlar arası eklentiler için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="d9189-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="d9189-105">Bu, bir işlem kuralları kümesine uyması gereken yeni bir eklenti genişletilebilirlik modeli oluşturarak ile elde edildi.</span><span class="sxs-lookup"><span data-stu-id="d9189-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="d9189-106">Eklentiler, NuGet Istemcilerinin ayrı bir işlemde başlatması için kendi içinde bulunan yürütülebilir dosya (.NET Core World ' te çalıştırılabilir).</span><span class="sxs-lookup"><span data-stu-id="d9189-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="d9189-107">Bu bir kez doğru yazma, her yerde çalışan eklenti.</span><span class="sxs-lookup"><span data-stu-id="d9189-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="d9189-108">Bu, tüm NuGet istemci araçlarıyla çalışır.</span><span class="sxs-lookup"><span data-stu-id="d9189-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="d9189-109">Eklentiler .NET Framework (NuGet. exe, MSBuild. exe ve Visual Studio) ya da .NET Core (DotNet. exe) olabilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="d9189-110">NuGet Istemcisi ve eklentisi arasındaki sürümlü bir iletişim protokolü tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d9189-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="d9189-111">Başlangıç el sıkışması sırasında, 2 işlem protokol sürümü üzerinde anlaşacak.</span><span class="sxs-lookup"><span data-stu-id="d9189-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="d9189-112">Tüm NuGet istemci araçları senaryolarını kapsayacak şekilde, bunlardan biri hem .NET Framework hem de .NET Core eklentisine gerek duyar.</span><span class="sxs-lookup"><span data-stu-id="d9189-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="d9189-113">Aşağıda, eklentilerin istemci/çerçeve birleşimleri açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d9189-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="d9189-114">İstemci aracı</span><span class="sxs-lookup"><span data-stu-id="d9189-114">Client tool</span></span>  | <span data-ttu-id="d9189-115">Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="d9189-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d9189-116">Visual Studio</span></span> | <span data-ttu-id="d9189-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-117">.NET Framework</span></span> |
| <span data-ttu-id="d9189-118">DotNet. exe</span><span class="sxs-lookup"><span data-stu-id="d9189-118">dotnet.exe</span></span> | <span data-ttu-id="d9189-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d9189-119">.NET Core</span></span> |
| <span data-ttu-id="d9189-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="d9189-120">NuGet.exe</span></span> | <span data-ttu-id="d9189-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-121">.NET Framework</span></span> |
| <span data-ttu-id="d9189-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="d9189-122">MSBuild.exe</span></span> | <span data-ttu-id="d9189-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-123">.NET Framework</span></span> |
| <span data-ttu-id="d9189-124">Mono üzerinde NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="d9189-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="d9189-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="d9189-126">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="d9189-126">How does it work</span></span>

<span data-ttu-id="d9189-127">Üst düzey iş akışı aşağıdaki gibi açıklanabilir:</span><span class="sxs-lookup"><span data-stu-id="d9189-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="d9189-128">NuGet kullanılabilir eklentileri bulur.</span><span class="sxs-lookup"><span data-stu-id="d9189-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="d9189-129">Uygun olduğunda NuGet, eklentileri öncelik sırasıyla yineleyebilir ve tek tek başlatır.</span><span class="sxs-lookup"><span data-stu-id="d9189-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="d9189-130">NuGet, isteğe hizmet veren ilk eklentiyi kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9189-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="d9189-131">Eklentiler artık gerekli olmadığında kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="d9189-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="d9189-132">Genel eklenti gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="d9189-132">General plugin requirements</span></span>

<span data-ttu-id="d9189-133">Geçerli protokol sürümü *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="d9189-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="d9189-134">Bu sürüm altında, gereksinimler aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d9189-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="d9189-135">Windows ve mono üzerinde çalışacak geçerli, güvenilir bir Authenticode imza Derlemeleriyle aynı.</span><span class="sxs-lookup"><span data-stu-id="d9189-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="d9189-136">Henüz Linux ve Mac üzerinde çalıştırılan derlemeler için özel bir güven gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="d9189-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="d9189-137">İlgili sorun</span><span class="sxs-lookup"><span data-stu-id="d9189-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="d9189-138">NuGet istemci araçlarının geçerli güvenlik bağlamı altında durum bilgisiz başlatma desteği.</span><span class="sxs-lookup"><span data-stu-id="d9189-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="d9189-139">Örneğin, NuGet istemci araçları daha sonra açıklanan eklenti protokolünün dışında yükseltme veya ek başlatma gerçekleştirmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="d9189-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="d9189-140">Açıkça belirtilmediği takdirde etkileşimli değil.</span><span class="sxs-lookup"><span data-stu-id="d9189-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="d9189-141">Anlaşmalı eklenti Protokolü sürümüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="d9189-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="d9189-142">Makul bir zaman dönemi içindeki tüm isteklere yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="d9189-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="d9189-143">Devam eden tüm işlemler için iptal isteklerini dikkate alarak.</span><span class="sxs-lookup"><span data-stu-id="d9189-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="d9189-144">Teknik belirtim aşağıdaki özelliklere göre daha ayrıntılı olarak açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="d9189-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="d9189-145">NuGet paketi Indirme eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="d9189-146">NuGet çapraz Plat kimlik doğrulama eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="d9189-147">İstemci-eklentisi etkileşimi</span><span class="sxs-lookup"><span data-stu-id="d9189-147">Client - Plugin interaction</span></span>

<span data-ttu-id="d9189-148">NuGet istemci araçları ve eklentileri, JSON ile standart akışlar (stdin, stdout, stderr) üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="d9189-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="d9189-149">Tüm veriler UTF-8 kodlu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d9189-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="d9189-150">Eklentiler "-Plugin" bağımsız değişkeniyle başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d9189-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="d9189-151">Bir Kullanıcı bu bağımsız değişken olmadan bir eklenti yürütülebiliri doğrudan başlattığında, eklenti bir protokol el sıkışması için beklemek yerine bilgilendirici bir ileti verebilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="d9189-152">Protokol el sıkışma zaman aşımı 5 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="d9189-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="d9189-153">Eklenti, kurulumu olabildiğince kısa bir süre içinde tamamlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d9189-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="d9189-154">NuGet istemci araçları, bir NuGet kaynağı için hizmet dizinini geçirerek bir eklentinin desteklenen işlemlerini sorgular.</span><span class="sxs-lookup"><span data-stu-id="d9189-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="d9189-155">Bir eklenti desteklenen hizmet türlerinin varlığını denetlemek için hizmet dizinini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="d9189-156">NuGet istemci araçları ve eklentisi arasındaki iletişim çift yönlüdür.</span><span class="sxs-lookup"><span data-stu-id="d9189-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="d9189-157">Her istekte 5 saniyelik bir zaman aşımı vardır.</span><span class="sxs-lookup"><span data-stu-id="d9189-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="d9189-158">İşlemlerin daha uzun sürme olması gerekiyorsa, isteğin zaman aşımına uğramasını engellemek için ilgili işlemin bir ilerleme iletisi göndermesi gerekir. 1 dakika sonra bir eklenti boşta kabul edilir ve kapatılır.</span><span class="sxs-lookup"><span data-stu-id="d9189-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="d9189-159">Eklenti yükleme ve bulma</span><span class="sxs-lookup"><span data-stu-id="d9189-159">Plugin installation and discovery</span></span>

<span data-ttu-id="d9189-160">Eklentiler, kural tabanlı bir dizin yapısı aracılığıyla keşfedilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="d9189-161">CI/CD senaryoları ve Power Users, davranışı geçersiz kılmak için ortam değişkenlerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="d9189-162">Bu ve `NUGET_NETFX_PLUGIN_PATHS` `NUGET_NETCORE_PLUGIN_PATHS` yalnızca NuGet araçları 'nın ve sonraki sürümlerin 5.3 + sürümü ile kullanılabilir olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d9189-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="d9189-163">`NUGET_NETFX_PLUGIN_PATHS`-.NET Framework tabanlı araç (NuGet. exe/MSBuild. exe/Visual Studio) tarafından kullanılacak eklentileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d9189-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="d9189-164">`NUGET_PLUGIN_PATHS`Önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="d9189-165">(Yalnızca NuGet sürümü 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="d9189-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="d9189-166">`NUGET_NETCORE_PLUGIN_PATHS`-.NET Core tabanlı araç (DotNet. exe) tarafından kullanılacak eklentileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d9189-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="d9189-167">`NUGET_PLUGIN_PATHS`Önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="d9189-168">(Yalnızca NuGet sürümü 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="d9189-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="d9189-169">`NUGET_PLUGIN_PATHS`-Bu NuGet işlemi için kullanılacak eklentileri tanımlar, öncelik saklıdır.</span><span class="sxs-lookup"><span data-stu-id="d9189-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="d9189-170">Bu ortam değişkeni ayarlandıysa, kural tabanlı bulmayı geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="d9189-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="d9189-171">Çerçeveye özgü değişkenlerden biri belirtilmişse yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d9189-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="d9189-172">Kullanıcı konumu, içindeki `%UserProfile%/.nuget/plugins`NuGet giriş konumu.</span><span class="sxs-lookup"><span data-stu-id="d9189-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="d9189-173">Bu konum geçersiz kılınamaz.</span><span class="sxs-lookup"><span data-stu-id="d9189-173">This location cannot be overriden.</span></span> <span data-ttu-id="d9189-174">.NET Core ve .NET Framework eklentileri için farklı bir kök dizin kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d9189-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="d9189-175">Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-175">Framework</span></span> | <span data-ttu-id="d9189-176">Kök bulma konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="d9189-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d9189-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="d9189-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="d9189-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="d9189-179">Her eklenti kendi klasörüne yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="d9189-180">Eklenti giriş noktası, yüklü klasörün adı, .NET Core için. dll uzantıları ve .NET Framework için. exe uzantısı olur.</span><span class="sxs-lookup"><span data-stu-id="d9189-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="d9189-181">Şu anda eklentilerin yüklenmesi için Kullanıcı hikayesi yok.</span><span class="sxs-lookup"><span data-stu-id="d9189-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="d9189-182">Gerekli dosyaları önceden belirlenmiş konuma taşımak basittir.</span><span class="sxs-lookup"><span data-stu-id="d9189-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="d9189-183">Desteklenen işlemler</span><span class="sxs-lookup"><span data-stu-id="d9189-183">Supported operations</span></span>

<span data-ttu-id="d9189-184">Yeni eklenti Protokolü altında iki işlem desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d9189-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="d9189-185">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="d9189-185">Operation name</span></span> | <span data-ttu-id="d9189-186">En düşük protokol sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-186">Minimum protocol version</span></span> | <span data-ttu-id="d9189-187">En düşük NuGet istemci sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="d9189-188">Paketi indir</span><span class="sxs-lookup"><span data-stu-id="d9189-188">Download Package</span></span> | <span data-ttu-id="d9189-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="d9189-189">1.0.0</span></span> | <span data-ttu-id="d9189-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="d9189-190">4.3.0</span></span> |
| [<span data-ttu-id="d9189-191">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d9189-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="d9189-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="d9189-192">2.0.0</span></span> | <span data-ttu-id="d9189-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="d9189-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="d9189-194">Doğru çalışma zamanı altında eklenti çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d9189-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="d9189-195">DotNet. exe senaryolarında NuGet için, eklentiler DotNet. exe ' nin söz konusu çalışma zamanının altında yürütebilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="d9189-196">Bu, uyumlu bir DotNet. exe/eklenti birleşiminin kullanıldığından emin olmak için eklenti sağlayıcıdır ve tüketicidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="d9189-197">Örnek olarak, Kullanıcı-konum eklentilerine yönelik olası bir sorun oluşabilir. 2,0 çalışma zamanı altındaki bir DotNet. exe, 2,1 çalışma zamanı için yazılmış bir eklenti kullanmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="d9189-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="d9189-198">Özellikleri önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="d9189-198">Capabilities caching</span></span>

<span data-ttu-id="d9189-199">Eklentilerin güvenlik doğrulaması ve örnekleme maliyetlidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="d9189-200">İndirme işlemi kimlik doğrulama işleminden daha sık yapılır, ancak ortalama NuGet kullanıcısının yalnızca bir kimlik doğrulama eklentisine sahip olma olasılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="d9189-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="d9189-201">Bu deneyimi geliştirmek için, NuGet verilen istek için işlem taleplerini önbelleğe alacak.</span><span class="sxs-lookup"><span data-stu-id="d9189-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="d9189-202">Bu önbellek, eklenti anahtarı eklenti yolu olacak şekilde eklenti başına ve bu özellik önbelleğinin süresi 30 gündür.</span><span class="sxs-lookup"><span data-stu-id="d9189-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="d9189-203">Önbellek içinde `%LocalAppData%/NuGet/plugins-cache` bulunur ve ortam değişkeni `NUGET_PLUGINS_CACHE_PATH`ile geçersiz kılınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d9189-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="d9189-204">Bu [önbelleği](../../consume-packages/managing-the-global-packages-and-cache-folders.md)temizlemek için, bir tane, `plugins-cache` seçeneğiyle Yereller komutunu çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="d9189-205">`all` Yereller seçeneği artık eklenti önbelleğini de silecektir.</span><span class="sxs-lookup"><span data-stu-id="d9189-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="d9189-206">Protokol iletileri dizini</span><span class="sxs-lookup"><span data-stu-id="d9189-206">Protocol messages index</span></span>

<span data-ttu-id="d9189-207">Protokol sürümü *1.0.0* iletileri:</span><span class="sxs-lookup"><span data-stu-id="d9189-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="d9189-208">Close</span><span class="sxs-lookup"><span data-stu-id="d9189-208">Close</span></span>
    * <span data-ttu-id="d9189-209">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-210">İstek yük içermez</span><span class="sxs-lookup"><span data-stu-id="d9189-210">The request will contain no payload</span></span>
    * <span data-ttu-id="d9189-211">Yanıt beklenmez.</span><span class="sxs-lookup"><span data-stu-id="d9189-211">No response is expected.</span></span>  <span data-ttu-id="d9189-212">Doğru yanıt, eklenti işleminin hemen çıkmak için gereken bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d9189-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="d9189-213">Paketteki dosyaları Kopyala</span><span class="sxs-lookup"><span data-stu-id="d9189-213">Copy files in package</span></span>
    * <span data-ttu-id="d9189-214">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-215">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-215">The request will contain:</span></span>
        * <span data-ttu-id="d9189-216">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-216">the package ID and version</span></span>
        * <span data-ttu-id="d9189-217">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-217">the package source repository location</span></span>
        * <span data-ttu-id="d9189-218">hedef dizin yolu</span><span class="sxs-lookup"><span data-stu-id="d9189-218">destination directory path</span></span>
        * <span data-ttu-id="d9189-219">paketteki hedef dizin yoluna kopyalanacak numaralandırılabilir dosyalar</span><span class="sxs-lookup"><span data-stu-id="d9189-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="d9189-220">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-220">A response will contain:</span></span>
        * <span data-ttu-id="d9189-221">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-222">işlem başarılı olduysa, hedef dizindeki kopyalanmış dosyalar için bir dizi tam yol</span><span class="sxs-lookup"><span data-stu-id="d9189-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="d9189-223">Paket dosyasını Kopyala (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="d9189-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="d9189-224">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-225">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-225">The request will contain:</span></span>
        * <span data-ttu-id="d9189-226">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-226">the package ID and version</span></span>
        * <span data-ttu-id="d9189-227">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-227">the package source repository location</span></span>
        * <span data-ttu-id="d9189-228">Hedef dosya yolu</span><span class="sxs-lookup"><span data-stu-id="d9189-228">the destination file path</span></span>
    * <span data-ttu-id="d9189-229">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-229">A response will contain:</span></span>
        * <span data-ttu-id="d9189-230">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="d9189-231">Kimlik bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="d9189-231">Get credentials</span></span>
    * <span data-ttu-id="d9189-232">İstek yönü: eklenti > NuGet</span><span class="sxs-lookup"><span data-stu-id="d9189-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="d9189-233">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-233">The request will contain:</span></span>
        * <span data-ttu-id="d9189-234">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-234">the package source repository location</span></span>
        * <span data-ttu-id="d9189-235">geçerli kimlik bilgileri kullanılarak paket kaynak deposundan alınan HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="d9189-236">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-236">A response will contain:</span></span>
        * <span data-ttu-id="d9189-237">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-238">varsa, bir Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d9189-238">a username, if available</span></span>
        * <span data-ttu-id="d9189-239">bir parola varsa</span><span class="sxs-lookup"><span data-stu-id="d9189-239">a password, if available</span></span>

5.  <span data-ttu-id="d9189-240">Paketteki dosyaları al</span><span class="sxs-lookup"><span data-stu-id="d9189-240">Get files in package</span></span>
    * <span data-ttu-id="d9189-241">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-242">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-242">The request will contain:</span></span>
        * <span data-ttu-id="d9189-243">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-243">the package ID and version</span></span>
        * <span data-ttu-id="d9189-244">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-244">the package source repository location</span></span>
    * <span data-ttu-id="d9189-245">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-245">A response will contain:</span></span>
        * <span data-ttu-id="d9189-246">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-247">işlem başarılı olursa paketteki dosya yollarının numaralandırılabilir olması</span><span class="sxs-lookup"><span data-stu-id="d9189-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="d9189-248">İşlem taleplerini al</span><span class="sxs-lookup"><span data-stu-id="d9189-248">Get operation claims</span></span> 
    * <span data-ttu-id="d9189-249">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-250">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-250">The request will contain:</span></span>
        * <span data-ttu-id="d9189-251">paket kaynağı için hizmet dizini. JSON</span><span class="sxs-lookup"><span data-stu-id="d9189-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="d9189-252">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-252">the package source repository location</span></span>
    * <span data-ttu-id="d9189-253">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-253">A response will contain:</span></span>
        * <span data-ttu-id="d9189-254">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-255">işlem başarılı olduysa, desteklenen işlem sayısı (ör.: paket indirme).</span><span class="sxs-lookup"><span data-stu-id="d9189-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="d9189-256">Bir eklenti paket kaynağını desteklemiyorsa, eklenti boş bir desteklenen işlemler kümesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="d9189-257">Bu ileti, *2.0.0*sürümünde güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d9189-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="d9189-258">Bu, geriye dönük uyumluluğu korumak için istemcsahiptir.</span><span class="sxs-lookup"><span data-stu-id="d9189-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="d9189-259">Paket karmasını al</span><span class="sxs-lookup"><span data-stu-id="d9189-259">Get package hash</span></span>
    * <span data-ttu-id="d9189-260">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-261">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-261">The request will contain:</span></span>
        * <span data-ttu-id="d9189-262">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-262">the package ID and version</span></span>
        * <span data-ttu-id="d9189-263">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-263">the package source repository location</span></span>
        * <span data-ttu-id="d9189-264">karma algoritması</span><span class="sxs-lookup"><span data-stu-id="d9189-264">the hash algorithm</span></span>
    * <span data-ttu-id="d9189-265">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-265">A response will contain:</span></span>
        * <span data-ttu-id="d9189-266">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-267">işlem başarılı olduysa, istenen karma algoritmasını kullanan bir paket dosyası karması</span><span class="sxs-lookup"><span data-stu-id="d9189-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="d9189-268">Paket sürümlerini al</span><span class="sxs-lookup"><span data-stu-id="d9189-268">Get package versions</span></span>
    * <span data-ttu-id="d9189-269">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-270">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-270">The request will contain:</span></span>
        * <span data-ttu-id="d9189-271">paket KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="d9189-271">the package ID</span></span>
        * <span data-ttu-id="d9189-272">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-272">the package source repository location</span></span>
    * <span data-ttu-id="d9189-273">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-273">A response will contain:</span></span>
        * <span data-ttu-id="d9189-274">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-275">işlem başarılı olduysa paket sürümleri Numaralandırılabilir</span><span class="sxs-lookup"><span data-stu-id="d9189-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="d9189-276">Hizmet dizinini al</span><span class="sxs-lookup"><span data-stu-id="d9189-276">Get service index</span></span>
    * <span data-ttu-id="d9189-277">İstek yönü: eklenti > NuGet</span><span class="sxs-lookup"><span data-stu-id="d9189-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="d9189-278">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-278">The request will contain:</span></span>
        * <span data-ttu-id="d9189-279">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-279">the package source repository location</span></span>
    * <span data-ttu-id="d9189-280">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-280">A response will contain:</span></span>
        * <span data-ttu-id="d9189-281">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-282">işlem başarılı olduysa hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="d9189-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="d9189-283">Masını</span><span class="sxs-lookup"><span data-stu-id="d9189-283">Handshake</span></span>
     * <span data-ttu-id="d9189-284">İstek yönü:  NuGet < > eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="d9189-285">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-285">The request will contain:</span></span>
         * <span data-ttu-id="d9189-286">Geçerli eklenti Protokolü sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="d9189-287">desteklenen en düşük eklenti Protokolü sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="d9189-288">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-288">A response will contain:</span></span>
         * <span data-ttu-id="d9189-289">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="d9189-290">işlem başarılı olduysa, anlaşmalı protokol sürümü.</span><span class="sxs-lookup"><span data-stu-id="d9189-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="d9189-291">Bir hata, eklentinin sonlandırılmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="d9189-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="d9189-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="d9189-292">Initialize</span></span>
     * <span data-ttu-id="d9189-293">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d9189-294">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-294">The request will contain:</span></span>
         * <span data-ttu-id="d9189-295">NuGet istemci aracı sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="d9189-296">NuGet istemci aracı etkin dili.</span><span class="sxs-lookup"><span data-stu-id="d9189-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="d9189-297">Bu, kullanılıyorsa ForceEnglishOutput ayarını dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="d9189-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="d9189-298">varsayılan protokol varsayılan istek zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="d9189-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="d9189-299">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-299">A response will contain:</span></span>
         * <span data-ttu-id="d9189-300">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="d9189-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="d9189-301">Bir hata, eklentinin sonlandırılmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="d9189-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="d9189-302">Günlük</span><span class="sxs-lookup"><span data-stu-id="d9189-302">Log</span></span>
     * <span data-ttu-id="d9189-303">İstek yönü: eklenti > NuGet</span><span class="sxs-lookup"><span data-stu-id="d9189-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="d9189-304">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-304">The request will contain:</span></span>
         * <span data-ttu-id="d9189-305">istek için günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="d9189-305">the log level for the request</span></span>
         * <span data-ttu-id="d9189-306">günlüğe kaydedilecek ileti</span><span class="sxs-lookup"><span data-stu-id="d9189-306">a message to log</span></span>
     * <span data-ttu-id="d9189-307">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-307">A response will contain:</span></span>
         * <span data-ttu-id="d9189-308">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="d9189-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="d9189-309">NuGet işlemini izle çıkış çıkışı</span><span class="sxs-lookup"><span data-stu-id="d9189-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="d9189-310">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d9189-311">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-311">The request will contain:</span></span>
         * <span data-ttu-id="d9189-312">NuGet işlem KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="d9189-312">the NuGet process ID</span></span>
     * <span data-ttu-id="d9189-313">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-313">A response will contain:</span></span>
         * <span data-ttu-id="d9189-314">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="d9189-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="d9189-315">Önceden getirme paketi</span><span class="sxs-lookup"><span data-stu-id="d9189-315">Prefetch package</span></span>
     * <span data-ttu-id="d9189-316">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d9189-317">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-317">The request will contain:</span></span>
         * <span data-ttu-id="d9189-318">paket KIMLIĞI ve sürümü</span><span class="sxs-lookup"><span data-stu-id="d9189-318">the package ID and version</span></span>
         * <span data-ttu-id="d9189-319">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-319">the package source repository location</span></span>
     * <span data-ttu-id="d9189-320">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-320">A response will contain:</span></span>
         * <span data-ttu-id="d9189-321">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="d9189-322">Kimlik bilgilerini ayarla</span><span class="sxs-lookup"><span data-stu-id="d9189-322">Set credentials</span></span>
     * <span data-ttu-id="d9189-323">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d9189-324">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-324">The request will contain:</span></span>
         * <span data-ttu-id="d9189-325">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-325">the package source repository location</span></span>
         * <span data-ttu-id="d9189-326">kullanılabiliyorsa, bilinen son paket kaynağı Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d9189-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="d9189-327">kullanılabiliyorsa, bilinen son paket kaynak parolası</span><span class="sxs-lookup"><span data-stu-id="d9189-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="d9189-328">kullanılabiliyorsa, bilinen son Proxy Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d9189-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="d9189-329">kullanılabiliyorsa, bilinen son proxy parolası</span><span class="sxs-lookup"><span data-stu-id="d9189-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="d9189-330">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-330">A response will contain:</span></span>
         * <span data-ttu-id="d9189-331">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="d9189-332">Günlük düzeyini ayarla</span><span class="sxs-lookup"><span data-stu-id="d9189-332">Set log level</span></span>
     * <span data-ttu-id="d9189-333">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="d9189-334">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-334">The request will contain:</span></span>
         * <span data-ttu-id="d9189-335">Varsayılan günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="d9189-335">the default log level</span></span>
     * <span data-ttu-id="d9189-336">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-336">A response will contain:</span></span>
         * <span data-ttu-id="d9189-337">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="d9189-338">Protokol sürümü *2.0.0* iletileri</span><span class="sxs-lookup"><span data-stu-id="d9189-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="d9189-339">Işlem taleplerini al</span><span class="sxs-lookup"><span data-stu-id="d9189-339">Get Operation Claims</span></span>

* <span data-ttu-id="d9189-340">İstek yönü:  NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="d9189-341">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-341">The request will contain:</span></span>
        * <span data-ttu-id="d9189-342">paket kaynağı için hizmet dizini. JSON</span><span class="sxs-lookup"><span data-stu-id="d9189-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="d9189-343">paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="d9189-343">the package source repository location</span></span>
    * <span data-ttu-id="d9189-344">Bir yanıt şunu içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-344">A response will contain:</span></span>
        * <span data-ttu-id="d9189-345">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="d9189-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="d9189-346">işlem başarılı olduysa, desteklenen işlem sayısı.</span><span class="sxs-lookup"><span data-stu-id="d9189-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="d9189-347">Bir eklenti paket kaynağını desteklemiyorsa, eklenti boş bir desteklenen işlemler kümesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d9189-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="d9189-348">Hizmet dizini ve paket kaynağı null ise, eklenti kimlik doğrulamasıyla yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="d9189-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="d9189-349">Kimlik doğrulama kimlik bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="d9189-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="d9189-350">İstek yönü: NuGet-> eklentisi</span><span class="sxs-lookup"><span data-stu-id="d9189-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="d9189-351">Bu istek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d9189-351">The request will contain:</span></span>
    * <span data-ttu-id="d9189-352">Kullanılmamışsa</span><span class="sxs-lookup"><span data-stu-id="d9189-352">Uri</span></span>
    * <span data-ttu-id="d9189-353">ısretry</span><span class="sxs-lookup"><span data-stu-id="d9189-353">isRetry</span></span>
    * <span data-ttu-id="d9189-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d9189-354">NonInteractive</span></span>
    * <span data-ttu-id="d9189-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="d9189-355">CanShowDialog</span></span>
* <span data-ttu-id="d9189-356">Bir yanıt şunu içerir</span><span class="sxs-lookup"><span data-stu-id="d9189-356">A response will contain</span></span>
    * <span data-ttu-id="d9189-357">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d9189-357">Username</span></span>
    * <span data-ttu-id="d9189-358">Parola</span><span class="sxs-lookup"><span data-stu-id="d9189-358">Password</span></span>
    * <span data-ttu-id="d9189-359">`Message`</span><span class="sxs-lookup"><span data-stu-id="d9189-359">Message</span></span>
    * <span data-ttu-id="d9189-360">Kimlik doğrulama türleri listesi</span><span class="sxs-lookup"><span data-stu-id="d9189-360">List of Auth Types</span></span>
    * <span data-ttu-id="d9189-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="d9189-361">MessageResponseCode</span></span>
