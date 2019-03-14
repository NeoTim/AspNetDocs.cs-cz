---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: ASP.NET MVC přehled zobrazení (VB) | Dokumentace Microsoftu
author: StephenWalther
description: Co se zobrazení ASP.NET MVC a jak se liší od stránku HTML? V tomto kurzu Stephen Walther vás seznámí s zobrazení a předvádí, jak můžete t...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: a7f4afd70a17281123a7448a00896c186b9a00f8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067723"
---
<a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="a1638-104">ASP.NET MVC – přehled zobrazení (VB)</span><span class="sxs-lookup"><span data-stu-id="a1638-104">ASP.NET MVC Views Overview (VB)</span></span>
====================
<span data-ttu-id="a1638-105">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a1638-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="a1638-106">Co se zobrazení ASP.NET MVC a jak se liší od stránku HTML?</span><span class="sxs-lookup"><span data-stu-id="a1638-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="a1638-107">V tomto kurzu Stephen Walther vás seznámí s zobrazení a ukazuje, jak můžete využít výhod zobrazení dat a pomocných rutin HTML v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>


<span data-ttu-id="a1638-108">Účelem tohoto kurzu je poskytne stručný úvod do ASP.NET MVC zobrazení, zobrazení dat a pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="a1638-109">Na konci tohoto kurzu budete vědět, jak vytvářet nová zobrazení, předat data z kontroleru zobrazení a použití pomocných rutin HTML ke generování obsahu v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="a1638-110">Principy zobrazení</span><span class="sxs-lookup"><span data-stu-id="a1638-110">Understanding Views</span></span>

<span data-ttu-id="a1638-111">Na rozdíl od ASP nebo ASP.NET ASP.NET MVC neobsahuje nic, který přímo odpovídá na stránku.</span><span class="sxs-lookup"><span data-stu-id="a1638-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="a1638-112">V aplikaci MVC rozhraní ASP.NET není stránku na disku, který odpovídá cestě v adrese URL, kterou zadáte do adresního řádku prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a1638-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="a1638-113">Nejbližší věc do stránky v aplikaci ASP.NET MVC se volá *zobrazení*.</span><span class="sxs-lookup"><span data-stu-id="a1638-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="a1638-114">V aplikaci ASP.NET MVC se mapují příchozí požadavky prohlížeče na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a1638-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="a1638-115">Zobrazení může vrátit akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a1638-115">A controller action might return a view.</span></span> <span data-ttu-id="a1638-116">Akce kontroleru může ale provést i jiný druh akce, jako je probíhá přesměrování na jiný akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a1638-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="a1638-117">Výpis 1 obsahuje řadič jednoduché s názvem HomeController.</span><span class="sxs-lookup"><span data-stu-id="a1638-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="a1638-118">HomeController zpřístupňuje s názvem Index() a Details() dvě akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a1638-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="a1638-119">**Výpis 1 - HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="a1638-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="a1638-120">První akci Index() akci, můžete vyvolat zadáním následující adresy URL do adresního řádku prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="a1638-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="a1638-121">/ Home/Index</span><span class="sxs-lookup"><span data-stu-id="a1638-121">/Home/Index</span></span>

<span data-ttu-id="a1638-122">Druhou akci Details() akci, můžete vyvolat tak, že do prohlížeče zadáte tuto adresu:</span><span class="sxs-lookup"><span data-stu-id="a1638-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="a1638-123">/ Home/podrobností</span><span class="sxs-lookup"><span data-stu-id="a1638-123">/Home/Details</span></span>

