---
uid: web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
title: Vytvoření REST API s směrováním atributů ve webovém rozhraní API 2 pro ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2013
ms.assetid: 23fc77da-2725-4434-99a0-ff872d96336b
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing
msc.type: authoredcontent
ms.openlocfilehash: 6eac36767bf34857d5341188d0653e7fec7cade2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "86188796"
---
# <a name="create-a-rest-api-with-attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="7d79a-102">Vytvoření REST API s směrováním atributů ve webovém rozhraní API 2 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7d79a-102">Create a REST API with Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="7d79a-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7d79a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7d79a-104">Webové rozhraní API 2 podporuje nový typ směrování, kterému se říká *Směrování atributů*.</span><span class="sxs-lookup"><span data-stu-id="7d79a-104">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="7d79a-105">Obecný přehled směrování atributů najdete v tématu [Směrování atributů ve webovém rozhraní API 2](attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="7d79a-105">For a general overview of attribute routing, see [Attribute Routing in Web API 2](attribute-routing-in-web-api-2.md).</span></span> <span data-ttu-id="7d79a-106">V tomto kurzu budete používat směrování atributů k vytvoření REST API pro kolekci knih.</span><span class="sxs-lookup"><span data-stu-id="7d79a-106">In this tutorial, you will use attribute routing to create a REST API for a collection of books.</span></span> <span data-ttu-id="7d79a-107">Rozhraní API bude podporovat tyto akce:</span><span class="sxs-lookup"><span data-stu-id="7d79a-107">The API will support the following actions:</span></span>

| <span data-ttu-id="7d79a-108">Akce</span><span class="sxs-lookup"><span data-stu-id="7d79a-108">Action</span></span> | <span data-ttu-id="7d79a-109">Příklad identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="7d79a-109">Example URI</span></span> |
| --- | --- |
| <span data-ttu-id="7d79a-110">Získá seznam všech knih.</span><span class="sxs-lookup"><span data-stu-id="7d79a-110">Get a list of all books.</span></span> | <span data-ttu-id="7d79a-111">/api/books</span><span class="sxs-lookup"><span data-stu-id="7d79a-111">/api/books</span></span> |
| <span data-ttu-id="7d79a-112">Získat knihu podle ID</span><span class="sxs-lookup"><span data-stu-id="7d79a-112">Get a book by ID.</span></span> | <span data-ttu-id="7d79a-113">/api/books/1</span><span class="sxs-lookup"><span data-stu-id="7d79a-113">/api/books/1</span></span> |
| <span data-ttu-id="7d79a-114">Získejte podrobnosti knihy.</span><span class="sxs-lookup"><span data-stu-id="7d79a-114">Get the details of a book.</span></span> | <span data-ttu-id="7d79a-115">/api/books/1/details</span><span class="sxs-lookup"><span data-stu-id="7d79a-115">/api/books/1/details</span></span> |
| <span data-ttu-id="7d79a-116">Získá seznam knih podle žánru.</span><span class="sxs-lookup"><span data-stu-id="7d79a-116">Get a list of books by genre.</span></span> | <span data-ttu-id="7d79a-117">/api/books/fantasy</span><span class="sxs-lookup"><span data-stu-id="7d79a-117">/api/books/fantasy</span></span> |
| <span data-ttu-id="7d79a-118">Získá seznam knih podle data publikování.</span><span class="sxs-lookup"><span data-stu-id="7d79a-118">Get a list of books by publication date.</span></span> | <span data-ttu-id="7d79a-119">/API/Books/Date/2013-02-16/API/Books/Date/2013/02/16 (alternativní formulář)</span><span class="sxs-lookup"><span data-stu-id="7d79a-119">/api/books/date/2013-02-16 /api/books/date/2013/02/16 (alternate form)</span></span> |
| <span data-ttu-id="7d79a-120">Získá seznam knih podle konkrétního autora.</span><span class="sxs-lookup"><span data-stu-id="7d79a-120">Get a list of books by a particular author.</span></span> | <span data-ttu-id="7d79a-121">/api/authors/1/books</span><span class="sxs-lookup"><span data-stu-id="7d79a-121">/api/authors/1/books</span></span> |

