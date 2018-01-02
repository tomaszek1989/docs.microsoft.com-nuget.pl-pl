---
title: "Wersji wstępnej wersji w pakietach NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: df6a366a-22c1-47bb-8017-18231311ce88
description: "Wskazówki dotyczące tworzenia pakiety wersji wstępnej"
keywords: "przechowywanie wersji, przechowywanie wersji pakietu NuGet, wersje wstępne NuGet, wstępnej pakietów NuGet, wersje pakietu w wersji zapoznawczej, wersji RC pakietów, wersje pakietu w wersji Beta, wersjonowania semantycznego NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 07cb9b9bdeeea6f283e95a11a06d7f2043c9b17c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="building-pre-release-packages"></a>Tworzenie pakiety wersji wstępnej

Zawsze, gdy zwolnieniu zaktualizowany pakiet z nowym numerem wersji NuGet uzna, że jeden jako "najnowsza stabilna wersja" jak pokazano na przykład w interfejsie użytkownika Menedżera pakietów w programie Visual Studio:

![Interfejs użytkownika Menedżera pakietów przedstawiający najnowsze stabilna wersja](media/Prerelease_01-LatestStable.png)

Stabilna wersja to taki, który jest uznawany za niezawodny do użycia w środowisku produkcyjnym. Najnowsze stabilna wersja jest również ten, który zostanie zainstalowany jako aktualizacja pakietu lub w czasie przywracania pakietu (pod warunkiem ograniczenia zgodnie z opisem w [ponowne zainstalowanie i aktualizowanie pakietów](../consume-packages/reinstalling-and-updating-packages.md)).

Do obsługi cyklu życia wersji oprogramowania, NuGet w wersji 1.6 lub nowszym umożliwia dystrybucji pakiety wersji wstępnej, gdzie numer wersji obejmuje sufiks wersjonowania semantycznego takich jak `-alpha`, `-beta`, lub `-rc`. Aby uzyskać więcej informacji, zobacz [wersji pakietu](../reference/package-versioning.md#pre-release-versions).

Można określić takie wersji na dwa sposoby:

- `.nuspec`Plik: zawiera sufiksu wersją semantyczną w `version` elementu:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- Zestawu atrybutów: podczas tworzenia pakietu z projektu programu Visual Studio (`.csproj` lub `.vbproj`), użyj `AssemblyInformationalVersionAttribute` do określania wersji:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet przejmuje zamiast określona w tym wartości `AssemblyVersion` atrybut, który nie obsługuje wersjonowania semantycznego.

Gdy wszystko jest gotowe do wydania stabilną wersję, po prostu usuń sufiks i pakiet ma pierwszeństwo przed wszystkie wersje wstępne. Ponownie, zobacz [wersji pakietu](../reference/package-versioning.md#pre-release-versions).


## <a name="installing-and-updating-pre-release-packages"></a>Instalowanie i aktualizowanie pakiety wersji wstępnej

Domyślnie podczas pracy z pakietami NuGet nie zawiera wersji wstępnych, ale to zachowanie można zmienić w następujący sposób:

- **Interfejs użytkownika Menedżera pakietów w programie Visual Studio**: W **Zarządzaj pakietami NuGet** interfejsu użytkownika, sprawdź **Uwzględnij wersję wstępną** pola:

    ![Dołącz wstępnej pole wyboru w programie Visual Studio](media/Prerelease_02-CheckPrerelease.png)

    Ustawienie lub usunięcie zaznaczenia tego pola, zostaną odświeżone interfejsu użytkownika Menedżera pakietów i listę dostępnych wersji, które można zainstalować.

- **Konsola Menedżera pakietów**: Użyj `-IncludePrerelease` przełącznik z `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, i `Update-Package` poleceń. Zapoznaj się [w programie PowerShell](../tools/powershell-reference.md).

- **Interfejs wiersza polecenia NuGet**: Użyj `-prerelease` przełącznik z `install`, `update`, `delete`, i `mirror` poleceń. Zapoznaj się [odwołanie NuGet interfejsu wiersza polecenia](../tools/nuget-exe-cli-reference.md)


## <a name="semantic-versioning"></a>Wersjonowania semantycznego

[Wersjonowania semantycznego lub programu SemVer Konwencji](http://semver.org/spec/v1.0.0.html) opisano, jak korzystać z ciągów numery wersji w celu przedstawienia ich znaczenie kodu źródłowego.

W tym Konwencji każdej wersji ma trzy części `Major.Minor.Patch`, mają następujące znaczenie:

- `Major`: Zmiany krytyczne
- `Minor`: Nowe funkcje, ale wstecznie zgodne
- `Patch`: Wstecznie zgodne wprowadzono poprawki błędów tylko

Wersje wstępne następnie są wskazywane przez dodanie łącznika i ciąg po numer poprawki. Jak to działa, można użyć * żadnych * ciągu po łącznika i NuGet, będą traktować pakietu jako wersji wstępnej. Następnie NuGet Wyświetla numer wersji pełnej w odpowiednich interfejsu użytkownika, pozostawiając konsumentów interpretować znaczenie dla siebie.

Pamiętając o tym warto zazwyczaj wykonaj rozpoznanym konwencji nazewnictwa, takie jak następujące:

- `-alpha`: Wersja alfa, zwykle używany w przypadku pracy w toku i eksperymenty
- `-beta`: Wydania beta, zazwyczaj jest pełną Następna funkcja planowane wersji, ale może zawierać znanych błędów.
- `-rc`: Wersji release candidate, zwykle potencjalnie ostateczną zlecenia (stable), chyba że wyłonić znaczących usterki.

> [!Note]
> NuGet nie obsługuje [zgodnego programu SemVer (v2.0.0)](http://semver.org/spec/v2.0.0.html) wersja wstępna liczby za pomocą kropkowego, podobnie jak w `1.0.1-build.23`. Można użyć formularza, takich jak `1.0.1-build23` , ale jest to zawsze uważane za wersji wstępnej.

Niezależnie od sufiksy, jednak należy użyć, NuGet zapewni ich pierwszeństwo w odwrotnej kolejności alfabetycznej:

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta12
1.0.1-beta05
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
```

Co zostało pokazane, wersji bez żadnego sufiksu będą zawsze miały pierwszeństwo przed wersje wstępne. Należy pamiętać, że użycie numeryczny sufiksy z tagami wersji wstępnej, którzy mogą korzystać z dwucyfrowych numery (lub więcej), umożliwia zera wiodące beta01 i beta05 upewnij się, że ich sortowania prawidłowo po dłuższego liczby.