<span data-ttu-id="a1638-124">Akce Index() vrátí zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-124">The Index() action returns a view.</span></span> <span data-ttu-id="a1638-125">Většinu akcí, které vytvoříte vrátí zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-125">Most actions that you create will return views.</span></span> <span data-ttu-id="a1638-126">Akce však může vrátit jiné druhy výsledky akce.</span><span class="sxs-lookup"><span data-stu-id="a1638-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="a1638-127">Například akce Details() vrátí RedirectToActionResult, který přesměruje na akce Index() příchozího požadavku.</span><span class="sxs-lookup"><span data-stu-id="a1638-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="a1638-128">Akce Index() obsahuje následující jediný řádek kódu:</span><span class="sxs-lookup"><span data-stu-id="a1638-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="a1638-129">View()</span><span class="sxs-lookup"><span data-stu-id="a1638-129">View()</span></span>

<span data-ttu-id="a1638-130">Tento řádek kódu vrátí zobrazení, které musí být v následujícím umístění na vašem webovém serveru:</span><span class="sxs-lookup"><span data-stu-id="a1638-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="a1638-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="a1638-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="a1638-132">Cesta k zobrazení je odvozen z názvu kontroleru a názvu akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a1638-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="a1638-133">Pokud dáváte přednost, může být explicitní o zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="a1638-134">Následující řádek kódu vrátí zobrazení s názvem Fred:</span><span class="sxs-lookup"><span data-stu-id="a1638-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="a1638-135">Zobrazení (Fred)</span><span class="sxs-lookup"><span data-stu-id="a1638-135">View( Fred )</span></span>

<span data-ttu-id="a1638-136">Pokud je spuštěn tento řádek kódu, zobrazení je vrácen z následující cestu:</span><span class="sxs-lookup"><span data-stu-id="a1638-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="a1638-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="a1638-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a1638-138">Pokud budete chtít vytvořit testy jednotek pro aplikace ASP.NET MVC je vhodné k explicitnímu názvy zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="a1638-139">Tímto způsobem můžete vytvořit testování částí k ověření, že očekávané zobrazení byl vrácen akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a1638-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>


## <a name="adding-content-to-a-view"></a><span data-ttu-id="a1638-140">Přidávání obsahu do zobrazení</span><span class="sxs-lookup"><span data-stu-id="a1638-140">Adding Content to a View</span></span>

<span data-ttu-id="a1638-141">Zobrazení je standard (dokumentu HTML, který může obsahovat skriptů X).</span><span class="sxs-lookup"><span data-stu-id="a1638-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="a1638-142">Přidat dynamický obsah k zobrazení pomocí skriptů.</span><span class="sxs-lookup"><span data-stu-id="a1638-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="a1638-143">Například zobrazení v informacích 2 ukazuje aktuální datum a čas.</span><span class="sxs-lookup"><span data-stu-id="a1638-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="a1638-144">**Listing 2 - \Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="a1638-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="a1638-145">Všimněte si, že tělo stránky HTML v zobrazení 2 obsahuje následující skript:</span><span class="sxs-lookup"><span data-stu-id="a1638-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="a1638-146">&lt;Response.Write(DateTime.Now) %&gt;</span><span class="sxs-lookup"><span data-stu-id="a1638-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="a1638-147">Použít skript oddělovače &lt;% a %&gt; označit začátek a konec skriptu.</span><span class="sxs-lookup"><span data-stu-id="a1638-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="a1638-148">Tento skript je napsána v jazyce Visual basic.</span><span class="sxs-lookup"><span data-stu-id="a1638-148">This script is written in Visual basic.</span></span> <span data-ttu-id="a1638-149">Zobrazí aktuální datum a čas voláním metody Response.Write() metody k vykreslení obsahu v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a1638-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="a1638-150">Skript oddělovače &lt;% a %&gt; lze použít k provedení jednoho nebo více příkazů.</span><span class="sxs-lookup"><span data-stu-id="a1638-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="a1638-151">Vzhledem k tomu, že volání metody Response.Write() tak často, Microsoft vám poskytne zástupce pro volání metody Response.Write() metody.</span><span class="sxs-lookup"><span data-stu-id="a1638-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="a1638-152">Zobrazení v informacích 3 používá oddělovače &lt;% = a %&gt; jako zástupce pro volání metody Response.Write().</span><span class="sxs-lookup"><span data-stu-id="a1638-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="a1638-153">**Listing 3 - Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="a1638-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="a1638-154">Libovolný jazyk .NET můžete použít ke generování dynamického obsahu v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="a1638-155">Za normálních okolností vše můžete pomocí jazyka Visual Basic .NET nebo C# pro zápis kontrolerů a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-155">Normally, you�ll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="a1638-156">Použití pomocných rutin HTML k vygenerování zobrazení obsahu</span><span class="sxs-lookup"><span data-stu-id="a1638-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="a1638-157">Aby bylo snazší k přidání obsahu do zobrazení, můžete využít výhod nástroje s názvem *pomocné rutiny HTML*.</span><span class="sxs-lookup"><span data-stu-id="a1638-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="a1638-158">Pomocné rutiny HTML, je obvykle metodu, která z nich generuje řetězec.</span><span class="sxs-lookup"><span data-stu-id="a1638-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="a1638-159">Pomocné rutiny HTML můžete použít ke generování standardní elementy jazyka HTML, jako jsou textová pole, odkazy, rozevírací seznamy a pole se seznamem.</span><span class="sxs-lookup"><span data-stu-id="a1638-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="a1638-160">Například zobrazení výpisu 4 využívá registrů tři pomocných rutin HTML – Pomocníci BeginForm() TextBox() a Password() – ke generování přihlášení formulář (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="a1638-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="a1638-161">**Listing 4 -- \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="a1638-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]


