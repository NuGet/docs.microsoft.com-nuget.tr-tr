---
title: NuGet CLI komutu kaynakları
description: Komut nuget.exe için başvuru kaynakları
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548114"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="5d392-103">kaynakları komut (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5d392-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="5d392-104">**İçin geçerlidir:** paket tüketim, yayımlama &bullet; **desteklenen sürümler:** tüm</span><span class="sxs-lookup"><span data-stu-id="5d392-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5d392-105">Kullanıcı kapsam yapılandırma dosyası veya belirtilen yapılandırma dosyasında yer alan kaynakları listesini yönetir.</span><span class="sxs-lookup"><span data-stu-id="5d392-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="5d392-106">Kullanıcı kapsam yapılandırma dosyası şu konumdadır `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5d392-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="5d392-107">Nuget.org kaynak URL'si Not `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="5d392-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="5d392-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="5d392-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="5d392-109">Burada `<operation>` biri *listesinde, eklemek, kaldırmak, devre dışı bırakma, etkinleştirme* veya *güncelleştirme*, `<name>` kaynak adıdır ve `<source>` kaynağının URL'si.</span><span class="sxs-lookup"><span data-stu-id="5d392-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="5d392-110">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="5d392-110">Options</span></span>

| <span data-ttu-id="5d392-111">Seçenek</span><span class="sxs-lookup"><span data-stu-id="5d392-111">Option</span></span> | <span data-ttu-id="5d392-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5d392-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d392-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5d392-113">ConfigFile</span></span> | <span data-ttu-id="5d392-114">Uygulamak için NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="5d392-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5d392-115">Belirtilmezse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5d392-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5d392-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5d392-116">ForceEnglishOutput</span></span> | <span data-ttu-id="5d392-117">*(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="5d392-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5d392-118">Biçimi</span><span class="sxs-lookup"><span data-stu-id="5d392-118">Format</span></span> | <span data-ttu-id="5d392-119">Uygulandığı `list` eylem ve `Detailed` (varsayılan) veya `Short`.</span><span class="sxs-lookup"><span data-stu-id="5d392-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="5d392-120">Yardım</span><span class="sxs-lookup"><span data-stu-id="5d392-120">Help</span></span> | <span data-ttu-id="5d392-121">Bilgi komut için yardımı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5d392-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="5d392-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5d392-122">NonInteractive</span></span> | <span data-ttu-id="5d392-123">Kullanıcı girişini veya onaylar ister bastırır.</span><span class="sxs-lookup"><span data-stu-id="5d392-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5d392-124">Parola</span><span class="sxs-lookup"><span data-stu-id="5d392-124">Password</span></span> | <span data-ttu-id="5d392-125">Kaynak kimliğini doğrulamak için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="5d392-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="5d392-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="5d392-126">StorePasswordInClearText</span></span> | <span data-ttu-id="5d392-127">Varsayılan davranışını şifrelenmiş biçimde depolamak yerine şifrelenmemiş metin parolayı depolamak için gösterir.</span><span class="sxs-lookup"><span data-stu-id="5d392-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="5d392-128">UserName</span><span class="sxs-lookup"><span data-stu-id="5d392-128">UserName</span></span> | <span data-ttu-id="5d392-129">Kaynak ile kimlik doğrulaması için kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5d392-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="5d392-130">Ayrıntı Düzeyi</span><span class="sxs-lookup"><span data-stu-id="5d392-130">Verbosity</span></span> | <span data-ttu-id="5d392-131">Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*.</span><span class="sxs-lookup"><span data-stu-id="5d392-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="5d392-132">Nuget.exe daha sonra paket kaynağına erişmek için kullanılan aynı kullanıcı bağlamı altında da kaynaklarının parola eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5d392-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="5d392-133">Parola yapılandırma dosyasında şifrelenen depolanır ve bu şifrelenmiş olarak yalnızca aynı kullanıcı bağlamında şifresi çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="5d392-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="5d392-134">Örneğin bir yapı sunucusunda yapı sunucusunu görevi altında çalıştırılacağı Windows kullanıcıyla parolanın şifrelenmesi NuGet paketlerini geri yüklemek için kullandığınızda.</span><span class="sxs-lookup"><span data-stu-id="5d392-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="5d392-135">Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5d392-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5d392-136">Örnekler</span><span class="sxs-lookup"><span data-stu-id="5d392-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
