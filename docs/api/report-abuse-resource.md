---
title: Szablon raportu do adresu URL nadużyć, NuGet interfejsu API
description: Szablon adresu URL nadużycia raport umożliwia klientom do wyświetlenia łącza nadużycia raportu w jego interfejsie użytkownika.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818470"
---
# <a name="report-abuse-url-template"></a>Szablon adresu URL nadużycia raportu

Istnieje możliwość dla klienta do tworzenia adresów URL, które mogą być używane przez użytkownika do zgłaszania nadużyć o określonym pakiecie. Jest to przydatne, gdy źródło pakietu chce włączyć wszystkie delegować nadużycia raporty do źródła pakietu klienta środowiska (strona nawet 3).

Zasób używany do pobierania zawartości pakietu jest `ReportAbuseUriTemplate` można znaleźć zasobu w [indeksu usługi](service-index.md).

## <a name="versioning"></a>Przechowywanie wersji

Następujące `@type` są używane wartości:

@type Wartość                       | Uwagi
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | Początkowa wersja
ReportAbuseUriTemplate/3.0.0-rc   | Alias `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Szablon adresu URL

Adres URL następujący interfejs API jest wartość `@id` właściwości skojarzone z jedną z wyżej wymienionych zasobów `@type` wartości.

## <a name="http-methods"></a>Metody HTTP

Mimo że klient nie jest przeznaczony na wysyłanie żądań do adresu URL programu report nadużyć w imieniu użytkownika, strony sieci web powinna obsługiwać `GET` metodę umożliwiającą klikniętej adres URL, który można łatwo otworzyć w przeglądarce sieci web.

## <a name="construct-the-url"></a>Utworzyć adres URL

Podany identyfikator znanego pakietu i wersję, implementacja klienta można konstruować adresu URL, które umożliwiają dostęp do interfejsu sieci web. Implementacja klienta powinien być wyświetlany tego utworzony adres URL (lub łączem) użytkownika, dzięki czemu Otwórz przeglądarkę sieci web do adresu URL i żadnych raportów na potrzeby nadużycia. Implementacja formularz raportu nadużycia zależy od implementacji serwera.

Wartość `@id` jest zawierające dowolny z następujących znaczników symbol zastępczy ciągu adresu URL:

### <a name="url-placeholders"></a>Symbole zastępcze adresu URL

Nazwa        | Typ    | Wymagane | Uwagi
----------- | ------- | -------- | -----
`{id}`      | string  | Brak       | Identyfikator pakietu do zgłaszania nadużyć dla
`{version}` | string  | Brak       | Wersja pakietu do zgłaszania nadużyć dla

`{id}` i `{version}` wartości interpretowane przez implementację serwera musi być bez uwzględniania wielkości liter i nie poufne czy normalizowane jest wersja.

Na przykład szablon nadużycia raportu nuget.org wygląda następująco:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Jeśli implementacja klienta wymaga do wyświetlenia łącza do formularza nadużycia raport NuGet.Versioning 4.3.0, czy to utworzyć następujący adres URL i przekazywanie ich do użytkownika:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
