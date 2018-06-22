---
title: Polecenie setapikey NuGet interfejsu wiersza polecenia
description: Informacje dotyczące polecenia setapikey nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817687"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="7119f-103">polecenie setapikey (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7119f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="7119f-104">**Dotyczy:** zużycie pakietu, publikowanie &bullet; **obsługiwane wersje:** wszystkie</span><span class="sxs-lookup"><span data-stu-id="7119f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7119f-105">Zapisuje klucz interfejsu API dla danego adresu URL podanego serwera do `NuGet.Config` tak, aby nie trzeba wprowadzać dla kolejnych poleceń.</span><span class="sxs-lookup"><span data-stu-id="7119f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7119f-106">Użycie</span><span class="sxs-lookup"><span data-stu-id="7119f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="7119f-107">gdzie `<source>` identyfikuje serwer i `<key>` to klucz lub hasło, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="7119f-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="7119f-108">Jeśli `<source>` jest pominięty, zakłada nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7119f-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="7119f-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="7119f-109">Options</span></span>

| <span data-ttu-id="7119f-110">Opcja</span><span class="sxs-lookup"><span data-stu-id="7119f-110">Option</span></span> | <span data-ttu-id="7119f-111">Opis</span><span class="sxs-lookup"><span data-stu-id="7119f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7119f-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7119f-112">ConfigFile</span></span> | <span data-ttu-id="7119f-113">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7119f-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7119f-114">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="7119f-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7119f-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7119f-115">ForceEnglishOutput</span></span> | <span data-ttu-id="7119f-116">*(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="7119f-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7119f-117">Pomoc</span><span class="sxs-lookup"><span data-stu-id="7119f-117">Help</span></span> | <span data-ttu-id="7119f-118">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="7119f-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="7119f-119">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="7119f-119">NonInteractive</span></span> | <span data-ttu-id="7119f-120">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="7119f-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7119f-121">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="7119f-121">Verbosity</span></span> | <span data-ttu-id="7119f-122">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="7119f-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7119f-123">Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7119f-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7119f-124">Przykłady</span><span class="sxs-lookup"><span data-stu-id="7119f-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```