<span data-ttu-id="7d79a-122">Všechny metody jsou jen pro čtení (požadavky HTTP GET).</span><span class="sxs-lookup"><span data-stu-id="7d79a-122">All methods are read-only (HTTP GET requests).</span></span>

<span data-ttu-id="7d79a-123">Pro datovou vrstvu budeme používat Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7d79a-123">For the data layer, we'll use Entity Framework.</span></span> <span data-ttu-id="7d79a-124">Záznamy o knihách budou obsahovat následující pole:</span><span class="sxs-lookup"><span data-stu-id="7d79a-124">Book records will have the following fields:</span></span>

- <span data-ttu-id="7d79a-125">ID</span><span class="sxs-lookup"><span data-stu-id="7d79a-125">ID</span></span>
- <span data-ttu-id="7d79a-126">Nadpis</span><span class="sxs-lookup"><span data-stu-id="7d79a-126">Title</span></span>
- <span data-ttu-id="7d79a-127">Žánru</span><span class="sxs-lookup"><span data-stu-id="7d79a-127">Genre</span></span>
- <span data-ttu-id="7d79a-128">Datum publikace</span><span class="sxs-lookup"><span data-stu-id="7d79a-128">Publication date</span></span>
- <span data-ttu-id="7d79a-129">Cena</span><span class="sxs-lookup"><span data-stu-id="7d79a-129">Price</span></span>
- <span data-ttu-id="7d79a-130">Popis</span><span class="sxs-lookup"><span data-stu-id="7d79a-130">Description</span></span>
- <span data-ttu-id="7d79a-131">AuthorID (cizí klíč pro tabulku autorů)</span><span class="sxs-lookup"><span data-stu-id="7d79a-131">AuthorID (foreign key to an Authors table)</span></span>

<span data-ttu-id="7d79a-132">Pro většinu požadavků ale rozhraní API vrátí podmnožinu těchto dat (název, autor a Žánr).</span><span class="sxs-lookup"><span data-stu-id="7d79a-132">For most requests, however, the API will return a subset of this data (title, author, and genre).</span></span> <span data-ttu-id="7d79a-133">Chcete-li získat úplný záznam, požadavky klienta `/api/books/{id}/details` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-133">To get the complete record, the client requests `/api/books/{id}/details`.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d79a-134">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7d79a-134">Prerequisites</span></span>

<span data-ttu-id="7d79a-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7d79a-135">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="7d79a-136">Vytvoření projektu sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d79a-136">Create the Visual Studio Project</span></span>

<span data-ttu-id="7d79a-137">Začněte spuštěním sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d79a-137">Start by running Visual Studio.</span></span> <span data-ttu-id="7d79a-138">V nabídce **soubor** vyberte **Nový** a pak vyberte **projekt**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-138">From the **File** menu, select **New** and then select **Project**.</span></span>

<span data-ttu-id="7d79a-139">Rozbalte položku **nainstalovanou**  >  kategorii**Visual C#** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-139">Expand the **Installed** > **Visual C#** category.</span></span> <span data-ttu-id="7d79a-140">V části **Visual C#** vyberte **Web**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-140">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="7d79a-141">V seznamu šablon projektu vyberte **ASP.NET webová aplikace (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-141">In the list of project templates, select **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="7d79a-142">Pojmenujte projekt &quot; BooksAPI &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-142">Name the project &quot;BooksAPI&quot;.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image1.png)

<span data-ttu-id="7d79a-143">V dialogovém okně **Nová webová aplikace ASP.NET** vyberte **prázdnou** šablonu.</span><span class="sxs-lookup"><span data-stu-id="7d79a-143">In the **New ASP.NET Web Application** dialog, select the **Empty** template.</span></span> <span data-ttu-id="7d79a-144">V části Přidat složky a základní reference pro klikněte zaškrtněte políčko **webové rozhraní API** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-144">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="7d79a-145">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-145">Click **OK**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image2.png)

<span data-ttu-id="7d79a-146">Tím se vytvoří kostra projektu, který je nakonfigurován pro funkce webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7d79a-146">This creates a skeleton project that is configured for Web API functionality.</span></span>

