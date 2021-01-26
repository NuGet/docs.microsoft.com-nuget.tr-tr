---
title: NuGet CLı kaynakları komutu
description: nuget.exe Sources komutuna yönelik başvuru
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780001"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="3c4de-103">Sources komutu (NuGet CLı)</span><span class="sxs-lookup"><span data-stu-id="3c4de-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="3c4de-104">**Uygulama hedefi:** paket tüketimi, yayımlama &bullet; **Desteklenen sürümler:** tümü</span><span class="sxs-lookup"><span data-stu-id="3c4de-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3c4de-105">Kullanıcı kapsamı yapılandırma dosyasında veya belirtilen yapılandırma dosyasında bulunan kaynak listesini yönetir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="3c4de-106">Kullanıcı kapsamı yapılandırma dosyası `%appdata%\NuGet\NuGet.Config` (Windows) ve `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="3c4de-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="3c4de-107">Nuget.org için kaynak URL 'sinin olduğunu unutmayın `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="3c4de-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="3c4de-108">Kullanım</span><span class="sxs-lookup"><span data-stu-id="3c4de-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="3c4de-109">Burada `<operation>` bir *liste, ekleme, kaldırma, etkinleştirme, devre dışı bırakma* veya *güncelleştirme*, `<name>` kaynağın adı ve `<source>` kaynağın URL 'si olduğu yerdir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span> <span data-ttu-id="3c4de-110">Tek seferde yalnızca bir kaynak üzerinde işlem yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c4de-110">You can operate on only one source at a time.</span></span>

## <a name="options"></a><span data-ttu-id="3c4de-111">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="3c4de-111">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="3c4de-112">Uygulanacak NuGet yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="3c4de-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3c4de-113">Belirtilmemişse, `%AppData%\NuGet\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` ya da `~/.config/NuGet/NuGet.Config` (Mac/Linux) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3c4de-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="3c4de-114">*(3,5 +)* nuget.exe, sabit ve Ingilizce tabanlı bir kültür kullanılarak çalışmaya zorlar.</span><span class="sxs-lookup"><span data-stu-id="3c4de-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Format`**

  <span data-ttu-id="3c4de-115">`list`Eyleme uygulanır ve `Detailed` (varsayılan) veya olabilir `Short` .</span><span class="sxs-lookup"><span data-stu-id="3c4de-115">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span>

- **`-?|-help`**

  <span data-ttu-id="3c4de-116">Komut için yardım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3c4de-116">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="3c4de-117">Kaynağın adı.</span><span class="sxs-lookup"><span data-stu-id="3c4de-117">Name of the source.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="3c4de-118">Kullanıcı girişi veya onayları için istemleri bastırır.</span><span class="sxs-lookup"><span data-stu-id="3c4de-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Password`**

  <span data-ttu-id="3c4de-119">Kaynakla kimlik doğrulaması için parolayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-119">Specifies the password for authenticating with the source.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="3c4de-120">Paket (ler) kaynağının yolu.</span><span class="sxs-lookup"><span data-stu-id="3c4de-120">Path to the package(s) source.</span></span>

- **`-StorePasswordInClearText`**

  <span data-ttu-id="3c4de-121">Şifrelenmiş bir form depolamanın varsayılan davranışı yerine parolayı şifrelenmemiş metin olarak depolamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-121">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span>

- **`-UserName`**

  <span data-ttu-id="3c4de-122">Kaynakla kimlik doğrulaması için Kullanıcı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-122">Specifies the user name for authenticating with the source.</span></span>

- **`-ValidAuthenticationTypes`**

  <span data-ttu-id="3c4de-123">Bu kaynak için geçerli kimlik doğrulama türlerinin virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="3c4de-123">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="3c4de-124">Varsayılan olarak, tüm kimlik doğrulama türleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-124">By default, all authentication types are valid.</span></span> <span data-ttu-id="3c4de-125">Örnek: `basic,negotiate`.</span><span class="sxs-lookup"><span data-stu-id="3c4de-125">Example: `basic,negotiate`.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="3c4de-126">Çıkışta gösterilecek ayrıntı miktarını belirtir: `normal` (varsayılan), `quiet` veya `detailed` .</span><span class="sxs-lookup"><span data-stu-id="3c4de-126">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

> [!Note]
> <span data-ttu-id="3c4de-127">Daha sonra paket kaynağına erişmek için nuget.exe, kaynakların parolasını aynı kullanıcı bağlamına eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3c4de-127">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="3c4de-128">Parola yapılandırma dosyasında şifrelenmiş olarak depolanır ve yalnızca, şifrelendiğinden aynı kullanıcı bağlamında şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="3c4de-128">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="3c4de-129">Örneğin, NuGet paketlerini geri yüklemek için bir yapı sunucusu kullandığınızda, parola, yapı sunucusu görevinin çalışacağı aynı Windows kullanıcıyla şifrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="3c4de-129">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="3c4de-130">Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3c4de-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3c4de-131">Örnekler</span><span class="sxs-lookup"><span data-stu-id="3c4de-131">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
