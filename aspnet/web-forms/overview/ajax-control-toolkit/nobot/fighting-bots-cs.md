---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: Boj s roboty (C#) | Dokumentace Microsoftu
author: wenz
description: Automatizované robotů sádra webové protokoly a další weby s nevyžádanou poštou, odesílání formulářů komentář bez nutnosti zásahu uživatele. Ovládací prvek NoBot v Con technologie ASP.NET AJAX...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: 178d839f67d70670b3b5acf470acb7ae8cf1c33f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59405804"
---
# <a name="fighting-bots-c"></a><span data-ttu-id="4934a-104">Boj s roboty (C#)</span><span class="sxs-lookup"><span data-stu-id="4934a-104">Fighting Bots (C#)</span></span>

<span data-ttu-id="4934a-105">by [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4934a-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4934a-106">[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) nebo [stahovat PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4934a-106">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)</span></span>

> <span data-ttu-id="4934a-107">Automatizované robotů sádra webové protokoly a další weby s nevyžádanou poštou, odesílání formulářů komentář bez nutnosti zásahu uživatele.</span><span class="sxs-lookup"><span data-stu-id="4934a-107">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="4934a-108">Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může pomoct bojují těchto robotů.</span><span class="sxs-lookup"><span data-stu-id="4934a-108">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>


## <a name="overview"></a><span data-ttu-id="4934a-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="4934a-109">Overview</span></span>

<span data-ttu-id="4934a-110">Automatizované robotů sádra webové protokoly a další weby s nevyžádanou poštou, odesílání formulářů komentář bez nutnosti zásahu uživatele.</span><span class="sxs-lookup"><span data-stu-id="4934a-110">Automated bots plaster weblogs and other websites with spam, submitting comment forms without any user interaction.</span></span> <span data-ttu-id="4934a-111">Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může pomoct bojují těchto robotů.</span><span class="sxs-lookup"><span data-stu-id="4934a-111">The NoBot control in the ASP.NET AJAX Control Toolkit can help fight those bots.</span></span>

## <a name="steps"></a><span data-ttu-id="4934a-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="4934a-112">Steps</span></span>

<span data-ttu-id="4934a-113">Jeden běžný postup, se kterými porazíte robotů je použití CAPTCHAs zcela automatizovat veřejné Turing test zjistit počítače a od sebe lidí.</span><span class="sxs-lookup"><span data-stu-id="4934a-113">One common approach to defeat bots is to use CAPTCHAs Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="4934a-114">Turing test byl původně test kde někdo museli rozhodovat, jestli je partnerem komunikace člověk nebo počítač.</span><span class="sxs-lookup"><span data-stu-id="4934a-114">A Turing test was originally a test where someone needed to decide whether a communication partner is a human or a machine.</span></span> <span data-ttu-id="4934a-115">Na webu testu CAPTCHA obvykle obsahuje bitovou kopii s některé zkreslený písmena v něm.</span><span class="sxs-lookup"><span data-stu-id="4934a-115">In the web, a CAPTCHA usually consists of an image with some distorted letters on it.</span></span> <span data-ttu-id="4934a-116">Cílem je, že může číst pouze lidských písmena v imagi, zatímco OCR algoritmy se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="4934a-116">The idea is that only a human can read the letters on the image, whereas OCR algorithms will fail.</span></span>

<span data-ttu-id="4934a-117">Existuje několik výhod a nevýhod tohoto přístupu diskusi o to je však nad rámec tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="4934a-117">There are several advantages and disadvantages to this approach, but a discussion of this is beyond the scope of this tutorial.</span></span> <span data-ttu-id="4934a-118">Je však ovládacího prvku v ASP.NET AJAX Control Toolkit, který nabízí podobný přístup: `NoBot`.</span><span class="sxs-lookup"><span data-stu-id="4934a-118">There is however a control in the ASP.NET AJAX Control Toolkit which provides a similar approach: `NoBot`.</span></span> <span data-ttu-id="4934a-119">Je snazší překonat než testu CAPTCHA, ale je velmi snadno používá a tarify velmi dobře ve službě websites jako blogy, kde bude považován za úspěšné Pokud většinu nevyžádané pošty pokusy jsou zrušena, což `NoBot` ovládacího prvku můžete provést.</span><span class="sxs-lookup"><span data-stu-id="4934a-119">It is easier to overcome than a CAPTCHA, but is very easy to use and fares extremely well on websites like blogs where it is considered a success if most spam attempts are defeated, which the `NoBot` control can do.</span></span>

`NoBot` <span data-ttu-id="4934a-120">zachycuje postback aktuální webové formuláře ASP.NET, pokud je splněna alespoň jedna z těchto podmínek:</span><span class="sxs-lookup"><span data-stu-id="4934a-120">intercepts the postback of the current ASP.NET web form if at least one of these conditions is met:</span></span>

- <span data-ttu-id="4934a-121">Prohlížeči nepodaří vyřešit díl stavebnice JavaScript (například při deaktivaci JavaScript)</span><span class="sxs-lookup"><span data-stu-id="4934a-121">The browser fails to solve a JavaScript puzzle (for instance when JavaScript is deactivated)</span></span>
- <span data-ttu-id="4934a-122">Formulář pro rychlé odeslané uživatele</span><span class="sxs-lookup"><span data-stu-id="4934a-122">The user submitted the form to fast</span></span>
- <span data-ttu-id="4934a-123">IP adresa klienta odeslání formuláře příliš často v určitou dobu.</span><span class="sxs-lookup"><span data-stu-id="4934a-123">The client IP address submitted the form too often in a certain period of time.</span></span>

<span data-ttu-id="4934a-124">Za účelem ověření pro tyto podmínky `NoBot` ovládací prvek požaduje tyto atributy (všechny z nich volitelný):</span><span class="sxs-lookup"><span data-stu-id="4934a-124">In order to check for these conditions, the `NoBot` control requires these attributes (all of them optional):</span></span>

- `ResponseMinimumDelaySeconds` <span data-ttu-id="4934a-125">minimální velikost sady sekund mezi jednotlivými zpětnými odesláními</span><span class="sxs-lookup"><span data-stu-id="4934a-125">minimum amount of seconds between postbacks</span></span>
- `CutoffWindowSeconds` <span data-ttu-id="4934a-126">Délka Časový interval, ve kterém jsou postbacků extenderu jedna IP adresa míry</span><span class="sxs-lookup"><span data-stu-id="4934a-126">length of time interval in which postbacks from one IP are measures</span></span>
- `CutoffMaximumInstances` <span data-ttu-id="4934a-127">maximální velikost sady sekund na časový interval</span><span class="sxs-lookup"><span data-stu-id="4934a-127">maximum amount of seconds per time interval</span></span>

<span data-ttu-id="4934a-128">Následující kód požadavky tohoto aspoň 2 sekundy uplynout mezi jednotlivými zpětnými odesláními a, které existují pouze pět zpětného odeslání nebo nižší v rámci intervalu 30 sekund:</span><span class="sxs-lookup"><span data-stu-id="4934a-128">The following markup demands that at least two seconds elapse between postbacks and that there are only five postbacks or less within a 30 seconds interval:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

<span data-ttu-id="4934a-129">Potom jako obvykle, nezapomeňte zahrnout `ScriptManager` na stránce tak, aby je načtena knihovna ASP.NET AJAX a Control Toolkit je možné:</span><span class="sxs-lookup"><span data-stu-id="4934a-129">Then as usual make sure to include the `ScriptManager` in the page so that the ASP.NET AJAX library is loaded and the Control Toolkit can be used:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

<span data-ttu-id="4934a-130">Protože většina kontrol `NoBot` dělá dojít na straně serveru, je potřeba zkontrolovat výsledek tyto ověření.</span><span class="sxs-lookup"><span data-stu-id="4934a-130">Since most of the checks `NoBot` is doing occur on the server side, you need to check the result of these validations.</span></span> <span data-ttu-id="4934a-131">To lze provést zavoláním `NoBot`společnosti `IsValid()` metody.</span><span class="sxs-lookup"><span data-stu-id="4934a-131">This can be done by calling `NoBot`'s `IsValid()` method.</span></span> <span data-ttu-id="4934a-132">Má jeden argument (jako `out` parametr /`ByRef` parametrů) typu `NoBotState`.</span><span class="sxs-lookup"><span data-stu-id="4934a-132">It has one argument (as an `out` parameter/`ByRef` parameter) which is of type `NoBotState`.</span></span> <span data-ttu-id="4934a-133">Řetězcové vyjádření obsahuje příčinu selhání kontroly a `Valid` jinak.</span><span class="sxs-lookup"><span data-stu-id="4934a-133">Its string representation contains the reason when the check fails and `Valid` otherwise.</span></span> <span data-ttu-id="4934a-134">Následující kód vracel zprávu podle `NoBot`je výsledek:</span><span class="sxs-lookup"><span data-stu-id="4934a-134">The following code outputs a message according to `NoBot`'s result:</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

<span data-ttu-id="4934a-135">Nakonec musíte formuláře pro odeslání a prvku popisku na výstup zprávu, a vy budete hotovi!</span><span class="sxs-lookup"><span data-stu-id="4934a-135">Finally, you need a form to submit and a label element to output the message, and you are done!</span></span>

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

<span data-ttu-id="4934a-136">Při spouštění tohoto skriptu a deaktivovat JavaScript nebo odesláním formuláře v prvních dvou sekund nebo odesláním formuláře sedminásobně během 30 sekund, zobrazí se chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="4934a-136">When you run this script and deactivate JavaScript or submit the form within the first two seconds or submit the form seven times within thirty seconds, you will get an error message.</span></span> <span data-ttu-id="4934a-137">Ale pomocí tohoto ovládacího prvku obezřetně, protože pouze 90 95 % uživatelé mít JavaScript aktivovat, proto se nezdaří % 5 až 10 uživatelů `NoBot`v testu.</span><span class="sxs-lookup"><span data-stu-id="4934a-137">However use this control wisely, since only about 90-95% of users have JavaScript activated, therefore 5-10% of users will fail `NoBot`'s test.</span></span>


[![T<span data-ttu-id="4934a-138">jeho chybová zpráva by mohla být způsobena robota]</span><span class="sxs-lookup"><span data-stu-id="4934a-138">his error message could have been caused by a bot]</span></span>(fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

<span data-ttu-id="4934a-139">Tato chybová zpráva by mohla být způsobena robota ([kliknutím ji zobrazíte obrázek v plné velikosti](fighting-bots-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4934a-139">This error message could have been caused by a bot ([Click to view full-size image](fighting-bots-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4934a-140">Next</span><span class="sxs-lookup"><span data-stu-id="4934a-140">Next</span></span>](fighting-bots-vb.md)
