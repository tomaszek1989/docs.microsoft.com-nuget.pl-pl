---
title: polecenia NuGet dotNet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Krótkie odwołanie poleceń związanych z NuGet przy użyciu interfejsu wiersza polecenia platformy dotnet."
keywords: polecenia NuGet DotNet dotnet, przywracania dotnet, zmienne lokalne nuget dotnet, dotnet nuget wypychania, pakowanie dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a>polecenia dotNet

DotNet interfejsu wiersza polecenia, uruchamiany na systemu Windows, Mac OS X i Linux, zawiera pewną liczbę poleceń podstawowych nuget.exe wymienione poniżej. W przypadku, gdy dotnet zawiera żądanego polecenia, nie jest konieczne do pobrania nuget.exe.

- [**Pakiet DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu dla zestawu SDK NETCore projekty do pakietu NuGet. Należy używać innych typów projektów[`nuget pack`](cli-ref-pack.md)
- [**Przywracanie DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu. Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget restore`.
- [**Zmienne lokalne nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): usuwa lub wyświetla ich listę zasobów lokalnych NuGet, takich jak http żądania pamięci podręcznej, tymczasowego pamięci podręcznej lub folderu pakietów globalne dla komputera.
- [**wypychania nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): wypchnięcia pakietu na serwerze i publikuje ją dotyczy nuget.org, Visual Studio Team Services lub żadnych innych serwerów NuGet.
- [**Usuń DotNet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z serwera, dotyczy nuget.org, Visual Studio Team Services lub żadnych innych serwerów NuGet.