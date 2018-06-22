---
title: Tworzenie pakietów NuGet dla platformy uniwersalnej systemu Windows
description: End-to-end Przewodnik tworzenia pakietów NuGet dla platformy uniwersalnej systemu Windows przy użyciu składnika środowiska wykonawczego systemu Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: c5d5bf72b99f6c2fe1b0a708ddb314d5711bc73d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818285"
---
# <a name="create-uwp-packages"></a><span data-ttu-id="cb624-103">Tworzenie pakietów platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cb624-103">Create UWP packages</span></span>

<span data-ttu-id="cb624-104">[Windows platformy Uniwersalnej](https://developer.microsoft.com/windows) zapewnia platformę aplikacji wspólne dla wszystkich urządzeń z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cb624-104">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="cb624-105">W tym modelu aplikacji platformy uniwersalnej systemu Windows można wywołać zarówno WinRT interfejsów API, które są wspólne dla wszystkich urządzeń, a także interfejsów API (w tym Win32 i .NET), które są specyficzne dla rodziny urządzeń, na którym jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="cb624-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="cb624-106">W tym przewodniku tworzenia pakietu NuGet z natywnego platformy uniwersalnej systemu Windows składnika (w tym formancie XAML) używanego w zarządzanego i natywnego projektów.</span><span class="sxs-lookup"><span data-stu-id="cb624-106">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb624-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb624-107">Prerequisites</span></span>

1. <span data-ttu-id="cb624-108">2017 usługi Visual Studio lub Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cb624-108">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="cb624-109">Bezpłatnie zainstalować 2017 Community edition z [visualstudio.com](https://www.visualstudio.com/); można także wersje Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="cb624-109">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="cb624-110">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb624-110">NuGet CLI.</span></span> <span data-ttu-id="cb624-111">Pobierz najnowszą wersję `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji (pobierania `.exe` bezpośrednio).</span><span class="sxs-lookup"><span data-stu-id="cb624-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="cb624-112">Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="cb624-112">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="cb624-113">Tworzenie składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="cb624-113">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="cb624-114">W programie Visual Studio, wybierz **Plik > Nowy > projektu**, rozwiń węzeł **Visual C++ > Windows > uniwersalnych** węzła, wybierz opcję **składnika środowiska wykonawczego systemu Windows (uniwersalny system Windows)** szablonu, Zmień nazwę na ImageEnhancer, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="cb624-114">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="cb624-115">Zaakceptuj wartości domyślne dla wersji docelowej i minimalna wersja po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="cb624-115">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![Tworzenie nowego projektu składnika środowiska wykonawczego systemu Windows platformy uniwersalnej systemu Windows](media/UWP-NewProject.png)

1. <span data-ttu-id="cb624-117">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań wybierz **Dodaj > Nowy element**, kliknij przycisk **Visual C++ > XAML** węzła, wybierz opcję **kontrolki z szablonem**, Zmień nazwę, aby AwesomeImageControl.cpp, a następnie kliknij przycisk **Dodaj**:</span><span class="sxs-lookup"><span data-stu-id="cb624-117">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![Dodawanie nowego elementu opartego na szablonie kontrolki XAML do projektu](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="cb624-119">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **właściwości.**</span><span class="sxs-lookup"><span data-stu-id="cb624-119">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="cb624-120">Na stronie właściwości rozwiń **właściwości konfiguracji > C/C++** i kliknij przycisk **pliki wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="cb624-120">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="cb624-121">W okienku po prawej stronie Zmień wartość atrybutu **generować pliki dokumentacji XML** tak:</span><span class="sxs-lookup"><span data-stu-id="cb624-121">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![Ustawienia Generuj pliki dokumentacji XML tak.](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="cb624-123">Kliknij prawym przyciskiem myszy *rozwiązania* teraz, wybierz **tworzenia partii**, sprawdź trzy pola debugowania w oknie dialogowym, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cb624-123">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="cb624-124">Dzięki temu się upewnić, że w po wykonaniu kompilacji wygenerować pełny zestaw artefaktów dla poszczególnych systemów docelowych, obsługiwanych przez usługę systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="cb624-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![Wsadowe kompilacji](media/UWP-BatchBuild.png)

1. <span data-ttu-id="cb624-126">W zadaniu wsadowym Tworzenie okna dialogowego, a następnie kliknij przycisk **kompilacji** Sprawdź projektu i tworzenia plików wyjściowych wymagające pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb624-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="cb624-127">W tym przewodniku używasz artefakty debugowania dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="cb624-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="cb624-128">Dla pakietu bez debugowania zamiast tego Sprawdź opcje wersji w oknie dialogowym Tworzenie partii i zapoznaj się wynikowy folderów wersji w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="cb624-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="cb624-129">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="cb624-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="cb624-130">Aby utworzyć pierwszy `.nuspec` plików, wykonaj poniższe trzy kroki.</span><span class="sxs-lookup"><span data-stu-id="cb624-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="cb624-131">Sekcje, które należy wykonać, a następnie przedstawiono inne niezbędne aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="cb624-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="cb624-132">Otwórz wiersz polecenia i przejdź do folderu zawierającego `ImageEnhancer.vcxproj` (są to podfolder poniżej, gdzie to plik rozwiązania).</span><span class="sxs-lookup"><span data-stu-id="cb624-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="cb624-133">Uruchom NuGet `spec` polecenie, aby wygenerować `ImageEnhancer.nuspec` (nazwa pliku jest pobierana z nazwy `.vcxproj` plików):</span><span class="sxs-lookup"><span data-stu-id="cb624-133">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="cb624-134">Otwórz `ImageEnhancer.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="cb624-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="cb624-135">`<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="cb624-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="cb624-136">Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="cb624-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="cb624-137">Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na `<tags>` element, jak te znaczniki ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="cb624-137">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="cb624-138">Dodawanie metadanych systemu Windows do pakietu</span><span class="sxs-lookup"><span data-stu-id="cb624-138">Adding Windows metadata to the package</span></span>

<span data-ttu-id="cb624-139">Składnik środowiska uruchomieniowego systemu Windows wymaga metadanych, które opisują wszystkich typów publicznie dostępnych, co umożliwia dla innych aplikacji i bibliotek użycie składnika.</span><span class="sxs-lookup"><span data-stu-id="cb624-139">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="cb624-140">Te metadane znajduje się w pliku winmd, który jest tworzony podczas kompilowania projektu i muszą być zawarte w pakiecie NuGet.</span><span class="sxs-lookup"><span data-stu-id="cb624-140">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="cb624-141">Plik XML z danymi IntelliSense jest również zbudowana w tym samym czasie i powinna być również uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="cb624-141">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="cb624-142">Dodaj następujące `<files>` węzeł `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="cb624-142">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="cb624-143">Dodawanie zawartości XAML</span><span class="sxs-lookup"><span data-stu-id="cb624-143">Adding XAML content</span></span>

<span data-ttu-id="cb624-144">Aby uwzględnić XAML formantu o składnika, należy dodać pliku XAML, który ma szablonu domyślnego dla formantu (wygenerowane przez szablon projektu).</span><span class="sxs-lookup"><span data-stu-id="cb624-144">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="cb624-145">Może to również przechodzi `<files>` sekcji:</span><span class="sxs-lookup"><span data-stu-id="cb624-145">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="cb624-146">Dodawanie bibliotek implementacji natywnej</span><span class="sxs-lookup"><span data-stu-id="cb624-146">Adding the native implementation libraries</span></span>

<span data-ttu-id="cb624-147">W ramach składnika, logiki core typu ImageEnhancer jest w kodzie natywnym, który znajduje się w różnych `ImageEnhancer.dll` zestawy, które są generowane dla poszczególnych docelowych runtime (x 86 i x64 ARM).</span><span class="sxs-lookup"><span data-stu-id="cb624-147">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="cb624-148">Aby uwzględnić je w pakiecie, odwoływać je w `<files>` sekcji wraz z ich plików zasobów .pri skojarzone:</span><span class="sxs-lookup"><span data-stu-id="cb624-148">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="cb624-149">Dodawanie .targets</span><span class="sxs-lookup"><span data-stu-id="cb624-149">Adding .targets</span></span>

<span data-ttu-id="cb624-150">Następnie projektów C++ i JavaScript, które mogą korzystać z pakietu NuGet muszą pliku .targets w celu identyfikowania niezbędne pliki zestawu i winmd.</span><span class="sxs-lookup"><span data-stu-id="cb624-150">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="cb624-151">(C# i Visual Basic, projekty w tym automatycznie.) Utwórz ten plik przez skopiowanie poniższy tekst do `ImageEnhancer.targets` i zapisz go w tym samym folderze co `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="cb624-151">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="cb624-152">_Uwaga_: to `.targets` pliku musi mieć taką samą nazwę jak identyfikator pakietu (np. `<Id>` element `.nupspec` pliku):</span><span class="sxs-lookup"><span data-stu-id="cb624-152">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="cb624-153">Następnie można znaleźć `ImageEnhancer.targets` w Twojej `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="cb624-153">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="cb624-154">Końcowe .nuspec</span><span class="sxs-lookup"><span data-stu-id="cb624-154">Final .nuspec</span></span>

<span data-ttu-id="cb624-155">Twoje final `.nuspec` pliku powinna wyglądać podobnie do następującego: gdzie ponownie twoje_imie należy zamienić na odpowiednie wartości:</span><span class="sxs-lookup"><span data-stu-id="cb624-155">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="cb624-156">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="cb624-156">Package the component</span></span>

<span data-ttu-id="cb624-157">Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="cb624-157">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="cb624-158">Spowoduje to wygenerowanie `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="cb624-158">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="cb624-159">Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="cb624-159">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Wyświetlanie pakietu ImageEnhancer Explorer pakietu NuGet](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="cb624-161">A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="cb624-161">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="cb624-162">Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="cb624-162">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="cb624-163">Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="cb624-163">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="cb624-164">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="cb624-164">Related topics</span></span>

- [<span data-ttu-id="cb624-165">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="cb624-165">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="cb624-166">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="cb624-166">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="cb624-167">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="cb624-167">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="cb624-168">Obsługa wielu wersje programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cb624-168">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="cb624-169">Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="cb624-169">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="cb624-170">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="cb624-170">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)