---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Kurz: Vytvořte webovou aplikaci a datové modely pro EF Database First s ASP.NET MVC'
description: Tento kurz se zaměřuje na vytvoření webové aplikace a generování datové modely založené na databázových tabulek.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 481a0ee9b19e5d35d736b2cc937a124900bce446
ms.sourcegitcommit: 289e051cc8a90e8f7127e239fda73047bde4de12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/25/2019
ms.locfileid: "58426130"
---
# <a name="tutorial-create-the-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="af71d-103">Kurz: Vytvořte webovou aplikaci a datové modely pro EF Database First s ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="af71d-103">Tutorial: Create the the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="af71d-104">Pomocí generování uživatelského rozhraní ASP.NET, MVC a Entity Framework, můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi.</span><span class="sxs-lookup"><span data-stu-id="af71d-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="af71d-105">V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který umožňuje uživatelům zobrazit, upravit, vytvořit a odstranit data, která se nachází v databázové tabulce.</span><span class="sxs-lookup"><span data-stu-id="af71d-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="af71d-106">Generovaný kód odpovídá sloupců v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="af71d-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="af71d-107">Tento kurz se zaměřuje na vytvoření webové aplikace a generování datové modely založené na databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="af71d-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="af71d-108">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="af71d-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af71d-109">Vytvoření webové aplikace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="af71d-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="af71d-110">Generovat modelů</span><span class="sxs-lookup"><span data-stu-id="af71d-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af71d-111">Požadavky</span><span class="sxs-lookup"><span data-stu-id="af71d-111">Prerequisites</span></span>

