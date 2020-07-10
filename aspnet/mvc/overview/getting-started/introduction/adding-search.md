---
uid: mvc/overview/getting-started/introduction/adding-search
title: Hledat | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/17/2019
ms.assetid: df001954-18bf-4550-b03d-43911a0ea186
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-search
msc.type: authoredcontent
ms.openlocfilehash: f6d6d32a648fed453be924790a1b55698c9cf209
ms.sourcegitcommit: 0d583ed9253103f3e50b6d729276e667591cdd41
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211477"
---
# <a name="search"></a><span data-ttu-id="71d41-102">Search</span><span class="sxs-lookup"><span data-stu-id="71d41-102">Search</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="adding-a-search-method-and-search-view"></a><span data-ttu-id="71d41-103">Přidání vyhledávací metody a zobrazení vyhledávání</span><span class="sxs-lookup"><span data-stu-id="71d41-103">Adding a Search Method and Search View</span></span>

<span data-ttu-id="71d41-104">V této části přidáte funkci hledání do `Index` metody Action, která umožňuje hledat filmy podle žánru nebo názvu.</span><span class="sxs-lookup"><span data-stu-id="71d41-104">In this section you'll add search capability to the `Index` action method that lets you search movies by genre or name.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71d41-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="71d41-105">Prerequisites</span></span>

<span data-ttu-id="71d41-106">Aby bylo možné spárovat snímky obrazovky této části, je nutné spustit aplikaci (F5) a přidat následující filmy do databáze.</span><span class="sxs-lookup"><span data-stu-id="71d41-106">To match this section's screenshots, you need to run the application (F5) and add the following movies to the database.</span></span>

| <span data-ttu-id="71d41-107">Nadpis</span><span class="sxs-lookup"><span data-stu-id="71d41-107">Title</span></span> | <span data-ttu-id="71d41-108">Datum vydání</span><span class="sxs-lookup"><span data-stu-id="71d41-108">Release Date</span></span> | <span data-ttu-id="71d41-109">Žánru</span><span class="sxs-lookup"><span data-stu-id="71d41-109">Genre</span></span> | <span data-ttu-id="71d41-110">Cena</span><span class="sxs-lookup"><span data-stu-id="71d41-110">Price</span></span> |
| ----- | ------------ | ----- | ----- |
| <span data-ttu-id="71d41-111">Ghostbusters</span><span class="sxs-lookup"><span data-stu-id="71d41-111">Ghostbusters</span></span> | <span data-ttu-id="71d41-112">6/8/1984</span><span class="sxs-lookup"><span data-stu-id="71d41-112">6/8/1984</span></span> | <span data-ttu-id="71d41-113">Komedie</span><span class="sxs-lookup"><span data-stu-id="71d41-113">Comedy</span></span> | <span data-ttu-id="71d41-114">6,99</span><span class="sxs-lookup"><span data-stu-id="71d41-114">6.99</span></span> |
| <span data-ttu-id="71d41-115">Ghostbusters II</span><span class="sxs-lookup"><span data-stu-id="71d41-115">Ghostbusters II</span></span> | <span data-ttu-id="71d41-116">6/16/1989</span><span class="sxs-lookup"><span data-stu-id="71d41-116">6/16/1989</span></span> | <span data-ttu-id="71d41-117">Komedie</span><span class="sxs-lookup"><span data-stu-id="71d41-117">Comedy</span></span> | <span data-ttu-id="71d41-118">6,99</span><span class="sxs-lookup"><span data-stu-id="71d41-118">6.99</span></span> |
| <span data-ttu-id="71d41-119">Globálním Apes</span><span class="sxs-lookup"><span data-stu-id="71d41-119">Planet of the Apes</span></span> | <span data-ttu-id="71d41-120">3/27/1986</span><span class="sxs-lookup"><span data-stu-id="71d41-120">3/27/1986</span></span> | <span data-ttu-id="71d41-121">Akce</span><span class="sxs-lookup"><span data-stu-id="71d41-121">Action</span></span> | <span data-ttu-id="71d41-122">5.99</span><span class="sxs-lookup"><span data-stu-id="71d41-122">5.99</span></span> |

