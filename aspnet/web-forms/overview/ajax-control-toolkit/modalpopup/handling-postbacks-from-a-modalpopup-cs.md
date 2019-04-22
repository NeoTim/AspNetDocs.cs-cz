---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: Zpracování postbacků z ovládacího prvku ModalPopup (C#) | Dokumentace Microsoftu
author: wenz
description: Ovládací prvek ovládacího prvku ModalPopup v sadou nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální místní nabídky pomocí znamená, že na straně klienta. Zvláštní pozornost musí být provedeny, když pos...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 54dd3bae21e661e0b17cab6a71f0df33b6712bcd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59388553"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a><span data-ttu-id="42e00-104">Zpracování postbacků z ovládacího prvku ModalPopup (C#)</span><span class="sxs-lookup"><span data-stu-id="42e00-104">Handling Postbacks from a ModalPopup (C#)</span></span>

<span data-ttu-id="42e00-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="42e00-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="42e00-106">[Stáhněte si kód](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="42e00-106">[Download Code](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)</span></span>

> <span data-ttu-id="42e00-107">Ovládací prvek ovládacího prvku ModalPopup v sadou nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální místní nabídky pomocí znamená, že na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="42e00-107">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="42e00-108">Při zpětném odeslání z rozbalené, musí být přijata zvláštní pozornost.</span><span class="sxs-lookup"><span data-stu-id="42e00-108">Special care must be taken when a postback is created from within the popup.</span></span>


## <a name="overview"></a><span data-ttu-id="42e00-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="42e00-109">Overview</span></span>

<span data-ttu-id="42e00-110">Ovládací prvek ovládacího prvku ModalPopup v sadou nástrojů AJAX Control Toolkit nabízí jednoduchý způsob, jak vytvořit modální místní nabídky pomocí znamená, že na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="42e00-110">The ModalPopup control in the AJAX Control Toolkit offers a simple way to create a modal popup using client-side means.</span></span> <span data-ttu-id="42e00-111">Při zpětném odeslání z rozbalené, musí být přijata zvláštní pozornost.</span><span class="sxs-lookup"><span data-stu-id="42e00-111">Special care must be taken when a postback is created from within the popup.</span></span>

## <a name="steps"></a><span data-ttu-id="42e00-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="42e00-112">Steps</span></span>

<span data-ttu-id="42e00-113">K aktivaci funkce technologie ASP.NET AJAX a Control Toolkit `ScriptManager` ovládací prvek je třeba umístit kdekoli na stránce (ale v rámci `<form>` element):</span><span class="sxs-lookup"><span data-stu-id="42e00-113">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the `<form>` element):</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

<span data-ttu-id="42e00-114">V dalším kroku přidáte panel, který slouží jako modální místní nabídky.</span><span class="sxs-lookup"><span data-stu-id="42e00-114">Next, add a panel which serves as the modal popup.</span></span> <span data-ttu-id="42e00-115">Uživatel může existuje, zadejte název a e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="42e00-115">There, the user can enter a name and an email address.</span></span> <span data-ttu-id="42e00-116">Tlačítko slouží k automaticky otevírané okno zavřete a uložte informace.</span><span class="sxs-lookup"><span data-stu-id="42e00-116">A button is used to close the popup and save the information.</span></span> <span data-ttu-id="42e00-117">Všimněte si, `OnClick` atribut je nastaven tak, aby zpětné odeslání vyvolá se při kliknutí na toto tlačítko:</span><span class="sxs-lookup"><span data-stu-id="42e00-117">Note that the `OnClick` attribute is set so that a postback occurs when this button is clicked:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

<span data-ttu-id="42e00-118">Samotná stránka se skládá ze dvou popisků stejné informace: jméno a e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="42e00-118">The page itself consists of two labels for exactly the same information: name and email address.</span></span> <span data-ttu-id="42e00-119">Tlačítko se používá k aktivaci Modální místní nabídky:</span><span class="sxs-lookup"><span data-stu-id="42e00-119">A button is used to trigger the modal popup:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

<span data-ttu-id="42e00-120">Aby bylo možné automaticky otevírané okno se zobrazí, přidejte `ModalPopupExtender` ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="42e00-120">In order to make the popup appear, add the `ModalPopupExtender` control.</span></span> <span data-ttu-id="42e00-121">Nastavte `PopupControlID` atribut ID v panelu a `TargetControlID` ID tlačítka:</span><span class="sxs-lookup"><span data-stu-id="42e00-121">Set the `PopupControlID` attribute to the panel's ID and `TargetControlID` to the button's ID:</span></span>

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

<span data-ttu-id="42e00-122">Nyní pokaždé, když `Save` je stisknuto tlačítko Modální místní nabídky, server-side `SaveData()` provedení metody.</span><span class="sxs-lookup"><span data-stu-id="42e00-122">Now whenever the `Save` button within the modal popup is clicked, the server-side `SaveData()` method is executed.</span></span> <span data-ttu-id="42e00-123">V úložišti dat, můžete ušetřit zadané údaje.</span><span class="sxs-lookup"><span data-stu-id="42e00-123">There, you could save the entered data in a data store.</span></span> <span data-ttu-id="42e00-124">Z důvodu zjednodušení nová data jenom výstup v popisku:</span><span class="sxs-lookup"><span data-stu-id="42e00-124">For the sake of simplicity, the new data is just output in the label:</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

<span data-ttu-id="42e00-125">TextBox – ovládací prvky v rámci Modální místní nabídky by měl být také, zaplněny aktuální jméno a e-mailu.</span><span class="sxs-lookup"><span data-stu-id="42e00-125">Also, the textbox controls within the modal popup should be filled with the current name and email.</span></span> <span data-ttu-id="42e00-126">Ale to je nutné pouze dojde bez zpětného odeslání.</span><span class="sxs-lookup"><span data-stu-id="42e00-126">However this is only necessary when no postback occurs.</span></span> <span data-ttu-id="42e00-127">Pokud je zpětné volání, funkce stav zobrazení ASP.NET automaticky vyplnit textová pole s příslušnými hodnotami.</span><span class="sxs-lookup"><span data-stu-id="42e00-127">If there is a postback, the ASP.NET viewstate feature will automatically fill the textboxes with the appropriate values.</span></span>

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]


<span data-ttu-id="42e00-128">[![Vyvolá Modální místní nabídky zpětné volání](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="42e00-128">[![The modal popup causes a postback](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)</span></span>

<span data-ttu-id="42e00-129">Vyvolá Modální místní nabídky zpětné volání ([kliknutím ji zobrazíte obrázek v plné velikosti](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="42e00-129">The modal popup causes a postback ([Click to view full-size image](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="42e00-130">[Předchozí](using-modalpopup-with-a-repeater-control-cs.md)
> [další](positioning-a-modalpopup-cs.md)</span><span class="sxs-lookup"><span data-stu-id="42e00-130">[Previous](using-modalpopup-with-a-repeater-control-cs.md)
[Next](positioning-a-modalpopup-cs.md)</span></span>
