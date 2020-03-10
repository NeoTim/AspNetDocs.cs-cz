---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543748"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="91b8a-104">Přístup k datům modelu z kontroleru</span><span class="sxs-lookup"><span data-stu-id="91b8a-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="91b8a-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="91b8a-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="91b8a-106">Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="91b8a-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="91b8a-107">Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.</span><span class="sxs-lookup"><span data-stu-id="91b8a-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="91b8a-108">Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="91b8a-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="91b8a-109">V této části vytvoříme novou třídu MoviesController a napíšeme kód, který načte data z filmu a zobrazí se zpátky do prohlížeče pomocí šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="91b8a-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="91b8a-110">Klikněte pravým tlačítkem na složku Controllers a vytvořte novou MoviesController.</span><span class="sxs-lookup"><span data-stu-id="91b8a-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="91b8a-111">[Přidat kontroler ![](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="91b8a-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="91b8a-112">Tím se vytvoří nový soubor "MoviesController.cs" pod naší \Controllers složkou v rámci našeho projektu.</span><span class="sxs-lookup"><span data-stu-id="91b8a-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="91b8a-113">Pojďme aktualizovat MovieController, aby se načetl seznam filmů z naší nově vyplněné databáze.</span><span class="sxs-lookup"><span data-stu-id="91b8a-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="91b8a-114">Provádíme dotaz LINQ, abychom načetli jenom filmy vydané po léto 1984.</span><span class="sxs-lookup"><span data-stu-id="91b8a-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="91b8a-115">K vygenerování tohoto seznamu videí budete potřebovat šablonu zobrazení, takže v metodě klikněte pravým tlačítkem myši a vyberte Přidat zobrazení a vytvořte ho.</span><span class="sxs-lookup"><span data-stu-id="91b8a-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="91b8a-116">V dialogovém okně Přidat zobrazení oznamujeme, že předáváme seznam&lt;filmy. Models. Movie&gt; do naší šablony zobrazení.</span><span class="sxs-lookup"><span data-stu-id="91b8a-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="91b8a-117">Na rozdíl od předchozích časů jsme použili dialog Přidat zobrazení a rozhodli jste se vytvořit "prázdnou" šablonu. Tento čas oznamujeme, že chceme, aby se v aplikaci Visual Studio automaticky vytvořila šablona zobrazení pro nás s nějakým výchozím obsahem.</span><span class="sxs-lookup"><span data-stu-id="91b8a-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="91b8a-118">Provedeme to tak, že v rozevírací nabídce zobrazení obsahu vyberete položku seznam.</span><span class="sxs-lookup"><span data-stu-id="91b8a-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="91b8a-119">Mějte na paměti, že pokud máte vytvořenou novou třídu, budete muset aplikaci zkompilovat, aby se zobrazila v dialogovém okně Přidat zobrazení.</span><span class="sxs-lookup"><span data-stu-id="91b8a-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![Přidat zobrazení](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="91b8a-121">Klikněte na tlačítko Přidat a systém automaticky vygeneruje kód pro zobrazení pro nás, který zobrazí náš seznam filmů.</span><span class="sxs-lookup"><span data-stu-id="91b8a-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="91b8a-122">To je dobrý čas ke změně &lt;H2&gt; nadpisu na něco, co se stalo s zobrazením Hello World.</span><span class="sxs-lookup"><span data-stu-id="91b8a-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="91b8a-123">[Filmy ![– Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="91b8a-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="91b8a-124">Spusťte aplikaci a na panelu Adresa navštivte/Movies.</span><span class="sxs-lookup"><span data-stu-id="91b8a-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="91b8a-125">Nyní jsme načetli data z databáze pomocí základního dotazu v rámci kontroleru a vrátili data do zobrazení, které ví o videu.</span><span class="sxs-lookup"><span data-stu-id="91b8a-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="91b8a-126">Toto zobrazení se pak roztočí seznamem filmů a vytvoří tabulku dat pro nás.</span><span class="sxs-lookup"><span data-stu-id="91b8a-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="91b8a-127">[![seznam filmů – Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="91b8a-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="91b8a-128">V této aplikaci nebudeme implementovat funkce Edit, Details a DELETE, takže nepotřebujeme výchozí odkazy, které vytvořila šablona generování uživatelského rozhraní pro nás.</span><span class="sxs-lookup"><span data-stu-id="91b8a-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="91b8a-129">Otevřete soubor/Movies/Index.aspx a odeberte ho.</span><span class="sxs-lookup"><span data-stu-id="91b8a-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="91b8a-130">Tady je zdrojový kód, který by naše aktualizovaná šablona zobrazení vypadala po provedení těchto změn:</span><span class="sxs-lookup"><span data-stu-id="91b8a-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="91b8a-131">Vytváříme odkazy, které nepotřebujeme, takže je pro tento příklad odstraníme.</span><span class="sxs-lookup"><span data-stu-id="91b8a-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="91b8a-132">Náš odkaz pro vytváření nových odkazů budeme uchovávat, i když to bude dál!</span><span class="sxs-lookup"><span data-stu-id="91b8a-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="91b8a-133">V našem příkladu vypadá naše aplikace s odebraným sloupcem.</span><span class="sxs-lookup"><span data-stu-id="91b8a-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="91b8a-134">[![seznam filmů – Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="91b8a-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="91b8a-135">Teď máme jednoduchý seznam našich filmových dat.</span><span class="sxs-lookup"><span data-stu-id="91b8a-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="91b8a-136">Pokud ale klikneme na odkaz vytvořit nový, zobrazí se chyba, protože se nepřipojí.</span><span class="sxs-lookup"><span data-stu-id="91b8a-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="91b8a-137">Pojďme implementovat metodu akce vytvoření a umožnit uživateli zadat nové filmy v naší databázi.</span><span class="sxs-lookup"><span data-stu-id="91b8a-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="91b8a-138">[Předchozí](getting-started-with-mvc-part4.md)
> [Další](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="91b8a-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