### <a name="domain-models"></a><span data-ttu-id="7d79a-147">Doménové modely</span><span class="sxs-lookup"><span data-stu-id="7d79a-147">Domain Models</span></span>

<span data-ttu-id="7d79a-148">Dále přidejte třídy pro doménové modely.</span><span class="sxs-lookup"><span data-stu-id="7d79a-148">Next, add classes for domain models.</span></span> <span data-ttu-id="7d79a-149">V Průzkumník řešení klikněte pravým tlačítkem na složku modely.</span><span class="sxs-lookup"><span data-stu-id="7d79a-149">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="7d79a-150">Vyberte **Přidat**a pak vybrat **třídu**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-150">Select **Add**, then select **Class**.</span></span> <span data-ttu-id="7d79a-151">Pojmenujte třídu `Author` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-151">Name the class `Author`.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image3.png)

<span data-ttu-id="7d79a-152">Nahraďte kód v Author.cs následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="7d79a-152">Replace the code in Author.cs with the following:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample1.cs)]

<span data-ttu-id="7d79a-153">Nyní přidejte další třídu s názvem `Book` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-153">Now add another class named `Book`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample2.cs)]

### <a name="add-a-web-api-controller"></a><span data-ttu-id="7d79a-154">Přidat kontroler webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="7d79a-154">Add a Web API Controller</span></span>

<span data-ttu-id="7d79a-155">V tomto kroku přidáme kontroler webového rozhraní API, který používá Entity Framework jako datovou vrstvu.</span><span class="sxs-lookup"><span data-stu-id="7d79a-155">In this step, we'll add a Web API controller that uses Entity Framework as the data layer.</span></span>

<span data-ttu-id="7d79a-156">Sestavte projekt stisknutím kombinace kláves CTRL+SHIFT+B.</span><span class="sxs-lookup"><span data-stu-id="7d79a-156">Press CTRL+SHIFT+B to build the project.</span></span> <span data-ttu-id="7d79a-157">Entity Framework používá reflexi ke zjištění vlastností modelů, takže vyžaduje zkompilované sestavení pro vytvoření schématu databáze.</span><span class="sxs-lookup"><span data-stu-id="7d79a-157">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

<span data-ttu-id="7d79a-158">V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers.</span><span class="sxs-lookup"><span data-stu-id="7d79a-158">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="7d79a-159">Vyberte **Přidat**a pak vybrat **kontroler**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-159">Select **Add**, then select **Controller**.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image4.png)

<span data-ttu-id="7d79a-160">V dialogovém okně **Přidat generování uživatelského rozhraní** vyberte **KONTROLER webového rozhraní API 2 s akcemi pomocí Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-160">In the **Add Scaffold** dialog, select **Web API 2 Controller with actions, using Entity Framework**.</span></span>

[![](create-a-rest-api-with-attribute-routing/_static/image6.png)](create-a-rest-api-with-attribute-routing/_static/image5.png)

<span data-ttu-id="7d79a-161">V dialogovém okně **Přidat řadič** jako **název kontroleru**zadejte &quot; BooksController &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-161">In the **Add Controller** dialog, for **Controller name**, enter &quot;BooksController&quot;.</span></span> <span data-ttu-id="7d79a-162">Zaškrtněte &quot; políčko použít akce asynchronního kontroleru &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-162">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="7d79a-163">V případě **třídy model**vyberte možnost &quot; Kniha &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-163">For **Model class**, select &quot;Book&quot;.</span></span> <span data-ttu-id="7d79a-164">(Pokud nevidíte `Book` třídu uvedenou v rozevíracím seznamu, ujistěte se, že jste projekt sestavili.) Pak klikněte na tlačítko "+".</span><span class="sxs-lookup"><span data-stu-id="7d79a-164">(If you don't see the `Book` class listed in the dropdown, make sure that you built the project.) Then click the "+" button.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image7.png)

<span data-ttu-id="7d79a-165">V dialogovém okně **nový kontext dat** klikněte na **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-165">Click **Add** in the **New Data Context** dialog.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image8.png)

