---
title: NuGet çapraz platform eklentileri
description: NuGet.exe, dotnet.exe, msbuild.exe ve Visual Studio için NuGet çapraz platform eklentileri
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794206"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="006c5-103">NuGet çapraz platform eklentileri</span><span class="sxs-lookup"><span data-stu-id="006c5-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="006c5-104">Nuget'te 4.8 + çapraz platform eklentileri için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="006c5-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="006c5-105">Bu ile katı bir işlemin kuralları kümesi için uygun olan yeni bir eklenti genişletilebilirlik modeli, oluşturarak elde.</span><span class="sxs-lookup"><span data-stu-id="006c5-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="006c5-106">NuGet istemcileri ayrı bir işlemde başlatma bağımsız yürütülebilir (runnables) .NET Core dünyanın artırmasını.</span><span class="sxs-lookup"><span data-stu-id="006c5-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="006c5-107">Doğru yazma eklentisi her yerde çalıştırın bir kez budur.</span><span class="sxs-lookup"><span data-stu-id="006c5-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="006c5-108">NuGet istemci araçları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="006c5-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="006c5-109">Eklentileri, .NET Framework'ün (NuGet.exe, MSBuild.exe ve Visual Studio) ya da .NET Core (dotnet.exe) olabilir.</span><span class="sxs-lookup"><span data-stu-id="006c5-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="006c5-110">NuGet istemci ile eklenti arasındaki tutulan iletişim protokolü tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="006c5-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="006c5-111">Başlangıç anlaşması sırasında Protokolü sürüm 2 işlemleri anlaşır.</span><span class="sxs-lookup"><span data-stu-id="006c5-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="006c5-112">Tüm NuGet istemci araçları senaryolarınızı kapsaması için bir .NET Framework hem de .NET Core eklentisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="006c5-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="006c5-113">Aşağıdaki eklenti istemci/framework birleşimlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="006c5-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="006c5-114">İstemci aracı</span><span class="sxs-lookup"><span data-stu-id="006c5-114">Client tool</span></span>  | <span data-ttu-id="006c5-115">Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="006c5-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="006c5-116">Visual Studio</span></span> | <span data-ttu-id="006c5-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-117">.NET Framework</span></span> |
| <span data-ttu-id="006c5-118">DotNet.exe</span><span class="sxs-lookup"><span data-stu-id="006c5-118">dotnet.exe</span></span> | <span data-ttu-id="006c5-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="006c5-119">.NET Core</span></span> |
| <span data-ttu-id="006c5-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="006c5-120">NuGet.exe</span></span> | <span data-ttu-id="006c5-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-121">.NET Framework</span></span> |
| <span data-ttu-id="006c5-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="006c5-122">MSBuild.exe</span></span> | <span data-ttu-id="006c5-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-123">.NET Framework</span></span> |
| <span data-ttu-id="006c5-124">NuGet.exe Mono üzerinde</span><span class="sxs-lookup"><span data-stu-id="006c5-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="006c5-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="006c5-126">Nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="006c5-126">How does it work</span></span>

<span data-ttu-id="006c5-127">Üst düzey iş akışı şu şekilde açıklanabilir:</span><span class="sxs-lookup"><span data-stu-id="006c5-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="006c5-128">NuGet, kullanılabilir eklentiler bulur.</span><span class="sxs-lookup"><span data-stu-id="006c5-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="006c5-129">Uygun olduğunda NuGet öncelik sırasına ve başlar birer birer eklentileri üzerinden yineleme yapma.</span><span class="sxs-lookup"><span data-stu-id="006c5-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="006c5-130">NuGet, istek servis edebilirsiniz ilk eklenti kullanır.</span><span class="sxs-lookup"><span data-stu-id="006c5-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="006c5-131">Artık gerekli olmadığında eklentileri kapatılır.</span><span class="sxs-lookup"><span data-stu-id="006c5-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="006c5-132">Genel eklentisi gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="006c5-132">General plugin requirements</span></span>

