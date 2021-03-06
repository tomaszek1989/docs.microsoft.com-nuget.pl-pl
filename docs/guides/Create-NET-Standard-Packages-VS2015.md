---
title: Tworzenie .NET Standard i pakiety NuGet programu .NET Framework przy użyciu programu Visual Studio 2015
description: Przewodnik end-to-end tworzenia pakietów platformy .NET Standard i NuGet programu .NET Framework za pomocą NuGet 3.x i programu Visual Studio 2015.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: c66e782ea5d4e9e2a9585d8301dc2a1b2e8c72b9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818737"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Utwórz pakiety .NET Standard i .NET Framework z programem Visual Studio 2015

**Uwaga:** 2017 usługi Visual Studio jest zalecane w przypadku tworzenia bibliotek .NET Standard. Visual Studio 2015 może działać, ale narzędzi platformy .NET Core został przeniesiony do trybu tylko do podglądu stanu. Zobacz [tworzenie i publikowanie pakietu z programu Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+ i Visual Studio 2017 r.

[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET. Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia. Umożliwia ona deweloperom tworzyć kod, który jest można używać we wszystkich programów .NET i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.

Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu NuGet przeznaczonych dla platformy .NET Standard 1.4 biblioteki lub pakietu przeznaczonych dla platformy .NET Framework 4.6. Biblioteki standardowe 1.4 .NET działa za pośrednictwem platformy .NET Framework 4.6.1, uniwersalnych systemu Windows 10 platformy .NET Core i Mono/Xamarin. Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja .NET). Można wybrać innych wersji biblioteki standardowej .NET, jeśli chcesz.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2015 Update 3
1. (Tylko standardowe .NET) [.NET core SDK](https://www.microsoft.com/net/download/)
1. Interfejs wiersza polecenia NuGet. Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji. Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.

    > [!Note]
    > nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.

## <a name="create-the-class-library-project"></a>Tworzenie projektu biblioteki klas

1. W programie Visual Studio **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > systemu Windows** węzła, wybierz opcję **biblioteki klas (przenośna)**, Zmień nazwę na AppLogger i wybierz **OK**.

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. W **dodać przenośnej biblioteki klas** okno dialogowe zostanie wyświetlone, wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`. (Jeśli przeznaczonych dla platformy .NET Framework, można wybrać dowolną wskazaną opcje są odpowiednie.)

1. Jeśli przeznaczonych dla platformy .NET Standard, kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **biblioteki** , a następnie wybierz **docelowej platformy .NET Standard** w **docelowych** sekcji. Ta akcja monituje o potwierdzenie, po którym można wybrać `.NET Standard 1.4` (lub inna wersja dostępna) z listy rozwijanej:

    ![Ustawienie docelowej platformy .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. Polecenie **kompilacji** Zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.

1. Dodaj swój kod do składnika, na przykład:

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. Ustaw konfigurację do wersji, skompilować projekt i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release` folderu.

## <a name="create-and-update-the-nuspec-file"></a>Tworzenie i aktualizowanie pliku .nuspec

1. Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogger.csproj` folder (jeden poziom w dół where `.sln` pliku), i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `AppLogger.nuspec` pliku:

    ```cli
    nuget spec
    ```

1. Otwórz `AppLogger.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość. `<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. Dodaj zestawy odwołań `.nuspec` plików, to znaczy biblioteki DLL i pliku IntelliSense XML:

    Jeśli przeznaczonych dla platformy .NET Standard, wpisy zostaną wyświetlone podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    Jeśli przeznaczonych dla platformy .NET Framework, wpisy zostaną wyświetlone podobne do następujących:

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** do wygenerowania wszystkich plików w pakiecie.

### <a name="declaring-dependencies"></a>Deklarowanie zależności

Jeśli jest zależne od innych pakietów NuGet, listy w manifeście `<dependencies>` element z `<group>` elementów. Na przykład aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszym, należy dodać:

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

Składnia *wersji* tutaj wskazuje, czy w wersji 8.0.3 lub nowszy jest dopuszczalne atrybutu. Aby określić inną wersję zakresów, zapoznaj się [wersji pakietu](../reference/package-versioning.md).

### <a name="adding-a-readme"></a>Dodawanie pliku readme

Tworzenie sieci `readme.txt` pliku, umieść go w folderze głównym projektu i odwołuje się do niego w `.nuspec` pliku:

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

Visual Studio wyświetlania `readme.txt` po zainstalowaniu pakietu do projektu. Plik nie jest wyświetlane, gdy zainstalowane w projektach platformy .NET Core lub pakietów, które są zainstalowane jako zależność.

## <a name="package-the-component"></a>Pakiet składnika

Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:

```cli
nuget pack AppLogger.nuspec
```

Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`. Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość (wyświetlane dla platformy .NET Standard):

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie. Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.

Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).

Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux. Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.

## <a name="related-topics"></a>Tematy pokrewne

- [odwołanie .nuspec](../reference/nuspec.md)
- [Obsługa wielu wersje programu .NET framework](../create-packages/supporting-multiple-target-frameworks.md)
- [Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md)
- [Pakiety symboli](../create-packages/symbol-packages.md)
- [Przechowywanie wersji pakietów](../reference/package-versioning.md)
- [Dokumentacja biblioteki standardowej .NET](/dotnet/articles/standard/library)
- [Eksportowanie do platformy .NET Core z .NET Framework](/dotnet/articles/core/porting/index)
