---
title: Limity, NuGet interfejsu API szybkości
description: Interfejsy API NuGet będzie wymusić limity szybkości, aby uniemożliwić nadużycia.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a>Limity szybkości

Interfejs API NuGet.org wymusza, aby uniemożliwić nadużycia limitów szybkości. Żądania, które przekraczają limit szybkości zwrócił następujący błąd: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

W poniższej tabeli wymieniono limity szybkości dla interfejsu API NuGet.org.

## <a name="package-search"></a>Wyszukaj pakiet

> [!Note]
> Firma Microsoft zaleca używanie NuGet.org [interfejsów API w wersji 3](https://docs.microsoft.com/nuget/api/search-query-service-resource) wyszukiwania, wydajności i nie ma żadnych obecnie ograniczenia. V1 i V2 wyszukiwania interfejsów API, followins ograniczenia:


| interfejs API | Typ limitu | Wartość limitu | Przypadków użycia interfejsu API |
|:---|:---|:---|:---|
**POBIERZ** `/api/v1/Packages` | IP | 1000 na minutę | Zapytanie metadanych pakietu NuGet za pośrednictwem v1 OData `Packages` kolekcji |
**POBIERZ** `/api/v1/Search()` | IP | 3000 na minutę | Wyszukaj pakietów NuGet za pośrednictwem punktu końcowego wyszukiwania v1 | 
**POBIERZ** `/api/v2/Packages` | IP | 20000 na minutę | Zapytanie metadanych pakietu NuGet za pośrednictwem v2 OData `Packages` kolekcji | 
**POBIERZ** `/api/v2/Packages/$count` | IP | 100 na minutę | Zapytanie liczby pakietów NuGet za pośrednictwem v2 OData `Packages` kolekcji | 

## <a name="package-push-and-unlist"></a>Pakiet wypychania i Unlist

| interfejs API | Typ limitu | Wartość limitu | Przypadków użycia interfejsu API | 
|:---|:---|:---|:--- |
**UMIEŚĆ** `/api/v2/package` | Klucz interfejsu API | 100 na minutę | Przekaż nowy pakiet NuGet (wersja) za pośrednictwem punktu końcowego wypychania v2 
**USUŃ** `/api/v2/package/{id}/{version}` | Klucz interfejsu API | 100 na minutę | Unlist pakietu NuGet (wersja) za pośrednictwem punktu końcowego v2 