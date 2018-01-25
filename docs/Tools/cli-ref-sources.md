---
title: "NuGet CLI kaynakları komut | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Komut nuget.exe için başvuru kaynakları"
keywords: "nuget başvuru kaynakları, komut kaynakları"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c1cd909c0c35d52f0269d267367669df46f9db55
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="d6a28-104">kaynakları komutu (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d6a28-104">sources command (NuGet CLI)</span></span>

<span data-ttu-id="d6a28-105">**Uygulandığı öğe:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="d6a28-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d6a28-106">Bulunan kaynakları listesini yönetir `%AppData%\NuGet\NuGet.Config` veya belirtilen yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d6a28-106">Manages the list of sources located in `%AppData%\NuGet\NuGet.Config` or the specified configuration file.</span></span>

<span data-ttu-id="d6a28-107">Nuget.org kaynak URL'sini olduğuna dikkat edin `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d6a28-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="d6a28-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="d6a28-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="d6a28-109">Burada `<operation>` biri *listesinde, eklemek, kaldırmak, etkinleştirme, devre dışı bırakma,* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="d6a28-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="d6a28-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="d6a28-110">Options</span></span>

| <span data-ttu-id="d6a28-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="d6a28-111">Option</span></span> | <span data-ttu-id="d6a28-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d6a28-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6a28-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d6a28-113">ConfigFile</span></span> | <span data-ttu-id="d6a28-114">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="d6a28-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d6a28-115">Belirtilmezse, *%AppData%\NuGet\NuGet.Config* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6a28-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d6a28-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d6a28-116">ForceEnglishOutput</span></span> | <span data-ttu-id="d6a28-117">*(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar.</span><span class="sxs-lookup"><span data-stu-id="d6a28-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d6a28-118">Biçimi</span><span class="sxs-lookup"><span data-stu-id="d6a28-118">Format</span></span> | <span data-ttu-id="d6a28-119">Uygulandığı öğe `list` eylem ve `Detailed` (varsayılan) veya `Short`.</span><span class="sxs-lookup"><span data-stu-id="d6a28-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="d6a28-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="d6a28-120">Help</span></span> | <span data-ttu-id="d6a28-121">Bilgi komutu için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d6a28-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="d6a28-122">Etkileşimli olmayan</span><span class="sxs-lookup"><span data-stu-id="d6a28-122">NonInteractive</span></span> | <span data-ttu-id="d6a28-123">Kullanıcı girişi veya onayı için ister gizler.</span><span class="sxs-lookup"><span data-stu-id="d6a28-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d6a28-124">Parola</span><span class="sxs-lookup"><span data-stu-id="d6a28-124">Password</span></span> | <span data-ttu-id="d6a28-125">Kaynağı ile kimlik doğrulaması için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="d6a28-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="d6a28-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="d6a28-126">StorePasswordInClearText</span></span> | <span data-ttu-id="d6a28-127">Şifrelenmiş biçimde depolamak varsayılan davranışını yerine şifresiz metin parolayı depolamak için gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6a28-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="d6a28-128">UserName</span><span class="sxs-lookup"><span data-stu-id="d6a28-128">UserName</span></span> | <span data-ttu-id="d6a28-129">Kaynağı ile kimlik doğrulaması için kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="d6a28-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="d6a28-130">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="d6a28-130">Verbosity</span></span> | <span data-ttu-id="d6a28-131">Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="d6a28-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="d6a28-132">Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamında kaynakları parola eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6a28-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="d6a28-133">Parola yapılandırma dosyasında şifrelenen depolanır ve şifrelenmiş olan gibi yalnızca aynı kullanıcı bağlamında şifresi çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="d6a28-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="d6a28-134">Dolayısıyla örneğin bir yapı sunucusunu aynı Windows kullanıcı derleme sunucu görevi çalıştırılacağı parola şifrelenmelidir NuGet paketlerini geri yüklemek için kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="d6a28-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="d6a28-135">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d6a28-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d6a28-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d6a28-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