<span data-ttu-id="006c5-133">Geçerli protokol sürümü *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="006c5-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="006c5-134">Bu sürümü'nün altında gereksinimleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="006c5-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="006c5-135">Windows ve Mono üzerinde çalışacak bir geçerli ve güvenilen Authenticode imzası derlemeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="006c5-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="006c5-136">Linux ve Mac henüz çalışan derlemeler için özel güven gereksinimi yoktur.</span><span class="sxs-lookup"><span data-stu-id="006c5-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="006c5-137">İlgili sorun</span><span class="sxs-lookup"><span data-stu-id="006c5-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="006c5-138">NuGet istemci Araçları'nın geçerli güvenlik bağlamı altında durum bilgisi olmayan başlatma destekler.</span><span class="sxs-lookup"><span data-stu-id="006c5-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="006c5-139">Örneğin, NuGet istemci araçlarını yükseltme veya daha sonra açıklanan eklenti Protokolü dışında ek başlatma gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="006c5-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="006c5-140">Açıkça belirtilmediği sürece olmayan etkileşimli olması.</span><span class="sxs-lookup"><span data-stu-id="006c5-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="006c5-141">Üzerinde anlaşılan eklentisini protokolü sürümüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="006c5-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="006c5-142">Tüm istekler için makul bir süre içinde yanıt.</span><span class="sxs-lookup"><span data-stu-id="006c5-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="006c5-143">Tüm devam eden işlemi iptal isteklerini dikkate.</span><span class="sxs-lookup"><span data-stu-id="006c5-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="006c5-144">Teknik belirtim aşağıdaki özellikleri daha ayrıntılı açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="006c5-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="006c5-145">NuGet paketini indirme eklentisi</span><span class="sxs-lookup"><span data-stu-id="006c5-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="006c5-146">NuGet kimlik doğrulama eklentisini plat çapraz</span><span class="sxs-lookup"><span data-stu-id="006c5-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="006c5-147">İstemci - eklentisi etkileşimi</span><span class="sxs-lookup"><span data-stu-id="006c5-147">Client - Plugin interaction</span></span>

<span data-ttu-id="006c5-148">NuGet istemci araçları ve eklentileri ile JSON standart akış (stdin, stdout, stderr) iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="006c5-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="006c5-149">Tüm verileri UTF-8 olarak kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="006c5-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="006c5-150">Eklenti bağımsız değişkeniyle başlatılır "-eklentisi".</span><span class="sxs-lookup"><span data-stu-id="006c5-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="006c5-151">Kullanıcı doğrudan bu bağımsız değişken yürütülebilir bir eklenti başlatır durumunda, eklenti için bir protokol anlaşması beklemek yerine bilgilendirici bir ileti verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="006c5-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="006c5-152">Protokol anlaşması zaman aşımı, 5 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="006c5-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="006c5-153">Eklenti, mümkün olduğunca bir miktar eksikliği kurulum olarak tamamlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="006c5-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="006c5-154">NuGet istemci araçları NuGet kaynağı için hizmet dizini geçirerek bir eklenti'nın desteklenen işlemler sorgular.</span><span class="sxs-lookup"><span data-stu-id="006c5-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="006c5-155">Bir eklenti için desteklenen hizmet türlerinin varlığını denetlemek için hizmet dizini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="006c5-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="006c5-156">NuGet istemci araçları ile eklenti arasındaki iletişim çift yönlü ' dir.</span><span class="sxs-lookup"><span data-stu-id="006c5-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="006c5-157">Her isteğin 5 saniyelik bir zaman aşımı vardır.</span><span class="sxs-lookup"><span data-stu-id="006c5-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="006c5-158">İşlemleri daha uzun sürer istemiyorsanız ilgili işlem istek zaman aşımına uğramadan engellemek için bir ilerleme iletisi göndermesi gerekir. 1 dakika kaldıktan sonra bir eklenti boşta kabul edilip kapatılır.</span><span class="sxs-lookup"><span data-stu-id="006c5-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="006c5-159">Eklenti yükleme ve bulma</span><span class="sxs-lookup"><span data-stu-id="006c5-159">Plugin installation and discovery</span></span>

