---
title: Tworzenie zlokalizowanych pakietów NuGet
description: Szczegółowe informacje na dwa sposoby tworzenia zlokalizowane pakiety NuGet, w tym wszystkie zestawy w jednym pakiecie lub publikowanie osobnych zestawów.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 1088f174c6a1ec21f876ccc3d79c9b40eee4758f
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817795"
---
# <a name="creating-localized-nuget-packages"></a>Tworzenie zlokalizowanych pakietów NuGet

Istnieją dwa sposoby tworzenia zlokalizowane wersje biblioteki:

1. Uwzględnij wszystkie zestawy zlokalizowanych zasobów w jednym pakiecie.
1. Utwórz oddzielne satelity zlokalizowane pakiety, wykonując obowiązek ścisłego przestrzegania Konwencji.

Obie metody ma swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Zestawy zlokalizowanych zasobów w jednym pakiecie

W tym zestawy zlokalizowanych zasobów w jednym pakiecie jest zwykle najprostsza metoda. W tym celu należy utworzyć foldery zawarte w `lib` obsługiwane języka innego niż domyślny pakiet (założono, że to en-us). W tych folderach można umieścić zestawy zasobów i zlokalizowanych plików IntelliSense XML.

Na przykład następujące struktury folderów obsługuje, niemiecki (de), włoski (go), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Widać, że języki są wszystkie wymienione poniżej `net40` folderu docelowego framework. Jeśli jesteś [obsługujący wiele platform](../create-packages/supporting-multiple-target-frameworks.md), następnie folder w węźle `lib` każdego wariantu.

