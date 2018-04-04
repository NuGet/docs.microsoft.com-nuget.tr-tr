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
ms.openlocfilehash: 5fb34654dc294de34cf0e15f784240884dc1e3d1
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="ee2e6-104">kaynakları komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ee2e6-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="ee2e6-105">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="ee2e6-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ee2e6-106">Kullanıcı kapsam yapılandırma dosyası veya belirtilen yapılandırma dosyasında bulunan kaynakları listesini yönetir.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-106">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="ee2e6-107">Kullanıcı kapsam yapılandırma dosyası şu konumdadır `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-107">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="ee2e6-108">Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-108">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="ee2e6-109">Kullanım</span><span class="sxs-lookup"><span data-stu-id="ee2e6-109">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="ee2e6-110">Burada `<operation>` biri *listesinde, eklemek, kaldırmak, etkinleştirme, devre dışı bırakma,* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-110">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="ee2e6-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="ee2e6-111">Options</span></span>

| <span data-ttu-id="ee2e6-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="ee2e6-112">Option</span></span> | <span data-ttu-id="ee2e6-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee2e6-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee2e6-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ee2e6-114">ConfigFile</span></span> | <span data-ttu-id="ee2e6-115">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ee2e6-116">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ee2e6-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ee2e6-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ee2e6-118">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ee2e6-119">Biçimi</span><span class="sxs-lookup"><span data-stu-id="ee2e6-119">Format</span></span> | <span data-ttu-id="ee2e6-120">Uygulandığı öğe `list` eylem ve `Detailed` (varsayılan) veya `Short`.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="ee2e6-121">Yardım</span><span class="sxs-lookup"><span data-stu-id="ee2e6-121">Help</span></span> | <span data-ttu-id="ee2e6-122">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="ee2e6-123">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="ee2e6-123">NonInteractive</span></span> | <span data-ttu-id="ee2e6-124">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ee2e6-125">Parola</span><span class="sxs-lookup"><span data-stu-id="ee2e6-125">Password</span></span> | <span data-ttu-id="ee2e6-126">Kaynağı ile kimlik doğrulaması için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="ee2e6-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="ee2e6-127">StorePasswordInClearText</span></span> | <span data-ttu-id="ee2e6-128">Şifrelenmiş biçimde depolamak varsayılan davranışını yerine şifresiz metin parolayı depolamak için gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="ee2e6-129">UserName</span><span class="sxs-lookup"><span data-stu-id="ee2e6-129">UserName</span></span> | <span data-ttu-id="ee2e6-130">Kaynağı ile kimlik doğrulaması için kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="ee2e6-131">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="ee2e6-131">Verbosity</span></span> | <span data-ttu-id="ee2e6-132">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="ee2e6-133">Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamında kaynakları parola eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="ee2e6-134">Parola yapılandırma dosyasında şifrelenen depolanır ve şifrelenmiş olan gibi yalnızca aynı kullanıcı bağlamında şifresi çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="ee2e6-135">Dolayısıyla örneğin bir yapı sunucusunu aynı Windows kullanıcı derleme sunucu görevi çalıştırılacağı parola şifrelenmelidir NuGet paketlerini geri yüklemek için kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="ee2e6-136">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ee2e6-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ee2e6-137">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ee2e6-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
