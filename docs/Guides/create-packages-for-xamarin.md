---
title: "Tworzenie pakietów NuGet i Platform (dla systemu iOS, Android i Windows) | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Przewodnik end-to-end tworzenia pakietów NuGet dla platformy Xamarin w systemie macierzystych interfejsów API dla systemu iOS, Android i Windows."
keywords: "Utwórz pakiet, pakietów dla platformy Xamarin, pakietów i platform"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f0131e4f447e2e0ab5a1d17e476a425eaa01b61
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/01/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="4fc72-104">Tworzenie pakietów i platform</span><span class="sxs-lookup"><span data-stu-id="4fc72-104">Create cross-platform packages</span></span>

<span data-ttu-id="4fc72-105">Pakiet wieloplatformowych zawiera kod, który używa macierzystych interfejsów API w systemach iOS, Android i Windows, w zależności od środowiska wykonawczego systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="4fc72-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="4fc72-106">Chociaż jest to prosty zrobić, zaleca się pozwala deweloperom korzystać z pakietu z PCL lub powierzchnia .NET standardowych bibliotek za pośrednictwem wspólnego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4fc72-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="4fc72-107">W tym przewodniku tworzenia pakietu NuGet i platform, który może być używana w przenośnych projekty w systemach iOS, Android i Windows.</span><span class="sxs-lookup"><span data-stu-id="4fc72-107">In this walkthrough you create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="4fc72-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4fc72-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="4fc72-109">Tworzenie projektu kodu struktury i abstrakcji</span><span class="sxs-lookup"><span data-stu-id="4fc72-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="4fc72-110">Wpisz swój kod specyficzne dla platformy</span><span class="sxs-lookup"><span data-stu-id="4fc72-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="4fc72-111">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="4fc72-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="4fc72-112">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="4fc72-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="4fc72-113">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="4fc72-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="4fc72-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4fc72-114">Pre-requisites</span></span>

1. <span data-ttu-id="4fc72-115">Visual Studio 2015 z platformy uniwersalnej systemu Windows (UWP) i Xamarin.</span><span class="sxs-lookup"><span data-stu-id="4fc72-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="4fc72-116">Bezpłatnie zainstalować Community edition z [visualstudio.com](https://www.visualstudio.com/); oczywiście można również wersje Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4fc72-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="4fc72-117">Aby dołączyć narzędzia platformy uniwersalnej systemu Windows i program Xamarin, wybierz Instalacja niestandardowa, a następnie wybierz odpowiednie opcje.</span><span class="sxs-lookup"><span data-stu-id="4fc72-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="4fc72-118">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="4fc72-118">NuGet CLI.</span></span> <span data-ttu-id="4fc72-119">Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4fc72-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="4fc72-120">Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="4fc72-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="4fc72-121">nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="4fc72-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="4fc72-122">Tworzenie projektu kodu struktury i abstrakcji</span><span class="sxs-lookup"><span data-stu-id="4fc72-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="4fc72-123">Pobierz i uruchom [wtyczki dla rozszerzenia szablonów Xamarin](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4fc72-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="4fc72-124">Te szablony ułatwi późniejszą tworzenia struktury projektu na potrzeby tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="4fc72-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="4fc72-125">W programie Visual Studio **Plik > Nowy > Projekt**, wyszukiwania `Plugin`, wybierz pozycję **dodatek plug-in dla platformy Xamarin** szablonu, Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="4fc72-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nowy projekt pusta aplikacja (przenośna platformy Xamarin.Forms) w programie Visual Studio](media/CrossPlatform-NewProject.png)

