---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Přidání dat do databáze pomocí migrace Code First | Dokumentace Microsoftu
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59421664"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="718bf-102">Přidání dat do databáze pomocí migrace Code First</span><span class="sxs-lookup"><span data-stu-id="718bf-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="718bf-103">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="718bf-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="718bf-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="718bf-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="718bf-105">V této části použijete [migrace Code First](https://msdn.microsoft.com/data/jj591621) v EF naplnit databázi daty testu.</span><span class="sxs-lookup"><span data-stu-id="718bf-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="718bf-106">Z **nástroje** příkaz **Správce balíčků NuGet**, vyberte **konzoly Správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="718bf-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="718bf-107">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="718bf-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="718bf-108">Tento příkaz přidá složku do projektu s názvem migrace a navíc Configuration.cs ve složce migrace s názvem souboru kódu.</span><span class="sxs-lookup"><span data-stu-id="718bf-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="718bf-109">Otevřete soubor Configuration.cs.</span><span class="sxs-lookup"><span data-stu-id="718bf-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="718bf-110">Přidejte následující **pomocí** příkazu.</span><span class="sxs-lookup"><span data-stu-id="718bf-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="718bf-111">Pak přidejte následující kód, který **Configuration.Seed** metody:</span><span class="sxs-lookup"><span data-stu-id="718bf-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="718bf-112">V okně konzoly Správce balíčků zadejte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="718bf-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="718bf-113">První příkaz vygeneruje kód, který vytvoří databázi a druhý příkaz spustí tento kód.</span><span class="sxs-lookup"><span data-stu-id="718bf-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="718bf-114">Databáze se vytvoří místně, pomocí [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span><span class="sxs-lookup"><span data-stu-id="718bf-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="718bf-115">Prozkoumejte rozhraní API (volitelné)</span><span class="sxs-lookup"><span data-stu-id="718bf-115">Explore the API (Optional)</span></span>

<span data-ttu-id="718bf-116">Stisknutím klávesy F5 spusťte aplikaci v režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="718bf-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="718bf-117">Visual Studio spustí službu IIS Express a spustí webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="718bf-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="718bf-118">Visual Studio pak spustí prohlížeč a otevře domovskou stránku aplikace.</span><span class="sxs-lookup"><span data-stu-id="718bf-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="718bf-119">Když Visual Studio spustí webový projekt, přiřadí číslo portu.</span><span class="sxs-lookup"><span data-stu-id="718bf-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="718bf-120">Na následujícím obrázku je číslo portu 50524.</span><span class="sxs-lookup"><span data-stu-id="718bf-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="718bf-121">Při spuštění aplikace se zobrazí jiné číslo portu.</span><span class="sxs-lookup"><span data-stu-id="718bf-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="718bf-122">Na domovské stránce se implementuje pomocí technologie ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="718bf-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="718bf-123">V horní části stránky je odkaz, který říká "Rozhraní API".</span><span class="sxs-lookup"><span data-stu-id="718bf-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="718bf-124">Tento odkaz vám přináší na stránku nápovědy pro automaticky generované pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="718bf-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="718bf-125">(Další způsob, jakým vygeneruje tuto stránku nápovědy a jak můžete přidat vlastní dokumentaci na stránku, najdete v článku [vytváření stránky nápovědy pro rozhraní ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Kliknutím na dlaždici Nápověda odkazů na stránky zobrazíte podrobnosti o rozhraní API, včetně formát požadavku a odpovědi.</span><span class="sxs-lookup"><span data-stu-id="718bf-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="718bf-126">Rozhraní API umožňuje operace CRUD v databázi.</span><span class="sxs-lookup"><span data-stu-id="718bf-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="718bf-127">Zde je souhrn rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="718bf-127">The following summarizes the API.</span></span>

| <span data-ttu-id="718bf-128">Autoři</span><span class="sxs-lookup"><span data-stu-id="718bf-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="718bf-129">ZÍSKÁNÍ rozhraní api/autorů</span><span class="sxs-lookup"><span data-stu-id="718bf-129">GET api/authors</span></span> | <span data-ttu-id="718bf-130">Získáte všichni autoři.</span><span class="sxs-lookup"><span data-stu-id="718bf-130">Get all authors.</span></span> |
| <span data-ttu-id="718bf-131">Rozhraní api GET/autoři / {id}</span><span class="sxs-lookup"><span data-stu-id="718bf-131">GET api/authors/{id}</span></span> | <span data-ttu-id="718bf-132">Získat Autor podle ID.</span><span class="sxs-lookup"><span data-stu-id="718bf-132">Get an author by ID.</span></span> |
| <span data-ttu-id="718bf-133">PŘÍSPĚVEK/api/autorů</span><span class="sxs-lookup"><span data-stu-id="718bf-133">POST /api/authors</span></span> | <span data-ttu-id="718bf-134">Vytvořte nový Autor.</span><span class="sxs-lookup"><span data-stu-id="718bf-134">Create a new author.</span></span> |
| <span data-ttu-id="718bf-135">Vložení/webové rozhraní API/autoři / {id}</span><span class="sxs-lookup"><span data-stu-id="718bf-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="718bf-136">Aktualizujte existující Autor.</span><span class="sxs-lookup"><span data-stu-id="718bf-136">Update an existing author.</span></span> |
| <span data-ttu-id="718bf-137">ODSTRANIT/webové rozhraní API/autoři / {id}</span><span class="sxs-lookup"><span data-stu-id="718bf-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="718bf-138">Odstraňte Autor.</span><span class="sxs-lookup"><span data-stu-id="718bf-138">Delete an author.</span></span> |

| <span data-ttu-id="718bf-139">Knihy</span><span class="sxs-lookup"><span data-stu-id="718bf-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="718bf-140">ZÍSKAT /api/books</span><span class="sxs-lookup"><span data-stu-id="718bf-140">GET /api/books</span></span> | <span data-ttu-id="718bf-141">Získáte všechny knihy.</span><span class="sxs-lookup"><span data-stu-id="718bf-141">Get all books.</span></span> |
| <span data-ttu-id="718bf-142">ZÍSKAT/webové rozhraní API/books / {id}</span><span class="sxs-lookup"><span data-stu-id="718bf-142">GET /api/books/{id}</span></span> | <span data-ttu-id="718bf-143">Získat knihu podle ID.</span><span class="sxs-lookup"><span data-stu-id="718bf-143">Get a book by ID.</span></span> |
| <span data-ttu-id="718bf-144">Publikovat/api/knihy</span><span class="sxs-lookup"><span data-stu-id="718bf-144">POST /api/books</span></span> | <span data-ttu-id="718bf-145">Vytvoření nového adresáře.</span><span class="sxs-lookup"><span data-stu-id="718bf-145">Create a new book.</span></span> |
| <span data-ttu-id="718bf-146">Vložení/webové rozhraní API/books / {id}</span><span class="sxs-lookup"><span data-stu-id="718bf-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="718bf-147">Aktualizace existujícího adresáře.</span><span class="sxs-lookup"><span data-stu-id="718bf-147">Update an existing book.</span></span> |
| <span data-ttu-id="718bf-148">ODSTRANIT/webové rozhraní API/books / {id}</span><span class="sxs-lookup"><span data-stu-id="718bf-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="718bf-149">Odstraňte knihy.</span><span class="sxs-lookup"><span data-stu-id="718bf-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="718bf-150">Zobrazení databáze (nepovinné)</span><span class="sxs-lookup"><span data-stu-id="718bf-150">View the Database (Optional)</span></span>

<span data-ttu-id="718bf-151">Při spuštění příkazu Update-databázi EF vytváření databáze a volá se, `Seed` metody.</span><span class="sxs-lookup"><span data-stu-id="718bf-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="718bf-152">Když aplikaci spouštíte místně, pomocí EF [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span><span class="sxs-lookup"><span data-stu-id="718bf-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="718bf-153">Databázi můžete zobrazit v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="718bf-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="718bf-154">Z **zobrazení** nabídce vyberte možnost **Průzkumník objektů systému SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="718bf-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="718bf-155">V **připojit k serveru** dialogového okna v **název serveru** textové pole, zadejte "(localdb) \v11.0".</span><span class="sxs-lookup"><span data-stu-id="718bf-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="718bf-156">Nechte **ověřování** možnost "Ověřování Windows".</span><span class="sxs-lookup"><span data-stu-id="718bf-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="718bf-157">Klikněte na **Připojit**.</span><span class="sxs-lookup"><span data-stu-id="718bf-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="718bf-158">Visual Studio na instanci LocalDB se připojí a zobrazuje existujících databází v okně Průzkumník objektů systému SQL Server.</span><span class="sxs-lookup"><span data-stu-id="718bf-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="718bf-159">Lze rozbalit uzly zobrazíte tabulky, které EF vytvořili.</span><span class="sxs-lookup"><span data-stu-id="718bf-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="718bf-160">Chcete-li zobrazit data, klikněte pravým tlačítkem na tabulku a vyberte **Data zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="718bf-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="718bf-161">Následující snímek obrazovky ukazuje výsledky pro tabulku knihy.</span><span class="sxs-lookup"><span data-stu-id="718bf-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="718bf-162">Všimněte si, že EF naplnit databázi daty počáteční hodnoty a tabulka obsahuje cizí klíč do tabulky autoři.</span><span class="sxs-lookup"><span data-stu-id="718bf-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="718bf-163">[Předchozí](part-2.md)
> [další](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="718bf-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
