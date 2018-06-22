---
title: Informacje o wersji 1.8 NuGet
description: Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 1.8 NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1801d62b786717c088429fbeca6f1f72f5ab6b4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820108"
---
# <a name="nuget-18-release-notes"></a><span data-ttu-id="10932-103">Informacje o wersji 1.8 NuGet</span><span class="sxs-lookup"><span data-stu-id="10932-103">NuGet 1.8 Release Notes</span></span>

<span data-ttu-id="10932-104">[Informacje o wersji NuGet 1.7](../release-notes/nuget-1.7.md) | [NuGet 2.0 informacje o wersji](../release-notes/nuget-2.0.md)</span><span class="sxs-lookup"><span data-stu-id="10932-104">[NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md) | [NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md)</span></span>

<span data-ttu-id="10932-105">NuGet 1.8 został wydany 23 maj 2012.</span><span class="sxs-lookup"><span data-stu-id="10932-105">NuGet 1.8 was released on May 23, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="10932-106">Znane problem</span><span class="sxs-lookup"><span data-stu-id="10932-106">Known Installation Issue</span></span>
<span data-ttu-id="10932-107">Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="10932-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="10932-108">Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.</span><span class="sxs-lookup"><span data-stu-id="10932-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="10932-109">Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki VS](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="10932-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="10932-110">Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".</span><span class="sxs-lookup"><span data-stu-id="10932-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a><span data-ttu-id="10932-111">NuGet 1.8 niezgodne z systemem Windows XP, poprawki opublikowane</span><span class="sxs-lookup"><span data-stu-id="10932-111">NuGet 1.8 Incompatible with Windows XP, hotfix published</span></span>

<span data-ttu-id="10932-112">Wkrótce po NuGet 1.8 został zwolniony, dowiedzieliśmy się, że zmiana kryptografii 1.8 spowodowało przerwanie użytkowników w systemie Windows XP.</span><span class="sxs-lookup"><span data-stu-id="10932-112">Shortly after NuGet 1.8 was released, we learned that a cryptography change in 1.8 broke users on Windows XP.</span></span>

<span data-ttu-id="10932-113">Ponieważ firma Microsoft wydała poprawkę rozwiązującą ten problem.</span><span class="sxs-lookup"><span data-stu-id="10932-113">We have since released a hotfix that addresses this issue.</span></span>  <span data-ttu-id="10932-114">Aktualizacja NuGet za pośrednictwem galerii rozszerzeń programu Visual Studio, pojawi się tej poprawki.</span><span class="sxs-lookup"><span data-stu-id="10932-114">By updating NuGet through the Visual Studio Extension Gallery, you receive this hotfix.</span></span>

## <a name="features"></a><span data-ttu-id="10932-115">Funkcje</span><span class="sxs-lookup"><span data-stu-id="10932-115">Features</span></span>

### <a name="satellite-packages-for-localized-resources"></a><span data-ttu-id="10932-116">Pakiety satelity dla zlokalizowanych zasobów</span><span class="sxs-lookup"><span data-stu-id="10932-116">Satellite Packages for Localized Resources</span></span>
<span data-ttu-id="10932-117">NuGet 1.8 obsługuje teraz możliwość tworzenia oddzielne pakiety zlokalizowane zasoby, podobnie do funkcji satelickie zestawu programu .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="10932-117">NuGet 1.8 now supports the ability to create separate packages for localized resources, similar to the satellite assembly capabilities of the .NET Framework.</span></span>  <span data-ttu-id="10932-118">Pakiet satelity jest tworzony w taki sam sposób jak inny pakiet NuGet dodając kilka Konwencji:</span><span class="sxs-lookup"><span data-stu-id="10932-118">A satellite package is created in the same way as any other NuGet package with the addition of a few conventions:</span></span>

* <span data-ttu-id="10932-119">Satelita pakietu identyfikator i nazwa pliku powinna zawierać sufiks, który pasuje do jednej ze standardowych [kultury ciągów używanych przez program .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span><span class="sxs-lookup"><span data-stu-id="10932-119">The satellite package ID and file name should include a suffix that matches one of the standard [culture strings used by the .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).</span></span>
* <span data-ttu-id="10932-120">W jego `.nuspec` pliku pakietu satelity należy zdefiniować element języka z tej samej ciąg kultury używany w Identyfikatorach</span><span class="sxs-lookup"><span data-stu-id="10932-120">In its `.nuspec` file, the satellite package should define a language element with the same culture string used in the ID</span></span>
* <span data-ttu-id="10932-121">Pakiet satelity należy zdefiniować zależności w jego `.nuspec` pliku do jego pakietu core, to po prostu pakiet o tym samym identyfikatorze minus sufiks języka.</span><span class="sxs-lookup"><span data-stu-id="10932-121">The satellite package should define a dependency in its `.nuspec` file to its core package, which is simply the package with the same ID minus the language suffix.</span></span>  <span data-ttu-id="10932-122">Pakiet podstawowy musi być dostępny w repozytorium dla pomyślnej instalacji.</span><span class="sxs-lookup"><span data-stu-id="10932-122">The core package needs to be available in the repository for successful installation.</span></span>

<span data-ttu-id="10932-123">Aby zainstalować pakiet z zlokalizowanych zasobów, deweloper jawnie wybiera zlokalizowanego pakietu z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="10932-123">To install a package with localized resources, a developer explicitly selects the localized package from the repository.</span></span> <span data-ttu-id="10932-124">Obecnie galerii NuGet nie daje dowolnego rodzaju szczególnego traktowania do pakietów satelity.</span><span class="sxs-lookup"><span data-stu-id="10932-124">At present, the NuGet gallery does not give any kind of special treatment to satellite packages.</span></span>

![Okno dialogowe Menedżera pakietów z pacakges zlokalizowanych](./media/dlg-w-loc-packs.png)

<span data-ttu-id="10932-126">Ponieważ pakietu satelity zawiera listę zależności do pakietu core, zarówno satelity i podstawowe pakiety są pobierane do folderu pakietów NuGet i zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="10932-126">Because the satellite package lists a dependency to its core package, both the satellite and core packages are pulled into the NuGet packages folder and installed.</span></span>

![Folder pakiety z pakietami zlokalizowanych](./media/fldr-loc-packs.png)

<span data-ttu-id="10932-128">Ponadto podczas instalowania pakietu satelity, NuGet również rozpoznaje konwencji nazewnictwa ciąg kultury i następnie kopiuje zestawu zlokalizowanych zasobów do poprawne podfolderu w pakiecie core, dzięki czemu mogą być pobierane przez program .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="10932-128">Additionally, while installing the satellite package, NuGet also recognizes the culture string naming convention and then copies the localized resource assembly into the correct subfolder within the core package so that it can be picked by the .NET Framework.</span></span>

![Podstawowe folderu pakietu z folderu skopiowanego zasobu](./media/fldr-copied-loc.png)

<span data-ttu-id="10932-130">Jedną istniejącą usterkę zauważyć z pakietami satelity jest NuGet nie kopiuje zlokalizowanych zasobów do `bin` folderu dla projektów witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="10932-130">One existing bug to note with satellite packages is that NuGet does not copy localized resources to the `bin` folder for Web site projects.</span></span>  <span data-ttu-id="10932-131">Ten problem zostanie rozwiązany w następnej wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="10932-131">This issue will be fixed in the next release of NuGet.</span></span>

<span data-ttu-id="10932-132">Dla kompletnego przykładu pokazuje sposób tworzenia i używania pakietów satelity, zobacz [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).</span><span class="sxs-lookup"><span data-stu-id="10932-132">For a complete sample demonstrating how to create and use satellite packages, see [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).</span></span>

### <a name="package-restore-consent"></a><span data-ttu-id="10932-133">Zgody przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="10932-133">Package Restore Consent</span></span>
<span data-ttu-id="10932-134">W 1.8 NuGet możemy ustanowić przygotowuje obsługi ważne ograniczenia na Przywracanie pakietu, aby chronić prywatność użytkowników.</span><span class="sxs-lookup"><span data-stu-id="10932-134">In NuGet 1.8, we laid the groundwork for supporting an important constraint on package restore to protect user privacy.</span></span> <span data-ttu-id="10932-135">To ograniczenie wymaga deweloperom tworzenie projektów i rozwiązań, które używają Przywracanie pakietu do jawnie wyrażenia zgody na przywracanie pakietów na przechodzenie do trybu online, aby pobrać pakiety ze źródeł pakietów skonfigurowanych.</span><span class="sxs-lookup"><span data-stu-id="10932-135">This constraint requires developers building projects and solutions that are using package restore to explicitly consent to package restore’s going online to download packages from configured package sources.</span></span>

<span data-ttu-id="10932-136">Istnieją 2 sposoby zapewnienia tej zgody.</span><span class="sxs-lookup"><span data-stu-id="10932-136">There are 2 ways to provide this consent.</span></span> <span data-ttu-id="10932-137">Pierwszy znajdują się w pakiet Menedżera okna dialogowego konfiguracji jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="10932-137">The first can be found in the package manager configuration dialog as shown below.</span></span>  <span data-ttu-id="10932-138">Ta metoda jest przeznaczone głównie dla deweloperów maszyn.</span><span class="sxs-lookup"><span data-stu-id="10932-138">This method is primarily intended for developer machines.</span></span>

![Okno dialogowe konfiguracji Menedżera pakietów](./media/pr-consent-configdlg.png)

<span data-ttu-id="10932-140">Druga metoda jest ustawiona środowiska zmiennej "EnableNuGetPackageRestore" na wartość "true".</span><span class="sxs-lookup"><span data-stu-id="10932-140">The second method is to set the environment variable “EnableNuGetPackageRestore” to the value “true”.</span></span>  <span data-ttu-id="10932-141">Ta metoda jest przeznaczona dla instalacji nienadzorowanej maszyny, takich jak serwery CI lub kompilacji.</span><span class="sxs-lookup"><span data-stu-id="10932-141">This method is intended for unattended machines such as CI or build servers.</span></span>

<span data-ttu-id="10932-142">Teraz jak już wspomniano, firma Microsoft ma tylko określone przygotowuje tej funkcji w NuGet 1.8.</span><span class="sxs-lookup"><span data-stu-id="10932-142">Now, as stated above, we have only laid the groundwork for this feature in NuGet 1.8.</span></span>  <span data-ttu-id="10932-143">W praktyce oznacza to, że podczas dodaliśmy wszystkie logiki, aby włączyć funkcję jest obecnie wymuszone w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="10932-143">Practically, this means that while we’ve added all of the logic to enable the feature, it's not currently enforced in this version.</span></span> <span data-ttu-id="10932-144">Zostanie włączona, jednak w następnej wersji programu NuGet, więc możemy się go jak najszybciej, aby odpowiednio skonfigurować środowiska i w związku z tym nie występować po Rozpoczniemy wymuszenia ograniczenia zgody.</span><span class="sxs-lookup"><span data-stu-id="10932-144">It will be enabled, however, in the next release of NuGet, so we wanted to make you aware of it as soon as possible so that you can configure your environments appropriately and therefore not be impacted when we start enforce the consent constraint.</span></span>

<span data-ttu-id="10932-145">Aby uzyskać więcej informacji, zobacz [wpis w blogu zespołu](http://blog.nuget.org/20120518/package-restore-and-consent.html) tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="10932-145">For more details, please see the [team blog post](http://blog.nuget.org/20120518/package-restore-and-consent.html) on this feature.</span></span>

### <a name="nugetexe-performance-improvements"></a><span data-ttu-id="10932-146">Ulepszenia wydajności nuget.exe</span><span class="sxs-lookup"><span data-stu-id="10932-146">nuget.exe Performance Improvements</span></span>
<span data-ttu-id="10932-147">Zmieniając polecenia instalacji, aby pobrać i zainstalować pakiety równolegle NuGet 1.8 wprowadzono znacznej poprawy wydajności nuget.exe — i przez Przywracanie pakietu rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="10932-147">By modifying the install command to download and install packages in parallel, NuGet 1.8 brings dramatic performance improvements to nuget.exe – and by extension package restore.</span></span>  <span data-ttu-id="10932-148">Wysokiego poziomu testowania pokazuje, że wydajność w przypadku instalowania pakietów 6 w projekcie zwiększa się o około 35% w NuGet 1.8.</span><span class="sxs-lookup"><span data-stu-id="10932-148">High level testing shows that performance for installing 6 packages into a project improves by about 35% in NuGet 1.8.</span></span>  <span data-ttu-id="10932-149">Zwiększenie liczby pakietów do 25 zawiera bardziej wydajne około 60%.</span><span class="sxs-lookup"><span data-stu-id="10932-149">Increasing the number of packages to 25 shows a performance gain of about 60%.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="10932-150">Poprawki błędów</span><span class="sxs-lookup"><span data-stu-id="10932-150">Bug Fixes</span></span>
<span data-ttu-id="10932-151">NuGet 1.8 zawiera kilka poprawek, ze szczególnym uwzględnieniem konsoli Menedżera pakietów i przepływ pracy przywracania pakietu, szczególnie, co wiąże się zgody przywracania pakietu i integracja z systemem Windows 8 Express.</span><span class="sxs-lookup"><span data-stu-id="10932-151">NuGet 1.8 includes quite a few bug fixes with an emphasis on the package manager console and package restore workflow, particularly as it relates to package restore consent and Windows 8 Express integration.</span></span>
<span data-ttu-id="10932-152">Pełną listę prac elementów usunięto w wersji NuGet 1.8, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="10932-152">For a full list of work items fixed in NuGet 1.8, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>