<span data-ttu-id="4fc72-127">Wynikowa rozwiązania zawiera dwa projekty PCL, wraz z różnych projektów specyficzne dla platformy:</span><span class="sxs-lookup"><span data-stu-id="4fc72-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="4fc72-128">PCL o nazwie `Plugin.LoggingLibrary.Abstractions (Portable)`, w tym przypadku definiuje interfejs publiczny (powierzchni interfejsu API) składnika `ILoggingLibrary` zawarte w pliku ILoggingLibrary.cs interfejsu.</span><span class="sxs-lookup"><span data-stu-id="4fc72-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="4fc72-129">Jest to, gdzie zdefiniować interfejs do biblioteki.</span><span class="sxs-lookup"><span data-stu-id="4fc72-129">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="4fc72-130">Inne PCL `Plugin.LoggingLibrary (Portable)`, zawiera kod w CrossLoggingLibrary.cs, który będzie zlokalizować specyficzne dla platformy implementację abstrakcyjnej interfejsu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4fc72-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="4fc72-131">Zwykle nie należy do modyfikowania tego pliku.</span><span class="sxs-lookup"><span data-stu-id="4fc72-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="4fc72-132">Projekty poszczególnych platform, takich jak `Plugin.LoggingLibrary.Android`, każdy zawiera zawierają natywnych implementacji interfejsu w ich odpowiednich plików LoggingLibraryImplementation.cs.</span><span class="sxs-lookup"><span data-stu-id="4fc72-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="4fc72-133">Jest to, które służy do tworzenia biblioteki kodu.</span><span class="sxs-lookup"><span data-stu-id="4fc72-133">This is where you build out your library's code.</span></span>

<span data-ttu-id="4fc72-134">Domyślnie plik ILoggingLibrary.cs projektu abstrakcje zawiera definicję interfejsu, ale żadnych metod.</span><span class="sxs-lookup"><span data-stu-id="4fc72-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="4fc72-135">Na potrzeby tego przewodnika, Dodaj `Log` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4fc72-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="4fc72-136">Wpisz swój kod specyficzne dla platformy</span><span class="sxs-lookup"><span data-stu-id="4fc72-136">Write your platform-specific code</span></span>

<span data-ttu-id="4fc72-137">Aby zaimplementować implementacja specyficzna dla platformy `ILoggingLibrary` interfejsu i jego metod, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4fc72-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="4fc72-138">Otwórz `LoggingLibraryImplementation.cs` pliku każdej platformy projektu i dodać wymagany kod.</span><span class="sxs-lookup"><span data-stu-id="4fc72-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="4fc72-139">Na przykład (przy użyciu `Plugin.LoggingLibrary.Android` projektu):</span><span class="sxs-lookup"><span data-stu-id="4fc72-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="4fc72-140">Powtórz tej implementacji w projektach dla wszystkich platform, które mają być obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4fc72-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="4fc72-141">Kliknij prawym przyciskiem myszy projekt iOS, wybierz **właściwości**, kliknij przycisk **kompilacji** i Usuń "\iPhone" z **ścieżka wyjściowa** i **pliku dokumentacji XML**  ustawienia.</span><span class="sxs-lookup"><span data-stu-id="4fc72-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="4fc72-142">Dotyczy to tylko nowsze wygodę w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="4fc72-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="4fc72-143">Zapisz plik po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="4fc72-143">Save the file when done.</span></span>
1. <span data-ttu-id="4fc72-144">Kliknij prawym przyciskiem myszy rozwiązanie, wybierz **programu Configuration Manager...** i sprawdź **kompilacji** pól PCLs i poszczególnych platform w przypadku obsługi.</span><span class="sxs-lookup"><span data-stu-id="4fc72-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="4fc72-145">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** Sprawdź swoją pracę i utworzyć artefaktów, które można następnie pakietu.</span><span class="sxs-lookup"><span data-stu-id="4fc72-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="4fc72-146">Jeśli występują błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz **przywracania pakietów NuGet** zainstalować zależności i skompiluj ponownie.</span><span class="sxs-lookup"><span data-stu-id="4fc72-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="4fc72-147">Aby utworzyć dla systemu iOS należy Mac sieciowe podłączone do programu Visual Studio, zgodnie z opisem w [wprowadzenie do platformy Xamarin.iOS dla programu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="4fc72-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="4fc72-148">Jeśli nie masz dostępnych Mac, należy wyczyścić projektu systemu iOS w programie configuration manager (krok 3 powyżej).</span><span class="sxs-lookup"><span data-stu-id="4fc72-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="4fc72-149">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="4fc72-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="4fc72-150">Otwórz wiersz polecenia, przejdź do `LoggingLibrary` folderu o jeden poziom poniżej where `.sln` pliku jest i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `Package.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="4fc72-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```cli
nuget spec
```

1. <span data-ttu-id="4fc72-151">Zmień nazwę tego pliku do `LoggingLibrary.nuspec` i otwórz go w edytorze.</span><span class="sxs-lookup"><span data-stu-id="4fc72-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="4fc72-152">Zaktualizuj plik zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="4fc72-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="4fc72-153">`<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="4fc72-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="4fc72-154">Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="4fc72-154">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="4fc72-155">Można sufiks wersji pakietu z `-alpha`, `-beta` lub `-rc` aby oznaczyć do pakietu jako wersji wstępnej, sprawdź [wersje wstępne](../create-packages/prerelease-packages.md) uzyskać więcej informacji o wersji wstępnych.</span><span class="sxs-lookup"><span data-stu-id="4fc72-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="4fc72-156">Dodawanie zestawów odwołań</span><span class="sxs-lookup"><span data-stu-id="4fc72-156">Add reference assemblies</span></span>

