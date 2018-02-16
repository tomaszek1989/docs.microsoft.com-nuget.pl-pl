---
title: "Przewodnik wprowadzający do korzystania z pakietów NuGet z poziomu programu Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki dotyczące procesu instalacji i przy użyciu pakietu NuGet w projekcie programu Visual Studio."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet, za pomocą pakietów NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0030877803ac7403f26e27ac3c5a0303d69c489
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="0c256-104">Zainstaluj i użyj pakietu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c256-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="0c256-105">Pakiety NuGet zawiera kod wielokrotnego użytku, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="0c256-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="0c256-106">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="0c256-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="0c256-107">Pakiety są zainstalowane do projektu programu Visual Studio przy użyciu interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów, zgodnie z opisem w tym artykule popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu i projektu Windows platformy Uniwersalnej.</span><span class="sxs-lookup"><span data-stu-id="0c256-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console, as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span>

<span data-ttu-id="0c256-108">Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz.</span><span class="sxs-lookup"><span data-stu-id="0c256-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="0c256-109">Po odniesienia, można wywołać pakietu za pośrednictwem jej interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0c256-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="0c256-110">**Rozpoczynać nuget.org**: nuget.org przeglądania jest jak .NET deweloperzy zazwyczaj znaleźć składników może zostać ponownie użyty we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="0c256-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="0c256-111">Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="0c256-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="0c256-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0c256-112">Pre-requisites</span></span>

- <span data-ttu-id="0c256-113">Visual Studio 2017 z obciążeniem rozwoju platformy uniwersalnej systemu Windows, lub</span><span class="sxs-lookup"><span data-stu-id="0c256-113">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="0c256-114">Visual Studio 2015 Update 3 z narzędzia dla uniwersalnych aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0c256-114">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="0c256-115">Można zainstalować 2017 Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/) lub użyj Professional lub Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="0c256-115">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="0c256-116">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="0c256-116">Create a project</span></span>

<span data-ttu-id="0c256-117">Można zainstalować pakietów NuGet w projekcie .NET określonego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="0c256-117">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="0c256-118">Dla tego przewodnika możesz użyć prostej aplikacji uniwersalnych systemu Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="0c256-118">For this walkthrough, you use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="0c256-119">Tworzenie projektu za pomocą programu Visual Studio **Plik > Nowy projekt...**  i wybierając **uniwersalnych systemu Windows > Pusta aplikacja (uniwersalna systemu Windows)**.</span><span class="sxs-lookup"><span data-stu-id="0c256-119">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="0c256-120">Zaakceptuj wartości domyślne dla wersji docelowej i minimalna wersja po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="0c256-120">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="0c256-121">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="0c256-121">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="0c256-122">Aby zainstalować pakiet, należy użyć interfejsu użytkownika Menedżera pakietów lub konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="0c256-122">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="0c256-123">Interfejs użytkownika Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="0c256-123">Package Manager UI</span></span>

1. <span data-ttu-id="0c256-124">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **odwołania** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0c256-124">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Zarządzanie pakietami NuGet polecenia dla odwołania do projektu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="0c256-126">Wybierz polecenie "nuget.org" jako **źródła pakietu**, wybierz pozycję **Przeglądaj** karcie, wyszukaj **Newtonsoft.Json**, wybierz z listy tego pakietu i wybierz  **Zainstaluj**:</span><span class="sxs-lookup"><span data-stu-id="0c256-126">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="0c256-128">Zaakceptuj wszystkie monity licencji.</span><span class="sxs-lookup"><span data-stu-id="0c256-128">Accept any license prompts.</span></span>

1. <span data-ttu-id="0c256-129">(Visual Studio 2017) Jeśli zostanie wyświetlony monit, aby wybrać format pakietu zarządzania, wybierz **PackageReference w pliku projektu**:</span><span class="sxs-lookup"><span data-stu-id="0c256-129">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Wybieranie formatu odwołanie do pakietu](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="0c256-131">Jeśli zostanie wyświetlony monit o przegląd zmian dokonanych, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c256-131">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="0c256-132">Konsola Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="0c256-132">Package Manager Console</span></span>

1. <span data-ttu-id="0c256-133">Wybierz **Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="0c256-133">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="0c256-134">Po otwarciu konsoli, sprawdź, czy **domyślny projekt** listy rozwijanej pokazuje projektu, do którego ma zostać zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="0c256-134">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="0c256-135">Jeśli masz jednego projektu w rozwiązaniu została już wybrana.</span><span class="sxs-lookup"><span data-stu-id="0c256-135">If you have a single project in the solution, it is already selected.</span></span>

    ![Lokalizowanie pakiet Newtonsoft.Json](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="0c256-137">Wprowadź polecenie `Install-Package Newtonsoft.json` (zobacz [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="0c256-137">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="0c256-138">W oknie konsoli wyświetlane dane wyjściowe polecenia.</span><span class="sxs-lookup"><span data-stu-id="0c256-138">The console window shows output for the command.</span></span> <span data-ttu-id="0c256-139">Błędy zazwyczaj wskazują, że pakiet nie jest zgodna z platformy docelowej projektu.</span><span class="sxs-lookup"><span data-stu-id="0c256-139">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="0c256-140">Użyj Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c256-140">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="0c256-141">Przy użyciu pakietu Newtonsoft.Json w projekcie, można wywołać jej `JsonConvert.SerializeObject` metodę, aby przekonwertować obiekt na ciąg zrozumiałą dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0c256-141">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="0c256-142">Otwórz `MainPage.xaml` i Zastąp istniejące `Grid` element z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="0c256-142">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="0c256-143">Otwórz `MainPage.xaml.cs` pliku (znajdujący się w Eksploratorze rozwiązań w obszarze `MainPage.xaml` węzła) i Wstaw następujący kod w `MainPage` konstruktora:</span><span class="sxs-lookup"><span data-stu-id="0c256-143">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="0c256-144">Nawet jeśli pakiet Newtonsoft.Json dodane do projektu, red zygzaki jest wyświetlany w obszarze `JsonConvert` ponieważ potrzebne `using` instrukcji w górnej części pliku kodu:</span><span class="sxs-lookup"><span data-stu-id="0c256-144">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="0c256-145">Tworzenie i uruchamianie aplikacji, naciskając klawisz F5 lub wybranie **Debuguj > Rozpocznij debugowanie**:</span><span class="sxs-lookup"><span data-stu-id="0c256-145">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Początkowe dane wyjściowe aplikacji platformy uniwersalnej systemu Windows](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="0c256-147">Wybierz przycisk, aby wyświetlić zawartość obiektu TextBlock zastąpione tekst JSON:</span><span class="sxs-lookup"><span data-stu-id="0c256-147">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Dane wyjściowe aplikacji platformy uniwersalnej systemu Windows po wybraniu przycisku](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="0c256-149">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="0c256-149">Related articles</span></span>

- [<span data-ttu-id="0c256-150">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="0c256-150">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="0c256-151">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="0c256-151">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="0c256-152">Sposoby instalacji pakietu</span><span class="sxs-lookup"><span data-stu-id="0c256-152">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="0c256-153">Konfigurowanie zachowania programu NuGet</span><span class="sxs-lookup"><span data-stu-id="0c256-153">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)