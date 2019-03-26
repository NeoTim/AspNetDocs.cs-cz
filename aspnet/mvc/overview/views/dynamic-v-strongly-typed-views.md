---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dynamické zobrazení vs. Zobrazení se silnými typy | Dokumentace Microsoftu
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: bde40f609db25f590108bfc2396071c0033a1326
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/25/2019
ms.locfileid: "58423335"
---
<a name="dynamic-v-strongly-typed-views"></a>Dynamické zobrazení vs. zobrazení se silnými typy
====================
Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))

Existují tři způsoby, jak předat informace z řadiče zobrazení v architektuře ASP.NET MVC 3:

1. Jako model silného typu objektu.
2. Jako dynamický typ (pomocí @model dynamické)
3. Pomocí objekt ViewBag

Můžu jste napsali jednoduchou aplikaci MVC 3 horní blogu můžete porovnat a kontrast zobrazení dynamických webů a silného typu. Kontroler začíná jednoduchým seznamem blogy:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

Klikněte pravým tlačítkem myši v metodě IndexNotStonglyTyped() a přidat zobrazení Razor.

[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

Ujistěte se, **vytvoření zobrazení se silnými typy** políčko není zaškrtnuté. Výsledné zobrazení neobsahuje většinu:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

Protože používáme dynamické a ne zobrazení se silnými typy, intellisense vám nepomohly USA. Dokončený kód je zobrazena níže:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

Teď přidáme zobrazení se silnými typy. Přidejte následující kód do kontroleru:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]


Všimněte si, že je přesně stejný návratový View(topBlogs); volat jako jiné silného typu zobrazení. Klikněte pravým tlačítkem uvnitř *StonglyTypedIndex()* a vyberte **přidat zobrazení**. Tentokrát vyberte **blogu** třída modelu a vyberte **seznamu** jako šablona Scaffold.

[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

Uvnitř novou šablonu zobrazení jsme získat podporu technologie intellisense.

[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

Projekt c# si můžete stáhnout [tady](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).