<span data-ttu-id="a1638-162">[![Dialogové okno Nový projekt](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a1638-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="a1638-163">**Obrázek 01**: Standardní přihlašovací formulář ([kliknutím ji zobrazíte obrázek v plné velikosti](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="a1638-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>


<span data-ttu-id="a1638-164">Všechny metody pomocných rutin HTML se nazývají na vlastnosti Html zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="a1638-165">Například voláním metody Html.TextBox() vykreslení textové pole.</span><span class="sxs-lookup"><span data-stu-id="a1638-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="a1638-166">Všimněte si, že používáte skript oddělovače &lt;% = a %&gt; při volání metody Html.TextBox() i Html.Password() pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="a1638-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="a1638-167">Tyto pomocné rutiny jednoduše vrátit řetězec.</span><span class="sxs-lookup"><span data-stu-id="a1638-167">These helpers simply return a string.</span></span> <span data-ttu-id="a1638-168">Je třeba volat metody Response.Write() k vykreslení řetězec, který se v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a1638-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="a1638-169">Použití metody pomocné rutiny HTML není povinné.</span><span class="sxs-lookup"><span data-stu-id="a1638-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="a1638-170">Jejich usnadnit vám život díky snížení objemu HTML a skript, který budete muset napsat.</span><span class="sxs-lookup"><span data-stu-id="a1638-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="a1638-171">Zobrazení výpisu 5 vykreslí přesně stejný formulář jako zobrazení výpisu 4 bez použití pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="a1638-172">**Listing 5 -- \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="a1638-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="a1638-173">Máte také možnost vytvoření vlastních pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="a1638-174">Můžete například vytvořit GridView() Pomocná metoda, která automaticky zobrazí sadu záznamů databáze v tabulku HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="a1638-175">V tomto tématu budeme věnovat v tomto kurzu **pomocných rutin HTML vytvořením Custom**.</span><span class="sxs-lookup"><span data-stu-id="a1638-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="a1638-176">Pomocí zobrazení dat k předávání dat k zobrazení</span><span class="sxs-lookup"><span data-stu-id="a1638-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="a1638-177">Zobrazení dat použijete k předání dat z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="a1638-178">Představte si zobrazit data, jako je balíček, který můžete odeslat prostřednictvím e-mailu.</span><span class="sxs-lookup"><span data-stu-id="a1638-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="a1638-179">Všechna data z kontroleru předána do zobrazení musí být odeslána pomocí tohoto balíčku.</span><span class="sxs-lookup"><span data-stu-id="a1638-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="a1638-180">Například kontroler v informacích 6 přidá zprávu zobrazíte data.</span><span class="sxs-lookup"><span data-stu-id="a1638-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="a1638-181">**Výpis 6 - ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="a1638-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="a1638-182">Kontroler ViewData vlastnost představuje kolekci párů názvu a hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a1638-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="a1638-183">Výpis 6 metodu Index() přidá položku do kolekce dat zobrazení s názvem zprávy s hodnotou Hello World!.</span><span class="sxs-lookup"><span data-stu-id="a1638-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="a1638-184">Při zobrazení je vrácený metodou Index(), data zobrazení je automaticky předána do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="a1638-185">Zobrazení výpisu 7 načte zprávy z dat zobrazení a vykreslí zprávy do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a1638-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="a1638-186">**Listing 7 -- \Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="a1638-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="a1638-187">Všimněte si, že zobrazení využívá metodu pomocné rutiny HTML Html.Encode() při vykreslování zprávy.</span><span class="sxs-lookup"><span data-stu-id="a1638-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="a1638-188">Pomocné rutiny HTML Html.Encode() kóduje zvláštní znaky, jako &lt; a &gt; do znaků, které jsou bezpečné pro zobrazení na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="a1638-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="a1638-189">Pokaždé, když se vám zobrazit obsah, který uživatel odešle na web, by měl kódování obsahu, aby se zabránilo útoků založených na injektáži JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="a1638-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="a1638-190">(Protože jsme vytvořili zprávu si v ProductController, budeme zadávat t opravdu potřebujete ke kódování zprávy.</span><span class="sxs-lookup"><span data-stu-id="a1638-190">(Because we created the message ourselves in the ProductController, we don�t really need to encode the message.</span></span> <span data-ttu-id="a1638-191">Nicméně je dobré se vždy volat metodu Html.Encode() při zobrazení obsahu načítá ze zobrazení dat v rámci zobrazení.)</span><span class="sxs-lookup"><span data-stu-id="a1638-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="a1638-192">Ve výpisu 7 jsme využil předání jednoduché řetězcovou zprávu z řadiče zobrazení dat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="a1638-193">Zobrazení dat můžete použít také k předání dalších typů dat, jako jsou kolekce záznamů databáze z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="a1638-194">Například pokud chcete zobrazit obsah databázové tabulky produktů v zobrazení, pak by úspěšně prošel zpracováním kolekce databáze záznamů v zobrazení data.</span><span class="sxs-lookup"><span data-stu-id="a1638-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="a1638-195">Máte také možnost předat data silného typu zobrazení z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="a1638-196">V tomto tématu budeme věnovat v tomto kurzu **Principy silného typu zobrazení dat a zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="a1638-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="a1638-197">Souhrn</span><span class="sxs-lookup"><span data-stu-id="a1638-197">Summary</span></span>

<span data-ttu-id="a1638-198">Tento kurz poskytuje stručný úvod do ASP.NET MVC zobrazení, zobrazení dat a pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="a1638-199">V prvním oddílu jste zjistili, jak přidat nová zobrazení do projektu.</span><span class="sxs-lookup"><span data-stu-id="a1638-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="a1638-200">Jste zjistili, že je nutné přidat zobrazení do správné složky pro volání z určitý kontroler.</span><span class="sxs-lookup"><span data-stu-id="a1638-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="a1638-201">Dále jsme probírali tématu pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="a1638-202">Jste se naučili, jak pomocných rutin HTML umožňují snadno vygenerovat standardní obsah ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="a1638-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="a1638-203">Nakonec jste zjistili, jak využít výhod zobrazení dat k předání dat z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a1638-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1638-204">[Předchozí](passing-data-to-view-master-pages-cs.md)
> [další](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a1638-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>