## <a name="updating-the-index-form"></a><span data-ttu-id="71d41-123">Aktualizace formuláře indexu</span><span class="sxs-lookup"><span data-stu-id="71d41-123">Updating the Index Form</span></span>

<span data-ttu-id="71d41-124">Začněte aktualizací `Index` metody Action na existující `MoviesController` třídu.</span><span class="sxs-lookup"><span data-stu-id="71d41-124">Start by updating the `Index` action method to the existing `MoviesController` class.</span></span> <span data-ttu-id="71d41-125">Zde je kód:</span><span class="sxs-lookup"><span data-stu-id="71d41-125">Here's the code:</span></span>

[!code-csharp[Main](adding-search/samples/sample1.cs?highlight=1,6-9)]

<span data-ttu-id="71d41-126">První řádek `Index` metody vytvoří následující dotaz [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) pro výběr filmů:</span><span class="sxs-lookup"><span data-stu-id="71d41-126">The first line of the `Index` method creates the following [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) query to select the movies:</span></span>

[!code-csharp[Main](adding-search/samples/sample2.cs)]

<span data-ttu-id="71d41-127">V tomto okamžiku je definován dotaz, ale ještě nebyl v databázi spuštěn.</span><span class="sxs-lookup"><span data-stu-id="71d41-127">The query is defined at this point, but hasn't yet been run against the database.</span></span>

<span data-ttu-id="71d41-128">Pokud `searchString` parametr obsahuje řetězec, dotaz na filmy je upraven pro filtrování podle hodnoty hledaného řetězce, a to pomocí následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="71d41-128">If the `searchString` parameter contains a string, the movies query is modified to filter on the value of the search string, using the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample3.cs)]