* [<span data-ttu-id="af71d-112">Začínáme s Entity Framework 6 Database First pomocí MVC 5</span><span class="sxs-lookup"><span data-stu-id="af71d-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="af71d-113">Vytvoření webové aplikace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="af71d-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="af71d-114">V nové řešení nebo do stejného řešení jako databázového projektu vytvořte nový projekt v sadě Visual Studio a vyberte **webová aplikace ASP.NET** šablony.</span><span class="sxs-lookup"><span data-stu-id="af71d-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="af71d-115">Pojmenujte projekt **ContosoSite**.</span><span class="sxs-lookup"><span data-stu-id="af71d-115">Name the project **ContosoSite**.</span></span>

![Vytvoření projektu](creating-the-web-application/_static/image1.png)

<span data-ttu-id="af71d-117">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="af71d-117">Click **OK**.</span></span>

<span data-ttu-id="af71d-118">V okně Nový projekt ASP.NET, vyberte **MVC** šablony.</span><span class="sxs-lookup"><span data-stu-id="af71d-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="af71d-119">Můžete vymazat **hostovat v cloudu** možnost prozatím, protože budete nasazovat aplikaci do cloudu později.</span><span class="sxs-lookup"><span data-stu-id="af71d-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="af71d-120">Klikněte na tlačítko **OK** k vytvoření aplikace.</span><span class="sxs-lookup"><span data-stu-id="af71d-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="af71d-121">Projekt je vytvořen s výchozí soubory a složky.</span><span class="sxs-lookup"><span data-stu-id="af71d-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="af71d-122">V tomto kurzu budete používat Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="af71d-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="af71d-123">Verze rozhraní Entity Framework můžete zkontrolovat ve vašem projektu prostřednictvím okna spravovat balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="af71d-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="af71d-124">V případě potřeby aktualizujte na verzi rozhraní Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="af71d-124">If necessary, update your version of Entity Framework.</span></span>

![Zobrazit verze](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="af71d-126">Generovat modelů</span><span class="sxs-lookup"><span data-stu-id="af71d-126">Generate the models</span></span>

<span data-ttu-id="af71d-127">Modely Entity Framework teď vytvoříte z databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="af71d-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="af71d-128">Tyto modely jsou třídy, které budete používat pro práci s daty.</span><span class="sxs-lookup"><span data-stu-id="af71d-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="af71d-129">Každý model zrcadlí tabulky v databázi a obsahuje vlastnosti, které odpovídají sloupcům v tabulce.</span><span class="sxs-lookup"><span data-stu-id="af71d-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="af71d-130">Klikněte pravým tlačítkem myši **modely** a pak zvolte položku **přidat** a **nová položka**.</span><span class="sxs-lookup"><span data-stu-id="af71d-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="af71d-131">V okně Přidat novou položku vyberte **Data** v levém podokně a **datový Model Entity ADO.NET** z možností v prostředním podokně.</span><span class="sxs-lookup"><span data-stu-id="af71d-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="af71d-132">Pojmenujte nový soubor modelu **ContosoModel**.</span><span class="sxs-lookup"><span data-stu-id="af71d-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="af71d-133">Klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="af71d-133">Click **Add**.</span></span>

<span data-ttu-id="af71d-134">V Průvodci modelem Entity Data vyberte **EF designeru z databáze**.</span><span class="sxs-lookup"><span data-stu-id="af71d-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="af71d-135">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="af71d-135">Click **Next**.</span></span>

<span data-ttu-id="af71d-136">Pokud máte připojení k databázi definována v rámci vývojového prostředí, může se zobrazit jeden z těchto připojení předem vybraná.</span><span class="sxs-lookup"><span data-stu-id="af71d-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="af71d-137">Chcete vytvořit nové připojení k databázi, kterou jste vytvořili v první části tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="af71d-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="af71d-138">Klikněte na tlačítko **nové připojení** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="af71d-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="af71d-139">V okně Vlastnosti připojení zadat název místního serveru, kde byla vytvořena databáze (v tomto případě **(localdb) \ProjectsV13**).</span><span class="sxs-lookup"><span data-stu-id="af71d-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="af71d-140">Po zadání názvu serveru, vyberte z dostupných databází ContosoUniversityData.</span><span class="sxs-lookup"><span data-stu-id="af71d-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![nastavit vlastnosti připojení](creating-the-web-application/_static/image8.png)

<span data-ttu-id="af71d-142">Klikněte na **OK**.</span><span class="sxs-lookup"><span data-stu-id="af71d-142">Click **OK**.</span></span>

<span data-ttu-id="af71d-143">Vlastnosti správné připojení se teď zobrazují.</span><span class="sxs-lookup"><span data-stu-id="af71d-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="af71d-144">Můžete použít výchozí název připojení v souboru Web.Config.</span><span class="sxs-lookup"><span data-stu-id="af71d-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="af71d-145">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="af71d-145">Click **Next**.</span></span>

<span data-ttu-id="af71d-146">Vyberte nejnovější verzi rozhraní Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="af71d-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="af71d-147">Klikněte na **Další**.</span><span class="sxs-lookup"><span data-stu-id="af71d-147">Click **Next**.</span></span>

<span data-ttu-id="af71d-148">Vyberte **tabulky** ke generování modely pro všechny tři tabulky.</span><span class="sxs-lookup"><span data-stu-id="af71d-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="af71d-149">Klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="af71d-149">Click **Finish**.</span></span>

<span data-ttu-id="af71d-150">Pokud se zobrazí upozornění zabezpečení, vyberte **OK** pokračoval šablony.</span><span class="sxs-lookup"><span data-stu-id="af71d-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="af71d-151">Modely se generují z databázové tabulky a diagramu se zobrazí, který ukazuje vlastnosti a vztahy mezi tabulkami.</span><span class="sxs-lookup"><span data-stu-id="af71d-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![Diagram modelu](creating-the-web-application/_static/image11.png)

<span data-ttu-id="af71d-153">Složku modely nyní obsahuje mnoho nových souborů související s modely, které byly generovány z databáze.</span><span class="sxs-lookup"><span data-stu-id="af71d-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="af71d-154">**ContosoModel.Context.cs** soubor obsahuje třídu, která je odvozena z **DbContext** třídy a poskytuje vlastnosti pro každou třídu modelu, odpovídající do databázové tabulky.</span><span class="sxs-lookup"><span data-stu-id="af71d-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="af71d-155">**Course.cs**, **Enrollment.cs**, a **Student.cs** soubory obsahují, které představují tabulky databáze třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="af71d-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="af71d-156">Třídy kontextu a tříd modelu bude používat při práci s generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="af71d-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="af71d-157">Než budete pokračovat s tímto kurzem, sestavte projekt.</span><span class="sxs-lookup"><span data-stu-id="af71d-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="af71d-158">V další části bude generovat kód založený na datové modely, ale, že část nebude fungovat, pokud projekt nebyl sestaven.</span><span class="sxs-lookup"><span data-stu-id="af71d-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af71d-159">Další kroky</span><span class="sxs-lookup"><span data-stu-id="af71d-159">Next steps</span></span>

<span data-ttu-id="af71d-160">V tomto kurzu se naučíte:</span><span class="sxs-lookup"><span data-stu-id="af71d-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af71d-161">Vytvoření webové aplikace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="af71d-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="af71d-162">Vygeneruje modely</span><span class="sxs-lookup"><span data-stu-id="af71d-162">Generated the models</span></span>

<span data-ttu-id="af71d-163">Pokračujte k dalšímu kurzu se naučíte vytvořit vygenerování kódu založeném na datové modely.</span><span class="sxs-lookup"><span data-stu-id="af71d-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="af71d-164">Generování zobrazení</span><span class="sxs-lookup"><span data-stu-id="af71d-164">Generating views</span></span>](generating-views.md)
