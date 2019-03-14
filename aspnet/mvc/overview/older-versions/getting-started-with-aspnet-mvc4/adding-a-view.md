---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: Přidání zobrazení | Dokumentace Microsoftu
author: Rick-Anderson
description: 'Poznámka: Najít aktualizovanou verzi tohoto kurzu je k dispozici tady, která používá ASP.NET MVC 5 a Visual Studio 2013. Je bezpečnější, sledovat a ukázka mnohem jednodušší...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 7b55a55db6207b8ff18b2dd207e919cee45f6973
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067726"
---
<a name="adding-a-view"></a><span data-ttu-id="69354-104">Přidání zobrazení</span><span class="sxs-lookup"><span data-stu-id="69354-104">Adding a View</span></span>
====================
<span data-ttu-id="69354-105">Podle [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="69354-105">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

> > [!NOTE]
> > <span data-ttu-id="69354-106">Je k dispozici aktualizovaná verze tohoto kurzu [tady](../../getting-started/introduction/getting-started.md) , která používá ASP.NET MVC 5 a Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="69354-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="69354-107">Je bezpečnější, postupujte podle mnohem jednodušší a ukazuje další funkce.</span><span class="sxs-lookup"><span data-stu-id="69354-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="69354-108">V této části se chystáte změnit `HelloWorldController` třídu použít zobrazení soubory šablon do čistě zapouzdření proces generování odpovědi HTML do klienta.</span><span class="sxs-lookup"><span data-stu-id="69354-108">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="69354-109">Vytvoříte soubor šablony zobrazení pomocí [zobrazovací modul Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) zavedené v architektuře ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="69354-109">You'll create a view template file using the [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="69354-110">Šablony Razor na základě zobrazení mají *.cshtml* příponu souboru a poskytují elegantní způsob, jak vytvořit HTML výstup pomocí jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="69354-110">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="69354-111">Razor minimalizuje počet znaků a vyžaduje při psaní zobrazit šablonu stisknutí kláves a umožňuje rychlé, dynamika kódování pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="69354-111">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="69354-112">Aktuálně `Index` metoda vrátí řetězec a zobrazí se zpráva, která je pevně zakódovaný ve třídě controller.</span><span class="sxs-lookup"><span data-stu-id="69354-112">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="69354-113">Změnit `Index` metodu pro návrat `View` objektu, jak je znázorněno v následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="69354-113">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="69354-114">`Index` Výše uvedené metody používá šablonu zobrazení k vygenerování odpověď ve formátu HTML v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="69354-114">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="69354-115">Metody kontroleru (označované také jako [metody akce](http://rachelappel.com/asp.net-mvc-actionresults-explained)), například `Index` metody popsané výše, obvykle vracet [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (nebo třída odvozená z [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), není primitivní typy, jako je řetězec.</span><span class="sxs-lookup"><span data-stu-id="69354-115">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="69354-116">V projektu, přidat zobrazení šablony, který vám pomůže s `Index` metody.</span><span class="sxs-lookup"><span data-stu-id="69354-116">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="69354-117">Chcete-li to provést, klepněte pravým tlačítkem myši `Index` metoda a klikněte na tlačítko **přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="69354-117">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="69354-118">**Přidat zobrazení** zobrazí se dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="69354-118">The **Add View** dialog box appears.</span></span> <span data-ttu-id="69354-119">Ponechte výchozí nastavení, jako jsou a klikněte na tlačítko **přidat** tlačítka:</span><span class="sxs-lookup"><span data-stu-id="69354-119">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="69354-120">*MvcMovie\Views\HelloWorld* složky a *MvcMovie\Views\HelloWorld\Index.cshtml* se vytvoří soubor.</span><span class="sxs-lookup"><span data-stu-id="69354-120">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="69354-121">Zobrazí se jim v **Průzkumníka řešení**:</span><span class="sxs-lookup"><span data-stu-id="69354-121">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="69354-122">Zobrazí se následující *Index.cshtml* soubor, který byl vytvořen:</span><span class="sxs-lookup"><span data-stu-id="69354-122">The following shows the *Index.cshtml* file that was created:</span></span>

![HelloWorldIndex](adding-a-view/_static/image4.png)

<span data-ttu-id="69354-124">Přidejte následující kód HTML v části `<h2>` značky.</span><span class="sxs-lookup"><span data-stu-id="69354-124">Add the following HTML under the `<h2>` tag.</span></span>

[!code-html[Main](adding-a-view/samples/sample2.html)]

<span data-ttu-id="69354-125">Kompletní *MvcMovie\Views\HelloWorld\Index.cshtml* souboru je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="69354-125">The complete *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

<span data-ttu-id="69354-126">Pokud používáte sadu Visual Studio 2012, v Průzkumníku řešení, klikněte pravým tlačítkem myši *Index.cshtml* a vyberte možnost **zobrazení v nástroje Page Inspector**.</span><span class="sxs-lookup"><span data-stu-id="69354-126">If you are using Visual Studio 2012, in solution explorer, right click the *Index.cshtml* file and select **View in Page Inspector**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="69354-128">[Nástroj Page Inspector kurzu](../../views/using-page-inspector-in-aspnet-mvc.md) obsahuje další informace o tento nový nástroj.</span><span class="sxs-lookup"><span data-stu-id="69354-128">The [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) has more information about this new tool.</span></span>

<span data-ttu-id="69354-129">Alternativně spusťte aplikaci a přejděte `HelloWorld` kontroler (`http://localhost:xxxx/HelloWorld`).</span><span class="sxs-lookup"><span data-stu-id="69354-129">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="69354-130">`Index` Metoda ve vašem řadiči nedělalo množství práce, jednoduše spustili příkaz `return View()`, která zadané, že metoda by měla používat soubor šablony zobrazení k vykreslení odezva do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="69354-130">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="69354-131">Protože jste nezadali explicitní název souboru šablony zobrazení pro použití, ASP.NET MVC na výchozí použití *Index.cshtml* zobrazení souboru v *\Views\HelloWorld* složky.</span><span class="sxs-lookup"><span data-stu-id="69354-131">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="69354-132">Následující obrázek ukazuje řetězec &quot;Hello z našich zobrazit šablonu!&quot; pevně zakódované v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-132">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="69354-133">Vypadá hodně Dobrá.</span><span class="sxs-lookup"><span data-stu-id="69354-133">Looks pretty good.</span></span> <span data-ttu-id="69354-134">Všimněte si však, že v prohlížeči na záhlaví okna zobrazuje &quot;indexu Moje ASP.NET A&quot; a uvádí, že velké objemy odkaz nahoře na stránce &quot;vaše logo.&quot; Níže &quot;vaše logo sem.&quot; odkazu jsou informace o registraci a protokolu v odkazech a níže, který odkazuje na domovskou stránku a obraťte se na stránky.</span><span class="sxs-lookup"><span data-stu-id="69354-134">However, notice that the browser's title bar shows &quot;Index My ASP.NET A&quot; and the big link on the top of the page says &quot;your logo here.&quot; Below the &quot;your logo here.&quot; link are registration and log in links, and below that links to Home, About and Contact pages.</span></span> <span data-ttu-id="69354-135">Změňme některé z nich.</span><span class="sxs-lookup"><span data-stu-id="69354-135">Let's change some of these.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="69354-136">Změna zobrazení a rozložení stránky</span><span class="sxs-lookup"><span data-stu-id="69354-136">Changing Views and Layout Pages</span></span>

<span data-ttu-id="69354-137">Nejprve, kterou chcete změnit &quot;vaše logo sem.&quot; nadpis v horní části stránky.</span><span class="sxs-lookup"><span data-stu-id="69354-137">First, you want to change the &quot;your logo here.&quot; title at the top of the page.</span></span> <span data-ttu-id="69354-138">Tento text je společné pro všechny stránky.</span><span class="sxs-lookup"><span data-stu-id="69354-138">That text is common to every page.</span></span> <span data-ttu-id="69354-139">Ve skutečnosti implementaci na jenom jednom místě v projektu, i když se zobrazí na každé stránce v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="69354-139">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="69354-140">Přejděte */zobrazení/Shared* složky v **Průzkumníku řešení** a otevřete  *\_Layout.cshtml* souboru.</span><span class="sxs-lookup"><span data-stu-id="69354-140">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="69354-141">Tento soubor se nazývá *stránku rozložení* a je sdílený &quot;prostředí&quot; , všechny ostatní stránky použít.</span><span class="sxs-lookup"><span data-stu-id="69354-141">This file is called a *layout page* and it's the shared &quot;shell&quot; that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="69354-143">Šablony rozložení umožňují zadat kontejner rozložení HTML vašeho webu na jednom místě a použijte ji na několika stránkách ve vaší lokalitě.</span><span class="sxs-lookup"><span data-stu-id="69354-143">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="69354-144">Najít `@RenderBody()` řádku.</span><span class="sxs-lookup"><span data-stu-id="69354-144">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="69354-145">`RenderBody` je zástupný symbol, kde všechny v zobrazení konkrétní stránky, můžete vytvořit, zobrazit &quot;zabalené&quot; stránce rozložení.</span><span class="sxs-lookup"><span data-stu-id="69354-145">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="69354-146">Například, pokud vyberete o odkaz *Views\Home\About.cshtml* je zobrazení vykresleno uvnitř `RenderBody` metody.</span><span class="sxs-lookup"><span data-stu-id="69354-146">For example, if you select the About link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="69354-147">Změna záhlaví název webu v šabloně rozložení z &quot;vaše logo&quot; k &quot;MVC Movie&quot;.</span><span class="sxs-lookup"><span data-stu-id="69354-147">Change the site-title heading in the layout template from &quot;your logo here&quot; to &quot;MVC Movie&quot;.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="69354-148">Obsah prvku název nahraďte následující značky:</span><span class="sxs-lookup"><span data-stu-id="69354-148">Replace the contents of the title element with the following markup:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="69354-149">Spusťte aplikaci a Všimněte si, že nyní říká &quot;MVC Movie &quot;.</span><span class="sxs-lookup"><span data-stu-id="69354-149">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="69354-150">Klikněte na tlačítko **o** odkaz kde najdete v článku ukazuje, jak tuto stránku &quot;MVC Movie&quot;také.</span><span class="sxs-lookup"><span data-stu-id="69354-150">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="69354-151">Jsme byli schopni jednou provést změnu v šabloně rozložení a mít všechny stránky na webu odrážely nový název.</span><span class="sxs-lookup"><span data-stu-id="69354-151">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="69354-152">Teď Změníme název zobrazení indexu.</span><span class="sxs-lookup"><span data-stu-id="69354-152">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="69354-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="69354-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="69354-154">Existují dvě místa, kde provést změnu: první, text, který se zobrazí v záhlaví prohlížeče a v hlavičce sekundární ( `<h2>` element).</span><span class="sxs-lookup"><span data-stu-id="69354-154">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="69354-155">Budete je provedete trochu jinak, uvidíte, jaké verze kódu se změní kterou část aplikace.</span><span class="sxs-lookup"><span data-stu-id="69354-155">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

<span data-ttu-id="69354-156">K označení názvu HTML zobrazení kódu nad sady `Title` vlastnost `ViewBag` objektu (což je v *Index.cshtml* zobrazit šablonu).</span><span class="sxs-lookup"><span data-stu-id="69354-156">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="69354-157">Pokud podíváte zpátky na zdrojový kód šablony rozložení, můžete si všimnout, že šablona používá tuto hodnotu v `<title>` element jako součást `<head>` část HTML, které jsme dřív ke změně.</span><span class="sxs-lookup"><span data-stu-id="69354-157">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span> <span data-ttu-id="69354-158">Použití této funkce `ViewBag` přístup, můžete snadno předat další parametry mezi zobrazit šablonu a soubor rozložení.</span><span class="sxs-lookup"><span data-stu-id="69354-158">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="69354-159">Spusťte aplikaci a přejděte do `http://localhost:xx/HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="69354-159">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="69354-160">Všimněte si, že došlo ke změně názvu prohlížeče, záhlaví primární a sekundární záhlaví.</span><span class="sxs-lookup"><span data-stu-id="69354-160">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="69354-161">(Pokud se nezobrazí změny v prohlížeči, pravděpodobně jste zobrazili obsah uložený v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="69354-161">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="69354-162">Stisknutím kláves Ctrl + F5 v prohlížeči k vynucení odpověď ze serveru, který se má načíst.) Název prohlížeče se vytvoří s `ViewBag.Title` jsme si nastavili *Index.cshtml* zobrazit šablony a další &quot;-filmová aplikace&quot; přidá soubor rozložení.</span><span class="sxs-lookup"><span data-stu-id="69354-162">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="69354-163">Všimněte si také způsob, jak v obsahu *Index.cshtml* zobrazit šablonu byl sloučen s  *\_Layout.cshtml* zobrazit šablonu a odpověď o jedné HTML byl odeslán do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="69354-163">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="69354-164">Rozložení šablony usnadňují skutečně provést změny, které platí pro všechny stránky v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="69354-164">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="69354-165">Naše nepatrné &quot;data&quot; (v tomto případě &quot;Hello z našich zobrazit šablonu!&quot; zprávu) je pevně zakódované, i když.</span><span class="sxs-lookup"><span data-stu-id="69354-165">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="69354-166">Má aplikace MVC &quot;V&quot; (zobrazení) a máte &quot;C&quot; (controller), ale žádné &quot;M&quot; (modelu) ještě.</span><span class="sxs-lookup"><span data-stu-id="69354-166">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="69354-167">Po chvíli, projdeme postup vytvoření databáze a načíst datový model z něj.</span><span class="sxs-lookup"><span data-stu-id="69354-167">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="69354-168">Předání dat z Kontroleru zobrazení</span><span class="sxs-lookup"><span data-stu-id="69354-168">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="69354-169">Předtím, než jsme přejděte k databázi a mluvit o modely, ale nejprve se seznámíme předávání informací z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-169">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="69354-170">Kontroler třídy jsou vyvolány v reakci na příchozí adrese URL žádosti.</span><span class="sxs-lookup"><span data-stu-id="69354-170">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="69354-171">Třída kontroleru je místo, kde píšete kód, který zpracovává příchozí prohlížeč požádá, načte data z databáze a nakonec rozhodne, jaký typ odpověď k odeslání zpět do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="69354-171">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="69354-172">Zobrazit šablony pak lze z kontroleru pro generování a formátovat odpověď ve formátu HTML v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="69354-172">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="69354-173">Kontrolery odpovídají za poskytování libovolné dat nebo objekty jsou nutné v pořadí pro šablonu zobrazení k vykreslení odezva do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="69354-173">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="69354-174">Osvědčený postup: **Zobrazit šablonu by nikdy provádění obchodní logiky nebo pracovat přímo s databází**.</span><span class="sxs-lookup"><span data-stu-id="69354-174">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="69354-175">Zobrazit šablonu místo toho by měla fungovat jenom s data, která je poskytována kontroleru.</span><span class="sxs-lookup"><span data-stu-id="69354-175">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="69354-176">Zachování to &quot;oddělení oblastí zájmu&quot; pomáhá udržovat váš kód čistý, možností intenzivního testování a jednodušší údržbu.</span><span class="sxs-lookup"><span data-stu-id="69354-176">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="69354-177">V současné době `Welcome` metodu akce v `HelloWorldController` třídy přijímá `name` a `numTimes` parametr a potom výstupy hodnoty přímo do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="69354-177">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="69354-178">Spíše než mít řadič vykreslení této odpovědi jako řetězec, Změníme kontroler místo toho použít šablonu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-178">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="69354-179">Zobrazit šablonu vygeneruje dynamické odpovědi, což znamená, že je potřeba předat odpovídající částí dat z kontroleru zobrazení k vygenerování odpovědi.</span><span class="sxs-lookup"><span data-stu-id="69354-179">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="69354-180">Můžete to provést tak, že kontroler umístit dynamických dat (parametry), která vyžaduje zobrazení šablony `ViewBag` objekt, který se pak můžou zobrazit šablonu.</span><span class="sxs-lookup"><span data-stu-id="69354-180">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="69354-181">Vraťte se na *HelloWorldController.cs* soubor a změňte `Welcome` metoda pro přidání `Message` a `NumTimes` hodnota, která se `ViewBag` objektu.</span><span class="sxs-lookup"><span data-stu-id="69354-181">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="69354-182">`ViewBag` je to dynamický objekt, což znamená, že můžete vložit cokoliv, co chcete `ViewBag` objekt nemá žádné definované vlastnosti, dokud je něco v ji vložíte.</span><span class="sxs-lookup"><span data-stu-id="69354-182">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="69354-183">[Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapují pojmenované parametry (`name` a `numTimes`) z řetězce dotazu do adresního řádku parametrům ve své metodě.</span><span class="sxs-lookup"><span data-stu-id="69354-183">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="69354-184">Kompletní *HelloWorldController.cs* souboru vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="69354-184">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="69354-185">Nyní `ViewBag` objekt obsahuje data, která bude předána do zobrazení automaticky.</span><span class="sxs-lookup"><span data-stu-id="69354-185">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="69354-186">Dále je třeba úvodní zobrazit šablonu!</span><span class="sxs-lookup"><span data-stu-id="69354-186">Next, you need a Welcome view template!</span></span> <span data-ttu-id="69354-187">V **sestavení** nabídce vyberte možnost **sestavení MvcMovie** k Ujistěte se, že je projekt kompilován.</span><span class="sxs-lookup"><span data-stu-id="69354-187">In the **Build** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="69354-188">Klikněte pravým tlačítkem na uvnitř `Welcome` metoda a klikněte na tlačítko **přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="69354-188">Then right-click inside the `Welcome` method and click **Add View**.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="69354-189">Co **přidat zobrazení** dialogové okno bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="69354-189">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image11.png)

<span data-ttu-id="69354-190">Klikněte na tlačítko **přidat**a poté přidejte následující kód `<h2>` element na novém *Welcome.cshtml* souboru.</span><span class="sxs-lookup"><span data-stu-id="69354-190">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="69354-191">Vytvoříte smyčku, která uvádí, že &quot;Hello&quot; tolikrát, kolikrát uživatel uvádí, že by měl.</span><span class="sxs-lookup"><span data-stu-id="69354-191">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="69354-192">Kompletní *Welcome.cshtml* souboru je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="69354-192">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

<span data-ttu-id="69354-193">Spusťte aplikaci a přejděte na následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="69354-193">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="69354-194">Data jsou na základě adresy URL a předat pomocí řadiče [modelu pořadače](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span><span class="sxs-lookup"><span data-stu-id="69354-194">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="69354-195">Balíčky data do kontroleru `ViewBag` objektu a, které se objekt předá do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-195">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="69354-196">Zobrazení pak zobrazí data jako kód HTML pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="69354-196">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="69354-197">V příkladu výše jsme použili `ViewBag` objekt k předávání dat z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-197">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="69354-198">Druhá možnost v tomto kurzu budeme používat model zobrazení k předání dat z kontroleru zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-198">Latter in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="69354-199">Přístup modelu zobrazení k předávání dat je mnohem obecně upřednostňované nad přístup kontejner objektů a dat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="69354-199">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="69354-200">Naleznete v příspěvku blogu [V silně typované zobrazení dynamické](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) Další informace.</span><span class="sxs-lookup"><span data-stu-id="69354-200">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span>

<span data-ttu-id="69354-201">Kontejneru, který byl typ z &quot;M&quot; pro model, ale není typ databáze.</span><span class="sxs-lookup"><span data-stu-id="69354-201">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="69354-202">Pojďme se na to co jsme se naučili a vytvořit databázi videa.</span><span class="sxs-lookup"><span data-stu-id="69354-202">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="69354-203">[Předchozí](adding-a-controller.md)
> [další](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="69354-203">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>