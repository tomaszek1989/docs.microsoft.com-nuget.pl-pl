---
title: Rozwiązywanie sporów nazwa pakietu NuGet
description: Proces rozwiązywanie sporów między związane z znakowania, znaków towarowych i innych konfliktów wydawcy pakietu NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: f7749dec0726162f122db91397e9581cfad23890
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817548"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Rozwiązywanie sporów nazwy pakietu NuGet

W tym artykule przedstawiono proces zalecane rozwiązanie członkom społeczności, rozwiązywanie sporów z innych wydawców NuGet.

Na przykład załóżmy, że Northwind Traders sprawia, że systemu CRM, dla którego zapewniają sterowników klienta jako MSI do pobrania z witryny sieci Web. Irena, niezależnie od dewelopera wymaga ułatwić korzystanie z biblioteki klienta firmy Northwind i konwertuje go na pakietu NuGet o nazwie `NorthwindTraders.Client`. Później Northwind chce utworzyć oficjalnego pakietu NuGet w swoich własnych ich biblioteki klienta i w związku z tym chcesz rozstrzygania własność firmy Irena nazwę pakietu.

W tym scenariuszu Irena nie wydaje się być działające z zamiarów zły, ale raczej obsługuje narzędzia i klientów firmy Northwind, podając własne czasu i kod. W tym samym czasie Northwind jest uzasadnione właścicielem nazwy Northwind.

Wykonując z procesem opisanym niżej Northwind i Irena mogą współdziałać ze sobą odpowiedniego rozwiązania, ponieważ zarówno zainteresowani obsługująca społeczności deweloperów. Zwykle nie jest niezbędna dla zespołu NuGet do angażowania; Współpraca zwykle działa się najlepiej. W rzeczywistości co sporów zespołu NuGet uwagi do daty została działał bez zespołu konieczności przekazać ocenie.

## <a name="process"></a>Proces

1. Skontaktuj się z właściciele pakietu masz sporów przy użyciu **właścicieli skontaktuj się z** łącze na stronie Szczegóły pakietu. Opis problemu w rodzaju i w sposób bezpośredni.
2. Wyślij kopię wiadomości [ support@nuget.org ](mailto:support@nuget.org) tak, aby NuGet i .NET Foundation wiedzą z sporów.
3. Poczekaj maksymalnie 30 dni rozwiązanie problemu, a następnie powiadom [ support@nuget.org ](mailto:support@nuget.org) ponownie. Nuget.org zespołem pomocy technicznej będzie angażowanie i spróbuj pracy za pośrednictwem sporów z obu stron.
