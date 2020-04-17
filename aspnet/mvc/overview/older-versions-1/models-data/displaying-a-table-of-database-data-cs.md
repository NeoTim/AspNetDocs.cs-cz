---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: Zobrazení tabulky dat databáze (C#) | Dokumenty společnosti Microsoft
author: rick-anderson
description: V tomto tutoriálu předvádím dvě metody zobrazení sady databázových záznamů. I zobrazit dvě metody formátování sadu databázových záznamů v HTML ta ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3fca8ac9e9b4e549ca76ffa282cc03aa4cc50e88
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2020
ms.locfileid: "81542051"
---
# <a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="3676f-104">Zobrazení tabulky databázových dat (C#)</span><span class="sxs-lookup"><span data-stu-id="3676f-104">Displaying a Table of Database Data (C#)</span></span>

<span data-ttu-id="3676f-105">podle [společnosti Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3676f-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3676f-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="3676f-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="3676f-107">V tomto tutoriálu předvádím dvě metody zobrazení sady databázových záznamů.</span><span class="sxs-lookup"><span data-stu-id="3676f-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="3676f-108">Zobrazil(a) jsem dvě metody formátování sady databázových záznamů v tabulce HTML.</span><span class="sxs-lookup"><span data-stu-id="3676f-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="3676f-109">Nejprve vám ukážu, jak můžete naformátovat databázové záznamy přímo v rámci zobrazení.</span><span class="sxs-lookup"><span data-stu-id="3676f-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="3676f-110">Dále jsem ukázat, jak můžete využít částečné při formátování databázových záznamů.</span><span class="sxs-lookup"><span data-stu-id="3676f-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="3676f-111">Cílem tohoto kurzu je vysvětlit, jak můžete zobrazit tabulku HTML databázových dat v ASP.NET aplikace MVC.</span><span class="sxs-lookup"><span data-stu-id="3676f-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="3676f-112">Nejprve se dozvíte, jak pomocí nástrojů generování uživatelského a uživatelského zařízení zahrnuté v sadě Visual Studio generovat zobrazení, které automaticky zobrazuje sadu záznamů.</span><span class="sxs-lookup"><span data-stu-id="3676f-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="3676f-113">Dále se dozvíte, jak použít částečné jako šablonu při formátování záznamů databáze.</span><span class="sxs-lookup"><span data-stu-id="3676f-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="3676f-114">Vytvoření tříd modelu</span><span class="sxs-lookup"><span data-stu-id="3676f-114">Create the Model Classes</span></span>

<span data-ttu-id="3676f-115">Zobrazíme sadu záznamů z tabulky databáze Filmy.</span><span class="sxs-lookup"><span data-stu-id="3676f-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="3676f-116">Databázová tabulka Filmy obsahuje následující sloupce:</span><span class="sxs-lookup"><span data-stu-id="3676f-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>

| <span data-ttu-id="3676f-117">**Název sloupce**</span><span class="sxs-lookup"><span data-stu-id="3676f-117">**Column Name**</span></span> | <span data-ttu-id="3676f-118">**Typ dat**</span><span class="sxs-lookup"><span data-stu-id="3676f-118">**Data Type**</span></span> | <span data-ttu-id="3676f-119">**Povolit hodnoty Null**</span><span class="sxs-lookup"><span data-stu-id="3676f-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3676f-120">ID</span><span class="sxs-lookup"><span data-stu-id="3676f-120">Id</span></span> | <span data-ttu-id="3676f-121">Int</span><span class="sxs-lookup"><span data-stu-id="3676f-121">Int</span></span> | <span data-ttu-id="3676f-122">False</span><span class="sxs-lookup"><span data-stu-id="3676f-122">False</span></span> |
| <span data-ttu-id="3676f-123">Nadpis</span><span class="sxs-lookup"><span data-stu-id="3676f-123">Title</span></span> | <span data-ttu-id="3676f-124">Nvarchar(200)</span><span class="sxs-lookup"><span data-stu-id="3676f-124">Nvarchar(200)</span></span> | <span data-ttu-id="3676f-125">False</span><span class="sxs-lookup"><span data-stu-id="3676f-125">False</span></span> |
| <span data-ttu-id="3676f-126">Ředitel</span><span class="sxs-lookup"><span data-stu-id="3676f-126">Director</span></span> | <span data-ttu-id="3676f-127">NVarchar(50)</span><span class="sxs-lookup"><span data-stu-id="3676f-127">NVarchar(50)</span></span> | <span data-ttu-id="3676f-128">False</span><span class="sxs-lookup"><span data-stu-id="3676f-128">False</span></span> |
| <span data-ttu-id="3676f-129">Datum zveřejnění</span><span class="sxs-lookup"><span data-stu-id="3676f-129">DateReleased</span></span> | <span data-ttu-id="3676f-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="3676f-130">DateTime</span></span> | <span data-ttu-id="3676f-131">False</span><span class="sxs-lookup"><span data-stu-id="3676f-131">False</span></span> |

<span data-ttu-id="3676f-132">Aby bylo možné reprezentovat tabulky Filmy v naší ASP.NET aplikace MVC, musíme vytvořit třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="3676f-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="3676f-133">V tomto kurzu používáme Microsoft Entity Framework k vytvoření našich tříd modelu.</span><span class="sxs-lookup"><span data-stu-id="3676f-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="3676f-134">V tomto kurzu používáme Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="3676f-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="3676f-135">Je však důležité si uvědomit, že můžete použít celou řadu různých technologií pro interakci s databází z ASP.NET aplikace MVC, včetně LINQ na SQL, NHibernate nebo ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="3676f-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="3676f-136">Průvodce datovým modelem entity spusťte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="3676f-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="3676f-137">Klepněte pravým tlačítkem myši na složku Modely v okně Průzkumník řešení a vyberte možnost nabídky **Přidat, Novou položku**.</span><span class="sxs-lookup"><span data-stu-id="3676f-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="3676f-138">Vyberte kategorii **Data** a vyberte šablonu **ADO.NET datového modelu entity.**</span><span class="sxs-lookup"><span data-stu-id="3676f-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="3676f-139">Dejte svému datovému modelu název *MoviesDBModel.edmx* a klikněte na tlačítko **Přidat.**</span><span class="sxs-lookup"><span data-stu-id="3676f-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="3676f-140">Po klepnutí na tlačítko Přidat se zobrazí Průvodce datovým modelem entity (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="3676f-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="3676f-141">Průvodce dokončujte následujícím postupem:</span><span class="sxs-lookup"><span data-stu-id="3676f-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="3676f-142">V kroku **Zvolit obsah modelu** vyberte volbu Generovat z **databáze.**</span><span class="sxs-lookup"><span data-stu-id="3676f-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="3676f-143">V kroku **Zvolit datové připojení** použijte datové připojení *MoviesDB.mdf* a název *MoviesDBEntities* pro nastavení připojení.</span><span class="sxs-lookup"><span data-stu-id="3676f-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="3676f-144">Klikněte na tlačítko **Další.**</span><span class="sxs-lookup"><span data-stu-id="3676f-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="3676f-145">V kroku **Zvolit databázové objekty** rozbalte uzel Tabulky a vyberte tabulku Filmy.</span><span class="sxs-lookup"><span data-stu-id="3676f-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="3676f-146">Zadejte *modely* oboru názvů a klepněte na tlačítko **Dokončit.**</span><span class="sxs-lookup"><span data-stu-id="3676f-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="3676f-147">[![Vytváření tříd LINQ na SQL](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="3676f-148">**Obrázek 01**: Vytvoření tříd LINQ na SQL[(Klepnutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>

<span data-ttu-id="3676f-149">Po dokončení Průvodce datovým modelem entity se otevře Návrhář modelu dat entity.</span><span class="sxs-lookup"><span data-stu-id="3676f-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="3676f-150">Návrhář by měl zobrazit entitu Filmy (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="3676f-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="3676f-151">[![Návrhář datového modelu entity](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="3676f-152">**Obrázek 02**: Návrhář datového modelu entity[(Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>

<span data-ttu-id="3676f-153">Než budeme pokračovat, musíme udělat jednu změnu.</span><span class="sxs-lookup"><span data-stu-id="3676f-153">We need to make one change before we continue.</span></span> <span data-ttu-id="3676f-154">Průvodce daty entit generuje třídu modelu s názvem *Filmy,* která představuje databázovou tabulku Filmy.</span><span class="sxs-lookup"><span data-stu-id="3676f-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="3676f-155">Vzhledem k tomu, že budeme používat Filmy třídy představují konkrétní film, musíme upravit název třídy *být film* místo *filmy* (jednotné číslo spíše než množné číslo).</span><span class="sxs-lookup"><span data-stu-id="3676f-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="3676f-156">Poklepejte na název třídy na povrchu návrháře a změňte název třídy z Filmy na Film.</span><span class="sxs-lookup"><span data-stu-id="3676f-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="3676f-157">Po provedení této změny vygenerujte třídu Movie klepnutím na tlačítko **Uložit** (ikona diskety).</span><span class="sxs-lookup"><span data-stu-id="3676f-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="3676f-158">Vytvoření ovladače pro filmy</span><span class="sxs-lookup"><span data-stu-id="3676f-158">Create the Movies Controller</span></span>

<span data-ttu-id="3676f-159">Teď, když máme způsob, jak reprezentovat naše databázové záznamy, můžeme vytvořit řadič, který vrací sbírku filmů.</span><span class="sxs-lookup"><span data-stu-id="3676f-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="3676f-160">V okně Průzkumník řešení sady Visual Studio klepněte pravým tlačítkem myši na složku Řadiče a vyberte možnost nabídky **Přidat, Řadič** (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="3676f-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="3676f-161">[![Nabídka Přidat ovladač](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="3676f-162">**Obrázek 03**: Nabídka Přidat ovladač[(Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>

<span data-ttu-id="3676f-163">Po zobrazení dialogového okna **Přidat řadič** zadejte název řadiče MovieController (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="3676f-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="3676f-164">Kliknutím na tlačítko **Přidat** přidejte nový ovladač.</span><span class="sxs-lookup"><span data-stu-id="3676f-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="3676f-165">[![Dialogové okno Přidat řadič](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="3676f-166">**Obrázek 04**: Dialogové okno Přidat ovladač([Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>

<span data-ttu-id="3676f-167">Musíme upravit akci Index() vystavenou řadičem filmu tak, aby vrátil sadu databázových záznamů.</span><span class="sxs-lookup"><span data-stu-id="3676f-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="3676f-168">Upravte řadič tak, aby vypadal jako řadič v výpisu 1.</span><span class="sxs-lookup"><span data-stu-id="3676f-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="3676f-169">**Výpis 1 – Řadiče\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="3676f-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="3676f-170">V výpisu 1, MoviesDBEntities třída se používá k reprezentaci databáze MoviesDB.</span><span class="sxs-lookup"><span data-stu-id="3676f-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="3676f-171">Chcete-li použít tuto třídu, je třeba importovat obor názvů MvcApplication1.Models takto:</span><span class="sxs-lookup"><span data-stu-id="3676f-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="3676f-172">pomocí MvcApplication1.Models;</span><span class="sxs-lookup"><span data-stu-id="3676f-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="3676f-173">Entity *výrazu. MovieSet.ToList()* vrátí sadu všech filmů z tabulky databáze Filmy.</span><span class="sxs-lookup"><span data-stu-id="3676f-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="3676f-174">Vytvoření zobrazení</span><span class="sxs-lookup"><span data-stu-id="3676f-174">Create the View</span></span>

<span data-ttu-id="3676f-175">Nejjednodušší způsob, jak zobrazit sadu databázových záznamů v tabulce HTML, je využít možnosti uživatelského prostředí poskytovaného sadou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3676f-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="3676f-176">Vytvořte si aplikaci výběrem možnosti nabídky **Sestavení, Sestavení řešení**.</span><span class="sxs-lookup"><span data-stu-id="3676f-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="3676f-177">Před otevřením dialogového okna **Přidat zobrazení** je nutné vytvořit aplikaci, jinak se vaše třídy dat v dialogovém okně nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="3676f-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="3676f-178">Klikněte pravým tlačítkem myši na akci Index() a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 5).</span><span class="sxs-lookup"><span data-stu-id="3676f-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="3676f-179">[![Přidání zobrazení](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="3676f-180">**Obrázek 05**: Přidání zobrazení[(Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>

<span data-ttu-id="3676f-181">V dialogovém okně **Přidat zobrazení** zaškrtněte políčko Vytvořit **zobrazení silného typu**.</span><span class="sxs-lookup"><span data-stu-id="3676f-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="3676f-182">Vyberte třídu Film jako **třídu dat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="3676f-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="3676f-183">Jako obsah **zobrazení** vyberte *Seznam* (viz obrázek 6).</span><span class="sxs-lookup"><span data-stu-id="3676f-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="3676f-184">Výběrem těchto možností se vygeneruje zobrazení silného typu, které zobrazí seznam filmů.</span><span class="sxs-lookup"><span data-stu-id="3676f-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="3676f-185">[![Dialogové okno Přidat zobrazení](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="3676f-186">**Obrázek 06**: Dialogové okno Přidat zobrazení([Kliknutím zobrazíte obrázek v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>

<span data-ttu-id="3676f-187">Po klepnutí na tlačítko **Přidat** se automaticky vygeneruje zobrazení v seznamu 2.</span><span class="sxs-lookup"><span data-stu-id="3676f-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="3676f-188">Toto zobrazení obsahuje kód potřebný k iterátu prostřednictvím kolekce filmů a zobrazení jednotlivých vlastností filmu.</span><span class="sxs-lookup"><span data-stu-id="3676f-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="3676f-189">**Výpis 2 – Zobrazení\Film\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="3676f-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="3676f-190">Aplikaci můžete spustit výběrem možnosti nabídky **Ladění, Spustit ladění** (nebo stisknutím klávesy F5).</span><span class="sxs-lookup"><span data-stu-id="3676f-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="3676f-191">Spuštění aplikace spustí aplikaci Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="3676f-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="3676f-192">Pokud přejdete na adresu URL /Movie, zobrazí se stránka na obrázku 7.</span><span class="sxs-lookup"><span data-stu-id="3676f-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="3676f-193">[![Tabulka filmů](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="3676f-194">**Obrázek 07**: Tabulka[filmů(Klikněte pro zobrazení obrázku v plné velikosti)](displaying-a-table-of-database-data-cs/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="3676f-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>

<span data-ttu-id="3676f-195">Pokud se vám nelíbí nic o vzhledu mřížky databázových záznamů na obrázku 7, pak můžete jednoduše upravit zobrazení indexu.</span><span class="sxs-lookup"><span data-stu-id="3676f-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="3676f-196">Můžete například změnit hlavičku *DateReleased* na *Datum vydání* úpravou zobrazení rejstříku.</span><span class="sxs-lookup"><span data-stu-id="3676f-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="3676f-197">Vytvoření šablony s částečným</span><span class="sxs-lookup"><span data-stu-id="3676f-197">Create a Template with a Partial</span></span>

<span data-ttu-id="3676f-198">Když se zobrazení příliš zkomplikuje, je vhodné začít rozdělit zobrazení na částečné.</span><span class="sxs-lookup"><span data-stu-id="3676f-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="3676f-199">Použití částečných částek usnadňuje pochopení a údržbu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="3676f-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="3676f-200">Vytvoříme částečný, který můžeme použít jako šablonu pro formátování každého z záznamů filmové databáze.</span><span class="sxs-lookup"><span data-stu-id="3676f-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="3676f-201">Chcete-li vytvořit částečné, postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="3676f-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="3676f-202">Klepněte pravým tlačítkem myši na složku Zobrazení\Film a vyberte možnost nabídky **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="3676f-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="3676f-203">Zaškrtněte políčko *Vytvořit částečné zobrazení (.ascx).*</span><span class="sxs-lookup"><span data-stu-id="3676f-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="3676f-204">Pojmenujte částečnou *movietemplate*.</span><span class="sxs-lookup"><span data-stu-id="3676f-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="3676f-205">Zaškrtněte políčko **Vytvořit zobrazení silného typu**.</span><span class="sxs-lookup"><span data-stu-id="3676f-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="3676f-206">Jako *třídu dat zobrazení*vyberte Vyvěšení .</span><span class="sxs-lookup"><span data-stu-id="3676f-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="3676f-207">Jako obsah *zobrazení*vyberte Možnost Prázdné .</span><span class="sxs-lookup"><span data-stu-id="3676f-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="3676f-208">Kliknutím na tlačítko **Přidat** přidáte částečné část projektu.</span><span class="sxs-lookup"><span data-stu-id="3676f-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="3676f-209">Po dokončení těchto kroků upravte šablonu MovieTemplate tak, aby vypadala jako Výpis 3.</span><span class="sxs-lookup"><span data-stu-id="3676f-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="3676f-210">**Výpis 3 – Zobrazení\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="3676f-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="3676f-211">Částečné v výpisu 3 obsahuje šablonu pro jeden řádek záznamů.</span><span class="sxs-lookup"><span data-stu-id="3676f-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="3676f-212">Upravené zobrazení indexu v seznamu 4 používá částečné movietemplate.</span><span class="sxs-lookup"><span data-stu-id="3676f-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="3676f-213">**Výpis 4 – Zobrazení\Film\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="3676f-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="3676f-214">Zobrazení v výpisu 4 obsahuje foreach smyčky, která iterates přes všechny filmy.</span><span class="sxs-lookup"><span data-stu-id="3676f-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="3676f-215">Pro každý film se k formátování filmu používá šablona MovieTemplate.</span><span class="sxs-lookup"><span data-stu-id="3676f-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="3676f-216">MovieTemplate je vykreslen voláním RenderPartial() pomocné metody.</span><span class="sxs-lookup"><span data-stu-id="3676f-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="3676f-217">Upravené zobrazení indexu vykreslí stejnou tabulku HTML databázových záznamů.</span><span class="sxs-lookup"><span data-stu-id="3676f-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="3676f-218">Pohled byl však značně zjednodušen.</span><span class="sxs-lookup"><span data-stu-id="3676f-218">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="3676f-219">RenderPartial() Metoda se liší od většiny jiných pomocných metod, protože nevrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="3676f-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="3676f-220">Proto je nutné volat RenderPartial() &lt;metoda pomocí % Html.RenderPartial(); %&gt; místo &lt;%= Html.RenderPartial(); %&gt;.</span><span class="sxs-lookup"><span data-stu-id="3676f-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="3676f-221">Souhrn</span><span class="sxs-lookup"><span data-stu-id="3676f-221">Summary</span></span>

<span data-ttu-id="3676f-222">Cílem tohoto kurzu bylo vysvětlit, jak lze zobrazit sadu databázových záznamů v tabulce HTML.</span><span class="sxs-lookup"><span data-stu-id="3676f-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="3676f-223">Nejprve jste se naučili, jak vrátit sadu záznamů databáze z akce kontroleru s využitím rozhraní Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="3676f-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="3676f-224">Dále jste se naučili používat generování uživatelského přilnavého zařízení sady Visual Studio ke generování zobrazení, které automaticky zobrazuje kolekci položek.</span><span class="sxs-lookup"><span data-stu-id="3676f-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="3676f-225">Nakonec jste se naučili, jak zjednodušit zobrazení využitím částečné.</span><span class="sxs-lookup"><span data-stu-id="3676f-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="3676f-226">Naučili jste se používat částečné jako šablonu, takže můžete formátovat každý záznam databáze.</span><span class="sxs-lookup"><span data-stu-id="3676f-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3676f-227">[Předchozí](creating-model-classes-with-linq-to-sql-cs.md)
> [další](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="3676f-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>