<span data-ttu-id="7d79a-166">V dialogovém okně **Přidat řadič** klikněte na **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-166">Click **Add** in the **Add Controller** dialog.</span></span> <span data-ttu-id="7d79a-167">Generování uživatelského rozhraní přidá třídu s názvem `BooksController` , která definuje kontroler rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7d79a-167">The scaffolding adds a class named `BooksController` that defines the API controller.</span></span> <span data-ttu-id="7d79a-168">Přidá také třídu s názvem `BooksAPIContext` ve složce modely, která definuje kontext dat pro Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7d79a-168">It also adds a class named `BooksAPIContext` in the Models folder, which defines the data context for Entity Framework.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image9.png)

### <a name="seed-the-database"></a><span data-ttu-id="7d79a-169">Přidání dat do databáze</span><span class="sxs-lookup"><span data-stu-id="7d79a-169">Seed the Database</span></span>

<span data-ttu-id="7d79a-170">V nabídce Nástroje vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-170">From the Tools menu, select **NuGet Package Manager**, and then select **Package Manager Console**.</span></span>

<span data-ttu-id="7d79a-171">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7d79a-171">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample3.ps1)]

<span data-ttu-id="7d79a-172">Tento příkaz vytvoří složku migrace a přidá nový soubor kódu s názvem Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="7d79a-172">This command creates a Migrations folder and adds a new code file named Configuration.cs.</span></span> <span data-ttu-id="7d79a-173">Otevřete tento soubor a přidejte následující kód do `Configuration.Seed` metody.</span><span class="sxs-lookup"><span data-stu-id="7d79a-173">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample4.cs)]

<span data-ttu-id="7d79a-174">V okně konzoly Správce balíčků zadejte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="7d79a-174">In the Package Manager Console window, type the following commands.</span></span>

[!code-powershell[Main](create-a-rest-api-with-attribute-routing/samples/sample5.ps1)]

<span data-ttu-id="7d79a-175">Tyto příkazy vytvoří místní databázi a vyvolávají metodu počáteční hodnoty k naplnění databáze.</span><span class="sxs-lookup"><span data-stu-id="7d79a-175">These commands create a local database and invoke the Seed method to populate the database.</span></span>

![](create-a-rest-api-with-attribute-routing/_static/image10.png)

## <a name="add-dto-classes"></a><span data-ttu-id="7d79a-176">Přidat třídy DTO</span><span class="sxs-lookup"><span data-stu-id="7d79a-176">Add DTO Classes</span></span>

<span data-ttu-id="7d79a-177">Pokud aplikaci teď spustíte a odešlete požadavek GET na/API/Books/1, odpověď vypadá podobně jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="7d79a-177">If you run the application now and send a GET request to /api/books/1, the response looks similar to the following.</span></span> <span data-ttu-id="7d79a-178">(Přidal (a) jsem odsazení pro čitelnost.)</span><span class="sxs-lookup"><span data-stu-id="7d79a-178">(I added indentation for readability.)</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample6.json)]

<span data-ttu-id="7d79a-179">Místo toho chci, aby tento požadavek vrátil podmnožinu polí.</span><span class="sxs-lookup"><span data-stu-id="7d79a-179">Instead, I want this request to return a subset of the fields.</span></span> <span data-ttu-id="7d79a-180">Také chci, aby vracel jméno autora, nikoli ID autora.</span><span class="sxs-lookup"><span data-stu-id="7d79a-180">Also, I want it to return the author's name, rather than the author ID.</span></span> <span data-ttu-id="7d79a-181">K tomuto účelu upraví metody kontroleru tak, aby vracely *objekt pro přenos dat* (DTO) místo modelu EF.</span><span class="sxs-lookup"><span data-stu-id="7d79a-181">To accomplish this, we'll modify the controller methods to return a *data transfer object* (DTO) instead of the EF model.</span></span> <span data-ttu-id="7d79a-182">DTO je objekt, který je určen pouze k přenosu dat.</span><span class="sxs-lookup"><span data-stu-id="7d79a-182">A DTO is an object that is designed only to carry data.</span></span>

