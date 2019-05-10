---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: Použití ovládacího prvku DynamicPopulate s uživatelského ovládacího prvku a JavaScriptem (C#) | Dokumentace Microsoftu
author: wenz
description: ASP.NET AJAX Control Toolkit ovládacího prvku DynamicPopulate volání webové služby (nebo metodu stránky) a vyplní výsledné hodnoty do cílového ovládacího prvku na t...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 387cad748428249273cf9708b794dd8864cf982f
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125053"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a><span data-ttu-id="a45d3-103">Použití ovládacího prvku DynamicPopulate s uživatelským ovládacím prvkem a JavaScriptem (C#)</span><span class="sxs-lookup"><span data-stu-id="a45d3-103">Using DynamicPopulate with a User Control And JavaScript (C#)</span></span>

<span data-ttu-id="a45d3-104">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a45d3-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a45d3-105">[Stáhněte si kód](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a45d3-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)</span></span>

> <span data-ttu-id="a45d3-106">DynamicPopulate ovládacího prvku ASP.NET AJAX Control Toolkit volání webové služby (nebo metodu stránky) a zkopíruje výslednou hodnotu na cílový ovládací prvek na stránce bez aktualizace stránky.</span><span class="sxs-lookup"><span data-stu-id="a45d3-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="a45d3-107">Je také možné aktivovat naplnění psát vlastní kód JavaScript na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="a45d3-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="a45d3-108">Zvláštní pozornost má ale mají být provedeny, když zařízení extender se nachází v uživatelském ovládacím prvku.</span><span class="sxs-lookup"><span data-stu-id="a45d3-108">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="overview"></a><span data-ttu-id="a45d3-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="a45d3-109">Overview</span></span>

<span data-ttu-id="a45d3-110">`DynamicPopulate` Ovládacího prvku ASP.NET AJAX Control Toolkit volání webové služby (nebo metodu stránky) a zkopíruje výslednou hodnotu na cílový ovládací prvek na stránce bez aktualizace stránky.</span><span class="sxs-lookup"><span data-stu-id="a45d3-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="a45d3-111">Je také možné aktivovat naplnění psát vlastní kód JavaScript na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="a45d3-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="a45d3-112">Zvláštní pozornost má ale mají být provedeny, když zařízení extender se nachází v uživatelském ovládacím prvku.</span><span class="sxs-lookup"><span data-stu-id="a45d3-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="a45d3-113">Kroky</span><span class="sxs-lookup"><span data-stu-id="a45d3-113">Steps</span></span>

<span data-ttu-id="a45d3-114">Za prvé, třeba webové služby ASP.NET, která implementuje metodu, které jsou volány `DynamicPopulateExtender` ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a45d3-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="a45d3-115">Webová služba implementuje metodu `getDate()` , která očekává jeden argument typu řetězec, volá `contextKey`, protože `DynamicPopulate` ovládací prvek odešle jednu část informací o kontextu se každé volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="a45d3-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="a45d3-116">Zde je kód (soubor `DynamicPopulate.cs.asmx`) načte aktuální datum v jednom ze tří formátů:</span><span class="sxs-lookup"><span data-stu-id="a45d3-116">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="a45d3-117">V dalším kroku vytvoření nového uživatelského ovládacího prvku (`.ascx` souboru), označen následující deklarace v jeho první řádek:</span><span class="sxs-lookup"><span data-stu-id="a45d3-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="a45d3-118">A &lt; `label` &gt; element se použije k zobrazení dat pocházejících ze serveru.</span><span class="sxs-lookup"><span data-stu-id="a45d3-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

<span data-ttu-id="a45d3-119">V souboru uživatelského ovládacího prvku, jsme také pomocí přepínačů tři, každý z nich představuje jednu ze tří možných datum formátů podporovaných webovou službu.</span><span class="sxs-lookup"><span data-stu-id="a45d3-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="a45d3-120">Když uživatel klikne na jednom z přepínačů, prohlížeč provede kód jazyka JavaScript, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="a45d3-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

<span data-ttu-id="a45d3-121">Tento kód přistupuje k `DynamicPopulateExtender` (Nedělejte si starosti o neobvyklé ID ale to se budeme dále) a aktivuje dynamické naplnění daty.</span><span class="sxs-lookup"><span data-stu-id="a45d3-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="a45d3-122">V rámci aktuální přepínač `this.value` odkazuje na jeho hodnotu, která je `format1`, `format2` nebo `format3` přesně co metodu webové očekává.</span><span class="sxs-lookup"><span data-stu-id="a45d3-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="a45d3-123">Jediné, co chybí v prvku uživatel zatím je `DynamicPopulateExtender` ovládací prvek, který odkazuje přepínačů k webové službě.</span><span class="sxs-lookup"><span data-stu-id="a45d3-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="a45d3-124">Může znovu nezapomeňte strangeová ID používané v ovládacím prvku: `mcd1$myDate` místo `myDate`.</span><span class="sxs-lookup"><span data-stu-id="a45d3-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="a45d3-125">Dříve, kód jazyka JavaScript používaný `mcd1_dpe1` přístup `DynamicPopulateExtender` místo `dpe1`. Tato strategie vytváření názvů je zvláštní požadavek při použití `DynamicPopulateExtender` v rámci uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a45d3-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="a45d3-126">Kromě toho budete muset vložit uživatelského ovládacího prvku určitým způsobem, aby to fungovalo.</span><span class="sxs-lookup"><span data-stu-id="a45d3-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="a45d3-127">Vytvoření nové stránky technologie ASP.NET a zaregistrujte předponu značky uživatelského ovládacího prvku, který jste právě implementovali:</span><span class="sxs-lookup"><span data-stu-id="a45d3-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

<span data-ttu-id="a45d3-128">Pak musíte uvést technologie ASP.NET AJAX `ScriptManager` ovládací prvek na nové stránce:</span><span class="sxs-lookup"><span data-stu-id="a45d3-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

<span data-ttu-id="a45d3-129">Nakonec přidejte uživatelský ovládací prvek na stránce.</span><span class="sxs-lookup"><span data-stu-id="a45d3-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="a45d3-130">Budete muset nastavit jeho `ID` atribut (a `runat="server"`, samozřejmě), ale budete muset nastavit na konkrétní název: `mcd1` vzhledem k tomu, že toto je předpona používaná pro přístup k ní pomocí jazyka JavaScript v rámci uživatelského ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="a45d3-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

<span data-ttu-id="a45d3-131">A to je všechno!</span><span class="sxs-lookup"><span data-stu-id="a45d3-131">And that's it!</span></span> <span data-ttu-id="a45d3-132">Na stránce se chová podle očekávání: Uživatel klikne na jednom z přepínačů, ovládací prvek v sadě nástrojů volat webovou službu a zobrazí aktuální datum v požadovaném formátu.</span><span class="sxs-lookup"><span data-stu-id="a45d3-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>

<span data-ttu-id="a45d3-133">[![Přepínací tlačítka jsou umístěny do uživatelského ovládacího prvku](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a45d3-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="a45d3-134">Přepínací tlačítka jsou umístěny do uživatelského ovládacího prvku ([kliknutím ji zobrazíte obrázek v plné velikosti](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="a45d3-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a45d3-135">[Předchozí](dynamically-populating-a-control-using-javascript-code-cs.md)
> [další](dynamically-populating-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a45d3-135">[Previous](dynamically-populating-a-control-using-javascript-code-cs.md)
[Next](dynamically-populating-a-control-vb.md)</span></span>