<span data-ttu-id="006c5-160">Eklentileri tabanlı bir dizin yapısı bulunacaktır.</span><span class="sxs-lookup"><span data-stu-id="006c5-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="006c5-161">CI/CD senaryoları ve ileri kullanıcılar bir ortam değişkeni davranışı geçersiz kılmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="006c5-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="006c5-162">`NUGET_PLUGIN_PATHS` -ayrılmış öncelik o NuGet işlemi için kullanılacak eklentileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="006c5-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="006c5-163">Bu ortam değişkenine ayarlanmışsa tabanlı bulma geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="006c5-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="006c5-164">Kullanıcı konumu, NuGet giriş konumda `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="006c5-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="006c5-165">Bu konum, geçersiz kılınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="006c5-165">This location cannot be overriden.</span></span> <span data-ttu-id="006c5-166">.NET Core ve .NET Framework eklenti için farklı bir kök dizini kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="006c5-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="006c5-167">Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-167">Framework</span></span> | <span data-ttu-id="006c5-168">Bulma kökü</span><span class="sxs-lookup"><span data-stu-id="006c5-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="006c5-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="006c5-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="006c5-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="006c5-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="006c5-171">Her eklentinin kendi klasöründe yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="006c5-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="006c5-172">Eklentisi giriş noktası adı yüklü klasöründe .dll uzantılar için .NET Core ve .NET Framework için .exe uzantısına sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="006c5-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="006c5-173">Şu anda hiçbir kullanıcı hikayesi için eklenti yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="006c5-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="006c5-174">Gerekli dosyaları önceden belirlenmiş konuma hareket ettirmek kadar basittir.</span><span class="sxs-lookup"><span data-stu-id="006c5-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="006c5-175">Desteklenen işlemler</span><span class="sxs-lookup"><span data-stu-id="006c5-175">Supported operations</span></span>

<span data-ttu-id="006c5-176">İki işlem altında yeni eklenti Protokolü desteklenir.</span><span class="sxs-lookup"><span data-stu-id="006c5-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="006c5-177">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="006c5-177">Operation name</span></span> | <span data-ttu-id="006c5-178">En düşük protokol sürümü</span><span class="sxs-lookup"><span data-stu-id="006c5-178">Minimum protocol version</span></span> | <span data-ttu-id="006c5-179">En düşük NuGet istemci sürümü</span><span class="sxs-lookup"><span data-stu-id="006c5-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="006c5-180">Paketini indirme</span><span class="sxs-lookup"><span data-stu-id="006c5-180">Download Package</span></span> | <span data-ttu-id="006c5-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="006c5-181">1.0.0</span></span> | <span data-ttu-id="006c5-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="006c5-182">4.3.0</span></span> |
| [<span data-ttu-id="006c5-183">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="006c5-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="006c5-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="006c5-184">2.0.0</span></span> | <span data-ttu-id="006c5-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="006c5-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="006c5-186">Eklentileri doğru çalışma zamanı altında çalışan</span><span class="sxs-lookup"><span data-stu-id="006c5-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="006c5-187">Bu belirli dotnet.exe çalışma zamanı altında yürütebilmek için eklentileri dotnet.exe senaryolarda NuGet için gerekir.</span><span class="sxs-lookup"><span data-stu-id="006c5-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="006c5-188">Bu uyumlu dotnet.exe/plugin birlikte kullanılan emin olmak için eklenti sağlayıcısı ve tüketici üzerinde olur.</span><span class="sxs-lookup"><span data-stu-id="006c5-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="006c5-189">Olası bir sorun meydana gelebilecek kullanıcı konumu eklenti ile olduğunda, örneğin, 2.0 çalışma zamanı altında bir dotnet.exe 2.1 çalışma zamanı için yazılan bir eklenti kullanmayı dener.</span><span class="sxs-lookup"><span data-stu-id="006c5-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="006c5-190">Önbelleğe alma özellikleri</span><span class="sxs-lookup"><span data-stu-id="006c5-190">Capabilities caching</span></span>

<span data-ttu-id="006c5-191">Güvenlik doğrulaması ve eklentileri örneğinin pahalı.</span><span class="sxs-lookup"><span data-stu-id="006c5-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="006c5-192">İndirme işlemi, ancak ortalama NuGet kullanıcının yalnızca bir kimlik doğrulama eklentisini olasılığı kimlik doğrulama işlemi, daha sık gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="006c5-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="006c5-193">NuGet deneyimini iyileştirmek üzere belirtilen istek için işlem talepleri önbelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="006c5-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="006c5-194">Bu önbellek eklentisi eklentisi yolu olan eklentisi anahtarı ile ve bu özellikleri önbellek için sona erme 30 gündür.</span><span class="sxs-lookup"><span data-stu-id="006c5-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="006c5-195">Önbellek bulunan `%LocalAppData%/NuGet/plugins-cache` ve ortam değişkeni ile geçersiz kılınmış `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="006c5-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="006c5-196">Bu temizlemek için [önbellek](../../consume-packages/managing-the-global-packages-and-cache-folders.md), bir yerel öğeler çalıştırabilirsiniz komutunu `plugins-cache` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="006c5-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="006c5-197">`all` Yereller seçeneği artık da silinir plugins önbellek.</span><span class="sxs-lookup"><span data-stu-id="006c5-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="006c5-198">İletişim kuralı iletileri dizini</span><span class="sxs-lookup"><span data-stu-id="006c5-198">Protocol messages index</span></span>