<span data-ttu-id="7d79a-183">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **Přidat**  |  **novou složku**.</span><span class="sxs-lookup"><span data-stu-id="7d79a-183">In Solution Explorer, right-click the project and select **Add** | **New Folder**.</span></span> <span data-ttu-id="7d79a-184">Pojmenujte složku &quot; DTO &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-184">Name the folder &quot;DTOs&quot;.</span></span> <span data-ttu-id="7d79a-185">Přidejte třídu s názvem `BookDto` do složky DTO s následující definicí:</span><span class="sxs-lookup"><span data-stu-id="7d79a-185">Add a class named `BookDto` to the DTOs folder, with the following definition:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample7.cs)]

<span data-ttu-id="7d79a-186">Přidejte další třídu s názvem `BookDetailDto` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-186">Add another class named `BookDetailDto`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample8.cs)]

<span data-ttu-id="7d79a-187">Dále aktualizujte `BooksController` třídu tak, aby vracela `BookDto` instance.</span><span class="sxs-lookup"><span data-stu-id="7d79a-187">Next, update the `BooksController` class to return `BookDto` instances.</span></span> <span data-ttu-id="7d79a-188">Pro projekty instancí do instancí použijeme metodu [Queryable. Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) . `Book` `BookDto`</span><span class="sxs-lookup"><span data-stu-id="7d79a-188">We'll use the [Queryable.Select](https://msdn.microsoft.com/library/system.linq.queryable.select.aspx) method to project `Book` instances to `BookDto` instances.</span></span> <span data-ttu-id="7d79a-189">Zde je aktualizovaný kód pro třídu Controller.</span><span class="sxs-lookup"><span data-stu-id="7d79a-189">Here is the updated code for the controller class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample9.cs)]

> [!NOTE]
> <span data-ttu-id="7d79a-190">Odstranil `PutBook` (a) `PostBook` metody, `DeleteBook` protože nejsou pro tento kurz potřeba.</span><span class="sxs-lookup"><span data-stu-id="7d79a-190">I deleted the `PutBook`, `PostBook`, and `DeleteBook` methods, because they aren't needed for this tutorial.</span></span>

<span data-ttu-id="7d79a-191">Když teď aplikaci spustíte a vyžádáte/API/Books/1, tělo odpovědi by mělo vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="7d79a-191">Now if you run the application and request /api/books/1, the response body should look like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample10.json)]

## <a name="add-route-attributes"></a><span data-ttu-id="7d79a-192">Přidat atributy směrování</span><span class="sxs-lookup"><span data-stu-id="7d79a-192">Add Route Attributes</span></span>

<span data-ttu-id="7d79a-193">Dále převedeme kontroler na použití směrování atributů.</span><span class="sxs-lookup"><span data-stu-id="7d79a-193">Next, we'll convert the controller to use attribute routing.</span></span> <span data-ttu-id="7d79a-194">Nejprve do kontroleru přidejte atribut **RoutePrefix** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-194">First, add a **RoutePrefix** attribute to the controller.</span></span> <span data-ttu-id="7d79a-195">Tento atribut definuje počáteční segmenty identifikátorů URI pro všechny metody tohoto kontroleru.</span><span class="sxs-lookup"><span data-stu-id="7d79a-195">This attribute defines the initial URI segments for all methods on this controller.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample11.cs?highlight=1)]

<span data-ttu-id="7d79a-196">Pak přidejte atributy **[Route]** k akcím kontroleru následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="7d79a-196">Then add **[Route]** attributes to the controller actions, as follows:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample12.cs?highlight=1,7)]

<span data-ttu-id="7d79a-197">Šablona trasy pro každou metodu kontroleru je předponou a řetězcem zadaným v atributu **Route** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-197">The route template for each controller method is the prefix plus the string specified in the **Route** attribute.</span></span> <span data-ttu-id="7d79a-198">Pro `GetBook` metodu zahrnuje šablona trasy parametrizovaný řetězec &quot; {ID: int} &quot; , který odpovídá, pokud segment identifikátoru URI obsahuje celočíselnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="7d79a-198">For the `GetBook` method, the route template includes the parameterized string &quot;{id:int}&quot;, which matches if the URI segment contains an integer value.</span></span>

