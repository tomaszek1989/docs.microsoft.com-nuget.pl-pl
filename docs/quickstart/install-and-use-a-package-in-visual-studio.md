---
title: Przewodnik wprowadzający do korzystania z pakietów NuGet z poziomu programu Visual Studio
description: Samouczek wskazówki dotyczące procesu instalacji i przy użyciu pakietu NuGet w projekcie programu Visual Studio.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: a64a87319e9bc6dc992892783d00dc42db1b1dd8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818857"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Szybki Start: Instalowanie i użyj pakietu w programie Visual Studio

Pakiety NuGet zawiera kod wielokrotnego użytku, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach. Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle. Pakiety są zainstalowane w projekcie programu Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów. W tym artykule przedstawiono proces, korzystając z popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu i projektu Windows platformy Uniwersalnej. Ten sam proces ma zastosowanie do innych projektów .NET lub .NET Core.

Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz. Po odniesienia, można wywołać pakietu za pośrednictwem jej interfejsu API.

> [!Tip]
> **Rozpoczynać nuget.org**: nuget.org przeglądania jest jak .NET deweloperzy zazwyczaj znaleźć składników może zostać ponownie użyty we własnych aplikacjach. Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne

- Visual Studio 2017 z obciążeniem rozwoju platformy uniwersalnej systemu Windows, lub
- Visual Studio 2015 Update 3 z narzędzia dla uniwersalnych aplikacji systemu Windows.

Można zainstalować 2017 Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/) lub użyj Professional lub Enterprise Edition.

## <a name="create-a-project"></a>Tworzenie projektu

Można zainstalować pakietów NuGet w przypadku projektów .NET, pod warunkiem, że pakiet obsługuje samą platformę docelową jako projekt.

W ramach tego przewodnika należy użyć prostej aplikacji uniwersalnych systemu Windows (UWP). Tworzenie projektu za pomocą programu Visual Studio **Plik > Nowy projekt...**  i wybierając **uniwersalnych systemu Windows > Pusta aplikacja (uniwersalna systemu Windows)**. Zaakceptuj wartości domyślne dla wersji docelowej i minimalna wersja po wyświetleniu monitu.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Dodaj pakiet Newtonsoft.Json NuGet

Aby zainstalować pakiet, należy użyć interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów. Po zainstalowaniu pakietu NuGet rejestruje zależności w jednym pliku projektu lub `packages.config` pliku. Aby uzyskać więcej informacji, zobacz [pakietu omówienie zużycia i przepływ pracy](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Interfejs użytkownika Menedżera pakietów

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.

    ![Zarządzanie pakietami NuGet polecenia dla odwołania do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. Wybierz polecenie "nuget.org" jako **źródła pakietu**, wybierz pozycję **Przeglądaj** karcie, wyszukaj **Newtonsoft.Json**, wybierz z listy tego pakietu i wybierz  **Zainstaluj**:

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. Zaakceptuj wszystkie monity licencji.

1. (Visual Studio 2017) Jeśli zostanie wyświetlony monit, aby wybrać format pakietu zarządzania, wybierz **PackageReference w pliku projektu**:

    ![Wybierając format pakietu administracyjnego](media/QS_Use-03b-SelectFormat.png)

1. Jeśli zostanie wyświetlony monit o przegląd zmian dokonanych, wybierz **OK**.

### <a name="package-manager-console"></a>Konsola Menedżera pakietów

1. Wybierz **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia menu.

1. Po otwarciu konsoli, sprawdź, czy **domyślny projekt** listy rozwijanej pokazuje projektu, do którego ma zostać zainstalowany pakiet. Jeśli masz jednego projektu w rozwiązaniu została już wybrana.

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. Wprowadź polecenie `Install-Package Newtonsoft.json` (zobacz [Install-Package](../tools/ps-ref-install-package.md)). W oknie konsoli wyświetlane dane wyjściowe polecenia. Błędy zazwyczaj wskazują, że pakiet nie jest zgodna z platformy docelowej projektu.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Użyj Newtonsoft.Json interfejsu API w aplikacji

Przy użyciu pakietu Newtonsoft.Json w projekcie, można wywołać jej `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg zrozumiałą dla użytkownika.

1. Otwórz `MainPage.xaml` i Zastąp istniejące `Grid` element z następujących czynności:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Otwórz `MainPage.xaml.cs` pliku (znajdujący się w Eksploratorze rozwiązań w obszarze `MainPage.xaml` węzła) i Wstaw następujący kod w `MainPage` konstruktora:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Nawet jeśli pakiet Newtonsoft.Json dodane do projektu, red zygzaki jest wyświetlany w obszarze `JsonConvert` ponieważ potrzebne `using` instrukcji w górnej części pliku kodu:

    ```cs
    using Newtonsoft.json;
    ```

1. Tworzenie i uruchamianie aplikacji, naciskając klawisz F5 lub wybranie **Debuguj > Rozpocznij debugowanie**:

    ![Początkowe dane wyjściowe aplikacji platformy uniwersalnej systemu Windows](media/QS_Use-06-AppStart.png)

1. Wybierz przycisk, aby wyświetlić zawartość obiektu TextBlock zastąpione tekst JSON:

    ![Dane wyjściowe aplikacji platformy uniwersalnej systemu Windows po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>Pokrewne artykuły

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Sposoby instalacji pakietu](../consume-packages/ways-to-install-a-package.md)
- [Konfigurowanie zachowania programu NuGet](../consume-packages/configuring-nuget-behavior.md)