<span data-ttu-id="71d41-129">`s => s.Title`Výše uvedený kód je [výraz lambda](https://msdn.microsoft.com/library/bb397687.aspx).</span><span class="sxs-lookup"><span data-stu-id="71d41-129">The `s => s.Title` code above is a [Lambda Expression](https://msdn.microsoft.com/library/bb397687.aspx).</span></span> <span data-ttu-id="71d41-130">Výrazy lambda se používají v dotazech [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) založených na metodách jako argumenty standardních metod operátoru dotazu, jako je metoda [WHERE](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) použitá ve výše uvedeném kódu.</span><span class="sxs-lookup"><span data-stu-id="71d41-130">Lambdas are used in method-based [LINQ](https://msdn.microsoft.com/library/bb397926.aspx) queries as arguments to standard query operator methods such as the [Where](https://msdn.microsoft.com/library/system.linq.enumerable.where.aspx) method used in the above code.</span></span> <span data-ttu-id="71d41-131">Dotazy LINQ nejsou provedeny při jejich definování nebo při jejich úpravě voláním metody, jako je `Where` nebo `OrderBy` .</span><span class="sxs-lookup"><span data-stu-id="71d41-131">LINQ queries are not executed when they are defined or when they are modified by calling a method such as `Where` or `OrderBy`.</span></span> <span data-ttu-id="71d41-132">Místo toho je provádění dotazu odloženo, což znamená, že vyhodnocení výrazu je zpožděno, dokud se jeho realizovaná hodnota neopakuje nebo je [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) volána metoda.</span><span class="sxs-lookup"><span data-stu-id="71d41-132">Instead, query execution is deferred, which means that the evaluation of an expression is delayed until its realized value is actually iterated over or the [`ToList`](https://msdn.microsoft.com/library/bb342261.aspx) method is called.</span></span> <span data-ttu-id="71d41-133">V `Search` ukázce je dotaz spuštěn v zobrazení *index. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="71d41-133">In the `Search` sample, the query is executed in the *Index.cshtml* view.</span></span> <span data-ttu-id="71d41-134">Další informace o odložení provádění dotazů naleznete v tématu [provádění dotazů](https://msdn.microsoft.com/library/bb738633.aspx).</span><span class="sxs-lookup"><span data-stu-id="71d41-134">For more information about deferred query execution, see [Query Execution](https://msdn.microsoft.com/library/bb738633.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="71d41-135">Metoda [Contains](https://msdn.microsoft.com/library/bb155125.aspx) je spuštěna v databázi, nikoli kód jazyka c# výše.</span><span class="sxs-lookup"><span data-stu-id="71d41-135">The [Contains](https://msdn.microsoft.com/library/bb155125.aspx) method is run on the database, not the c# code above.</span></span> <span data-ttu-id="71d41-136">V databázi [obsahuje](https://msdn.microsoft.com/library/bb155125.aspx) mapy [typu SQL jako](https://msdn.microsoft.com/library/ms179859.aspx), což rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="71d41-136">On the database, [Contains](https://msdn.microsoft.com/library/bb155125.aspx) maps to [SQL LIKE](https://msdn.microsoft.com/library/ms179859.aspx), which is case insensitive.</span></span>

<span data-ttu-id="71d41-137">Nyní můžete aktualizovat `Index` zobrazení, které zobrazí formulář uživateli.</span><span class="sxs-lookup"><span data-stu-id="71d41-137">Now you can update the `Index` view that will display the form to the user.</span></span>

<span data-ttu-id="71d41-138">Spusťte aplikaci a přejděte na */Movies/index*.</span><span class="sxs-lookup"><span data-stu-id="71d41-138">Run the application and navigate to */Movies/Index*.</span></span> <span data-ttu-id="71d41-139">Připojit řetězec dotazu, například `?searchString=ghost` k adrese URL.</span><span class="sxs-lookup"><span data-stu-id="71d41-139">Append a query string such as `?searchString=ghost` to the URL.</span></span> <span data-ttu-id="71d41-140">Zobrazí se filtrované filmy.</span><span class="sxs-lookup"><span data-stu-id="71d41-140">The filtered movies are displayed.</span></span>

![SearchQryStr](adding-search/_static/image1.png)

<span data-ttu-id="71d41-142">Změníte-li podpis `Index` metody tak, aby měl parametr s názvem `id` , `id` parametr bude odpovídat `{id}` zástupnému symbolu pro výchozí trasy nastavené v souboru *App \_ Start\RouteConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="71d41-142">If you change the signature of the `Index` method to have a parameter named `id`, the `id` parameter will match the `{id}` placeholder for the default routes set in the *App\_Start\RouteConfig.cs* file.</span></span>

[!code-json[Main](adding-search/samples/sample4.json)]

<span data-ttu-id="71d41-143">Původní `Index` metoda vypadá takto::</span><span class="sxs-lookup"><span data-stu-id="71d41-143">The original `Index` method looks like this::</span></span>

[!code-csharp[Main](adding-search/samples/sample5.cs)]

<span data-ttu-id="71d41-144">Upravená `Index` Metoda by vypadala takto:</span><span class="sxs-lookup"><span data-stu-id="71d41-144">The modified `Index` method would look as follows:</span></span>

[!code-csharp[Main](adding-search/samples/sample6.cs?highlight=1,3)]

<span data-ttu-id="71d41-145">Nyní můžete název hledání předat jako data trasy (segment adresy URL) místo jako hodnotu řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="71d41-145">You can now pass the search title as route data (a URL segment) instead of as a query string value.</span></span>

![](adding-search/_static/image2.png)

<span data-ttu-id="71d41-146">Nemůžete ale očekávat, že uživatelé můžou upravovat adresu URL pokaždé, když chtějí hledat film.</span><span class="sxs-lookup"><span data-stu-id="71d41-146">However, you can't expect users to modify the URL every time they want to search for a movie.</span></span> <span data-ttu-id="71d41-147">Takže teď přidáte uživatelské rozhraní, které jim umožní filtrovat filmy.</span><span class="sxs-lookup"><span data-stu-id="71d41-147">So now you'll add UI to help them filter movies.</span></span> <span data-ttu-id="71d41-148">Pokud jste změnili podpis `Index` metody pro testování způsobu předání parametru ID vázaného na trasu, změňte jej tak, aby `Index` Metoda přebírá řetězcový parametr s názvem `searchString` :</span><span class="sxs-lookup"><span data-stu-id="71d41-148">If you changed the signature of the `Index` method to test how to pass the route-bound ID parameter, change it back so that your `Index` method takes a string parameter named `searchString`:</span></span>

[!code-csharp[Main](adding-search/samples/sample7.cs)]

<span data-ttu-id="71d41-149">Otevřete soubor *Views\Movies\Index.cshtml* a hned za `@Html.ActionLink("Create New", "Create")` přidejte značku formuláře zvýrazněné níže:</span><span class="sxs-lookup"><span data-stu-id="71d41-149">Open the *Views\Movies\Index.cshtml* file, and just after `@Html.ActionLink("Create New", "Create")`, add the form markup highlighted below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample8.cshtml?highlight=12-15)]

