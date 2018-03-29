---
title: NuGet CLI kaynakları komut | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Komut nuget.exe için başvuru kaynakları
keywords: nuget başvuru kaynakları, komut kaynakları
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f682a5209556ec6741473ccf2648e8f38bb568b9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="779e0-104">kaynakları komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="779e0-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="779e0-105">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="779e0-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="779e0-106">Kullanıcı kapsam yapılandırma dosyası veya belirtilen yapılandırma dosyasında bulunan kaynakları listesini yönetir.</span><span class="sxs-lookup"><span data-stu-id="779e0-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="779e0-107">Kullanıcı kapsam yapılandırma dosyası şu konumdadır `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="779e0-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="779e0-108">Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="779e0-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="779e0-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="779e0-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="779e0-110">Burada `<operation>` biri *listesinde, eklemek, kaldırmak, etkinleştirme, devre dışı bırakma,* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="779e0-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="779e0-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="779e0-111">Options</span></span>

| <span data-ttu-id="779e0-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="779e0-112">Option</span></span> | <span data-ttu-id="779e0-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="779e0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="779e0-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="779e0-114">ConfigFile</span></span> | <span data-ttu-id="779e0-115">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="779e0-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="779e0-116">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="779e0-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="779e0-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="779e0-117">ForceEnglishOutput</span></span> | <span data-ttu-id="779e0-118">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="779e0-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="779e0-119">Biçimi</span><span class="sxs-lookup"><span data-stu-id="779e0-119">Format</span></span> | <span data-ttu-id="779e0-120">Uygulandığı öğe `list` eylem ve `Detailed` (varsayılan) veya `Short`.</span><span class="sxs-lookup"><span data-stu-id="779e0-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="779e0-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="779e0-121">Help</span></span> | <span data-ttu-id="779e0-122">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="779e0-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="779e0-123">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="779e0-123">NonInteractive</span></span> | <span data-ttu-id="779e0-124">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="779e0-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="779e0-125">Parola</span><span class="sxs-lookup"><span data-stu-id="779e0-125">Password</span></span> | <span data-ttu-id="779e0-126">Kaynağı ile kimlik doğrulaması için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="779e0-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="779e0-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="779e0-127">StorePasswordInClearText</span></span> | <span data-ttu-id="779e0-128">Şifrelenmiş biçimde depolamak varsayılan davranışını yerine şifresiz metin parolayı depolamak için gösterir.</span><span class="sxs-lookup"><span data-stu-id="779e0-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="779e0-129">UserName</span><span class="sxs-lookup"><span data-stu-id="779e0-129">UserName</span></span> | <span data-ttu-id="779e0-130">Kaynağı ile kimlik doğrulaması için kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="779e0-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="779e0-131">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="779e0-131">Verbosity</span></span> | <span data-ttu-id="779e0-132">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="779e0-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="779e0-133">Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamında kaynakları parola eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="779e0-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="779e0-134">Parola yapılandırma dosyasında şifrelenen depolanır ve şifrelenmiş olan gibi yalnızca aynı kullanıcı bağlamında şifresi çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="779e0-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="779e0-135">Dolayısıyla örneğin bir yapı sunucusunu aynı Windows kullanıcı derleme sunucu görevi çalıştırılacağı parola şifrelenmelidir NuGet paketlerini geri yüklemek için kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="779e0-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="779e0-136">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="779e0-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="779e0-137">Örnekler</span><span class="sxs-lookup"><span data-stu-id="779e0-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
