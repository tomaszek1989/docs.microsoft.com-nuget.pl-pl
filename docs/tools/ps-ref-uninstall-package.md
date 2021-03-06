---
title: Odinstaluj — pakiet NuGet w programie PowerShell
description: Odwołanie do polecenia programu PowerShell Odinstaluj pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818870"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (konsola menedżera pakietów w programie Visual Studio)

*W tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakietu dezinstalacji programu PowerShell, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*

Usuwa pakiet z projektu, opcjonalnie usunięcie jego zależności. Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.

## <a name="syntax"></a>Składnia

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Jeśli tego pakietu zależą inne pakiety, polecenie zakończy się niepowodzeniem, jeśli nie zostanie określona opcja Force.

## <a name="parameters"></a>Parametry

| Parametr | Opis |
| --- | --- |
| Id | (Wymagane) Identyfikator pakietu do odinstalowania. Id przełącznika sam jest opcjonalna. |
| Wersja | Wersja pakietu do odinstalowania, przyjęty obecnie zainstalowanej wersji. |
| RemoveDependencies | Odinstaluj pakiet i jego nieużywane zależności. Oznacza to jeśli wszystkie zależności zależy od niego inny pakiet, zostaje pominięta. |
| ProjectName | Projekt, z którego ma zostać odinstalowany pakiet, domyślnie używany do projektu domyślnego. |
| Wymuś | Wymusza pakietu do odinstalowania, nawet jeśli inne pakiety są od niego zależne. |
| Instrukcja WhatIf | Pokazuje, co się stanie, uruchamiając polecenie bez rzeczywistego wykonania dezinstalacji. |

Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.

## <a name="common-parameters"></a>Wspólne parametry

`Uninstall-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.

## <a name="examples"></a>Przykłady

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
