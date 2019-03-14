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
ms.openlocfilehash: 325194fc1f980714ea2fc26cfaa13d86ae9d2f89
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068017"
---
<a name="collapsing-and-expanding-a-panel-from-javascript-c"></a><span data-ttu-id="b63d8-103">Sbalení a rozbalení panelu JavaScriptem (C#)</span><span class="sxs-lookup"><span data-stu-id="b63d8-103">Collapsing and Expanding a Panel from JavaScript (C#)</span></span>
====================
<span data-ttu-id="b63d8-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="b63d8-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="b63d8-105">[Stáhněte si kód](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="b63d8-105">[Download Code](http://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)</span></span>

> <span data-ttu-id="b63d8-106">CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit rozšiřuje panelu a poskytuje možnost Sbalit obsah a rozbalte ho znovu.</span><span class="sxs-lookup"><span data-stu-id="b63d8-106">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="b63d8-107">Tyto dvě akce se dá taky spustit z vlastního kódu jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b63d8-107">These two actions can also be triggered from custom JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="b63d8-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="b63d8-108">Overview</span></span>

<span data-ttu-id="b63d8-109">CollapsiblePanel ovládacího prvku ASP.NET AJAX Control Toolkit rozšiřuje panelu a poskytuje možnost Sbalit obsah a rozbalte ho znovu.</span><span class="sxs-lookup"><span data-stu-id="b63d8-109">The CollapsiblePanel control in the ASP.NET AJAX Control Toolkit extends a panel and provides it with the capability to collapse its contents and expand it again.</span></span> <span data-ttu-id="b63d8-110">Tyto dvě akce se dá taky spustit z vlastního kódu jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b63d8-110">These two actions can also be triggered from custom JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="b63d8-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="b63d8-111">Steps</span></span>

<span data-ttu-id="b63d8-112">Za prvé, vytvoří novou stránku ASP.NET a zahrnout `ScriptManager` v rámci ten `<form>` element.</span><span class="sxs-lookup"><span data-stu-id="b63d8-112">First of all, create a new ASP.NET page and include the `ScriptManager` within the one `<form>` element.</span></span> <span data-ttu-id="b63d8-113">Tento kód načte knihovny rozhraní ASP.NET AJAX, která vyžaduje Toolkit ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="b63d8-113">This loads the ASP.NET AJAX library which is required by the Control Toolkit:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="b63d8-114">Potom vytvořte panel s nějakým text tak, aby uvidíte efekt rozbalení/sbalení:</span><span class="sxs-lookup"><span data-stu-id="b63d8-114">Then, create a panel with some text so that the collapse/expand effect can be seen:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="b63d8-115">Jak vidíte, na panelu odkazuje na třídu šablony stylů CSS, která je znázorněna zde (a v podstatě definuje barvu pozadí a šířka panelu):</span><span class="sxs-lookup"><span data-stu-id="b63d8-115">As you can see, the panel references a CSS class which is shown here (and basically defines a background color and the panel's width):</span></span>

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

<span data-ttu-id="b63d8-116">`CollapsiblePanelExtender` Vyžaduje ovládací prvek `TargetControlID` atribut tak, aby se sadou nástrojů ví, který panel chcete sbalit či rozbalit na vyžádání:</span><span class="sxs-lookup"><span data-stu-id="b63d8-116">The `CollapsiblePanelExtender` control requires the `TargetControlID` attribute so that the toolkit knows which panel to collapse or expand upon request:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

<span data-ttu-id="b63d8-117">Bohužel zařízení extender aktuálně nevystavuje konkrétního rozhraní API pro sbalení a rozbalení panelu, ale bude provádět některé nedokumentované metody.</span><span class="sxs-lookup"><span data-stu-id="b63d8-117">Unfortunately, the extender currently does not expose a specific API for collapsing or expanding the panel, but some undocumented methods will do.</span></span> <span data-ttu-id="b63d8-118">Za prvé přidejte tři tlačítka HTML na stránku, která se potom aktivuje JavaScript na straně klienta, který chcete sbalit nebo rozbalit obsah panelu:</span><span class="sxs-lookup"><span data-stu-id="b63d8-118">First of all, add three HTML buttons to the page which will then trigger the client-side JavaScript to collapse or expand the panel's contents:</span></span>

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="b63d8-119">V kódu jazyka JavaScript na straně klienta (pracovat s `<script type="text/javascript">`), `$find()` metoda musí být používán k přístupu `CollapsiblePanelExtender`.</span><span class="sxs-lookup"><span data-stu-id="b63d8-119">In the client-side JavaScript code (started with `<script type="text/javascript">`), the `$find()` method needs to be used to access the `CollapsiblePanelExtender`.</span></span> <span data-ttu-id="b63d8-120">`$find("cpe")` vrátí na něj odkaz.</span><span class="sxs-lookup"><span data-stu-id="b63d8-120">`$find("cpe")` will return a reference to it.</span></span> <span data-ttu-id="b63d8-121">Odtud na konkrétní metody vyřeší daný úkol.</span><span class="sxs-lookup"><span data-stu-id="b63d8-121">From there on, specific methods will solve the task at hand.</span></span>

<span data-ttu-id="b63d8-122">Metoda pro otevření (rozšíření) se nazývá panelu `_doOpen()`; následující kód implementuje `doOpen()` funkce volá, když dojde ke kliknutí na první tlačítko:</span><span class="sxs-lookup"><span data-stu-id="b63d8-122">The method for opening (expanding) the panel is called `_doOpen()`; the following code implements the `doOpen()` function called when the first button is clicked:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

<span data-ttu-id="b63d8-123">Pro zavření nebo sbalení panelu `_doClose()` metoda musí být provedeny.</span><span class="sxs-lookup"><span data-stu-id="b63d8-123">For closing, or collapsing the panel, the `_doClose()` method needs to be executed.</span></span> <span data-ttu-id="b63d8-124">Proto když uživatel klikne na druhé tlačítko, se nazývá následujícího kódu jazyka JavaScript:</span><span class="sxs-lookup"><span data-stu-id="b63d8-124">So when the user clicks on the second button, the following JavaScript code is called:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

<span data-ttu-id="b63d8-125">Na třetí tlačítko přepíná stav panelu: z sbaleny do rozbalený a naopak.</span><span class="sxs-lookup"><span data-stu-id="b63d8-125">The third button toggles the state of the panel: from collapsed to expanded, and vice versa.</span></span> <span data-ttu-id="b63d8-126">`CollapsiblePanelExtender` Zpřístupňuje `toggle()` metodu, která činí přesně: vrátí stav panelu.</span><span class="sxs-lookup"><span data-stu-id="b63d8-126">The `CollapsiblePanelExtender` exposes the `toggle()` method which does exactly that: reverses the state of the panel.</span></span> <span data-ttu-id="b63d8-127">Ale k dispozici je také další přístup (která vnitřně používá `toggle()` metoda): `get_Collapsed()` Metodu `CollapsiblePanelExtender()` uvádí, zda je panel odebrána nebo ne.</span><span class="sxs-lookup"><span data-stu-id="b63d8-127">However there is also another approach (which is internally used by the `toggle()` method): The `get_Collapsed()` method of the `CollapsiblePanelExtender()` tells us whether the panel is collapsed or not.</span></span> <span data-ttu-id="b63d8-128">V závislosti na návratový typ této funkce, na panelu je pak buď rozšířit (`_doOpen()` metoda) nebo sbalené (`_doClose()`) metody:</span><span class="sxs-lookup"><span data-stu-id="b63d8-128">Depending on the return value of this function, the panel is then either expanded (`_doOpen()` method) or collapsed (`_doClose()`) method:</span></span>

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]


<span data-ttu-id="b63d8-129">[![Na třetí tlačítko změní stav panelu: z sbaleny do rozšíření a zpět](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b63d8-129">[![The third button changes the state of the panel: from collapsed to expanded and back](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="b63d8-130">Na třetí tlačítko změní stav panelu: z sbaleny do rozšíření a zpět ([kliknutím ji zobrazíte obrázek v plné velikosti](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b63d8-130">The third button changes the state of the panel: from collapsed to expanded and back ([Click to view full-size image](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b63d8-131">Next</span><span class="sxs-lookup"><span data-stu-id="b63d8-131">Next</span></span>](collapsing-and-expanding-a-panel-from-javascript-vb.md)