| <span data-ttu-id="7d79a-199">Metoda</span><span class="sxs-lookup"><span data-stu-id="7d79a-199">Method</span></span> | <span data-ttu-id="7d79a-200">Šablona směrování</span><span class="sxs-lookup"><span data-stu-id="7d79a-200">Route Template</span></span> | <span data-ttu-id="7d79a-201">Příklad identifikátoru URI</span><span class="sxs-lookup"><span data-stu-id="7d79a-201">Example URI</span></span> |
| --- | --- | --- |
| `GetBooks` | <span data-ttu-id="7d79a-202">rozhraní API/knihy</span><span class="sxs-lookup"><span data-stu-id="7d79a-202">"api/books"</span></span> | `http://localhost/api/books` |
| `GetBook` | <span data-ttu-id="7d79a-203">API/Books/{ID: int}</span><span class="sxs-lookup"><span data-stu-id="7d79a-203">"api/books/{id:int}"</span></span> | `http://localhost/api/books/5` |

## <a name="get-book-details"></a><span data-ttu-id="7d79a-204">Získat podrobnosti knihy</span><span class="sxs-lookup"><span data-stu-id="7d79a-204">Get Book Details</span></span>

<span data-ttu-id="7d79a-205">Aby bylo možné získat podrobnosti o knize, odešle klient požadavek GET na `/api/books/{id}/details` , kde *{ID}* je ID knihy.</span><span class="sxs-lookup"><span data-stu-id="7d79a-205">To get book details, the client will send a GET request to `/api/books/{id}/details`, where *{id}* is the ID of the book.</span></span>

<span data-ttu-id="7d79a-206">Do třídy přidejte následující metodu `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-206">Add the following method to the `BooksController` class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample13.cs)]

<span data-ttu-id="7d79a-207">Pokud si vyžádáte `/api/books/1/details` , odpověď vypadá nějak takto:</span><span class="sxs-lookup"><span data-stu-id="7d79a-207">If you request `/api/books/1/details`, the response looks like this:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample14.json)]

## <a name="get-books-by-genre"></a><span data-ttu-id="7d79a-208">Získat knihy podle žánru</span><span class="sxs-lookup"><span data-stu-id="7d79a-208">Get Books By Genre</span></span>

<span data-ttu-id="7d79a-209">Pokud chcete získat seznam knih v konkrétním žánru, pošle klient požadavek GET na `/api/books/genre` , kde *Žánr* je název žánru.</span><span class="sxs-lookup"><span data-stu-id="7d79a-209">To get a list of books in a specific genre, the client will send a GET request to `/api/books/genre`, where *genre* is the name of the genre.</span></span> <span data-ttu-id="7d79a-210">(Například `/api/books/fantasy` .)</span><span class="sxs-lookup"><span data-stu-id="7d79a-210">(For example, `/api/books/fantasy`.)</span></span>

<span data-ttu-id="7d79a-211">Přidejte následující metodu do `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-211">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample15.cs)]

<span data-ttu-id="7d79a-212">Tady definujeme trasu, která obsahuje parametr {Žánr} v šabloně identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="7d79a-212">Here we are defining a route that contains a {genre} parameter in the URI template.</span></span> <span data-ttu-id="7d79a-213">Všimněte si, že webové rozhraní API dokáže rozlišovat tyto dva identifikátory URI a směrovat je do různých metod:</span><span class="sxs-lookup"><span data-stu-id="7d79a-213">Notice that Web API is able to distinguish these two URIs and route them to different methods:</span></span>

`/api/books/1`

`/api/books/fantasy`

<span data-ttu-id="7d79a-214">Důvodem je, že `GetBook` Metoda obsahuje omezení, že segment "ID" musí být celočíselná hodnota:</span><span class="sxs-lookup"><span data-stu-id="7d79a-214">That's because the `GetBook` method includes a constraint that the "id" segment must be an integer value:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample16.cs?highlight=1)]

<span data-ttu-id="7d79a-215">Pokud si vyžádáte/API/Books/fantasy, odpověď vypadá nějak takto:</span><span class="sxs-lookup"><span data-stu-id="7d79a-215">If you request /api/books/fantasy, the response looks like this:</span></span>

