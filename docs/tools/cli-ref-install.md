---
title: Polecenie install NuGet interfejsu wiersza polecenia
description: Dokumentacja dla polecenia install nuget.exe
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 8aaf4c2563aa802900a102848fc33fc8708a135d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817892"
---
# <a name="install-command-nuget-cli"></a>install command, polecenie (interfejs wiersza polecenia NuGet)

**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** wszystkie

Pobiera i instaluje pakiet w projekcie, domyślnie używany do bieżącego folderu przy użyciu określonego pakietu źródeł.

> [!Tip]
> Aby pobrać pakiet bezpośrednio poza kontekstem projektu, odwiedź stronę pakietu na [nuget.org](https://www.nuget.org) i wybierz **Pobierz** łącza.

Jeśli nie określono żadnych źródeł, wymienione w pliku konfigurację globalną `%appdata%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux), są używane. Zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md) dodatkowe szczegóły.

Jeśli nie określono żadnych określonych pakietów, `install` instaluje wszystkie pakiety wymienione w projekcie `packages.config` plików, dzięki czemu podobny do [ `restore` ](cli-ref-restore.md).

`install` Polecenia nie modyfikuje plik projektu lub `packages.config`; w ten sposób jest podobna do `restore` w tym go tylko dodaje pakiety do dysku, ale nie zmienia zależności projektu.

Aby dodać zależność, Dodaj pakiet za pomocą Menedżera pakietów interfejsu użytkownika lub konsoli w programie Visual Studio, albo zmodyfikować `packages.config` , a następnie uruchom albo `install` lub `restore`.

## <a name="usage"></a>Użycie

```cli
nuget install <packageID | configFilePath> [options]
```

gdzie `<packageID>` nazwy pakietu do zainstalowania (przy użyciu najnowszej wersji,) lub `<configFilePath>` identyfikuje `packages.config` plik zawierający listę pakietów do zainstalowania. Można wskazać określoną wersję z `-Version` opcji.

## <a name="options"></a>Opcje

| Opcja | Opis |
| --- | --- |
| ConfigFile | Plik konfiguracyjny NuGet do zastosowania. Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.|
| DependencyVersion | *(4.4 +)*  Określa określonej wersji, Zastępowanie domyślnego zachowania rozpoznawania zależności. |
| DisableParallelProcessing | Wyłącza równolegle wielu pakietów. |
| ExcludeVersion | Instaluje pakiet do folderu o nazwie z tylko nazwę pakietu i nie numer wersji. |
| FallbackSource | *(3.2 +)*  Lista źródła pakietów do użycia jako przejścia, w przypadku, gdy nie można znaleźć pakietu w podstawowej lub źródło domyślne. |
| ForceEnglishOutput | *(3.5 +)* Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura. |
| Framework | *(4.4 +)*  Platformy docelowej służy do wybierania zależności. Wartość domyślna to "Any" Jeśli nie zostanie określony. |
| Pomoc | Wyświetla Pomoc dla polecenia. |
| NoCache | Zapobiega przy użyciu pamięci podręcznej pakietów NuGet. Zobacz [Zarządzanie globalne pakietów i foldery pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Nieinterakcyjne | Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń. |
| OutputDirectory | Określa folder, w którym są zainstalowane pakiety. Jeśli folder nie jest określony, używany jest bieżący folder. |
| PackageSaveMode | Określa typy plików, aby zapisać po zainstalowaniu pakietu: jeden z `nuspec`, `nupkg`, lub `nuspec;nupkg`. |
| Wydanie wstępne | Zezwala na pakiety wersji wstępnej do zainstalowania. Ta flaga nie jest wymagana, gdy trwa przywracanie pakietów z `packages.config`. |
| RequireConsent | Sprawdza, czy Przywracanie pakietów jest włączona przed pobierania i instalowania pakietów. Aby uzyskać więcej informacji, zobacz [przywracania pakietów](../consume-packages/package-restore.md). |
| SolutionDirectory | Określa folder główny rozwiązaniu, dla których pod kątem przywracania pakietów. |
| Źródło | Określa listę źródła pakietu (jako adresy URL). W przypadku jego pominięcia polecenie używa źródeł dostarczone w plikach konfiguracji, zobacz [NuGet Konfigurowanie zachowania](../consume-packages/configuring-nuget-behavior.md). |
| Szczegółowość | Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*. |
| Wersja | Określa wersję pakietu do zainstalowania. |

Zobacz też [zmienne środowiskowe](cli-ref-environment-variables.md)

## <a name="examples"></a>Przykłady

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
