---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
title: Postupné provedení několika animací (C#) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Umožňuje spustit severa...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7dc02b18-2b5d-4844-b7c5-cbd818477163
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-cs
msc.type: authoredcontent
ms.openlocfilehash: a5b11b14458fdf06fb4ee18ae94c4846307e2115
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65108856"
---
# <a name="executing-several-animations-after-each-other-c"></a><span data-ttu-id="196a6-104">Postupné provedení několika animací (C#)</span><span class="sxs-lookup"><span data-stu-id="196a6-104">Executing Several Animations after Each Other (C#)</span></span>

<span data-ttu-id="196a6-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="196a6-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="196a6-106">[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="196a6-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3CS.pdf)</span></span>

> <span data-ttu-id="196a6-107">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="196a6-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="196a6-108">Umožňuje spuštění několika animací jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="196a6-108">It allows to run several animations one after the other.</span></span>

<span data-ttu-id="196a6-109">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="196a6-109">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="196a6-110">Umožňuje spuštění několika animací jednu po druhé.</span><span class="sxs-lookup"><span data-stu-id="196a6-110">It allows to run several animations one after the other.</span></span>

## <a name="steps"></a><span data-ttu-id="196a6-111">Kroky</span><span class="sxs-lookup"><span data-stu-id="196a6-111">Steps</span></span>

<span data-ttu-id="196a6-112">Za prvé, zahrnout `ScriptManager` na stránce; potom technologie ASP.NET AJAX je načíst knihovnu, což umožňuje použití Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="196a6-112">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample1.aspx)]

<span data-ttu-id="196a6-113">Animace se použijí pro panel text, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="196a6-113">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample2.aspx)]

<span data-ttu-id="196a6-114">V přidružené třídy šablony stylů CSS pro panel definovat barvu pozadí nice a také nastavit Pevná šířka panelu:</span><span class="sxs-lookup"><span data-stu-id="196a6-114">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](executing-several-animations-after-each-other-cs/samples/sample3.css)]

<span data-ttu-id="196a6-115">Pak přidejte `AnimationExtender` na stránku, poskytování `ID`, `TargetControlID` atribut a povinný údaj `runat="server":`</span><span class="sxs-lookup"><span data-stu-id="196a6-115">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server":`</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample4.aspx)]

<span data-ttu-id="196a6-116">V rámci `<Animations>` uzlu, použijte `<OnLoad>` ke spuštění animací, jakmile úplným načtením stránky.</span><span class="sxs-lookup"><span data-stu-id="196a6-116">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="196a6-117">Obecně platí `<OnLoad>` přijímá pouze jeden animace.</span><span class="sxs-lookup"><span data-stu-id="196a6-117">Generally, `<OnLoad>` only accepts one animation.</span></span> <span data-ttu-id="196a6-118">Animace framework umožňuje připojit k několika animací do jednoho pomocí `<Sequence>` elementu.</span><span class="sxs-lookup"><span data-stu-id="196a6-118">The Animation framework allows you to join several animations into one using the `<Sequence>` element.</span></span> <span data-ttu-id="196a6-119">Všechny animace v rámci `<Sequence>` jsou spuštěný jeden po druhém.</span><span class="sxs-lookup"><span data-stu-id="196a6-119">All animations within `<Sequence>` are executed one after the other.</span></span> <span data-ttu-id="196a6-120">Tady je možné značky `AnimationExtender` ovládací prvek, nejprve Příprava panelu širší a zmenšení výšku:</span><span class="sxs-lookup"><span data-stu-id="196a6-120">Here is the a possible markup for the `AnimationExtender` control, first making the panel wider and then decreasing its height:</span></span>

[!code-aspx[Main](executing-several-animations-after-each-other-cs/samples/sample5.aspx)]

<span data-ttu-id="196a6-121">Při spuštění tohoto skriptu panelu první získá širší a potom menší.</span><span class="sxs-lookup"><span data-stu-id="196a6-121">When you run this script, the panel first gets wider and then smaller.</span></span>

<span data-ttu-id="196a6-122">[![Nejprve je vyšší šířku](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="196a6-122">[![First the width is increased](executing-several-animations-after-each-other-cs/_static/image2.png)](executing-several-animations-after-each-other-cs/_static/image1.png)</span></span>

<span data-ttu-id="196a6-123">Nejprve je vyšší šířku ([kliknutím ji zobrazíte obrázek v plné velikosti](executing-several-animations-after-each-other-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="196a6-123">First the width is increased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image3.png))</span></span>

<span data-ttu-id="196a6-124">[![Pak je snížení výšky](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="196a6-124">[![Then the height is decreased](executing-several-animations-after-each-other-cs/_static/image5.png)](executing-several-animations-after-each-other-cs/_static/image4.png)</span></span>

<span data-ttu-id="196a6-125">Pak se sníží výška ([kliknutím ji zobrazíte obrázek v plné velikosti](executing-several-animations-after-each-other-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="196a6-125">Then the height is decreased ([Click to view full-size image](executing-several-animations-after-each-other-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="196a6-126">[Předchozí](executing-several-animations-at-the-same-time-cs.md)
> [další](animation-depending-on-a-condition-cs.md)</span><span class="sxs-lookup"><span data-stu-id="196a6-126">[Previous](executing-several-animations-at-the-same-time-cs.md)
[Next](animation-depending-on-a-condition-cs.md)</span></span>
