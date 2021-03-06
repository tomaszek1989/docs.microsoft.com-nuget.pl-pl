---
title: Odwołanie do pliku .nuspec dla NuGet
description: Plik .nuspec zawiera metadane pakietów używane podczas tworzenia pakietu i do dostarczania informacji klientów pakietu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 142f82386395b8ab2ed1d57218db9bc1d2e98638
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843449"
---
# <a name="nuspec-reference"></a>odwołanie .nuspec

A `.nuspec` plik jest manifestu XML, który zawiera metadane pakietów. Ten manifest służy do tworzenia pakietu i podaj informacje dla klientów. Manifest zawsze znajduje się w pakiecie.

W tym temacie:

- [Ogólna postać i schematu](#general-form-and-schema)
- [Zastąpienia tokenów](#replacement-tokens) (jeśli jest używana w projekcie programu Visual Studio)
- [Zależności](#dependencies)
- [Odwołania do zestawów jawne](#explicit-assembly-references)
- [Odwołania zestawu](#framework-assembly-references)
- [W tym pliki zestawu](#including-assembly-files)
- [W tym pliki zawartości](#including-content-files)
- [Przykłady](#examples)

## <a name="general-form-and-schema"></a>Ogólna postać i schematu

Bieżący `nuspec.xsd` można znaleźć w pliku schematu [repozytorium NuGet GitHub](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

W tym schemacie `.nuspec` plik ma następującą postać ogólne:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Wizualnych reprezentacji schematu, otwórz plik schematu w programie Visual Studio w trybie projektowania, a następnie kliknij przycisk na **Eksploratora schematu XML** łącza. Alternatywnie Otwórz plik jako kod, kliknij prawym przyciskiem myszy w edytorze i wybierz **Pokaż Eksploratora schematu XML**. W obu przypadkach, uzyskasz widoku podobne do pokazanego poniżej (w przypadku większości rozwinięte):

![Visual Studio Explorer schematu z nuspec.xsd Otwórz](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Atrybuty metadanych

`<metadata>` Obsługuje element atrybutów opisanych w poniższej tabeli.

| Atrybut | Wymagane | Opis |
| --- | --- | --- | 
| **minClientVersion** | Nie | Określa minimalną wersję klienta NuGet, który można zainstalować ten pakiet, wymuszane przez nuget.exe oraz Menedżera pakietów programu Visual Studio. Jest on używany zawsze wtedy, gdy pakiet jest zależny od określonych funkcji `.nuspec` plików, które zostały dodane w konkretnej wersji klienta programu NuGet. Na przykład pakiet przy użyciu `developmentDependency` atrybut należy określić "2.8" dla `minClientVersion`. Podobnie, pakiet przy użyciu `contentFiles` (zobacz następną sekcję) należy ustawić element `minClientVersion` do "3.3". Należy zauważyć, że ponieważ klienci programu NuGet przed 2.5 nie rozpoznają tej flagi należy ich *zawsze* odmówić można zainstalować pakietu, niezależnie od tego, co `minClientVersion` zawiera. |

### <a name="required-metadata-elements"></a>Elementy wymagane metadane

Mimo że następujące elementy są minimalne wymagania dotyczące pakietu, należy rozważyć dodanie [elementy opcjonalne metadane](#optional-metadata-elements) usprawniających atrakcyjniejsze środowisko pracy deweloperzy muszą z pakietem.

Te elementy muszą znajdować się w `<metadata>` elementu.

| Element | Opis |
| --- | --- |
| **id** | Identyfikator pakietu bez uwzględniania wielkości liter, który musi być unikatowa w witrynie nuget.org lub cokolwiek innego pakietu, który znajduje się w galerii. Identyfikatory nie mogą zawierać spacji ani znaków, które nie są prawidłowe dla danego adresu URL i zazwyczaj korzystają z reguły w przestrzeni nazw .NET. Zobacz [wybierając identyfikator unikatowy pakiet](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) wskazówki. |
| **Wersja** | Wersja pakietu, następujące *Wersja_główna.WERSJA_POMOCNICZA.poprawka* wzorca. Numery wersji mogą zawierać sufiks wersji wstępnej, zgodnie z opisem w [przechowywanie wersji pakietów](../reference/package-versioning.md#pre-release-versions). |
| **Opis elementu** | Długi opis pakietu do wyświetlania w interfejsie użytkownika. |
| **Autorzy** | Rozdzielana przecinkami lista autorów pakietów, pasujące nazwy profilu w witrynie nuget.org. Te są wyświetlane w galerii pakietów NuGet w witrynie nuget.org i są odwoływania się do pakietów przez ten sam autorów. |

### <a name="optional-metadata-elements"></a>Elementy opcjonalne metadane

Te elementy mogą być widoczne w `<metadata>` elementu.

#### <a name="single-elements"></a>Pojedyncze elementy

| Element | Opis |
| --- | --- |
| **Tytuł** | Tytuł przyjaznego dla człowieka pakietu, zwykle używanych w interfejsie użytkownika wyświetla w witrynach nuget.org i Menedżera pakietów w programie Visual Studio. Jeśli nie zostanie określony, identyfikator pakietu jest używany. |
| **Właściciele** | Rozdzielana przecinkami lista twórców pakietów przy użyciu nazwy profilu w witrynie nuget.org. Jest to często tej samej listy podobnie jak w `authors`i jest ignorowana podczas przekazywania pakietu na stronie nuget.org. Zobacz [właścicieli pakietu zarządzania w witrynie nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | Adres URL strony głównej pakietu, często wyświetlany w użytkownika, jak również adres nuget.org. |
| **licenseUrl** | Adres URL licencji pakietu, często wyświetlany w użytkownika, jak również adres nuget.org. |
| **iconUrl** | Adres URL obrazu 64 x 64 z przezroczystość tła do użycia jako ikona dla pakietu wyświetlania w interfejsie użytkownika. Pamiętaj, że ten element zawiera *bezpośredni adres URL obrazu* a nie jej adres URL strony sieci web zawierającej obraz. Na przykład, aby użyć obrazu z witryny GitHub, należy użyć plik raw, takie jak adres URL <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>. |
| **requireLicenseAcceptance** | Wartość logiczna określająca, czy klient musi monitować konsumenta o zaakceptowanie licencji pakietu przed zainstalowaniem pakietu. |
| **developmentDependency** | *(2.8 +)*  Wartość logiczna określająca, czy pakiet jest oznaczone jako — tylko zależnością programistyczną, co zapobiega uwzględniane jako zależności w innych pakietach pakietu. |
| **Podsumowanie** | Krótki opis pakietu do wyświetlania w interfejsie użytkownika. Jeśli argument jest pominięty, skróconą wersję `description` jest używany. |
| **releaseNotes** | *(w wersji 1.5 +)*  Opis zmian wprowadzonych w tej wersji pakietu, często używany w interfejsie użytkownika, takich jak **aktualizacje** kartę z Menedżera pakietów Visual Studio zamiast opisu pakietu. |
| **copyright** | *(w wersji 1.5 +)*  Copyright szczegóły pakietu. |
| **Język** | Identyfikator ustawień regionalnych dla pakietu. Zobacz [tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md). |
| **tagi**  | Rozdzielany spacjami lista tagów i słów kluczowych, które opisują możliwości pakietu i pomocy pakietów za pomocą wyszukiwania i filtrowania. |
| **serviceable** | *(3.3 +)*  NuGet wewnętrznego użytku tylko. |
| **repozytorium** | Metadane repozytorium, składający się z czterech atrybuty opcjonalne: *typu* i *adresu url* *(4.0 i nowsze)*, i *gałęzi* i  *zatwierdzenie* *(4.6 +)*. Te atrybuty zezwalać na mapowanie .nupkg do repozytorium, którego kompilacja, z których można pobrać jak wyjaśniono, jak poszczególne gałęzi lub zatwierdzania, który skompilowany pakiet. |

#### <a name="collection-elements"></a>Elementy kolekcji

| Element | Opis |
| --- | --- |
**packageTypes** | *(3.5 +)*  Zbiór zero lub więcej `<packageType>` elementów, określając typ pakietu, jeśli inne niż tradycyjne zależności pakietu. Każdy packageType ma atrybuty *nazwa* i *wersji*. Zobacz [ustawienie typu pakietu](../create-packages/creating-a-package.md#setting-a-package-type). |
| **zależności** | Kolekcja zero lub więcej `<dependency>` elementy określenie zależności dotyczących pakietu. Poszczególne zależności ma atrybuty *identyfikator*, *wersji*, *obejmują* (3.x+) i *wykluczyć* (3.x+). Zobacz [zależności](#dependencies) poniżej. |
| **frameworkAssemblies** | *(1.2 +)*  Zbiór zero lub więcej `<frameworkAssembly>` elementów identyfikowanie odwołania do zestawów .NET Framework, które wymaga tego pakietu, dzięki któremu czy odwołania są dodawane do projektów, korzystanie z pakietu. Została każda frameworkAssembly *assemblyName* i *targetFramework* atrybutów. Zobacz [określenie zestawu struktury odwołuje się do globalnej pamięci podręcznej zestawów](#specifying-framework-assembly-references-gac) poniżej. |
| **odwołania** | *(w wersji 1.5 +)*  Zbiór zero lub więcej `<reference>` elementy nazewnictwa zestawów, w tym pakiecie `lib` folderu, które są dodawane jako odwołania do projektu. Każde odwołanie zawiera *pliku* atrybutu. `<references>` może również zawierać `<group>` element z *targetFramework* atrybut, który następnie zawiera `<reference>` elementów. Jeśli argument jest pominięty, wszystkie odwołania w `lib` są uwzględniane. Zobacz [odwołania do zestawów jawne określenie](#specifying-explicit-assembly-references) poniżej. |
| **contentFiles** | *(3.3 +)*  Zbiór `<files>` elementy, które identyfikują plików zawartości do uwzględnienia w projekcie odbierająca komunikaty. Te pliki są określane przy użyciu zestawu atrybutów, które opisują, jak powinna być używana w ramach systemu projektu. Zobacz [określenie plików do uwzględnienia w pakiecie](#specifying-files-to-include-in-the-package) poniżej. |

### <a name="files-element"></a>Element Pliki

`<package>` Węzeł może zawierać `<files>` węzeł jako element równorzędny do `<metadata>`, a lub `<contentFiles>` podrzędne w ramach `<metadata>`, aby określić, które pliki zestawu i zawartości do uwzględnienia w pakiecie. Zobacz [w tym pliki zestawu](#including-assembly-files) i [pliki zawartości w tym](#including-content-files) później w tym temacie, aby uzyskać szczegółowe informacje.

## <a name="replacement-tokens"></a>Zastąpienia tokenów

Podczas tworzenia pakietu [ `nuget pack` polecenia](../tools/cli-ref-pack.md) zastępuje rozdzielonych $ tokenów w `.nuspec` pliku `<metadata>` węzła z wartości, które pochodzą z poziomu pliku projektu lub `pack` polecenia `-properties`przełącznika.

W wierszu polecenia określ wartości tokenu `nuget pack -properties <name>=<value>;<name>=<value>`. Na przykład takie jak możesz użyć tokenu `$owners$` i `$desc$` w `.nuspec` i podaj wartości w pakowania czasu w następujący sposób:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Aby użyć wartości z projektem, określ tokenów opisane w poniższej tabeli (AssemblyInfo odwołuje się do pliku w `Properties` takich jak `AssemblyInfo.cs` lub `AssemblyInfo.vb`).

Aby korzystać z tych tokenów, należy uruchomić `nuget pack` przy użyciu pliku projektu, a nie po prostu `.nuspec`. Na przykład przy użyciu następującego polecenia `$id$` i `$version$` tokenów w `.nuspec` pliku są zastępowane projektu `AssemblyName` i `AssemblyVersion` wartości:

```ps
nuget pack MyProject.csproj
```

Zazwyczaj w przypadku projektu tworzony `.nuspec` początkowo przy użyciu `nuget spec MyProject.csproj` automatycznie zawierający niektóre z tych tokenów standardowych. Jednakże jeśli projekt nie ma wartości dla wymaganych `.nuspec` elementów, a następnie `nuget pack` zakończy się niepowodzeniem. Ponadto w przypadku zmiany wartości projektu, upewnij się odbudować przed utworzeniem pakietu; Można to zrobić wygodna przy użyciu polecenia pakietu `build` przełącznika.

Z wyjątkiem produktów `$configuration$`, wartości w projekcie są używane zamiast dowolne przypisane do tego samego tokenu w wierszu polecenia.

| Token | Wartość źródła | Wartość
| --- | --- | ---
| **$id$** | Plik projektu | AssemblyName (tytuł) z pliku projektu |
| **$version$** | AssemblyInfo | AssemblyInformationalVersion, jeśli jest obecna, w przeciwnym razie AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Zestaw bibliotek DLL | Konfiguracja używana do tworzenia zestawu, domyślnie używany do debugowania. Należy pamiętać, że aby utworzyć pakiet za pomocą konfiguracji wydania, należy zawsze używać `-properties Configuration=Release` w wierszu polecenia. |

Tokeny, również może służyć do rozpoznawania ścieżek, po włączeniu [plików zestawu](#including-assembly-files) i [zawartości plików](#including-content-files). Tokeny mają takie same nazwy właściwości programu MSBuild, dzięki czemu można wybrać pliki do uwzględnienia w zależności od bieżącej konfiguracji kompilacji. Na przykład, jeśli używasz następujące generatory kodów w `.nuspec` pliku:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

I kompilowania zestawu którego `AssemblyName` jest `LoggingLibrary` z `Release` konfiguracji w programie MSBuild, a wiersze wynikowe `.nuspec` plik w pakiecie znajduje się w następujący sposób:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Zależności

`<dependencies>` Elemencie `<metadata>` zawiera dowolną liczbę `<dependency>` elementy, które identyfikują innych pakietów, od których zależy Pakiet najwyższego poziomu. Atrybuty dla każdego `<dependency>` są następujące:

| Atrybut | Opis |
| --- | --- |
| `id` | (Wymagane) Identyfikator pakietu zależności, takie jak "EntityFramework" i "NUnit", czyli nazwy nuget.org pakietu zawiera strona pakietu. |
| `version` | (Wymagane) Zakres wersji dopuszczalne jako zależność. Zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards) dla określonej składni. |
| include | Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności do uwzględnienia w pakiecie końcowym. Wartość domyślna to `none`. |
| wykluczanie | Rozdzielana przecinkami lista dołączania/wykluczania tagów (patrz poniżej), wskazujący zależności, które mają zostać wykluczone w pakiecie końcowym. Wartość domyślna to `all`. Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`. Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`. |

| Uwzględnianie/wykluczanie znaczników | Odpowiednie foldery elementu docelowego |
| --- | --- |
| Pliki | Zawartość |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasobów i FrameworkAssemblies |
| kompilacji | lib |
| kompilacja | Kompilacja (cele i właściwości programu MSBuild) |
| natywne | natywne |
| brak | Brak folderów |
| wszystkie | Wszystkie foldery |

Na przykład następujące wiersze wskazywać zależności na `PackageA` wersji 1.1.0 lub nowszej, a `PackageB` wersji 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Następujące wiersze wskazują zależności na te same pakiety, ale określono jako uwzględniane `contentFiles` i `build` folderów `PackageA` i wszystko, ale `native` i `compile` folderów `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Uwaga: Podczas tworzenia `.nuspec` projektu używającego `nuget spec`, zależności, które istnieją w tym projekcie są automatycznie uwzględniane w wynikowym `.nuspec` pliku.

### <a name="dependency-groups"></a>Grupy zależności

*W wersji 2.0 +*

Jako alternatywy dla pojedynczego płaskiej listy, można określić zależności zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<dependencies>`.

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<dependency>` elementów. Te zależności są instalowane razem, gdy platforma docelowa jest zgodny z profilem framework projektu.

`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listę zależności. Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.

> [!Important]
> Nie można się zmieszać format grupy z płaską listą.

W poniższym przykładzie pokazano różnych odmian `<group>` elementu:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Odwołania do zestawów jawne

`<references>` Element jawnie określa zestawy, które projekt docelowy powinny odwoływać się przy użyciu pakietu. Gdy ten element jest obecny, NuGet dodać odwołania do tylko zestawy wymienionych; nie powoduje dodania odwołania do innych zestawów, w tym pakiecie `lib` folderu.

Na przykład następująca `<references>` elementu powoduje, że rozszerzenie NuGet, aby dodać odwołania do tylko `xunit.dll` i `xunit.extensions.dll` nawet, jeśli istnieją dodatkowe zestawy w pakiecie:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Jawne odwołania są zwykle używane dla zestawów tylko w czasie projektowania. Korzystając z [kontrakty kodu](/dotnet/framework/debug-trace-profile/code-contracts), na przykład zestawy umowy muszą być obok zestawów środowiska uruchomieniowego, które mogą rozszerzyć, aby je znaleźć programu Visual Studio, ale zestawy kontraktu nie musi być przywoływanego przez projekt lub skopiowany w projekcie `bin` folderu.

Podobnie jawnych odwołań może służyć do struktur testów jednostek, takich jak XUnit, którą jej narzędzi, zestawy znajdujące się obok zestawów środowiska uruchomieniowego, ale nie wymaga dołączeni ich jako odwołania do projektu.

### <a name="reference-groups"></a>Grupy odwołań

Alternatywą dla pojedynczego płaskiej listy odwołania można określić zgodnie z profilem framework projekt docelowy za pomocą `<group>` elementów w obrębie `<references>`.

Każda grupa ma atrybut o nazwie `targetFramework` i zawiera zero lub więcej `<reference>` elementów. Te odwołania są dodawane do projektu, gdy platforma docelowa jest zgodny z profilem framework projektu.

`<group>` Elementu bez `targetFramework` atrybut jest używany jako domyślny lub fallback listy odwołań. Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework.

> [!Important]
> Nie można się zmieszać format grupy z płaską listą.

W poniższym przykładzie pokazano różnych odmian `<group>` elementu:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Odwołania zestawu

Zestawy struktury są te, które są częścią programu .NET framework i powinien już znajdować się w globalnej pamięci podręcznej zestawów (GAC) dla dowolnej podanej maszyny. Identyfikując te zestawy w ramach `<frameworkAssemblies>` elementu pakietu można upewnij się, że wymagane odwołania są dodawane do projektu, w przypadku, gdy projekt nie ma już odwołania te. Takie zestawy oczywiście nie są uwzględnione w pakiecie bezpośrednio.

`<frameworkAssemblies>` Element zawiera zero lub więcej `<frameworkAssembly>` elementów, z których każdy określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **assemblyName** | (Wymagane) W pełni kwalifikowanej nazwy zestawu. |
| **targetFramework** | (Opcjonalnie) Określa platformę docelową, której dotyczy odwołanie. Jeśli argument jest pominięty, wskazuje, że odwołanie ma zastosowanie do wszystkich środowisk. Zobacz [ustalać platformy docelowe](../reference/target-frameworks.md) identyfikatorów dokładnie framework. |

W poniższym przykładzie pokazano odwołanie do `System.Net` dla wszystkich docelowych struktur i odwołania do `System.ServiceModel` dla programu .NET Framework 4.0 tylko:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>W tym pliki zestawu

Jeśli stosujesz konwencje opisanego w [Tworzenie pakietu](../create-packages/creating-a-package.md), nie trzeba jawnie określić listę plików w `.nuspec` pliku. `nuget pack` Polecenia automatycznie przejmuje on niezbędne pliki.

> [!Important]
> Po zainstalowaniu do projektu pakiet NuGet automatycznie dodaje odwołania do zestawów do pakietu biblioteki dll, *z wyłączeniem* te, które są nazywane `.resources.dll` ponieważ one muszą być zlokalizowane zestawy satelickie. Z tego powodu należy unikać `.resources.dll` dla plików, w przeciwnym razie zawierające kod essential pakietu.

Aby pominąć to zachowanie automatyczne i jawnie kontrolować pliki, które są umieszczone w pakiecie, umieść `<files>` element jako element podrzędny elementu `<package>` (i element równorzędny `<metadata>`), identyfikowanie poszczególnych plików za pomocą oddzielnego `<file>` elementu. Na przykład:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Nuget 2.x i starszych i projektów za pomocą `packages.config`, `<files>` element umożliwia również dołączać niezmienne pliki zawartości, gdy pakiet jest zainstalowany. Za pomocą narzędzi NuGet 3.3 + i projekty PackageReference `<contentFiles>` element jest używany zamiast tego. Zobacz [pliki zawartości w tym](#including-content-files) poniżej szczegółowe informacje.

### <a name="file-element-attributes"></a>Atrybuty elementu pliku

Każdy `<file>` element określa następujące atrybuty:

| Atrybut | Opis |
| --- | --- |
| **src** | Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu. Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną. Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego. |
| **docelowy** | Względna ścieżka do folderu, w pakiecie, gdzie są umieszczone pliki źródłowe, musi zaczynać się od `lib`, `content`, `build`, lub `tools`. Zobacz [tworzenie .nuspec z katalogu roboczego oparty na Konwencji](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji. Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego. |

### <a name="examples"></a>Przykłady

**Pojedynczy zestaw**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Pojedynczy zestaw specyficzne dla platformy docelowej**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Zbiór bibliotek DLL, przy użyciu symboli wieloznacznych**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Biblioteki DLL dla różnych platform**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Wykluczenie plików**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>W tym pliki zawartości

Pliki zawartości są niezmienne pliki, które pakietu musi zawierać się w projekcie. Trwa niezmienne, nie mają one zostać zmodyfikowane przez konsumencki projektu. Pliki zawartości przykład obejmują:

- Obrazy, które są osadzane jako zasoby
- Pliki źródłowe, które już są kompilowane
- Skrypty, które muszą być dołączone do danych wyjściowych kompilacji projektu
- Pliki konfiguracji dla pakietów, które należy uwzględnić w projekcie, ale nie ma potrzeby zmiany specyficzne dla projektu

Zawartość, pliki są zawarte w pakiecie przy użyciu `<files>` elementu, określając `content` folderu w `target` atrybutu. Jednak takie pliki są ignorowane, gdy pakiet jest zainstalowany w projekcie przy użyciu funkcji PackageReference, który zamiast tego używa `<contentFiles>` elementu.

Maksymalna zgodność z wykorzystywanie projektów pakietu najlepiej określa pliki zawartości w oba te elementy.

### <a name="using-the-files-element-for-content-files"></a>Za pomocą elementu plików dla plików zawartości

W przypadku plików zawartości, po prostu użyć tego samego formatu jak w przypadku plików zestawu jednak określić `content` jako podstawowy folder w `target` atrybutu, jak pokazano w poniższych przykładach.

**Podstawowe pliki zawartości**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Pliki zawartości przy użyciu struktury katalogów**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Plik zawartości, które są specyficzne dla platformy docelowej**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Skopiowany do folderu z dot w nazwie pliku zawartości**

W tym przypadku NuGet widzi, że rozszerzenie w `target` nie pasuje do rozszerzenia w `src` i w związku z tym traktuje tę część nazwy w `target` jako folder:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Pliki zawartości, bez rozszerzenia**

Aby dołączyć pliki bez rozszerzenia, należy użyć `*` lub `**` symboli wieloznacznych:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Pliki zawartości głębokości ścieżki i głębokiego obiektem docelowym**

W tym przypadku ponieważ pasuje do rozszerzenia pliku źródłowego i docelowego, NuGet zakłada, że obiekt docelowy jest nazwa pliku, a nie folder:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Zmiana nazwy pliku zawartości w pakiecie**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Wykluczenie plików**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Za pomocą elementu contentFiles dla plików zawartości

*NuGet 4.0 + przy użyciu funkcji PackageReference*

Domyślnie pakiet umieszcza zawartość `contentFiles` folder (patrz poniżej) i `nuget pack` uwzględnione wszystkie pliki w folderze przy użyciu atrybutów domyślnych. W takim przypadku nie jest konieczne uwzględnienie `contentFiles` w węźle `.nuspec` wcale.

Do kontroli, które pliki są uwzględnione `<contentFiles>` element określa to zbiór `<files>` obejmują elementy, które identyfikują konkretne pliki.

Te pliki są określane za pomocą zestaw atrybutów, które opisują, jak powinna być używana w ramach systemu projektu:

| Atrybut | Opis |
| --- | --- |
| **include** | (Wymagane) Lokalizacja pliku lub plików, obejmujący podlegają wykluczenia określonego przez `exclude` atrybutu. Ścieżka jest względem `.nuspec` pliku, chyba że określony jest ścieżką bezwzględną. Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego. |
| **exclude** | Rozdzieloną średnikami listę plików lub wzorce plików do wykluczenia z `src` lokalizacji. Symbol wieloznaczny `*` jest dozwolone i podwójne symbolu wieloznacznego `**` wskazuje folder wyszukiwania rekurencyjnego. |
| **buildAction** | Akcja kompilacji, aby przypisać do elementu zawartości dla platformy MSBuild, takich jak `Content`, `None`, `Embedded Resource`, `Compile`itp. Wartość domyślna to `Compile`. |
| **copyToOutput** | Wartość Boolean wskazującą, czy chcesz skopiować elementy zawartości do kompilacji (lub opublikować) folder wyjściowy. Wartością domyślną jest false. |
| **spłaszczanie** | Wartość logiczna wskazująca, czy skopiować elementy zawartości na pojedynczy folder w danych wyjściowych kompilacji (true) czy zachować strukturę folderów w pakiecie (false). Ta flaga działa tylko, gdy copyToOutput flaga jest ustawiona na wartość true. Wartością domyślną jest false. |

Instalując pakiet NuGet dotyczy elementów podrzędnych `<contentFiles>` od góry do dołu. Jeśli wiele wpisów pasuje do tego samego pliku wszystkie wpisy są stosowane. Wpis umieszczony najwyżej zastępuje wpisy niżej, jeśli występuje konflikt z tego samego atrybutu.

#### <a name="package-folder-structure"></a>Struktura folderów pakietu

Projekt pakietu powinien struktury zawartości przy użyciu następującego wzorca:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` może być `cs`, `vb`, `fs`, `any`, lub litery odpowiednikiem danego `$(ProjectLanguage)`
- `TxM` jest dowolnym prawne krótka nazwa docelowej platformy obsługującej NuGet (zobacz [ustalać platformy docelowe](../reference/target-frameworks.md)).
- Dowolnej struktury folderów może być dołączany na końcu tej składni.

Na przykład:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Puste foldery można użyć `.` zrezygnować z dostarczanie zawartości dla niektórych kombinacji języka i TxM, na przykład:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Sekcji z przykładowym pliki

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>Przykład .nuspec plików

**Prosty `.nuspec` nie określające zależności lub plików**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

**A `.nuspec` z zależnościami**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**A `.nuspec` z plikami**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**A `.nuspec` za pomocą zestawów framework**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

W tym przykładzie poniżej są zainstalowane dla określonego projektu celów:

- .NET4 -> `System.Web`, `System.Net`
- . NET4 -> Profil klienta `System.Net`
- Program Silverlight 3 -> `System.Json`
- Program Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
