---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: Zakázání akcí během animace (VB) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Podporuje také akce...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 811e1d75f79885f3f4c561d9211fec625fcf1807
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068452"
---
<a name="disabling-actions-during-animation-vb"></a><span data-ttu-id="1b429-104">Zakázání akcí během animace (VB)</span><span class="sxs-lookup"><span data-stu-id="1b429-104">Disabling Actions during Animation (VB)</span></span>
====================
<span data-ttu-id="1b429-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1b429-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1b429-106">[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="1b429-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)</span></span>

> <span data-ttu-id="1b429-107">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="1b429-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1b429-108">Podporuje také akce, jako je kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="1b429-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="1b429-109">Ale při kliknutí myší spuštění animace, je třeba zakázat kliknutí myší během animace.</span><span class="sxs-lookup"><span data-stu-id="1b429-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>


## <a name="overview"></a><span data-ttu-id="1b429-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="1b429-110">Overview</span></span>

<span data-ttu-id="1b429-111">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="1b429-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1b429-112">Podporuje také akce, jako je kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="1b429-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="1b429-113">Ale při kliknutí myší spuštění animace, je třeba zakázat kliknutí myší během animace.</span><span class="sxs-lookup"><span data-stu-id="1b429-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="1b429-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="1b429-114">Steps</span></span>

<span data-ttu-id="1b429-115">Za prvé, zahrnout `ScriptManager` na stránce; potom technologie ASP.NET AJAX je načíst knihovnu, což umožňuje použití Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="1b429-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

<span data-ttu-id="1b429-116">Uplatní se animace k tlačítku HTML tímto způsobem:</span><span class="sxs-lookup"><span data-stu-id="1b429-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

<span data-ttu-id="1b429-117">Mějte na paměti, že ovládací prvek je použít místo webový ovládací prvek, protože jsme nechcete, aby na tlačítko Vytvořit zpětné volání; právě zahájí animací na straně klienta pro nás.</span><span class="sxs-lookup"><span data-stu-id="1b429-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="1b429-118">Pak přidejte `AnimationExtender` na stránku, poskytování `ID`, `TargetControlID` atribut a povinný údaj `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="1b429-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

<span data-ttu-id="1b429-119">V rámci `<Animations>` uzlu `<OnClick>` je správný prvek a zpracování kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="1b429-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="1b429-120">Však může být stisknuto během animace, stejně.</span><span class="sxs-lookup"><span data-stu-id="1b429-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="1b429-121">`<EnableAction>` Element zařídit, který.</span><span class="sxs-lookup"><span data-stu-id="1b429-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="1b429-122">Nastavení `Enabled="false"` zakáže tlačítko jako součást animace.</span><span class="sxs-lookup"><span data-stu-id="1b429-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="1b429-123">Protože používáme několika jednotlivých animací (zakázání tlačítka a skutečné animací), `<Parallel>` je vyžadován prvek připevněte jedné animace dohromady do jedné.</span><span class="sxs-lookup"><span data-stu-id="1b429-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="1b429-124">Tady je kompletní kód pro `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="1b429-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

<span data-ttu-id="1b429-125">Také je možné znovu povolit tlačítko po animaci pomocí následujícího elementu XML na konci seznamu:</span><span class="sxs-lookup"><span data-stu-id="1b429-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

<span data-ttu-id="1b429-126">Ale v daném scénáři to může být zbytečné od tlačítko setmívá a není viditelný na konci animace.</span><span class="sxs-lookup"><span data-stu-id="1b429-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>


<span data-ttu-id="1b429-127">[![Poté, co běží animaci je tlačítko neaktivní.](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1b429-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)</span></span>

<span data-ttu-id="1b429-128">Je tlačítko neaktivní co nejdříve po spuštění animace ([kliknutím ji zobrazíte obrázek v plné velikosti](disabling-actions-during-animation-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="1b429-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1b429-129">[Předchozí](animating-in-response-to-user-interaction-vb.md)
> [další](triggering-an-animation-in-another-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="1b429-129">[Previous](animating-in-response-to-user-interaction-vb.md)
[Next](triggering-an-animation-in-another-control-vb.md)</span></span>