<span data-ttu-id="006c5-199">Protokol sürümü *1.0.0* iletileri:</span><span class="sxs-lookup"><span data-stu-id="006c5-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="006c5-200">Close</span><span class="sxs-lookup"><span data-stu-id="006c5-200">Close</span></span>
    * <span data-ttu-id="006c5-201">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-202">İstek yükü yok içerir</span><span class="sxs-lookup"><span data-stu-id="006c5-202">The request will contain no payload</span></span>
    * <span data-ttu-id="006c5-203">Yanıt bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="006c5-203">No response is expected.</span></span>  <span data-ttu-id="006c5-204">Doğru yanıtı hemen çıkılmasına eklentisi için işlemidir.</span><span class="sxs-lookup"><span data-stu-id="006c5-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="006c5-205">Paketteki dosyaları Kopyala</span><span class="sxs-lookup"><span data-stu-id="006c5-205">Copy files in package</span></span>
    * <span data-ttu-id="006c5-206">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-207">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-207">The request will contain:</span></span>
        * <span data-ttu-id="006c5-208">paket kimliği ve sürüm</span><span class="sxs-lookup"><span data-stu-id="006c5-208">the package ID and version</span></span>
        * <span data-ttu-id="006c5-209">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-209">the package source repository location</span></span>
        * <span data-ttu-id="006c5-210">Hedef dizin yolu</span><span class="sxs-lookup"><span data-stu-id="006c5-210">destination directory path</span></span>
        * <span data-ttu-id="006c5-211">numaralandırılabilir bir hedef dizin yolu kopyalanacak paket dosyaları</span><span class="sxs-lookup"><span data-stu-id="006c5-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="006c5-212">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-212">A response will contain:</span></span>
        * <span data-ttu-id="006c5-213">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-214">İşlem başarılı ise hedef dizinde kopyalanan dosyaların tam yollarının bir numaralandırılabilir</span><span class="sxs-lookup"><span data-stu-id="006c5-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="006c5-215">Paket dosyası (.nupkg) kopyalayın</span><span class="sxs-lookup"><span data-stu-id="006c5-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="006c5-216">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-217">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-217">The request will contain:</span></span>
        * <span data-ttu-id="006c5-218">paket kimliği ve sürüm</span><span class="sxs-lookup"><span data-stu-id="006c5-218">the package ID and version</span></span>
        * <span data-ttu-id="006c5-219">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-219">the package source repository location</span></span>
        * <span data-ttu-id="006c5-220">Hedef dosya yolu</span><span class="sxs-lookup"><span data-stu-id="006c5-220">the destination file path</span></span>
    * <span data-ttu-id="006c5-221">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-221">A response will contain:</span></span>
        * <span data-ttu-id="006c5-222">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="006c5-223">Kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="006c5-223">Get credentials</span></span>
    * <span data-ttu-id="006c5-224">Yön istek: eklenti NuGet -></span><span class="sxs-lookup"><span data-stu-id="006c5-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="006c5-225">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-225">The request will contain:</span></span>
        * <span data-ttu-id="006c5-226">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-226">the package source repository location</span></span>
        * <span data-ttu-id="006c5-227">Geçerli kimlik bilgilerini kullanarak paket kaynak deposundan alınan HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="006c5-228">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-228">A response will contain:</span></span>
        * <span data-ttu-id="006c5-229">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-230">varsa bir kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="006c5-230">a username, if available</span></span>
        * <span data-ttu-id="006c5-231">varsa bir parola</span><span class="sxs-lookup"><span data-stu-id="006c5-231">a password, if available</span></span>