`[ { "Title": "Midnight Rain", "Author": "Ralls, Kim", "Genre": "Fantasy" }, { "Title": "Maeve Ascendant", "Author": "Corets, Eva", "Genre": "Fantasy" }, { "Title": "The Sundered Grail", "Author": "Corets, Eva", "Genre": "Fantasy" } ]`

## <a name="get-books-by-author"></a><span data-ttu-id="7d79a-216">Získat knihy podle autora</span><span class="sxs-lookup"><span data-stu-id="7d79a-216">Get Books By Author</span></span>

<span data-ttu-id="7d79a-217">Chcete-li získat seznam knih pro určitého autora, klient odešle požadavek GET na adresu `/api/authors/id/books` , kde *ID* je ID autora.</span><span class="sxs-lookup"><span data-stu-id="7d79a-217">To get a list of a books for a particular author, the client will send a GET request to `/api/authors/id/books`, where *id* is the ID of the author.</span></span>

<span data-ttu-id="7d79a-218">Přidejte následující metodu do `BooksController` .</span><span class="sxs-lookup"><span data-stu-id="7d79a-218">Add the following method to `BooksController`.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample17.cs)]

<span data-ttu-id="7d79a-219">Tento příklad je zajímavý, protože &quot; knihy &quot; se považují za podřízený prostředek &quot; autorů &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-219">This example is interesting because &quot;books&quot; is treated a child resource of &quot;authors&quot;.</span></span> <span data-ttu-id="7d79a-220">Tento model je poměrně společný v rozhraních API RESTful.</span><span class="sxs-lookup"><span data-stu-id="7d79a-220">This pattern is quite common in RESTful APIs.</span></span>

<span data-ttu-id="7d79a-221">Znak tilda (~) v šabloně trasy Přepisuje předponu trasy v atributu **RoutePrefix** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-221">The tilde (~) in the route template overrides the route prefix in the **RoutePrefix** attribute.</span></span>

## <a name="get-books-by-publication-date"></a><span data-ttu-id="7d79a-222">Získat knihy podle data publikování</span><span class="sxs-lookup"><span data-stu-id="7d79a-222">Get Books By Publication Date</span></span>

<span data-ttu-id="7d79a-223">Chcete-li získat seznam knih podle data publikování, klient odešle požadavek GET na `/api/books/date/yyyy-mm-dd` , kde *RRRR-MM-DD* je datum.</span><span class="sxs-lookup"><span data-stu-id="7d79a-223">To get a list of books by publication date, the client will send a GET request to `/api/books/date/yyyy-mm-dd`, where *yyyy-mm-dd* is the date.</span></span>

<span data-ttu-id="7d79a-224">Tady je jeden ze způsobů, jak to provést:</span><span class="sxs-lookup"><span data-stu-id="7d79a-224">Here is one way to do this:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample18.cs)]

<span data-ttu-id="7d79a-225">`{pubdate:datetime}`Parametr je omezený, aby odpovídal hodnotě **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-225">The `{pubdate:datetime}` parameter is constrained to match a **DateTime** value.</span></span> <span data-ttu-id="7d79a-226">Tato funkce funguje, ale ve skutečnosti je to více opravňující než vám.</span><span class="sxs-lookup"><span data-stu-id="7d79a-226">This works, but it's actually more permissive than we'd like.</span></span> <span data-ttu-id="7d79a-227">Například tyto identifikátory URI budou odpovídat i trase:</span><span class="sxs-lookup"><span data-stu-id="7d79a-227">For example, these URIs will also match the route:</span></span>

`/api/books/date/Thu, 01 May 2008`

`/api/books/date/2000-12-16T00:00:00`

<span data-ttu-id="7d79a-228">S povolením těchto identifikátorů URI není nic špatné.</span><span class="sxs-lookup"><span data-stu-id="7d79a-228">There's nothing wrong with allowing these URIs.</span></span> <span data-ttu-id="7d79a-229">Můžete však omezit směrování na konkrétní formát přidáním omezení regulárního výrazu do šablony trasy:</span><span class="sxs-lookup"><span data-stu-id="7d79a-229">However, you can restrict the route to a particular format by adding a regular-expression constraint to the route template:</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample19.cs?highlight=1)]