<span data-ttu-id="71d41-150">`Html.BeginForm`Pomocná rutina vytvoří počáteční `<form>` značku.</span><span class="sxs-lookup"><span data-stu-id="71d41-150">The `Html.BeginForm` helper creates an opening `<form>` tag.</span></span> <span data-ttu-id="71d41-151">`Html.BeginForm`Pomocná osoba způsobí odeslání formuláře do sebe sama, když ho uživatel odešle kliknutím na tlačítko **Filtr** .</span><span class="sxs-lookup"><span data-stu-id="71d41-151">The `Html.BeginForm` helper causes the form to post to itself when the user submits the form by clicking the **Filter** button.</span></span>

<span data-ttu-id="71d41-152">Při zobrazení a úpravách souborů zobrazení má Visual Studio 2013 dobrým vylepšením.</span><span class="sxs-lookup"><span data-stu-id="71d41-152">Visual Studio 2013 has a nice improvement when displaying and editing View files.</span></span> <span data-ttu-id="71d41-153">Když aplikaci spustíte s otevřeným zobrazením souboru, Visual Studio 2013 vyvolá správnou metodu akce kontroleru pro zobrazení zobrazení.</span><span class="sxs-lookup"><span data-stu-id="71d41-153">When you run the application with a view file open, Visual Studio 2013 invokes the correct controller action method to display the view.</span></span>

![](adding-search/_static/image3.png)

<span data-ttu-id="71d41-154">Otevřete zobrazení index v aplikaci Visual Studio (jak je znázorněno na obrázku výše), klepnutím na centrum F5 nebo F5 spusťte aplikaci a potom zkuste vyhledat film.</span><span class="sxs-lookup"><span data-stu-id="71d41-154">With the Index view open in Visual Studio (as shown in the image above), tap Ctr F5 or F5 to run the application and then try searching for a movie.</span></span>

![](adding-search/_static/image4.png)

<span data-ttu-id="71d41-155">Neexistuje `HttpPost` přetížení `Index` metody.</span><span class="sxs-lookup"><span data-stu-id="71d41-155">There's no `HttpPost` overload of the `Index` method.</span></span> <span data-ttu-id="71d41-156">Nepotřebujete ho, protože metoda nemění stav aplikace, stačí data filtrovat.</span><span class="sxs-lookup"><span data-stu-id="71d41-156">You don't need it, because the method isn't changing the state of the application, just filtering data.</span></span>

<span data-ttu-id="71d41-157">Můžete přidat následující `HttpPost Index` metodu.</span><span class="sxs-lookup"><span data-stu-id="71d41-157">You could add the following `HttpPost Index` method.</span></span> <span data-ttu-id="71d41-158">V takovém případě by se akce původce shodovala s `HttpPost Index` metodou a `HttpPost Index` Metoda by běžela, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="71d41-158">In that case, the action invoker would match the `HttpPost Index` method, and the `HttpPost Index` method would run as shown in the image below.</span></span>

[!code-csharp[Main](adding-search/samples/sample9.cs)]

![SearchPostGhost](adding-search/_static/image5.png)

