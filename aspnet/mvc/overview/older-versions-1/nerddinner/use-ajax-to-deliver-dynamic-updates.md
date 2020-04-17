---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Použití ajaxu k doručování dynamických aktualizací | Dokumenty společnosti Microsoft
author: rick-anderson
description: Krok 10 implementuje podporu pro přihlášené uživatele, aby RSVP jejich zájem o účast na večeři, pomocí Ajax-založený přístup integrovaný do detailu večeře ...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 13680b91edc665852fd4af56e4fc79551e6de15e
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541244"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="af2f2-103">Použití jazyka AJAX k dynamickým aktualizacím</span><span class="sxs-lookup"><span data-stu-id="af2f2-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="af2f2-104">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="af2f2-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="af2f2-105">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="af2f2-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="af2f2-106">Toto je krok 10 zdarma ["NerdDinner" aplikační kurz,](introducing-the-nerddinner-tutorial.md) který prochází, jak vytvořit malé, ale kompletní, webové aplikace pomocí ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="af2f2-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="af2f2-107">Krok 10 implementuje podporu pro přihlášené uživatele, aby rsvp jejich zájem o účast na večeři, pomocí Přístup založený na Ajax integrované do stránky podrobnosti o večeři.</span><span class="sxs-lookup"><span data-stu-id="af2f2-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="af2f2-108">Pokud používáte ASP.NET MVC 3, doporučujeme postupovat podle kurzů [Začínáme s MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo [MVC Music Store.](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="af2f2-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="af2f2-109">NerdDinner Krok 10: AJAX Povolení RSVPs přijímá</span><span class="sxs-lookup"><span data-stu-id="af2f2-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="af2f2-110">Nyní implementujeme podporu přihlášených uživatelů, abychom odpověděli na jejich zájem o účast na večeři.</span><span class="sxs-lookup"><span data-stu-id="af2f2-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="af2f2-111">Umožníme to pomocí přístupu založeného na AJAXintegrovaném na stránce s podrobnostmi o večeři.</span><span class="sxs-lookup"><span data-stu-id="af2f2-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="af2f2-112">Označuje, zda je uživatel rsvp'd</span><span class="sxs-lookup"><span data-stu-id="af2f2-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="af2f2-113">Uživatelé mohou navštívit adresu URL */Dinners/Details/[id]* a zobrazit podrobnosti o konkrétní večeři:</span><span class="sxs-lookup"><span data-stu-id="af2f2-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="af2f2-114">Metoda akce Details() je implementována takto:</span><span class="sxs-lookup"><span data-stu-id="af2f2-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="af2f2-115">Náš první krok k implementaci podpory RSVP bude přidání "IsUserRegistered(uživatelské jméno)" pomocné metody naše Dinner objektu (v rámci Dinner.cs částečné třídy jsme vytvořili dříve).</span><span class="sxs-lookup"><span data-stu-id="af2f2-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="af2f2-116">Tato pomocná metoda vrátí true nebo false v závislosti na tom, zda je uživatel aktuálně rsvp'd pro večeři:</span><span class="sxs-lookup"><span data-stu-id="af2f2-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="af2f2-117">Do šablony zobrazení Details.aspx pak můžeme přidat následující kód, který zobrazí příslušnou zprávu s uvedením, zda je uživatel pro událost zaregistrován nebo ne:</span><span class="sxs-lookup"><span data-stu-id="af2f2-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="af2f2-118">A teď, když uživatel navštíví večeři, pro kterou je zaregistrován, zobrazí se tato zpráva:</span><span class="sxs-lookup"><span data-stu-id="af2f2-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="af2f2-119">A když navštíví večeři, nejsou registrovány pro uvidí níže zprávu:</span><span class="sxs-lookup"><span data-stu-id="af2f2-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="af2f2-120">Implementace metody akce registru</span><span class="sxs-lookup"><span data-stu-id="af2f2-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="af2f2-121">Nyní přidáme funkce nezbytné k tomu, aby uživatelé mohli na večeři z podrobností povolit uživatelům rsvp pro večeři.</span><span class="sxs-lookup"><span data-stu-id="af2f2-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="af2f2-122">Chcete-li tento problém implementovat, vytvoříme novou třídu "RSVPController" kliknutím pravým tlačítkem myši na adresář \Controllers a výběrem příkazu nabídky&gt;Přidat řadič.</span><span class="sxs-lookup"><span data-stu-id="af2f2-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="af2f2-123">Budeme implementovat "Register" metoda akce v rámci nové třídy RSVPController, která trvá id pro Večeři jako argument, načte příslušný Dinner objekt, zkontroluje, zda přihlášený uživatel je aktuálně v seznamu uživatelů, kteří se zaregistrovali pro něj, a pokud ne přidá RSVP objekt pro ně:</span><span class="sxs-lookup"><span data-stu-id="af2f2-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="af2f2-124">Všimněte si, jak vracíme jednoduchý řetězec jako výstup metody akce.</span><span class="sxs-lookup"><span data-stu-id="af2f2-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="af2f2-125">Mohli jsme vložit tuto zprávu do šablony zobrazení - ale protože je tak malá, použijeme pomocnou metodu Content() v základní třídě řadiče a vrátíme zprávu řetězce jako výše.</span><span class="sxs-lookup"><span data-stu-id="af2f2-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="af2f2-126">Volání metody akce RSVPForEvent pomocí metody AJAX</span><span class="sxs-lookup"><span data-stu-id="af2f2-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="af2f2-127">Použijeme AJAX k vyvolání metody akce Register z našeho zobrazení Podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="af2f2-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="af2f2-128">Implementace je to docela snadné.</span><span class="sxs-lookup"><span data-stu-id="af2f2-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="af2f2-129">Nejprve přidáme dva odkazy na knihovnu skriptů:</span><span class="sxs-lookup"><span data-stu-id="af2f2-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="af2f2-130">První knihovna odkazuje na základní ASP.NET knihovny skriptů na straně klienta AJAX.</span><span class="sxs-lookup"><span data-stu-id="af2f2-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="af2f2-131">Tento soubor má velikost přibližně 24 kB (komprimovaný) a obsahuje základní funkce AJAX na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="af2f2-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="af2f2-132">Druhá knihovna obsahuje užitné funkce, které se integrují s vestavěnými pomocnými metodami ASP.NET MVC AJAX (které budeme brzy používat).</span><span class="sxs-lookup"><span data-stu-id="af2f2-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="af2f2-133">Potom můžeme aktualizovat kód šablony zobrazení, který jsme přidali dříve, takže místo toho, abychom namísto vynětí zprávy "Nejste registrováni pro tuto událost", místo toho vykreslujeme odkaz, který při pushprovádí volání AJAX, které vyvolá naši metodu akce RSVPForEvent na našem řadiči RSVP a RSVP uživatele:</span><span class="sxs-lookup"><span data-stu-id="af2f2-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="af2f2-134">Ajax.ActionLink() pomocná metoda použitá výše je vestavěná do ASP.NET MVC a je podobná metodě pomocného zařízení Html.ActionLink() s tím rozdílem, že namísto provedení standardní navigace provede volání AJAX na metodu akce po klepnutí na odkaz.</span><span class="sxs-lookup"><span data-stu-id="af2f2-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="af2f2-135">Výše voláme metodu akce "Register" na řadiči "RSVP" a předáváme mu DinnerID jako parametr "id".</span><span class="sxs-lookup"><span data-stu-id="af2f2-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="af2f2-136">Konečný parametr AjaxOptions, který předáváme, naznačuje, že chceme vzít obsah &lt;&gt; vrácený z metody akce a aktualizovat element HTML div na stránce, jehož id je "rsvpmsg".</span><span class="sxs-lookup"><span data-stu-id="af2f2-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="af2f2-137">A teď, když uživatel přejde na večeři, pro kterou ještě není zaregistrován, zobrazí se mu odkaz na rsvp:</span><span class="sxs-lookup"><span data-stu-id="af2f2-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="af2f2-138">Pokud kliknou na odkaz "RSVP pro tuto událost", prodají volání AJAX metodě akce Register na kontroleru RSVP a po dokončení se jim zobrazí aktualizovaná zpráva jako níže:</span><span class="sxs-lookup"><span data-stu-id="af2f2-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="af2f2-139">Šířka pásma sítě a provoz zapojených při tomto volání AJAX je opravdu lehký.</span><span class="sxs-lookup"><span data-stu-id="af2f2-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="af2f2-140">Když uživatel klikne na odkaz "RSVP pro tuto událost", je malý požadavek na síť HTTP POST proveden na adresu URL */Dinners/Register/1,* která vypadá níže na lince:</span><span class="sxs-lookup"><span data-stu-id="af2f2-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="af2f2-141">A odpověď z naší metody Registrace akce je jednoduše:</span><span class="sxs-lookup"><span data-stu-id="af2f2-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="af2f2-142">Toto lehké volání je rychlé a bude fungovat i přes pomalou síť.</span><span class="sxs-lookup"><span data-stu-id="af2f2-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="af2f2-143">Přidání animace jQuery</span><span class="sxs-lookup"><span data-stu-id="af2f2-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="af2f2-144">Funkce AJAX, kterou jsme implementovali, funguje dobře a rychle.</span><span class="sxs-lookup"><span data-stu-id="af2f2-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="af2f2-145">Někdy se to může stát tak rychle, že si uživatel nemusí všimnout, že odkaz RSVP byl nahrazen novým textem.</span><span class="sxs-lookup"><span data-stu-id="af2f2-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="af2f2-146">Chcete-li výsledek trochu více zřejmé, můžeme přidat jednoduchou animaci upozornit na aktualizační zprávu.</span><span class="sxs-lookup"><span data-stu-id="af2f2-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="af2f2-147">Výchozí ASP.NET šablona projektu MVC obsahuje jQuery - vynikající (a velmi populární) open source JavaScript knihovnu, která je také podporována společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="af2f2-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="af2f2-148">jQuery poskytuje řadu funkcí, včetně pěkné HTML DOM výběra efektů knihovny.</span><span class="sxs-lookup"><span data-stu-id="af2f2-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="af2f2-149">Chcete-li použít jQuery, nejprve na něj přidáme odkaz na skript.</span><span class="sxs-lookup"><span data-stu-id="af2f2-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="af2f2-150">Vzhledem k tomu, že budeme používat jQuery v různých místech v rámci našich stránek, přidáme odkaz na skript v našem souboru stránky předlohy Site.master, aby jej mohly používat všechny stránky.</span><span class="sxs-lookup"><span data-stu-id="af2f2-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="af2f2-151">*Tip: Ujistěte se, že jste nainstalovali opravu hotfix JavaScript intellisense pro vs 2008 SP1, která umožňuje bohatší podporu intellisense pro soubory JavaScript (včetně jQuery). Můžete si jej stáhnout z:http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="af2f2-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="af2f2-152">Kód napsaný pomocí JQuery často používá globální metodu JavaScriptu "$()", která načítá jeden nebo více elementů HTML pomocí voliče CSS.</span><span class="sxs-lookup"><span data-stu-id="af2f2-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="af2f2-153">Například *$("#rsvpmsg")* vybere libovolný element HTML s id rsvpmsg, zatímco *$(".something")* vybere všechny prvky s názvem třídy CSS "něco".</span><span class="sxs-lookup"><span data-stu-id="af2f2-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="af2f2-154">Můžete také psát pokročilejší dotazy, jako je "vrátit všechna zaškrtnutá přepínací tlačítka" pomocí výběrového dotazu, jako je: *$("input[@type=radio][@checked]")*.</span><span class="sxs-lookup"><span data-stu-id="af2f2-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="af2f2-155">Jakmile vyberete prvky, můžete volat metody na ně provést akci, jako je jejich skrytí: *$("#rsvpmsg").hide();*</span><span class="sxs-lookup"><span data-stu-id="af2f2-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="af2f2-156">Pro náš scénář RSVP definujeme jednoduchou funkci JavaScriptu s názvem "AnimateRSVPMessage", &lt;která&gt; vybere div "rsvpmsg" a animuje velikost jeho textového obsahu.</span><span class="sxs-lookup"><span data-stu-id="af2f2-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="af2f2-157">Níže uvedený kód spustí text malý a pak způsobí, že zvýšení v průběhu 400 milisekund časový rámec:</span><span class="sxs-lookup"><span data-stu-id="af2f2-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="af2f2-158">Můžeme pak wire-up tuto funkci JavaScript, které mají být volány po našem volání AJAX úspěšně dokončí předáním jeho jméno naše Ajax.ActionLink() pomocné metody (přes AjaxOptions "OnSuccess" vlastnost události):</span><span class="sxs-lookup"><span data-stu-id="af2f2-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="af2f2-159">A teď, když je kliknuto na odkaz "RSVP pro tuto událost" a naše volání AJAX úspěšně dokončí, obsahová zpráva odeslaná zpět se animuje a roste:</span><span class="sxs-lookup"><span data-stu-id="af2f2-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="af2f2-160">Kromě poskytování "OnSuccess" událost AjaxOptions objekt zpřístupňuje OnBegin, OnFailure a OnComplete události, které můžete zpracovat (spolu s řadou dalších vlastností a užitečných možností).</span><span class="sxs-lookup"><span data-stu-id="af2f2-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="af2f2-161">Vyčištění - refaktorovat částečné zobrazení RSVP</span><span class="sxs-lookup"><span data-stu-id="af2f2-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="af2f2-162">Naše šablona zobrazení podrobností začíná být trochu dlouhá, což přesčas trochu ztíží pochopení.</span><span class="sxs-lookup"><span data-stu-id="af2f2-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="af2f2-163">Chcete-li zlepšit čitelnost kódu, dokončeme vytvořením částečného zobrazení – RSVPStatus.ascx – které zapouzdřuje veškerý kód zobrazení RSVP pro naši stránku Podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="af2f2-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="af2f2-164">Můžeme to udělat kliknutím pravým tlačítkem myši na složku \Views\Dinners a výběrem příkazu nabídky Přidat-&gt;zobrazit.</span><span class="sxs-lookup"><span data-stu-id="af2f2-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="af2f2-165">Budeme mít to trvat Dinner objekt jako jeho silně typed ViewModel.</span><span class="sxs-lookup"><span data-stu-id="af2f2-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="af2f2-166">Poté můžeme zkopírovat/vložit obsah RSVP z našeho zobrazení Details.aspx do něj.</span><span class="sxs-lookup"><span data-stu-id="af2f2-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="af2f2-167">Poté, co jsme udělali, že pojďme také vytvořit další částečné zobrazení - EditAndDeleteLinks.ascx - to zapouzdřuje naše Upravit a odstranit odkaz zobrazit kód.</span><span class="sxs-lookup"><span data-stu-id="af2f2-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="af2f2-168">Budeme také mít vzít Dinner objekt jako jeho silně typed ViewModel a zkopírujte nebo vložte upravit a odstranit logiku z našeho Details.aspx zobrazení do něj.</span><span class="sxs-lookup"><span data-stu-id="af2f2-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="af2f2-169">Naše podrobnosti zobrazení šablony pak můžete zahrnout pouze dvě html.RenderPartial() volání metody v dolní části:</span><span class="sxs-lookup"><span data-stu-id="af2f2-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="af2f2-170">Díky čistič kódu číst a udržovat.</span><span class="sxs-lookup"><span data-stu-id="af2f2-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="af2f2-171">Další krok</span><span class="sxs-lookup"><span data-stu-id="af2f2-171">Next Step</span></span>

<span data-ttu-id="af2f2-172">Podívejme se nyní na to, jak můžeme ajax dále používat a přidat interaktivní podporu mapování do naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="af2f2-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="af2f2-173">[Předchozí](secure-applications-using-authentication-and-authorization.md)
> [další](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="af2f2-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
