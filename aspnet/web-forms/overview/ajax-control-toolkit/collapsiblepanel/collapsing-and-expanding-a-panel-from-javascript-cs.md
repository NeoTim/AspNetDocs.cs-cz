---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: Sbalení a rozbalení panelu JavaScriptem (C#) | Dokumentace Microsoftu
author: wenz
description: Rozšiřuje panelu CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit a poskytuje možnost Sbalit obsah a rozbalte ho...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 157a486af3d11dfbd7431680b6c9fe4f0e262892
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59422392"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a>Sbalení a rozbalení panelu JavaScriptem (C#)

by [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)

> CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit rozšiřuje panelu a poskytuje možnost Sbalit obsah a rozbalte ho znovu. Tyto dvě akce se dá taky spustit z vlastního kódu jazyka JavaScript.


## <a name="overview"></a>Přehled

CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit rozšiřuje panelu a poskytuje možnost Sbalit obsah a rozbalte ho znovu. Tyto dvě akce se dá taky spustit z vlastního kódu jazyka JavaScript.

## <a name="steps"></a>Kroky

Za prvé, vytvoří novou stránku ASP.NET a zahrnout `ScriptManager` v rámci ten `<form>` element. Tento kód načte knihovny rozhraní ASP.NET AJAX, která vyžaduje Toolkit ovládacího prvku:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

Potom vytvořte panel s nějakým text tak, aby uvidíte efekt rozbalení/sbalení:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

Jak vidíte, na panelu odkazuje na třídu šablony stylů CSS, která je znázorněna zde (a v podstatě definuje barvu pozadí a šířka panelu):

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

`CollapsiblePanelExtender` Vyžaduje ovládací prvek `TargetControlID` atribut tak, aby se sadou nástrojů ví, který panel chcete sbalit či rozbalit na vyžádání:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

Bohužel zařízení extender aktuálně nevystavuje konkrétního rozhraní API pro sbalení a rozbalení panelu, ale bude provádět některé nedokumentované metody. Za prvé přidejte tři tlačítka HTML na stránku, která se potom aktivuje JavaScript na straně klienta, který chcete sbalit nebo rozbalit obsah panelu:

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

V kódu jazyka JavaScript na straně klienta (pracovat s `<script type="text/javascript">`), `$find()` metoda musí být používán k přístupu `CollapsiblePanelExtender`. `$find("cpe")` vrátí na něj odkaz. Odtud na konkrétní metody vyřeší daný úkol.

Metoda pro otevření (rozšíření) se nazývá panelu `_doOpen()`; následující kód implementuje `doOpen()` funkce volá, když dojde ke kliknutí na první tlačítko:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

Pro zavření nebo sbalení panelu `_doClose()` metoda musí být provedeny. Proto když uživatel klikne na druhé tlačítko, se nazývá následujícího kódu jazyka JavaScript:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

Na třetí tlačítko přepíná stav panelu: z sbaleny do rozbalený a naopak. `CollapsiblePanelExtender` Zpřístupňuje `toggle()` metodu, která činí přesně: vrátí stav panelu. Ale k dispozici je také další přístup (která vnitřně používá `toggle()` metoda): `get_Collapsed()` Metodu `CollapsiblePanelExtender()` uvádí, zda je panel odebrána nebo ne. V závislosti na návratový typ této funkce, na panelu je pak buď rozšířit (`_doOpen()` metoda) nebo sbalené (`_doClose()`) metody:

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]


[![Na třetí tlačítko změní stav panelu: z sbaleny do rozšíření a zpět](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)

Na třetí tlačítko změní stav panelu: z sbaleny do rozšíření a zpět ([kliknutím ji zobrazíte obrázek v plné velikosti](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))

> [!div class="step-by-step"]
> [Next](collapsing-and-expanding-a-panel-from-javascript-vb.md)