Z tych folderów w miejscu, następnie odwołać wszystkie pliki w Twojej `.nuspec`:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Jeden pakiet przykładzie, który korzysta z tej metody jest [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Zalety i wady (zestawy zlokalizowanych zasobów)

Tworzenie pakietów wszystkie języki w jednym pakiecie ma kilka wady:

1. **Udostępnione metadanych**: ponieważ pakietu NuGet może zawierać tylko jeden `.nuspec` plików, można zapewnić metadane tylko jeden język. Oznacza to, że NuGet nie stanowi obsługuje zlokalizowanych metadanych.
1. **Rozmiar pakietu**: w zależności od liczby obsługiwanych języków, biblioteki może stać się znacznie duży, który spowalnia Instalowanie i przywracanie pakietu.
1. **Zwalnia równoczesne**: tworzenie pakietów zlokalizowane pliki w jednym pakiecie wymaga wersji wszystkie zasoby w tym pakiecie jednocześnie, zamiast możliwość oddzielnie wersji każdej lokalizacji. Ponadto żadnych aktualizacji do dowolnej lokalizacji co wymaga nowej wersji cały pakiet.

Jednak także ma kilka korzyści:

1. **Prostota**: konsumentów pakietu pobrać wszystkich obsługiwanych języków w jednej instalacji, zamiast instalować oddzielnie każdego języka. Pojedynczy pakiet jest również łatwiej znaleźć na nuget.org.
1. **Sprzężona wersji**: ponieważ wszystkie zestawy zasobów znajdują się w tym samym pakiecie jako podstawowy zestaw, wszystkie mają ten sam numer wersji i nie uruchamiaj ryzyko błędnego pobierania całkowicie niezależna.

## <a name="localized-satellite-packages"></a>Pakiety satelity zlokalizowanych

Podobnie jak środowisko .NET Framework obsługuje zestawy satelickie, ta metoda oddziela zlokalizowanych zasobów i plików IntelliSense XML w pakiety satelity.

To robić, podstawowy pakiet używa konwencji nazewnictwa `{identifier}.{version}.nupkg` i zawiera zestaw dla języka domyślnego (na przykład "en US). Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierał następującą strukturę:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Następnie zestaw satelicki używa konwencji nazewnictwa `{identifier}.{language}.{version}.nupkg`, takich jak `ContosoUtilities.de.1.0.0.nupkg`. Identyfikator **musi** dokładnie odpowiadać podstawowego pakietu.

Ponieważ to oddzielny pakiet ma własną `.nuspec` pliku, który zawiera zlokalizowane metadanych. Zachować ostrożność, który język w `.nuspec` **musi** zgodne z działaniem używanym w nazwie pliku.

Zestawu satelickiego **musi** deklarować dokładnej wersji głównej pakietu także jako zależności, przy użyciu notacji wersji [] \(zobacz [wersji pakietu](../reference/package-versioning.md)). Na przykład `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować zależność `ContosoUtilities.1.0.0.nupkg` przy użyciu `[1.0.0]` notacji. Oczywiście pakietu satelity ma numer wersji innego niż podstawowy pakiet.

Struktura pakietu satelity następnie muszą zawierać zestaw zasobów i plik XML IntelliSense w w podfolderze odpowiadający `{language}` w nazwie pliku pakietu:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Uwaga**: chyba że określone podhodowli, takich jak `ja-JP` są niezbędne, zawsze używaj wyższy identyfikator języka poziomu, tak samo, jak `ja`.

W zestawie satelickim rozpozna NuGet **tylko** tych plików w folderze, który odpowiada `{language}` w nazwie pliku. Wszystkie pozostałe są ignorowane.

Gdy są spełnione wszystkie następujące konwencje NuGet rozpozna pakietu jako pakiet satelity i instalowanie zlokalizowanych plików w pakiecie głównej `lib` folderu, tak jakby były one pierwotnie powiązane. Odinstalowywanie pakietu satelity spowoduje usunięcie jej pliki z tego samego folderu.

Należy utworzyć dodatkowe zestawy satelickie w taki sam sposób dla każdego obsługiwanego języka. Na przykład sprawdź zestaw pakietów platformy ASP.NET MVC:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowy w języku angielskim)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (wersja niemiecka)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))

### <a name="summary-of-required-conventions"></a>Podsumowanie konwencje wymagane

- Pakiet podstawowy musi mieć nazwę. `{identifier}.{version}.nupkg`
- Pakiet satelity musi mieć nazwę. `{identifier}.{language}.{version}.nupkg`
- Pakiet satelity `.nuspec` musi określać języka aby dopasować nazwę pliku.
- Pakiet satelity należy zadeklarować zależność dokładnej wersji głównej przy użyciu notacji [] w jego `.nuspec` pliku. Zakresy nie są obsługiwane.
- Pakiet satelity należy umieścić pliki w `lib\[{framework}\]{language}` folderu, która dokładnie odpowiada `{language}` w nazwie pliku.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Zalety i wady (satelity pakietów)

Używanie pakietów satelity ma kilka korzyści:

1. **Rozmiar pakietu**: jest zminimalizowany ogólną rozmiaru pakiet główny i konsumentów tylko ponoszenia kosztów każdego języka będą wykorzystywane.
1. **Oddzielne metadanych**: każdy pakiet satelity ma własną `.nuspec` pliku i w związku z tym zlokalizowanych metadanych ponieważ. Może to umożliwić niektórych konsumentów łatwiej znaleźć pakietów, wyszukując nuget.org z warunkami zlokalizowane.
1. **Całkowicie niezależna wersjach**: zestawy satelickie może być zwolnione wraz z upływem czasu, a nie w całości, umożliwiając rozłożenia wysiłków lokalizacji.

Jednak pakiety satelity mieć własny zestaw wady:

1. **Bałaganu**: zamiast pojedynczy pakiet ma wiele pakietów, które mogą prowadzić do dużej liczby wyników nuget.org i długą listę odwołań w projekcie programu Visual Studio.
1. **Konwencje Strict**. Pakiety satelity musi dokładnie zgodne z konwencjami lub zlokalizowane wersje nie zostać pobrana prawidłowo.
1. **Przechowywanie wersji**: każdy pakiet satelity musi mieć zależność dokładnej wersji głównej pakietu. Oznacza to, że aktualizacji pakietu głównej mogą wymagać aktualizacji wszystkich pakietów satelity również nawet wtedy, gdy nie zmienił się zasoby.
