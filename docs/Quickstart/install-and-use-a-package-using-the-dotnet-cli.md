---
title: "Wprowadzenie do przewodnika za pomocą pakietów NuGet przez dotnet interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na proces instalowania i używania pakietu NuGet w projekcie platformy .NET Core."
keywords: "instalowania NuGet użycia pakietu NuGet, instalowanie pakietów NuGet, odwołania do pakietu NuGet, za pomocą pakietów NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 11b417644a46008f91fdcd5e0ba0a1fcf0bdc0e0
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="16554-104">Zainstalować i używać pakietu przy użyciu dotnet interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="16554-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="16554-105">Pakiety NuGet zawiera kod wielokrotnego użytku, który inni deweloperzy udostępnić użytkownikowi do użycia w projektach.</span><span class="sxs-lookup"><span data-stu-id="16554-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="16554-106">Zobacz [co to jest NuGet?](../What-is-NuGet.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="16554-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="16554-107">Pakiety są zainstalowane w projekcie platformy .NET Core za pomocą `dotnet add package` polecenia zgodnie z opisem w tym artykule popularnych [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) pakietu.</span><span class="sxs-lookup"><span data-stu-id="16554-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="16554-108">Po zakończeniu instalacji można znaleźć pakietu w kodzie z `using <namespace>` gdzie \<przestrzeni nazw\> jest przeznaczony dla pakietu używasz.</span><span class="sxs-lookup"><span data-stu-id="16554-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="16554-109">Po odniesienia, można wywołać pakietu za pośrednictwem jej interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16554-109">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="16554-110">**Rozpoczynać nuget.org**: nuget.org przeglądania jest jak .NET deweloperzy zazwyczaj znaleźć składników może zostać ponownie użyty we własnych aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="16554-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="16554-111">Można wyszukiwać nuget.org bezpośrednio lub znaleźć i zainstalować pakiety w programie Visual Studio, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="16554-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="16554-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16554-112">Pre-requisites</span></span>

- <span data-ttu-id="16554-113">[.NET Core SDK](https://www.microsoft.com/net/download/), która zapewnia `dotnet` narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="16554-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="16554-114">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="16554-114">Create a project</span></span>

<span data-ttu-id="16554-115">Można zainstalować pakietów NuGet w projekcie .NET określonego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="16554-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="16554-116">W ramach tego przewodnika Utwórz prosty projekt konsoli .NET Core w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="16554-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="16554-117">Utwórz folder dla projektu.</span><span class="sxs-lookup"><span data-stu-id="16554-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="16554-118">Utwórz projekt za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="16554-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="16554-119">Użyj `dotnet run` do przetestowania, czy aplikacja została utworzona poprawnie.</span><span class="sxs-lookup"><span data-stu-id="16554-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="16554-120">Dodaj pakiet Newtonsoft.Json NuGet</span><span class="sxs-lookup"><span data-stu-id="16554-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="16554-121">Użyj następującego polecenia, aby zainstalować `Newtonsoft.json` pakietu:</span><span class="sxs-lookup"><span data-stu-id="16554-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="16554-122">Po zakończeniu działania polecenia Otwórz `.csproj` plik, aby wyświetlić odwołania dodane:</span><span class="sxs-lookup"><span data-stu-id="16554-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="16554-123">Użyj Newtonsoft.Json interfejsu API w aplikacji</span><span class="sxs-lookup"><span data-stu-id="16554-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="16554-124">Otwórz `Program.cs` pliku i Dodaj następujący wiersz na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="16554-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="16554-125">Dodaj następujący kod przed `class Program` wiersza:</span><span class="sxs-lookup"><span data-stu-id="16554-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="16554-126">Zastąp `Main` funkcji z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="16554-126">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="16554-127">Tworzenie i uruchamianie aplikacji przy użyciu `dotnet run` polecenia.</span><span class="sxs-lookup"><span data-stu-id="16554-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="16554-128">Dane wyjściowe powinny mieć reprezentacja JSON `Account` obiektu w kodzie:</span><span class="sxs-lookup"><span data-stu-id="16554-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="16554-129">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="16554-129">Related articles</span></span>

- [<span data-ttu-id="16554-130">Omówienie i przepływ pracy zużycia pakietu</span><span class="sxs-lookup"><span data-stu-id="16554-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="16554-131">Znajdowanie i wybieranie pakietów</span><span class="sxs-lookup"><span data-stu-id="16554-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="16554-132">Sposoby instalacji pakietu</span><span class="sxs-lookup"><span data-stu-id="16554-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="16554-133">Konfigurowanie zachowania programu NuGet</span><span class="sxs-lookup"><span data-stu-id="16554-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)