5.  <span data-ttu-id="006c5-232">Paketteki dosyaları Al</span><span class="sxs-lookup"><span data-stu-id="006c5-232">Get files in package</span></span>
    * <span data-ttu-id="006c5-233">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-234">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-234">The request will contain:</span></span>
        * <span data-ttu-id="006c5-235">paket kimliği ve sürüm</span><span class="sxs-lookup"><span data-stu-id="006c5-235">the package ID and version</span></span>
        * <span data-ttu-id="006c5-236">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-236">the package source repository location</span></span>
    * <span data-ttu-id="006c5-237">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-237">A response will contain:</span></span>
        * <span data-ttu-id="006c5-238">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-239">İşlem başarılı olduysa, paketteki dosya yollarının bir numaralandırılabilir</span><span class="sxs-lookup"><span data-stu-id="006c5-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="006c5-240">İşlem talebi alır</span><span class="sxs-lookup"><span data-stu-id="006c5-240">Get operation claims</span></span> 
    * <span data-ttu-id="006c5-241">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-242">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-242">The request will contain:</span></span>
        * <span data-ttu-id="006c5-243">Paket kaynağı için hizmet index.json</span><span class="sxs-lookup"><span data-stu-id="006c5-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="006c5-244">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-244">the package source repository location</span></span>
    * <span data-ttu-id="006c5-245">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-245">A response will contain:</span></span>
        * <span data-ttu-id="006c5-246">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-247">numaralandırılabilir, desteklenen işlemler (örn: paket yükleme) işlemi başarılı olursa.</span><span class="sxs-lookup"><span data-stu-id="006c5-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="006c5-248">Eklenti, bir eklenti paket kaynağı desteklemiyorsa boş bir desteklenen işlemler kümesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="006c5-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="006c5-249">Bu ileti sürümünde güncelleştirildi *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="006c5-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="006c5-250">Geriye dönük uyumluluğu korumak için istemcide var.</span><span class="sxs-lookup"><span data-stu-id="006c5-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="006c5-251">Paket karmasını alır</span><span class="sxs-lookup"><span data-stu-id="006c5-251">Get package hash</span></span>
    * <span data-ttu-id="006c5-252">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-253">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-253">The request will contain:</span></span>
        * <span data-ttu-id="006c5-254">paket kimliği ve sürüm</span><span class="sxs-lookup"><span data-stu-id="006c5-254">the package ID and version</span></span>
        * <span data-ttu-id="006c5-255">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-255">the package source repository location</span></span>
        * <span data-ttu-id="006c5-256">karma algoritması</span><span class="sxs-lookup"><span data-stu-id="006c5-256">the hash algorithm</span></span>
    * <span data-ttu-id="006c5-257">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-257">A response will contain:</span></span>
        * <span data-ttu-id="006c5-258">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-259">İşlem başarılı olursa, istenen karma algoritması kullanarak bir paket dosya karması</span><span class="sxs-lookup"><span data-stu-id="006c5-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="006c5-260">Paket sürümü alma</span><span class="sxs-lookup"><span data-stu-id="006c5-260">Get package versions</span></span>
    * <span data-ttu-id="006c5-261">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-262">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-262">The request will contain:</span></span>
        * <span data-ttu-id="006c5-263">paket kimliği</span><span class="sxs-lookup"><span data-stu-id="006c5-263">the package ID</span></span>
        * <span data-ttu-id="006c5-264">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-264">the package source repository location</span></span>
    * <span data-ttu-id="006c5-265">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-265">A response will contain:</span></span>
        * <span data-ttu-id="006c5-266">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-267">numaralandırılabilir işlemi başarılı olursa, paket sürümleri</span><span class="sxs-lookup"><span data-stu-id="006c5-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="006c5-268">Hizmet dizini alın</span><span class="sxs-lookup"><span data-stu-id="006c5-268">Get service index</span></span>
    * <span data-ttu-id="006c5-269">Yön istek: eklenti NuGet -></span><span class="sxs-lookup"><span data-stu-id="006c5-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="006c5-270">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-270">The request will contain:</span></span>
        * <span data-ttu-id="006c5-271">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-271">the package source repository location</span></span>
    * <span data-ttu-id="006c5-272">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-272">A response will contain:</span></span>
        * <span data-ttu-id="006c5-273">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-274">İşlem başarılı ise hizmet dizini</span><span class="sxs-lookup"><span data-stu-id="006c5-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="006c5-275">Anlaşması</span><span class="sxs-lookup"><span data-stu-id="006c5-275">Handshake</span></span>
     * <span data-ttu-id="006c5-276">Yön istek: NuGet <> – eklentisi</span><span class="sxs-lookup"><span data-stu-id="006c5-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="006c5-277">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-277">The request will contain:</span></span>
         * <span data-ttu-id="006c5-278">Geçerli eklentisi protokolü sürümü</span><span class="sxs-lookup"><span data-stu-id="006c5-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="006c5-279">desteklenen en düşük eklentisi protokol sürümü</span><span class="sxs-lookup"><span data-stu-id="006c5-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="006c5-280">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-280">A response will contain:</span></span>
         * <span data-ttu-id="006c5-281">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="006c5-282">İşlem başarılı olduysa anlaşılan protokol sürümü.</span><span class="sxs-lookup"><span data-stu-id="006c5-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="006c5-283">Bir hata eklenti sonlandırmada neden olur.</span><span class="sxs-lookup"><span data-stu-id="006c5-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="006c5-284">başlatma</span><span class="sxs-lookup"><span data-stu-id="006c5-284">Initialize</span></span>
     * <span data-ttu-id="006c5-285">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="006c5-286">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-286">The request will contain:</span></span>
         * <span data-ttu-id="006c5-287">NuGet istemci aracı sürümü</span><span class="sxs-lookup"><span data-stu-id="006c5-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="006c5-288">NuGet istemci aracı geçerli dili.</span><span class="sxs-lookup"><span data-stu-id="006c5-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="006c5-289">Bu dikkate ForceEnglishOutput ayarı kullandıysanız alır.</span><span class="sxs-lookup"><span data-stu-id="006c5-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="006c5-290">protokol varsayılan yerini varsayılan isteği zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="006c5-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="006c5-291">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-291">A response will contain:</span></span>
         * <span data-ttu-id="006c5-292">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="006c5-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="006c5-293">Bir hata eklenti sonlandırmada neden olur.</span><span class="sxs-lookup"><span data-stu-id="006c5-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="006c5-294">Günlük</span><span class="sxs-lookup"><span data-stu-id="006c5-294">Log</span></span>
     * <span data-ttu-id="006c5-295">Yön istek: eklenti NuGet -></span><span class="sxs-lookup"><span data-stu-id="006c5-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="006c5-296">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-296">The request will contain:</span></span>
         * <span data-ttu-id="006c5-297">istek için günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="006c5-297">the log level for the request</span></span>
         * <span data-ttu-id="006c5-298">günlüğe kaydedilecek iletinin</span><span class="sxs-lookup"><span data-stu-id="006c5-298">a message to log</span></span>
     * <span data-ttu-id="006c5-299">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-299">A response will contain:</span></span>
         * <span data-ttu-id="006c5-300">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="006c5-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="006c5-301">İzleyici NuGet işlem çıkışı</span><span class="sxs-lookup"><span data-stu-id="006c5-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="006c5-302">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="006c5-303">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-303">The request will contain:</span></span>
         * <span data-ttu-id="006c5-304">NuGet işlem kimliği</span><span class="sxs-lookup"><span data-stu-id="006c5-304">the NuGet process ID</span></span>
     * <span data-ttu-id="006c5-305">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-305">A response will contain:</span></span>
         * <span data-ttu-id="006c5-306">işlemin sonucunu gösteren bir yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="006c5-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="006c5-307">Paket Hazırlık</span><span class="sxs-lookup"><span data-stu-id="006c5-307">Prefetch package</span></span>
     * <span data-ttu-id="006c5-308">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="006c5-309">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-309">The request will contain:</span></span>
         * <span data-ttu-id="006c5-310">paket kimliği ve sürüm</span><span class="sxs-lookup"><span data-stu-id="006c5-310">the package ID and version</span></span>
         * <span data-ttu-id="006c5-311">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-311">the package source repository location</span></span>
     * <span data-ttu-id="006c5-312">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-312">A response will contain:</span></span>
         * <span data-ttu-id="006c5-313">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="006c5-314">Kimlik bilgilerini ayarla</span><span class="sxs-lookup"><span data-stu-id="006c5-314">Set credentials</span></span>
     * <span data-ttu-id="006c5-315">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="006c5-316">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-316">The request will contain:</span></span>
         * <span data-ttu-id="006c5-317">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-317">the package source repository location</span></span>
         * <span data-ttu-id="006c5-318">Son bilinen paket kaynağı kullanıcı adı, mevcutsa</span><span class="sxs-lookup"><span data-stu-id="006c5-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="006c5-319">Son bilinen paket kaynağı parolası, mevcutsa</span><span class="sxs-lookup"><span data-stu-id="006c5-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="006c5-320">Son bilinen proxy kullanıcı adı, mevcutsa</span><span class="sxs-lookup"><span data-stu-id="006c5-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="006c5-321">Son bilinen bir ara sunucu parolasını, mevcutsa</span><span class="sxs-lookup"><span data-stu-id="006c5-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="006c5-322">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-322">A response will contain:</span></span>
         * <span data-ttu-id="006c5-323">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="006c5-324">Günlük düzeyini ayarlama</span><span class="sxs-lookup"><span data-stu-id="006c5-324">Set log level</span></span>
     * <span data-ttu-id="006c5-325">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="006c5-326">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-326">The request will contain:</span></span>
         * <span data-ttu-id="006c5-327">Varsayılan günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="006c5-327">the default log level</span></span>
     * <span data-ttu-id="006c5-328">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-328">A response will contain:</span></span>
         * <span data-ttu-id="006c5-329">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="006c5-330">Protokol sürümü *2.0.0* iletileri</span><span class="sxs-lookup"><span data-stu-id="006c5-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="006c5-331">İşlem talebi alır</span><span class="sxs-lookup"><span data-stu-id="006c5-331">Get Operation Claims</span></span>

