---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: Dynamické zobrazení vs. Zobrazení silného typu | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 30b84c71c86e455f15a659abf566750f1c6eea90
ms.sourcegitcommit: feb88edfb01b32f6fc9488f0f0ddb3c5b34e6ff0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2020
ms.locfileid: "88702943"
---
# <a name="dynamic-v-strongly-typed-views"></a>Dynamické zobrazení vs. zobrazení se silnými typy

od [Rick Anderson](https://twitter.com/RickAndMSFT)

Existují tři způsoby, jak předat informace z kontroleru k zobrazení v ASP.NET MVC 3:

1. Jako objekt modelu silného typu.
2. Jako dynamický typ (pomocí @model dynamického)
3. Použití ViewBag

Napsal (a) jsem jednoduchou přední aplikaci MVC 3 k porovnání a kontrastu dynamických a silných zobrazení typu. Kontroler začíná jednoduchým seznamem blogů:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

Klikněte pravým tlačítkem na metodu IndexNotStonglyTyped () a přidejte zobrazení Razor.

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

Ujistěte se, že není zaškrtnuto políčko **vytvořit zobrazení silného typu** . Výsledný pohled neobsahuje mnohem:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

Vzhledem k tomu, že používáme dynamické a nesilné zobrazení, IntelliSense nám to nepomůže. Dokončený kód je zobrazen níže:

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646. NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

Nyní přidáme zobrazení silného typu. Do kontroleru přidejte následující kód:

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

Všimněte si, že je přesně stejný návratový pohled (topBlogs); volání jako zobrazení bez silného typu. Klikněte pravým tlačítkem myši v *StonglyTypedIndex ()* a vyberte **Přidat zobrazení**. Tentokrát vyberte třídu modelu **blogu** a vyberte **seznam** jako šablonu generování uživatelského rozhraní.

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

V nové šabloně zobrazení získáme podporu IntelliSense.

[![7002. IntelliSense [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)
