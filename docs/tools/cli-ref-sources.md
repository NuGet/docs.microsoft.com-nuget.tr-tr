---
title: NuGet CLI komutu kaynakları
description: Komut nuget.exe için başvuru kaynakları
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610629"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="bcf31-103">kaynakları komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bcf31-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="bcf31-104">**İçin geçerlidir:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="bcf31-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="bcf31-105">Kullanıcı kapsam yapılandırma dosyası veya belirtilen yapılandırma dosyasında yer alan kaynakları listesini yönetir.</span><span class="sxs-lookup"><span data-stu-id="bcf31-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="bcf31-106">Kullanıcı kapsam yapılandırma dosyası şu konumdadır `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="bcf31-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="bcf31-107">Nuget.org kaynak URL'si Not `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="bcf31-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="bcf31-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="bcf31-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="bcf31-109">Burada `<operation>` biri *listesinde, eklemek, kaldırmak, devre dışı bırakma, etkinleştirme* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="bcf31-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="bcf31-110">Bir kerede yalnızca bir kaynak üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="bcf31-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="bcf31-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="bcf31-111">Options</span></span>

| <span data-ttu-id="bcf31-112">Seçenek</span><span class="sxs-lookup"><span data-stu-id="bcf31-112">Option</span></span> | <span data-ttu-id="bcf31-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bcf31-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bcf31-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bcf31-114">ConfigFile</span></span> | <span data-ttu-id="bcf31-115">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="bcf31-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bcf31-116">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bcf31-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bcf31-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bcf31-117">ForceEnglishOutput</span></span> | <span data-ttu-id="bcf31-118">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="bcf31-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bcf31-119">Biçimi</span><span class="sxs-lookup"><span data-stu-id="bcf31-119">Format</span></span> | <span data-ttu-id="bcf31-120">Uygulandığı `list` eylem ve `Detailed` (varsayılan) veya `Short`.</span><span class="sxs-lookup"><span data-stu-id="bcf31-120">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="bcf31-121">Help</span><span class="sxs-lookup"><span data-stu-id="bcf31-121">Help</span></span> | <span data-ttu-id="bcf31-122">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bcf31-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="bcf31-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bcf31-123">NonInteractive</span></span> | <span data-ttu-id="bcf31-124">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="bcf31-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bcf31-125">Parola</span><span class="sxs-lookup"><span data-stu-id="bcf31-125">Password</span></span> | <span data-ttu-id="bcf31-126">Kaynak kimliğini doğrulamak için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="bcf31-126">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="bcf31-127">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="bcf31-127">StorePasswordInClearText</span></span> | <span data-ttu-id="bcf31-128">Varsayılan davranışını şifrelenmiş biçimde depolamak yerine şifrelenmemiş metin parolayı depolamak için gösterir.</span><span class="sxs-lookup"><span data-stu-id="bcf31-128">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="bcf31-129">UserName</span><span class="sxs-lookup"><span data-stu-id="bcf31-129">UserName</span></span> | <span data-ttu-id="bcf31-130">Kaynak ile kimlik doğrulaması için kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="bcf31-130">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="bcf31-131">Verbosity</span><span class="sxs-lookup"><span data-stu-id="bcf31-131">Verbosity</span></span> | <span data-ttu-id="bcf31-132">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="bcf31-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="bcf31-133">Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamı altında da kaynaklarının parola eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bcf31-133">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="bcf31-134">Parola yapılandırma dosyasında şifrelenen depolanır ve bu şifrelenmiş olarak yalnızca aynı kullanıcı bağlamında şifresi çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="bcf31-134">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="bcf31-135">Örneğin bir yapı sunucusunda yapı sunucusunu görevi altında çalıştırılacağı Windows kullanıcıyla parolanın şifrelenmesi NuGet paketlerini geri yüklemek için kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="bcf31-135">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="bcf31-136">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bcf31-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bcf31-137">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bcf31-137">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