<span data-ttu-id="7d79a-230">Nyní se budou shodovat pouze kalendářní data ve formě &quot; yyyy-MM-DD &quot; .</span><span class="sxs-lookup"><span data-stu-id="7d79a-230">Now only dates in the form &quot;yyyy-mm-dd&quot; will match.</span></span> <span data-ttu-id="7d79a-231">Všimněte si, že pro ověření, že máme reálné datum, nepoužíváme regulární výraz.</span><span class="sxs-lookup"><span data-stu-id="7d79a-231">Notice that we don't use the regex to validate that we got a real date.</span></span> <span data-ttu-id="7d79a-232">Tato hodnota je zpracována, když se webové rozhraní API pokusí převést segment identifikátoru URI na instanci **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="7d79a-232">That is handled when Web API tries to convert the URI segment into a **DateTime** instance.</span></span> <span data-ttu-id="7d79a-233">Neplatné datum, jako je například ' 2012-47-99 ', nebude převedeno a klient obdrží chybu 404.</span><span class="sxs-lookup"><span data-stu-id="7d79a-233">An invalid date such as '2012-47-99' will fail to be converted, and the client will get a 404 error.</span></span>

<span data-ttu-id="7d79a-234">Můžete také podporovat oddělovač lomítka ( `/api/books/date/yyyy/mm/dd` ) přidáním dalšího atributu **[Route]** s jiným regulárním výrazem.</span><span class="sxs-lookup"><span data-stu-id="7d79a-234">You can also support a slash separator (`/api/books/date/yyyy/mm/dd`) by adding another **[Route]** attribute with a different regex.</span></span>

[!code-html[Main](create-a-rest-api-with-attribute-routing/samples/sample20.html)]

<span data-ttu-id="7d79a-235">Tady je jen malý, ale důležitý detail.</span><span class="sxs-lookup"><span data-stu-id="7d79a-235">There is a subtle but important detail here.</span></span> <span data-ttu-id="7d79a-236">Druhá šablona trasy obsahuje zástupný znak ( \* ) na začátku parametru {pubdate}:</span><span class="sxs-lookup"><span data-stu-id="7d79a-236">The second route template has a wildcard character (\*) at the start of the {pubdate} parameter:</span></span>

[!code-json[Main](create-a-rest-api-with-attribute-routing/samples/sample21.json)]

<span data-ttu-id="7d79a-237">Tím se oznámí směrovacímu modulu, že {pubdate} by se měl shodovat se zbytkem identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="7d79a-237">This tells the routing engine that {pubdate} should match the rest of the URI.</span></span> <span data-ttu-id="7d79a-238">Ve výchozím nastavení je parametr šablony shodný s jedním segmentem identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="7d79a-238">By default, a template parameter matches a single URI segment.</span></span> <span data-ttu-id="7d79a-239">V tomto případě chceme, aby {pubdate} zahrnoval několik segmentů identifikátorů URI:</span><span class="sxs-lookup"><span data-stu-id="7d79a-239">In this case, we want {pubdate} to span several URI segments:</span></span>

`/api/books/date/2013/06/17`

## <a name="controller-code"></a><span data-ttu-id="7d79a-240">Kód kontroleru</span><span class="sxs-lookup"><span data-stu-id="7d79a-240">Controller Code</span></span>

<span data-ttu-id="7d79a-241">Zde je kompletní kód pro třídu BooksController.</span><span class="sxs-lookup"><span data-stu-id="7d79a-241">Here is the complete code for the BooksController class.</span></span>

[!code-csharp[Main](create-a-rest-api-with-attribute-routing/samples/sample22.cs)]

## <a name="summary"></a><span data-ttu-id="7d79a-242">Shrnutí</span><span class="sxs-lookup"><span data-stu-id="7d79a-242">Summary</span></span>

<span data-ttu-id="7d79a-243">Směrování atributů poskytuje větší kontrolu a větší flexibilitu při navrhování identifikátorů URI pro vaše rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="7d79a-243">Attribute routing gives you more control and greater flexibility when designing the URIs for your API.</span></span>
