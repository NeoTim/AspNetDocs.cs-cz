---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: Pomocí ovládacích prvků AJAX Control Toolkit ovládacích prvků a extenderů (C#) | Dokumentace Microsoftu
author: microsoft
description: Informace o přidání ovládacích prvků AJAX Control Toolkit a zařízení Extender na stránky ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 82fae91e40ec2f1508fe5c82992eeef4abc4e19a
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419220"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a><span data-ttu-id="5f540-103">Použití ovládacích prvků a rozšiřujících ovládacích prvků AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="5f540-103">Using AJAX Control Toolkit Controls and Control Extenders (C#)</span></span>

<span data-ttu-id="5f540-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5f540-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5f540-105">Informace o přidání ovládacích prvků AJAX Control Toolkit a zařízení Extender na stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f540-105">Learn how to add AJAX Control Toolkit controls and extenders to your ASP.NET pages.</span></span>


<span data-ttu-id="5f540-106">Sada nástrojů AJAX Control Toolkit obsahuje sadu ovládacích prvků a extenderů ovládacích prvků.</span><span class="sxs-lookup"><span data-stu-id="5f540-106">The AJAX Control Toolkit contains a set of controls and control extenders.</span></span> <span data-ttu-id="5f540-107">V tomto kurzu (BRIEF) se dozvíte, jak přidat ovládací prvky a ovládací prvek extenderů ke stránce ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f540-107">In this brief tutorial, you learn how to add both controls and control extenders to an ASP.NET page.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5f540-108">Pokyny k instalaci sadou nástrojů AJAX Control Toolkit a sadou nástrojů AJAX Control Toolkit přidává do panelu nástrojů Visual Studio nebo Visual Web Developer naleznete v kurzu [Začínáme se sadou nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span><span class="sxs-lookup"><span data-stu-id="5f540-108">For instructions on installing the AJAX Control Toolkit and adding the AJAX Control Toolkit to the Visual Studio/Visual Web Developer toolbox, see the tutorial [Get Started with the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).</span></span>


## <a name="using-ajax-control-toolkit-controls"></a><span data-ttu-id="5f540-109">Pomocí ovládacích prvků AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="5f540-109">Using AJAX Control Toolkit Controls</span></span>

<span data-ttu-id="5f540-110">Ovládací prvek AJAX Control Toolkit funguje stejně jako normální ovládací prvek technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f540-110">An AJAX Control Toolkit control works just like a normal ASP.NET control.</span></span> <span data-ttu-id="5f540-111">Přetáhněte ovládací prvek z panelu nástrojů na stránce ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f540-111">You can drag the control from the toolbox onto an ASP.NET page.</span></span> <span data-ttu-id="5f540-112">Přidejte ovládací prvek na stránce v zobrazení návrhu nebo v zobrazení zdroje.</span><span class="sxs-lookup"><span data-stu-id="5f540-112">You can add the control to the page in either Design view or Source view.</span></span>

<span data-ttu-id="5f540-113">Jestli používáte ovládací prvky z sadou nástrojů AJAX Control Toolkit je speciální požadavků.</span><span class="sxs-lookup"><span data-stu-id="5f540-113">There is one special requirement when using the controls from the AJAX Control Toolkit.</span></span> <span data-ttu-id="5f540-114">Stránka musí obsahovat ovládací prvek ScriptManager.</span><span class="sxs-lookup"><span data-stu-id="5f540-114">The page must contain a ScriptManager control.</span></span> <span data-ttu-id="5f540-115">Ovládací prvek ScriptManager je zodpovědná za všechny nezbytné JavaScript vyžaduje ovládacích prvků AJAX Control Toolkit včetně.</span><span class="sxs-lookup"><span data-stu-id="5f540-115">The ScriptManager control is responsible for including all of the necessary JavaScript required by the AJAX Control Toolkit controls.</span></span>

<span data-ttu-id="5f540-116">Například karta sada nástrojů AJAX Control Toolkit obsahuje ovládací prvek s názvem ovládací prvek editoru.</span><span class="sxs-lookup"><span data-stu-id="5f540-116">For example, the AJAX Control Toolkit tab includes a control named the Editor control.</span></span> <span data-ttu-id="5f540-117">Tento ovládací prvek zobrazuje bohaté možnosti editoru jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="5f540-117">This control displays a rich HTML editor.</span></span> <span data-ttu-id="5f540-118">Postupujte podle těchto kroků přidejte ovládací prvek editoru na stránku:</span><span class="sxs-lookup"><span data-stu-id="5f540-118">Follow these steps to add the Editor control to a page:</span></span>

1. <span data-ttu-id="5f540-119">Vytvořit novou stránku ASP.NET s názvem ShowEditor.aspx</span><span class="sxs-lookup"><span data-stu-id="5f540-119">Create a new ASP.NET page named ShowEditor.aspx</span></span>
2. <span data-ttu-id="5f540-120">Vyberte ovládací prvek ScriptManager from beneath na kartě Rozšíření AJAX v sadě nástrojů a přetáhněte ovládací prvek na stránce.</span><span class="sxs-lookup"><span data-stu-id="5f540-120">Select the ScriptManager control from beneath the AJAX Extensions tab in the toolbox and drag the control onto the page.</span></span>
3. <span data-ttu-id="5f540-121">Vyberte ovládací prvek editoru from beneath sadou nástrojů AJAX Control Toolkit kartu na panelu nástrojů a přetáhněte ovládací prvek na stránce (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="5f540-121">Select the Editor control from beneath the AJAX Control Toolkit tab in the toolbox and drag the control onto the page (see Figure 1).</span></span> <span data-ttu-id="5f540-122">Návrhář by měl vypadat jako na obrázku 2.</span><span class="sxs-lookup"><span data-stu-id="5f540-122">The Designer should look like Figure 2.</span></span>
4. <span data-ttu-id="5f540-123">Spustit web tak, že vyberete možnost nabídky **ladit, spustit ladění** nebo stisknutí klávesy F5.</span><span class="sxs-lookup"><span data-stu-id="5f540-123">Run the web site by selecting the menu option **Debug, Start Debugging** or hitting the F5 key.</span></span>
5. <span data-ttu-id="5f540-124">Měli byste vidět stránku na obrázku 3.</span><span class="sxs-lookup"><span data-stu-id="5f540-124">You should see the page in Figure 3.</span></span>


[![S<span data-ttu-id="5f540-125">jak zvolit ovládací prvek editoru HTML]</span><span class="sxs-lookup"><span data-stu-id="5f540-125">electing the HTML Editor control]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

<span data-ttu-id="5f540-126">**Obrázek 01**: Vyberte ovládací prvek editoru HTML ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-126">**Figure 01**: Selecting the HTML Editor control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))</span></span>


[![V<span data-ttu-id="5f540-127">Visual Studio návrháře ovládacímu prvku ScriptManager a úpravy]</span><span class="sxs-lookup"><span data-stu-id="5f540-127">isual Studio Designer with ScriptManager and Edit control]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

<span data-ttu-id="5f540-128">**Obrázek 02**: Návrhář Visual Studio ovládacímu prvku ScriptManager a úpravy ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-128">**Figure 02**: Visual Studio Designer with ScriptManager and Edit control([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))</span></span>


[![T<span data-ttu-id="5f540-129">stránka DisplayEditor.aspx he]</span><span class="sxs-lookup"><span data-stu-id="5f540-129">he DisplayEditor.aspx page]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

<span data-ttu-id="5f540-130">**Obrázek 03**: Na stránce DisplayEditor.aspx ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-130">**Figure 03**: The DisplayEditor.aspx page([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))</span></span>


## <a name="using-ajax-control-toolkit-control-extenders"></a><span data-ttu-id="5f540-131">Použití jazyka AJAX Toolkit ovládací prvek extenderů</span><span class="sxs-lookup"><span data-stu-id="5f540-131">Using AJAX Control Toolkit Control Extenders</span></span>

<span data-ttu-id="5f540-132">Sada nástrojů AJAX Control Toolkit obsahuje také ovládací prvek extenderů.</span><span class="sxs-lookup"><span data-stu-id="5f540-132">The AJAX Control Toolkit also contains control extenders.</span></span> <span data-ttu-id="5f540-133">Jak název napovídá, – extender ovládacího prvku rozšiřuje funkce existujícího ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="5f540-133">As its name suggests, a control extender extends the functionality of an existing control.</span></span> <span data-ttu-id="5f540-134">Například zařízení extender ConfirmButton ovládací prvek rozšiřuje standardní ovládací prvek tlačítko technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5f540-134">For example, the ConfirmButton control extender extends the standard ASP.NET Button control.</span></span> <span data-ttu-id="5f540-135">Zařízení extender změní chování s ovládací prvek tlačítka tak, aby na tomto tlačítku zobrazí potvrzovací dialogové okno po kliknutí.</span><span class="sxs-lookup"><span data-stu-id="5f540-135">The extender changes the Button control�s behavior so that the Button displays a confirmation dialog when you click it.</span></span>

<span data-ttu-id="5f540-136">Extender ovládacího prvku, stejně jako ovládací prvek AJAX Control Toolkit vyžaduje ovládací prvek ScriptManager.</span><span class="sxs-lookup"><span data-stu-id="5f540-136">A control extender, just like an AJAX Control Toolkit control, requires a ScriptManager control.</span></span> <span data-ttu-id="5f540-137">Než začnete používat ovládací prvek extenderů na stránce, musíte přidat ovládací prvek ScriptManager na stránku.</span><span class="sxs-lookup"><span data-stu-id="5f540-137">You must add a ScriptManager control to a page before you start using control extenders in the page.</span></span>

<span data-ttu-id="5f540-138">Následujícím postupem použít zařízení extender ConfirmButton ovládacího prvku:</span><span class="sxs-lookup"><span data-stu-id="5f540-138">Follow these steps to use the ConfirmButton control extender:</span></span>

1. <span data-ttu-id="5f540-139">Vytvořit novou stránku ASP.NET s názvem ShowConfirmButton.aspx</span><span class="sxs-lookup"><span data-stu-id="5f540-139">Create a new ASP.NET page named ShowConfirmButton.aspx</span></span>
2. <span data-ttu-id="5f540-140">Přidání ovládacího prvku ScriptManager na stránce přetažením ovládací prvek na stránce from beneath na kartě Rozšíření AJAX.</span><span class="sxs-lookup"><span data-stu-id="5f540-140">Add a ScriptManager control to the page by dragging the control onto the page from beneath the AJAX Extensions tab.</span></span>
3. <span data-ttu-id="5f540-141">Přidejte ovládací prvek standardní tlačítko na stránce přetažením tlačítko from beneath standardní kartu na panelu nástrojů na plochu návrháře.</span><span class="sxs-lookup"><span data-stu-id="5f540-141">Add a standard Button control to the page by dragging the Button from beneath the Standard tab in the toolbox onto the Designer surface.</span></span>
4. <span data-ttu-id="5f540-142">Klikněte na tlačítko **přidat zařízení Extender** úloh možnost (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="5f540-142">Click the **Add Extender** task option (see Figure 4).</span></span>
5. <span data-ttu-id="5f540-143">V dialogovém okně Zvolit rozšíření vyberte ConfirmButtonExtender (viz obrázek 5) a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="5f540-143">In the Choose Extender dialog, select ConfirmButtonExtender (see Figure 5) and click the OK button.</span></span>
6. <span data-ttu-id="5f540-144">Vyberte ovládací prvek tlačítko v návrháři a rozbalte zařízení Extender Button1\_ConfirmButtonExtender uzel v okně Vlastnosti (viz obrázek 6).</span><span class="sxs-lookup"><span data-stu-id="5f540-144">Select the Button control in the Designer and expand the Extenders, Button1\_ConfirmButtonExtender node in the Properties window (see Figure 6).</span></span> <span data-ttu-id="5f540-145">Přiřaďte hodnotu *skutečně?* ConfirmText vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5f540-145">Assign the value *�Really?�* to the ConfirmText property.</span></span>
7. <span data-ttu-id="5f540-146">Spuštění stránky tak, že vyberete možnost nabídky **ladit, spustit ladění** nebo stiskněte klávesu F5.</span><span class="sxs-lookup"><span data-stu-id="5f540-146">Run the page by selecting the menu option **Debug, Start Debugging** or hit the F5 key.</span></span>


[![T<span data-ttu-id="5f540-147">má možnost přidat rozšíření úloh]</span><span class="sxs-lookup"><span data-stu-id="5f540-147">he Add Extender task option]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

<span data-ttu-id="5f540-148">**Obrázek 04**: Možnost přidat rozšíření úlohy ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-148">**Figure 04**: The Add Extender task option([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))</span></span>


[![S<span data-ttu-id="5f540-149">jak zvolit – extender ConfirmButton ovládacího prvku]</span><span class="sxs-lookup"><span data-stu-id="5f540-149">electing the ConfirmButton control extender]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

<span data-ttu-id="5f540-150">**Obrázek 05**: Výběr zařízení extender ConfirmButton ovládacího prvku ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-150">**Figure 05**: Selecting the ConfirmButton control extender([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))</span></span>


[![S<span data-ttu-id="5f540-151">Vlastnost ConfirmButton černobílé]</span><span class="sxs-lookup"><span data-stu-id="5f540-151">etting a ConfirmButton property]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

<span data-ttu-id="5f540-152">**Obrázek 06**: Nastavení vlastnosti ConfirmButton ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-152">**Figure 06**: Setting a ConfirmButton property([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))</span></span>


<span data-ttu-id="5f540-153">Po otevření stránky, měli byste vidět tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5f540-153">When the page opens, you should see a button.</span></span> <span data-ttu-id="5f540-154">Až kliknete na tlačítko, zobrazí potvrzovací dialogové okno na obrázku 7.</span><span class="sxs-lookup"><span data-stu-id="5f540-154">When you click the button, you get the confirmation dialog in Figure 7.</span></span>


[![D<span data-ttu-id="5f540-155">Dialogové okno pro potvrzení isplaying]</span><span class="sxs-lookup"><span data-stu-id="5f540-155">isplaying the confirmation dialog]</span></span>(using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

<span data-ttu-id="5f540-156">**Obrázek 07**: Zobrazení dialogového okna potvrzení ([kliknutím ji zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="5f540-156">**Figure 07**: Displaying the confirmation dialog([Click to view full-size image](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))</span></span>


<span data-ttu-id="5f540-157">Všimněte si, že je obvykle není přetáhnout – extender ovládacího prvku na stránku.</span><span class="sxs-lookup"><span data-stu-id="5f540-157">Notice that you normally do not drag a control extender onto a page.</span></span> <span data-ttu-id="5f540-158">Místo toho použít **přidat zařízení Extender** úlohy přidat rozšiřující ovládací prvek, který jste už přidali na stránku.</span><span class="sxs-lookup"><span data-stu-id="5f540-158">Instead, you use the **Add Extender** task option to add an extender to a control that you have already added to a page.</span></span> <span data-ttu-id="5f540-159">Všimněte si kromě toho, že nastavíte ovládacího prvku vlastnosti rozšíření tak, že otevřete okno vlastností pro ovládací prvek se rozšiřuje.</span><span class="sxs-lookup"><span data-stu-id="5f540-159">Notice, furthermore, that you set control extender properties by opening the property sheet for the control being extended.</span></span>

<span data-ttu-id="5f540-160">Jeden ovládací prvek ASP.NET, je možné rozšířit pomocí více zařízení Extender ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="5f540-160">A single ASP.NET control can be extended by multiple control extenders.</span></span> <span data-ttu-id="5f540-161">Seznam vlastností pro ovládací prvek se rozšiřuje se zobrazí všechny ovládací prvek extenderů přidružený k ovládacímu prvku.</span><span class="sxs-lookup"><span data-stu-id="5f540-161">The property sheet for the control being extended will list all of the control extenders associated with the control.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5f540-162">[Předchozí](get-started-with-the-ajax-control-toolkit-cs.md)
> [další](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5f540-162">[Previous](get-started-with-the-ajax-control-toolkit-cs.md)
[Next](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)</span></span>
