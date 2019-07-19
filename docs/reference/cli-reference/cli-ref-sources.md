---
title: NuGet CLı kaynakları komutu
description: NuGet. exe kaynakları komutu için başvuru
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328284"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="1108e-103">Sources komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="1108e-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="1108e-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="1108e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1108e-105">Kullanıcı kapsamı yapılandırma dosyasında veya belirtilen yapılandırma dosyasında bulunan kaynak listesini yönetir.</span><span class="sxs-lookup"><span data-stu-id="1108e-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="1108e-106">Kullanıcı kapsamı yapılandırma dosyası (Windows) ve `%appdata%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="1108e-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="1108e-107">Nuget.org için kaynak URL 'sinin olduğunu `https://api.nuget.org/v3/index.json`unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1108e-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="1108e-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="1108e-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="1108e-109">Burada `<operation>` bir *liste, ekleme, kaldırma, etkinleştirme, devre dışı bırakma* veya *güncelleştirme* `<name>` , kaynağın adı ve `<source>` kaynağın URL 'si olduğu yerdir.</span><span class="sxs-lookup"><span data-stu-id="1108e-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="1108e-110">Tek seferde yalnızca bir kaynak üzerinde işlem yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1108e-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="1108e-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="1108e-111">Options</span></span>

| <span data-ttu-id="1108e-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="1108e-112">Option</span></span> | <span data-ttu-id="1108e-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1108e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1108e-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1108e-114">ConfigFile</span></span> | <span data-ttu-id="1108e-115">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="1108e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1108e-116">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1108e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1108e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1108e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="1108e-118">*(3,5 +)* NuGet. exe ' yi sabit, Ingilizce tabanlı bir kültür kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="1108e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1108e-119">Biçimi</span><span class="sxs-lookup"><span data-stu-id="1108e-119">Format</span></span> | <span data-ttu-id="1108e-120">Eyleme uygulanır ve `Detailed` (varsayılan) veya `Short`olabilir. `list`</span><span class="sxs-lookup"><span data-stu-id="1108e-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="1108e-121">Help</span><span class="sxs-lookup"><span data-stu-id="1108e-121">Help</span></span> | <span data-ttu-id="1108e-122">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1108e-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="1108e-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1108e-123">NonInteractive</span></span> | <span data-ttu-id="1108e-124">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="1108e-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1108e-125">Parola</span><span class="sxs-lookup"><span data-stu-id="1108e-125">Password</span></span> | <span data-ttu-id="1108e-126">Kaynakla kimlik doğrulaması için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="1108e-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="1108e-127">Storepasswordincöğrentext</span><span class="sxs-lookup"><span data-stu-id="1108e-127">StorePasswordInClearText</span></span> | <span data-ttu-id="1108e-128">Şifrelenmiş bir form depolamanın varsayılan davranışı yerine parolayı şifrelenmemiş metin olarak depolamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="1108e-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="1108e-129">UserName</span><span class="sxs-lookup"><span data-stu-id="1108e-129">UserName</span></span> | <span data-ttu-id="1108e-130">Kaynakla kimlik doğrulaması için Kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1108e-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="1108e-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1108e-131">Verbosity</span></span> | <span data-ttu-id="1108e-132">Çıktıda görünen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="1108e-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="1108e-133">Paket kaynağına erişmek için NuGet. exe ' nin daha sonra kullanıldığından, kaynakların parolasını aynı kullanıcı bağlamında eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1108e-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="1108e-134">Parola yapılandırma dosyasında şifrelenmiş olarak depolanır ve yalnızca, şifrelendiğinden aynı kullanıcı bağlamında şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="1108e-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="1108e-135">Örneğin, NuGet paketlerini geri yüklemek için bir yapı sunucusu kullandığınızda, parola, yapı sunucusu görevinin çalışacağı aynı Windows kullanıcıyla şifrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="1108e-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="1108e-136">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1108e-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1108e-137">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1108e-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
