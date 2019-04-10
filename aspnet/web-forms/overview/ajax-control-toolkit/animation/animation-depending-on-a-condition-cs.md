---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: Animace závislá na podmínce (C#) | Dokumentace Microsoftu
author: wenz
description: Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku. Určuje, zda je animace...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: c05f0976a135615f7a272b8057eb4c56677e5117
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59412421"
---
# <a name="animation-depending-on-a-condition-c"></a><span data-ttu-id="74106-104">Animace závislá na podmínce (C#)</span><span class="sxs-lookup"><span data-stu-id="74106-104">Animation Depending On a Condition (C#)</span></span>

<span data-ttu-id="74106-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="74106-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="74106-106">[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="74106-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)</span></span>

> <span data-ttu-id="74106-107">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="74106-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="74106-108">Určuje, zda je animaci spustit nebo ne může také záviset na podmínky v podobě kódu jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="74106-108">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>


## <a name="overview"></a><span data-ttu-id="74106-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="74106-109">Overview</span></span>

<span data-ttu-id="74106-110">Animace ovládacího prvku ASP.NET AJAX Control Toolkit je právě ovládacího prvku, ale celé rozhraní pro přidání animace k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="74106-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="74106-111">Určuje, zda je animaci spustit nebo ne může také záviset na podmínky v podobě kódu jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="74106-111">Whether an animation is run or not can also depend on a condition in form of some JavaScript code.</span></span>

## <a name="steps"></a><span data-ttu-id="74106-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="74106-112">Steps</span></span>

<span data-ttu-id="74106-113">Za prvé, zahrnout `ScriptManager` na stránce; potom technologie ASP.NET AJAX je načíst knihovnu, což umožňuje použití Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="74106-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

<span data-ttu-id="74106-114">Animace se použijí pro panel text, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="74106-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

<span data-ttu-id="74106-115">V přidružené třídy šablony stylů CSS pro panel definovat barvu pozadí nice a také nastavit Pevná šířka panelu:</span><span class="sxs-lookup"><span data-stu-id="74106-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

<span data-ttu-id="74106-116">Pak přidejte `AnimationExtender` na stránku, poskytování `ID`, `TargetControlID` atribut a povinný údaj</span><span class="sxs-lookup"><span data-stu-id="74106-116">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory</span></span> `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

<span data-ttu-id="74106-117">V rámci `<Animations>` uzlu, použijte `<OnLoad>` ke spuštění animací, jakmile úplným načtením stránky.</span><span class="sxs-lookup"><span data-stu-id="74106-117">Within the `<Animations>` node, use `<OnLoad>` to run the animations once the page has been fully loaded.</span></span> <span data-ttu-id="74106-118">Místo jednoho regulární animací `<Condition>` element vstupu do play.</span><span class="sxs-lookup"><span data-stu-id="74106-118">Instead of one of the regular animations, the `<Condition>` element comes into play.</span></span> <span data-ttu-id="74106-119">Kód jazyka JavaScript ve formě hodnoty `ConditionScript` atribut je proveden za běhu.</span><span class="sxs-lookup"><span data-stu-id="74106-119">The JavaScript code provided as the value of the `ConditionScript` attribute is executed at runtime.</span></span> <span data-ttu-id="74106-120">Pokud je vyhodnocen jako true, animace provádí, v opačném případě ne.</span><span class="sxs-lookup"><span data-stu-id="74106-120">If it evaluates to true, the animation is executed, otherwise not.</span></span> <span data-ttu-id="74106-121">Následující kód obsahuje dvě animace, každý z nich prováděný 50 % případů na náhodné.</span><span class="sxs-lookup"><span data-stu-id="74106-121">The following markup provides two animations, each of them being executed in 50% of cases upon random.</span></span> <span data-ttu-id="74106-122">Protože může existovat jenom jeden animace v rámci `<OnLoad>`, dva `<Condition>` animace se propojují s použitím `<Sequence>` element:</span><span class="sxs-lookup"><span data-stu-id="74106-122">Since there may only be one animation within `<OnLoad>`, the two `<Condition>` animations are joined together using the `<Sequence>` element:</span></span>

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

<span data-ttu-id="74106-123">Všimněte si, že menší než znaménko (`<`) v `ConditionScript` atribut musí být uvozený uvozovacím znakem ().</span><span class="sxs-lookup"><span data-stu-id="74106-123">Note that the less than sign (`<`) in the `ConditionScript` attribute must be escaped ().</span></span> <span data-ttu-id="74106-124">Při spuštění tohoto skriptu, buď žádná spuštění animace, nebo jeden z nich nemá, nebo obě.</span><span class="sxs-lookup"><span data-stu-id="74106-124">When you run this script, either no animation runs, or one of the two does, or both do.</span></span>


[![T<span data-ttu-id="74106-125">he panel je mizení bez změny velikosti, takže druhého spuštění animace, první z nich nebyl]</span><span class="sxs-lookup"><span data-stu-id="74106-125">he panel is fading out without resizing, so the second animation runs, the first one didn't]</span></span>(animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

<span data-ttu-id="74106-126">Je panelu mizení bez změny velikosti, takže druhého spuštění animace, první z nich nebyl ([kliknutím ji zobrazíte obrázek v plné velikosti](animation-depending-on-a-condition-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="74106-126">The panel is fading out without resizing, so the second animation runs, the first one didn't ([Click to view full-size image](animation-depending-on-a-condition-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="74106-127">[Předchozí](executing-several-animations-after-each-other-cs.md)
> [další](picking-one-animation-out-of-a-list-cs.md)</span><span class="sxs-lookup"><span data-stu-id="74106-127">[Previous](executing-several-animations-after-each-other-cs.md)
[Next](picking-one-animation-out-of-a-list-cs.md)</span></span>
