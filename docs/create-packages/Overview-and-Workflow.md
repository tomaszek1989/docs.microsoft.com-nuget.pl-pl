---
title: Omówienie i przepływ pracy tworzenia pakietów NuGet
description: Omówienie procesu tworzenia i publikowania pakietu NuGet, wraz z łączami do innych części określonego procesu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 1e2a7299be64d33bd0d697522cf5febb2022e0ee
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817017"
---
# <a name="package-creation-workflow"></a>Przepływ pracy tworzenia pakietu

Tworzenie pakietu rozpoczyna się od kompilowanym kodzie (zazwyczaj zestawów platformy .NET) do pakietu i udostępniać innym osobom, za pomocą galerii nuget.org publicznych lub prywatnych galerii w danej organizacji. Pakiet można także dodatkowe pliki takie jak plik readme, który jest wyświetlany, gdy pakiet jest zainstalowany i może zawierać przekształceń do niektórych plików projektu.

Pakiet mogą również służyć tylko ściągania we wszystkich innych zależności nie zawierająca żadnego kodu własnych. Taki pakiet to wygodny sposób dostarczyć zestawu SDK, który składa się z wielu niezależnych pakietów. W pozostałych przypadkach pakiet może zawierać tylko symbol (`.pdb`) pliki do pomocy debugowania.

> [!Note]
> Podczas tworzenia pakietu do użytku przez inne ważne jest zrozumienie ich przyjmowanie zależności na pracę. Tak tworzenie i publikowanie pakietu oznacza także zobowiązań naprawiania błędów i co inne aktualizacje lub w bardzo najmniej wprowadzania dostępna jako pakiet otworzyć źródła, aby inne osoby mogą pomóc w jego utrzymania.

Niezależnie od przypadku utworzenie pakietu zaczyna się od podejmowaniu decyzji, które zestawy i inne pliki do pakietu. Następnie można utworzyć pliku manifestu, nazywane `.nuspec` pliku do opisywania zawartość pakietu wraz z jego identyfikatora, numer wersji, informacje o prawach autorskich, właściwości programu MSBuild i elementów docelowych i wiele innych.

Kiedy zostały przygotowane wszystkie niezbędne pliki w odpowiednie foldery i utworzono odpowiednie `.nuspec` pliku, następnie należy użyć `nuget pack` polecenia (lub [docelowy programu MSBuild pakiet](../reference/msbuild-targets.md)) do sobą wszystkie elementy `.nupkg` pliku. Następnie możesz wdrożyć pakiet do dowolnego hosta umożliwia dostęp do niego innymi deweloperami.

> [!Tip]
> Pakiet NuGet o `.nupkg` rozszerzenie jest po prostu pliku ZIP. Aby łatwo sprawdzić zawartość dowolnego pakietu, zmień rozszerzenie do `.zip` i rozwiń jego zawartość w zwykły sposób. Po prostu upewnij się, zmień rozszerzenie do `.nupkg` przed podjęciem próby przekazania jej do hosta.

Aby dowiedzieć się i zrozumieć proces tworzenia, rozpoczynać [utworzenie pakietu](../create-packages/creating-a-package.md) który przeprowadzi Cię przez podstawowe procesy wspólnej do wszystkich pakietów.

Z tego miejsca należy wziąć pod uwagę wiele innych opcji pakietu:

- [Obsługujący wiele platform docelowych](../create-packages/supporting-multiple-target-frameworks.md) opisuje sposób tworzenia pakietu z wieloma odmianami dla różnych platform .NET Framework.
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md) opisuje struktury pakietu z wielu zasobów językowych oraz korzystanie z osobnych satelity zlokalizowanych pakietów.
- [Pakiety wersji wstępnej](../create-packages/prerelease-packages.md) pokazano, jak wersji alfa, beta i rc pakietów do klientów, którzy są zainteresowani.
- [Źródło i przekształcenia pliku Config](../create-packages/source-and-config-file-transformations.md) w tym artykule opisano, jak zarówno jednokierunkowe tokenu zamienianie w plikach, które są dodawane do projektu i zmodyfikować `web.config` i `app.config` z ustawień, które są również obsługiwane się po odinstalowaniu pakietu .
- [Symbol pakiety](../create-packages/symbol-packages.md) zawiera wskazówki dotyczące dostarczanie symboli dla biblioteki, umożliwiające konsumentom wkroczyć do kodu podczas debugowania.
- [Przechowywanie wersji pakietu](../reference/package-versioning.md) omówiono sposób zidentyfikować dokładną wersję, umożliwiające zależności (inne pakiety, które korzystanie z pakietu).
- [Oryginalne pakiety](../create-packages/native-packages.md) opisano proces tworzenia pakietu w konsumentach napisanych w języku C++.
- [Podpisywanie pakietów](../create-packages/sign-a-package.md) opisano proces dodawania podpisu cyfrowego do pakietu.

Jeśli następnie możesz przystąpić do publikowania pakietu nuget.org, wykonaj prosty proces w [opublikowania pakietu](../create-packages/publish-a-package.md).

Jeśli chcesz użyć zamiast nuget.org prywatnej źródło danych, zobacz [Hosting Omówienie pakietów](../hosting-packages/overview.md)
