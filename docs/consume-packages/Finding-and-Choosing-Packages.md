---
title: Wyszukiwanie i Wybieranie pakietów NuGet
description: Przegląd jak znaleźć i wybrać najlepsze pakietów NuGet dla projektu, w tym informacji o składni wyszukiwania NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: f1bb145229b0db0e8fdb7fdb31a59aa50bd1d57b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817905"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Znajdowanie i ocena pakietów NuGet dla projektu

Podczas uruchamiania żadnego projektu platformy .NET lub gdy zidentyfikować potrzeba funkcjonalności aplikacji lub usługi, można zapisać samodzielnie wiele czasu i problemy przy użyciu istniejących pakietów NuGet, które spełniają wymagających. Te pakiety mogą pochodzić z kolekcji publicznego [nuget.org](http://www.nuget.org/packages/), ani prywatny źródła dostarczonego przez organizację lub innej firmy.

## <a name="finding-packages"></a>Znajdowanie pakietów

Podczas odwiedzania nuget.org lub otworzyć Interfejs użytkownika Menedżera pakietów w programie Visual Studio, możesz wyświetlić listę pakietów posortowane według całkowitej pliki do pobrania. To natychmiast pokazuje pakiety najbardziej powszechnie używany przez miliony projektów platformy .NET. Jest dobrym pomysłem, a następnie, że co najmniej niektóre pakiety wymienione w pierwszym kilka stron będą przydatne w projektach.

![Domyślny widok nuget.org/packages przedstawiający najpopularniejszych pakietów](media/Finding-01-Popularity.png)

Powiadomienie **Uwzględnij wersję wstępną** opcji w prawym górnym rogu strony. Po wybraniu nuget.org zawiera wszystkie wersje pakietów, w tym w wersji beta oraz inne wersje wczesne. Aby wyświetlić tylko stabilne zwolnione, wyczyść pole wyboru.

Do określonych potrzeb wyszukiwanie według znaczników (Menedżera pakietów w Visual Studio lub w portalu, takich jak nuget.org) jest najbardziej typowe metody odnajdowania odpowiedniego pakietu. Na przykład wyszukiwanie "json" zawiera listę wszystkich pakietów NuGet, które są oznaczane tego słowa kluczowego i w związku z tym niektóre relacją do formatu JSON danych.

![Wyniki wyszukiwania dla "json" na nuget.org](media/Finding-02-SearchResults.png)

Można także przeszukać za pomocą Identyfikatora pakietu, jeśli znasz go. Zobacz [wyszukiwania składni](#search-syntax) poniżej.

W tej chwili wyniki wyszukiwania są posortowane tylko według przydatności, dlatego zazwyczaj chcesz przeglądać co najmniej pierwszy kilka stron wyników dla potrzeb pakietów lub uściślić wyszukiwanych terminów dokładniej.

### <a name="does-the-package-support-my-projects-target-framework"></a>Pakiet obsługuje platformy docelowej mój projekt?

NuGet instaluje pakiet w projekcie tylko wtedy, gdy platforma docelowa projektu obejmują obsługiwanych platform tego pakietu. Jeśli pakiet nie jest zgodny, NuGet problemy z błędem.

Niektóre pakiety listy ich obsługiwanych platform bezpośrednio w galerii nuget.org, ale takich danych nie jest wymagane, wiele pakietów nie zawierają tej listy. Obecnie jest sposób wyszukiwania nuget.org pakietów obsługujące platformę określony element docelowy (Ta funkcja jest pod uwagę, zobacz [NuGet problem 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Na szczęście można określić obsługiwanych platform za pośrednictwem dwóch innych środków:

1. Próba zainstalowania pakietu do projektu przy użyciu [ `Install-Package` ](../tools/ps-ref-install-package.md) w konsoli Menedżera pakietów NuGet. Jeśli pakiet nie jest zgodny, to polecenie przedstawia obsługiwane platformy pakietu.

1. Pobierz pakiet ze swojej strony przy użyciu nuget.org **ręcznego pobrania** łącze w obszarze **informacji**. Zmień rozszerzenie z `.nupkg` do `.zip`i Otwórz plik, aby zbadać zawartość jego `lib` folderu. Widzisz podfoldery dla każdego z obsługiwanych platform, gdzie każdy podfolder nosi nazwę z moniker platformy docelowej (TFM; zobacz [docelowych platform](../reference/target-frameworks.md)). Jeśli widzisz nie podfoldery `lib` i tylko pojedynczego pliku DLL, możesz musi próby zainstalowania pakietu w projekcie, aby odnaleźć zgodności.

## <a name="pre-release-packages"></a>Pakiety wersji wstępnej

Wielu autorów pakietu wprowadź Podgląd i beta zwalnia dostępne, ponieważ nadal poprawiają i wyszukiwanie informacji zwrotnych dotyczących ich najnowsze wersje.

Domyślnie nuget.org zawiera pakiety wersji wstępnej w wynikach wyszukiwania. Aby wyszukać tylko stabilne wersje, wyczyść **Uwzględnij wersję wstępną** opcji w prawym górnym rogu strony

![Obejmują wstępnej wyboru na nuget.org](media/Finding-06-include-prerelease.png)

W programie Visual Studio, a podczas korzystania z narzędzi interfejsu wiersza polecenia NuGet i dotnet NuGet nie ma domyślnie wersje wstępne. Aby zmienić to zachowanie, wykonaj następujące czynności:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, ustaw **Uwzględnij wersję wstępną** pole. Ustawienie lub usunięcie zaznaczenia tego pola odświeża interfejsu użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.

    ![Dołącz wstępnej pole wyboru w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń. Zapoznaj się [w programie PowerShell](../tools/powershell-reference.md).

- **nuget.exe CLI**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń. Zapoznaj się [odwołanie NuGet interfejsu wiersza polecenia](../tools/nuget-exe-cli-reference.md)

- **DotNet.exe CLI**: Określ za pomocą dokładnej wersji wstępnej `-v` argumentu. Zapoznaj się [dotnet Dodaj odwołanie do pakietu](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Oryginalne pakiety języka C++

NuGet obsługuje natywnych języka C++ pakietów można używane w projektach C++ w programie Visual Studio. Dzięki temu **Zarządzaj pakietami NuGet** polecenia menu kontekstowe projektów, wprowadza `native` platformy docelowej i zapewnia integrację programu MSBuild.

Można znaleźć natywnego pakietów na [nuget.org](https://www.nuget.org/packages), wyszukiwanie przy użyciu `tag:native`. Takie pakiety zwykle zapewniają `.targets` i `.props` pliki, które NuGet importuje automatycznie, gdy pakiet zostanie dodany do projektu.

## <a name="evaluating-packages"></a>Ocena pakietów

Najlepszym sposobem oceny przydatność pakietu jest aby go pobrać i wypróbować w kodzie (wszystkie pakiety na nuget.org są regularnie skanowany w poszukiwaniu wirusów, sposobem). Po wszystkich każdy pakiet bardzo popularny otrzymano wprowadzenie do korzystania z niego tylko kilka deweloperzy i może być jednym z pierwszych użytkowników!

W tym samym czasie przy użyciu pakietu NuGet oznacza, że przyjmowanie zależności, tak aby zapewnić, że jest niezawodna. Instalowanie i testowanie bezpośrednio pakietu jest czasochłonne, można także zapoznać się znacznie jakości pakietu, korzystając z informacji na stronie listy pakietu:

- *Pobiera statystyki*: na stronie pakiet na nuget.org, **statystyki** sekcji przedstawiono całkowitą pliki do pobrania, pobierania najnowszej wersji i średnia pliki do pobrania na dzień. Większą liczbą wskazują, że inni deweloperzy miały zależność od pakietu, co oznacza, że jej okazał się.

    ![Statystyka na stronie listy pakiet pobierania](media/Finding-03-Downloads.png)

- *Historia wersji*: na stronie pakiet Sprawdź w obszarze **informacji** dla daty ostatniej aktualizacji i sprawdź, czy **Historia wersji**. Dobrze utrzymywana pakiet ma najnowsze aktualizacje i historię zaawansowanych wersji. Pakiety zaniedbanych ma kilka aktualizacji i często nie zostały zaktualizowane za jakiś czas.

    ![Historia wersji na stronie listy pakietu](media/Finding-04-VersionHistory.png)

- *Instaluje najnowsze*: na stronie pakiet w obszarze **statystyki**, wybierz pozycję **Wyświetl pełne statystyki**. Strona pełne statystyki przedstawia pakiet instaluje w ciągu ostatnich sześciu tygodni, przez numer wersji. Pakiet, który aktywnie korzystają z innymi deweloperami zazwyczaj jest lepszym rozwiązaniem niż jeden, który nie jest.

- *Obsługuje*: na stronie pakiet w obszarze **informacji**, wybierz pozycję **witryny projektu** (jeśli jest dostępny) aby zobaczyć, jakie Obsługa opcje Autor zawiera. Projekt o dedykowanej witryny zazwyczaj lepiej jest obsługiwane.

- *Historia Developer*: na stronie pakiet w obszarze **właścicieli**, wybierz tego właściciela, aby zobaczyć, jakie inne pakiety opublikowanych przez nich. Z wielu pakietów są bardziej prawdopodobne zachować obsługę pracy w przyszłości.

- *Otwórz wkładów źródła*: wiele pakietów są obsługiwane w repozytoria open source, co umożliwia deweloperom w zależności od ich bezpośrednio współtworzenia poprawek usterek i funkcji ulepszenia. Historia wkład dowolnego danego pakietu jest również dobry wskaźnik ile Deweloperzy są aktywnego udziału użytkownika.

- *Przeprowadzenie rozmów z właścicielami*: nowych deweloperów na pewno może być jednakowo zatwierdzone do produkcji dużą pakietów do użycia i zaleca się nadanie im możliwość dostosowania inną ekosystemem NuGet. Pamiętając o tym, dotrzeć bezpośrednio do deweloperów pakietu za pomocą **właścicieli skontaktuj się z** opcję w obszarze **informacji** na stronie listy. To, aby były przyjemnością do pracy z potrzebami!

- *Zastrzeżone prefiksy identyfikator pakietu*: wiele właścicieli pakietu zostały zastosowane do i przyznano [pakietu zastrzeżony prefiks Identyfikatora](../reference/id-prefix-reservation.md). Po wyświetleniu visual znacznik wyboru obok identyfikator pakietu na [nuget.org](https://www.nuget.org/), lub w programie Visual Studio, oznacza to spełnienia właściciela pakietu naszych [kryteria](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) dla Identyfikatora prefiksu rezerwacji. Oznacza to, że właściciel pakietu jest w trakcie wyczyść na identyfikowaniu nimi i ich pakietu.

> [!Note]
> Zawsze zachować ostrożność, z warunkami licencji pakietu, które można wyświetlić, wybierając **informacje dotyczące licencji** na stronie listy pakietu w nuget.org. Jeśli pakiet nie określa postanowienia licencyjne, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą **skontaktuj się z właścicieli** łącze na stronie pakiet. Microsoft nie licencji jakiejkolwiek własności intelektualnej użytkownikowi od innych dostawców pakietu i nie jest odpowiedzialny za informacji dostarczonych przez strony trzecie.

## <a name="search-syntax"></a>Wyszukiwanie składni

Wyszukaj pakiet NuGet działa tak samo nuget.org, z poziomu interfejsu wiersza polecenia NuGet, a w ramach rozszerzenia Menedżera pakietów NuGet w programie Visual Studio. Ogólnie rzecz biorąc wyszukiwanie jest stosowany do słów kluczowych, a także opisy pakietu.

- **Słowa kluczowe**: wyszukiwania wyszukuje odpowiednie pakiety, które zawierać żadnego z podanych słów kluczowych. Przykład: `modern UI`. Aby wyszukać pakietów, które zawiera wszystkie podane słów kluczowych, użyj "+" między warunków, takich jak `modern+UI`.
- **Wyrażenia**: wprowadzania terminów w cudzysłowie wyszukuje dokładne dopasowania bez uwzględniania wielkości liter w tych warunkach. Przykład: `"modern UI" package`
- **Filtrowanie**: wyszukiwanego terminu może dotyczyć określoną właściwość przy użyciu składni `<property>:<term>` gdzie `<property>` (bez uwzględniania wielkości liter) może być `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, i `owner`. Warunki mogą być zawarte w cudzysłowie, jeśli to konieczne, i można wyszukiwać wiele właściwości, w tym samym czasie. Ponadto wyszukuje `id` właściwości są dopasowania podciąg, podczas gdy `packageid` używa dokładnego dopasowania. Przykłady:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
