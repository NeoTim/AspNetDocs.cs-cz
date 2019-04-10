---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: Vytvoření omezení trasy (C#) | Dokumentace Microsoftu
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak prohlížeč požaduje shoda tras tak, že vytvoříte omezení trasy s regulárními výrazy.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 42c0ce5e158e2fe9387ac218ac0762b6362094f9
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59389568"
---
# <a name="creating-a-route-constraint-c"></a>Vytvoření omezení trasy (C#)

podle [Stephen Walther](https://github.com/StephenWalther)

> V tomto kurzu Stephen Walther ukazuje, jak můžete řídit, jak prohlížeč požaduje shoda tras tak, že vytvoříte omezení trasy s regulárními výrazy.


Pomocí omezení trasy omezte požadavků prohlížeče, které odpovídají konkrétní trasy. Regulární výraz můžete použít k určení omezení trasy.

Představte si například, kterou jste definovali trasy v informacích 1 v souboru Global.asax.

**Listing 1 - Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

Výpis 1 obsahuje trasa s názvem produktu. Trasy produktu můžete použít k mapování požadavků prohlížeče ProductController součástí výpis 2.

**Výpis 2 - Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

Všimněte si, že akce Details() vystavené kontroler produktu přijímá jeden parametr s názvem productId. Tento parametr je parametr celé číslo.

Trasy definované v informacích 1 se shodují s některým z následujících adres URL:

- / Produktu/23
- / Produktu/7

Bohužel trasy se taky shodovat následující adresy URL:

- / Produktu/Bla
- / Produktu/apple

Protože akce Details() očekává jako parametr celé číslo, požadavku, který obsahuje něco jiného než celočíselnou hodnotu způsobí chybu. Například pokud do prohlížeče zadáte adresu URL /Product/apple pak zobrazí se chybová stránka na obrázku 1.


[![TDialogové okno Nový projekt he](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**Obrázek 01**: Stránka rozbalit zobrazuje ([kliknutím ji zobrazíte obrázek v plné velikosti](creating-a-route-constraint-cs/_static/image2.png))


Co vlastně chcete udělat, je odpovídá pouze adresy URL, které obsahují productId správné celé číslo. Omezení můžete použít při definování trasy omezovat adresy URL, které odpovídají trasy. Upravené trasy produktu ve výpisu 3 obsahuje omezení regulárního výrazu, který odpovídá jen celá čísla.

**Listing 3 - Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

\D+ regulárního výrazu odpovídá jedné nebo více celých čísel. Vlivem tohoto omezení trasy produkt tak, aby odpovídala následující adresy URL:

- / Produkt/3
- / Produktu/8999

Ale ne následující adresy URL:

- / Produktu/apple
- / Produktu

- Tyto požadavky prohlížeče bude zpracován adresou jiné cestě nebo, pokud nejsou žádné odpovídající trasy *prostředek se nenašel* se vrátí chyba.

> [!div class="step-by-step"]
> [Předchozí](creating-custom-routes-cs.md)
> [další](creating-a-custom-route-constraint-cs.md)
