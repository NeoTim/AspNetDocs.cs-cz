---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Vytvoření zobrazení (uživatelského rozhraní) | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59408235"
---
# <a name="create-the-view-ui"></a>Vytvoření zobrazení (uživatelského rozhraní)

podle [Mike Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části se začnou definovat kód HTML pro aplikace a přidání datové vazby mezi HTML a model zobrazení.

Otevřete soubor Views/Home/Index.cshtml. Celý obsah tohoto souboru nahraďte následujícím kódem.

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

Většina `div` prvky jsou pro [Bootstrap](http://getbootstrap.com/) práce se styly. Důležité prvky jsou ty, které se `data-bind` atributy. Tento atribut odkazuje na model zobrazení HTML.

Příklad:

[!code-html[Main](part-7/samples/sample2.html)]

V tomto příkladu &quot; `text` &quot; vazby způsobí, že `<p>` prvek, který chcete zobrazit hodnotu `error` vlastnost z modelu zobrazení. Vzpomeňte si, že `error` byl deklarován jako `ko.observable`:

[!code-javascript[Main](part-7/samples/sample3.js)]

Vždy, když je nová hodnota přiřazená `error`, Knockout aktualizace textu `<p>` element.

`foreach` Vazby říká Knockout pro cyklický průchod obsah `books` pole. Pro každou položku v poli, vytvoří novou Knockout &lt;li&gt; elementu. Vazby v kontextu `foreach` odkazují na vlastnosti pro položku pole. Příklad:

[!code-html[Main](part-7/samples/sample4.html)]

Tady `text` vazby načte vlastnost Autor jednotlivé knihy.

Pokud nyní aplikaci spustíte, by měl vypadat takto:

![](part-7/_static/image1.png)

Seznam knihy načte asynchronně, po načtení stránky. Právě teď &quot;podrobnosti&quot; odkazy nejsou funkční. Tato funkce přidáme v další části.

> [!div class="step-by-step"]
> [Předchozí](part-6.md)
> [další](part-8.md)
