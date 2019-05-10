---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
title: Sbalení a rozbalení panelu JavaScriptem (VB) | Dokumentace Microsoftu
author: wenz
description: Rozšiřuje panelu CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit a poskytuje možnost Sbalit obsah a rozbalte ho...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 298789b4-2964-49f5-a0a8-d4dbeb9ff2c2
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: f9e279e8700024f28cf589581f09a4bbd95118de
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65133514"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-vb"></a>Sbalení a rozbalení panelu JavaScriptem (VB)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1VB.pdf)

> CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit rozšiřuje panelu a poskytuje možnost Sbalit obsah a rozbalte ho znovu. Tyto dvě akce se dá taky spustit z vlastního kódu jazyka JavaScript.

## <a name="overview"></a>Přehled

CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit rozšiřuje panelu a poskytuje možnost Sbalit obsah a rozbalte ho znovu. Tyto dvě akce se dá taky spustit z vlastního kódu jazyka JavaScript.

## <a name="steps"></a>Kroky

Za prvé, vytvoří novou stránku ASP.NET a zahrnout `ScriptManager` v rámci ten `<form>` element. Tento kód načte knihovny rozhraní ASP.NET AJAX, která vyžaduje Toolkit ovládacího prvku:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample1.aspx)]

Potom vytvořte panel s nějakým text tak, aby uvidíte efekt rozbalení/sbalení:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample2.aspx)]

Jak vidíte, na panelu odkazuje na třídu šablony stylů CSS, která je znázorněna zde (a v podstatě definuje barvu pozadí a šířka panelu):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample3.css)]

`CollapsiblePanelExtender` Vyžaduje ovládací prvek `TargetControlID` atribut tak, aby se sadou nástrojů ví, který panel chcete sbalit či rozbalit na vyžádání:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample4.aspx)]

Bohužel zařízení extender aktuálně nevystavuje konkrétního rozhraní API pro sbalení a rozbalení panelu, ale bude provádět některé nedokumentované metody. Za prvé přidejte tři tlačítka HTML na stránku, která se potom aktivuje JavaScript na straně klienta, který chcete sbalit nebo rozbalit obsah panelu:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample5.aspx)]

V kódu jazyka JavaScript na straně klienta (pracovat s `<script type="text/javascript">`), `$find()` metoda musí být používán k přístupu `CollapsiblePanelExtender`. `$find("cpe")` vrátí na něj odkaz. Odtud na konkrétní metody vyřeší daný úkol.

Metoda pro otevření (rozšíření) se nazývá panelu `_doOpen()`; následující kód implementuje `doOpen()` funkce volá, když dojde ke kliknutí na první tlačítko:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample6.js)]

Pro zavření nebo sbalení panelu `_doClose()` metoda musí být provedeny. Proto když uživatel klikne na druhé tlačítko, se nazývá následujícího kódu jazyka JavaScript:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample7.js)]

Na třetí tlačítko přepíná stav panelu: z sbaleny do rozbalený a naopak. `CollapsiblePanelExtender` Zpřístupňuje `toggle()` metodu, která činí přesně: vrátí stav panelu. Ale k dispozici je také další přístup (která vnitřně používá `toggle()` metoda): `get_Collapsed()` Metodu `CollapsiblePanelExtender()` uvádí, zda je panel odebrána nebo ne. V závislosti na návratový typ této funkce, na panelu je pak buď rozšířit (`_doOpen()` metoda) nebo sbalené (`_doClose()`) metody:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-vb/samples/sample8.js)]

[![Na třetí tlačítko změní stav panelu: z sbaleny do rozšíření a zpět](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image1.png)

Na třetí tlačítko změní stav panelu: z sbaleny do rozšíření a zpět ([kliknutím ji zobrazíte obrázek v plné velikosti](collapsing-and-expanding-a-panel-from-javascript-vb/_static/image3.png))

> [!div class="step-by-step"]
> [Předchozí](collapsing-and-expanding-a-panel-from-javascript-cs.md)