* <span data-ttu-id="006c5-332">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="006c5-333">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-333">The request will contain:</span></span>
        * <span data-ttu-id="006c5-334">Paket kaynağı için hizmet index.json</span><span class="sxs-lookup"><span data-stu-id="006c5-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="006c5-335">Paket kaynağı depo konumu</span><span class="sxs-lookup"><span data-stu-id="006c5-335">the package source repository location</span></span>
    * <span data-ttu-id="006c5-336">Bir yanıt içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-336">A response will contain:</span></span>
        * <span data-ttu-id="006c5-337">işlemin sonucunu gösteren bir yanıt kodu</span><span class="sxs-lookup"><span data-stu-id="006c5-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="006c5-338">bir numaralandırma işlemi başarılı olursa, desteklenen işlemler.</span><span class="sxs-lookup"><span data-stu-id="006c5-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="006c5-339">Eklenti, bir eklenti paket kaynağı desteklemiyorsa boş bir desteklenen işlemler kümesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="006c5-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="006c5-340">Hizmet dizini ve paket kaynağı null ise, eklenti ile kimlik doğrulaması yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="006c5-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="006c5-341">Kimlik doğrulama kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="006c5-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="006c5-342">Yön istek: NuGet eklentisi -></span><span class="sxs-lookup"><span data-stu-id="006c5-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="006c5-343">İstek içerir:</span><span class="sxs-lookup"><span data-stu-id="006c5-343">The request will contain:</span></span>
    * <span data-ttu-id="006c5-344">URI</span><span class="sxs-lookup"><span data-stu-id="006c5-344">Uri</span></span>
    * <span data-ttu-id="006c5-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="006c5-345">isRetry</span></span>
    * <span data-ttu-id="006c5-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="006c5-346">NonInteractive</span></span>
    * <span data-ttu-id="006c5-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="006c5-347">CanShowDialog</span></span>
* <span data-ttu-id="006c5-348">Bir yanıt içerir</span><span class="sxs-lookup"><span data-stu-id="006c5-348">A response will contain</span></span>
    * <span data-ttu-id="006c5-349">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="006c5-349">Username</span></span>
    * <span data-ttu-id="006c5-350">Parola</span><span class="sxs-lookup"><span data-stu-id="006c5-350">Password</span></span>
    * <span data-ttu-id="006c5-351">İleti</span><span class="sxs-lookup"><span data-stu-id="006c5-351">Message</span></span>
    * <span data-ttu-id="006c5-352">Kimlik doğrulama türlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="006c5-352">List of Auth Types</span></span>
    * <span data-ttu-id="006c5-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="006c5-353">MessageResponseCode</span></span>