<span data-ttu-id="71d41-160">Nicméně i v případě, že přidáte tuto `HttpPost` verzi `Index` metody, existuje omezení, jak je vše implementováno.</span><span class="sxs-lookup"><span data-stu-id="71d41-160">However, even if you add this `HttpPost` version of the `Index` method, there's a limitation in how this has all been implemented.</span></span> <span data-ttu-id="71d41-161">Představte si, že chcete vytvořit záložku konkrétního hledání nebo chcete poslat odkaz na přátele, na které můžou kliknout, aby se zobrazil stejný filtrovaný seznam filmů.</span><span class="sxs-lookup"><span data-stu-id="71d41-161">Imagine that you want to bookmark a particular search or you want to send a link to friends that they can click in order to see the same filtered list of movies.</span></span> <span data-ttu-id="71d41-162">Všimněte si, že adresa URL požadavku HTTP POST je stejná jako adresa URL žádosti GET (localhost: xxxxx/video/index) – v samotné adrese URL nejsou žádné vyhledávací informace.</span><span class="sxs-lookup"><span data-stu-id="71d41-162">Notice that the URL for the HTTP POST request is the same as the URL for the GET request (localhost:xxxxx/Movies/Index) -- there's no search information in the URL itself.</span></span> <span data-ttu-id="71d41-163">Nyní jsou informace o hledaném řetězci odesílány na server jako hodnota pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="71d41-163">Right now, the search string information is sent to the server as a form field value.</span></span> <span data-ttu-id="71d41-164">To znamená, že nemůžete zachytit informace o hledání do záložky nebo odeslat přátelům v adrese URL.</span><span class="sxs-lookup"><span data-stu-id="71d41-164">This means you can't capture that search information to bookmark or send to friends in a URL.</span></span>

<span data-ttu-id="71d41-165">Řešením je použití přetížení `BeginForm` , které určuje, že žádost post by měla do adresy URL přidat informace o hledání a že by měla být směrována na `HttpGet` verzi `Index` metody.</span><span class="sxs-lookup"><span data-stu-id="71d41-165">The solution is to use an overload of `BeginForm` that specifies that the POST request should add the search information to the URL and that it should be routed to the `HttpGet` version of the `Index` method.</span></span> <span data-ttu-id="71d41-166">Nahraďte existující metodu bez parametrů `BeginForm` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="71d41-166">Replace the existing parameterless `BeginForm` method with the following markup:</span></span>

[!code-cshtml[Main](adding-search/samples/sample10.cshtml)]

![BeginFormPost_SM](adding-search/_static/image6.png)

<span data-ttu-id="71d41-168">Když teď odešlete hledání, adresa URL obsahuje řetězec vyhledávacího dotazu.</span><span class="sxs-lookup"><span data-stu-id="71d41-168">Now when you submit a search, the URL contains a search query string.</span></span> <span data-ttu-id="71d41-169">Hledání bude také jít na `HttpGet Index` metodu Action, i když máte `HttpPost Index` metodu.</span><span class="sxs-lookup"><span data-stu-id="71d41-169">Searching will also go to the `HttpGet Index` action method, even if you have a `HttpPost Index` method.</span></span>

![IndexWithGetURL](adding-search/_static/image7.png)

## <a name="adding-search-by-genre"></a><span data-ttu-id="71d41-171">Přidávání hledání podle žánru</span><span class="sxs-lookup"><span data-stu-id="71d41-171">Adding Search by Genre</span></span>

<span data-ttu-id="71d41-172">Pokud jste přidali `HttpPost` verzi `Index` metody, odstraňte ji nyní.</span><span class="sxs-lookup"><span data-stu-id="71d41-172">If you added the `HttpPost` version of the `Index` method, delete it now.</span></span>

<span data-ttu-id="71d41-173">V dalším kroku přidáte funkci, která uživatelům umožní Hledat filmy podle žánru.</span><span class="sxs-lookup"><span data-stu-id="71d41-173">Next, you'll add a feature to let users search for movies by genre.</span></span> <span data-ttu-id="71d41-174">Nahraďte metodu `Index` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="71d41-174">Replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](adding-search/samples/sample11.cs)]

