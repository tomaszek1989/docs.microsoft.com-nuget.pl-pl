---
title: "Sposoby można zainstalować pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "W tym artykule opisano proces instalowania pakietów NuGet do projektu, w tym, co się dzieje na dysku oraz pliki dotyczy projektu."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a><span data-ttu-id="fb08f-104">Różne sposoby, można zainstalować pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="fb08f-104">Different ways to install a NuGet Package</span></span>

<span data-ttu-id="fb08f-105">Pakiety NuGet zostaną pobrane i zainstalowane przy użyciu dowolnej z następujących metod (zobacz [NuGet zainstalować narzędzia klienta](../install-nuget-client-tools.md) Jeśli nie są już zainstalowane):</span><span class="sxs-lookup"><span data-stu-id="fb08f-105">NuGet packages are downloaded and installed using any of the following methods (see [Install NuGet client tools](../install-nuget-client-tools.md) if you don't have these installed already):</span></span>

| <span data-ttu-id="fb08f-106">Metoda</span><span class="sxs-lookup"><span data-stu-id="fb08f-106">Method</span></span> | <span data-ttu-id="fb08f-107">Opis</span><span class="sxs-lookup"><span data-stu-id="fb08f-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fb08f-108">DotNet.exe interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fb08f-108">dotnet.exe CLI</span></span><br/>`dotnet install <package_name>` | <span data-ttu-id="fb08f-109">(Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\>rozszerza jego zawartość do folderu w bieżącym katalogu i dodaje odwołanie do pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fb08f-109">(All platforms) Downloads the package identified by \<package_name\>, expands its contents into a folder in the current directory, and adds a reference to the project file.</span></span> <span data-ttu-id="fb08f-110">Również pobiera i instaluje zależności.</span><span class="sxs-lookup"><span data-stu-id="fb08f-110">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="fb08f-111">Instalowanie i używanie pakietu (wiersz polecenia dotnet)</span><span class="sxs-lookup"><span data-stu-id="fb08f-111">Install and use a package (dotnet CLI)</span></span>](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[<span data-ttu-id="fb08f-112">Polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="fb08f-112">dotnet commands</span></span>](../tools/dotnet-commands.md)</li></ul> |
| <span data-ttu-id="fb08f-113">Interfejs użytkownika Menedżera pakietów (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fb08f-113">Package Manager UI (Visual Studio)</span></span> | <span data-ttu-id="fb08f-114">(System Windows i Mac) Udostępnia interfejs, za pomocą którego można wybrać, wybierz i zainstaluj pakietów oraz ich zależności w projekcie.</span><span class="sxs-lookup"><span data-stu-id="fb08f-114">(Windows and Mac) Provides a UI through which you can browse, select, and install packages and their dependencies into a project.</span></span> <span data-ttu-id="fb08f-115">Dodaje odwołania do zainstalowanych pakietów do pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fb08f-115">Adds references to installed packages to the project file.</span></span><ul><li>[<span data-ttu-id="fb08f-116">Instalowanie i używanie pakietu (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fb08f-116">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="fb08f-117">Informacje o interfejsie użytkownika Menedżera pakietów (system Windows)</span><span class="sxs-lookup"><span data-stu-id="fb08f-117">Package Manager UI reference (Windows)</span></span>](../tools/package-manager-ui.md)</li><li>[<span data-ttu-id="fb08f-118">W tym pakietu NuGet w projekcie (Mac)</span><span class="sxs-lookup"><span data-stu-id="fb08f-118">Including a NuGet package in your project (Mac)</span></span>](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| <span data-ttu-id="fb08f-119">Konsola Menedżera pakietów (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fb08f-119">Package Manager Console (Visual Studio)</span></span><br/>`Install-Package <package_name>` | <span data-ttu-id="fb08f-120">(Tylko system Windows) Pobiera i instaluje pakiet identyfikowane przez \<nazwa_pakietu\> do określonego projektu w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="fb08f-120">(Windows only) Downloads and installs the package identified by \<package_name\> into a specified project in the solution, then adds a reference to the project file.</span></span> <span data-ttu-id="fb08f-121">Również pobiera i instaluje zależności.</span><span class="sxs-lookup"><span data-stu-id="fb08f-121">Also downloads and installs dependencies.</span></span><ul><li>[<span data-ttu-id="fb08f-122">Instalowanie i używanie pakietu (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fb08f-122">Install and use a package (Visual Studio)</span></span>](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[<span data-ttu-id="fb08f-123">Przewodnik Konsola Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="fb08f-123">Package Manager Console guide</span></span>](../tools/package-manager-console.md)</li></ul> |
| <span data-ttu-id="fb08f-124">nuget.exe interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="fb08f-124">nuget.exe CLI</span></span><br/>`nuget install <package_name>` | <span data-ttu-id="fb08f-125">(Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i rozwija jego zawartość do folderu w bieżącym katalogu; można również pobrać wszystkie pakiety wymienione w `packages.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="fb08f-125">(All platforms) Downloads the package identified by \<package_name\> and expands its contents into a folder in the current directory; can also download all packages listed in a `packages.config` file.</span></span> <span data-ttu-id="fb08f-126">Również pobiera i instaluje zależności, ale nie zmienia plików projektu.</span><span class="sxs-lookup"><span data-stu-id="fb08f-126">Also downloads and installs dependencies, but makes no changes to project files.</span></span><ul><li>[<span data-ttu-id="fb08f-127">polecenie instalacji</span><span class="sxs-lookup"><span data-stu-id="fb08f-127">install command</span></span>](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a><span data-ttu-id="fb08f-128">Proces instalacji ogólne</span><span class="sxs-lookup"><span data-stu-id="fb08f-128">General install process</span></span>

<span data-ttu-id="fb08f-129">Ogólnie rzecz biorąc NuGet wykonuje następujące pytanie, aby zainstalować pakiet:</span><span class="sxs-lookup"><span data-stu-id="fb08f-129">In general, NuGet does the following then asked to install a package:</span></span>

1. <span data-ttu-id="fb08f-130">Pobieranie pakietu:</span><span class="sxs-lookup"><span data-stu-id="fb08f-130">Acquire the package:</span></span>
    - <span data-ttu-id="fb08f-131">Sprawdź, czy żądany pakiet już istnieje w pamięci podręcznej (zobacz [Zarządzanie pamięci podręcznej NuGet](managing-the-nuget-cache.md)).</span><span class="sxs-lookup"><span data-stu-id="fb08f-131">Check if the requested package already exists in a cache (see [Managing the NuGet cache](managing-the-nuget-cache.md)).</span></span>
    - <span data-ttu-id="fb08f-132">Jeśli pakiet nie jest w pamięci podręcznej, próby pobrania pakietu ze źródeł na liście [pliki konfiguracji](Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fb08f-132">If the package is not in the cache, attempt to download the package from the sources listed in the [configuration files](Configuring-NuGet-Behavior.md).</span></span>
      - <span data-ttu-id="fb08f-133">Dla projektów przy użyciu `packages.config` format odwołania, NuGet wykorzystuje kolejność źródeł w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fb08f-133">For projects using the `packages.config` reference format, NuGet uses the order of the sources in the configuration.</span></span>
      - <span data-ttu-id="fb08f-134">W przypadku projektów przy użyciu formatu PackageReference NuGet kontroli źródła, które są najpierw folderów lokalnych kontroli źródła w udziałach sieciowych, a następnie sprawdza źródła HTTP (Internet).</span><span class="sxs-lookup"><span data-stu-id="fb08f-134">For projects using the PackageReference format, NuGet checks sources that are local folders first, then checks sources on network shares, then checks HTTP (Internet) sources.</span></span>
      - <span data-ttu-id="fb08f-135">Ogólnie rzecz biorąc kolejność, w którym NuGet kontroli źródła nie jest szczególnie przydatne, ponieważ wszystkie danego pakietu o określoną liczbę identyfikator i wersja jest dokładnie taka sama niezależnie od źródła został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="fb08f-135">In general, the order in which NuGet checks sources isn't particularly meaningful, because any given package with a specific identifier and version number is exactly the same on whatever source it's found.</span></span>
    - <span data-ttu-id="fb08f-136">Jeśli pakiet jest pomyślnie uzyskano z jednego ze źródeł, NuGet dodaje go do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="fb08f-136">If the package is successfully acquired from one of the sources, NuGet adds it to the cache.</span></span> <span data-ttu-id="fb08f-137">W przeciwnym razie instalacja nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="fb08f-137">Otherwise, installation fails.</span></span>

1. <span data-ttu-id="fb08f-138">Rozwiń pakiet w projekcie.</span><span class="sxs-lookup"><span data-stu-id="fb08f-138">Expand the package into the project.</span></span>
    - <span data-ttu-id="fb08f-139">Rozszerzanie oznacza rozpakować zawartość pakietu do odpowiedniego podfolderu.</span><span class="sxs-lookup"><span data-stu-id="fb08f-139">Expanding means unzipping the package's contents into an appropriate subfolder.</span></span> <span data-ttu-id="fb08f-140">Kopię `.nupkg` również znajduje się w podfolderze.</span><span class="sxs-lookup"><span data-stu-id="fb08f-140">A copy of the `.nupkg` itself is also placed in the subfolder.</span></span>
    - <span data-ttu-id="fb08f-141">Jeśli pakiet jest instalowany do projektu programu Visual Studio lub .NET Core, tylko te pliki, które są odpowiednie do platformy docelowej projektu zostaną rozwinięte.</span><span class="sxs-lookup"><span data-stu-id="fb08f-141">If the package is being installed into a Visual Studio or .NET Core project, only the files relevant to the project's target framework are expanded.</span></span> <span data-ttu-id="fb08f-142">Podczas instalacji przy użyciu wiersza polecenia nuget.exe zostaną rozwinięte wszystkie zestawy.</span><span class="sxs-lookup"><span data-stu-id="fb08f-142">When installed using the nuget.exe command line, all assemblies are expanded.</span></span>

1. <span data-ttu-id="fb08f-143">Jeśli pakiet jest zainstalowany w programie Visual Studio lub platformy dotnet interfejsu wiersza polecenia, odwołanie zostanie dodany do pliku odpowiedni projekt (lub `packages.config` dla niektórych typów projektów programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="fb08f-143">If the package is installed within Visual Studio or the dotnet CLI, a reference is added to the appropriate project file (or `packages.config` for some project types in Visual Studio).</span></span>

## <a name="related-topics"></a><span data-ttu-id="fb08f-144">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="fb08f-144">Related topics</span></span>

- [<span data-ttu-id="fb08f-145">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="fb08f-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="fb08f-146">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="fb08f-146">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="fb08f-147">Konfigurowanie zachowania pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="fb08f-147">Configuring NuGet behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
- [<span data-ttu-id="fb08f-148">Zarządzanie pamięcią podręczną pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="fb08f-148">Managing the NuGet cache</span></span>](managing-the-nuget-cache.md)