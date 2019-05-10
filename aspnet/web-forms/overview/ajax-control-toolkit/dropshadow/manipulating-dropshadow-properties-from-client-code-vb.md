---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
title: Vlastností ovládacího prvku DropShadow klientským kódem (VB) | Dokumentace Microsoftu
author: wenz
description: Sada nástrojů AJAX Control Toolkit ovládacího prvku DropShadow rozšiřuje panel s vrhá stín. Vlastnosti zařízení extender lze také změnit pomocí klienta jazyka JavaScript...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 11be4211-2fb9-4e15-b6d4-2aa623d81f3e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c44a1e95564c668f017f6116f3e62652e87eeac
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65116952"
---
# <a name="manipulating-dropshadow-properties-from-client-code-vb"></a><span data-ttu-id="059b2-104">Změna vlastností ovládacího prvku DropShadow klientským kódem (VB)</span><span class="sxs-lookup"><span data-stu-id="059b2-104">Manipulating DropShadow Properties from Client Code (VB)</span></span>

<span data-ttu-id="059b2-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="059b2-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="059b2-106">[Stáhněte si kód](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="059b2-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.vb.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2VB.pdf)</span></span>

> <span data-ttu-id="059b2-107">Sada nástrojů AJAX Control Toolkit ovládacího prvku DropShadow rozšiřuje panel s vrhá stín.</span><span class="sxs-lookup"><span data-stu-id="059b2-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="059b2-108">Vlastnosti zařízení extender můžete také změnit pomocí kód JavaScript klienta.</span><span class="sxs-lookup"><span data-stu-id="059b2-108">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="overview"></a><span data-ttu-id="059b2-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="059b2-109">Overview</span></span>

<span data-ttu-id="059b2-110">Sada nástrojů AJAX Control Toolkit ovládacího prvku DropShadow rozšiřuje panel s vrhá stín.</span><span class="sxs-lookup"><span data-stu-id="059b2-110">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="059b2-111">Vlastnosti zařízení extender můžete také změnit pomocí kód JavaScript klienta.</span><span class="sxs-lookup"><span data-stu-id="059b2-111">Properties of this extender can also be changed using client JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="059b2-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="059b2-112">Steps</span></span>

<span data-ttu-id="059b2-113">Kód spustí se panel, který obsahuje několik řádků textu:</span><span class="sxs-lookup"><span data-stu-id="059b2-113">The code starts with a panel containing some lines of text:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample1.aspx)]

<span data-ttu-id="059b2-114">Přidružené třídy šablony stylů CSS poskytuje nice pozadí panelu:</span><span class="sxs-lookup"><span data-stu-id="059b2-114">The associated CSS class gives the panel a nice background color:</span></span>

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample2.css)]

<span data-ttu-id="059b2-115">`DropShadowExtender` Se přidá k rozšíření na panelu s efektem stínu, krytí nastavena na 50 %:</span><span class="sxs-lookup"><span data-stu-id="059b2-115">The `DropShadowExtender` is added to extend the panel with a drop shadow effect, opacity set to 50%:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample3.aspx)]

<span data-ttu-id="059b2-116">Potom technologie ASP.NET AJAX `ScriptManager` ovládací prvek umožňuje Control Toolkit pracovat:</span><span class="sxs-lookup"><span data-stu-id="059b2-116">Then, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample4.aspx)]

<span data-ttu-id="059b2-117">Jiného panelu obsahuje dva odkazy jazyka JavaScript pro nastavení krytí vrhá stín: minus odkaz snižuje krytí má stín, plus odkaz se zvyšuje.</span><span class="sxs-lookup"><span data-stu-id="059b2-117">Another panel contains two JavaScript links for setting the opacity of the drop shadow: the minus link decreases the shadow's opacity, the plus link increases it.</span></span>

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample5.aspx)]

<span data-ttu-id="059b2-118">Funkce jazyka JavaScript `changeOpacity()` musí nejdříve vyhledejte `DropShadowExtender` ovládací prvek na stránce.</span><span class="sxs-lookup"><span data-stu-id="059b2-118">The JavaScript function `changeOpacity()` must then first find the `DropShadowExtender` control on the page.</span></span> <span data-ttu-id="059b2-119">Definuje technologie ASP.NET AJAX `$find()` metodu pro právě tuto úlohu.</span><span class="sxs-lookup"><span data-stu-id="059b2-119">ASP.NET AJAX defines the `$find()` method for exactly that task.</span></span> <span data-ttu-id="059b2-120">Pak, bude `get_Opacity()` metoda načte aktuální krytí `set_Opacity()` metoda ji nastaví.</span><span class="sxs-lookup"><span data-stu-id="059b2-120">Then, the `get_Opacity()` method retrieves the current opacity, the `set_Opacity()` method sets it.</span></span> <span data-ttu-id="059b2-121">Kód jazyka JavaScript pak vloží aktuální hodnota neprůhlednosti `<label>` element:</span><span class="sxs-lookup"><span data-stu-id="059b2-121">The JavaScript code then puts the current opacity value in the `<label>` element:</span></span>

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-vb/samples/sample6.html)]

<span data-ttu-id="059b2-122">[![Neprůhlednost se změní na straně klienta](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="059b2-122">[![The opacity is changed on the client side](manipulating-dropshadow-properties-from-client-code-vb/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-vb/_static/image1.png)</span></span>

<span data-ttu-id="059b2-123">Neprůhlednost se změní na straně klienta ([kliknutím ji zobrazíte obrázek v plné velikosti](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="059b2-123">The opacity is changed on the client side ([Click to view full-size image](manipulating-dropshadow-properties-from-client-code-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="059b2-124">Předchozí</span><span class="sxs-lookup"><span data-stu-id="059b2-124">Previous</span></span>](adjusting-the-z-index-of-a-dropshadow-vb.md)