<span data-ttu-id="71d41-175">Tato verze `Index` metody přebírá další parametr, konkrétně `movieGenre` .</span><span class="sxs-lookup"><span data-stu-id="71d41-175">This version of the `Index` method takes an additional parameter, namely `movieGenre`.</span></span> <span data-ttu-id="71d41-176">První pár řádků kódu vytvoří `List` objekt pro uchování filmových žánrů z databáze.</span><span class="sxs-lookup"><span data-stu-id="71d41-176">The first few lines of code create a `List` object to hold movie genres from the database.</span></span>

<span data-ttu-id="71d41-177">Následující kód je dotaz LINQ, který načte všechny žánry z databáze.</span><span class="sxs-lookup"><span data-stu-id="71d41-177">The following code is a LINQ query that retrieves all the genres from the database.</span></span>

[!code-csharp[Main](adding-search/samples/sample12.cs)]

<span data-ttu-id="71d41-178">Kód používá `AddRange` metodu obecné `List` kolekce k přidání všech různých žánrů do seznamu.</span><span class="sxs-lookup"><span data-stu-id="71d41-178">The code uses the `AddRange` method of the generic `List` collection to add all the distinct genres to the list.</span></span> <span data-ttu-id="71d41-179">(Bez `Distinct` modifikátoru by se přidaly duplicitní žánry – například komedie by se přidalo dvakrát v našem příkladu).</span><span class="sxs-lookup"><span data-stu-id="71d41-179">(Without the `Distinct` modifier, duplicate genres would be added — for example, comedy would be added twice in our sample).</span></span> <span data-ttu-id="71d41-180">Kód pak uloží seznam žánrů v `ViewBag.MovieGenre` objektu.</span><span class="sxs-lookup"><span data-stu-id="71d41-180">The code then stores the list of genres in the `ViewBag.MovieGenre` object.</span></span> <span data-ttu-id="71d41-181">Při ukládání dat kategorií (například filmových žánrů) jako objektu [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) do `ViewBag` pole je přístup k datům kategorie v rozevíracím seznamu typický pro aplikace MVC.</span><span class="sxs-lookup"><span data-stu-id="71d41-181">Storing category data (such a movie genres) as a [SelectList](https://msdn.microsoft.cus/library/system.web.mvc.selectlist(v=vs.108).aspx) object in a `ViewBag`, then accessing the category data in a dropdown list box is a typical approach for MVC applications.</span></span>

<span data-ttu-id="71d41-182">Následující kód ukazuje, jak ověřit `movieGenre` parametr.</span><span class="sxs-lookup"><span data-stu-id="71d41-182">The following code shows how to check the `movieGenre` parameter.</span></span> <span data-ttu-id="71d41-183">Pokud není prázdný, kód dál omezí dotaz na filmy, aby vybral vybrané filmy na zadaný Žánr.</span><span class="sxs-lookup"><span data-stu-id="71d41-183">If it's not empty, the code further constrains the movies query to limit the selected movies to the specified genre.</span></span>

[!code-csharp[Main](adding-search/samples/sample13.cs)]

<span data-ttu-id="71d41-184">Jak bylo uvedeno dříve, dotaz není spuštěn v databázi, dokud se seznam filmů neopakuje (k tomu dojde v zobrazení, po `Index` návratu metody Action).</span><span class="sxs-lookup"><span data-stu-id="71d41-184">As stated previously, the query is not run on the database until the movie list is iterated over (which happens in the View, after the `Index` action method returns).</span></span>

## <a name="adding-markup-to-the-index-view-to-support-search-by-genre"></a><span data-ttu-id="71d41-185">Přidání značek do zobrazení indexu pro podporu hledání podle žánru</span><span class="sxs-lookup"><span data-stu-id="71d41-185">Adding Markup to the Index View to Support Search by Genre</span></span>

<span data-ttu-id="71d41-186">Přidejte `Html.DropDownList` pomocníka do souboru *Views\Movies\Index.cshtml* těsně před `TextBox` pomocnou rutinou.</span><span class="sxs-lookup"><span data-stu-id="71d41-186">Add an `Html.DropDownList` helper to the *Views\Movies\Index.cshtml* file, just before the `TextBox` helper.</span></span> <span data-ttu-id="71d41-187">Dokončený kód je uveden níže:</span><span class="sxs-lookup"><span data-stu-id="71d41-187">The completed markup is shown below:</span></span>

[!code-cshtml[Main](adding-search/samples/sample14.cshtml?highlight=11)]

<span data-ttu-id="71d41-188">V následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="71d41-188">In the following code:</span></span>

[!code-cshtml[Main](adding-search/samples/sample15.cshtml)]

<span data-ttu-id="71d41-189">Parametr "MovieGenre" poskytuje klíč, pomocí kterého může `DropDownList` Pomocník najít `IEnumerable<SelectListItem>` v `ViewBag` .</span><span class="sxs-lookup"><span data-stu-id="71d41-189">The parameter "MovieGenre" provides the key for the `DropDownList` helper to find a `IEnumerable<SelectListItem>` in the `ViewBag`.</span></span> <span data-ttu-id="71d41-190">`ViewBag`Byla naplněna v metodě Action:</span><span class="sxs-lookup"><span data-stu-id="71d41-190">The `ViewBag` was populated in the action method:</span></span>

[!code-csharp[Main](adding-search/samples/sample16.cs?highlight=10)]

<span data-ttu-id="71d41-191">Parametr all poskytuje popisek možnosti.</span><span class="sxs-lookup"><span data-stu-id="71d41-191">The parameter "All" provides an option label.</span></span> <span data-ttu-id="71d41-192">Pokud v prohlížeči zkontrolujete tuto volbu, uvidíte, že její atribut "value" je prázdný.</span><span class="sxs-lookup"><span data-stu-id="71d41-192">If you inspect that choice in your browser, you'll see that its "value" attribute is empty.</span></span> <span data-ttu-id="71d41-193">Vzhledem k tomu, že náš řadič filtruje pouze `if` řetězec `null` , není ani prázdný, odesláním prázdné hodnoty `movieGenre` zobrazíte všechny žánry.</span><span class="sxs-lookup"><span data-stu-id="71d41-193">Since our controller only filters `if` the string is not `null` or empty, submitting an empty value for `movieGenre` shows all genres.</span></span>

<span data-ttu-id="71d41-194">Můžete také nastavit možnost, která bude standardně vybrána.</span><span class="sxs-lookup"><span data-stu-id="71d41-194">You can also set an option to be selected by default.</span></span> <span data-ttu-id="71d41-195">Pokud jste jako výchozí možnost chtěli "komedie", změnili byste kód v řadiči, například:</span><span class="sxs-lookup"><span data-stu-id="71d41-195">If you wanted "Comedy" as your default option, you would change the code in the Controller like so:</span></span>

[!code-cshtml[Main](adding-search/samples/sample17.cshtml)]

<span data-ttu-id="71d41-196">Spusťte aplikaci a přejděte na */Movies/index*.</span><span class="sxs-lookup"><span data-stu-id="71d41-196">Run the application and browse to */Movies/Index*.</span></span> <span data-ttu-id="71d41-197">Zkuste hledat podle žánru, podle názvu filmu a podle obou kritérií.</span><span class="sxs-lookup"><span data-stu-id="71d41-197">Try a search by genre, by movie name, and by both criteria.</span></span>

![](adding-search/_static/image8.png)

<span data-ttu-id="71d41-198">V této části jste vytvořili metodu a zobrazení akce hledání, které umožní uživatelům hledat podle názvu a žánru.</span><span class="sxs-lookup"><span data-stu-id="71d41-198">In this section you created a search action method and view that let users search by movie title and genre.</span></span> <span data-ttu-id="71d41-199">V další části se podíváte na postup přidání vlastnosti do `Movie` modelu a postup přidání inicializátoru, který automaticky vytvoří testovací databázi.</span><span class="sxs-lookup"><span data-stu-id="71d41-199">In the next section, you'll look at how to add a property to the `Movie` model and how to add an initializer that will automatically create a test database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="71d41-200">[Předchozí](examining-the-edit-methods-and-edit-view.md) 
>  [Další](adding-a-new-field.md)</span><span class="sxs-lookup"><span data-stu-id="71d41-200">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-a-new-field.md)</span></span>
