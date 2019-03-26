---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
title: Přidání animace k ovládacímu prvku (C#) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Tento kurz ukazuje, jak...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0f1fc1f5-9dbd-44e7-931e-387d42f0342b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: aac6e97ae5d3d777c3644515628d2669076a88c4
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/25/2019
ms.locfileid: "58421918"
---
<a name="adding-animation-to-a-control-c"></a><span data-ttu-id="ea475-104">Přidání animace k ovládacímu prvku (C#)</span><span class="sxs-lookup"><span data-stu-id="ea475-104">Adding Animation to a Control (C#)</span></span>
====================
<span data-ttu-id="ea475-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="ea475-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="ea475-106">[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="ea475-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1CS.pdf)</span></span>

> <span data-ttu-id="ea475-107">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="ea475-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ea475-108">Tento kurz ukazuje, jak nastavit tyto animace.</span><span class="sxs-lookup"><span data-stu-id="ea475-108">This tutorial shows how to set up such an animation.</span></span>


## <a name="overview"></a><span data-ttu-id="ea475-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="ea475-109">Overview</span></span>

<span data-ttu-id="ea475-110">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="ea475-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="ea475-111">Tento kurz ukazuje, jak nastavit tyto animace.</span><span class="sxs-lookup"><span data-stu-id="ea475-111">This tutorial shows how to set up such an animation.</span></span>

## <a name="steps"></a><span data-ttu-id="ea475-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="ea475-112">Steps</span></span>

<span data-ttu-id="ea475-113">Prvním krokem je jako obvykle zahrnují `ScriptManager` na stránce tak, aby je načtena knihovna ASP.NET AJAX a Control Toolkit je možné:</span><span class="sxs-lookup"><span data-stu-id="ea475-113">The first step is as usual to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="ea475-114">Animace v tomto scénáři se použijí pro panel text, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="ea475-114">The animation in this scenario will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="ea475-115">Přidružené třídy šablony stylů CSS pro panel definuje barvu pozadí a šířku:</span><span class="sxs-lookup"><span data-stu-id="ea475-115">The associated CSS class for the panel defines a background color and a width:</span></span>

[!code-css[Main](adding-animation-to-a-control-cs/samples/sample3.css)]

<span data-ttu-id="ea475-116">Dále až, potřebujeme `AnimationExtender`.</span><span class="sxs-lookup"><span data-stu-id="ea475-116">Next up, we need the `AnimationExtender`.</span></span> <span data-ttu-id="ea475-117">Po zadání `ID` a obvyklého `runat="server"`, `TargetControlID` atribut musí být nastaven na ovládací prvek pro animaci v našem případě panelu:</span><span class="sxs-lookup"><span data-stu-id="ea475-117">After providing an `ID` and the usual `runat="server"`, the `TargetControlID` attribute must be set to the control to animate in our case, the panel:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="ea475-118">Celý animace použije deklarativně pomocí syntaxe jazyka XML, bohužel momentálně nejsou plně podporovány v sadě Visual Studio IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="ea475-118">The whole animation is applied declaratively, using an XML syntax, unfortunately currently not fully supported by Visual Studio's IntelliSense.</span></span> <span data-ttu-id="ea475-119">Kořenový uzel je `<Animations>;` v rámci tohoto uzlu, jsou povoleny několik událostí, které určují, kdy animace přezkumném místě:</span><span class="sxs-lookup"><span data-stu-id="ea475-119">The root node is `<Animations>;` within this node, several events are allowed which determine when the animation(s) take(s) place:</span></span>

- <span data-ttu-id="ea475-120">`OnClick` (kliknutí myší)</span><span class="sxs-lookup"><span data-stu-id="ea475-120">`OnClick` (mouse click)</span></span>
- <span data-ttu-id="ea475-121">`OnHoverOut` (když ukazatel myši opustí ovládací prvek)</span><span class="sxs-lookup"><span data-stu-id="ea475-121">`OnHoverOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="ea475-122">`OnHoverOver` (po umístění ukazatele myši nad ovládací prvek, zastavuje `OnHoverOut` animace)</span><span class="sxs-lookup"><span data-stu-id="ea475-122">`OnHoverOver` (when the mouse hovers over a control, stopping the `OnHoverOut` animation)</span></span>
- <span data-ttu-id="ea475-123">`OnLoad` (Pokud na stránce se načetl)</span><span class="sxs-lookup"><span data-stu-id="ea475-123">`OnLoad` (when the page has been loaded)</span></span>
- <span data-ttu-id="ea475-124">`OnMouseOut` (když ukazatel myši opustí ovládací prvek)</span><span class="sxs-lookup"><span data-stu-id="ea475-124">`OnMouseOut` (when the mouse leaves a control)</span></span>
- <span data-ttu-id="ea475-125">`OnMouseOver` (po umístění ukazatele myši nad ovládací prvek, ne zastavení `OnMouseOut` animace)</span><span class="sxs-lookup"><span data-stu-id="ea475-125">`OnMouseOver` (when the mouse hovers over a control, not stopping the `OnMouseOut` animation)</span></span>

<span data-ttu-id="ea475-126">Rozhraní framework obsahuje sadu animace, každý z nich představované vlastní – element XML.</span><span class="sxs-lookup"><span data-stu-id="ea475-126">The framework comes with a set of animations, each one represented by its own XML element.</span></span> <span data-ttu-id="ea475-127">Tady je výběr:</span><span class="sxs-lookup"><span data-stu-id="ea475-127">Here is a selection:</span></span>

- <span data-ttu-id="ea475-128">`<Color>` (a změníte barvu)</span><span class="sxs-lookup"><span data-stu-id="ea475-128">`<Color>` (changing a color)</span></span>
- <span data-ttu-id="ea475-129">`<FadeIn>` (pozvolného)</span><span class="sxs-lookup"><span data-stu-id="ea475-129">`<FadeIn>` (fading in)</span></span>
- <span data-ttu-id="ea475-130">`<FadeOut>` (mizení)</span><span class="sxs-lookup"><span data-stu-id="ea475-130">`<FadeOut>` (fading out)</span></span>
- <span data-ttu-id="ea475-131">`<Property>` (při změně hodnoty vlastnosti ovládacího prvku)</span><span class="sxs-lookup"><span data-stu-id="ea475-131">`<Property>` (changing a control's property)</span></span>
- <span data-ttu-id="ea475-132">`<Pulse>` (pulsating)</span><span class="sxs-lookup"><span data-stu-id="ea475-132">`<Pulse>` (pulsating)</span></span>
- <span data-ttu-id="ea475-133">`<Resize>` (Změna velikosti)</span><span class="sxs-lookup"><span data-stu-id="ea475-133">`<Resize>` (changing the size)</span></span>
- <span data-ttu-id="ea475-134">`<Scale>` (proporcionálně změnou velikosti)</span><span class="sxs-lookup"><span data-stu-id="ea475-134">`<Scale>` (proportionally changing the size)</span></span>

<span data-ttu-id="ea475-135">V tomto příkladu se zesvětlit panelu. Animace přijmou půl sekundy (`Duration` atribut), zobrazení 24 snímků (kroky animace) za sekundu (`Fps` atributu).</span><span class="sxs-lookup"><span data-stu-id="ea475-135">In this example, the panel shall fade out. The animation shall take 1.5 seconds (`Duration` attribute), displaying 24 frames (animation steps) per second (`Fps` attribute).</span></span> <span data-ttu-id="ea475-136">Tady je kompletní kód pro `AnimationExtender` ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="ea475-136">Here is the complete markup for the `AnimationExtender` control:</span></span>

[!code-aspx[Main](adding-animation-to-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="ea475-137">Při spuštění tohoto skriptu na panelu se zobrazí a setmívá v jedné a půl sekundy.</span><span class="sxs-lookup"><span data-stu-id="ea475-137">When you run this script, the panel is displayed and fades out in one and a half seconds.</span></span>


<span data-ttu-id="ea475-138">[![Je mizení panelu](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ea475-138">[![The panel is fading out](adding-animation-to-a-control-cs/_static/image2.png)](adding-animation-to-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="ea475-139">Na panelu je mizení ([kliknutím ji zobrazíte obrázek v plné velikosti](adding-animation-to-a-control-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ea475-139">The panel is fading out ([Click to view full-size image](adding-animation-to-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ea475-140">Next</span><span class="sxs-lookup"><span data-stu-id="ea475-140">Next</span></span>](executing-several-animations-at-the-same-time-cs.md)
