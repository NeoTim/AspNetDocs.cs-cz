---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
title: Úprava indexu z ovládacího prvku DropShadow (C#) | Dokumentace Microsoftu
author: wenz
description: Sada nástrojů AJAX Control Toolkit ovládacího prvku DropShadow rozšiřuje panel s vrhá stín. Ale stín někdy je v konfliktu s jinými ovládacími prvky pro insta...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 14133833-e518-4347-87b9-6b6f71f14a77
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-cs
msc.type: authoredcontent
ms.openlocfilehash: 5cee2acfac74c0790a7ad82bbfb503a8a16f6b47
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065995"
---
<a name="adjusting-the-z-index-of-a-dropshadow-c"></a><span data-ttu-id="83613-104">Úprava indexu Z ovládacího prvku DropShadow (C#)</span><span class="sxs-lookup"><span data-stu-id="83613-104">Adjusting the Z-Index of a DropShadow (C#)</span></span>
====================
<span data-ttu-id="83613-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="83613-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="83613-106">[Stáhněte si kód](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="83613-106">[Download Code](http://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1CS.pdf)</span></span>

> <span data-ttu-id="83613-107">Sada nástrojů AJAX Control Toolkit ovládacího prvku DropShadow rozšiřuje panel s vrhá stín.</span><span class="sxs-lookup"><span data-stu-id="83613-107">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="83613-108">Ale stín někdy je v konfliktu s jinými ovládacími prvky, například ovládací prvek ASP.NET nabídky.</span><span class="sxs-lookup"><span data-stu-id="83613-108">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="83613-109">Pokud položka nabídky se zobrazí, se zobrazí za vrhá stín.</span><span class="sxs-lookup"><span data-stu-id="83613-109">When a menu entry pops up, it appears behind the drop shadow.</span></span>


## <a name="overview"></a><span data-ttu-id="83613-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="83613-110">Overview</span></span>

<span data-ttu-id="83613-111">Sada nástrojů AJAX Control Toolkit ovládacího prvku DropShadow rozšiřuje panel s vrhá stín.</span><span class="sxs-lookup"><span data-stu-id="83613-111">The DropShadow control in the AJAX Control Toolkit extends a panel with a drop shadow.</span></span> <span data-ttu-id="83613-112">Ale stín někdy je v konfliktu s jinými ovládacími prvky, například ovládací prvek ASP.NET nabídky.</span><span class="sxs-lookup"><span data-stu-id="83613-112">However this shadow sometimes conflicts with other controls, for instance the ASP.NET Menu control.</span></span> <span data-ttu-id="83613-113">Pokud položka nabídky se zobrazí, se zobrazí za vrhá stín.</span><span class="sxs-lookup"><span data-stu-id="83613-113">When a menu entry pops up, it appears behind the drop shadow.</span></span>

## <a name="steps"></a><span data-ttu-id="83613-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="83613-114">Steps</span></span>

<span data-ttu-id="83613-115">Kód začíná samostatně, Panel obsahující dostatečné množství textu, tak, aby panel obsahuje dostatek text pro efekt uvidí:</span><span class="sxs-lookup"><span data-stu-id="83613-115">The code commences with the Panel itself, containing enough text so that the panel contains enough text for the effect to be visible:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample1.aspx)]

<span data-ttu-id="83613-116">Jiného panelu je umístěna přímo před `panelShadow` panel.</span><span class="sxs-lookup"><span data-stu-id="83613-116">Another panel is placed directly before the `panelShadow` panel.</span></span> <span data-ttu-id="83613-117">Obsahuje nabídku s vodorovné orientaci, tak, aby položky nabídek zobrazují nad (nebo spíše: v části) `dropShadow` panel):</span><span class="sxs-lookup"><span data-stu-id="83613-117">It contains a menu with horizontal orientation so that menu entries appear over (or rather: under) the `dropShadow` panel):</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample2.aspx)]

<span data-ttu-id="83613-118">Pak, bude `DropShadowExtender` se přidá k rozšíření `panelShadow` panelu s efektem stínu:</span><span class="sxs-lookup"><span data-stu-id="83613-118">Then, the `DropShadowExtender` is added to extend the `panelShadow` panel with a drop shadow effect:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample3.aspx)]

<span data-ttu-id="83613-119">Nakonec technologie ASP.NET AJAX `ScriptManager` ovládací prvek umožňuje Control Toolkit pracovat:</span><span class="sxs-lookup"><span data-stu-id="83613-119">Finally, the ASP.NET AJAX `ScriptManager` control enables the Control Toolkit to work:</span></span>

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample4.aspx)]

<span data-ttu-id="83613-120">Při spuštění tohoto skriptu se zobrazí pod panelu položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="83613-120">When you run this script, the menu entries appear underneath the panel.</span></span> <span data-ttu-id="83613-121">Ale používá třídu šablony stylů CSS v nabídce `panel` kde stačí definovat dvě věci, aby se elementy zobrazí před na panelu:</span><span class="sxs-lookup"><span data-stu-id="83613-121">However the menu uses the CSS class `panel` where you just have to define two things to make elements appear in front of the other panel:</span></span>

- <span data-ttu-id="83613-122">Relativní umístění</span><span class="sxs-lookup"><span data-stu-id="83613-122">Relative positioning</span></span>
- <span data-ttu-id="83613-123">Kladné z-index</span><span class="sxs-lookup"><span data-stu-id="83613-123">A positive z-index</span></span>

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-cs/samples/sample5.css)]

<span data-ttu-id="83613-124">Pak, bude `DropShadowExtender` ovládací prvek není v konfliktu už pomocí ovládacího prvku nabídky.</span><span class="sxs-lookup"><span data-stu-id="83613-124">Then, the `DropShadowExtender` control does not conflict any longer with the Menu control.</span></span>


<span data-ttu-id="83613-125">[![Před: Položka nabídky se nezobrazuje](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="83613-125">[![Before: The menu entry is not visible](adjusting-the-z-index-of-a-dropshadow-cs/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image1.png)</span></span>

<span data-ttu-id="83613-126">Před: Položka nabídky se nezobrazuje ([kliknutím ji zobrazíte obrázek v plné velikosti](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="83613-126">Before: The menu entry is not visible ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image3.png))</span></span>


<span data-ttu-id="83613-127">[![Po: Zobrazí se položka nabídky](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="83613-127">[![After: The menu entry appears](adjusting-the-z-index-of-a-dropshadow-cs/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-cs/_static/image4.png)</span></span>

<span data-ttu-id="83613-128">Po: Zobrazí se položka nabídky ([kliknutím ji zobrazíte obrázek v plné velikosti](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="83613-128">After: The menu entry appears ([Click to view full-size image](adjusting-the-z-index-of-a-dropshadow-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="83613-129">Next</span><span class="sxs-lookup"><span data-stu-id="83613-129">Next</span></span>](manipulating-dropshadow-properties-from-client-code-cs.md)