<span data-ttu-id="4fc72-157">Aby uwzględnić zestawy referencyjne specyficzne dla platformy, Dodaj następujący kod do `<files>` elementu `LoggingLibrary.nuspec` odpowiednio dla obsługiwanych platform:</span><span class="sxs-lookup"><span data-stu-id="4fc72-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="4fc72-158">Aby skrócić nazwy plików DLL i kod XML, kliknij prawym przyciskiem myszy na żadnym konkretnym projektem, wybierz opcję **biblioteki** , a następnie zmień nazwy zestawu.</span><span class="sxs-lookup"><span data-stu-id="4fc72-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="4fc72-159">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="4fc72-159">Add dependencies</span></span>

<span data-ttu-id="4fc72-160">Jeśli masz określonych zależności dla implementacji native użyj `<dependencies>` element z `<group>` elementy, aby określić, na przykład:</span><span class="sxs-lookup"><span data-stu-id="4fc72-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="4fc72-161">Na przykład następujące ustawiał iTextSharp jako zależność UAP docelowych:</span><span class="sxs-lookup"><span data-stu-id="4fc72-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="4fc72-162">Końcowe .nuspec</span><span class="sxs-lookup"><span data-stu-id="4fc72-162">Final .nuspec</span></span>

<span data-ttu-id="4fc72-163">Twoje final `.nuspec` pliku powinna wyglądać podobnie do następującego: gdzie ponownie twoje_imie należy zamienić na odpowiednie wartości:</span><span class="sxs-lookup"><span data-stu-id="4fc72-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="4fc72-164">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="4fc72-164">Package the component</span></span>

<span data-ttu-id="4fc72-165">Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="4fc72-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="4fc72-166">Spowoduje to wygenerowanie `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4fc72-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="4fc72-167">Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="4fc72-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Wyświetlanie pakietu LoggingLibrary Explorer pakietu NuGet](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="4fc72-169">A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="4fc72-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="4fc72-170">Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="4fc72-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="4fc72-171">Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4fc72-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="4fc72-172">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="4fc72-172">Related topics</span></span>

- [<span data-ttu-id="4fc72-173">Plik Nuspec odwołania</span><span class="sxs-lookup"><span data-stu-id="4fc72-173">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="4fc72-174">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="4fc72-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="4fc72-175">Przechowywanie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="4fc72-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="4fc72-176">Obsługa wielu wersje programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fc72-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4fc72-177">W tym właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="4fc72-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="4fc72-178">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="4fc72-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)